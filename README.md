# 🔗 VLESS XHTTP Converter — Podkop Edition

Веб-утилита для конвертации `vless://` ссылок в JSON-конфигурацию outbound sing-box.

## ✨ Возможности

- ⚡ Мгновенная конвертация в браузере (без сервера)
- 🔒 Поддержка **Reality** и **TLS**
- 🚀 Транспорт **XHTTP** (splithttp) с настройкой mode / path / host
- 📋 Копирование JSON одной кнопкой
- ⌨️ **Enter** для быстрой конвертации
- 🌙 Тёмный дизайн с подсветкой синтаксиса
- 📱 Адаптивный интерфейс

## 🚀 Использование

**Онлайн:** [eikeidev.github.io/vless-xtls-converter](https://eikeidev.github.io/vless-xtls-converter/)

**Локально:** откройте `index.html` в любом браузере.

Вставьте ссылку:

```
vless://uuid@server:443?type=xhttp&security=reality&sni=example.com&pbk=KEY&sid=ID&fp=chrome&path=/xhttp&mode=auto#MyProxy
```

Нажмите **«Конвертировать в JSON»** или **Enter** — готовый outbound появится ниже.

## 📋 Поддерживаемые параметры

| Параметр | Описание | По умолчанию |
|---|---|---|
| `type` | Тип транспорта | `xhttp` |
| `security` | Шифрование (`reality` / `tls`) | — |
| `sni` | Server Name Indication | — |
| `pbk` | Reality public key | — |
| `sid` | Reality short ID | — |
| `fp` | Fingerprint (uTLS) | `chrome` |
| `path` | Путь транспорта | `/` |
| `mode` | Режим XHTTP | `auto` |
| `host` | HTTP host | = `sni` |
| `alpn` | ALPN протоколы | `h2,http/1.1` |
| `allowInsecure` | Пропуск проверки сертификата | `0` |

## 📦 Пример вывода

```json
{
  "type": "vless",
  "tag": "MyProxy",
  "server": "server",
  "server_port": 443,
  "uuid": "uuid",
  "flow": "",
  "tls": {
    "enabled": true,
    "server_name": "example.com",
    "alpn": ["h2", "http/1.1"],
    "reality": {
      "enabled": true,
      "public_key": "KEY",
      "short_id": "ID"
    },
    "utls": {
      "enabled": true,
      "fingerprint": "chrome"
    }
  },
  "transport": {
    "type": "xhttp",
    "path": "/xhttp",
    "host": "example.com",
    "mode": "auto"
  }
}
```

## ⚙️ Требования

- Любой современный браузер
- Интернет **не нужен** — всё работает локально
