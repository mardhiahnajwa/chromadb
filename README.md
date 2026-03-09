# ChromaDB Docker Compose Setup

This Docker Compose configuration runs the ChromaDB vector database in a containerized environment.

## Prerequisites

- Docker and Docker Compose installed on your system
- Sufficient disk space for vector database storage

## Quick Start

### Start the Service

```bash
# Start ChromaDB in the foreground
docker compose up

# Start ChromaDB in the background
docker compose up -d
```

### Stop the Service

```bash
docker compose down
```

## Configuration

### Service Details

- **Container Name**: `chromadb`
- **Image**: `chromadb/chroma`
- **Port**: 3001 (mapped to localhost:3001)
- **Data Volume**: `./chroma-data:/data`

### Accessing ChromaDB

Once running, access ChromaDB at:
```
http://localhost:3001
```

## Data Persistence

The `chroma-data` directory on your host machine is mounted to `/data` inside the container. This ensures your vector database data persists even after the container stops.

```
./chroma-data/          # Host directory (created automatically)
└── (container data)    # Mount point: /data
```

## Common Commands

```bash
# View logs
docker compose logs -f

# View container status
docker compose ps

# Execute commands in the running container
docker compose exec chromadb <command>

# Rebuild without cache
docker compose up --build --no-cache
```

## Troubleshooting

### Port Already in Use
If port 3001 is already in use, modify the `docker-compose.yml` file:
```yaml
ports:
  - "3002:8000"  # Map to a different host port
```

### Permission Issues
If you encounter permission issues with the `chroma-data` directory:
```bash
# Grant write permissions
chmod -R 755 ./chroma-data
```

## More Information

- [ChromaDB Documentation](https://docs.trychroma.com/)
- [Docker Compose Reference](https://docs.docker.com/compose/compose-file/)
