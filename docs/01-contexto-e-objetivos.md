# Contexto e Objetivos do Estudo

## Contexto do Desafio

Este projeto foi desenvolvido como parte do desafio da DIO (Digital Innovation One) sobre uso do NotebookLM como ferramenta de aprendizagem ativa. O objetivo é criar um caderno temático estruturado que consolide conhecimentos fundamentais de Java e Spring Boot aplicados ao desenvolvimento de APIs REST, utilizando inteligência artificial para síntese, revisão e organização do aprendizado.

## Tema Escolhido

**"Java e Spring Boot para Desenvolvimento de APIs REST"**

A escolha desse tema responde à demanda prática de desenvolvedores que precisam dominar o ecossistema Spring Boot para criar APIs robustas, escaláveis e seguras. Spring Boot é o framework mais adotado na indústria Java para desenvolvimento rápido de microserviços e APIs, abstraindo grande parte da configuração complexa do Spring Framework tradicional.

## Justificativa da Escolha

Spring Boot oferece convenções que permitem aos desenvolvedores focarem na lógica de negócio em vez de configuração de infraestrutura. Domínio dos conceitos centrais — controle de fluxo via Controller, lógica de negócio via Service, persistência via Repository e JPA — é essencial para qualquer desenvolvedor Java que queira atuar na área de back-end. O NotebookLM, por sua vez, proporciona uma maneira interativa de processar e revisar esses conceitos, transformando textos densos em insights estruturados e perguntas de revisão.

## Objetivo Geral

Criar um caderno temático no NotebookLM que consolide conhecimentos fundamentais de Java e Spring Boot aplicados ao desenvolvimento de APIs REST, permitindo revisão ativa, identificação de lacunas e geração de prompts reutilizáveis para estudo contínuo.

## Objetivos Específicos

1. **Curadoria de fontes** — Selecionar e documentar de 3 a 5 fontes abertas e confiáveis sobre Java e Spring Boot.
2. **Experimentos de prompts** — Testar e documentar diferentes estratégias de engenharia de prompts no NotebookLM para revisão de conceitos.
3. **Registro de cicatrizes** — Documentar dificuldades reais encontradas durante o processo e as soluções encontradas.
4. **Miniguia de estudo** — Produzir um miniguia conciso e didático que summarize os principais tópicos.
5. **Glossário de termos** — Consolidar definições dos termos técnicos mais relevantes.
6. **Prompts reutilizáveis** — Criar prompts que possam ser usados futuramente para revisão e teste de conhecimento.

## Conhecimentos a Consolidar

> **Nota:** Este material é baseado em Spring Boot 3.x, a versão LTS mais recente do ecossistema Spring.

- Java aplicado ao back-end (sintaxe avançada, features modernas);
- Spring Framework — Inversão de controle e injeção de dependência;
- Spring Boot — inicialização acelerada, auto-configuração;
- Arquitetura em camadas — separação de responsabilidades;
- Controller — recebimento e roteamento de requisições HTTP;
- Service — lógica de negócio, validação e coordenação;
- Repository — abstração de acesso a dados;
- REST — princípios arquiteturais, métodos HTTP, códigos de status;
- DTOs — transferência de dados entre camadas;
- Validação — anotações de constraint, feedback ao cliente;
- Tratamento de exceções — handlers global, respostas de erro consistentes;
- Spring Data JPA — mapeamento objeto-relacional, consultas;
- Persistência — entidade, tabela, chaves estrangeiras;
- Boas práticas de API — versionamento, documentação;
- Testes — unidade e integração com Spring Test;

## Como o NotebookLM será usado como ferramenta de aprendizagem ativa

O NotebookLM será utilizado da seguinte forma:

1. **Síntese de fontes** — alimentar o NotebookLM com documentos oficiais e artigos sobre cada tópico, pedindo resumos executivos e exemplos de código simplificados.
2. **Geração de perguntas de revisão** — utilizar prompts específicos para que o modelo gere perguntas e gabaritos sobre cada conceito.
3. **Comparação de conceitos** — solicitar comparações entre abordagens (ex: Controller vs Service responsibilities, JPA vs JDBC).
4. **Identificação de lacunas** — pedir ao modelo que identifique o que ainda não foi compreendido profundamente, baseando-se apenas nas fontes fornecidas.
5. **Mapas de estudo** — gerar esquemas hierárquicos ou mind maps conceituais a partir dos textos alimentados.
6. **Revisão espaçada** — criar perguntas variadas sobre o mesmo tema em sessões diferentes para reforçar a memorização.

O fluxo adotado não consiste em confiar cegamente nas respostas do modelo, mas sim usá-lo como facilitador: as fontes permanecem como autoridade última, e as saídas do NotebookLM são validadas contra a documentação oficial e o código-funcionante.

---

**Fonte do desafio:** DIO - Desafio Aprendizagem Ativa com NotebookLM