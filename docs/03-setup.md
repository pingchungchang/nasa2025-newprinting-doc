# Setup
## Prerequisites

> 請在這邊寫出環境建置的需求

## Environment Variables (.env)
- `ubuntu/django-backend`: 修改 `config/settings.py`:
    - `AUTH_LDAP_SERVER_URI`、`AUTH_LDAP_USER_DN_TEMPLATE`: LDAP 驗證方式
    - `REDIS_PASSWORD`, `CACHES["default"]["SENTINELS"]`: redis
    - `DATABASES`: postgres
- `ubuntu/postgres-ha`（.env 忘記改成 .env.example 忘記 push 了 QQ）:
    - modify the environment in `docker-compose.yml`
```
- PATRONI_CLUSTER_NAME=${PATRONI_CLUSTER_NAME}
- NODE_NAME=${NODE_NAME}
- NODE_IP=${NODE_IP}
- NODE1_IP=${NODE1_IP}
- NODE2_IP=${NODE2_IP}
- NODE3_IP=${NODE3_IP}
- PG_SUPERUSER=${PG_SUPERUSER}
- PG_SUPERUSER_PASSWORD=${PG_SUPERUSER_PASSWORD}
- PG_REPL_USER=${PG_REPL_USER}
- PG_REPL_PASSWORD=${PG_REPL_PASSWORD}
- PATRONI_RESTAPI_PASSWORD=${PATRONI_RESTAPI_PASSWORD}
```
- `ubuntu/redis`
    - Fix the 172.16.127.122s into the IP of the current machine, and the 172.16.127.103s to the initial master IP

## Step-by-Step Local Launch
- `ubuntu/redis`:
    - rename `.env.example` to `.env` and modify to match environment
    - Fix the 172.16.127.122s into the IP of the current machine, and the 172.16.127.103s to the initial master IP
    - In ubuntu/redis/, add an .env and set REDIS_PASSWORD=your_password, then run sudo docker compose up --build
- `ubuntu/django-backend`:
    - modify `.env` to match environment
    - run `docker compose up --build`
- `ubuntu/postgres-ha`:
    - create a `.env` to announce `NODE{1,2,3}_NAME, NODE{1,2,3}_IP, NODE_NAME, NODE_IP`
    - run `docker compose up --build`


## Troubleshooting / FAQ

- 前端不能登入：postgres 死了，可能要重啟，如果有問題就把 postgres 的 etcd staorage 砍掉之後 restart
- 可以登入但列印失敗：windows 跟 ubuntu 連線不穩定，過一陣子再試一次可能就好了（具體問題還是抓不到QQ）
