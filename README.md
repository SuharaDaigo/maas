# MAAS(Metal as a Service)をインストールするためのAnsibleプレイブック

本番環境用のMAAS環境をPostgreSQLデータベースと共に構築するAnsibleプレイブックです。

## 前提条件

- Ubuntu 22.04以降
- Ansible 2.9以降
- sudo権限

## 設定

### 1. 変数ファイルの設定

`playbook/vars/maas_config.yml`ファイルで設定を変更してください：

```yaml
# 管理者アカウント
maas_admin_user: "your_username"
maas_admin_pass: "your_secure_password"
maas_admin_email: "your_email@example.com"

# PostgreSQLデータベース設定
postgres_password: "your_database_password"
```

サンプルファイルも用意されています：
```bash
cp playbook/vars/maas_config.yml.example playbook/vars/maas_config.yml
```

### 2. セキュリティに関する注意

- パスワードは強力なものを設定してください
- 本番環境では`maas_config.yml`をGit管理から除外することを推奨します

## プレイブックの実行

```bash
cd playbook
ansible-playbook -i hosts.ini install_maas.yml
```

## インストール後の設定

プレイブック実行後、以下の設定を行ってください：

1. **DNS設定**: フォワーダーを設定（例: 8.8.8.8）
2. **イメージインポート**: Ubuntu LTSイメージを選択
3. **SSH鍵**: Launchpad、GitHub、またはローカルファイルから追加
4. **DHCP有効化**: 必要なサブネットでDHCPを有効化

## アクセス

- **Web UI**: `http://your_server_ip:5240/MAAS/`
- **管理者ログイン**: 設定したユーザー名とパスワードでログイン