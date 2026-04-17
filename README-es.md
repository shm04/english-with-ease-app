# English With Ease (EWE) — Plataforma LMS

> **Categoría:** SaaS EdTech Privado 
> **Cliente:** EWE Academy  
> **Estado del Proyecto:** En Producción (v1.2)

---

# 📗 Tabla de Contenidos
- [📖 Acerca del Proyecto](#acerca-del-proyecto)
- [🚀 Características Principales](#caracteristicas-principales)
- [🏗️ Diseño Arquitectónico](#diseno-arquitectonico)
- [💻 Stack Tecnológico](#stack-tecnologico)
- [🧗 Profundidad Técnica](#profundidad-tecnica)
- [🔒 Propiedad Intelectual y Acceso al Código](#acceso-al-codigo)
- [🔭 Roadmap de Futuras Características](#futuras-caracteristicas)
- [👥 Autores](#autores)
- [📝 Licencia](#licencia)

---

## 📖 Acerca del Proyecto <a name="acerca-del-proyecto"></a>
Antes de la plataforma EWE, las operaciones de la academia estaban fragmentadas. Los instructores perdían entre **5 y 10 horas por semana** en tareas administrativas manuales: buscar en Google Drive, renombrar grabaciones de Google Meet, ajustar permisos de uso compartido y distribuir enlaces manualmente vía WhatsApp. 

EWE es un Sistema de Gestión de Aprendizaje (LMS) construido a medida, diseñado para centralizar la gestión académica y eliminar la fricción administrativa a través de una automatización profunda.

**Enlaces Clave:**
* [Live Demo / Sitio Web](#) 
* [Recorrido en Video (Loom)](#)

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🚀 Características Principales <a name="caracteristicas-principales"></a>
* **Motor de Sincronización Automática con Google Workspace:** Un servicio en segundo plano que identifica grabaciones de Google Meet en tiempo real, las mueve a directorios organizados, actualiza los permisos de visualización mediante API y las publica de forma segura.
* **Infraestructura de Auto-Recuperación (Auto-Healing):** Lógica de sistema de archivos resiliente que detecta si los directorios de Google Drive son renombrados o eliminados, remapeándolos automáticamente para evitar enlaces rotos.
* **Portales Multi-Rol (Multi-Tenant):** Entornos personalizados y seguros para Administradores, Profesores y Estudiantes.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🏗️ Diseño Arquitectónico <a name="diseno-arquitectonico"></a>
El proyecto sigue una **Arquitectura de Capas Modulares** inspirada en los principios de la **Arquitectura Hexagonal / Clean Architecture**.

* **Módulos Basados en Dominio (DDD):** El sistema está dividido en dominios lógicos: `Auth`, `Courses`, `Enrollments`, `Recordings` y `Dashboard`.
* **Adaptadores Primarios (Driving):** Controladores de Express.js v5 que manejan estrictamente las peticiones HTTP.
* **Capa de Servicios (Lógica de Negocio):** Lógica pura que reside en servicios como `SyncRecordingsService`.
* **Adaptadores Secundarios (Driven):** * **Patrón Repositorio:** Desacopla las operaciones de PostgreSQL (Neon DB) de la capa de negocio.
  * **Adaptadores de Infraestructura:** Módulos dedicados para la API de Google Drive y la API de Google Meet.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 💻 Stack Tecnológico <a name="stack-tecnologico"></a>
* **Frontend:** React 19, Vite v7, Tailwind CSS v4, Zustand, TanStack Query v5.
* **Backend:** Node.js, Express v5, `node-cron`.
* **Base de Datos:** PostgreSQL (Neon DB).
* **Infraestructura:** APIs de Google Workspace, Netlify, Railway.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🧗 Profundidad Técnica: El Reto del Motor de Sincronización <a name="profundidad-tecnica"></a>
El desafío de ingeniería más complejo fue manejar los límites de tasa (rate limits) de la API de Google mientras se movían archivos de video pesados y se aseguraba un 100% de disponibilidad en los permisos.  

**La Solución de Ingeniería:** 1. Se implementó una **Máquina de Estados de Validación** que comprueba la integridad de la carpeta antes de cualquier operación de sincronización.
2. Se desarrolló un **Mecanismo de Auto-Healing** utilizando un manejo de errores personalizado para detectar errores de "Archivo no encontrado" y activar una reconstrucción recursiva del directorio.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🔒 Propiedad Intelectual y Acceso al Código <a name="acceso-al-codigo"></a>
El código fuente de este proyecto es **Propiedad Privada** de Elevate Agency y EWE Academy. No está abierto para clonación pública ni contribuciones.

**Revisión del código:**
Estoy disponible para realizar un **Recorrido Técnico (Technical Walkthrough)** a través de pantalla compartida durante una entrevista. En esta sesión, puedo demostrar la estructura de carpetas, la implementación del Patrón Repositorio y la lógica de gestión de estado.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🔭 Roadmap de Futuras Características <a name="futuras-caracteristicas"></a>
- [ ] **Motor de Pruebas Avanzado Integrado:** Evaluaciones diagnósticas interactivas (completar espacios, comprensión lectora, calificación en vivo) directamente en la plataforma para medir el progreso del estudiante.
- [ ] **Analíticas Impulsadas por IA:** Seguimiento de métricas de retención de estudiantes basadas en el tiempo de visualización de videos.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 👥 Autores <a name="autores"></a>

👤 **Sebastián Hernández**
* **Rol:** Lead Developer / Arquitecto
* **Agencia:** [Elevate Agency](https://your-elevate-link.com)
* **LinkedIn:** [Sebastián Hernández](https://www.linkedin.com/in/your-profile)
* **GitHub:** [@your-github](https://github.com/your-github)

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 📝 Licencia <a name="licencia"></a>
Este proyecto es de **Propiedad Privada y Código Cerrado**. Todos los derechos reservados por Elevate Agency y EWE Academy.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>
