# Desafio Dio - **Criando um Sistema de Orçamento, Utilizando CQRS, Quarkus, Kafka e Deploy no EKS**



### Projeto **Sistema de Orçamento com CQRS, Quarkus, Kafka e Implantação no EKS**

O objetivo deste projeto é criar um sistema de orçamento robusto e escalável usando a arquitetura CQRS (Command Query Responsibility Segregation), a estrutura Quarkus, o barramento de mensagens Kafka e implantá-lo no Kubernetes Engine (EKS).



## **Arquitetura**

O sistema será dividido em dois componentes principais:

### **Componente de Comando**

- Responsável por receber comandos de orçamento e persistir as alterações no banco de dados.
- Escrito em Java usando Quarkus.
- Utiliza JAX-RS para expor endpoints REST.
- Utiliza JPA para persistir dados no banco de dados.

- Comando:** Responsável por receber comandos de orçamento e persistir as alterações no banco de dados.

  

  ### **Componente de Consulta**

  - Responsável por fornecer uma visão atualizada dos orçamentos.

  - Escrito em Java usando Quarkus.

  - Utiliza JAX-RS para expor endpoints REST.

  - Utiliza consultas SQL para recuperar dados do banco de dados.

    

- #### **Barramento de Mensagens Kafka**

  - Responsável por transmitir comandos do componente de comando para o componente de consulta.

  - Garante que as consultas sempre tenham uma visão atualizada dos orçamentos.

    

  ### **Implantação no EKS**

  - O sistema será implantado em um cluster EKS usando Kubernetes.

  - Isso fornecerá escalabilidade, disponibilidade e gerenciamento automatizado. 

  - O sistema será implantado no EKS usando o Kubernetes. Isso fornecerá escalabilidade, disponibilidade e gerenciamento automatizado.

    

### **Tecnologias**

- **Quarkus:** Estrutura Java para desenvolvimento de microsserviços rápidos e escaláveis.
- **CQRS:** Padrão de design que separa as responsabilidades de comando e consulta.
- **Kafka:** Barramento de mensagens distribuído para comunicação assíncrona.
- **EKS:** Plataforma de contêiner gerenciada para implantação e gerenciamento de aplicativos em Kubernetes.



### **Fluxo de Trabalho**

1. **Criação de Orçamento:** Um cliente envia um comando HTTP POST para o endpoint de criação de orçamento do componente de comando.
2. O componente de comando persiste o novo orçamento no banco de dados e publica um evento no tópico Kafka "orcamentos".
3. O componente de consulta recebe o evento Kafka e atualiza sua visão dos orçamentos.
4. **Atualização de Orçamento:** Um cliente envia um comando HTTP PUT para o endpoint de atualização de orçamento do componente de comando.
5. O componente de comando atualiza o orçamento existente no banco de dados e publica um evento no tópico Kafka "orcamentos".
6. O componente de consulta recebe o evento Kafka e atualiza sua visão dos orçamentos.
7. **Consulta de Orçamento:** Um cliente envia um comando HTTP GET para o endpoint de consulta de orçamento do componente de consulta.
8. O componente de consulta retorna uma visão atualizada do orçamento.

1. **Criação de Orçamento:** Um comando é enviado para o componente de comando, criando um novo orçamento no banco de dados.
2. **Atualização de Orçamento:** Um comando é enviado para o componente de comando, atualizando um orçamento existente no banco de dados.
3. **Consulta de Orçamento:** Uma consulta é enviada ao componente de consulta, retornando uma visão atualizada do orçamento.



### **Benefícios**

- **Separação de Preocupações:** O CQRS separa as responsabilidades de comando e consulta, tornando o sistema mais fácil de manter.
- **Escalabilidade:** O Quarkus e o Kafka permitem que o sistema seja escalado horizontalmente para atender à crescente demanda.
- **Consistência de Dados:** O banco de dados garante a consistência dos dados, mesmo em caso de falhas.
- **Implantação Facilitada:** O EKS simplifica a implantação e o gerenciamento do sistema.



### **Conclusão**

Este projeto fornecerá um sistema de orçamento completo e escalável que atende aos requisitos de negócios. A combinação de CQRS, Quarkus, Kafka e EKS garante desempenho, confiabilidade e facilidade de manutenção.



**Componente de Comando (Quarkus)**

java

```java
@Path("/orcamentos")
public class OrcamentoResource {

    @POST
    @Consumes(MediaType.APPLICATION_JSON)
    public Response criarOrcamento(Orcamento orcamento) {
        orcamentoService.criarOrcamento(orcamento);
        return Response.status(201).build();
    }

    @PUT
    @Path("/{id}")
    @Consumes(MediaType.APPLICATION_JSON)
    public Response atualizarOrcamento(@PathParam("id") Long id, Orcamento orcamento) {
        orcamentoService.atualizarOrcamento(id, orcamento);
        return Response.status(200).build();
    }
}
```



**Componente de Consulta (Quarkus)**

java

```java
@Path("/orcamentos")
public class OrcamentoConsultaResource {

    @GET
    @Produces(MediaType.APPLICATION_JSON)
    public List<Orcamento> listarOrcamentos() {
        return orcamentoService.listarOrcamentos();
    }

    @GET
    @Path("/{id}")
    @Produces(MediaType.APPLICATION_JSON)
    public Orcamento obterOrcamento(@PathParam("id") Long id) {
        return orcamentoService.obterOrcamento(id);
    }
}
```



**Configuração do Kafka (application.properties)**

properties

```properties
quarkus.kafka.bootstrap.servers=localhost:9092
quarkus.kafka.producer.topic=orcamentos
```



**Implantação no EKS**

yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: orcamento-comando
  labels:
    app: orcamento-comando
spec:
  replicas: 1
  selector:
    matchLabels:
      app: orcamento-comando
  template:
    metadata:
      labels:
        app: orcamento-comando
    spec:
      containers:
        - name: orcamento-comando
          image: meu-registro.io/orcamento-comando:latest
          ports:
            - containerPort: 8080
```



**Código de Serviço de Orçamento (Quarkus)**

java

```java
@ApplicationScoped
public class OrcamentoService {

    @Inject
    private OrcamentoRepository orcamentoRepository;

    @Inject
    private KafkaProducer<String, Orcamento> orcamentoProducer;

    public void criarOrcamento(Orcamento orcamento) {
        orcamentoRepository.persist(orcamento);
        orcamentoProducer.send("orcamentos", orcamento);
    }

    public void atualizarOrcamento(Long id, Orcamento orcamento) {
        Orcamento orcamentoExistente = orcamentoRepository.findById(id);
        orcamentoExistente.setValor(orcamento.getValor());
        orcamentoRepository.persist(orcamentoExistente);
        orcamentoProducer.send("orcamentos", orcamentoExistente);
    }

    public List<Orcamento> listarOrcamentos() {
        return orcamentoRepository.listAll();
    }

    public Orcamento obterOrcamento(Long id) {
        return orcamentoRepository.findById(id);
    }
}
```



**Interface de Repositório de Orçamento (Quarkus)**

java

```java
public interface OrcamentoRepository {

    void persist(Orcamento orcamento);

    Orcamento findById(Long id);

    List<Orcamento> listAll();
}
```



**Implementação do Repositório de Orçamento (Quarkus)**

java

```java
@ApplicationScoped
public class OrcamentoRepositoryImpl implements OrcamentoRepository {

    @PersistenceContext
    private EntityManager entityManager;

    @Override
    public void persist(Orcamento orcamento) {
        entityManager.persist(orcamento);
    }

    @Override
    public Orcamento findById(Long id) {
        return entityManager.find(Orcamento.class, id);
    }

    @Override
    public List<Orcamento> listAll() {
        return entityManager.createQuery("SELECT o FROM Orcamento o", Orcamento.class).getResultList();
    }
}
```



**Entidade Orçamento (Quarkus)**

java

```java
@Entity
@Table(name = "orcamentos")
public class Orcamento {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String nome;

    private BigDecimal valor;

    // getters and setters
}
```



**Configuração Adicional do Kafka (application.properties)**

properties

```properties
quarkus.kafka.consumer.topic=orcamentos
quarkus.kafka.consumer.group-id=orcamento-consulta
```

**Implementação do Consumidor Kafka para o Componente de Consulta (Quarkus)**

java

```java
@ApplicationScoped
public class OrcamentoConsultaConsumer {

    @KafkaListener(topics = "orcamentos", groupId = "orcamento-consulta")
    public void consumirOrcamento(Orcamento orcamento) {
        // Atualizar a visão do orçamento no componente de consulta
    }
}
```





# LABS DIO - DESAFIO ESPECIALISTA

Criando um sistema de orçamento, utilizando CQRS, Quarkus, Kafka e deploy no EKS



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



https://web.dio.me/lab/criando-um-sistema-de-orcamento-utilizando-cqrs-quarkus-kafka-e-deploy-no-eks/learning/e06e539f-50b2-4703-a55a-4870e4184e6a
