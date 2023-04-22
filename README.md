
## Serviços AWS utilizados:

Amazon Cognito
Amazon DynamoDB
Amazon API Gateway
AWS Lambda

## Etapas do desenvolvimento:

1. Criando uma API REST no Amazon API Gateway:
- Acesse o Dashboard do API Gateway e selecione "Create API".
- Escolha "REST API" e selecione "Build".
- Escolha o protocolo "REST" e crie uma nova API.
- Selecione o Endpoint Type "Regional" e clique em "Create API".
- Crie um recurso selecionando "Actions" -> "Create Resource" e escolha o nome "Items".
2. Criando uma tabela no Amazon DynamoDB:
- Acesse o Dashboard do DynamoDB e selecione "Create table".
- Escolha o nome "Items" e o Partition key "id", em seguida clique em "Create table".
3. Criando uma função no AWS Lambda para inserir itens na tabela:
- Acesse o Dashboard do Lambda e crie uma nova função com o nome "put_item_function".
- Insira o código da função "put_item_function.js", disponível na pasta /src, e realize o deploy.
- Configure a execução da role no console do IAM, selecionando a role criada e adicionando uma política inline para permitir a ação "putItem" no serviço DynamoDB.
4. Integrando o API Gateway com o Lambda backend:
- Selecione a API criada no Dashboard do API Gateway e escolha o recurso "Items".
- Crie um método "POST" e integre com a função Lambda "put_item_function".
- Salve e faça o deploy da API, selecionando a opção "New Stage [dev]".
5. Realizando uma requisição POST com o POSTMAN:
- Adicione uma nova requisição com o método "POST" e copie o endpoint gerado pelo API Gateway.
- No corpo da requisição, adicione o seguinte body:
```
{
"id": "003",
"price": 600
}
```
- Envie a requisição.
6. Configurando um pool de usuários no Amazon Cognito:
- Acesse o Dashboard do Cognito e crie um novo User Pool com o nome "TestPool".
- Escolha a opção "Email address or phone number" para login e defina a força da senha desejada.
- Desabilite o Multi-Factor Authentication (MFA) e personalize a verificação de e-mail através do link de verificação.
- Crie um App Client com o nome "TestClient" para ter acesso ao User Pool.
7. Configurando um autorizador do Amazon Cognito para uma API REST no Amazon API Gateway:
- Selecione a API criada no Dashboard do API Gateway e escolha "Authorizers" -> "Create New Authorizer".
- Defina o nome como "CognitoAuth", o tipo como "Cognito" e selecione o User Pool criado anteriormente.
- Escolha "Authorization" como Token Source.
No Método Request, selecione o autorizador criado para a autorização.

7. No POSTMAN

- Selecione a solicitação criada para inserir um item e vá para a seção "Authorization". Defina o tipo como "Bearer Token" e insira o token copiado.
- Clique em "Send" para enviar a solicitação e testar a API.