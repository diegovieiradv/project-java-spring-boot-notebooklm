# Caderno de Estudos: Java e Spring Boot com NotebookLM

## Sobre o Projeto

Um caderno temático para consolidação de conhecimentos em Java e Spring Boot aplicados ao desenvolvimento de APIs REST, utilizando o NotebookLM como ferramenta de aprendizagem ativa. Este projeto foi desenvolvido como parte do desafio da DIO (Digital Innovation One).

---

## Objetivo

Consolidar conhecimentos fundamentais de Java e Spring Boot para APIs REST por meio de um caderno estruturado, com curadoria de fontes, experimentos de engenharia de prompts, documentação de dificuldades e um miniguia de estudo reutilizável.

---

## Tema Escolhido

**Java e Spring Boot para Desenvolvimento de APIs REST**

O tema responde à demanda prática de desenvolvedores que precisam dominar o ecossistema Spring Boot para criar APIs robustas, escaláveis e seguras. O caderno cobre desde fundamentos (IoC, Controllers, Services) até tópicos avançados (persistência com JPA, validação, tratamento de erros).

---

## Ferramentas Utilizadas

| Ferramenta | Uso no Projeto |
|------------|----------------|
| NotebookLM | Aprendizagem ativa, síntese de fontes, geração de perguntas |
| Git | Controle de versão e histórico de mudanças |
| GitHub | Repositório remoto e portfólio |
| Markdown | Formatação de todos os documentos |
| Java | Linguagem de programação |
| Spring Boot | Framework para desenvolvimento de APIs REST |

---

## Contexto e Objetivos

O projeto foi estruturado em 10 etapas, seguindo o fluxo: analisar, planejar, executar, revisar, commitar. Cada etapa foi documentada separadamente.

**Objetivos específicos:**
1. Curadoria de 3 a 5 fontes abertas e confiáveis
2. Experimentos de engenharia de prompts no NotebookLM
3. Documentação de cicatrizes (dificuldades reais)
4. Miniguia de estudo com conceitos fundamentais
5. Glossário de termos técnicos
6. Prompts reutilizáveis para estudo contínuo

---

## Curadoria de Fontes

5 fontes oficiais e confiáveis foram selecionadas:

| # | Fonte | Tema Principal |
|---|-------|----------------|
| 1 | Spring Boot Docs | Auto-configuração, aplicação completa |
| 2 | Spring Guides | RESTful Web Service do zero |
| 3 | Java Docs | Fundamentos modernos da linguagem |
| 4 | Spring Data JPA | JPA, Repository, consultas |
| 5 | Spring Web Client | Consumir APIs REST externas |

📄 [Ver curadoria completa](docs/02-fontes.md)

---

## Experimentos com Prompts

5 prompts foram testados e documentados, cada um com versão original e melhorada:

| # | Prompt | Resultado Original | Resultado Melhorado |
|---|--------|-------------------|---------------------|
| 1 | Visão Geral | Resposta de ~2.000 palavras | Lista de 10 conceitos (~300 palavras) |
| 2 | Estrutura de Aprendizado | 2 fases, sem DTOs/testes | 3 fases com DTOs, testes, documentação |
| 3 | Comparação de Camadas | 2 camadas (Service ausente) | 3 camadas completas |
| 4 | Revisão com Perguntas | 4 perguntas avançadas | 6 perguntas equilibradas |
| 5 | Identificação de Lacunas | 6 tópicos não abordados | Material para expansão do miniguia |

📄 [Ver experimentos completos](docs/03-prompts.md)

---

## Principais Cicatrizes e Aprendizados

6 dificuldades reais foram documentadas durante o processo:

1. **Resposta extensa demais** → Impor limites claros (nº de itens, tamanho)
2. **Ausência de tópicos essenciais** → Solicitar explicitamente no prompt
3. **Lacuna nas fontes sobre Service** → Pedir "definição geral" quando há lacuna
4. **Poucas perguntas de revisão** → Especificar nº e distribuição
5. **Resposta muito técnica** → Definir o público-alvo
6. **Formato inadequado** → Especificar formato desejado (tabela, lista)

📄 [Ver troubleshoot completo](docs/04-troubleshooting.md)

---

## Miniguia

A miniguia consolida todos os conceitos fundamentais em 15 seções:

1. Introdução
2. O que é Spring Boot
3. Estrutura de uma API REST
4. Controller
5. Service
6. Repository
7. DTOs
8. Validação
9. Tratamento de erros
10. Persistência com JPA
11. Boas práticas
12. Resumo para revisão
13. Glossário
14. Perguntas de revisão
15. Prompts reutilizáveis

📄 [Ver miniguia completa](docs/05-miniguia.md)

---

## Glossário

16 termos essenciais documentados, incluindo: API, REST, Endpoint, Controller, Service, Repository, DTO, Entity, JPA, ORM, Dependency Injection, Bean, HTTP, JSON, Validation, Exception Handler.

📄 [Ver glossário na miniguia](docs/05-miniguia.md#13-glossário)

---

## Prompts Reutilizáveis

6 prompts estruturados para uso futuro:

1. Visão Geral (lista resumida de conceitos)
2. Estrutura de Aprendizado (roadmap progressivo)
3. Comparação (camadas ou tecnologias)
4. Revisão com Perguntas (distribuídas por nível)
5. Identificação de Lacunas (completar estudo)
6. Glossário (termos e definições)

📄 [Ver prompts na miniguia](docs/05-miniguia.md#15-prompts-reutilizáveis)

---

## Estrutura do Repositório

```
java-spring-boot-notebooklm/
├── README.md                          # Este arquivo
├── docs/
│   ├── 01-contexto-e-objetivos.md     # Contexto do desafio e objetivos
│   ├── 02-fontes.md                   # Curadoria de 5 fontes
│   ├── 03-prompts.md                  # 5 experimentos de prompts
│   ├── 04-troubleshooting.md          # 6 cicatrizes documentadas
│   └── 05-miniguia.md                 # Miniguia de estudo completa
├── assets/
│   └── imagens/                       # Imagens do projeto
└── .gitignore                         # Ignorados: IDE, logs, binários
```

---

## Como Reproduzir o Estudo

1. **Clonar o repositório:**
   ```bash
   git clone https://github.com/SEU-UARIO/java-spring-boot-notebooklm.git
   ```

2. **Criar notebook no NotebookLM:**
   - Acesse [NotebookLM](https://notebooklm.google.com/)
   - Crie um novo caderno
   - Adicione as 5 fontes listadas em `docs/02-fontes.md`

3. **Executar os prompts:**
   - Siga os 5 prompts documentados em `docs/03-prompts.md`
   - Teste as versões melhoradas
   - Compare os resultados

4. **Documentar suas próprias cicatrizes:**
   - Registre dificuldades encontradas
   - Siga o formato de `docs/04-troubleshooting.md`

5. **Usar a miniguia para revisão:**
   - Revise os 10 conceitos essenciais
   - Teste-se com as perguntas de revisão
   - Use os prompts reutilizáveis para novos estudos

---

## Aprendizados

- **Engenharia de prompts é essencial:** Prompts bem estruturados produzem respostas significativamente mais úteis
- **Restrições melhoram a qualidade:** Número de itens, formato e tópicos obrigatórios controlam a saída do modelo
- **O NotebookLM é honesto:** Quando há lacunas nas fontes, ele identifica e não inventa informações
- **Iteração é necessária:** A primeira versão de um prompt raramente é a melhor
- **Documentação autêntica:** Registrar dificuldades reais é mais valioso que uma narrativa perfeita

---

## Status do Projeto

| Etapa | Status |
|-------|--------|
| Inicialização | Concluída |
| Contexto e Objetivos | Concluída |
| Curadoria de Fontes | Concluída |
| Engenharia de Prompts | Concluída |
| Troubleshooting | Concluída |
| Miniguia | Concluída |
| Glossário | Concluído |
| Prompts Reutilizáveis | Concluídos |
| README Premium | Concluído |
| Auditoria Final | Concluída |

---

## Autor

Projeto desenvolvido para o desafio da DIO — Aprendizagem Ativa com NotebookLM.