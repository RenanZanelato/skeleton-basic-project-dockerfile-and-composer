# Estrutura basica para projetos

## Executando o Projeto
Substitua no arquivo docker-compose.yaml os parâmetros `_PORTA_` pela porta em que deseja executar o sistema

Após isso, execute no terminal o comando:
```shell
docker-compose up -d
```

Será gerado um container com nome `nome_do_projeto`. Entre no terminal dele e instale as dependências do projeto.
```shell
docker exec -it -u nome_do_projeto bash
cd /var/www/html
composer install
```

Pronto basta acessar no navegador `127.0.0.1:_PORTA_/` e começar a utilizar o sistema.
