# 🤖 AGENTS.md — Instrucciones para Agentes IA

## Contexto del proyecto

Este es un proyecto de **fichero único HTML** (Single Page Application autocontenida) para crear guiones técnicos audiovisuales en el ámbito educativo. Todo el código (HTML, CSS, JavaScript) está en un solo archivo: `guion-tecnico.html`.

## Arquitectura

```
guion-tecnico.html    ← ÚNICO fichero de código
├── <style>           ← CSS completo (reset, layout, componentes, print, responsive)
├── <body>            ← HTML semántico (header, toolbar, tabla, drawer, modals)
└── <script>          ← JavaScript vanilla ES6+ (estado, renderizado, persistencia)
```

### Principios de diseño

1. **Zero dependencias**: No hay frameworks, librerías externas, CDN ni imports. Todo es vanilla HTML/CSS/JS.
2. **Fichero único**: Todo el código debe permanecer dentro de `guion-tecnico.html`. No separar en ficheros CSS o JS salvo que el usuario lo pida explícitamente.
3. **Offline-first**: No hacer llamadas de red. No añadir CDNs, Google Fonts ni recursos externos.
4. **Portabilidad**: El fichero debe poder abrirse con doble clic en cualquier navegador moderno sin servidor.

### Estructura del JavaScript

| Sección | Responsabilidad |
|---|---|
| `OPTIONS` | Datos de validación para los desplegables (encuadre, angulación, movimiento, efecto, transición) |
| `REF_DATA` | Datos de referencia de lenguaje audiovisual para el panel lateral |
| `SEQ_COLORS` | Paleta de colores para diferenciar secuencias visualmente |
| `shots[]` | Array de objetos que representa el estado de todos los planos |
| Funciones de renderizado | `renderTable()`, `updateStats()`, `updateDurations()`, `updateSeqColors()` |
| Funciones de gestión | `addShot()`, `removeShot()`, `newShot()` |
| Persistencia | `save()`, `loadFromStorage()`, `exportJSON()`, `importJSON()` |
| UI | `toggleDrawer()`, `renderRefTab()`, `showToast()`, `confirmClear()` |

### Modelo de datos de un plano (shot)

```javascript
{
  secuencia: string,      // Nº de secuencia (1-300)
  plano: string,          // Nº de plano dentro de la secuencia (1-300)
  tiempo: string,         // Duración del plano en segundos
  descripcion: string,    // Descripción visual del plano
  encuadre: string,       // Tipo de plano (PD, PP, PM, PA, PC, PG, GPG)
  angulacion: string,     // Ángulo de cámara
  movimiento: string,     // Movimiento de cámara
  intertitulos: string,   // Texto en pantalla
  efecto: string,         // Efecto de vídeo durante el plano
  transicion: string,     // Transición al siguiente plano
  sonido: string,         // Descripción del sonido/música
  dialogo: string         // Texto de diálogos
}
```

### Persistencia

- **Auto-guardado**: Cada cambio en cualquier campo dispara un guardado con debounce de 800ms en `localStorage` bajo la clave `guion-tecnico-data`.
- **Exportación**: Serializa el estado completo a JSON y lo descarga como fichero.
- **Importación**: Lee un fichero JSON y restaura el estado completo.

## Directrices para modificaciones

### ✅ Hacer

- Mantener todo el código en un solo fichero HTML.
- Usar vanilla JavaScript (ES6+). No añadir frameworks ni librerías.
- Mantener la compatibilidad con navegadores modernos (Chrome, Firefox, Safari, Edge).
- Preservar los estilos de impresión (`@media print`) al modificar el layout.
- Usar las custom properties CSS (variables `--`) para colores y dimensiones.
- Mantener la delegación de eventos en `#shots-body` para los inputs de la tabla.
- Escapar HTML del usuario con `escapeHtml()` al insertar en el DOM.
- Probar que la función de impresión sigue funcionando tras cambios visuales.

### ❌ No hacer

- No separar el código en múltiples ficheros sin autorización explícita del usuario.
- No añadir dependencias externas (npm, CDN, Google Fonts, etc.).
- No usar `innerHTML` con datos del usuario sin escapar.
- No romper la estructura del objeto `shot` sin actualizar `newShot()`, `renderTable()` y la serialización JSON.
- No eliminar la funcionalidad `@media print` ni los atajos de teclado existentes.
- No cambiar la clave de `localStorage` (`guion-tecnico-data`) ya que los usuarios pueden tener datos guardados.

### Añadir una nueva columna al guión

1. Añadir el campo al objeto en `newShot()`.
2. Añadir la celda `<th>` en el HTML del `<thead>`.
3. Añadir la celda `<td>` en `renderTable()`.
4. Si es un desplegable, añadir las opciones en `OPTIONS`.
5. Si tiene datos de referencia, añadir la información en `REF_DATA`.
6. Ajustar los estilos de impresión si es necesario.

### Añadir una nueva opción a un desplegable existente

1. Añadir el valor al array correspondiente en `OPTIONS`.
2. Si procede, añadir la fila de referencia en `REF_DATA`.

## Convenciones de código

- **Idioma del código**: Variables y funciones en inglés. Comentarios y contenido de usuario en español.
- **Estilo CSS**: Usar BEM simplificado. Variables CSS con prefijo semántico (`--bg`, `--text`, `--accent`).
- **JavaScript**: `const` por defecto, `let` cuando sea necesario, nunca `var`. Funciones declarativas.
- **Commits**: Seguir Conventional Commits (`feat:`, `fix:`, `style:`, `docs:`, `refactor:`).

## Testing

Al no haber framework de testing, verificar manualmente:

1. **Abrir** el fichero en el navegador → debe mostrar el formulario vacío.
2. **Añadir plano** → debe aparecer una fila nueva con campos editables.
3. **Rellenar campos** → el auto-guardado debe activarse (toast "💾 Guardado automáticamente").
4. **Recargar página** → los datos deben persistir.
5. **Exportar JSON** → debe descargar un fichero `.json` válido.
6. **Importar JSON** → debe restaurar todos los datos.
7. **Imprimir** (`Ctrl+P`) → debe mostrar una tabla limpia en A4 apaisado sin botones ni controles.
8. **Vaciar todo** → debe pedir confirmación y borrar todos los datos.
9. **Panel de referencia** → debe abrirse/cerrarse y mostrar contenido en las 6 pestañas.
10. **Responsive** → verificar en viewport de 768px y menos.

## Ficheros del repositorio

| Fichero | Propósito | Editable |
|---|---|---|
| `guion-tecnico.html` | Aplicación web completa | ✅ Fichero principal |
| `templates/Gtécnico.xlsx` | Hoja de cálculo de referencia original | ⚠️ Solo referencia |
| `examples/ejemplo-guion-tecnico.json` | Datos de ejemplo importables extraídos del Excel | ✅ |
| `README.md` | Documentación del proyecto | ✅ |
| `AGENTS.md` | Este fichero — instrucciones para agentes IA | ✅ |
| `LICENSE` | Licencia Creative Commons CC BY-SA 4.0 | ✅ |
| `.gitignore` | Exclusiones del repositorio | ✅ |
