# Miniguia — Java e Spring Boot para APIs REST

Guia de estudo consolidado a partir de experimentos reais com NotebookLM. Conteúdo baseado nas 5 fontes curadas e validado por engenharia de prompts.

---

## 1. Introdução

Esta miniguia consolida os fundamentos de Java e Spring Boot aplicados ao desenvolvimento de APIs REST. O material foi construído a partir de:

- 5 fontes oficiais e confiáveis (Spring Boot Docs, Spring Guides, Java Docs, Spring Data JPA, Spring Web Client)
- 5 experimentos de engenharia de prompts no NotebookLM
- 6 cicatrizes documentadas (dificuldades e soluções reais)

O objetivo é fornecer um material de estudo conciso, didático e tecnicamente correto para desenvolvedores que querem dominar o desenvolvimento de APIs REST com Spring Boot.

---

## 2. O que é Spring Boot

Spring Boot é um framework baseado no Spring Framework que simplifica a criação de aplicações Java, especialmente APIs REST e microserviços.

**Características principais:**
- Auto-configuração — configura componentes automaticamente com base nas dependências
- Starters — agrupam dependências essenciais para cenários específicos
- Servidor embutido — Tomcat, Jetty ou Netty já inclusos
- Produção pronta — inclui métricas, health checks e monitoramento

**Anotação principal:**
```java
@SpringBootApplication // Combina @Configuration, @EnableAutoConfiguration, @ComponentScan
public class MinhaApiApplication {
    public static void main(String[] args) {
        SpringApplication.run(MinhaApiApplication.class, args);
    }
}
```

---

## 3. Estrutura de uma API REST

Uma API REST em Spring Boot segue uma arquitetura em camadas:

```
Requisição HTTP
    ↓
Controller (recebe e roteia)
    ↓
Service (lógica de negócio)
    ↓
Repository (acesso a dados)
    ↓
Banco de Dados
```

Cada camada tem responsabilidades claras e deve ser isolada das outras.

---

## 4. Controller

**Responsabilidade:** Receber requisições HTTP, extrair dados, validar entrada e retornar respostas.

**Anotações principais:**
- `@RestController` — combina @Controller + @ResponseBody
- `@RequestMapping` — mapeia URLs para métodos
- `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping` — métodos HTTP específicos
- `@RequestBody` — converte JSON do corpo da requisição em objeto Java
- `@RequestParam` — extrai parâmetros da query string
- `@PathVariable` — extrai variáveis da URL (ex: /usuarios/{id})

**Exemplo:**
```java
@RestController
@RequestMapping("/api/usuarios")
public class UsuarioController {

    @PostMapping
    public ResponseEntity<Usuario> criar(@RequestBody @Valid UsuarioDTO dto) {
        Usuario salvo = service.salvar(dto);
        return ResponseEntity.status(HttpStatus.CREATED).body(salvo);
    }

    @GetMapping("/{id}")
    public ResponseEntity<Usuario> buscarPorId(@PathVariable Long id) {
        return ResponseEntity.ok(service.buscarPorId(id));
    }
}
```

**Boas práticas:**
- Use DTOs para entrada/saída, nunca entidades diretamente
- Valide dados de entrada com `@Valid`
- Retorne códigos HTTP apropriados (201 para criação, 204 para exclusão)
- Use `ResponseEntity` para controle completo da resposta

---

## 5. Service

**Responsabilidade:** Centralizar regras de negócio, coordenar comunicação entre Controller e Repository, gerenciar transações.

**Anotações principais:**
- `@Service` — indica classe de serviço no container IoC
- `@Transactional` — gerencia transações de banco de dados

**Exemplo:**
```java
@Service
@Transactional
public class UsuarioService {

    @Autowired
    private UsuarioRepository repository;

    public Usuario salvar(UsuarioDTO dto) {
        // Validações de negócio aqui
        Usuario entidade = new Usuario();
        entidade.setNome(dto.getNome());
        entidade.setEmail(dto.getEmail());
        return repository.save(entidade);
    }

    public Usuario buscarPorId(Long id) {
        return repository.findById(id)
            .orElseThrow(() -> new ResourceNotFoundException("Usuário não encontrado"));
    }
}
```

**Boas práticas:**
- Não acesse banco de dados diretamente no Controller
- Use `@Transactional` em métodos que fazem múltiplas operações
- Valide regras de negócio antes de persistir
- Lance exceções específicas para erros de negócio

---

## 6. Repository

**Responsabilidade:** Abstrair acesso a dados, eliminar código repetitivo, gerenciar persistência.

**Anotações principais:**
- `@Repository` — indica componente de acesso a dados
- `@Query` — consultas SQL/JPQL customizadas

**Exemplo:**
```java
public interface UsuarioRepository extends JpaRepository<Usuario, Long> {

    // Consulta derivada pelo nome do método
    List<Usuario> findByNome(String nome);

    // Consulta customizada com @Query
    @Query("SELECT u FROM Usuario u WHERE u.email = :email")
    Optional<Usuario> findByEmail(@Param("email") String email);

    // Consulta nativa
    @Query(value = "SELECT * FROM usuarios WHERE ativo = true", nativeQuery = true)
    List<Usuario> findAtivos();
}
```

**Funcionalidades do Spring Data JPA:**
- Paginação: `Pageable` e `Page<T>`
- Ordenação: `Sort`
- Validação automática de `@Query` na inicialização
- Implementação automática de métodos de consulta

---

## 7. DTOs (Data Transfer Objects)

**Responsabilidade:** Transferir dados entre camadas sem expor entidades diretamente.

**Por que usar DTOs:**
- Separação de responsabilidades (entidade ≠ representação de API)
- Segurança (não expor campos sensíveis como senhas)
- Flexibilidade (formato de entrada pode ser diferente da saída)
- Validação isolada por contexto

**Exemplo:**
```java
// DTO de entrada
@Data
public class UsuarioDTO {
    @NotBlank(message = "Nome é obrigatório")
    private String nome;

    @Email(message = "Email inválido")
    private String email;
}

// DTO de saída
@Data
public class UsuarioResponseDTO {
    private Long id;
    private String nome;
    private String email;
    private LocalDateTime criadoEm;
}
```

---

## 8. Validação

**Responsabilidade:** Garantir que dados de entrada atendam a regras antes de serem processados.

**Anotações principais (JSR-303 / Bean Validation):**
- `@NotNull` — valor não pode ser nulo
- `@NotBlank` — string não pode ser vazia ou só espaços
- `@Size(min, max)` — tamanho mínimo e máximo
- `@Min(value)` / `@Max(value)` — valores numéricos
- `@Email` — formato de email válido
- `@Past` / `@Future` — datas no passado/futuro

**Uso no Controller:**
```java
@PostMapping
public ResponseEntity<Usuario> criar(@RequestBody @Valid UsuarioDTO dto) {
    // Se a validação falhar, retorna 400 Bad Request automaticamente
    ...
}
```

**Tratamento de erros de validação:**
```java
@RestControllerAdvice
public class TratamentoErros {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErroResponse> tratarValidacao(MethodArgumentNotValidException ex) {
        List<String> erros = ex.getBindingResult()
            .getFieldErrors()
            .stream()
            .map(e -> e.getField() + ": " + e.getDefaultMessage())
            .collect(Collectors.toList());

        return ResponseEntity.badRequest().body(new ErroResponse("Erro de validação", erros));
    }
}
```

---

## 9. Tratamento de Erros

**Responsabilidade:** Interceptar exceções e retornar respostas de erro padronizadas.

**Anotações principais:**
- `@RestControllerAdvice` — classe global de tratamento de exceções
- `@ExceptionHandler` — método que trata uma exceção específica

**Exemplo completo:**
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<ErroResponse> tratarNotFound(ResourceNotFoundException ex) {
        ErroResponse erro = new ErroResponse(ex.getMessage(), HttpStatus.NOT_FOUND.value());
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(erro);
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<ErroResponse> tratarValidacao(MethodArgumentNotValidException ex) {
        List<String> erros = ex.getBindingResult()
            .getFieldErrors()
            .stream()
            .map(e -> e.getField() + ": " + e.getDefaultMessage())
            .collect(Collectors.toList());
        ErroResponse erro = new ErroResponse("Erro de validação", erros);
        return ResponseEntity.badRequest().body(erro);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErroResponse> tratarGeral(Exception ex) {
        ErroResponse erro = new ErroResponse("Erro interno do servidor", HttpStatus.INTERNAL_SERVER_ERROR.value());
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(erro);
    }
}
```

**Resposta de erro padrão:**
```json
{
    "mensagem": "Usuário não encontrado",
    "status": 404,
    "timestamp": "2025-01-15T10:30:00",
    "erros": []
}
```

---

## 10. Persistência com JPA

**Responsabilidade:** Mapear objetos Java para tabelas de banco de dados (ORM).

**Anotações principais:**
- `@Entity` — marca classe como entidade JPA
- `@Table` — define nome da tabela
- `@Id` — marca chave primária
- `@GeneratedValue` — geração automática de ID
- `@Column` — mapeia coluna da tabela
- `@OneToMany`, `@ManyToOne`, `@ManyToMany` — relacionamentos

**Exemplo:**
```java
@Getter
@Setter
@NoArgsConstructor
@Entity
@Table(name = "usuarios")
public class Usuario {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(nullable = false, length = 100)
    private String nome;

    @Column(nullable = false, unique = true)
    private String email;

    @Column(nullable = false)
    private Boolean ativo = true;

    @OneToMany(mappedBy = "usuario", cascade = CascadeType.ALL)
    private List<Pedido> pedidos;
}

@Getter
@Setter
@NoArgsConstructor
@Entity
@Table(name = "pedidos")
public class Pedido {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "usuario_id")
    private Usuario usuario;

    private BigDecimal valorTotal;
    private String status;
    private LocalDateTime dataPedido;
}
```

*Em entidades JPA prefira `@Getter/@Setter` a `@Data` para evitar problemas com `equals/hashCode` e coleções lazy*

**Configuração em application.properties:**
```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

## 11. Boas Práticas de APIs REST

| Prática | Descrição |
|---------|-----------|
| Versionamento | Use `/api/v1/usuarios` para versionar sua API |
| Nomes coerentes | Use substantivos no plural (`/usuarios`, não `/usuario`) |
| Métodos HTTP corretos | GET (leitura), POST (criação), PUT (atualização), DELETE (exclusão) |
| Códigos de status | 200 (OK), 201 (Criado), 204 (Sem conteúdo), 400 (Requisição inválida), 404 (Não encontrado), 500 (Erro interno) |
| Paginação | Use `?page=0&size=10` para listas grandes |
| Documentação | Use Spring REST Docs ou Swagger/OpenAPI |
| Tratamento de erros | Use `@RestControllerAdvice` para respostas padronizadas |
| Validação | Valide sempre dados de entrada com `@Valid` |
| DTOs | Nunca exponha entidades diretamente nos endpoints |
| Segurança HTTPS | Use HTTPS em produção |

---

## 12. Resumo para Revisão

### 15 Conceitos Essenciais

| # | Conceito | Anotação/Classe |
|---|----------|-----------------|
| 1 | Inicialização | `@SpringBootApplication` |
| 2 | Injeção de Dependências | `@Autowired` |
| 3 | Configuração | `@Configuration` / `@Bean` |
| 4 | Controller | `@RestController` / `@RequestMapping` |
| 5 | Corpo da Requisição | `@RequestBody` |
| 6 | Corpo da Resposta | `@ResponseBody` / `ResponseEntity` |
| 7 | Parâmetros URL | `@RequestParam` / `@PathVariable` |
| 8 | Repositório JPA | `@Repository` / `@Query` |
| 9 | Validação | `@Valid` / `@NotBlank` |
| 10 | Tratamento de Erros | `@RestControllerAdvice` / `@ExceptionHandler` |
| 11 | Boas Práticas | `/api/v1/`, DTOs, HTTPS |
| 12 | Paginação | `Pageable`, `Page<T>` |
| 13 | Propriedades Externas | `application.properties` / `application.yml` + `@Value` / `@ConfigurationProperties` |
| 14 | Observabilidade (Actuator) | `/actuator/health`, `/actuator/metrics` |
| 15 | Cliente HTTP | `WebClient` / `RestTemplate` |

### Fluxo de uma Requisição

```
Cliente → Controller (@RequestBody) → Service (@Transactional) → Repository (JPA) → Banco
```

---

## 13. Glossário

| Termo | Definição |
|-------|-----------|
| **API** | Application Programming Interface — contrato de comunicação entre sistemas |
| **REST** | REpresentational State Transfer — arquitetura para APIs web |
| **Endpoint** | Ponto de acesso da API (URL + método HTTP) |
| **Controller** | Camada que recebe requisições HTTP e roteia para o handler adequado |
| **Service** | Camada de lógica de negócio e coordenação |
| **Repository** | Camada de acesso a dados (abstração do banco) |
| **DTO** | Data Transfer Object — objeto para transferência de dados entre camadas |
| **Entity** | Entidade JPA — mapeamento objeto-relacional |
| **JPA** | Java Persistence API — especificação para persistência de dados |
| **ORM** | Object-Relational Mapping — mapeamento objeto-relacional |
| **Dependency Injection** | Injeção de Dependência — container IoC resolve dependências automaticamente |
| **Bean** | Componente gerenciado pelo container IoC do Spring |
| **HTTP** | HyperText Transfer Protocol — protocolo de comunicação da web |
| **JSON** | JavaScript Object Notation — formato de dados leve e legível |
| **Validation** | Validação — verificação de regras em dados de entrada |
| **Exception Handler** | Tratador de Exceções — intercepta erros e retorna respostas padronizadas |

---

## 14. Perguntas de Revisão

### Nível Básico

1. **Qual é o papel da anotação `@SpringBootApplication`?**
   - *Resposta:* Ela serve como classe de entrada, ativando `@ComponentScan`, `@EnableAutoConfiguration` e `@Configuration`. É o ponto de partida para rodar a aplicação.

2. **Explique como Controller e Repository trabalham juntas para lidar com uma requisição de escrita.**
   - *Resposta:* O Controller recebe a requisição HTTP, decodifica o JSON com `@RequestBody` e retorna a resposta com `ResponseEntity`. O Repository lida com a persistência, gerenciando entidades no banco de dados via interfaces automáticas.

### Nível Intermediário

3. **Como o Spring Data JPA simplifica o desenvolvimento da camada de acesso a dados?**
   - *Resposta:* Reduz boilerplate ao exigir apenas declaração de interfaces. O Spring configura a implementação automaticamente. Valida `@Query` em tempo de inicialização para evitar erros em runtime.

4. **Quais ferramentas de teste o Spring Boot oferece para simular chamadas HTTP?**
   - *Resposta:* MockMvc (para simulação de requisições HTTP sem servidor real) e WebTestClient (para fluxos assíncronos e não-bloqueantes).

### Nível Avançado

5. **Quais mecanismos o Spring Boot Actuator oferece para observabilidade?**
   - *Resposta:* Endpoints como /health (status), /metrics (performance), /httpexchanges (histórico de requisições) e /auditevents (auditoria). Acessíveis via HTTP ou JMX.

6. **Quais tecnologias o Spring Boot oferece para otimizar empacotamento e inicialização?**
   - *Resposta:* GraalVM Native Images (compilação AOT), Cloud Native Buildpacks (imagens Docker), Checkpoint/Restore (restauração de memória).

---

## 15. Prompts Reutilizáveis

Estes prompts podem ser usados futuramente para revisão, teste de conhecimento e geração de material de estudo.

### Prompt 1 — Visão Geral
> "Com base exclusivamente nas fontes fornecidas, crie uma lista resumida (máximo 10 itens) dos conceitos essenciais de [TEMA]. Para cada conceito, inclua uma definição de uma linha e um exemplo de anotação ou classe quando aplicável."

### Prompt 2 — Estrutura de Aprendizado
> "Organize os conceitos de [TEMA] em uma sequência de aprendizado em 3 fases: (1) Fundamentos, (2) Desenvolvimento, (3) Produção. Para cada fase, liste de 3 a 5 tópicos com uma descrição de uma linha cada. Inclua [TÓPICOS ESPECÍFICOS]."

### Prompt 3 — Comparação
> "Explique as responsabilidades de [CAMADA 1], [CAMADA 2] e [CAMADA 3] em [TEMA]. Para cada camada, inclua: (1) responsabilidade principal em uma frase, (2) anotações principais, (3) exemplo de código de uma linha. Se alguma camada não estiver bem coberta nas fontes, forneça uma definição geral baseada no padrão do ecossistema."

### Prompt 4 — Revisão com Perguntas
> "Crie [NÚMERO] perguntas de revisão sobre os principais conceitos de [TEMA]. Distribua: [N] perguntas básicas, [N] intermediárias e [N] avançadas. Para cada pergunta, forneça um gabarito comentado de 2-3 linhas. Inclua pelo menos uma pergunta sobre [TÓPICO ESPECÍFICO]."

### Prompt 5 — Identificação de Lacunas
> "Com base nas fontes, identifique conceitos importantes sobre [TEMA] que ainda não foram abordados nesta conversa. Para cada conceito, inclua uma definição de uma linha e justifique por que é importante."

### Prompt 6 — Glossário
> "Crie um glossário com [N] termos essenciais de [TEMA]. Para cada termo, inclua a definição em uma frase e um exemplo prático quando aplicável."

---

**Material produzido para o desafio da DIO — Aprendizagem Ativa com NotebookLM**