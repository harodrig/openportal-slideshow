# openportal-slideshow

![CI](https://github.com/harodrig/openportal-slideshow/actions/workflows/ci.yml/badge.svg)

A minimalist photo slideshow served by a pure Node.js HTTP server with
no external dependencies. Built as a learning project covering frontend
development, containerization, security hardening, testing and CI/CD.

---

## Features

- Vanilla HTML, CSS and JavaScript — no frameworks
- Autoplay with configurable interval, keyboard navigation and fullscreen support
- NoSleep.js integration to prevent screen timeout during playback
- Pure Node.js HTTP server using only built-in modules
- Security headers, rate limiting and path traversal prevention
- Runs as a non-root user inside a Docker container
- Photos mounted as a read-only volume at runtime

---

## Requirements

- Node.js >= 20
- Docker and Docker Compose

---

## Running locally

**Without Docker:**
```bash
node index.js
# open http://localhost:3000
```

**With Docker:**
```bash
docker compose up
# open http://localhost:3000
```

Place images in the `./photos` directory before starting. Supported
formats: `jpg`, `jpeg`, `png`, `webp`, `gif`.

---

## Configuration

| Variable    | Default    | Description                        |
|-------------|------------|------------------------------------|
| `PORT`      | `3000`     | Port the server listens on         |
| `PHOTOS_DIR`| `./photos` | Path to the photos directory       |
| `NODE_ENV`  | `production` | Node environment                 |

---

## Development
```bash
# Install dev dependencies
npm install

# Run tests
npm test

# Lint
npm run lint

# Syntax check
npm run check

# Build Docker image
docker compose build

# Rebuild without cache
docker compose build --no-cache
```

---

## Project structure
```
photo-slideshow/
├── .github/workflows/    # CI and CD pipelines
├── public/               # Frontend (HTML, CSS, JS)
├── src/
│   ├── server.js         # HTTP server logic
│   └── rateLimiter.js    # In-memory rate limiter
├── tests/                # Node built-in test suite
├── photos/               # Mount point for images (not committed)
├── index.js              # Entry point
├── Dockerfile
└── docker-compose.yml
```

---

## API

| Method | Path              | Description                        |
|--------|-------------------|------------------------------------|
| GET    | `/`               | Serves the slideshow frontend      |
| GET    | `/api/photos`     | Returns JSON list of photo files   |
| GET    | `/photos/:file`   | Serves an individual image         |

---

## License

MIT
