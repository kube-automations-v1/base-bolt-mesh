# base-bolt-mesh

PostgreSQL 17 do ecossistema (padrão de nome: `base-<nome>`). Deploy via `shared-pipelines` → `cluster-gitops/apps/base-bolt-mesh`.

- **Interno (cluster):** `base-bolt-mesh-db.default.svc:5432`
- **VPN:** `100.77.183.32:30432`
- **Credenciais:** secret `base-bolt-mesh-credentials` (chaves `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`), criado manualmente no cluster — nunca no Git.
- **Persistência:** PVC 10Gi na StorageClass `local-path-retain` (dados em `/var/lib/rancher/k3s/storage/` na VM, preservados mesmo se o PVC for apagado).
- **Backup:** CronJob diário 03:00 (`pg_dump | gzip`), 7 últimos em PVC `base-bolt-mesh-backups`.
- **initdb/**: scripts SQL/sh rodados só na primeira inicialização do volume; mudanças depois exigem migração manual.

Doc completa: `cluster-gitops/README.md`.
