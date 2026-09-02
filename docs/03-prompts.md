# Engenharia de Prompts no NotebookLM

Este documento registra a estratégia e os resultados dos experimentos de prompts realizados no NotebookLM. O objetivo é testar diferentes abordagens de engenharia de prompts para revisão de conceitos, identificação de lacunas e geração de material de estudo a partir das fontes curadas.

## Estratégia de Experimentação

Os prompts foram desenhados para cobrir diferentes finalidades de estudo, todas baseadas exclusivamente nas 5 fontes curadas (Spring Boot Docs, Spring Guides, Java Docs, Spring Data JPA, Spring Web Client). Nenhuma resposta deve sair do escopo das fontes fornecidas.

---

## PROMPT 1 — Visão Geral

**Prompt original:**
> "Com base exclusivamente nas fontes fornecidas, explique os principais conceitos de Spring Boot necessários para desenvolver uma API REST."

**Objetivo:** Obter um resumo de alto nível dos conceitos essenciais.

---

## PROMPT 2 — Estrutura de Aprendizagem

**Prompt original:**
> "Organize os conceitos de desenvolvimento de APIs REST com Spring Boot em uma sequência de aprendizado do básico ao intermediário."

**Objetivo:** Obter um roadmap de estudo ordenado.

---

## PROMPT 3 — Comparação de Camadas

**Prompt original:**
> "Explique as responsabilidades das camadas Controller, Service e Repository e compare o papel de cada uma."

**Objetivo:** Comparar as três camadas centrais da arquitetura em Spring Boot.

---

## PROMPT 4 — Revisão com Perguntas

**Prompt original:**
> "Crie perguntas de revisão sobre os principais conceitos apresentados nas fontes e depois forneça um gabarito comentado."

**Objetivo:** Gerar perguntas de auto-revisão com gabaritos.

---

## PROMPT 5 — Identificação de Lacunas

**Prompt original:**
> "Com base nas fontes, identifique conceitos importantes sobre APIs REST com Spring Boot que ainda não foram abordados nesta conversa."

**Objetivo:** Descobrir o que pode ter sido esquecido ou subrepresentado.

---

## Formato dos Experimentos

Para cada experimento, o fluxo seguido foi:

1. **Apresentar o prompt** para o NotebookLM (com as 5 fontes carregadas).
2. **Executar no NotebookLM** — o usuário (você) roda o prompt na interface.
3. **Receber a resposta** — documentar o resultado obtido.
4. **Documentar o resultado** — registrar o que foi retornado.
5. **Analisar a qualidade** — avaliar se a resposta atende ao prompt, se usa as fontes, se é clara.
6. **Identificar limitações** — quais problemas foram observados (genérico, longa, falta de referência, etc.).
7. **Propor versão melhorada** — refinar o prompt para melhorar o resultado.
8. **Testar a versão melhorada** — executar o novo prompt e comparar.
9. **Comparar resultados** — analisar o que melhorou (ou piorou).

---

## Registros de Experimentos

### Experimento 1: Prompt 1 — Visão Geral

- **Status:** Executado ✅
- **Prompt:** "Com base exclusivamente nas fontes fornecidas, explique os principais conceitos de Spring Boot necessários para desenvolver uma API REST."
- **Objetivo:** Resumo de alto nível dos conceitos essenciais
- **Resultado obtido:** Resposta extensa (cerca de 2.000 palavras), dividida em 4 pilares:
  1. Inicialização e Configuração (IoC, Injeção de Dependência, `@SpringBootApplication`, Auto-configuração, Starters)
  2. Desenvolvimento de Endpoints (Spring MVC, Controllers, `@RequestBody`, `@RequestParam`, Jackson JSON, Validação, Exceções, CORS)
  3. Persistência de Dados (Spring Data JPA, Repositórios, `@Query`, SQL/NoSQL)
  4. Consumo de APIs (RestTemplate, WebClient)
- **Análise de qualidade:**
  - **Fidelidade às fontes:** Boa — conceitos como auto-configuração, Controllers e Spring Data JPA estão bem representados nas fontes curadas.
  - **Clareza:** Média — texto longo e técnico, com many sub-bullets. Difícil de absorver como "visão geral".
  - **Completude:** Alta — cobre a maioria dos conceitos pedidos, mas não menciona DTOs, camada de Service isoladamente, ou métodos HTTP específicos (GET, POST, PUT, DELETE).
  - **Utilidade prática:** Média — bom material para aprofundamento, mas excessivamente denso para uma introdução.
  - **Formato:** Seguiu o formato solicitado (explicação textual), mas não foi conciso como esperado para um "visão geral".
- **Limitações identificadas:**
  - Resposta muito longa para um prompt que pede "visão geral"
  - Não menciona a arquitetura em camadas (Controller → Service → Repository) explicitamente como conceito estrutural
  - Não inclui DTOs (Data Transfer Objects) como conceito importante
  - Cita WebFlux (pilha reativa) — possivelmente fora do escopo básico de "API REST com Spring Boot"
  - Não apresenta exemplos de código ou snippets curtos
  - Não lista métodos HTTP nem códigos de status
- **Prompt melhorado proposto:**
  > "Com base exclusivamente nas fontes fornecidas, crie uma lista resumida (máximo 10 itens) dos conceitos essenciais de Spring Boot para criar uma API REST. Para cada conceito, inclua uma definição de uma linha e um exemplo de anotação ou classe quando aplicável."
- **Resultado após mudança:** Lista de exatamente 10 conceitos, cada um com definição de uma linha e anotação/classe de exemplo:
  1. `@SpringBootApplication` — inicialização
  2. `@Autowired` — injeção de dependências
  3. `@Configuration` — classes de configuração
  4. `@Controller` — controllers anotados
  5. `@RequestBody` — leitura do corpo da requisição
  6. `@ResponseBody` — escrita do corpo da resposta
  7. `ResponseEntity` — controle completo de respostas
  8. `@RequestParam` — extração de parâmetros da URL
  9. `@Query` — camada de repositório JPA
  10. `WebClient` — cliente HTTP reativo

- **Comparação Original vs Melhorado:**

| Aspecto | Prompt Original | Prompt Melhorado |
|---------|-----------------|------------------|
| Tamanho da resposta | ~2.000 palavras | ~300 palavras |
| Formato | 4 pilares com sub-bullets | Lista de 10 itens |
| Definições | Longas e detalhadas | Concisas (uma linha) |
| Exemplos | Nenhum | Anotação/classe para cada item |
| Foco | Abrangente (inclui WebFlux) | Apenas essenciais para REST |
| Usabilidade para estudo | Densa, difícil de revisar | Rápida de revisar e memorizar |

- **Melhoria observada:** O prompt melhorado produziu uma resposta 6x mais concisa, com formato de lista (mais fácil de revisar) e exemplos práticos de anotações. A imposição de "máximo 10 itens" e "definição de uma linha" foi decisiva para controlar a extensão da resposta.
- **Aprendizado:** Prompts que pedem "visão geral" devem impor limites claros (número de itens, tamanho da resposta, formato). Caso contrário, o NotebookLM tende a gerar respostas completas e extensas, o que é útil para estudo profundo, mas não para síntese inicial. A restrição de formato (lista, X itens, Y palavras) é a ferramenta mais poderosa para controlar a saída do modelo.

### Experimento 2: Prompt 2 — Estrutura de Aprendizagem

- **Status:** Executado ✅
- **Prompt:** "Organize os conceitos de desenvolvimento de APIs REST com Spring Boot em uma sequência de aprendizado do básico ao intermediário."
- **Objetivo:** Roadmap de estudo ordenado
- **Resultado obtido:** Resposta organizada em 2 fases:
  - **Fase 1 — Fundamentos e Configuração Inicial (Básico):** Instalação, Sistemas de Build, `@SpringBootApplication`, IoC/DI, `@Configuration`/`@Bean`, Controllers/`@RequestParam`
  - **Fase 2 — Desenvolvimento de APIs Robustas (Intermediário):** `@RequestBody`/`@ResponseBody`/`ResponseEntity`, Spring Data JPA, Validação (JSR-303), Tratamento de Exceções (Controller Advice), Configuração Externa/Profiles, Consumo de APIs (RestTemplate/WebClient), Spring Boot Actuator
- **Análise de qualidade:**
  - **Fidelidade às fontes:** Boa — conceitos alinhados com as 5 fontes curadas
  - **Clareza:** Alta — progressão lógica do básico ao intermediário
  - **Completude:** Média-alta — cobre a maioria dos conceitos, mas omite DTOs, testes e documentação (Swagger/OpenAPI)
  - **Utilidade prática:** Alta — pode ser usado como roteiro de estudo real
  - **Formato:** Seguiu o formato solicitado (sequência de aprendizado)
- **Limitações identificadas:**
  - Não menciona **DTOs** (Data Transfer Objects) como conceito de transferência de dados entre camadas
  - Não inclui **testes** (unidade e integração) como etapa de aprendizado
  - Não cita **documentação de API** (Swagger/OpenAPI) como ferramenta complementar
  - Não menciona **CORS** nem **versionamento de API**
  - As fases são amplas — poderiam ser mais granulares (ex: separar validação de tratamento de exceções)
- **Prompt melhorado proposto:**
  > "Organize os conceitos de desenvolvimento de APIs REST com Spring Boot em uma sequência de aprendizado em 3 fases: (1) Fundamentos, (2) Desenvolvimento, (3) Produção. Para cada fase, liste de 3 a 5 tópicos com uma descrição de uma linha cada. Inclua DTOs, testes e documentação."
- **Resultado após mudança:** Resposta organizada em 3 fases com 11 tópicos no total:
  - **Fase 1 — Fundamentos:** Build/Inicialização, IoC/DI, `@SpringBootApplication`, Controllers/`@RequestParam`
  - **Fase 2 — Desenvolvimento:** DTOs/Jackson, Validação (JSR-303), Spring Data JPA, Testes (MockMvc/WebTestClient/Testcontainers)
  - **Fase 3 — Produção:** Configuração Externa/Profiles, Actuator, Empacotamento/Docker/GraalVM, Documentação (Spring REST Docs)

- **Comparação Original vs Melhorado:**

| Aspecto | Prompt Original | Prompt Melhorado |
|---------|-----------------|------------------|
| Número de fases | 2 (Básico, Intermediário) | 3 (Fundamentos, Desenvolvimento, Produção) |
| Total de tópicos | 13 | 11 |
| DTOs | ❌ Não mencionado | ✅ Incluído explicitamente |
| Testes | ❌ Não mencionado | ✅ MockMvc, WebTestClient, Testcontainers |
| Documentação | ❌ Não mencionado | ✅ Spring REST Docs |
| Containerização | ❌ Não mencionado | ✅ Docker, Cloud Native Buildpacks, GraalVM |
| Granularidade | Fases amplas | Fases mais equilibradas |

- **Melhoria observada:** O prompt melhorado adicionou 3 conceitos ausentes (DTOs, testes, documentação) e organizou em 3 fases mais equilibradas. A inclusão de "Inclua DTOs, testes e documentação" no prompt foi decisiva para preencher lacunas.
- **Aprendizado:** Para prompts de roadmap, especificar o número de fases e incluir tópicos ausentes (DTOs, testes, documentação) melhora significativamente a completude da resposta. O NotebookLM responde bem a restrições estruturais (3 fases, 3-5 tópicos cada). Incluir tópicos ausentes diretamente no prompt ("Inclua X, Y e Z") é mais eficaz do que esperar que o modelo os identifique sozinho.

### Experimento 3: Prompt 3 — Comparação de Camadas

- **Status:** Executado ✅
- **Prompt:** "Explique as responsabilidades das camadas Controller, Service e Repository e compare o papel de cada uma."
- **Objetivo:** Comparar as três camadas centrais da arquitetura em Spring Boot
- **Resultado obtido:** Resposta dividida em 3 seções:
  1. **Controller (Web/HTTP Stack):** Mapeamento de requisições, extração de dados (`@RequestParam`, `@RequestBody`), manipulação de respostas (`@ResponseBody`, `ResponseEntity`), integração com Jackson JSON
  2. **Repository (Data Access Stack):** Abstração de acesso a dados via Spring Data JPA, redução de boilerplate, consultas customizadas (`@Query`), paginação e auditoria
  3. **Service:** Resposta identifica uma **lacuna nas fontes** — "as fontes fornecidas não definem nem descrevem as responsabilidades da camada Service ou de sua respectiva anotação (`@Service`)"
- **Análise de qualidade:**
  - **Fidelidade às fontes:** Alta — o modelo foi honesto ao identificar que as fontes não cobrem a camada Service
  - **Clareza:** Alta — explicações técnicas bem estruturadas
  - **Completude:** Média — Controller e Repository bem cobertos, mas Service incompleto por limitação das fontes
  - **Utilidade prática:** Média — útil para entender Controller e Repository, mas não explica o fluxo completo
  - **Formato:** Seguiu parcialmente — pediu comparação de 3 camadas, mas só comparou 2 por limitação das fontes
- **Limitações identificadas:**
  - **Lacuna crítica:** A camada Service não foi explicada porque as fontes curadas não a cobrem adequadamente
  - Não apresenta o **fluxo completo** (Controller → Service → Repository)
  - Não menciona **DTOs** como conceito de transferência entre camadas
  - Não inclui **exemplos de código** ou diagramas
  - A comparação ficou incompleta (só 2 das 3 camadas)
- **Prompt melhorado proposto:**
  > "Com base nas fontes fornecidas, explique as responsabilidades das camadas Controller, Service e Repository em uma API REST com Spring Boot. Para cada camada, inclua: (1) responsabilidade principal em uma frase, (2) anotações principais, (3) exemplo de código de uma linha. Se alguma camada não estiver bem coberta nas fontes, forneça uma definição geral baseada no padrão do Spring."
- **Resultado após mudança:** Resposta completa com 3 camadas explicadas, cada uma com: responsabilidade principal, anotações principais e exemplo de código:
  - **Controller:** Expõe endpoints HTTP, recebe requisições, valida dados, retorna respostas. Anotações: `@RestController`, `@RequestMapping`, `@RequestBody`, `@RequestParam`. Exemplo: `@PostMapping("/produtos") public ResponseEntity<Produto> criar(@RequestBody Produto p) { ... }`
  - **Service:** Centraliza regras de negócio (padrão geral, não coberto pelas fontes). Anotações: `@Service`, `@Transactional`. Exemplo: `@Transactional public Produto salvar(Produto p) { return repository.save(p); }`
  - **Repository:** Abstrai acesso a dados via Spring Data JPA. Anotações: `@Repository`, `@Query`. Exemplo: `public interface ProdutoRepository extends JpaRepository<Produto, Long> { @Query("SELECT p FROM Produto p WHERE p.nome = :nome") List<Produto> buscarPorNome(String nome); }`

- **Comparação Original vs Melhorado:**

| Aspecto | Prompt Original | Prompt Melhorado |
|---------|-----------------|------------------|
| Camadas explicadas | 2 (Controller, Repository) | 3 (Controller, Service, Repository) |
| Service layer | ❌ "Lacuna nas Fontes" | ✅ Definição geral + anotações |
| Exemplos de código | ❌ Nenhum | ✅ Um para cada camada |
| Estrutura | Texto descritivo | Responsabilidade + Anotações + Código |
| Fluidez do conteúdo | Técnico mas incompleto | Completo e didático |

- **Melhoria observada:** O prompt melhorado produziu uma resposta **significativamente mais completa**: explicou todas as 3 camadas, incluiu exemplos de código e manteve a honestidade sobre a lacuna nas fontes. A solicitação "Se alguma camada não estiver bem coberta nas fontes, forneça uma definição geral" foi decisiva para preencher a lacuna sem comprometer a autenticidade.
- **Aprendizado:** Quando o NotebookLM identifica uma lacuna nas fontes, ele é honesto e não inventa informações. Isso é positivo para autenticidade, mas limita a completude da resposta. O prompt melhorado solicita uma definição geral quando a fonte não cobre o tópico, forçando o modelo a preencher a lacuna com conhecimento geral do Spring. A estrutura "responsabilidade + anotações + código" melhora a usabilidade para estudo.

---

### Experimento 4: Prompt 4 — Revisão com Perguntas

- **Status:** Executado ✅
- **Prompt:** "Crie perguntas de revisão sobre os principais conceitos apresentados nas fontes e depois forneça um gabarito comentado."
- **Objetivo:** Gerar perguntas de auto-revisão com gabaritos
- **Resultado obtido:** 4 perguntas com gabarito detalhado:
  1. **Integração e Persistência:** Como o Spring Data JPA simplifica o acesso a dados e qual validação realiza na inicialização?
  2. **Clientes HTTP:** O que é o WebClient, em qual projeto está integrado e quais suas características?
  3. **Observabilidade:** Quais ferramentas o Spring Boot Actuator oferece para produção?
  4. **Empacotamento:** Quais tecnologias o Spring Boot oferece para empacotamento e imagens de contêiner?
- **Análise de qualidade:**
  - **Fidelidade às fontes:** Alta — respostas referenciam conceitos das 5 fontes curadas
  - **Clareza:** Alta — perguntas objetivas e respostas bem estruturadas
  - **Completude:** Média —only 4 perguntas, focadas em tópicos avançados
  - **Utilidade prática:** Média — boas para revisão, mas faltam perguntas básicas
  - **Formato:** Seguiu o formato solicitado (perguntas + gabarito)
- **Limitações identificadas:**
  - **Poucas perguntas** (apenas 4) — ideal seriam 6-8
  - **Foco em tópicos avançados** — não há perguntas sobre conceitos básicos (Controllers, Services, IoC)
  - **Sem perguntas sobre arquitetura em camadas** (Controller → Service → Repository)
  - **Sem perguntas sobre DTOs, validação ou tratamento de exceções**
  - **Sem variedade de formato** — todas são perguntas abertas, sem múltipla escolha ou verdadeiro/falso
- **Prompt melhorado proposto:**
  > "Crie 6 perguntas de revisão sobre os principais conceitos de Spring Boot para APIs REST. Distribua: 2 perguntas básicas (fundamentos), 2 intermediárias (desenvolvimento) e 2 avançadas (produção). Para cada pergunta, forneça um gabarito comentado de 2-3 linhas. Inclua pelo menos uma pergunta sobre a arquitetura em camadas (Controller/Service/Repository)."
- **Resultado após mudança:** 6 perguntas distribuídas em 3 fases, com gabarito comentado:
  - **Fase 1 — Fundamentos (Básicas):** Questão 1 (`@SpringBootApplication`), Questão 2 (Arquitetura em Camadas — Controller/Repository)
  - **Fase 2 — Desenvolvimento (Intermediárias):** Questão 3 (Spring Data JPA), Questão 4 (Testes — MockMvc/WebTestClient)
  - **Fase 3 — Produção (Avançadas):** Questão 5 (Spring Boot Actuator), Questão 6 (Empacotamento/GraalVM/Checkpoint)

- **Comparação Original vs Melhorado:**

| Aspecto | Prompt Original | Prompt Melhorado |
|---------|-----------------|------------------|
| Número de perguntas | 4 | 6 |
| Distribuição | Todas intermediárias/avançadas | 2 básicas + 2 intermediárias + 2 avançadas |
| Arquitetura em camadas | ❌ Não incluída | ✅ Questão 2 (Controller/Repository) |
| Testes | ❌ Não incluído | ✅ Questão 4 (MockMvc/WebTestClient) |
| Cobertura | Focada em tópicos avançados | Equilibrada (fundamentos → produção) |
| Estrutura | Perguntas soltas | Organizadas por fase |

- **Melhoria observada:** O prompt melhorado produziu **50% mais perguntas** (6 vs 4) com **distribuição equilibrada** por nível de dificuldade. A inclusão da Questão 2 sobre arquitetura em camadas atendeu diretamente ao pedido do prompt. A estrutura por fases facilita o uso como material de estudo progressivo.
- **Aprendizado:** Prompts de revisão funcionam melhor quando especificam: (1) número de perguntas, (2) distribuição por nível de dificuldade, (3) tópicos obrigatórios. Isso garante cobertura equilibrada dos conceitos fundamentais e avançados. A solicitação explícita "Inclua pelo menos uma pergunta sobre arquitetura em camadas" foi decisiva para preencher essa lacuna.

---

### Experimento 5: Prompt 5 — Identificação de Lacunas

- **Status:** Executado ✅
- **Prompt:** "Com base nas fontes, identifique conceitos importantes sobre APIs REST com Spring Boot que ainda não foram abordados nesta conversa."
- **Objetivo:** Descobrir o que pode ter sido esquecido ou subrepresentado
- **Resultado obtido:** 6 conceitos identificados como não abordados:
  1. **Spring Data REST** — exposição automática de repositórios como endpoints HTTP
  2. **Spring HATEOAS** — hypermedia como nível mais alto de maturidade REST
  3. **Segurança Avançada** — OAuth2 Resource Server, Authorization Server, SAML 2.0
  4. **Graceful Shutdown** — desligamento gracioso em ambientes de nuvem
  5. **CORS, Versionamento e HTTP Caching** — recursos embutidos nos controllers
  6. **Servidores Web Embutidos** — Tomcat, Jetty, Netty auto-configurados
- **Análise de qualidade:**
  - **Fidelidade às fontes:** Alta — conceitos reais do ecossistema Spring Boot
  - **Clareza:** Alta — explicações técnicas precisas
  - **Completude:** Alta — identificou lacunas reais nas conversas anteriores
  - **Utilidade prática:** Alta — material valioso para expansão do miniguia
  - **Formato:** Lista numerada com explicações detalhadas
- **Limitações identificadas:**
  - Alguns tópicos (OAuth2/SAML, HATEOAS) são avançados demais para o escopo básico do projeto
  - Não mencionou DTOs (já abordados no Prompt 2 melhorado)
  - Não mencionou Tratamento de Exceções (já abordado no Prompt 2)
- **Aprendizado:** O prompt de identificação de lacunas é extremamente útil para completar um miniguia. Ele revelou tópicos importantes que não foram cobertos nas conversas anteriores, permitindo decidir quais incluir na versão final do material de estudo. É recomendado usá-lo como etapa final de qualquer processo de estudo com NotebookLM.

---

## Resumo dos 5 Experimentos

| # | Prompt | Resultado | Melhoria Principal |
|---|--------|-----------|-------------------|
| 1 | Visão Geral | Lista de 10 conceitos | Reduziu de ~2.000 para ~300 palavras |
| 2 | Estrutura de Aprendizagem | 3 fases com 11 tópicos | Adicionou DTOs, testes, documentação |
| 3 | Comparação de Camadas | 3 camadas completas | Preencheu lacuna do Service layer |
| 4 | Revisão com Perguntas | 6 perguntas equilibradas | Distribuição por nível de dificuldade |
| 5 | Identificação de Lacunas | 6 tópicos não abordados | Completou lacunas do estudo |

**Conclusão geral:** A engenharia de prompts é uma etapa essencial. Prompts bem estruturados com restrições claras (número de itens, formato, tópicos obrigatórios) produzem respostas significativamente mais úteis para estudo.

---

## Critérios de Qualidade

Para cada resposta gerada pelo NotebookLM, avaliamos os seguintes aspectos:

| Critério | O que verificamos |
|----------|-------------------|
| **Fidelidade às fontes** | A resposta cita ou se baseia corretamente nos documentos carregados, ou alucina/cria informações fora do escopo? |
| **Clareza** | O texto é fácil de ler? As definições são claras ou ambiguas? |
| **Completude** | Os conceitos solicitados são abordados de forma adequada, ou ficam de fora itens essenciais? |
| **Utilidade prática** | O resultado pode ser usado diretamente para estudo, ou precisa de edição significativa? |
| **Formato solicitado** | Se o pedido pedia tabela, tópicos ou comparação, o modelo seguiu o formato? |

---

## Próximos Passos

1. **Executar os prompts no NotebookLM** — com as 5 fontes carregadas, testar cada um dos 5 prompts principais.
2. **Preencher os registros** — após cada execução, preencher os campos de resultado, análise, limitações e melhorias.
3. **Iterar** — versões melhoradas dos prompts serão testadas e documentadas.
4. **Inserir no miniguia** — prompts reutilizáveis que funcionaram bem serão adicionados à seção final do caderno.

---

**Observação importante:** Nenhuma resposta deve ser dada como "verdade absoluta". O NotebookLM é uma ferramenta de síntese baseada nos documentos fornecidos, e todas as informações devem ser contrastadas com as fontes originais (Spring Docs, Java Docs, etc.).