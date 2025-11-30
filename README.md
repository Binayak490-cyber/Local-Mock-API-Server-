# Local API Mock Server

A configurable HTTP mock server for testing and development. Serve endpoints from JSON files with latency simulation, failure injection, and request logging.

## Features

-  Configure endpoints via JSON files
-  Simulate network latency
-  Inject failures for resilience testing
-  Request logging with timestamps
-  Hot-reload configuration without restart
-  CORS support
-  Template engine for dynamic responses (query params, timestamps)
-  Record and replay real traffic (stretch goal)

## Quick Start

```bash
# Start the server
python mock_server.py

# With custom config
python mock_server.py --config custom_config.json --port 8080
```

## Configuration

Create a `config.json` file:

```json
{
  "port": 8000,
  "cors": true,
  "endpoints": [
    {
      "path": "/api/users",
      "method": "GET",
      "response": {
        "users": [
          {"id": 1, "name": "Alice"},
          {"id": 2, "name": "Bob"}
        ],
        "timestamp": "{{timestamp}}"
      },
      "status": 200,
      "latency_ms": 100,
      "failure_rate": 0.0
    }
  ]
}
```

## Template Variables

- `{{timestamp}}` - Current ISO timestamp
- `{{query.param_name}}` - Query parameter value
- `{{random_int}}` - Random integer
- `{{uuid}}` - Random UUID

## API

### Reload Configuration
```bash
curl -X POST http://localhost:8000/__reload
```

### View Request Log
```bash
curl http://localhost:8000/__logs
```

## Learning Goals

- Build HTTP servers with Python's http.server
- Simulate resilience conditions (latency, failures)
- Design ergonomic test doubles
- Document API contracts and limitations

## Limitations

- Single-threaded by default (use threading for concurrent requests)
- No authentication/authorization
- Limited template engine (not a full Jinja2 replacement)
