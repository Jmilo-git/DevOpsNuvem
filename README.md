# Projeto DevOps: GHSJMO19

**Site:** https://jmilo-git.github.io/DevOpsNuvem/

**Imagem:** `ghcr.io/jmilo-git/devopsnuvem`

## O fluxo completo

1. As alterações do projeto são enviadas ao GitHub por meio do comando `git push`.
2. O GitHub Actions executa os workflows responsáveis por testar a aplicação e verificar o código.
3. Quando uma tag de versão é enviada, o workflow de publicação é acionado.
4. O Docker constrói a imagem da aplicação e a publica no GitHub Container Registry (GHCR).
5. A imagem pode ser baixada com `docker pull`, executada com `docker run` e verificada por meio da rota `/saude`.

## Linha do tempo

- **v1:** Primeira versão funcional da API, publicada como imagem Docker no GHCR. A aplicação respondia à rota `/saude` informando a versão v1.
- **v2:** Foi realizada uma alteração na porta em que a API escutava. Apesar de os testes automatizados terem passado, a aplicação não respondeu na porta esperada quando executada no contêiner.
- **v3:** Foi realizado o rollback no repositório utilizando `git revert`, desfazendo a alteração da porta. A nova versão foi publicada e voltou a responder corretamente na rota `/saude`.

## O que os testes não pegaram

Os testes automatizados não identificaram que a aplicação estava escutando em uma porta diferente daquela utilizada para acessar o contêiner. Isso aconteceu porque os testes verificavam o funcionamento da aplicação, mas não validavam sua comunicação externa na porta esperada.

Para evitar esse problema, poderia ser acrescentado um teste de integração ao pipeline, construindo e iniciando o contêiner e realizando uma requisição à rota `/saude`. Dessa forma, caso a aplicação não respondesse corretamente, a publicação seria interrompida.

## Quem fez o quê

**Aluno A:**

Participou da configuração da página de status utilizando GitHub Pages, verificou as permissões e a visibilidade da imagem no GHCR e realizou o rollback no repositório utilizando `git revert`, permitindo corrigir a alteração que causou o problema na versão v2.

**Aluno B:**
Configurou o workflow de publicação das imagens Docker, utilizando o GitHub Actions e o GitHub Container Registry. Publicou a primeira versão da aplicação (v1) e realizou a simulação da falha na versão v2, alterando a porta em que a API escutava. Também participou da execução dos contêineres, identificação do problema e verificação das versões após os rollbacks.


