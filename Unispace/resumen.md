# 🏗️ Arquitectura Hexagonal + DDD en Node.js (Backend UniSpace)

## 📚 Conceptos Fundamentales

### Arquitectura vs Spring Boot

|Concepto|Spring Boot|Node.js + Prisma|
|---|---|---|
|**Entidades**|`@Entity`|[User.ts](vscode-file://vscode-app/c:/Users/Joel/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)|
|**Repositorio (Interface)**|`@Repository`|[UserRepository.ts](vscode-file://vscode-app/c:/Users/Joel/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)|
|**Repositorio (Implementación)**|`UserRepositoryImpl`|`infrastructure/prisma/prisma-user.repository.ts`|
|**Servicios**|`@Service`|`application/UseCase.ts` (falta implementar)|
|**Controladores**|`@RestController`|[user.ts](vscode-file://vscode-app/c:/Users/Joel/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)|
|**ORM**|JPA/Hibernate|Prisma|
|**Config DB**|`application.properties`|[.env](vscode-file://vscode-app/c:/Users/Joel/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html)|

---

## 🎯 Estructura de Carpetas (Hexagonal)

src/modules/user/
├── domain/              ← Lógica de negocio pura
│   ├── User.ts         ← Entidad con métodos de negocio
│   └── value-objects/  ← Objetos inmutables validados (Email, Price)
├── ports/              ← Interfaces/Contratos (como interfaces Java)
│   └── UserRepository.ts
├── infrastructure/     ← Implementaciones concretas (Adapters)
│   └── prisma/
│       ├── prisma-user.repository.ts  ← Implementa UserRepository
│       └── user.mapper.ts             ← Convierte DB ↔ Domain
└── application/        ← Casos de uso (falta implementar)
    └── CreateUserUseCase.ts
---

## 🔄 Flujo de Datos

HTTP Request
    ↓
Routes (Express)
    ↓
Use Cases (Application Layer) ← FALTA IMPLEMENTAR
    ↓
Repository Interface (Port)
    ↓
Prisma Repository (Infrastructure)
    ↓
Prisma Client
    ↓
PostgreSQL
---

## 🛠️ ¿Qué es Prisma?

**Prisma = ORM (como JPA/Hibernate en Java)**

### Funciones principales:

1. **Define el esquema** de la BD ([schema.prisma](vscode-file://vscode-app/c:/Users/Joel/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html))
2. **Genera tipos TypeScript** automáticamente
3. **Consulta la BD** con métodos type-safe
4. **Maneja migraciones** (como Flyway/Liquibase)

### Comandos clave:

npx prisma generate       # Genera el cliente Prisma

npx prisma migrate dev    # Crea/aplica migraciones

npx prisma studio         # UI visual de la BD

---

## 🐳 Configuración Docker + Prisma

### Docker PostgreSQL:
docker run -e POSTGRES_PASSWORD=123 -p 5555:5432 -d postgres
### Spring Boot vs Prisma (Variables de entorno):

**Spring Boot** (variables separadas):
DB_HOST=localhost

DB_PORT=5555

DB_NAME=postgres

DB_USER=postgres

DB_PASSWORD=123

**Prisma** (connection string única):

DATABASE_URL="postgresql://postgres:123@localhost:5555/postgres?schema=public"

---

## 📦 Pasos para Levantar el Backend

### 1. Instalar dependencias
npm install
### 2. Generar Prisma Client
npx prisma generate

### 3. Levantar PostgreSQL en Docker
- docker run -e POSTGRES_PASSWORD=123 -p 5555:5432 -d postgres
### 4. Aplicar migraciones (crear tablas)

- npx prisma migrate dev

### 5. Iniciar servidor

- npm run dev
---

## 🎨 Value Objects (Patrón DDD)

Objetos inmutables con validación integrada:

export class Price {

  constructor(private readonly amount: number) {

    if (amount < 0) throw new Error('Price cannot be negative');

  }

}

**Ventaja:** Un [Price](vscode-file://vscode-app/c:/Users/Joel/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-browser/workbench/workbench.html) **siempre es válido**. No existe un price negativo.

---

## ✅ Ventajas de Arquitectura Hexagonal

|Aspecto|Beneficio|
|---|---|
|**Independencia**|El dominio NO depende de frameworks|
|**Testing**|Fácil hacer mocks de interfaces|
|**Cambio de BD**|Solo cambias `infrastructure/`|
|**Lógica centralizada**|Domain entities tienen comportamiento|

---

## 🚀 Próximos Pasos (Lo que falta)

1. **Crear capa Application** (`UseCase.ts`)
2. **Implementar servicios** de autenticación
3. **Conectar routes** con use cases
4. **Añadir middleware** de autenticación
5. **Implementar DTOs** para request/response

---

## 📝 Tecnologías del Stack

- **Runtime:** Node.js + TypeScript
- **Framework Web:** Express
- **ORM:** Prisma
- **Base de datos:** PostgreSQL
- **Arquitectura:** Hexagonal + DDD
- **Contenedor:** Docker

