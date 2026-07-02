# DVC: передача конфигурации remote между серверами

Краткая инструкция по тому, как правильно шарить настройки DVC remote при клонировании репозитория на новый сервер.

## Ключевой принцип

DVC хранит конфигурацию в двух файлах:

| Файл | Что хранит | Git |
|------|-----------|-----|
| `.dvc/config` | Публичные параметры remote (url, region, ...) | ✅ Коммитится |
| `.dvc/config.local` | Секреты (ключи доступа, пароли) | ❌ В `.gitignore` |

**Публичную конфигурацию коммитим в Git, секреты — никогда.**

## Настройка на исходном сервере

```bash
# 1. Добавить remote с публичными параметрами (пишется в .dvc/config)
dvc remote add -d storage s3://mybucket/dvcstore
dvc remote modify storage region us-east-1

# 2. Закоммитить конфигурацию
git add .dvc/config .dvc/.gitignore
git commit -m "Configure DVC remote storage"
git push

# 3. Настроить credentials локально (в .dvc/config.local, НЕ коммитится)
dvc remote modify --local storage access_key_id 'KEY'
dvc remote modify --local storage secret_access_key 'SECRET'
```

## Настройка на новом сервере

```bash
# 1. Клонировать репозиторий — конфигурация remote уже в .dvc/config
git clone <repo-url>
cd <repo>

# 2. Добавить только credentials (локально)
dvc remote modify --local storage access_key_id 'KEY'
dvc remote modify --local storage secret_access_key 'SECRET'

# 3. Скачать данные
dvc pull
```

## Способы передачи credentials

1. **`.dvc/config.local`** — на каждом сервере отдельно (см. выше).
2. **Переменные окружения** — удобно для CI/CD:

   ```bash
   export AWS_ACCESS_KEY_ID='KEY'
   export AWS_SECRET_ACCESS_KEY='SECRET'
   ```

3. **AWS credentials file** — `~/.aws/credentials`.
4. **Secrets management** — для production: AWS Secrets Manager, HashiCorp Vault,
   Kubernetes Secrets, GitHub Secrets и т.п.

## Проверка

```bash
dvc remote list          # список remote
dvc config -l            # вся конфигурация
dvc status -r storage    # проверить связь с remote
```
