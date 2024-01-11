# Introducción

## ¿Qué es Nginx?

Nginx, pronunciado como “engine-ex”, es un servidor web de código abierto que, desde su éxito inicial como servidor web, ahora también es usado como proxy inverso, cache de HTTP, y balanceador de carga.

Nginx creado originalmente por Igor Sysoev, y tuvo su primer lanzamiento público en octubre de 2004. Igor concibió inicialmente el software como una respuesta al problema C10K, que se refiere al problema de rendimiento de manejar 10,000 conexiones concurrentes.

## ¿Cómo Funciona?

Nginx está diseñado para ofrecer un bajo uso de memoria y alta concurrencia. En lugar de crear nuevos procesos para cada solicitud web, Nginx usa un enfoque asincrónico basado en eventos donde las solicitudes se manejan en un solo hilo.

Con Nginx, un proceso maestro puede controlar múltiples procesos de trabajo. El proceso maestro mantiene los procesos de trabajo, y son estos lo que hacen el procesamiento real.

Algunas características comunes que se ven en Nginx incluyen:

- Proxy inverso con caché
- IPv6
- Balanceo de carga
- Soporte FastCGI con almacenamiento en caché
- Websockets
- Manejo de archivos estáticos, archivos de índice y auto indexación
- TLS / SSL con SNI

![image](/img/images.png)