## Criador
Criado por Ryan Dahl.

## Problema inicial
Node.js foi criado com o intuito de como fazer I/O de um jeito diferente. Como fazer de um jeito que utilizasse menos memórias e thread.

## Arquitetura
O Node processa tudo em uma só thread, em um evento conhecido como event-loop.

## Exemplos

### Event-loop
- __[Single thread](primes-single-thread-server.js)__

Prime single-thread trata o recebimento de requisições, a cada requisição feita é enviada um callback.

### Pool threads
- __[Thread pool](files.js)__

### Multiplas-requisições
- __[Thread pool](primes-multi-thread-server)__

A cada requisição feita é enviado para um thread diferente, criando uma aplicação escalável.

## Execução de um arquivo Node
Para executar um script, digite:
```js
node <nomedoarquivo.js>
```