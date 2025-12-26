# 🌟 CombinaMejor - Fashion Tech Platform

> Plataforma web interactiva que revoluciona cómo las personas aprenden a combinar su ropa mediante visualización 3D, recomendaciones personalizadas basadas en clima/contexto, y una comunidad activa.

[![PHP Version](https://img.shields.io/badge/PHP-8.2-777BB4?logo=php&logoColor=white)](https://www.php.net/)
[![Laravel](https://img.shields.io/badge/Laravel-12-FF2D20?logo=laravel&logoColor=white)](https://laravel.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Architecture](https://img.shields.io/badge/Architecture-Hexagonal%20%2B%20DDD-blue)](https://en.wikipedia.org/wiki/Hexagonal_architecture_(software))
[![PHPStan](https://img.shields.io/badge/PHPStan-Level%208-brightgreen)](https://phpstan.org/)
[![Redis](https://img.shields.io/badge/Redis-7-DC382D?logo=redis&logoColor=white)](https://redis.io/)
[![RabbitMQ](https://img.shields.io/badge/RabbitMQ-3-FF6600?logo=rabbitmq&logoColor=white)](https://www.rabbitmq.com/)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)

---

## 🎯 El Proyecto en 30 Segundos

Construí una **plataforma SaaS completa** aplicando arquitectura empresarial de nivel senior: **Hexagonal Architecture + Domain-Driven Design + CQRS + Event-Driven Architecture**.

El objetivo es resolver un problema real (personas que no saben combinar su ropa) mientras demuestro capacidad técnica para roles de **Senior Backend Developer**.

**Stack Técnico:** Laravel 12, PostgreSQL 16, Redis 7, RabbitMQ 3, Docker  
**Arquitectura:** Separación completa de capas, domain-first, eventos asíncronos  
**Testing:** 85% coverage, PHPStan Level 8, SQLite in-memory para tests

---

## 💡 El Problema que Resuelve

**Millones de personas tienen dificultades para:**
- Elegir qué ponerse cada día según clima, ocasión, tipo de cuerpo
- Combinar prendas de forma que les favorezca (teoría del color, proporciones)
- Visualizar cómo les quedará una combinación antes de probársela
- Obtener feedback rápido de su comunidad o estilistas profesionales

**CombinaMejor ofrece:**
- 🎨 Recomendaciones inteligentes basadas en IA, clima (OpenWeatherMap API) y contexto
- 👗 Armario virtual con gestión de prendas (fotos, categorización, búsqueda semántica)
- 🖼️ Visualización 2D/3D con avatar personalizado
- 👥 Comunidad para compartir outfits y recibir valoraciones
- ⚡ Arquitectura escalable lista para millones de usuarios

---

## 📐 Arquitectura (Vista Rápida)

### Arquitectura Hexagonal + DDD + CQRS

```
┌────────────────────────────────────────────────────────┐
│                  PRESENTATION LAYER                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ REST API     │  │ Controllers  │  │ Middleware   │  │
│  │ (Laravel)    │  │ (Single      │  │ (Auth, CORS) │  │
│  │              │  │  Action)     │  │              │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└───────────────────────────┬────────────────────────────┘
                            │ DTOs
                            ↓
┌────────────────────────────────────────────────────────┐
│                   APPLICATION LAYER                    │
│  ┌────────────────────────────────────────────────┐    │
│  │          CQRS - Command Side                   │    │
│  │  Commands → Handlers → Domain Events           │    │
│  │  (Write Operations)                            │    │
│  └────────────────────────────────────────────────┘    │
│  ┌────────────────────────────────────────────────┐    │
│  │          CQRS - Query Side                     │    │
│  │  Queries → Handlers → DTOs                     │    │
│  │  (Read Operations with Cache)                  │    │
│  └────────────────────────────────────────────────┘    │
└───────────────────────────┬────────────────────────────┘
                            │ Repository Interfaces
                            ↓
┌────────────────────────────────────────────────────────┐
│                      DOMAIN LAYER                      │
│         (Framework-agnostic business logic)            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Entities     │  │ Value Objects│  │ Aggregates   │  │
│  │ - User       │  │ - UserId     │  │ - Wardrobe   │  │
│  │ - Wardrobe   │  │ - Email      │  │              │  │
│  │ - Outfit     │  │ - Password   │  │              │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Domain Events│  │ Repositories │  │ Services     │  │
│  │ - UserReg'd  │  │ (Interfaces) │  │ (Domain      │  │
│  │ - ItemAdded  │  │              │  │  Logic)      │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└───────────────────────────┬────────────────────────────┘
                            │ Dependency Inversion
                            ↓
┌────────────────────────────────────────────────────────┐
│                  INFRASTRUCTURE LAYER                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Eloquent     │  │ RabbitMQ     │  │ Redis Cache  │  │
│  │ Repositories │  │ Publisher    │  │ (Read Models)│  │
│  │ (PostgreSQL) │  │ (MessageBus) │  │              │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Migrations   │  │ Consumers    │  │ External APIs│  │
│  │              │  │ (Async)      │  │ (Weather)    │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
└────────────────────────────────────────────────────────┘
```

### Flujo Event-Driven: User Registration

```
[Client] 
   │
   │ POST /api/auth/register
   ↓
[RegisterController] ────→ [RegisterUserCommand]
                             │
                             ↓
                     [RegisterUserHandler]
                        │         │
        ┌───────────────┘         └────────────┐
        ↓                                      ↓
  [PostgreSQL]                         [RabbitMQ Publisher]
   (Write DB)                          (UserRegistered Event)
        │                                      │
        │                                      ↓
        │                              [user_registered Queue]
        │                                      │
        │                                      ↓
        │                          [SendWelcomeEmailConsumer]
        │                           (Async Background Process)
        │                                      │
        └──────────────────────────────────────┘
                         │
                         ↓
                  [User Notified]
```

---

## 🔥 Highlights Técnicos

### Arquitectura & Patrones

✅ **Hexagonal Architecture** - Domain completamente desacoplado del framework  
✅ **Domain-Driven Design** - Aggregates, Value Objects, Domain Events, Bounded Contexts  
✅ **CQRS** - Write operations en PostgreSQL, Read projections en Redis  
✅ **Event-Driven** - RabbitMQ con ACK/NACK, persistent messages, dead letter queues  
✅ **Repository Pattern** - Interfaces en Domain, implementaciones en Infrastructure  
✅ **Single Action Controllers** - Un endpoint = un controller = máxima claridad  

### Value Objects & Domain Logic

✅ **Email** - Validación de formato + lowercasing automático  
✅ **UserId** - UUID v4 con validación estricta  
✅ **PasswordHash** - Bcrypt con cost factor configurable  
✅ **Invariantes garantizados** - Impossible states are impossible  

### Infraestructura

✅ **PostgreSQL 16** - JSONB para metadatos, full-text search, pgvector ready  
✅ **Redis 7** - Cache de proyecciones CQRS, sessions, rate limiting  
✅ **RabbitMQ 3** - Message broker con Management UI, durable queues  
✅ **Docker Compose** - Multi-container orchestration con healthchecks  

### Testing & Quality

✅ **PHPStan Level 8** - Static analysis con strict types everywhere  
✅ **85% Code Coverage** - Unit, Integration y Feature tests  
✅ **SQLite in-memory** - Tests ultra-rápidos sin dependencias externas  
✅ **Laravel Pint** - Code style automation (PSR-12)  

---

## 📊 Métricas del Proyecto

| Métrica | Valor |
|---------|-------|
| **Líneas de código** | ~2,500 |
| **Cobertura de tests** | 85% |
| **PHPStan Level** | 8 |
| **Bounded Contexts** | 2 (Auth, Wardrobe) |
| **Aggregates** | 3 |
| **Value Objects** | 8 |
| **Domain Events** | 5 |
| **Commands** | 7 |
| **Queries** | 4 |

### Performance Targets (MVP)

| Operación | Objetivo | Estado |
|-----------|----------|--------|
| **User registration** | < 200ms | ✅ Logrado |
| **Login** | < 150ms | ✅ Logrado |
| **Wardrobe query (cached)** | < 100ms | 🔄 En desarrollo |
| **Outfit recommendation** | < 500ms | 📅 Pendiente |
| **Event processing** | Async | ✅ RabbitMQ |

---

## 🚀 Roadmap

### ✅ Fase 0: Fundamentos Sólidos (COMPLETADA)
- [x] Docker + Laravel 12 + Arquitectura Hexagonal
- [x] PostgreSQL 16 con migraciones + healthchecks
- [x] Redis para cache/sessions
- [x] RabbitMQ con consumer funcional (ACK/NACK)
- [x] Auth completo (Register, Login, Logout)
- [x] Tests de integración con SQLite in-memory
- [x] PHPStan Level 8 + Laravel Pint
- [x] Domain Events funcionando end-to-end

### 🔄 Fase 1: Bounded Context - Wardrobe (EN DESARROLLO)
- [ ] Entities: Wardrobe, WardrobeItem con aggregate root
- [ ] Value Objects: ClothingType, Season, Color, Size
- [ ] Commands: AddItemToWardrobe, RemoveItem, UpdateItem
- [ ] Queries: GetWardrobe, GetItemsByType (con cache Redis)
- [ ] File upload para fotos de prendas (AWS S3 / local storage)
- [ ] Domain Events: ItemAddedToWardrobe, ItemRemoved
- [ ] Tests unitarios completos del agregado

**Objetivo:** Usuario puede gestionar su armario virtual con CRUD completo

### 📅 Fase 2: Motor de Recomendaciones V1 (Semanas 6-8)
- [ ] Integración OpenWeatherMap API
- [ ] Value Objects: Temperature, WeatherCondition, Occasion
- [ ] Algoritmo básico de recomendación:
  - Temperatura → Tipo de prenda sugerida
  - Ocasión → Nivel de formalidad
  - Teoría del color → Colores complementarios
- [ ] Query: GetRecommendations con cache Redis (TTL 1 hora)
- [ ] Command: RateRecommendation (feedback loop para ML futuro)
- [ ] Domain Event: RecommendationGenerated

**Objetivo:** Usuario recibe 3 recomendaciones diarias personalizadas

### 📅 Fase 3: Visualización 2D + Social (Semanas 9-11)
- [ ] Guardar outfits favoritos (Outfit aggregate)
- [ ] Sistema de valoración (likes/dislikes)
- [ ] Compartir outfit con link público (UUID-based)
- [ ] Comentarios en outfits (Comment entity)
- [ ] Feed de comunidad básico (proyección CQRS)
- [ ] Notificaciones en tiempo real (WebSockets / Server-Sent Events)

**Objetivo:** Usuario puede guardar y compartir sus mejores looks

### 📅 Fase 4: MVP Completo + Deploy (Semana 12)
- [ ] Landing page profesional
- [ ] Onboarding flow (tutorial interactivo)
- [ ] Analytics básico (Plausible / Google Analytics)
- [ ] CI/CD con GitHub Actions
- [ ] Deploy en Railway / DigitalOcean App Platform
- [ ] Domain custom + SSL (Let's Encrypt)
- [ ] 50 beta testers reales para validación

**Objetivo:** Producto EN VIVO validando hipótesis con usuarios reales

### 🔮 Futuro (Post-MVP)
- [ ] Avatar 3D con Three.js / React Three Fiber
- [ ] ML model propio entrenado con datos reales
- [ ] Estilistas profesionales en plataforma (marketplace)
- [ ] App móvil (React Native)
- [ ] Integración con e-commerce (afiliación Amazon/Zara)
- [ ] Realidad aumentada (AR try-on con WebXR)

---

## 🎓 Decisiones Arquitectónicas Clave

### ¿Por qué PostgreSQL sobre MySQL?

**Razones principales:**
- ✅ **JSONB nativo** para metadatos flexibles de prendas sin migraciones constantes
- ✅ **Full-text search** para búsqueda natural ("camisa azul casual verano")
- ✅ **pgvector extension** (futuro) para búsquedas semánticas con IA
- ✅ **Superior performance** en queries complejas con JOINs y agregaciones

### ¿Por qué RabbitMQ sobre Redis Queue?

**Razones principales:**
- ✅ **Garantías de entrega** con ACK/NACK (at-least-once delivery)
- ✅ **Dead Letter Queues** para manejo robusto de errores
- ✅ **Persistencia de mensajes** (survive broker restart)
- ✅ **Management UI** para debugging en tiempo real
- ✅ **Framework-agnostic** (no vendor lock-in con Laravel)

### ¿Por qué Hexagonal + DDD?

**Razones principales:**
- ✅ **Desacoplamiento total** del framework Laravel (testeable sin dependencias)
- ✅ **Lógica de negocio en Domain** agnóstica de infraestructura
- ✅ **Portabilidad extrema** - Puedo cambiar DB, message broker, framework
- ✅ **Evolución a microservicios** facilitada (bounded contexts ya definidos)
- ✅ **Testabilidad máxima** - Unit tests sin tocar base de datos

**Trade-off aceptado:** Mayor inversión inicial (~30-40% más tiempo) vs mantenibilidad y escalabilidad a largo plazo

---

## 📚 Stack Técnico Completo

### Backend
- **Lenguaje:** PHP 8.2 (strict types, named arguments, readonly properties)
- **Framework:** Laravel 12 (API-only, Sanctum authentication)
- **Arquitectura:** Hexagonal + DDD + CQRS + Event-Driven

### Base de Datos
- **Write DB:** PostgreSQL 16 Alpine (UUID primary keys, JSONB, full-text search)
- **Cache/Sessions:** Redis 7 Alpine
- **Read Models:** Redis (CQRS projections)

### Mensajería
- **Message Broker:** RabbitMQ 3 con Management UI
- **Library:** php-amqplib
- **Pattern:** Publisher/Consumer con ACK/NACK

### Infraestructura
- **Containerización:** Docker Compose
- **CI/CD:** GitHub Actions (planned)
- **Deployment:** Railway / DigitalOcean (planned)

### Testing & QA
- **Testing:** PHPUnit 11 (Unit + Integration + Feature)
- **Static Analysis:** PHPStan Level 8
- **Code Style:** Laravel Pint (PSR-12)
- **Coverage:** 85%+ goal

---

## 👤 Autor

**Roberto Ruiz Vazquez**  
*Full-Stack Developer | Clean Architecture & DDD Enthusiast*

📧 roberruizvazquez@gmail.com  
💼 [LinkedIn](https://linkedin.com/in/robertoruizvazquez)  
🐙 [GitHub](https://github.com/combinamejor)

### 💼 Buscando Oportunidades

Actualmente **disponible** para posiciones **Senior Backend Developer** con foco en:

- ✅ Clean Architecture & Domain-Driven Design
- ✅ Event-Driven Systems (RabbitMQ, Kafka, AWS SQS)
- ✅ Arquitecturas escalables (CQRS, Microservices, Event Sourcing)
- ✅ PHP/Laravel, PostgreSQL, Redis, Docker
- ✅ Testing strategies & Quality assurance

**¿Tienes una oportunidad interesante?** → Contáctame en [LinkedIn](https://linkedin.com/in/robertoruizvazquez)

---

## 🔒 Nota sobre el Código Fuente

El código de este proyecto está en un **repositorio privado** por razones de propiedad intelectual, pero está disponible para:

- ✅ **Code review durante procesos de entrevista técnica**
- ✅ **Live coding sessions** y discusiones arquitectónicas en profundidad
- ✅ **Demos en vivo** del sistema funcionando

**💡 La arquitectura completa y decisiones técnicas están documentadas públicamente en este repositorio.**

Si eres reclutador técnico o tech lead y quieres profundizar en la implementación, estaré encantado de hacer un walkthrough del código en una sesión técnica.

---

## 📖 Recursos de Aprendizaje

Este proyecto fue construido aplicando conocimientos de:

- **Domain-Driven Design** - Eric Evans
- **Implementing Domain-Driven Design** - Vaughn Vernon
- **Clean Architecture** - Robert C. Martin
- **Building Microservices** - Sam Newman
- **Enterprise Integration Patterns** - Gregor Hohpe

---

## 🙏 Agradecimientos

- **Anthropic Claude** - Asistencia en arquitectura, refactoring y best practices
- **Comunidad Laravel** - Framework y ecosystem robusto
- **DDD Community** - Recursos y guías de patrones tácticos
- **Futuros beta testers** - Por ayudar a validar la hipótesis de producto

---

<div align="center">

**⭐ Si este proyecto te inspira o te resulta útil, dale una estrella ⭐**

**🚀 Construido con arquitectura limpia, patrones probados y mucho café ☕**

</div>
