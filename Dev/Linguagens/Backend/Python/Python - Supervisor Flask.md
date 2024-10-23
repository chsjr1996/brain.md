Para executar um servidor web de uma aplicação Python Flask utilizando o Gunicorn e o Supervisor, siga estes passos:

## Arquivo supervisor
Crie um arquivo no diretório `/etc/supervisor/conf.d` com a extensão `.conf` contendo as seguintes linhas:
```
[program:flaskapp]
directory=/var/www/html/flaskapp command=/var/www/html/flaskapp/venv/bin/gunicorn -w 4 -b 127.0.0.1:5000 file:function
autostart=true
autorestart=true
stderr_logfile=/var/log/flaskapp.err.log
stdout_logfile=/var/log/flaskapp.out.log
environment=PATH="/var/www/html/flaskapp/venv/bin",VIRTUAL_ENV="/var/www/html/flaskapp/venv",PYTHONPATH="/var/www/html/flaskapp/file"
```

> [!quote] Observações
> O trecho `file:function` se refere ao nome do arquivo principal da aplicação python e a função que executa a aplicação em si, podendo ser `main:app` ou `app:app`, etc...
> 
> O parâmetro `-w` se refere a quantidade de *workers* (ou processos) que serão utilizados para lidar com as requisições. Aumentar o número de *workers* aumenta a capacidade de lidar com requisições concorrentes, porém consome mais o uso da CPU, devendo respeitar a quantidade de núcleos do servidor ou usando a seguinte fórmula `workers = (2 x CPU cores) +1`.
> 
> **Atenção:** use o `gunicorn` de dentro do "venv" para garantir que a aplicação será executada com as devidas bibliotecas do projeto.

## Arquivo do nginx
```
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	server_name api.flask.com;

	location / {
		proxy_pass http://127.0.0.1:5000;
		proxy_set_header Host $host
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-Forwarded-Proto $scheme;
		try_files $uri $uri/ =404;
	}
}
```

---

> [!NOTE] Referências
> [Medium - Deploy flask app with nginx using gunicorn and supervisor](https://medium.com/ymedialabs-innovation/deploy-flask-app-with-nginx-using-gunicorn-and-supervisor-d7a93aa07c18)
