Podman ローカル起動
==================

このディレクトリには、CRISPRdirect を Podman と Apache でローカル起動するためのファイルが含まれています。

APACHE_PORT を `.env` で指定します。

```sh
cat .env
APACHE_PORT=20080
```

起動:

```sh
podman-compose up -d --build
```

確認:

```sh
curl -I http://localhost:20080
curl http://localhost:20080 | head
curl -I http://localhost:20080/doc/
curl -I http://localhost:20080/detail/
```

停止:

```sh
podman-compose down
```

ログ確認:

```sh
podman-compose logs web
```

ユーザーサービスとして登録:

```sh
./podman_enable_service.sh podman-compose-crisprdirect
```

上記を実行すると `~/.config/systemd/user/podman-compose-crisprdirect.service` が作成され、`podman-compose.yml` のサービスが現在のユーザーの systemd サービスとして有効化・起動されます。

状態確認:

```sh
systemctl --user status podman-compose-crisprdirect
```

自動起動の無効化と停止:

```sh
./podman_disable_service.sh podman-compose-crisprdirect
```
