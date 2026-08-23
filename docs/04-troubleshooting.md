# Cicatrizes / Troubleshooting — Engenharia de Prompts

Este documento registra as dificuldades reais encontradas durante os experimentos de prompts no NotebookLM. Cada problema é documentado com o prompt utilizado, o resultado observado, a hipótese da causa, a alteração feita e o aprendizado obtido.

---

## Cicatriz 1: Resposta Extensa Demais

**Problema:** O NotebookLM gerou uma resposta de ~2.000 palavras quando o usuário solicitou uma "visão geral" dos conceitos de Spring Boot.

**Prompt utilizado:**
> "Com base exclusivamente nas fontes fornecidas, explique os principais conceitos de Spring Boot necessários para desenvolver uma API REST."

**Resultado observado:** Resposta dividida em 4 pilares com muitos sub-bullets, muito densa para吸收ção inicial.

**Hipótese da causa:** O prompt não impunha limites claros de tamanho ou formato. O NotebookLM tende a gerar respostas completas e detalhadas quando não há restrições.

**Alteração feita:** Reescrever o prompt com restrições explícitas:
> "Com base exclusivamente nas fontes fornecidas, crie uma lista resumida (máximo 10 itens) dos conceitos essenciais de Spring Boot para criar uma API REST. Para cada conceito, inclua uma definição de uma linha e um exemplo de anotação ou classe quando aplicável."

**Novo prompt:** (utilizado no Experimento 1 melhorado)

**Resultado após a mudança:** Resposta de ~300 palavras, formato de lista com 10 itens, cada um com definição de uma linha e exemplo de anotação. Redução de 85% no tamanho.

**Aprendizado obtido:** Prompts que pedem "visão geral", "resumo" ou "introdução" devem impor limites claros (número de itens, tamanho da resposta, formato). Caso contrário, o modelo gera respostas extensas que são úteis para aprofundamento, mas não para síntese.

---

## Cicatriz 2: Ausência de Tópicos Essenciais

**Problema:** O NotebookLM não incluiu DTOs (Data Transfer Objects) em nenhuma das respostas iniciais, apesar de ser um conceito essencial para transferência de dados entre camadas em APIs REST com Spring Boot.

**Prompt utilizado:**
> "Organize os conceitos de desenvolvimento de APIs REST com Spring Boot em uma sequência de aprendizado do básico ao intermediário."

**Resultado observado:** Roadmap com 2 fases e 13 tópicos, mas sem menção a DTOs.

**Hipótese da causa:** As fontes curadas (Spring Boot Docs, Spring Guides, etc.) talvez não abordem DTOs explicitamente, ou o modelo priorizou outros conceitos mais "oficiais" nas fontes.

**Alteração feita:** Incluir a solicitação explícita de DTOs no prompt:
> "...Inclua DTOs, testes e documentação."

**Novo prompt:** (utilizado no Experimento 2 melhorado)

**Resultado após a mudança:** O prompt melhorado incluiu DTOs explicitamente na Fase 2 — Desenvolvimento, com a anotação `@RequestBody` e `@ResponseBody` associadas.

**Aprendizado obtido:** Quando um conceito é essencial mas pode não estar bem coberto nas fontes, é mais eficaz solicitar explicitamente sua inclusão no prompt ("Inclua X, Y e Z") do que esperar que o modelo o identifique sozinho.

---

## Cicatriz 3: Lacuna nas Fontes sobre Service Layer

**Problema:** O NotebookLM não conseguiu explicar a camada Service porque as fontes curadas não a cobrem adequadamente. O modelo foi honesto e identificou a lacuna, mas a resposta ficou incompleta.

**Prompt utilizado:**
> "Explique as responsabilidades das camadas Controller, Service e Repository e compare o papel de cada uma."

**Resultado observado:** Resposta detalhada sobre Controller e Repository, mas para Service: "Lacuna nas Fontes — o material fornecido não cobre a definição de uma camada Service".

**Hipótese da causa:** As 5 fontes curadas (Spring Boot Docs, Spring Guides, Java Docs, Spring Data JPA, Spring Web Client) focam em como usar as ferramentas, mas não explicam explicitamente a arquitetura em camadas (Controller → Service → Repository).

**Alteração feita:** Solicitar uma definição geral quando a fonte não cobre o tópico:
> "Se alguma camada não estiver bem coberta nas fontes, forneça uma definição geral baseada no padrão do Spring."

**Novo prompt:** (utilizado no Experimento 3 melhorado)

**Resultado após a mudança:** O modelo explicou a camada Service com base no "padrão geral adotado pelo ecossistema Spring", incluindo `@Service` e `@Transactional`, e manteve a honestidade sobre a lacuna nas fontes.

**Aprendizado obtido:** O NotebookLM é honesto quando identifica lacunas nas fontes — isso é positivo para autenticidade. O prompt pode solicitar uma "definição geral" quando a fonte não cobre o tópico, forçando o modelo a preencher a lacuna com conhecimento geral sem comprometer a honestidade.

---

## Cicatriz 4: Poucas Perguntas e Foco em Tópicos Avançados

**Problema:** O NotebookLM gerou apenas 4 perguntas de revisão, todas focadas em tópicos intermediários e avançados, sem perguntas sobre conceitos básicos.

**Prompt utilizado:**
> "Crie perguntas de revisão sobre os principais conceitos apresentados nas fontes e depois forneça um gabarito comentado."

**Resultado observado:** 4 perguntas sobre Spring Data JPA, WebClient, Spring Boot Actuator e empacotamento. Nenhuma sobre Controllers, Services, IoC ou arquitetura em camadas.

**Hipótese da causa:** O prompt não especificou número de perguntas nem distribuição por nível de dificuldade. O modelo priorizou tópicos mais "avançados" das fontes.

**Alteração feita:** Especificar número de perguntas, distribuição e tópicos obrigatórios:
> "Crie 6 perguntas de revisão sobre os principais conceitos de Spring Boot para APIs REST. Distribua: 2 perguntas básicas (fundamentos), 2 intermediárias (desenvolvimento) e 2 avançadas (produção). Para cada pergunta, forneça um gabarito comentado de 2-3 linhas. Inclua pelo menos uma pergunta sobre a arquitetura em camadas (Controller/Service/Repository)."

**Novo prompt:** (utilizado no Experimento 4 melhorado)

**Resultado após a mudança:** 6 perguntas distribuídas em 3 fases (2 básicas, 2 intermediárias, 2 avançadas), incluindo uma pergunta sobre arquitetura em camadas.

**Aprendizado obtido:** Prompts de revisão funcionam melhor quando especificam: (1) número de perguntas, (2) distribuição por nível de dificuldade, (3) tópicos obrigatórios. A solicitação explícita de tópicos ausentes ("Inclua pelo menos uma pergunta sobre X") é decisiva.

---

## Cicatriz 5: Resposta Muito Técnica para Iniciantes

**Problema:** Algumas respostas do NotebookLM são excessivamente técnicas e usam termos que podem não ser familiares para quem está começando (ex: "pilha Servlet", "Reactor", "codecs").

**Prompt utilizado:** Diversos prompts ao longo dos experimentos.

**Resultado observado:** Termos como "pilha reativa não-bloqueante", "Project Reactor", "codecs", "bootstrapping" apareceram sem explicação prévia.

**Hipótese da causa:** O NotebookLM assume que o público-alvo tem familiaridade com o ecossistema Spring, mesmo quando o prompt não especifica o nível de conhecimento.

**Alteração feita:** Não implementada diretamente — seria necessário adicionar ao prompt uma instrução como "Explique como se o leitor fosse um desenvolvedor Java iniciante em Spring Boot".

**Novo prompt:** (não testado nesta iteração)

**Resultado após a mudança:** [Não testado]

**Aprendizado obtido:** Para público iniciante, é importante especificar o nível de conhecimento no prompt. O NotebookLM adapta a linguagem ao público solicitado.

---

## Cicatriz 6: Formato de Resposta Inadequado

**Problema:** O NotebookLM às vezes gera respostas em formato textual longo quando o ideal seria tabela, lista ou comparação lado a lado.

**Prompt utilizado:** Diversos prompts ao longo dos experimentos.

**Resultado observado:** Perguntas que pediam "compare" geraram parágrafos descritivos em vez de tabelas comparativas.

**Hipótese da causa:** O prompt não especificou o formato desejado (tabela, lista, etc.).

**Alteração feita:** Incluir especificação de formato nos prompts melhorados (ex: "liste em formato de tabela", "crie uma lista numerada").

**Novo prompt:** (implementado nos prompts melhorados)

**Resultado após a migrationBuilder:** Respostas em formato de lista ou tabela quando solicitado.

**Aprendizado obtido:** O formato da resposta é tão importante quanto o conteúdo. Sempre especificar o formato desejado (tabela, lista, comparação lado a lado, etc.) para garantir usabilidade.

---

## Resumo dos Aprendizados

| # | Aprendizado | Aplicação |
|---|-------------|-----------|
| 1 | Impor limites claros (nº de itens, tamanho) | Sempre que pedir "visão geral" ou "resumo" |
| 2 | Solicitar explicitamente tópicos essenciais | Quando um conceito é importante mas pode não estar nas fontes |
| 3 | Pedir "definição geral" quando há lacuna | Quando o modelo identifica lacuna nas fontes |
| 4 | Especificar nº de perguntas e distribuição | Para prompts de revisão e teste |
| 5 | Definir o público-alvo no prompt | Quando o material é para iniciantes |
| 6 | Especificar o formato da resposta | Sempre que o formato for importante |

---

**Nota:** Este documento será atualizado a cada novo experimento que revelar uma dificuldade relevante. O objetivo é criar um registro autêntico do processo de aprendizagem, incluindo erros e correções.