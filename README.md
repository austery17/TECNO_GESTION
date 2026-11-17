# TecnoGestión S.A.C. — Sistema de Gestión Comercial (Spring Boot)

Proyecto para el curso **Herramientas de Desarrollo** — implementación de control de
versiones con Git y GitHub sobre un sistema de gestión comercial.

Sistema web con 4 módulos: **Login, Dashboard, Clientes, Productos y Ventas**,
construido con **Java 17 + Spring Boot 3 + Thymeleaf + Spring Data JPA**.
Los datos se guardan en una **base de datos**: por defecto **H2 en archivo**
(no requiere instalar nada) y opcionalmente **MySQL**.

## Requisitos

- Java JDK **17** o superior
- Maven (o usar el que trae integrado tu IDE)
- Visual Studio Code con las extensiones **"Extension Pack for Java"** y
  **"Spring Boot Extension Pack"** (o IntelliJ IDEA, que ya trae soporte Spring Boot)

## Cómo ejecutarlo

### Opción 1: Visual Studio Code
1. Abre la carpeta del proyecto en VS Code (`Archivo > Abrir carpeta`).
2. Espera a que VS Code detecte el proyecto Maven e instale las dependencias
   (lo hace automáticamente la primera vez, necesita internet).
3. Abre `src/main/java/com/tecnogestion/TecnogestionApplication.java`.
4. Haz clic en **Run** (▶) sobre el método `main`, o usa el ícono de Spring Boot
   Dashboard en la barra lateral.

### Opción 2: Terminal (Maven)
```bash
mvn spring-boot:run
```

### Opción 3: Generar el .jar y ejecutarlo
```bash
mvn clean package
java -jar target/tecnogestion.jar
```

Luego abre en el navegador: **http://localhost:8080**

**Usuario de prueba:** admin
**Contraseña de prueba:** admin123

## Estructura del proyecto

```
tecnogestion-spring/
├── pom.xml                         # Dependencias Maven (Web, Thymeleaf, JPA, H2, MySQL)
├── src/main/java/com/tecnogestion/
│   ├── TecnogestionApplication.java
│   ├── controller/                 # LoginController, DashboardController,
│   │                                  ClienteController, ProductoController, VentaController
│   ├── model/                      # Usuario, Cliente, Producto, Venta
│   ├── repository/                 # Repositorios Spring Data JPA
│   ├── config/                     # DataInitializer (datos de ejemplo)
│   └── service/                    # Lógica de acceso a datos para cada entidad
└── src/main/resources/
    ├── application.properties
    ├── templates/                  # Vistas Thymeleaf (login, dashboard, clientes, productos, ventas)
    │   └── fragments/layout.html   # Menú lateral, barra superior, modal de confirmación y avisos
    └── static/
        ├── css/style.css           # Tema visual (navy + cobalto)
        └── js/app.js               # Búsqueda en tablas, modales, calculadora de venta, animaciones
```

## Notas sobre el proyecto

- **Base de datos**: los datos persisten entre reinicios. Las tablas
  (`usuarios`, `clientes`, `productos`, `ventas`) se crean solas
  (`spring.jpa.hibernate.ddl-auto=update`) y se cargan datos de ejemplo
  la primera vez (`config/DataInitializer`).
  - **H2 (por defecto)**: archivo en `./data/tecnogestion.mv.db`. Consola en
    http://localhost:8080/h2-console
    (JDBC URL: `jdbc:h2:file:./data/tecnogestion`, usuario `sa`, sin contraseña).
    Para reiniciar los datos, borra la carpeta `data/`.
  - **MySQL**: crea/levanta MySQL y ejecuta
    `mvn spring-boot:run -Dspring-boot.run.profiles=mysql`
    (la base `tecnogestion` se crea sola; ajusta con las variables de entorno
    `DB_URL`, `DB_USER`, `DB_PASSWORD`).
- **Autenticación simple** basada en sesión HTTP (`HttpSession`), sin Spring
  Security, para mantener el proyecto liviano.

## Sugerencia de ramas de Git para este proyecto

- `main` — versión estable
- `develop` — integración de módulos
- `feature/login` — pantalla e integración de inicio de sesión
- `feature/clientes` — módulo de clientes
- `feature/productos` — módulo de productos
- `feature/ventas` — módulo de ventas
