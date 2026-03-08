# TODO Management Full-Stack Application :

## 🏗 1. Architecture Overview

- __`Tech Stack`__

- `Backend:` Spring Boot 3.x
- `Security:` Spring Security + JWT + OAuth2
- `DB (Test):` H2
- `DB (Prod):` MySQL (Azure Database for MySQL)
- `Frontend:` React
- `DevOps:` Docker, Azure DevOps
- `Cloud:` Azure App Service

```scss
React (Azure App Service Static Web App)
        ↓
Spring Boot REST API (Azure App Service / Docker)
        ↓
Azure Database for MySQL (Prod)
H2 (Test profile)
```

## 🔹 2. Backend – Spring Boot REST API

- Step 1: Create Project
- Use Spring Initializr:

Dependencies:

- Spring Web
- Spring Data JPA
- Spring Security
- OAuth2 Resource Server
- MySQL Driver
- H2
- Lombok
- Validation
- Flyway (for migration)
- Docker Support


## 📁 Project Structure

```
todo-fullstack/
│
├── backend/
│   ├── pom.xml
│   ├── Dockerfile
│   └── src/main/java/com/todo/
│       ├── TodoApplication.java
│       ├── entity/
│       │   ├── User.java
│       │   ├── Role.java
│       │   └── Todo.java
│       ├── repository/
│       │   ├── UserRepository.java
│       │   └── TodoRepository.java
│       ├── service/
│       │   ├── AuthService.java
│       │   ├── UserService.java
│       │   └── TodoService.java
│       ├── controller/
│       │   ├── AuthController.java
│       │   ├── UserController.java
│       │   └── TodoController.java
│       ├── security/
│       │   ├── JwtUtil.java
│       │   ├── JwtFilter.java
│       │   └── SecurityConfig.java
│       ├── dto/
│       │   ├── LoginRequest.java
│       │   ├── RegisterRequest.java
│       │   └── TodoDto.java
│       └── exception/
│           └── GlobalExceptionHandler.java
│
│   └── src/main/resources/
│       ├── application.yml
│       └── db/migration/V1__init.sql
│
└── frontend/
    ├── package.json
    └── src/
        ├── App.js
        ├── api.js
        ├── Login.js
        ├── Register.js
        ├── Dashboard.js
        └── AdminPanel.js

```

=========================
🔵 BACKEND SOURCE CODE
=========================

## backend/pom.xml

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.todo</groupId>
    <artifactId>todo</artifactId>
    <version>0.0.1</version>
    <packaging>jar</packaging>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>3.2.0</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-security</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>

        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt-api</artifactId>
            <version>0.11.5</version>
        </dependency>

        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt-impl</artifactId>
            <scope>runtime</scope>
            <version>0.11.5</version>
        </dependency>

        <dependency>
            <groupId>io.jsonwebtoken</groupId>
            <artifactId>jjwt-jackson</artifactId>
            <scope>runtime</scope>
            <version>0.11.5</version>
        </dependency>

        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
        </dependency>

        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
        </dependency>

        <dependency>
            <groupId>org.flywaydb</groupId>
            <artifactId>flyway-core</artifactId>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
    </dependencies>
</project>
```

-------------------------------------------

##  Entity Layer :


__entity/Role.java__

```java
package com.todo.entity;

public enum Role {
    ROLE_ADMIN,
    ROLE_USER
}
```
__entity/User.java__

```java
package com.todo.entity;

import jakarta.persistence.*;
import lombok.*;

@Entity
@Table(name = "users")
@Getter @Setter
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(unique = true)
    private String username;

    private String password;

    @Enumerated(EnumType.STRING)
    private Role role;
}
```

__entity/Todo.java__

```java
package com.todo.entity;

import jakarta.persistence.*;
import lombok.*;

@Entity
@Getter @Setter
public class Todo {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String description;
    private boolean completed;

    @ManyToOne
    private User user;
}

```

__entity/RefreshToken.java__

```java
package com.todo.entity;

import jakarta.persistence.*;
import lombok.*;

import java.time.Instant;

@Entity
@Getter @Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class RefreshToken {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String token;

    private Instant expiryDate;

    private boolean revoked;

    @ManyToOne(fetch = FetchType.LAZY)
    private User user;
}
```

__entity/BlacklistedToken.java__

```java
package com.todo.entity;

import jakarta.persistence.*;
import lombok.*;

import java.time.Instant;

@Entity
@Getter @Setter
@NoArgsConstructor
@AllArgsConstructor
@Builder
public class BlacklistedToken {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String token;
    private Instant expiryDate;
}
```

---------------------------

## Repository layer:

__repository/UserRepository.java__

```java
package com.todo.repository;

import com.todo.model.User;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface UserRepository extends JpaRepository<User, Long> {

    Optional<User> findByUsername(String username);

    Optional<User> findByEmail(String email);

    Boolean existsByUsername(String username);

    Boolean existsByEmail(String email);

}

```

__repository/RoleRepository.java__
- Used during signup (assign ROLE_USER / ROLE_ADMIN)

```java
package com.todo.repository;

import com.todo.model.Role;
import com.todo.model.ERole;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface RoleRepository extends JpaRepository<Role, Long> {

    Optional<Role> findByName(ERole name);

}

```

__repository/TodoRepository.java__

```java
package com.todo.repository;

import com.todo.model.Todo;
import com.todo.model.User;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.List;

public interface TodoRepository extends JpaRepository<Todo, Long> {

    List<Todo> findByUser(User user);

    List<Todo> findByUserAndCompleted(User user, boolean completed);

}


```
__repository/RefreshTokenRepository.java__
- Stores refresh tokens (Remember Me + OAuth flow)

```java
package com.todo.repository;

import com.todo.model.RefreshToken;
import com.todo.model.User;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface RefreshTokenRepository extends JpaRepository<RefreshToken, Long> {

    Optional<RefreshToken> findByToken(String token);

    void deleteByUser(User user);

}
```

__repository/BlacklistedTokenRepository.java__
- Used for Logout + Token Revocation (VERY IMPORTANT for security)

```java

package com.todo.repository;

import com.todo.model.BlacklistedToken;
import org.springframework.data.jpa.repository.JpaRepository;

public interface BlacklistedTokenRepository extends JpaRepository<BlacklistedToken, Long> {

    boolean existsByToken(String token);

```

<img width="1136" height="736" alt="image" src="https://github.com/user-attachments/assets/3eee413c-4f1f-4935-9ecc-eeead68e4607" />


------------------------------------
## DTO LAYER

__dto/LoginRequest.java__

```java
package com.todo.dto;

import jakarta.validation.constraints.NotBlank;
import lombok.Data;

@Data
public class LoginRequest {
    @NotBlank
    private String username;

    @NotBlank
    private String password;
}
```

__dto/RegisterRequest.java__

```java
package com.todo.dto;

import jakarta.validation.constraints.NotBlank;
import lombok.Data;

@Data
public class RegisterRequest {

    @NotBlank
    private String username;

    @NotBlank
    private String password;
}
```

__dto/TodoDto.java__

```java
package com.todo.dto;

import jakarta.validation.constraints.NotBlank;
import lombok.Data;

@Data
public class TodoDto {

    @NotBlank
    private String title;

    private String description;
    private boolean completed;
}

```
---------------------------------------

## Security layer

__security/JwtUtil.java__

```
package com.todo.security;

import io.jsonwebtoken.*;
import io.jsonwebtoken.security.Keys;
import org.springframework.stereotype.Component;

import java.security.Key;
import java.util.Date;

@Component
public class JwtUtil {

    private final String SECRET = "verysecretkeyverysecretkeyverysecretkey123";
    private final long EXPIRATION = 1000 * 60 * 60 * 24;

    private final Key key = Keys.hmacShaKeyFor(SECRET.getBytes());

    public String generateToken(String username, String role) {

        return Jwts.builder()
                .setSubject(username)
                .claim("role", role)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + EXPIRATION))
                .signWith(key)
                .compact();
    }

    public String extractUsername(String token) {
        return getClaims(token).getSubject();
    }

    public String extractRole(String token) {
        return getClaims(token).get("role", String.class);
    }

    public boolean isValid(String token) {
        try {
            getClaims(token);
            return true;
        } catch (JwtException e) {
            return false;
        }
    }

    private Claims getClaims(String token) {
        return Jwts.parserBuilder()
                .setSigningKey(key)
                .build()
                .parseClaimsJws(token)
                .getBody();
    }
}

```

__security/JwtFilter.java__

```java

package com.todo.security;

import jakarta.servlet.FilterChain;
import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import lombok.RequiredArgsConstructor;

import org.springframework.http.HttpHeaders;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.web.authentication.WebAuthenticationDetailsSource;
import org.springframework.stereotype.Component;
import org.springframework.web.filter.OncePerRequestFilter;

import java.io.IOException;

@Component
@RequiredArgsConstructor
public class JwtFilter extends OncePerRequestFilter {

    private final JwtUtil jwtUtil;
    private final CustomUserDetailsService userDetailsService;

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain)
            throws ServletException, IOException {

        try {

            String header = request.getHeader(HttpHeaders.AUTHORIZATION);

            // No token → continue (public endpoints may still work)
            if (header == null || !header.startsWith("Bearer ")) {
                filterChain.doFilter(request, response);
                return;
            }

            String token = header.substring(7);

            // Invalid token → continue but no auth
            if (!jwtUtil.isValid(token)) {
                filterChain.doFilter(request, response);
                return;
            }

            String username = jwtUtil.extractUsername(token);

            // If already authenticated, skip
            if (username != null && SecurityContextHolder.getContext().getAuthentication() == null) {

                UserDetails userDetails = userDetailsService.loadUserByUsername(username);

                UsernamePasswordAuthenticationToken authToken =
                        new UsernamePasswordAuthenticationToken(
                                userDetails,
                                null,
                                userDetails.getAuthorities()
                        );

                authToken.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));

                SecurityContextHolder.getContext().setAuthentication(authToken);
            }

        } catch (Exception ex) {
            // Important: clear context if token parsing fails
            SecurityContextHolder.clearContext();
        }

        filterChain.doFilter(request, response);
    }
}
```


## security/SecurityConfig.java

```java
package com.todo.security;

import lombok.RequiredArgsConstructor;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;

import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;

import org.springframework.security.config.annotation.method.configuration.EnableMethodSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;

import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;

import org.springframework.security.web.AuthenticationEntryPoint;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.access.AccessDeniedHandler;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;

import org.springframework.security.config.annotation.web.builders.HttpSecurity;

import jakarta.servlet.http.HttpServletResponse;

@Configuration
@EnableMethodSecurity
@RequiredArgsConstructor
public class SecurityConfig {

    private final JwtFilter jwtFilter;

    // ================= PASSWORD ENCODER =================
    @Bean
    public PasswordEncoder passwordEncoder() {
        return new BCryptPasswordEncoder();
    }

    // ================= AUTH MANAGER =================
    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
        return config.getAuthenticationManager();
    }

    // ================= 401 HANDLER =================
    @Bean
    public AuthenticationEntryPoint unauthorizedHandler() {
        return (request, response, ex) ->
                response.sendError(HttpServletResponse.SC_UNAUTHORIZED, "Unauthorized: Invalid or missing token");
    }

    // ================= 403 HANDLER =================
    @Bean
    public AccessDeniedHandler accessDeniedHandler() {
        return (request, response, ex) ->
                response.sendError(HttpServletResponse.SC_FORBIDDEN, "Forbidden: You don't have permission");
    }

    // ================= SECURITY FILTER CHAIN =================
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

        http
            // Disable CSRF for REST API
            .csrf(csrf -> csrf.disable())

            // Stateless session (JWT)
            .sessionManagement(session ->
                    session.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            )

            // Exception handling
            .exceptionHandling(ex -> ex
                    .authenticationEntryPoint(unauthorizedHandler())
                    .accessDeniedHandler(accessDeniedHandler())
            )

            // Authorization rules
            .authorizeHttpRequests(auth -> auth

                    // PUBLIC ENDPOINTS
                    .requestMatchers("/api/auth/**").permitAll()
                    .requestMatchers("/h2-console/**").permitAll()

                    // ADMIN ONLY
                    .requestMatchers("/api/admin/**").hasRole("ADMIN")

                    // TODOS — logged in users
                    .requestMatchers(HttpMethod.GET, "/api/todos/**").hasAnyRole("USER","ADMIN")
                    .requestMatchers(HttpMethod.POST, "/api/todos/**").hasAnyRole("USER","ADMIN")
                    .requestMatchers(HttpMethod.PUT, "/api/todos/**").hasAnyRole("USER","ADMIN")
                    .requestMatchers(HttpMethod.DELETE, "/api/todos/**").hasAnyRole("USER","ADMIN")

                    // everything else
                    .anyRequest().authenticated()
            )

            // Add JWT filter
            .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class);

        // For H2 console
        http.headers(headers -> headers.frameOptions(frame -> frame.disable()));

        return http.build();
    }
}

```

-----------------------------------------------------------

## 🧩 SERVICE LAYER :

__service/AuthService.java__

```java
package com.todo.service;

import com.todo.dto.LoginRequest;
import com.todo.dto.RegisterRequest;
import com.todo.entity.Role;
import com.todo.entity.User;
import com.todo.repository.UserRepository;
import com.todo.security.JwtUtil;
import lombok.RequiredArgsConstructor;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;

@Service
@RequiredArgsConstructor
public class AuthService {

    private final UserRepository userRepo;
    private final PasswordEncoder encoder;
    private final JwtUtil jwt;

    public String register(RegisterRequest req) {

        if (userRepo.findByUsername(req.getUsername()).isPresent())
            throw new RuntimeException("Username already exists");

        User user = new User();
        user.setUsername(req.getUsername());
        user.setPassword(encoder.encode(req.getPassword()));
        user.setRole(Role.ROLE_USER);

        userRepo.save(user);

        return "User registered successfully";
    }

    public String login(LoginRequest req) {

        User user = userRepo.findByUsername(req.getUsername())
                .orElseThrow(() -> new RuntimeException("User not found"));

        if (!encoder.matches(req.getPassword(), user.getPassword()))
            throw new RuntimeException("Invalid password");

        return jwt.generateToken(user.getUsername(), user.getRole().name());
    }
}

```

__service/UserService.java (ADMIN ONLY OPERATIONS)__

```java
package com.todo.service;

import com.todo.entity.User;
import com.todo.repository.UserRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository repo;

    // ADMIN: View all users
    public List<User> getAllUsers() {
        return repo.findAll();
    }

    // ADMIN: Delete user
    public void deleteUser(Long id) {

        User user = repo.findById(id)
                .orElseThrow(() -> new RuntimeException("User not found"));

        repo.delete(user);
    }

    // ADMIN: Change role
    public User changeRole(Long id, String role) {

        User user = repo.findById(id)
                .orElseThrow(() -> new RuntimeException("User not found"));

        user.setRole(Enum.valueOf(com.todo.entity.Role.class, role));

        return repo.save(user);
    }
}
```

__service/TodoService.java (OWNERSHIP SECURITY 🔥)__

```java
package com.todo.service;

import com.todo.dto.TodoDto;
import com.todo.entity.Todo;
import com.todo.entity.User;
import com.todo.repository.TodoRepository;
import com.todo.repository.UserRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.security.core.context.SecurityContextHolder;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
@RequiredArgsConstructor
public class TodoService {

    private final TodoRepository todoRepo;
    private final UserRepository userRepo;

    private User currentUser() {
        String username = SecurityContextHolder.getContext().getAuthentication().getName();
        return userRepo.findByUsername(username)
                .orElseThrow(() -> new RuntimeException("User not found"));
    }

    // CREATE
    public Todo create(TodoDto dto) {

        Todo todo = new Todo();
        todo.setTitle(dto.getTitle());
        todo.setDescription(dto.getDescription());
        todo.setCompleted(false);
        todo.setUser(currentUser());

        return todoRepo.save(todo);
    }

    // READ MY TODOS
    public List<Todo> myTodos() {
        return todoRepo.findByUserId(currentUser().getId());
    }

    // UPDATE (only owner)
    public Todo update(Long id, TodoDto dto) {

        Todo todo = todoRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("Todo not found"));

        if (!todo.getUser().getId().equals(currentUser().getId()))
            throw new RuntimeException("You cannot edit others todos");

        todo.setTitle(dto.getTitle());
        todo.setDescription(dto.getDescription());
        todo.setCompleted(dto.isCompleted());

        return todoRepo.save(todo);
    }

    // DELETE (only owner)
    public void delete(Long id) {

        Todo todo = todoRepo.findById(id)
                .orElseThrow(() -> new RuntimeException("Todo not found"));

        if (!todo.getUser().getId().equals(currentUser().getId()))
            throw new RuntimeException("You cannot delete others todos");

        todoRepo.delete(todo);
    }
}
```

----------------------------------------------------------------------


## 🌐 CONTROLLERS

```java
controller/AuthController.java
package com.todo.controller;

import com.todo.dto.LoginRequest;
import com.todo.dto.RegisterRequest;
import com.todo.service.AuthService;
import jakarta.validation.Valid;
import lombok.RequiredArgsConstructor;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/auth")
@RequiredArgsConstructor
public class AuthController {

    private final AuthService service;

    @PostMapping("/register")
    public String register(@Valid @RequestBody RegisterRequest req) {
        return service.register(req);
    }

    @PostMapping("/login")
    public String login(@Valid @RequestBody LoginRequest req) {
        return service.login(req);
    }
}
```

## controller/UserController.java (ADMIN PROTECTED)

```java
package com.todo.controller;

import com.todo.entity.User;
import com.todo.service.UserService;
import lombok.RequiredArgsConstructor;
import org.springframework.security.access.prepost.PreAuthorize;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/admin/users")
@RequiredArgsConstructor
@PreAuthorize("hasRole('ADMIN')")
public class UserController {

    private final UserService service;

    @GetMapping
    public List<User> allUsers() {
        return service.getAllUsers();
    }

    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id) {
        service.deleteUser(id);
    }

    @PutMapping("/{id}/role")
    public User changeRole(@PathVariable Long id, @RequestParam String role) {
        return service.changeRole(id, role);
    }
}
```

__controller/TodoController.java__

```
package com.todo.controller;

import com.todo.dto.TodoDto;
import com.todo.entity.Todo;
import com.todo.service.TodoService;
import jakarta.validation.Valid;
import lombok.RequiredArgsConstructor;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/api/todos")
@RequiredArgsConstructor
public class TodoController {

    private final TodoService service;

    @PostMapping
    public Todo create(@Valid @RequestBody TodoDto dto) {
        return service.create(dto);
    }

    @GetMapping
    public List<Todo> myTodos() {
        return service.myTodos();
    }

    @PutMapping("/{id}")
    public Todo update(@PathVariable Long id, @RequestBody TodoDto dto) {
        return service.update(id, dto);
    }

    @DeleteMapping("/{id}")
    public void delete(@PathVariable Long id) {
        service.delete(id);
    }
}

```

------------------------------------

## src/main/java/com/todo/TodoApplication.java

```java
package com.todo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.domain.EntityScan;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;

@SpringBootApplication
@EntityScan(basePackages = "com.todo.entity")
@EnableJpaRepositories(basePackages = "com.todo.repository")
public class TodoApplication {

    public static void main(String[] args) {
        SpringApplication.run(TodoApplication.class, args);
    }
}

```

## Global Exception Handling:
__exception/GlobalExceptionHandler.java__

```java
package com.todo.exception;

import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.access.AccessDeniedException;
import org.springframework.validation.FieldError;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDateTime;
import java.util.HashMap;
import java.util.Map;

@RestControllerAdvice
public class GlobalExceptionHandler {

    // ========== VALIDATION ERRORS ==========
    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<?> handleValidation(MethodArgumentNotValidException ex) {

        Map<String, String> errors = new HashMap<>();

        for (FieldError error : ex.getBindingResult().getFieldErrors()) {
            errors.put(error.getField(), error.getDefaultMessage());
        }

        return build(HttpStatus.BAD_REQUEST, "Validation failed", errors);
    }

    // ========== ACCESS DENIED ==========
    @ExceptionHandler(AccessDeniedException.class)
    public ResponseEntity<?> handleAccessDenied(AccessDeniedException ex) {
        return build(HttpStatus.FORBIDDEN, "You are not allowed to access this resource", null);
    }

    // ========== RUNTIME ==========
    @ExceptionHandler(RuntimeException.class)
    public ResponseEntity<?> handleRuntime(RuntimeException ex) {
        return build(HttpStatus.BAD_REQUEST, ex.getMessage(), null);
    }

    // ========== GENERIC ==========
    @ExceptionHandler(Exception.class)
    public ResponseEntity<?> handleGeneric(Exception ex) {
        return build(HttpStatus.INTERNAL_SERVER_ERROR, "Unexpected server error", null);
    }

    private ResponseEntity<Map<String, Object>> build(HttpStatus status, String message, Object errors) {

        Map<String, Object> body = new HashMap<>();
        body.put("timestamp", LocalDateTime.now());
        body.put("status", status.value());
        body.put("message", message);

        if (errors != null)
            body.put("errors", errors);

        return new ResponseEntity<>(body, status);
    }
}
```

------ 
##  application.yml (H2 for Local, MySQL for Azure)

Spring profiles:

- __dev → H2 database__
- __prod → Azure MySQL__

src/main/resources/application.yml
```
spring:
  application:
    name: todo-app

  profiles:
    active: dev

---
# ================= DEV (LOCAL TESTING H2) =================
spring:
  config:
    activate:
      on-profile: dev

  datasource:
    url: jdbc:h2:mem:todo-db
    driver-class-name: org.h2.Driver
    username: sa
    password: ""

  h2:
    console:
      enabled: true
      path: /h2-console

  jpa:
    database-platform: org.hibernate.dialect.H2Dialect
    hibernate:
      ddl-auto: validate
    show-sql: true

  flyway:
    enabled: true
    locations: classpath:db/migration

server:
  port: 8080

---
# ================= PROD (AZURE MYSQL) =================
spring:
  config:
    activate:
      on-profile: prod

  datasource:
    url: ${MYSQL_URL}
    username: ${MYSQL_USER}
    password: ${MYSQL_PASSWORD}
    driver-class-name: com.mysql.cj.jdbc.Driver

  jpa:
    database-platform: org.hibernate.dialect.MySQL8Dialect
    hibernate:
      ddl-auto: validate
    show-sql: false

  flyway:
    enabled: true
    baseline-on-migrate: true
    locations: classpath:db/migration

server:
  port: 80


```
## 🗄️ 4. Flyway Migration (Schema + Upgrade Strategy):

__src/main/resources/db/migration/V1__init.sql__

```sql
-- ========================
-- USERS TABLE
-- ========================
CREATE TABLE users (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    role VARCHAR(20) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- ========================
-- TODO TABLE
-- ========================
CREATE TABLE todo (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description VARCHAR(500),
    completed BOOLEAN DEFAULT FALSE,
    user_id BIGINT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT fk_user
        FOREIGN KEY (user_id)
        REFERENCES users(id)
        ON DELETE CASCADE
);

-- INDEXES (performance)
CREATE INDEX idx_user_username ON users(username);
CREATE INDEX idx_todo_user ON todo(user_id);

```

<img width="911" height="551" alt="image" src="https://github.com/user-attachments/assets/677af5ae-29b5-4098-a719-c9171477d6d3" />


## Dockerfile

```Dockerfile
FROM eclipse-temurin:17-jdk
COPY target/todo-0.0.1.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

=========================
🟢 FRONTEND SOURCE CODE
=========================

## frontend/package.json

```json
{
  "name": "todo-ui",
  "version": "1.0.0",
  "dependencies": {
    "axios": "^1.6.0",
    "react-router-dom": "^6.0.0"
  }
}
```

## src/api.js

```java
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:8080/api"
});

api.interceptors.request.use(config => {
  const token = localStorage.getItem("token");
  if(token) config.headers.Authorization = `Bearer ${token}`;
  return config;
});

export default api;

```

## src/Login.js

```
import api from "./api";
import { useState } from "react";

function Login() {
  const [username,setUsername]=useState("");
  const [password,setPassword]=useState("");

  const login = async () => {
    const res = await api.post("/auth/login",{username,password});
    localStorage.setItem("token",res.data);
  };

  return (
    <>
      <input onChange={e=>setUsername(e.target.value)} />
      <input type="password" onChange={e=>setPassword(e.target.value)} />
      <button onClick={login}>Login</button>
    </>
  );
}
export default Login;

```

## 🚀 AZURE DEPLOYMENT STEPS
__1️⃣ Create MySQL__
- Use: Azure Database for MySQL

__2️⃣ Deploy Backend__
- Use: Azure App Service

```
az webapp up --name todo-backend --runtime "JAVA:17"
```

__3️⃣ Setup CI/CD__

- Use: Azure DevOps

__Create pipeline:__

- Build
- Test
- Docker build
- Push to Azure Container Registry
- Deploy to App Service

##################################################


<img width="949" height="620" alt="image" src="https://github.com/user-attachments/assets/eac75483-0420-4de5-9076-2aaaa0d66cd0" />

<img width="922" height="406" alt="image" src="https://github.com/user-attachments/assets/8de51549-7f68-4df4-956d-bbf00c278718" />

- 👉 Sequence diagram (interview gold question)
- 👉 Common interview questions based on this project (very frequently asked)
- Is  mark Todo as complete/incomplete functionality with
proper authorization checks included ?

Followed REST best practices with validation, exception handling, and
proper HTTP status codes

- Created and managed MySQL databases on Azure using environment-
based configuration

- Wrote database migration scripts for schema upgrades and rollbacks
- Deployed backend and frontend applications to Azure App Service
- Containerized the application using Docker and Docker Compose, and
deployed to Azure
- Implemented CI/CD pipelines, auto-scaling, blue-green, and canary
deployments using Azure DevOps




🔥 Full JWT filter implementation

🔥 Complete Todo CRUD with authorization

🔥 Azure DevOps YAML pipeline

🔥 Blue-Green slot configuration

🔥 Resume-ready explanation

🔥 GitHub repo template





