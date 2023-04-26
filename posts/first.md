---
id: first_post
date: 26-04-2023
update: 26-04-2023
author: raferdev
description: Primeiro post com algumas informações sobre este blog.
---

## 📝 Tópicos

- [Intro](#intro)
- [Sobre](#sobre)
- [Usage](#usage)
- [Como Funciona](#built_using)
- [Finalizando](#fim)
- [Authors](#authors)

## <a name = "intro"></a>

Eai galera, chegou a hora de fazer a primeira postagem depois de algum trabalho desenvolvendo essa aplicação web.

### Um pouco sobre o projeto: <a name = "sobre"></a>

A ideia princípal é separar o core da aplicação do seu conteúdo, sendo possível eu atualizar posts e detalhes em um repositório separado, apenas em markdown, e que irá refletir no site em produção na nuvem, ec2, etc.

A dor começou pois o uso de aplicações AWS, Microsoft Azure, Google Cloud, tem limitações para o uso free tier, o que claro é necessário, mas limita alguns projetos para quem esta começando a montar aplicações e pipelines mais robustas como projeto experimental.

Isso pois a quantidade de RAM é bem limitada, no caso eu uso o T2.micro, EC2 da AWS, e ao tentar realizar builds em ci/cd em imagens docker dentro da ec2 o servidor comumente cai. Tentei algumas estratégias como mudança de copilador, vite, webpack, etc, mas dependendo da versão do projeto não era possível.

Então também amante do MDX (markdown + jsx), da possíbilidade de criar conteúdo de forma fácil de implementar, sem pensar em html e css. Também por gostar de NextJS _e também por gosar quando o cartão de crédito não vem em dollar_ eu pensei numa aplicação que juntasse tudo isso.

Ponderei em fazer um cluster para subir um container só para criar as builds e dai salvar no servidor, mas a maioria das soluções são pagas. MASS aí vem o pulo do :cat: que é o uso das Actions do Github para montar a build. E o servidor docker para salvar a imagem já pronta para dar start no servidor.

## Como basicamente funciona: <a name = "intro"></a>

- 0# - O servidor NextJs busca o repositório com o markdown e detalhes do conteúdo, faz o fetch dos arquivos para dentro do servidor e roda os comandos para criar os componentes da página centrak.

- 1# - O repositório já tem o arquivo docker configurado para realizar a build, com uma imagem debian alphine para um container otimizado.

- 2# - Ao dar merge na branche 'prod' é iniciado a action para build da imagem docker num hosted do próprio github, e usado um app do docker pra depois que a build estiver pronta, subir ela para a conta docker na nuvem com a imagem.

- 3# - Agora com a imagem latest do seu app, é apenas uma action normal em um servidor selfhosted pra dar start do container.

- #4 - O container Ngnix serve os arquivos e é colocado com cache de 1 dia para não ficar consumindo direto do servidor NextJS e pesar mais o processamento.

## Finalizando <a name = "fim"></a>

Ainda falta muita coisa e a ideia é ser open source, reutilizavel, e simples. No caso agora falta muita refatoração pois para funcionar foram algumas tentativas e ideias que ficaram para trás.

## Autor

- [Rafael Fernandes](https://github.com/imraferdev)
