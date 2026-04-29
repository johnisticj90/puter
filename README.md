# Puter

An open-source, self-hostable cloud desktop environment. Run your own personal cloud OS in the browser.

[![Docker Image](https://github.com/HeyPuter/puter/actions/workflows/docker-image.yaml/badge.svg)](https://github.com/HeyPuter/puter/actions/workflows/docker-image.yaml)

## Features

- 🖥️ Full desktop environment in the browser
- 📁 File system with cloud storage
- 🔒 User authentication and permissions
- 🐳 Docker support for easy self-hosting
- 🌐 Web-based apps and extensibility

## Quick Start

### Using Docker

```bash
docker pull ghcr.io/heyputer/puter
docker run -d \
  -p 4100:4100 \
  -v puter_data:/var/puter \
  ghcr.io/heyputer/puter
```

Then open [http://localhost:4100](http://localhost:4100) in your browser.

### Manual Setup

**Prerequisites:**
- Node.js >= 16
- npm >= 8

```bash
# Clone the repository
git clone https://github.com/HeyPuter/puter.git
cd puter

# Install dependencies
npm install

# Copy environment config
cp .env.example .env

# Start the server
npm start
```

## Configuration

Copy `.env.example` to `.env` and adjust the values as needed.

| Variable | Description | Default |
|----------|-------------|--------|
| `PORT` | HTTP server port | `4100` |
| `PUTER_DOMAIN` | Domain for the instance | `localhost` |
| `STORAGE_PATH` | Path for user data storage | `./data` |

> **Personal note:** I run this on my home server with `STORAGE_PATH` pointed to an external drive (`/mnt/storage/puter`) so user data survives container rebuilds. Recommend doing the same if you're self-hosting long-term.

> **Heads up:** Port `4100` can conflict with some React/Vue dev servers if you're running this alongside other projects. I changed mine to `4200` in `.env` to avoid the headache — just remember to update the Docker `-p` flag too if you go that route.

> **Low-spec hardware tip:** If you're running this on something like a Raspberry Pi or an older box with ≤2GB RAM, add `--max-old-space-size=512` to the node start command in `package.json` to keep memory usage in check. Without it I was seeing the process get OOM-killed after a day or two of uptime.

## Development

```bash
# Run in development mode with hot reload
npm run dev

# Run tests
npm test

# Lint
npm run lint
```

## Contributing

Pull requests are welcome! Please open an issue first to discuss major changes.

## License

AGPL-3.0 — see [LICENSE](LICENSE) for details.
