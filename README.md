# mastercoin_front

Ola, fico muito contente em fazer esta prova, foi muito divertido.
neste README gostaria de deixar claro o que foi feito e como foi feito.
bom o front foi feito inteiramente em VUEJS e o back usando Padrões CQRS com a linguagem c# e .net core. tambem foi possivel colocar um MSTEST,
para testes diratamente no back. tambem é possivel iniciar o Swagger para testar a API diretamente.

as questões de validação da prova estão todas dentro da pagina de formulario de Usuario.
la estarão as validações de nome de Usuario, nome completo, data de aniversario, email validado e padrões de senha.
os demais itens da prova se encontram em sua paginas no meno do topo.
coloquei todas junto ao inves de subir 3 programas e como back 4 pois achei que tomaria menos do seu tempo, 
restaurando pacotes e iniciando algo de uma unica pagina. entao tudo que foi no front coloquei em um unico projeto.

VUEJS - 
para iniciar o front somente entre na pasta do projeto pelo terminal e execute "npm i" para restaurar os pacotes.
após concluido execute no terminal "npm run serve" para iniciar o projeto. lembrando que o back deve estar a rodar antes para estar em contato com a API

BACK - 

para iniciar o back pelo proprio visual studio ou ide de sua escolha, restaure os pacotes NUGUET, sete o projeto na pasta presentaton como padrão
o projeto foi feito en entity framework core o banco de dados usado foi o POSTGRES voce somente precisa alterar  a senha do usuari opostgres para a que voce usa, no consele de gerenciador de pacotes executar o comando "Add-Migration" ele ira te pedir um nome caso nao de certo apague a pasta "migrations" que se encontra no projeto infra da pasta 2-Infra as configurações de conexao de banco de dados esta no arquivo "MasterCoinContext" no projeto infra.


segue imagens do comentado.

1- formulario de cadastro de Usuario
![alt text](https://github.com/LordKai182/prova_mastercoin_front/blob/master/pagina1.png)



## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
