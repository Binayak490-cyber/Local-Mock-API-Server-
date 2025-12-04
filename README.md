# 🎮 Game Store Mock API Server

A flexible, feature-rich mock API server with a beautiful web interface for testing and development. Perfect for frontend development, API design, and learning REST principles.

## Features

- **12 Working Endpoints** - Complete game store API
- **Beautiful Dark Theme UI** - Professional developer-friendly interface  
- **Real Wishlist Storage** - Actual add/remove functionality that persists
- **Auto-generated Forms** - Parameter inputs for each endpoint
- **Real-time Monitoring** - Server health and request logging
- **Hot Reload** - Update config without restart
- **Template Engine** - Dynamic responses with query params
- **CORS Support** - Ready for frontend integration

## Quick Start

```bash
# Install dependencies
pip install -r requirements.txt

# Start the server
python main.py

# Open the web interface
# Navigate to http://localhost:8000
```

That's it! The beautiful web interface will open automatically.

## API Endpoints

### Games API (6 endpoints)
- `GET /api/games` - All games from database
- `GET /api/games/new-releases` - Filter new releases
- `GET /api/games/highest-rated` - Top rated games
- `GET /api/games/discounts` - Games with discounts
- `GET /api/games/search?title=X` - Search by title
- `GET /api/games/genre?genre=X` - Filter by genre

### Actions (2 endpoints)
- `POST /api/games/review?title=X&review=X` - Submit review
- `POST /api/games/wishlist?title=X` - Add to wishlist

### Wishlist Management (3 endpoints) 
- `GET /api/games/wishlist` - View all wishlist items
- `POST /api/games/wishlist?title=X` - Add game to wishlist
- `DELETE /api/games/wishlist?title=X` - Remove from wishlist

**Note:** Wishlist has REAL storage - changes persist during the session!

### System (3 endpoints)
- `GET /api/health` - Server health check
- `GET /__logs` - View request history
- `POST /__reload` - Hot-reload configuration

## Web Interface

The web interface provides:
- **Endpoint Browser** - All 12 endpoints with descriptions
- **Parameter Forms** - Auto-generated inputs for each endpoint
- **Response Viewer** - Formatted JSON with timing info
- **Status Monitor** - Real-time server health
- **Dark Theme** - Easy on the eyes

## Example Usage

### Using the Web Interface
1. Open http://localhost:8000
2. Click any endpoint (e.g., "All Games")
3. Fill in parameters if needed
4. Click "Send Request"
5. View the formatted response

### Using curl
```bash
# Get all games
curl http://localhost:8000/api/games

# Search for a game
curl "http://localhost:8000/api/games/search?title=Minecraft"

# Add to wishlist
curl -X POST "http://localhost:8000/api/games/wishlist?title=Fortnite"

# View wishlist
curl http://localhost:8000/api/games/wishlist

# Remove from wishlist
curl -X DELETE "http://localhost:8000/api/games/wishlist?title=Fortnite"

# Submit a review
curl -X POST "http://localhost:8000/api/games/review?title=Minecraft&review=Great+game"
```

## Configuration

The server is configured via `config/config.json`. Each endpoint can specify:

```json
{
  "path": "/api/games",
  "method": "GET",
  "response": {
    "games": "{{database}}",
    "count": "{{database_count}}"
  },
  "status": 200,
  "latency_ms": 100,
  "failure_rate": 0.0
}
```

### Template Variables
- `{{timestamp}}` - Current ISO timestamp
- `{{query.param_name}}` - Query parameter value
- `{{random_int}}` - Random integer (1-100)
- `{{random_price}}` - Random price ($20-$80)
- `{{uuid}}` - Random UUID
- `{{database}}` - Entire database
- `{{database_count}}` - Database record count
- `{{database_filter:field:value}}` - Filter database by field
- `{{database_find:field:value}}` - Find single record

### Hot Reload
Update `config.json` and reload without restart:
```bash
curl -X POST http://localhost:8000/__reload
```

## Project Structure

```
project/
├── main.py                     # Entry point
├── server/
│   └── mock_server.py         # Core server logic
├── config/
│   ├── config.json            # API endpoint definitions
│   ├── config_schema.json     # JSON schema validation
│   └── databases/
│       └── GAMES.JSON         # Game data
├── public/
│   ├── index.html             # Web interface
│   ├── static/
│   │   ├── styles.css         # Dark theme styles
│   │   └── app.js             # Frontend logic
│   └── README.md              # Frontend documentation
├── docs/                       # Additional documentation
├── examples/                   # Example requests
├── logs/                       # Request logs
└── requirements.txt            # Python dependencies
```

## Advanced Usage

### Custom Port
```bash
python main.py --port 8080
```

### Custom Config
```bash
python main.py --config config/custom_config.json
```

### View Logs
```bash
curl http://localhost:8000/__logs
```

### Simulate Latency
Edit `config.json` and set `latency_ms` for any endpoint:
```json
{
  "path": "/api/games",
  "latency_ms": 2000
}
```

### Simulate Failures
Set `failure_rate` (0.0 to 1.0) to randomly return errors:
```json
{
  "path": "/api/games",
  "failure_rate": 0.1
}
```

## Documentation

- [QUICKSTART.md](QUICKSTART.md) - 5-minute tutorial
- [docs/README.md](docs/README.md) - Detailed usage guide
- [docs/LEARNING.md](docs/LEARNING.md) - Learning guide & concepts
- [docs/API_REFERENCE.md](docs/API_REFERENCE.md) - Complete API reference
- [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) - System architecture
- [config/API_ENDPOINTS.md](config/API_ENDPOINTS.md) - Endpoint documentation
- [public/README.md](public/README.md) - Frontend documentation

## Use Cases

- **Frontend Development** - Test UI without a real backend
- **API Design** - Prototype and visualize API responses
- **Demos** - Show how APIs work without complex setup
- **Learning** - Understand REST principles and HTTP methods
- **Integration Testing** - Mock external services

## Testing

```bash
# Run integration tests
python server/test_server.py
```

## Limitations

- **Mock Server** - Most endpoints return predefined responses
- **Wishlist Only** - Only wishlist has real storage/modification
- **Single Session** - Data resets on server restart
- **No Authentication** - No auth/authorization layer
- **Exact Path Matching** - No wildcard routes

This is intentional - it's a mock server for testing, not a production database!

## Learning Goals

- Build HTTP servers with Python's `http.server`
- Understand REST API design patterns
- Simulate network conditions (latency, failures)
- Design ergonomic test doubles
- Document API contracts

## Contributing

Feel free to extend the configuration, add new endpoints, or enhance the frontend!

## License

MIT

---

**Ready to test your APIs? Start the server and open http://localhost:8000** 
