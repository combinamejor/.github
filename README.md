# 👗 Combinamejor

![Status](https://img.shields.io/badge/Status-WIP-orange)
![PHP](https://img.shields.io/badge/PHP-8.2-blue)
![Laravel](https://img.shields.io/badge/Laravel-12-red)
![React](https://img.shields.io/badge/React-18-61dafb)
![Docker](https://img.shields.io/badge/Docker-ready-0db7ed)
![AWS](https://img.shields.io/badge/AWS-preparing-232f3e)
![License](https://img.shields.io/badge/license-MIT-green)

**Combinamejor** es una plataforma que ayuda a los usuarios a **combinar prendas y accesorios de forma inteligente y visual**, creando outfits personalizados de manera rápida y sencilla.  
El proyecto sigue una arquitectura **desacoplada** (backend + frontend) y está diseñado con **buenas prácticas de ingeniería de software** para garantizar escalabilidad, mantenibilidad y seguridad.

---

## 🌟 Visión

- Simplificar la elección diaria de ropa mediante combinaciones automáticas.  
- Ofrecer un sistema visual que permita gestionar el armario digital del usuario.  
- Integrar algoritmos inteligentes para generar sugerencias personalizadas.  
- Construir un servicio cloud seguro para el almacenamiento y sincronización.  

---

## 🛠️ Arquitectura

El proyecto está dividido en varios repositorios:

- [📡 Backend (Laravel API)](https://github.com/combinamejor/combinamejor-web) – API RESTful en PHP 8.2 + Laravel 12, con autenticación y motor de reglas.  
- [🎨 Frontend (React)](https://github.com/combinamejor/combinamejor-web-client) – Interfaz visual en React + Vite para gestionar prendas y combinaciones.  
- [📖 Documentación](https://github.com/combinamejor/combinamejor-docs) _(en preparación)_ – Guías de uso, arquitectura y despliegue.

---

## 🚀 Estado actual

- ✅ Registro y login de usuarios con Sanctum.  
- ✅ Arquitectura desacoplada (API + cliente separado).  
- 🔄 Desarrollo del inventario de prendas.  
- ⏳ Motor de combinaciones inteligentes.  
- ⏳ Panel visual de outfits.  
- ⏳ Integración con AWS (ECS, ECR, S3, RDS).  

---

## 📌 Roadmap global

- [ ] Completar CRUD de prendas y accesorios.  
- [ ] Implementar motor de combinaciones basado en reglas e IA.  
- [ ] Integrar almacenamiento seguro en la nube (AWS).  
- [ ] Lanzar versión beta del frontend.  
- [ ] Mejorar documentación y abrir el proyecto a colaboradores externos.  

---

## 🧑‍💻 Tecnologías principales

- **Backend:** PHP 8.2, Laravel 12, MySQL, Redis, PHPUnit  
- **Frontend:** React + Vite, TailwindCSS  
- **Infraestructura:** Docker, Jenkins, AWS (ECS, ECR, S3, RDS)  
- **Patrones:** DDD + CQRS + SOLID  

---

## 📷 Demo (en desarrollo)

_(Próximamente capturas y/o gif mostrando el flujo básico: login → inventario → combinaciones)_

---

## 🤝 Contribuciones

Este proyecto se encuentra en desarrollo privado.  
Si te interesa colaborar, contáctanos directamente.

---

## 📄 Licencia

Este proyecto está bajo la licencia MIT.  
Consulta el archivo [LICENSE](LICENSE) para más detalles.
