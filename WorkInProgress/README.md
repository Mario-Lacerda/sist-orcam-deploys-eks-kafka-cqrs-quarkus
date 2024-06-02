# 206_CriandoSistemaOrcamentoUtilizandoCQRSQuarkusKafkaDeployEKS
Criando um sistema de orçamento, utilizando CQRS, Quarkus, Kafka e deploy no EKS



[**](https://web.dio.me/track/inter-java-developer)

##### Criando um sistema de orçamento, utilizando CQRS, Quarkus, Kafka e deploy no EKS

[**](https://hermes.digitalinnovation.one/lab_projects/files/6415f0fd-8962-4efa-9f48-24cd4f810300.zip)

[**](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/6dfd6a3c-9528-4fa2-8965-c23cee0c961f)[**](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/0f36aa70-db07-4357-95b6-3249eae76cd9)

<iframe id="ytc116" frameborder="0" allowfullscreen="1" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" title="Parte 1" width="100%" height="100%" src="https://www.youtube.com/embed/vXsKvDK0s4w?controls=0&amp;disablekb=1&amp;enablejsapi=1&amp;fs=0&amp;iv_load_policy=3&amp;modestbranding=1&amp;showinfo=0&amp;rel=0&amp;html5=1&amp;cc_load_policy=0&amp;origin=https%3A%2F%2Fweb.dio.me&amp;widgetid=1" sandbox="allow-same-origin allow-scripts allow-forms allow-popups allow-popups-to-escape-sandbox" data-gtm-yt-inspected-11="true" style="box-sizing: inherit; max-width: none; float: none; margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; font-stretch: inherit; line-height: inherit; font-family: inherit; font-size: 14px; vertical-align: baseline;"></iframe>



00:56

 

08:11









normal

auto

- CONTEÚDOS
- INFORMAÇÕES

- [Como usar os desafios de projetos para criar seu portfólio](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/6dfd6a3c-9528-4fa2-8965-c23cee0c961f)
- [Parte 1](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/e06e539f-50b2-4703-a55a-4870e4184e6a)
- [Parte 2](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/0f36aa70-db07-4357-95b6-3249eae76cd9)
- [Parte 3](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/2bcfd132-07c5-4685-95a6-c1a0e4cd4ea7)
- [Parte 4](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/6069af26-2b9e-4193-8d3c-4448e4796402)
- [Parte 5](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/e64042d2-3c0c-445b-b2e2-1b2ccc2ea00f)
- [Parte 6](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/6219b608-30b8-4f64-a59b-746be3aa978f)
- [Parte 7](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/9a44c2e2-8085-4db8-a525-262773d879ac)
- [Parte 8](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/6798de47-7b41-408e-98d3-2dd4181d3279)
- [Parte 9](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/b72ba00d-0f75-47e4-8d99-ff16a1b8db5c)
- [Parte 10](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/c0404cb3-0d3b-4a27-bb45-8ce36856929f)
- [Parte 11](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/5f1ba970-8140-4ad5-b33e-42c897783c03)
- [Objetivo do projeto](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/4e515d78-fd30-4170-87a5-d019df105fdf)



[**](https://web.dio.me/track/inter-java-developer)

##### Criando um sistema de orçamento, utilizando CQRS, Quarkus, Kafka e deploy no EKS

[**](https://hermes.digitalinnovation.one/lab_projects/files/6415f0fd-8962-4efa-9f48-24cd4f810300.zip)

[**](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/5f1ba970-8140-4ad5-b33e-42c897783c03)[**](https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/undefined)

Link do Repositório do Projeto: https://github.com/wesleyfuchter/cqrs-quarkus-kafka



- CONTEÚDOS
- INFORMAÇÕES

###### DESCRIÇÃO

Neste Labs vamos implantar uma aplicação escrita em Java/Kotlin no serviço Elastic Kubernetes Service da Amazon. A aplicação é um exemplo do padrão CQRS que contempla dois serviços Quarkus que se comunicam através de um barramento assíncrono usando o Kafka. Você vai aprender a criar os manifestos do Kubernetes para implantação no EKS e quais configurações são necessárias para ter o ambiente rodando em produção.

**Mensageria****Kafka****Quarkus****Java**

------

###### Back-End

###### Avançado

------

###### ESPECIALISTA

![author](https://hermes.digitalinnovation.one/users/author/photos/46372db7-d97d-4711-8a02-b97308e32845.png)

###### Wesley Fuchter

Software Engineer, Modus Create[**](https://www.linkedin.com/in/add-me-wesleyfuchter/)
