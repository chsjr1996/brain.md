
```js
import cluster from 'node:cluster';
import os from 'node:os';

const osCPUs = os.cpus().length;
const isProduction = process.env.NODE_ENV === 'prod';

export class AppCluster {
	static clusterize(cb: () => void): void {
		if (isProduction && cluster.isPrimary) {
			console.info(
				`Primary cluster "${process.pid}" is running!`,
			);

			for (let i = 0; i < osCPUs; i++) {
				cluster.fork();
			}

			cluster.on('online', (worker) => {
				console.info(`Worker ${worker} is online.`);
			});

			cluster.on('exit', (worker, code) => {
				console.warn(`Worker ${worker} has exited with code "${code}".`);
				cluster.fork();
			});
		} else {
			cb();
		}
	}
}
```
> app-cluster.ts

```js
import { AppCluster } from './app-cluster';

async function bootstrap() {
	const app = await NestFactory.create(AppModule);

	const allowedHeaders = [
		'Content-Type',
		'Accept',
		'Authorization'	,
		'Access-Control-Allow-Origin',
	];

	app.enableShutdownHooks();
	app.enableCors({
		origin: '*',
		credentials: true,
		methods: 'GET,PUT,POST',
		allowedHeaders: allowedHeaders.join(','),
	});

	await app.listen(3333);
}

AppCluster.clusterize(bootstrap);
```
> main.ts