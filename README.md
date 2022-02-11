# Amplify 

> Aplicação simples para desenvolvimento do trabalho de CLOUD ARCHITECTURE & DEVOPS - FIAP com os seguintes objetivos: 
> 
> - a realização da autenticação e autorização utilizando [Cognito](https://aws.amazon.com/pt/cognito/);
> - hospedagem da aplicação utilizando [Amplify](https://aws.amazon.com/pt/amplify/);
> - pipeline de entrega continua(CICD) no Amplify

### Como realizar o deploy da aplicação utilizando Amplify

1. Faça o clone desse repoistório para um diretório local em sua máquina;

2. Crie um novo repositório em sua conta pessoal no GitHub;

3. Feito isso é necessário que voce crie uma chave SSH para que você possa acessar sua conta através do Cloud9
 - Como criar sua chave ssh no [linux](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent);
 - Como adicionar sua chave no [GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account);

4. Para os passos seguintes é necessário que você possua algum conhecimento com o [Cloud9](https://aws.amazon.com/pt/cloud9/) pois é ele quem será usado como IDE para que possamos estar realizando a nossa hospedagem e CICD;

5. O próximo passo é subir o projeto que está local na sua máquina para o repositório criado, para isso realize os seguintes comandos: 

  ``` shell
   git init
   git add -A
   git commit -m "first commit"
   git remote add origin git@github.com:SEU-USUARIO/postgram.git
   git push origin master
   ```

6. Inicie a criação do hosting no S3 com o comando `amplify hosting add`
   -  Em 'Select the plugin module to execute ' selecione `Hosting with Amplify Console (Managed hosting with custom domains, Continuous deployment)`;
  
 -  Em 'Choose a type' selecione `Continuous deployment (Git-based deployments)`;

   -  Nesse passo deixe o terminal como esta e vá para outra aba no painel do amplify e entre no seu projeto `postagram` e selecione a aba `Hosting Environments`;
   
   - Selecione o GitHub e clique em `Connect branch` na lateral inferior direita;

   -  Autorize o amplify a acessar seu github, selecione o projeto `postagram` e a branch `master`. Clique em next;

   -  Escolha o `environment` `dev`;

   -  Habilite a opção `Enable full-stack continuous deployments (CI/CD)`;
  
 - Clique em `Create new role`, isso vai abrir uma nova aba onde apenas tem que clicar em next até criar a role necessária. Após o processo volte ao amplify e selecione a role criada. Caso ela não apareça na lista, clique em `Refresh existing roles`. Clique em Next;


   -  Revise as informações e clique em `Save and Deploy`. Isso vai criar um primeiro deploy. Pode ignorar ele por hora;
 
7. Volte ao Cloud9 e pressione enter no terminal que estava aguardando;

8. Execute os seguintes comandos para atualizar o github e executar o pipeline do projeto para adicionar o host do S3 diretamente via pipeline.

```
  git status
  git add -A
  git status
  git commit -m "adding hosting"
  git push origin master
  ```

9. Devolta ao console do amplify poderá ver que um pipeline iniciou a partir do push para o github que acabou de fazer. Caso ainda esteja rodando o pipeline de quando criou a configuração, apenas aguarde;

10. Você pode acompanhar cada fase clicando nela. E expandindo o log;

11. Durante o processo de build do frontend o pipeline vai rodar o `npm build` e fazer o upload dos artefatoas para o S3;

12. Ao final será possivel pegar o link do seu app no campo domain;

13. Acesse sua aplicação via o link e utilize normalmente.

14. Feito o `clone` do projeto e com a sua chave SSH gerada(lembrando que a chave também deverá ser gerada através do Cloud9, utilizando o terminal da IDE), você deverá ir até a raiz do projeto com o comando `cd react-login-register-page/`


Obs: este projeto foi clonado a partir do [Logster](https://github.com/ilyaszm/react-login-register-page)
