# Ansible Role: Lighthouse

Роль для установки и настройки Lighthouse - веб-интерфейса для мониторинга от VKCOM.

## Требования

- Ansible >= 2.9
- ОС: RHEL/CentOS 7/8/9
- Доступ к интернету для клонирования репозитория
- Права sudo для установки пакетов

## Параметры роли

Все переменные, которые можно переопределить, находятся в `defaults/main.yml`:

| Параметр | Значение по умолчанию | Описание |
|----------|----------------------|----------|
| `lighthouse_url` | `https://github.com/VKCOM/lighthouse.git` | URL репозитория Lighthouse |
| `lighthouse_dir` | `/var/www/lighthouse` | Директория для установки Lighthouse |
| `lighthouse_nginx_user` | `nginx` | Пользователь, от которого работает nginx |

## Зависимости

Роль автоматически устанавливает следующие пакеты:
- git
- epel-release
- nginx

SELinux контекст автоматически настраивается для директории Lighthouse.

## Примеры использования

### Базовое использование (все значения по умолчанию)

```yaml
- hosts: lighthouse
  roles:
    - role: lighthouse-role