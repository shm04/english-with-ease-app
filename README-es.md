# English With Ease (EWE) — Monorepo EdTech y Ecosistema LMS

> **Categoría:** SaaS EdTech Empresarial / Monorepo  
> **Cliente:** EWE Academy  
> **Lead Architect:** Sebastian Hernandez ([Elevate Agency](https://your-elevate-link.com))  
> **Estado del Proyecto:** En Producción (v2.0)

---

## 🌎 Idiomas
Leer en [Inglés](./README.md)

---

# 📗 Tabla de Contenidos
- [📖 Acerca del Proyecto y Filosofía Central](#acerca-del-proyecto)
- [🧠 Arquitectura: Modelo "Motor vs. Combustible"](#arquitectura)
- [🚀 Características Principales y Módulos](#caracteristicas-principales)
- [🗄️ Esquema de Base de Datos y Lógica de Gating](#base-de-datos)
- [💻 Stack Tecnológico y DevOps](#stack-tecnologico)
- [🧗 Profundidad Técnica](#profundidad-tecnica)
- [🔒 Política de Acceso al Código](#acceso-al-codigo)
- [👥 Autores](#autores)
- [📝 Licencia](#licencia)

---

## 📖 Acerca del Proyecto y Filosofía Central <a name="acerca-del-proyecto"></a>
EWE Academy es una plataforma EdTech moderna y escalable, diseñada para automatizar por completo el ciclo de vida del aprendizaje de idiomas. Construida como un **Monorepo** integral, contiene un Sistema de Gestión de Aprendizaje (LMS) a medida con estricta trazabilidad de datos.

La plataforma elimina la fricción administrativa (como la sincronización manual de grabaciones en Google Drive) mientras proporciona una experiencia premium y optimizada para la conversión de prospectos.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🧠 Arquitectura: Modelo "Motor vs. Combustible" <a name="arquitectura"></a>
La filosofía central de esta plataforma es la estricta separación de la lógica y el contenido.
* **El Motor (Engine):** El código fuente de la aplicación (arquitectura LMS, seguimiento, lógica de bloqueo y embudo de marketing). Es completamente agnóstico al contenido específico de inglés.
* **El Combustible (Fuel):** El contenido pedagógico (el Syllabus), mapeado a IDs inmutables e inyectado dinámicamente en la base de datos.

### Jerarquía de Datos del LMS (El ADN)
La arquitectura impone estrictamente esta progresión jerárquica:
1. **Book (Subnivel):** ej. A1.1, A1.2.
2. **Unit (Unidad):** 3 unidades por Book.
3. **Topic (Semana):** 1 Tema de conversación por semana.
4. **Assets (El Combustible):** Mini-Lecciones renderizadas a través de F-Components dinámicos (F1: Video, F2: Interactivo, F3: Audio, F4: Gramática), además de Quizzes (Exámenes) y subida de Evidencias.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🚀 Características Principales y Módulos <a name="caracteristicas-principales"></a>
* **Sincronización Automatizada con Google Workspace:** Un motor en segundo plano que detecta grabaciones de Google Meet, actualiza permisos y las publica de forma segura en el portal del estudiante sin intervención humana.
* **Motor Dinámico de Prueba de Nivel:** Un motor de evaluación polimórfico que soporta multimedia y varios tipos de preguntas. Cuenta con un **Algoritmo de Terminación Temprana** que detiene la prueba automáticamente si el usuario no supera un bloque de nivel específico, generando resultados compartibles.
* **Embudo de Marketing y Captura de Leads:** Páginas de aterrizaje optimizadas para CRO utilizando estrategias de precios ancla. Los leads se almacenan de forma segura en `ewe_marketing_leads` antes de pasar al motor de pruebas para evitar la fuga de datos.
* **Gestor de Contenido Admin (En Desarrollo):** Una interfaz de vista de árbol para que el equipo académico suba "Combustible", establezca reglas de bloqueo (gating) y mapee datos del syllabus (CSV/Excel) directamente a PostgreSQL.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🗄️ Esquema de Base de Datos y Lógica de Gating <a name="base-de-datos"></a>
* **Gating Académico:** Implementa bloqueos suaves/duros (Soft/Hard gating). Los estudiantes deben interactuar con las Mini-Lecciones (ML1-ML3) para desbloquear el Quiz Semanal. 
* **Fórmula de Finalización:** Un Topic alcanza el 100% de finalización mediante un cálculo estricto: **40% Mini-Lecciones + 30% Quiz (requiere puntaje >= 70%) + 30% Evidencia**. Rastreado eficientemente a través de la tabla pivote `user_topic_progress`.
* **Motor de Analíticas JSONB:** La prueba de nivel genera métricas granulares (proporciones de correctas/totales por Sección y Nivel). Para evitar inflar la base de datos, este payload se procesa y se guarda silenciosamente en una potente columna `JSONB` dentro de `ewe_test_results`.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 💻 Stack Tecnológico y DevOps <a name="stack-tecnologico"></a>
* **Frontend:** React 19, Vite, Tailwind CSS v4, React Router DOM, Lucide React.
* **Backend:** Node.js, Express.js.
* **Base de Datos:** PostgreSQL (Alojada en Neon.tech).
* **Rendimiento:** Scripts de automatización en Node.js que utilizan `sharp` para la descarga de imágenes externas y su conversión a WebP.
* **Despliegue y DevOps:** * **Frontend (Netlify):** Configurado vía `netlify.toml` para un enrutamiento SPA estricto y la inyección de tipos MIME para prevenir errores de carga de assets en Vite.
  * **Backend (Railway):** Conexiones SSL seguras a Neon DB forzadas mediante los flags `?sslmode=require&uselibpqcompat=true`.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🧗 Profundidad Técnica: Motor de Sincronización y Autorrecuperación <a name="profundidad-tecnica"></a>
Junto con la compleja lógica de Gating 40/30/30, el desafío backend más significativo fue el **Motor de Sincronización de Google Drive**. 

Manejar los límites de tasa de la API de Google mientras se movían archivos de video pesados requirió construir una **Infraestructura de Auto-Recuperación (Auto-Healing)**. El sistema utiliza un manejo de errores personalizado para detectar errores de "Archivo no encontrado" si un directorio es renombrado manualmente, activando una reconstrucción recursiva del directorio para asegurar que los enlaces nunca se rompan.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 🔒 Política de Acceso al Código <a name="acceso-al-codigo"></a>
El código fuente de este proyecto es **Propiedad Privada**. No está abierto para clonación pública ni contribuciones.

Estoy disponible para realizar un **Recorrido Técnico (Technical Walkthrough)** a través de una pantalla compartida durante una entrevista. En esta sesión, puedo demostrar la estructura del Monorepo, la lógica de mapeo "Motor vs. Combustible" y la implementación del payload de analíticas JSONB.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 👥 Autores <a name="autores"></a>

👤 **Sebastian Hernandez**
* **Rol:** Lead Architect / Full-Stack Engineer
* **Agencia:** [Elevate Agency](https://your-elevate-link.com)
* **LinkedIn:** [Sebastian Hernandez](https://www.linkedin.com/in/sebastian-hernandez-munoz/)
* **GitHub:** [@your-github](https://github.com/shm04)

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>

## 📝 Licencia <a name="licencia"></a>
Este proyecto es de **Propiedad Privada y Código Cerrado**. Todos los derechos reservados por Elevate Agency y EWE Academy.

<p align="right">(<a href="#readme-top">volver arriba</a>)</p>
