# Buscador de Ubicaciones de Almacén

Este es un sistema de búsqueda simple basado en HTML, CSS y JavaScript para localizar ítems dentro de un almacén. Permite buscar por diferentes atributos del producto y visualizar los resultados de forma paginada. Además, incluye una función de escáner de código de barras (utilizando la librería ZXing-JS) para facilitar la búsqueda, y un gestor de correcciones/observaciones pendientes.

## Características

* **Búsqueda Rápida:** Filtra los datos del almacén por ubicación, material, unidad, lote o cualquier texto contenido en la descripción.
* **Paginación de Resultados:** Muestra los resultados en páginas para una navegación eficiente, especialmente con grandes volúmenes de datos.
* **Escáner de Código de Barras:** Integración con la cámara del dispositivo para escanear códigos de barras (EAN-13, CODE-128, CODE-39, UPC-A, EAN-8, CODABAR) y rellenar automáticamente el campo de búsqueda con los últimos 18 caracteres del código escaneado.
* **Gestión de Correcciones/Observaciones:** Una sección dedicada para listar y gestionar correcciones o tareas pendientes en el almacén, con la capacidad de marcar elementos como completados (estado persistente usando `localStorage`).
* **Diseño Responsivo:** Interfaz adaptable a diferentes tamaños de pantalla (escritorio y móvil).

## Archivos del Proyecto

* `index.html`: El archivo principal de la aplicación que contiene la estructura HTML, estilos CSS y lógica JavaScript.
* `almacen_data.txt`: Archivo de texto que contiene los datos del almacén. Cada línea representa un registro y los campos están separados por tabulaciones (`\t`).
* `correcciones.txt`: Archivo de texto que contiene las correcciones o tareas pendientes. Cada línea representa una corrección, con la ubicación y la observación separadas por un punto y coma (`;`).

## Estructura de `almacen_data.txt`

El archivo `almacen_data.txt` debe tener el siguiente formato, con los campos separados por una tabulación (`\t`):

Ubicación\tMaterial\tUnidad\tLote\tTextoAdicional
Ej: 1101-01    378    CAJA    LOTE123    Descripción del Material X
Ej: A101-02    ABC-456    UNIDAD    LOTE456    Pieza de repuesto Y


**Es crucial que cada campo esté separado por un carácter de tabulación `\t` para que la aplicación pueda parsear los datos correctamente.**

## Estructura de `correcciones.txt`

El archivo `correcciones.txt` debe tener el siguiente formato, con los campos separados por un punto y coma (`;`):

Ubicación;Observación/Tarea
Ej: 1101-01;Revisar stock de material ABC
Ej: B205;Ajustar ubicación de herramientas


## Requisitos

* Un navegador web moderno (Chrome, Firefox, Edge, Safari).
* Para cargar los archivos `almacen_data.txt` y `correcciones.txt` correctamente, es recomendable servir la aplicación a través de un **servidor web local**. Abrir `index.html` directamente desde el sistema de archivos puede causar problemas de seguridad de CORS (Cross-Origin Resource Sharing) en algunos navegadores, impidiendo que los archivos `.txt` se carguen.

## Cómo Ejecutar

1.  **Clonar o Descargar:** Descarga o clona este repositorio en tu máquina local.
2.  **Crear Archivos de Datos:** Asegúrate de que `almacen_data.txt` y `correcciones.txt` existan en la misma carpeta que `index.html` y que contengan los datos en el formato especificado.
3.  **Servidor Web Local (Recomendado):**
    * **Python:** Si tienes Python instalado, puedes iniciar un servidor web simple navegando a la carpeta del proyecto en tu terminal y ejecutando:
        ```bash
        python -m http.server 8000
        ```
        Luego, abre tu navegador y ve a `http://localhost:8000`.
    * **Node.js (con `http-server`):** Si tienes Node.js, puedes instalar `http-server` globalmente:
        ```bash
        npm install -g http-server
        ```
        Luego, navega a la carpeta del proyecto y ejecuta:
        ```bash
        http-server
        ```
        Abre tu navegador y ve a la dirección que te indique el terminal (generalmente `http://127.0.0.1:8080`).
    * **Otros:** Puedes usar cualquier otro software de servidor web (Apache, Nginx, XAMPP, WAMP, MAMP) para servir la carpeta.
4.  **Acceder:** Abre `index.html` en tu navegador a través de la URL del servidor local.

## Uso

1.  **Búsqueda:** Escribe tu término de búsqueda en el campo de entrada. Los resultados se actualizarán automáticamente a medida que escribes.
2.  **Paginación:** Utiliza los botones "Anterior" y "Siguiente" para navegar por los resultados de la búsqueda.
3.  **Escáner de Código de Barras:** Haz clic en el botón "Escanear" para abrir el modal del escáner. Asegúrate de conceder permisos de cámara a tu navegador. Centra el código de barras en el área de escaneo. Una vez detectado, el valor (últimos 18 caracteres) se ingresará en el campo de búsqueda.
4.  **Ver Correcciones:** Haz clic en el botón "Ver Correcciones" para abrir el modal de tareas pendientes. Puedes marcar las correcciones como completadas usando las casillas de verificación. El estado de estas casillas se guarda automáticamente en el almacenamiento local de tu navegador.

## Notas Técnicas

* La librería `ZXing-JS` se carga desde un CDN para la funcionalidad de escaneo.
* El estado de las correcciones marcadas se persiste en el `localStorage` del navegador, lo que significa que tus marcas se mantendrán incluso si cierras y vuelves a abrir la aplicación.
* La aplicación es completamente del lado del cliente, no requiere una base de datos ni un backend complejo. Los datos se cargan desde archivos de texto simples.

## Solución de Problemas Comunes

* **"Error al cargar los datos: Error HTTP..."**: Asegúrate de que `almacen_data.txt` y `correcciones.txt` están en la misma carpeta que `index.html` y que estás sirviendo la aplicación a través de un servidor web local.
* **"Acceso a la cámara denegado" / "Cámara no encontrada"**:
    * Asegúrate de haber concedido permisos a tu navegador para usar la cámara.
    * Verifica que ninguna otra aplicación esté usando la cámara en ese momento.
    * Confirma que tu dispositivo tiene una cámara funcional.
* **La búsqueda no funciona o los datos no aparecen**: Revisa el archivo `almacen_data.txt` para asegurarte de que los campos están correctamente separados por **tabulaciones (`\t`)** y no por espacios o comas.
* **Las correcciones no cargan**: Revisa el archivo `correcciones.txt` para asegurarte de que los campos están correctamente separados por **puntos y comas (`;`)**.

---

**Autor:** [Luis David Espinoza @perreohipertenso]


**USO LIBRE**
