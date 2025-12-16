# Spring Boot - Projeto Message

Aplicação Spring Boot com sistema de mensagens, autenticação e suporte a múltiplos bancos de dados (H2, MySQL, PostgreSQL).

## Pré-requisitos

- **Java 17** ou superior
- **Gradle** (incluído via wrapper)
- **VS Code** com as seguintes extensões:
  - Extension Pack for Java (Microsoft)
  - Spring Boot Extension Pack (VMware)
  - Gradle for Java (Microsoft)

## Configuração do Ambiente

### 1. Instalar Java 17+

Verifique se o Java está instalado:
```bash
java -version
```

Se não estiver instalado, baixe o [OpenJDK 17](https://adoptium.net/) ou superior.

### 2. Configurar VS Code

1. Abra o VS Code
2. Instale as extensões recomendadas:
   - Pressione `Ctrl+Shift+X` (ou `Cmd+Shift+X` no Mac)
   - Procure e instale "Extension Pack for Java"
   - Procure e instale "Spring Boot Extension Pack"

## Como Rodar o Projeto

### Opção 1: Via Terminal Integrado do VS Code

1. Abra o projeto no VS Code:
   ```bash
   code .
   ```

2. Abra o terminal integrado (`Ctrl+` ` ou menu Terminal > New Terminal)

3. Execute o projeto:
   ```bash
   ./gradlew bootRun
   ```

   No Windows (se o comando acima não funcionar):
   ```bash
   .\gradlew.bat bootRun
   ```

4. Aguarde a mensagem:
   ```
   Started MessageApplication in X seconds
   ```

5. Acesse a aplicação em: http://localhost:8000

### Opção 2: Via Spring Boot Dashboard (VS Code)

1. Após instalar as extensões do Spring Boot, você verá o painel "Spring Boot Dashboard" na barra lateral esquerda

2. Clique no ícone do Spring Boot

3. Encontre "MessageApplication" na lista

4. Clique no botão ▶️ (Play) ao lado de "MessageApplication"

5. A aplicação iniciará e você verá os logs no terminal

### Opção 3: Via Arquivo Principal

1. No VS Code, navegue até: `src/main/java/example/message/MessageApplication.java`

2. Clique com botão direito no arquivo

3. Selecione "Run Java" ou pressione `F5`

## Acessos da Aplicação

### URLs Principais
- **Aplicação**: http://localhost:8000
- **Console H2**: http://localhost:8000/h2-console

### Console H2 (Banco de Dados)
Para acessar o console do banco H2:
- **URL**: http://localhost:8000/h2-console
- **JDBC URL**: `jdbc:h2:mem:testdb`
- **Username**: `SA`
- **Password**: (deixe em branco)


## Configuração de Banco de Dados

O projeto suporta três bancos de dados. Edite `src/main/resources/application.properties` para alternar:

### H2 (Padrão - Em Memória) ✅ ATIVO
```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
```

### MySQL (Descomente para usar)
```properties
# spring.datasource.url=jdbc:mysql://localhost:3306/nome_do_banco
# spring.datasource.username=seu_usuario
# spring.datasource.password=sua_senha
# spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
# spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
```

### PostgreSQL (Descomente para usar)
```properties
# spring.datasource.url=jdbc:postgresql://localhost:5432/nome_do_banco
# spring.datasource.driver-class-name=org.postgresql.Driver
# spring.jpa.database-platform=org.hibernate.dialect.PostgreSQLDialect
```

## Comandos Úteis

### Build do Projeto
```bash
./gradlew build
```

### Build sem executar testes
```bash
./gradlew build -x test
```

### Executar testes
```bash
./gradlew test
```

### Limpar build
```bash
./gradlew clean
```

### Verificar versão do Gradle
```bash
./gradlew --version
```

## Estrutura do Projeto

```
Spring-Boot-modulo/
├── src/
│   ├── main/
│   │   ├── java/example/message/
│   │   │   ├── MessageApplication.java    # Classe principal
│   │   │   └── SecurityConfig.java        # Configuração de segurança
│   │   └── resources/
│   │       ├── application.properties     # Configurações
│   │       └── schema.sql.bak            # Schema SQL (backup)
│   └── test/
│       ├── java/
│       └── resources/
├── build.gradle                           # Dependências e configuração
├── gradlew                               # Gradle Wrapper (Linux/Mac)
├── gradlew.bat                           # Gradle Wrapper (Windows)
└── README.md                             # Este arquivo
```

## Solução de Problemas

### Erro: "zip END header not found"
**Solução**: Limpe o cache do Gradle:
```bash
# Windows
rmdir /s /q %USERPROFILE%\.gradle\wrapper\dists\gradle-8.3-bin

# Linux/Mac
rm -rf ~/.gradle/wrapper/dists/gradle-8.3-bin
```

### Porta 8000 já em uso
**Solução**: Altere a porta em `application.properties`:
```properties
server.port=8080
```

### Aplicação não inicia
1. Verifique se o Java 17+ está instalado: `java -version`
2. Verifique se a porta 8000 está livre
3. Execute: `./gradlew clean build`
4. Tente novamente: `./gradlew bootRun`

### Erro de permissão no gradlew (Linux/Mac)
```bash
chmod +x gradlew
```

## Tecnologias Utilizadas

- **Spring Boot 3.1.4**
- **Spring Security** - Autenticação e autorização
- **Spring Data JPA** - ORM para banco de dados
- **H2 Database** - Banco em memória (desenvolvimento)
- **MySQL & PostgreSQL** - Suporte para bancos em produção
- **Gradle 8.3** - Gerenciamento de dependências
- **Java 17** - Linguagem base

## Desenvolvimento

### Hot Reload
Para ativar hot reload no VS Code:
1. Adicione ao `build.gradle`:
   ```gradle
   dependencies {
       developmentOnly 'org.springframework.boot:spring-boot-devtools'
   }
   ```
2. Reinicie a aplicação

### Debug no VS Code
1. Coloque breakpoints clicando na margem esquerda do editor
2. Pressione `F5` ou vá em Run > Start Debugging
3. Escolha "Java" quando solicitado
4. A aplicação iniciará em modo debug

## Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Licença

Este projeto é livre para uso educacional e desenvolvimento.

## Suporte

Para problemas ou dúvidas:
1. Verifique a seção "Solução de Problemas"
2. Consulte a [documentação oficial do Spring Boot](https://spring.io/projects/spring-boot)
3. Abra uma issue no repositório

---

