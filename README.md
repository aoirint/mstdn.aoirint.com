# mstdn.aoirint.com

## アカウント作成

```shell
sudo docker compose exec web bin/tootctl accounts create example_acct --email mail@example.com --confirmed
```

## Backup DB

```shell
docker compose down
docker compose up -d db
docker compose exec db pg_dump -Fc -U mastodon mastodon > "backups/postgres_$(date '+%Y-%m-%d_%H-%M-%S').dump"
```

## Restore DB

```shell
docker compose down
rm -rf postgres/
docker compose up -d db
cat backups/postgres.dump | docker compose exec -T db pg_restore -U mastodon -d mastodon --single-transaction
```

