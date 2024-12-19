# 3. Event Driven Architecture

Data: 19 de dezembro de 2024

## Status

Proposto

## Contexto

### Questão Aberta L4


Este documento tem como objetivo discutir a utilização da [`Event Driven Architecture`](https://en.wikipedia.org/wiki/Event-driven_architecture) no projeto proposto pelo desafio, conforme evidenciado na seção correspondente do arquivo [README](./../../../README.md):

> - Aplicação de arquiteturas (CQRS, [`Event-Sourcing`](https://martinfowler.com/eaaDev/EventSourcing.html), Microsserviços, Monolito Modular)  
> - Uso e implementação de `mensageria`  

Em projetos anteriores, enfrentamos a restrição de transações com baixo timeout (100ms) e `síncronas`, o que foi um impeditivo para a adoção de filas e da `Event Driven Architecture`, devido à baixa `latência` exigida no processamento dessas requisições em cenários onde concorrencia poderia existir para transacoes de mesma conta simultaneas onde sistemas robustos de mensageria poderiam adicionar `latencia adicional`.

Essas restrições não estão presentes no projeto atual, que deve ser assíncrono. Neste cenário torna-se favorável a utilização dessas ferramentas. Neste documento, discutiremos a implementação de `Mensageria`, bem como a necessidade de realizar uma sessão de [`Event-Storm`](https://en.wikipedia.org/wiki/Event_storming)  para nos ajudar a identificar fluxos e eventos relevantes do `Event-Sourcing`.

#### Leituras adicionais:
- [Event-sourcing (ES) em uma Arquitetura de Microsserviços](https://medium.com/@marcelomg21/event-sourcing-es-em-uma-arquitetura-de-microsservi%C3%A7os-852f6ce04595)
- [O que é uma arquitetura orientada por eventos?](https://aws.amazon.com/pt/event-driven-architecture/)
- [Como o Kafka e o RabbitMQ lidam com as mensagens de forma diferente?](https://aws.amazon.com/pt/compare/the-difference-between-rabbitmq-and-kafka/)

## Decisão

### Implementação de `Event Driven Architecture`

A decisão proposta é adotar a `Event Driven Architecture` no projeto atual, utilizando ferramentas de `mensageria` para garantir a comunicação assíncrona entre sistemas e eventos de negócio. 

**Passos para Implementação:**
1. **Realizar uma Sessão de `Event Storming`:**
   - Identificar os principais eventos do sistema e mapear seus fluxos.
   - Garantir alinhamento com os requisitos de negócios e técnicos.

2. **Escolha de Ferramentas de `Mensageria`:**
   - Avaliar e selecionar entre soluções como [`Kafka`](https://kafka.apache.org/) ou [`RabbitMQ`](https://www.rabbitmq.com/), considerando casos de uso específicos, volume esperado e requisitos de performance.

3. **Definição de `Padrões de Evento`:**
   - Estabelecer contratos claros para os eventos, como formato, versionamento e atributos obrigatórios.

4. **Testes de `Performance`:**
   - Realizar benchmarks para validar a latência adicionada pelo sistema de mensageria e garantir conformidade com os requisitos de SLA.

---

## Justificativa

A adoção de Event Driven Architecture oferece os seguintes benefícios ao projeto atual:
- **`Escalabilidade`**: Permite lidar com volumes crescentes de dados e requisições.
- **`Desacoplamento`**: Facilita a evolução e manutenção de serviços de forma independente.
- **`Resiliência`**: Aumenta a capacidade do sistema de operar mesmo com falhas parciais.
- **`Alinhamento Estratégico`**: Adere às boas práticas modernas para arquiteturas distribuídas, conforme descrito nos requisitos do desafio.

A ausência de restrições de baixa latência no projeto atual torna viável a utilização de ferramentas de mensageria robustas, mitigando limitações enfrentadas em projetos anteriores.

