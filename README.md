# WEB-YAPE

Este repositorio contiene dos páginas web independientes que usan Firebase Realtime Database:

- **`index.html`**: aplicación principal para el control diario y el cierre semanal de caja. Lee los pagos Yape desde la ruta actual `yapes/{codigoDeCaja}/{fecha}` y mantiene compatibilidad con la ruta `pagos` usada por versiones anteriores de la aplicación Android.
- **`simulador.html`**: herramienta de prueba. Envía pagos de ejemplo a la misma ruta que consume la aplicación principal y permite comprobar la conexión y la sincronización en tiempo real.

## Uso local

1. Sirve la carpeta con un servidor HTTP, por ejemplo:

   ```bash
   python3 -m http.server 8080
   ```

2. Abre `http://localhost:8080/index.html` para usar la aplicación principal.
3. Abre `http://localhost:8080/simulador.html` en otra pestaña.
4. En ambas páginas usa el mismo identificador de caja y la misma fecha. Envía un pago desde el simulador y verifica que el total de Yape se actualice en la aplicación principal.

> La base de datos debe tener reglas de Firebase que permitan las lecturas y escrituras necesarias para el entorno de prueba.

## Compatibilidad con Android

Los registros de la ruta heredada `pagos` se filtran por la fecha seleccionada usando `fecha`, `timestamp` o `createdAt`. Si el registro incluye `codigoCaja`, `codigoUnico`, `tenant` o `codigo`, también se valida que coincida con el identificador conectado. Los registros antiguos que no incluyen esos campos continúan siendo visibles para no perder yapeos reales.
