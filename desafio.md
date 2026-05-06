# Luizalabs - NotebookLM - Back-End com Python e FastAPI
https://notebooklm.google.com/notebook/ec42af24-99d4-4e8d-ab67-873785c14a1e

## Resumo estruturados do assunto
1. O Framework FastAPI O FastAPI é um framework web focado na construção de APIs RESTful. Ele atua como a ponte entre o cliente (front-end, aplicativos) e a lógica do servidor.
Alta Performance: É assíncrono por padrão (async/await), sendo extremamente rápido e comparável a linguagens como NodeJS e Go.
Documentação Automática: Gera documentações interativas como o Swagger UI de forma automática, permitindo visualizar e testar os endpoints da API facilmente pelo navegador.

3. Arquitetura e Organização do Projeto Para que o projeto seja escalável e fácil de manter, o código é estruturado de forma limpa (Clean Architecture), separando as responsabilidades:
Rotas (Routers): Gerenciam as URLs (como /pedidos, /usuarios) e os métodos HTTP da API (GET, POST, PUT, DELETE). Para manter a organização, utiliza-se o APIRouter para separar as rotas em diferentes arquivos baseados em seus temas.
Esquemas (Schemas): Utilizando a biblioteca Pydantic, os esquemas validam e forçam a tipagem dos dados (JSON) que entram e saem da API. Isso bloqueia informações incorretas automaticamente.
Modelos (Models): São as classes que representam as tabelas e relacionamentos diretamente no banco de dados.
Repositórios (Repositories): É a camada que concentra a lógica para salvar, editar ou buscar dados no banco, separando essa complexidade do restante da aplicação.

5. Gerenciamento de Banco de Dados A comunicação entre o código Python e o banco de dados é feita de maneira otimizada:
ORM (SQLAlchemy): O Object Relational Mapper (ORM) traduz os objetos e classes do Python em tabelas do banco de dados (como SQLite ou PostgreSQL), eliminando a necessidade de escrever códigos SQL manualmente de forma constante.
Migrações (Alembic): É a ferramenta responsável pelo versionamento e evolução do banco de dados. Se você adicionar ou remover uma coluna no seu código, o Alembic identifica a mudança e atualiza o banco de dados de forma automática e segura, sem perda de dados.
Sessões e Dependências: O FastAPI utiliza o recurso de Injeção de Dependências (Depends()) para abrir as sessões do banco de dados quando uma requisição se inicia e garantir o seu fechamento seguro logo em seguida.  

6. Autenticação e Segurança A segurança é tratada de forma prioritária para resguardar a integridade das informações:
Criptografia de Senhas: As senhas nunca são armazenadas em texto puro. Utiliza-se o algoritmo bcrypt para gerar hashes irreversíveis das senhas no banco de dados.
Tokens JWT (JSON Web Tokens) e OAuth2: Em vez de exigir a senha a cada clique, o sistema gera um Token JWT com um tempo de expiração na hora do login. Esse token atua como um crachá de autorização: o usuário o envia no cabeçalho (header) de cada requisição subsequente para provar sua identidade e acessar rotas restritas.  

7. Recursos Avançados
CORS e Middlewares: O CORS é configurado via middlewares (interceptadores) para permitir e controlar com segurança quais sites externos ou origens (como um aplicativo Front-End específico) podem consumir a sua API. Middlewares também podem interceptar e avaliar requisições antes que cheguem nas rotas.
Tarefas em Segundo Plano (Background Tasks): Para operações demoradas (como o envio de um e-mail após uma compra), o FastAPI permite despachar a tarefa para o background. Isso faz com que a API libere o usuário e devolva a resposta imediatamente, enquanto conclui o processamento em segundo plano.
Deploy com Docker: Na hora de ir para produção, a aplicação é frequentemente "empacotada" utilizando o Docker por meio de um arquivo Dockerfile. Isso empacota as dependências e o código juntos, permitindo hospedar o sistema com facilidade em plataformas nas nuvens, como a Render.

## Glossário com os principais conceitos aprendidos
Alembic / Migrações (Migrations): É a ferramenta associada ao SQLAlchemy responsável por gerenciar a evolução e o versionamento do banco de dados. Ele identifica quando você adiciona ou remove atributos no código e aplica essas alterações (migrações) no banco de dados de forma segura, sem perder os dados já existentes.  

API REST (Representational State Transfer): Uma interface de comunicação web baseada no protocolo HTTP, que atua como a ponte entre o cliente (front-end, aplicativos) e o servidor (back-end). O tráfego de dados é geralmente feito no formato padronizado JSON.
Background Tasks (Tarefas em Segundo Plano): Funcionalidade do FastAPI que permite despachar operações demoradas (como envio de e-mails ou processamento de pagamentos) para rodarem de forma paralela em segundo plano. Isso evita que a requisição do usuário demore, devolvendo uma resposta imediata enquanto o trabalho pesado continua.  

CORS (Cross-Origin Resource Sharing): É um mecanismo de segurança do navegador configurado no back-end que determina quais domínios, sites e aplicativos externos (origens diferentes) estão autorizados a consumir e acessar os dados da sua API.  
CRUD: Um acrônimo para as quatro operações fundamentais de gerenciamento de dados: Create (Criar), Read (Ler), Update (Atualizar) e Delete (Deletar).
Endpoint / Rota (Route): O endereço ou URL específico (ex: /usuarios, /pedidos) configurado na API que o cliente acessa para interagir com o sistema e executar uma determinada ação.  

Esquemas (Schemas / Pydantic): No contexto do FastAPI, os esquemas (utilizando a biblioteca Pydantic) são classes que definem a estrutura, o modelo e a tipagem rigorosa dos dados (JSON) que entram e saem da API. Eles servem para validar e padronizar o tráfego externo de informações.  

Hash / Bcrypt: Um processo de criptografia irreversível aplicado a informações sensíveis, como senhas, antes de serem salvas. A biblioteca Bcrypt converte a senha em um código embaralhado (hash), garantindo que, mesmo se o banco de dados for comprometido, as senhas originais não sejam descobertas.  

Injeção de Dependência (Depends): Um recurso nativo do FastAPI usado para declarar exigências que uma rota precisa para funcionar. O framework resolve isso automaticamente, sendo muito utilizado para abrir sessões de banco de dados ou validar tokens de autenticação antes que a rota principal seja executada.  

JWT (JSON Web Token): É um padrão de token utilizado para garantir autenticação segura do usuário nas requisições da API. Em vez de enviar e-mail e senha em toda operação, o usuário recebe um JWT na hora do login e passa a enviá-lo pelo cabeçalho (header) HTTP para provar sua identidade por um tempo limitado.  

Métodos HTTP: Os verbos utilizados nas requisições para indicar qual operação se deseja fazer na API. Os mais comuns são o GET (para obter ou listar dados), POST (para enviar e criar dados), PUT/PATCH (para atualizar dados) e DELETE (para remover dados).  

Middlewares: São interceptadores posicionados no meio do caminho entre o cliente e a rota. Eles processam toda requisição que chega à API antes que ela alcance a rota de destino e também podem manipular a resposta antes de ela ser devolvida ao cliente.  

Modelos (Models): Diferente dos esquemas, os modelos são classes que representam a estrutura de dados dentro da própria aplicação e do banco de dados. Eles indicam os nomes das tabelas e as colunas exatas que farão parte do banco.  

ORM (Object-Relational Mapping / SQLAlchemy): Ferramenta (como o SQLAlchemy) que traduz o código e os objetos orientados a objetos do Python para a linguagem do banco de dados (tabelas e comandos SQL). Isso permite interagir com o banco de dados escrevendo código Python sem precisar escrever consultas SQL manualmente de forma constante.  

Parâmetros de Rota e Query Strings: São formas de enviar dados via URL. Path parameters (parâmetros de rota) ficam embutidos diretamente no caminho (ex: /produtos/5) e costumam ser usados para identificar recursos específicos. Já Query parameters (query strings) ficam ao final da URL, após um ponto de interrogação (ex: /produtos?limite=10), e são geralmente usados para filtros e paginação.  

Repositório (Repository Pattern): É uma camada estrutural do projeto dedicada exclusivamente à lógica de acesso a dados. O repositório centraliza operações como buscar, salvar, alterar ou deletar registros do banco, isolando essa complexidade técnica do resto das rotas da API.  

Status Code (Códigos de Status HTTP): Números incluídos na resposta do servidor para sinalizar o resultado da requisição. A família 200 (como 200 OK ou 201 Created) indica sucesso, os códigos 400 (como 404 Not Found ou 401 Unauthorized) indicam que o cliente cometeu algum erro, e a família 500 aponta que ocorreu um erro interno no servidor.

## Conjunto de prompts reutilizáveis que possam apoiar futuras revisões sobre o tema
### Categoria 1: Fundamentos de APIs e FastAPI
Prompt de Revisão Teórica: "Explique com suas palavras a diferença entre Path Parameters (Parâmetros de Rota), Query Parameters e Request Body em uma requisição HTTP, dando um exemplo prático de uso para cada um no FastAPI."
Prompt de Validação: "O que são Schemas criados com o Pydantic? Qual é o papel deles no FastAPI e como eles ajudam a validar os dados que entram e saem da nossa API?"  

Prompt de Execução: "Qual é o comando para iniciar um servidor FastAPI utilizando o Uvicorn? Explique a utilidade da flag --reload durante o ambiente de desenvolvimento."

### Categoria 2: Arquitetura e Banco de Dados (SQLAlchemy)
Prompt Comparativo: "Em um projeto estruturado, qual é a diferença entre os 'Schemas' (dados de entrada e saída da API) e os 'Models' (modelos de banco de dados do SQLAlchemy)? Por que separamos esses dois conceitos?"  

Prompt de Padrão de Projeto: "Como funciona o padrão de projeto Repository (Repositório)? Explique por que é uma boa prática isolar a lógica de acesso e manipulação do banco de dados das rotas principais da API."  

Prompt de Relacionamento: "Como configuro uma chave estrangeira (Foreign Key) e um relacionamento bidirecional entre duas tabelas (ex: Usuário e Pedido) usando o SQLAlchemy?"

### Categoria 3: Migrações de Banco de Dados (Alembic)
Prompt de Fluxo de Trabalho: "Explique o que é o Alembic e por que precisamos dele para evoluir o banco de dados. Como é o fluxo para gerar uma nova migração (revisão) e aplicá-la ao banco de dados?"  

Prompt de Resolução de Problemas: "O que eu devo fazer caso uma migração do Alembic dê erro no meio do caminho ou eu precise adicionar uma nova coluna em uma tabela que já possui dados gravados?"

### Categoria 4: Segurança e Autenticação (JWT e Hashes)
Prompt de Segurança: "Por que é extremamente inseguro salvar senhas em texto puro no banco de dados? Explique como utilizamos bibliotecas como o Bcrypt para gerar hashes das senhas antes de salvá-las."  

Prompt de Fluxo de Autenticação: "Descreva passo a passo o fluxo de autenticação de uma API usando JWT (JSON Web Tokens). Como o token é gerado no momento do login e como exigimos ele nas rotas protegidas usando Depends()?"  

Prompt de Controle de Acesso: "O que é CORS (Cross-Origin Resource Sharing) e como utilizamos os Middlewares no FastAPI para autorizar ou bloquear que sites front-end específicos consumam nossa API?"

### Categoria 5: Desafios Práticos de Código
Desafio de Rota HTTP: "Escreva o código em Python de uma rota POST no FastAPI para criar um produto. A rota deve receber os dados validados por um schema, salvar no banco de dados usando um repositório, e retornar o Status Code 201 (Created)."
Desafio de Operações Assíncronas: "Crie um exemplo prático de como utilizar o recurso de Background Tasks (Tarefas em Segundo Plano) do FastAPI para simular o envio de um e-mail sem travar o tempo de resposta da requisição principal."
### 💡 Dica de estudo: Quando for utilizar esses prompts, você pode adicionar no final a instrução: "Faça perguntas ao final da sua explicação para testar se eu realmente entendi o conceito." Isso transformará a revisão em uma sessão de estudo interativa!
