# 🎬 Guión Técnico — Planificador Audiovisual Web

<div align="center">

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Modern CSS](https://img.shields.io/badge/CSS-Modern%20(L4+)-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![Versión](https://img.shields.io/badge/versión-v1.0.0-blue?style=for-the-badge)
[![ORCID](https://img.shields.io/badge/ORCID-0000--0003--3842--7694-A6CE39?style=for-the-badge&logo=orcid&logoColor=white)](https://orcid.org/0000-0003-3842-7694)
[![Licencia](https://img.shields.io/badge/Licencia-CC_BY--SA_4.0-orange?style=for-the-badge)](https://creativecommons.org/licenses/by-sa/4.0/)

**Aplicación web autocontenida para crear, editar e imprimir guiones técnicos audiovisuales.**

[Características](#-características) · [Demo](#-demo) · [Uso](#-uso) · [Tecnología](#-stack-tecnológico) · [Contribuir](#-contribuir)

</div>

---

## 📖 Descripción

Herramienta web diseñada para el **ámbito educativo** que permite a estudiantes y docentes construir guiones técnicos audiovisuales de forma interactiva. Sustituye la hoja de cálculo tradicional por un formulario web con validación, cálculos automáticos, panel de referencia integrado y salida optimizada para impresión.

> **Zero dependencias. Zero servidor. Un solo fichero HTML.**

---

## ✨ Características

| Funcionalidad | Descripción |
|---|---|
| 🎨 **Diseño cinematográfico** | Tema oscuro con acentos dorados y separación visual por secuencias |
| 📝 **Formulario completo** | 13 columnas: secuencia, plano, tiempo, descripción, encuadre, angulación, movimiento, intertítulos, efecto de vídeo, transición, sonido, diálogo y duración acumulada |
| 📋 **Desplegables validados** | Menús con opciones de lenguaje audiovisual: 7 encuadres, 5 angulaciones, 6 movimientos, 17 efectos, 9 transiciones |
| ➕ **Filas dinámicas** | Añadir y eliminar planos con auto-incremento de numeración |
| 📊 **Cálculos automáticos** | Duración total, nº de escenas, nº de planos y duración acumulada en tiempo real |
| 📚 **Panel de referencia** | Cajón lateral con 6 pestañas de información sobre lenguaje audiovisual |
| 💾 **Persistencia** | Autoguardado en `localStorage` + exportación/importación JSON |
| 🖨️ **Impresión optimizada** | Hoja de estilos `@media print` en A4 apaisado, limpia y en blanco y negro |
| ⌨️ **Atajos de teclado** | `Ctrl+S` guardar, `Ctrl+P` imprimir, `Ctrl+N` nuevo plano |
| 📱 **Responsive** | Adaptado a pantallas de escritorio, tablet y móvil |
| 🌐 **Offline** | Funciona sin conexión a internet |

---

## 🚀 Demo

Simplemente abre el fichero en tu navegador:

```bash
# Opción 1: doble clic sobre guion-tecnico.html

# Opción 2: desde terminal
xdg-open guion-tecnico.html        # Linux
open guion-tecnico.html             # macOS
start guion-tecnico.html            # Windows
```

---

## 📂 Estructura del proyecto

```
guion-tecnico/
├── guion-tecnico.html   # 🌐 Aplicación web (fichero único autocontenido)
├── templates/           # 📋 Plantillas originales
│   └── Gtécnico.xlsx    # 📊 Hoja de cálculo de referencia original
├── examples/            # 📁 Ejemplos de prueba
│   └── ejemplo-guion-tecnico.json # 📄 Datos de ejemplo importables
├── README.md            # 📖 Este archivo
├── AGENTS.md            # 🤖 Instrucciones para agentes IA
├── LICENSE              # ⚖️ Licencia Creative Commons CC BY-SA 4.0
└── .gitignore           # 🚫 Archivos excluidos del repositorio
```

---

## 🛠️ Stack Tecnológico

### Lenguajes

| Tecnología | Estándar / Nivel | Uso |
|---|---|---|
| **HTML5** | Living Standard | Estructura y formularios semánticos (`<table>`, `<select>`, `<textarea>`, `<input>`) |
| **CSS** | Modern CSS (Snapshot / Level 4+) | Diseño visual, variables nativas, layout Grid/Flex, tema oscuro y reglas de impresión |
| **JavaScript** | ES6+ (Vanilla) | Lógica de negocio reactiva, manipulación del DOM y persistencia |

### APIs del navegador

| API | Uso |
|---|---|
| **localStorage** | Persistencia de datos entre sesiones |
| **Blob / URL.createObjectURL** | Exportación de archivos JSON |
| **FileReader** | Importación de archivos JSON |
| **@media print** | Hoja de estilos específica para impresión en A4 |

### Técnicas de Modern CSS destacadas

- **Custom Properties (CSS Variables Level 2)** — Sistema de diseño con variables semánticas (`--bg`, `--accent`, `--border`) para cambios de estilo inmediatos.
- **CSS Grid & Flexbox (Level 2)** — Maquetación elástica del formulario superior, barra de herramientas y métricas.
- **Funciones matemáticas (Values & Units Level 4)** — Uso de `min(680px, 90vw)` y `calc()` para dimensionado fluido de cajones laterales sin scripts.
- **`position: sticky` (Positioning Level 3)** — Cabeceras de tabla fijas al desplazarse verticalmente sobre listas extensas de planos.
- **Estilos de impresión avanzados (`@media print`)** — Reconfiguración completa del layout para generar un documento limpio en A4 apaisado eliminando elementos de interfaz.
- **Pseudo-elementos y selectores de atributos** — Etiquetas de número de secuencia (`tr[data-seq]`) y decoradores cinemáticos con `::before`.

### Técnicas JavaScript destacadas

- **Event Delegation** — Un solo listener en el `<tbody>` para todas las celdas editables
- **Debounced Auto-save** — Guardado automático con retardo de 800ms para evitar escrituras excesivas
- **Template Literals** — Generación dinámica de HTML
- **Desestructuración y operadores spread** — Gestión limpia del estado

### Decisiones de arquitectura

| Decisión | Justificación |
|---|---|
| **Fichero único** | Máxima portabilidad: se comparte por email, USB o hosting estático |
| **Sin frameworks** | Sin curva de aprendizaje, sin build, sin node_modules |
| **Sin backend** | No requiere servidor, hosting ni base de datos |
| **Vanilla JS** | Rendimiento óptimo, sin dependencias que actualizar |
| **localStorage** | Persistencia sin autenticación ni configuración |

---

## 📋 Contenido audiovisual incluido

El formulario incluye las opciones de lenguaje audiovisual estándar:

<details>
<summary><strong>📷 Encuadres (7)</strong></summary>

| Encuadre | Abreviatura |
|---|---|
| Plano Detalle | PD |
| Primer Plano | PP |
| Plano Medio | PM |
| Plano Americano | PA |
| Plano Completo | PC |
| Plano General | PG |
| Gran Plano General | GPG |

</details>

<details>
<summary><strong>📐 Angulaciones (5)</strong></summary>

A nivel · Picado · Contrapicado · Cenital · Nadiral

</details>

<details>
<summary><strong>🎥 Movimientos (6)</strong></summary>

Fijo · Travelin · Paneo · Tilt · Steady · Cámara lenta (Slow motion)

</details>

<details>
<summary><strong>✨ Efectos de vídeo (17)</strong></summary>

Blanco y negro · Sepia · Desaturación · Color grading · Corrección de color · Grano de película · Glitch digital · Viñeteado · Cámara lenta · Cámara rápida · Estabilización / Inestabilidad · Desenfoque (Blur) · Lens flare · Deformaciones · Chroma key · Doble exposición · Enfoque selectivo

</details>

<details>
<summary><strong>🔀 Transiciones (9)</strong></summary>

Corte (Cut) · Fundido a negro · Fundido desde negro · Fundido encadenado (Dissolve) · Cortinilla (Wipe) · Corte Igualado (Match cut) · Corte Brusco (Jump Cut) · Iris cierra (Iris in) · Iris abre (Iris out)

</details>

---

## 🤝 Contribuir

1. Haz un fork del repositorio
2. Crea una rama con tu funcionalidad: `git checkout -b feature/nueva-funcionalidad`
3. Haz commit de tus cambios: `git commit -m 'feat: añadir nueva funcionalidad'`
4. Sube la rama: `git push origin feature/nueva-funcionalidad`
5. Abre un Pull Request

### Ideas de mejora

- [ ] Exportar a PDF directamente
- [ ] Modo claro / oscuro configurable
- [ ] Arrastrar y soltar para reordenar planos
- [ ] Importar datos directamente desde ficheros `.xlsx`
- [ ] Vista previa de storyboard con imágenes
- [ ] Soporte multiidioma (EN, FR, CA)
- [ ] PWA con Service Worker para instalación

---

## 👤 Autoría

Creado por **Daniel Losada**
- 🆔 **ORCID**: [0000-0003-3842-7694](https://orcid.org/0000-0003-3842-7694)
- 🐙 **GitHub**: [@danloi2 / guion-tecnico](https://github.com/danloi2/guion-tecnico)

---

## ⚖️ Licencia

Este proyecto se distribuye bajo la licencia **[Creative Commons Reconocimiento-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)](https://creativecommons.org/licenses/by-sa/4.0/deed.es)**.

Eres libre de compartir y adaptar el material, siempre que reconozcas la autoría original y mantengas la misma licencia. Consulta el archivo [LICENSE](LICENSE) para más detalles.

---

<div align="center">

Hecho con ❤️ para la educación audiovisual · **Daniel Losada**

**🎬 ¡Luces, cámara, guión técnico!**

</div>
