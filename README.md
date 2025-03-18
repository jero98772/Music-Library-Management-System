# Music Library Management System

A Clojure web application for managing musical scores (partitures) using Redis for storage. Provides RESTful API endpoints and a simple frontend interface.

## Description

**For Artists & Music Guardians:**
Imagine a place where your music leaps off the page and comes alive instantly—no downloads, no clunky software. This is a digital sanctuary for your scores, built to let your work shine right in the browser. Whether you’re jotting down a midnight melody on crumpled paper, resurrecting a forgotten classical piece, or experimenting with electronic beats, your compositions aren’t just stored—they’re experienced. Say goodbye to static PDFs and unreadable files; here, your partitures render beautifully on any device, anytime, so collaborators can see, play, and feel your vision without friction. No more lost manuscripts or format wars—just your art, breathing freely online, reaching ears and hearts faster than ever.


**Why Open Source? Because Music Belongs to Everyone.**  
This project isn’t locked behind corporate gates or paywalls—it’s built by and for the people who live and breathe music. Open source means every line of code is a shared hymn, a collective effort to protect and celebrate creativity. Like a jam session where anyone can grab an instrument, developers, musicians, and dreamers worldwide can tweak, improve, and reshape this tool. Want a feature that helps transcribe handwritten scores? Add it. Dream of a way to tag compositions by mood or cultural roots? Build it. Transparency isn’t just a buzzword here—it’s a promise. No hidden agendas, just a community stitching technology and passion into something that outlives us all. Together, we’re not just archiving notes; we’re safeguarding the stories, struggles, and sparks that make music humanity’s universal language. Join us, and turn the act of preservation into an act of love.


## Translations in:

<center>
[Spanish](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_es.md)
[Deutsch](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_ge.md) 
[Русский](https://github.com/jero98772/Music-Library-Management-System/blob/main/docs/readme_ru.md)
</center>

## Features

- **CRUD Operations**: Create, Read, Update, Delete musical scores
- **Redis Storage**: Persistent data storage using Redis
- **EDN Serialization**: Store complex Clojure data structures
- **REST API**: JSON-based API for programmatic access
- **Web Interface**: Basic HTML pages for manual interactions


## Technologies

- **Clojure** (1.10+)
- **Ring/Compojure** (Web framework)
- **Carmine** (Redis client)
- **Redis** (5.0+)
- **Leiningen** (Build tool)

## Prerequisites

- Java JDK 8+
- Leiningen 2.9.8+
- Redis Server 5.0+

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/music-lib.git
   cd music-lib/src
   ```

2. Install dependencies:
   ```bash
   lein deps
   ```

3. Start Redis server:
   ```bash
   redis-server
   ```

4. Run the application:
   ```bash
   lein ring server
   ```

The application will be available at `http://localhost:3000`


## Screenshots

![]()

## API Documentation

### Get All Partitures
```
GET /api/partiture
```
**Response:**
```json
{
  "count": 2,
  "partitureList": [
    {
      "id": "partiture:uuid1",
      "title": "Moonlight Sonata",
      "composer": "Beethoven",
      "created-at": "2023-09-20"
    }
  ]
}
```

### Create New Partiture
```
POST /api/partiture
```
**Parameters:**
- `title` (required)
- `composer` (required)
- `opus` (optional)
- `key` (optional)

**Example Response:**
```json
{
  "id": "partiture:550e8400-e29b-41d4-a716-446655440000"
}
```

### Get Single Partiture
```
GET /api/partiture/:id
```
**Response:**
```json
{
  "id": "partiture:uuid1",
  "title": "Moonlight Sonata",
  "composer": "Beethoven",
  "opus": "27/2",
  "key": "C# minor",
  "created-at": "2023-09-20"
}
```

### Update Partiture
```
PUT /api/partiture/:id
```
**Parameters:** Same as POST

### Delete Partiture
```
DELETE /api/partiture/:id
```

## Frontend Routes

- `/` - Main listing page
- `/add-partiture` - Add new score form
- `/partiture/:id` - Score detail view
- `/edit/:id` - Edit existing score
- `/delete/:id` - Delete confirmation

## Project Structure

```
├── src
│   └── music_lib
│       ├── core.clj    # Main application routes
│       └── db.clj      # Redis database operations
├── resources
│   └── public          # Static assets
│       ├── index.html
│       ├── add-partiture.html
│       └── ...other HTML files
├── project.clj         # Leiningen configuration
└── README.md
```

## Configuration

Redis connection settings (in `db.clj`):
```clojure
(def server-conn {
  :spec {
    :host "127.0.0.1"
    :port 6379
    :password nil
    :timeout-ms 3000}})
```

## Testing the API

Example using curl:
```bash
# Create new partiture
curl -X POST -d "title=Für Elise&composer=Beethoven" http://localhost:3000/api/partiture

# Get all partitures
curl http://localhost:3000/api/partiture

# Update partiture
curl -X PUT -d "opus=WoO59" http://localhost:3000/api/partiture/partiture:uuid1
```

## Error Handling

The API returns appropriate HTTP status codes:
- 200 OK
- 201 Created
- 404 Not Found
- 500 Internal Server Error

Errors include JSON responses with error details:
```json
{
  "error": "Partiture not found"
}
```

## Potential Improvements

1. Add authentication/authorization
2. Implement data validation
3. Add search functionality
4. Add pagination for large datasets
5. Implement proper error messages for frontend
6. Add test coverage
7. Containerize with Docker
8. Add Swagger/OpenAPI documentation

## Troubleshooting

Common Issues:
1. **Redis Connection Failed**
   - Ensure Redis server is running
   - Verify connection details in `db.clj`

2. **EDN Parsing Errors**
   - Check data format in Redis using `redis-cli`
   - Verify stored values are proper EDN

3. **Missing Dependencies**
   - Run `lein deps` to ensure all dependencies are fetched

## License

GPLv3 License , that mean you can use this project for any purpose, but you must put a reference for [https://github.com/jero98772/Music-Library-Management-System](https://github.com/jero98772/Music-Library-Management-System).

## Credits

Created using:
- [Compojure](https://github.com/weavejester/compojure)
- [Carmine](https://github.com/ptaoussanis/carmine)
- [Ring](https://github.com/ring-clojure/ring)