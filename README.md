# AREP_AplicacionesDistribuidas

-----------------------------------------------------------------------------------------
#### Realizado por: Nicolas Sebastian Achuri Macias 
---------------------------------------------------------------------------------------

1. De acuerdo a lo estipulado se deberia descargar el repositorio haciendo uso de

 ```
   git clone https://github.com/N1CKZ3B/AREP_AplicacionesDistribuidas
```
2. Se deberían correr los siguientes comandos para hacer funcionar el archivo principal

   ```
   javac -d build src/SimpleWebServer.java
   java -cp build SimpleWebServer
   ```

3. Se ingresa al localhost por el puerto 8080 y se puede hacer uso del servidor web completamente funcional

   ![image](https://github.com/user-attachments/assets/7ac236cc-dafb-4239-b8ca-3148ab02b3c8)

----------------------------------------------------------------------------------------------

<div align="justify">
El servidor se inicia mediante la clase principal SimpleWebServer, que configura un ServerSocket en el puerto especificado (como el 8080). Este socket escucha continuamente las conexiones entrantes. Para manejar estas conexiones de manera efectiva y sin bloquear el servidor, se utiliza un ExecutorService con un pool de hilos. Cada vez que llega una solicitud, el servidor acepta la conexión y delega el procesamiento a un nuevo hilo creado por el pool. Esto permite que el servidor maneje múltiples solicitudes al mismo tiempo sin que una solicitud bloquee a las demás.

Cuando el servidor acepta una conexión, se crea un objeto ClientHandler para gestionar la solicitud del cliente. Este objeto lee la solicitud HTTP del cliente a través del InputStream del socket. En el método run de ClientHandler, se analiza la solicitud para determinar el método HTTP (como GET o POST) y la ruta solicitada.

Para una solicitud GET, el servidor primero verifica si la ruta solicitada corresponde a un recurso estático, como un archivo HTML, CSS, JavaScript o una imagen. Si la ruta es /, el servidor redirige la solicitud a index.html como la página principal. Si la ruta es /api/services, el servidor responde con datos en formato JSON sobre los servicios ofrecidos. Para otras rutas, el servidor intenta servir el archivo correspondiente desde la carpeta raíz de documentos (WEB_ROOT).

En caso de que el archivo solicitado no exista, el servidor responde con un error 404. La respuesta al cliente se envía a través del OutputStream del socket. El servidor utiliza el método sendResponse para enviar el estado HTTP, el tipo de contenido y el cuerpo de la respuesta. Si se solicita un archivo estático, el servidor lee el contenido del archivo y lo envía al cliente. Si se trata de una solicitud REST, el servidor genera una respuesta en formato JSON.

</div>

