# Buscador de Ubicaciones de Almacén

Este proyecto es una aplicación web sencilla para buscar y encontrar ubicaciones de almacén, materiales, lotes y unidades basándose en datos cargados desde un archivo de texto. Incluye una funcionalidad de escáner de código de barras para facilitar la búsqueda.

## Características

* **Búsqueda en Tiempo Real:** Filtra instantáneamente los resultados a medida que escribes en el campo de búsqueda.
* **Paginación de Resultados:** Muestra los resultados en páginas para una mejor legibilidad y manejo de grandes volúmenes de datos.
* **Escáner de Código de Barras:** Permite escanear códigos de barras (EAN-13, CODE-128, CODE-39, UPC-A, EAN-8, CODABAR) usando la cámara del dispositivo para rellenar automáticamente el campo de búsqueda.
* **Limpieza de Búsqueda:** Botón para limpiar rápidamente el campo de búsqueda.
* **Carga de Datos Flexible:** Carga los datos de almacén desde un archivo `almacen_data.txt` local, permitiendo una fácil actualización de la información.
* **Diseño Responsivo:** Adaptado para funcionar tanto en dispositivos de escritorio como móviles.

## Cómo Usar

### 1. Preparación de los Datos

La aplicación espera encontrar un archivo llamado `almacen_data.txt` en el mismo directorio que el archivo `index.html`. Este archivo debe contener los datos del almacén en un formato separado por tabulaciones (`\t`), con la siguiente estructura por línea:
Ubicación\tMaterial\tUnidad\tLote\tTexto
**Ejemplo de `almacen_data.txt`:**
A101-01	MaterialXYZ	UN456	Lote123	Descripción del material XYZ en ubicación A101
B202-05	TornillosM8	KG789	Lote456	Caja de tornillos M8
C303-10	PinturaBlanca	LT101	Lote789	Pintura acrílica blanca para exteriores
Asegúrate de que tus datos sigan este formato para que la aplicación los lea correctamente.

### 2. Abrir la Aplicación

Debido a las restricciones de seguridad de los navegadores (CORS), **no puedes simplemente abrir el archivo `Untitled-2 (1).html` directamente desde tu sistema de archivos** (`file://`). La funcionalidad de cargar `almacen_data.txt` y, especialmente, el escáner de código de barras (que accede a la cámara), requiere un servidor web.

**Opciones para Ejecutar:**

* **Opción 1: Usar una extensión de servidor local (Recomendado para desarrollo)**
    Si usas Visual Studio Code, puedes instalar la extensión "Live Server". Haz clic derecho en `Untitled-2 (1).html` y selecciona "Open with Live Server". Esto abrirá el archivo en tu navegador a través de un servidor local (ej. `http://127.0.0.1:5500/Untitled-2%20(1).html`).

* **Opción 2: Usar un servidor HTTP simple (Python)**
    Si tienes Python instalado, puedes navegar a la carpeta donde guardaste `Untitled-2 (1).html` y `almacen_data.txt` en tu terminal, y ejecutar:
    ```bash
    python -m http.server 8000
    ```
    Luego, abre tu navegador y ve a `http://localhost:8000/Untitled-2%20(1).html`.

* **Opción 3: Desplegar en un servidor web real**
    Para uso en producción o compartido, sube todos los archivos (`Untitled-2 (1).html`, `almacen_data.txt`, etc.) a un servidor web (Apache, Nginx, GitHub Pages, Netlify, Vercel, etc.).

### 3. Interfaz de Usuario

* **Campo de Búsqueda:** Ingresa cualquier parte de la ubicación, material, unidad, lote o texto para filtrar los resultados.
* **Botón "Escanear":** Haz clic para abrir el modal del escáner de código de barras. Una vez que un código es escaneado, los últimos 18 caracteres del código serán ingresados automáticamente en el campo de búsqueda.
* **Botón "Limpiar Búsqueda" (`x`):** Aparece cuando hay texto en el campo de búsqueda y permite borrarlo rápidamente.
* **Resultados:** Los elementos coincidentes se mostrarán debajo del campo de búsqueda. Cada resultado muestra la Ubicación, Material, Lote, Unidad y Texto completo.
* **Paginación:** Utiliza los botones "Anterior" y "Siguiente" para navegar entre las páginas de resultados.

## Tecnología Utilizada

* **HTML5:** Estructura de la página.
* **CSS3:** Estilos para la interfaz de usuario.
* **JavaScript (ES6+):** Lógica de búsqueda, paginación y manejo del escáner.
* **ZXing-JS:** Librería JavaScript para el escaneo de códigos de barras. (CDN utilizado: `https://cdn.jsdelivr.net/npm/@zxing/library@0.19.1/umd/index.min.js`)
* **SVG Icons:** Icono de código de barras integrado directamente en el HTML.

## Requisitos

* Un navegador web moderno que soporte `navigator.mediaDevices` para la API de la cámara (para la función de escáner).
* Acceso a la cámara del dispositivo (se pedirá permiso al activar el escáner).

## Notas de Desarrollo

* El archivo HTML se nombró `Untitled-2.html`. Considera renombrarlo a `index.html` para una mayor convención en proyectos web.
* El campo `lote` y `unidad` en los resultados están mapeados a `item.unit` y `item.lote` respectivamente, lo que podría generar confusión. Revisa la lógica en el JavaScript si quieres que el campo "Lote" muestre `item.lote` y "Unidad" muestre `item.unit` o viceversa. Actualmente, el código asigna `item.unit` a "Lote" y `item.lote` a "Unidad" en la visualización, mientras que los datos se leen como `parts[2]` para `unit` y `parts[3]` para `lote`.
* La lógica de extracción de los últimos 18 caracteres del código de barras escaneado (`scannedText.slice(-18)`) está implementada. Si tus códigos de barras tienen otra longitud o formato, necesitarás ajustar esta línea.

---

**Autor:** [Luis David Espinoza @perreohipertenso]


**USO LIBRE**
