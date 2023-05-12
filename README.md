- for production, run this :

```
docker compose -f docker-compose.yml -f docker-compose-prod.yml build --no-cache && docker compose -f docker-compose.yml -f docker-compose-prod.yml up -d
```

- for development, run this :

```
docker compose -f docker-compose.yml build --no-cache && docker compose -f docker-compose.yml up -d
```