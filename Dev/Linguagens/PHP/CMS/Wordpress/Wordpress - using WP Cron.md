#php #cms
# Introdução
É possível utilizar o recurso WP CRON para criar tarefas agendadas que são executadas em horários e frequências especificas.


# Exemplos em código

É necessário adicionar uma ação com o nome do CRON e a função a ser executada pelo mesmo, desta forma:
```php
add_action( 'cron_name', 'function_name' );
// or
add_action( 'cron_name', array( $this, 'method_name' ) );
```

Após já é possível adicionar um agendamento para este evento, porém, é importante verificar se o mesmo já não foi agendado a fim de evitar a duplicação, por exemplo:
```php
if ( !wp_next_scheduled( 'cron_name' ) ) {
    wp_schedule_event( date(), 'daily', 'cron_name' );
}
```
> O primeiro parâmetro da função `wp_schedule_event` precisa ser um timestamp. O segundo determina a frequência do CRON veja as possibilidades [aqui](https://developer.wordpress.org/plugins/cron/understanding-wp-cron-scheduling/).

## Exemplo completo:
```php
public const CRON_NAME = 'oanewsender_contact_sent_info_reset_cron';

/**
 * Everyday at 00:00AM
 * 
 * @var string
 */
public const CRON_TIME = 'midnight';
public const CRON_RECURRENCE = 'daily';

private function __construct()
{
	add_action(self::CRON_NAME, array($this, 'run'));

	if (!wp_next_scheduled(self::CRON_NAME)) {
		wp_schedule_event(strtotime(self::CRON_TIME), self::CRON_RECURRENCE, self::CRON_NAME);
	}
}

public function run()
{
	// your code here!
}
```

## Verificando e disparando CRONs
É possível utilizar o "wp cli" para listar e disparar os eventos de CRON.

```
wp cron event list
```
> Lista os eventos agendados

```
wp cron event run cron_name
```
> Dispara um evento pelo nome, isso se o horário definido tiver sido atingido.

> [!NOTE] Dica
> Para rodar no modo root, passe a flag `--allow-root`

## Instalação WP Cron

```
curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
```

```
chmod +x wp-cli.phar
```

```
sudo mv wp-cli.phar /usr/local/bin/wp
```

## Referências
- https://developer.wordpress.org/plugins/cron/