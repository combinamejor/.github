# 🌟 Combinamejor  
### Plataforma de Armario Inteligente · Arquitectura Profesional · Seguridad y DevOps Moderno 🚀

![Status](https://img.shields.io/badge/Status-In_Active_Development-orange)
![PHP](https://img.shields.io/badge/PHP-8.2-blue)
![Laravel](https://img.shields.io/badge/Laravel-12-red)
![React](https://img.shields.io/badge/React-18-61dafb)
![Docker](https://img.shields.io/badge/Docker-Ready-0db7ed)
![AWS](https://img.shields.io/badge/AWS-Integration_in_progress-232f3e)
![Security](https://img.shields.io/badge/Security-Enhanced-green)
![CI/CD](https://img.shields.io/badge/CI/CD-Jenkins_+_GitHub_Actions-blue)
![Architecture](https://img.shields.io/badge/Architecture-DDD_+_CQRS-green)
![License](https://img.shields.io/badge/License-Private-yellow)

---

# 👕 ¿Qué es Combinamejor?

**Combinamejor** es una plataforma que ayuda a los usuarios a **gestionar su armario digital y crear outfits inteligentes de manera visual y rápida**.  
El proyecto se desarrolla con estándares profesionales de arquitectura, seguridad, despliegue y automatización.

Es el tipo de proyecto que una empresa moderna **podría desplegar en producción sin reescribir nada**.

---

# 🔐 Seguridad e Infraestructura (DevSecOps Ready)

Combinamejor se construye siguiendo una **arquitectura segura y automatizada**, con herramientas reales del mundo empresarial.

---

# 🛡️ **Prehooks locales (Seguridad del repositorio)**

Se utilizan **Git pre-push hooks** para evitar que llegue código inseguro o con errores al repositorio:

### ✔ Controles antes de cada push:
- `PHPStan` (nivel estricto)
- `Pint` (estilo PSR-12 automático)
- `PHPUnit` (tests deben pasar)
- Bloqueo de pushes si algo falla
- Control de credenciales expuestas

Esto garantiza que **ningún commit rompe la calidad del proyecto**.

---

# 🔄 **Integración Continua (CI)**

## 🚦 **GitHub Actions (Análisis inmediato en cada push)**

Pipeline CI:
- PHP 8.2 environment
- Instalación de dependencias
- Ejecución de PHPStan
- Ejecución de Pint
- Ejecución de tests (Feature + Unit)
- Validación del árbol DDD/CQRS

Resultado:
✔ Seguridad estática  
✔ Estilo de código  
✔ Test suite estable  
✔ Código listo para pasar a Jenkins/Producción  

*(Workflow privado por razones de seguridad)*

---

# 🔧 **Despliegue Continuo (CD) con Jenkins**

Combinamejor usa **Jenkins** en un servidor EC2 para gestionar:

### 📌 Pipeline de despliegue real
- Build de imagen Docker del backend
- Login automático en ECR (Amazon)
- Push de la imagen versionada al repositorio privado
- Lanzamiento del servicio ECS (staging/production)
- Limpieza de imágenes antiguas
- Notificaciones en consola

### ✔ Seguridad aplicada:
- IAM Roles mínimos para Jenkins
- AWS CLI configurada en servidor aislado
- tokens/credentials gestionados por variables de entorno

---

# ☁️ **Infraestructura en AWS (preparada para producción)**

### Servicios AWS utilizados:
- **ECS Fargate** → Ejecución serverless del backend
- **ECR** → Almacenamiento seguro de imágenes Docker
- **S3** → Gestión de imágenes de prendas y estáticos
- **IAM** → Roles con permisos mínimos
- **EC2** → Jenkins y monitorización
- **CloudWatch** → Logs estructurados

### Arquitectura objetivo (2025)
```
GitHub → GitHub Actions → Jenkins → Docker Image → ECR → ECS Fargate → S3 + RDS
```

---

# 🧱 Arquitectura del Proyecto

Combinamejor está dividido en repositorios independientes:

### 📡 Backend API (Privado)
- Laravel 12 (PHP 8.2)
- Arquitectura **DDD + CQRS**
- Servicios desacoplados
- Repositorios anti-Eloquent
- Testing completo
- Tokenización (Sanctum)
- Preparado para eventos y mensajería (RabbitMQ + Elixir)

### 🎨 Frontend (Privado)
- React 18 + Vite
- TailwindCSS
- Componentes desacoplados
- Armario visual + Outfits builder (en progreso)

### 📘 Documentación (En evolución)
- Diagramas de arquitectura
- Infraestructura cloud
- Guías de despliegue
- Roadmaps empresariales

---

# 🚀 Estado Actual del Desarrollo

### ✔ Backend
- Módulo Auth completado (Register/Login/Logout)
- Domain-Driven Design limpio
- Commands + Handlers (CQRS)
- ValueObjects estrictos
- Repositorios desacoplados de Eloquent
- Seguridad avanzada con prehooks + CI

### ✔ Frontend
- Flujo inicial y prototipado
- Integración con API en curso

### 🔄 Próximos pasos
- CRUD de prendas
- Motor de combinaciones inteligente
- Panel visual de outfits
- Integración con AWS ECS Fargate
- Sistema de colas con RabbitMQ + Elixir

---

# 🛣 Roadmap Global

- [x] Backend DDD base  
- [x] Módulo Auth completo  
- [x] Seguridad y prehooks  
- [x] Jenkins + ECR + CD  
- [ ] Wardrobe Engine  
- [ ] Outfit Engine  
- [ ] Recommender System (AI)  
- [ ] RabbitMQ Event Bus  
- [ ] Monitorización y observabilidad  
- [ ] Despliegue en producción AWS  

---

# 👨‍💻 Tecnologías y Buenas Prácticas

| Área | Tecnologías |
|------|-------------|
| Backend | PHP 8.2 · Laravel 12 · Sanctum |
| Frontend | React 18 · Vite · TailwindCSS |
| Arquitectura | DDD · CQRS · Hexagonal · SOLID |
| Testing | PHPUnit · Feature Tests |
| Seguridad | Prehooks · GitHub Actions · IAM |
| Contenedores | Docker · Docker Compose |
| CI/CD | GitHub Actions · Jenkins |
| Cloud | AWS ECS · ECR · S3 · IAM |

---

# 📷 Demo (Próximamente)

Se incluirá una demo visual del flujo completo:

- Registro / Login  
- Armario digital  
- Combinaciones inteligentes  
- Outfits visuales  

---

# 🤝 Contribuciones

Este proyecto es privado.  
Si deseas colaborar:

📩 Contacto directo (LinkedIn o email)

---

# 📄 Licencia

Todo el contenido es privado, con derechos reservados.  
No se permite copiar, usar ni redistribuir sin autorización.

---

# 🎯 Nota final

Combinamejor es un proyecto en crecimiento continuo, construido con:

- Arquitectura moderna  
- Seguridad real  
- DevOps actual  
- Visión de producto sólida  
- Mentalidad profesional y escalable  

Un espacio pensado para reclutadores, colaboradores y profesionales que quieran ver **cómo construyo software**.

