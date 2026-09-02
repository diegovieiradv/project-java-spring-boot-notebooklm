# Curadoria de Fontes de Estudo

Este documento lista de 3 a 5 fontes abertas (texto ou PDF) confiáveis sobre Java e Spring Boot para desenvolvimento de APIs REST. Cada fonte foi selecionada por sua relevância, credibilidade e adequação aos objetivos do projeto.

---

## Fonte 1: Documentação Oficial do Spring Boot

- **Título:** Spring Boot Documentation
- **Instituição/Autor:** Pivotal Software / Spring Framework Project
- **URL:** https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/
- **Tipo da Fonte:** Documentação oficial (online, continuamente atualizada)
- **Tema Coberto:** Conceitos fundamentais do Spring Boot, auto-configuração, criação de aplicações, propriedades de configuração, execução embalada (JAR/WAR), produção pronta para uso.
- **Justificativa da Escolha:** É a fonte mais autoritária sobre Spring Boot. Todo desenvolvedor que trabalha com o framework deve consultar a documentação oficial primeiro. Cobra do básico (como criar uma aplicação "hello world") ao avançado (produção, teste, segurança). Todas as outras fontes deste projeto serão validadas contra esta documentação.

---

## Fonte 2: Spring Guides - Guides Officiais

- **Título:** Spring Guides
- **Instituição/Autor:** Spring Project (Pivotal / VMware)
- **URL:** https://spring.io/guides
- **Tipo da Fonte:** Tutoriais passo a passo / documentação prática
- **Tema Coberto:** Guias concretos para cenários reais: "Building a RESTful Web Service", "Accessing Data with JPA", "Building an Application with Spring Boot". Cada guide caminha do projeto inicial ao código final funcional.
- **Justificativa da Escolha:** Os Spring Guides são exemplos funcionais e "copy-paste-ready" que demonstram conceitos em prática. O guide "Building a RESTful Web Service" cobre exatamente o fluxo Controller → Service → Repository → JPA que este projeto quer consolidar. São ideais para testar prompts no NotebookLM porque têm código curto e bem definido.

---

## Fonte 3: Documentação Oficial do Java

- **Título:** The Java™ Tutorials
- **Instituição/Autor:** Oracle Corporation
- **URL:** https://docs.oracle.com/javase/tutorial/
- **Tipo da Fonte:** Documentação oficial da linguagem Java (tutorials)
- **Tema Coberto:** Fundamentos da linguagem Java (from basics to advanced), generics, collections, streams, concurrency, módulos (Java 9+), boa prática de código.
- **Justificativa da Escolha:** Embora o foco do projeto seja Spring Boot, a base é a linguagem Java. Compreender recursos modernos da linguagem (records, var, streams) é essencial para ler e escrever código Spring Boot de forma idiomática. A documentação da Oracle é referência oficial e confiável.

---

## Fonte 4: Spring Data JPA Documentation

- **Título:** Spring Data JPA — Reference Documentation
- **Instituição/Autor:** Spring Project
- **URL:** https://docs.spring.io/spring-data/jpa/docs/current/reference/html/
- **Tipo da Fonte:** Documentação específica de persistência
- **Tema Coberto:** Spring Data JPA, entidades JPA, repositórios, consultas derivadas, @Query personalizado, paginação (Pageable), mudanças de esquema (migrations), integração com bancos (H2, HSQLDB, PostgreSQL, MySQL).
- **Justificativa da Escolha:** O acesso a dados é uma peça central de qualquer API REST. Esta fonte cobre o Repository e JPA em profundidade, incluindo como criar métodos de consulta apenas com nomes, como usar @Query, e como lidar com transações. Essencial para o tópico "Persistência com JPA" do miniguia.

---

## Fonte 5: WebClient (Spring Docs)

- **Título:** Consuming REST Web Services — Spring Framework Reference
- **Instituição/Autor:** Spring Project
- **URL:** https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#web-client
- **Tipo da Fonte:** Documentação do Spring Framework (cliente HTTP)
- **Tema Coberto:** Como consumir APIs REST a partir de uma aplicação Spring (RestTemplate, WebClient), envio de requisições GET/POST/PUT/DELETE, corpos de requisição/resposta (JSON), tratamento de erros, tempo limite (timeout), assincronia.
- **Justificativa da Escolha:** Completa o panorama: além de criar APIs (Controller/Service/Repository), uma aplicação Spring muitas vezes precisa consumir outras APIs. Esta fonte cobre o cliente HTTP oficial do Spring, essencial para entender como a camada de apresentação se comunica com serviços externos.

---

## Resumo da Curadoria

| # | Fonte | Tipo | Tema Principal |
|---|-------|------|----------------|
| 1 | Spring Boot Docs | Documentação oficial | Auto-configuração, aplicação completa |
| 2 | Spring Guides | Tutoriais práticos | RESTful Web Service do zero |
| 3 | Java Docs | Documentação da linguagem | Fundamentos modernos da linguagem |
| 4 | Spring Data JPA | Documentação de persistência | JPA, Repository, consultas |
| 5 | Spring Web Client | Documentação de cliente HTTP | Consumir APIs REST externas |

**Total de fontes:** 5 (dentro do limite de 3 a 5 estabelecido pelo desafio)

---

## Próximos Passos

1. Adicionar estas fontes manualmente ao NotebookLM (conforme orientação do desafio).
2. Após confirmação de que as fontes foram adicionadas, prosseguir para a Etapa 4 (Engenharia de Prompts).
3. Cada fonte será usada como base para os experimentos de prompt nas etapas seguintes.

---

**Critério de validade:** Todas as URLs foram verificadas e levam a documentos reais e públicos. Nenhuma fonte foi inventada. Caso alguma fonte se mostre inacessível ou inadequada, será substituída antes de seguir para a próxima etapa.