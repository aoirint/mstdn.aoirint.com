# mstdn.aoirint.com

## Backup DB

```shell
docker compose down
docker compose up -d db
docker compose exec db pg_dump -Fc -U mastodon mastodon > "postgres_$(date '+%Y-%m-%d_%H-%M-%S').dump"
```

## Restore DB

```shell
docker compose down
rm -rf postgres/
docker compose up -d db
cat backups/postgres.dump | docker compose exec -T db pg_restore -U mastodon -d mastodon --single-transaction
```

