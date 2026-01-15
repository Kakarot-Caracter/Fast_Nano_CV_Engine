# Fast Nano CV Engine

![Versión](https://img.shields.io/badge/version-0.1.0-blue.svg)
![Licencia](https://img.shields.io/badge/license-MIT-green.svg)
![Build](https://img.shields.io/badge/build-passing-brightgreen.svg)

```
    _   __ ___     _   __ ____     ______ _    __
   / | / //   |   / | / // __ \   / ____/| |  / /
  /  |/ // /| |  /  |/ // / / /  / /     | | / /
 / /|  // ___ | / /|  // /_/ /  / /___   | |/ /
/_/ |_//_/  |_|/_/ |_/ \____/   \____/   |___/
```

Un generador de CVs ultrarrápido, simple y elegante a partir de un archivo YAML. Crea un currículum profesional en formato HTML y PDF utilizando plantillas configurables.

## ✨ Características Principales

*   **Entrada de Datos Simple:** Define todo tu currículum en un archivo `YAML` limpio y fácil de editar.
*   **Generación Multi-formato:** Produce una versión web **HTML** y un archivo **PDF** profesional listos para imprimir o enviar.
*   **Motor de Plantillas:** Personaliza la apariencia de tu CV usando el motor de plantillas [Tera](https://keats.github.io/tera/).
*   **Plantillas Incluidas:** Viene con tres temas listos para usar: `base`, `dark` y `modern`.
*   **Rendimiento Nativo:** Construido en Rust para una generación casi instantánea.
*   **Interfaz de Línea de Comandos (CLI):** Integración perfecta en cualquier flujo de trabajo de terminal.

## ⚙️ Cómo Funciona

El motor sigue un proceso simple y eficiente para generar los documentos:

`Archivo YAML de Entrada` → `Motor Rust` → `Renderizado con Plantilla Tera` → `Archivos HTML y PDF de Salida`

## 📋 Prerrequisitos

Antes de empezar, asegúrate de tener lo siguiente instalado en tu sistema:

1.  **Rust y Cargo:** El entorno de desarrollo de Rust. Puedes instalarlo desde [rustup.rs](https://rustup.rs/).
2.  **Google Chrome / Chromium:** La generación de PDF depende de `headless_chrome`, por lo que es necesario tener el navegador instalado.

## 🚀 Instalación y Compilación

Sigue estos pasos para compilar el proyecto y tener el ejecutable listo.

1.  **Clona el Repositorio:**
    ```bash
    git clone https://github.com/Kakarot-Caracter/fast_nano_cv_engine.git
    cd fast_nano_cv_engine
    ```

2.  **Construye para Producción:**
    Este comando compila el proyecto con optimizaciones.
    ```bash
    cargo build --release
    ```

El binario ejecutable final se ubicará en `target/release/fast_nano_cv_engine`.

## USAGE

Una vez compilado, puedes usar el motor directamente desde tu terminal.

### Sintaxis del Comando

```
./target/release/fast_nano_cv_engine <archivo_yaml> [--template <nombre_plantilla>]
```

| Argumento              | Descripción                                                                                                |
| ---------------------- | ---------------------------------------------------------------------------------------------------------- |
| `<archivo_yaml>`       | **(Requerido)** La ruta a tu archivo `.yml` que contiene los datos del currículum.                              |
| `--template <nombre>` | **(Opcional)** El nombre de la plantilla a usar. Si no se especifica, se usará `base` por defecto. |

### Ejemplos de Uso

1.  **Generar CV con la plantilla por defecto (`base`):**
    ```bash
    ./target/release/fast_nano_cv_engine "cv.yml"
    ```

2.  **Generar CV usando la plantilla `modern`:**
    ```bash
    ./target/release/fast_nano_cv_engine "cv.yml" --template modern
    ```

3.  **Generar CV usando la plantilla `dark`:**
    ```bash
    ./target/release/fast_nano_cv_engine "cv.yml" --template dark
    ```

Los archivos resultantes (`.html` y `_CV.pdf`) se guardarán automáticamente en la carpeta `output/`.

### Uso en Desarrollo

Durante el desarrollo, puedes usar `cargo run` para compilar y ejecutar el programa en un solo paso:

```bash
cargo run -- "cv.yml" --template modern
```

## 📄 Formato del Archivo YAML

Para que el motor funcione, tu archivo `cv.yml` debe seguir una estructura específica. A continuación se detalla cada sección, basada en los modelos de datos del programa.

```yaml
personal:
  nombre: Giovanni Martinez
  titulo: Desarrollador Web
  telefono: "+595 972 472824"
  correo: giovannimartinezz122@gmail.com
  ubicacion: Asuncion, Paraguay
  web: "https://mi-portafolio-gamma-two.vercel.app/"
  linkedin: "https://linkedin.com/in/giovanni-martinez7017"
  github: "https://github.com/Kakarot-Caracter"

sobre_mi: >
  Apasionado desarrollador de software especializado en crear aplicaciones web modernas con Next.js, NestJS y tecnologías del ecosistema JavaScript. Desde muy joven, he trabajado en proyectos personales y profesionales que me han permitido fortalecer habilidades tanto en frontend como en backend, siempre explorando nuevas herramientas y soluciones innovadoras.

educacion:
  - institucion: Colegio Tecnico Cerro Cora
    grado: Bachillerato en informática
    ubicacion: Asuncion, Paraguay
    inicio: Feb 2022
    fin: Nov 2024
    logros:
      - Desarrollo de habilidades básicas en programación y resolución de problemas computacionales
      - Comprensión de conceptos fundamentales de informática, algoritmos y estructuras de datos

experiencia:
  - empresa: Taskflow
    puesto: Desarrollador Web
    inicio: Ene 2025
    fin: Mar 2025
    descripcion: >
      Aplicación de gestión de tareas con CRUD completo, filtrado por estado y autenticación de usuarios.
    logros:
      - Gestioné el estado de la aplicación con Zustand y optimicé consultas usando React Query.
      - Implementé una API segura y escalable con NestJS y Prisma.

habilidades:
  - Lenguajes de Programación: JavaScript, TypeScript, Python, Rust
  - Frontend: React, Next.js, TailwindCSS
  - Backend: NestJS, Node.js, REST API
  - Bases de Datos: PostgreSQL, MySQL, MongoDB, Prisma
  - Infraestructura: Linux, Docker, Git
```

### Descripción de las Secciones:

*   `personal`: (Objeto) Tu información de contacto básica. Todos los campos son strings, y la mayoría son opcionales excepto `nombre`, `titulo` y `correo`.
*   `sobre_mi`: (String) Un párrafo de resumen profesional.
*   `educacion`: (Lista de Objetos) Tu historial académico. Cada objeto debe contener `institucion`, `grado`, `inicio`, `fin` y una lista de `logros`.
*   `experiencia`: (Lista de Objetos) Tu historial laboral. Cada objeto debe contener `empresa`, `puesto`, `inicio`, `fin`, una `descripcion` opcional y una lista de `logros`.
*   `habilidades`: (Lista de Mapas) Una lista donde cada ítem es un mapa que representa una categoría y sus habilidades.

## 🎨 Plantillas Personalizadas

Crear tu propia plantilla es fácil:

1.  Crea un nuevo archivo `.html` en la carpeta `src/templates/`.
2.  Utiliza la sintaxis de [Tera](https://keats.github.io/tera/docs/#templates) para acceder a los datos del CV (puedes usar `base.html` como referencia).
3.  Ejecuta el programa apuntando a tu nueva plantilla con el flag `--template`.

Por ejemplo, si creas `mi_plantilla.html`, la usarías así:
```bash
./target/release/fast_nano_cv_engine cv.yml --template mi_plantilla
```

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Si tienes ideas para mejorar el proyecto, por favor abre un *issue* para discutirlo o envía un *pull request*.

## 📜 Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.