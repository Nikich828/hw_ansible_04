# Ansible Role: Vector

Устанавливает и настраивает Vector - observability data pipeline для сбора, трансформации и маршрутизации логов.

## Требования

- Ansible >= 2.9
- ОС: RHEL/CentOS 7/8/9
- Права sudo для установки пакетов

## Параметры роли

Все переменные, которые можно переопределить, находятся в `defaults/main.yml`:

| Параметр | Значение по умолчанию | Описание |
|----------|----------------------|----------|
| `vector_version` | `0.22.1` | Версия Vector для установки. Также принимает `latest` |
| `vector_config_dir` | `/etc/vector` | Путь к директории с конфигурацией Vector |
| `vector_config` | (см. ниже) | Конфигурация Vector в формате YAML. Полностью совместима с официальной документацией |

### Структура `vector_config`

По умолчанию используется следующая конфигурация:

```yaml
vector_config:
  api:
    enabled: true
    address: "0.0.0.0:8686"
  sources:
    demo_logs:
      type: demo_logs
      format: syslog
  sinks:
    to_clickhouse:
      type: clickhouse
      inputs:
        - demo_logs
      database: logs
      endpoint: "http://localhost:8123"
      table: vector_table
      compression: gzip
      healthcheck: true
      skip_unknown_fields: true