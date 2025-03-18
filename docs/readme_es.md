# Sistema de Gestión de Bibliotecas Musicales (traducción no verificada)

Una aplicación web en Clojure para gestionar partituras musicales usando Redis como almacenamiento. Ofrece endpoints RESTful API y una interfaz frontend sencilla.

## Traducciones disponibles:

<center>

[Русский](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_ru.md)

[Deutsch](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_ge.md) 

[English](https://github.com/jero98772/Music-Library-Management-System/blob/main/README.md)

</center>

## Descripción

**Para artistas y guardianes de la música:**  
Imagina un lugar donde tus partituras cobran vida al instante, sin descargas ni software engorroso. Este es un santuario digital para tus obras, diseñado para que tu trabajo brille directamente en el navegador. Ya sea que escribas una melodía nocturna en papel arrugado, rescates una pieza clásica olvidada o experimentes con ritmos electrónicos, tus composiciones no solo se almacenan: se experimentan. Di adiós a los PDF estáticos y archivos ilegibles; aquí, tus partituras se renderizan perfectamente en cualquier dispositivo, permitiendo que colaboradores vean, interpreten y sientan tu visión sin obstáculos. No más manuscritos perdidos ni guerras de formatos: solo tu arte, respirando libremente en línea, llegando a oídos y corazones más rápido que nunca.

**¿Por qué código abierto? Porque la música pertenece a todos.**  
Este proyecto no está tras puertas corporativas o muros de pago: está construido por y para quienes viven la música. "Código abierto" significa que cada línea es un himno compartido, un esfuerzo colectivo para proteger la creatividad. Como una jam session donde cualquiera puede tomar un instrumento, desarrolladores, músicos y soñadores pueden ajustar, mejorar y remodelar esta herramienta. ¿Quieres una función para transcribir partituras manuscritas? Añádela. ¿Sueñas con etiquetar obras por estado de ánimo o raíces culturales? Constrúyelo. La transparencia no es solo una palabra de moda: es una promesa. Sin agendas ocultas, solo una comunidad uniendo tecnología y pasión para crear algo que nos sobreviva. Juntos, no solo archivamos notas: preservamos historias, luchas y chispas que hacen de la música el lenguaje universal de la humanidad. Únete y convierte la preservación en un acto de amor.

## Características

- **Operaciones CRUD**: Crear, Leer, Actualizar, Eliminar partituras
- **Almacenamiento en Redis**: Persistencia de datos usando Redis
- **Serialización EDN**: Almacena estructuras complejas de Clojure
- **REST API**: API basada en JSON para acceso programático
- **Interfaz Web**: Páginas HTML básicas para interacción manual

## Tecnologías

- **Clojure** (1.10+)
- **Ring/Compojure** (Framework web)
- **Carmine** (Cliente Redis)
- **Redis** (5.0+)
- **Leiningen** (Herramienta de construcción)

## Requisitos

- Java JDK 8+
- Leiningen 2.9.8+
- Servidor Redis 5.0+

## Instalación

1. Clona el repositorio:
   ```bash
   git clone https://github.com/yourusername/music-lib.git
   cd music-lib/src
   ```

2. Instala dependencias:
   ```bash
   lein deps
   ```

3. Inicia el servidor Redis:
   ```bash
   redis-server
   ```

4. Ejecuta la aplicación:
   ```bash
   lein ring server
   ```

La aplicación estará disponible en `http://localhost:3000`

## Capturas de pantalla

![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/2.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/3.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/4.png)
![](https://raw.githubusercontent.com/jero98772/Music-Library-Management-System/refs/heads/main/docs/5.png)

## Documentación de la API

### Obtener todas las partituras
```
GET /api/partiture
```
**Respuesta:**
```json
{
  "count": 2,
  "partitureList": [
    {
      "id": "partiture:uuid1",
      "title": "Claro de Luna",
      "composer": "Beethoven",
      "created-at": "2023-09-20"
    }
  ]
}
```

### Crear nueva partitura
```
POST /api/partiture
```
**Parámetros:**
- `title` (requerido)
- `composer` (requerido)
- `opus` (opcional)
- `key` (opcional)

**Ejemplo de respuesta:**
```json
{
  "id": "partiture:550e8400-e29b-41d4-a716-446655440000"
}
```

### Obtener una partitura
```
GET /api/partiture/:id
```
**Respuesta:**
```json
{
  "id": "partiture:uuid1",
  "title": "Claro de Luna",
  "composer": "Beethoven",
  "instrumenr": "piano",
  "abc": "
X:3
T:Simple Song
M:4/4
L:1/8
K:C
[C]C2 [F]F2 [G]G2 [C]C2 |
w: This is a sim-ple song, sing a-long with me.

  ",
}
```

### Actualizar partitura
```
PUT /api/partiture/:id
```
**Parámetros:** Igual que POST

### Eliminar partitura
```
DELETE /api/partiture/:id
```

## Rutas del Frontend

- `/` - Página principal
- `/add-partiture` - Formulario de nueva partitura
- `/partiture/:id` - Vista detallada
- `/edit/:id` - Editar partitura
- `/delete/:id` - Confirmar eliminación

## Estructura del Proyecto

```
├── src
│   └── music_lib
│       ├── core.clj    # Rutas principales
│       └── db.clj      # Operaciones con Redis
├── resources
│   └── public          # Archivos estáticos
│       ├── index.html
│       ├── add-partiture.html
│       └── ...otros HTML
├── project.clj         # Configuración de Leiningen
└── README.md
```

## Configuración

Configuración de Redis (en `db.clj`):
```clojure
(def server-conn {
  :spec {
    :host "127.0.0.1"
    :port 6379
    :password nil
    :timeout-ms 3000}})
```

## Probando la API

Ejemplos con curl:
```bash
# Crear partitura
curl -X POST -d "title=Para Elisa&composer=Beethoven" http://localhost:3000/api/partiture

# Obtener todas
curl http://localhost:3000/api/partiture

# Actualizar
curl -X PUT -d "opus=WoO59" http://localhost:3000/api/partiture/partiture:uuid1
```

## Manejo de errores

La API devuelve códigos HTTP:
- 200 OK
- 201 Created
- 404 No encontrado
- 500 Error interno

Errores incluyen detalles en JSON:
```json
{
  "error": "Partitura no encontrada"
}
```

## Mejoras potenciales

1. Añadir autenticación/autorización
2. Validación de datos
3. Funcionalidad de búsqueda
4. Paginación para grandes conjuntos
5. Mejores mensajes de error en frontend
6. Pruebas automatizadas
7. Dockerización
8. Documentación Swagger/OpenAPI

## Solución de problemas

Problemas comunes:
1. **Error de conexión a Redis**
   - Verifica que Redis esté ejecutándose
   - Revisa la configuración en `db.clj`

2. **Errores de EDN**
   - Inspecciona datos con `redis-cli`
   - Asegura valores EDN válidos

3. **Dependencias faltantes**
   - Ejecuta `lein deps`

## Licencia

Licencia GPLv3. Puedes usar este proyecto libremente, pero debes incluir referencia a [https://github.com/jero98772/Music-Library-Management-System](https://github.com/jero98772/Music-Library-Management-System).

## Créditos

Creado con:
- [Compojure](https://github.com/weavejester/compojure)
- [Carmine](https://github.com/ptaoussanis/carmine)
- [Ring](https://github.com/ring-clojure/ring)