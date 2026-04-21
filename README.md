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
| `x_padding_bytes` / `xPaddingBytes` | XHTTP padding, **должен совпадать с сервером** | *(не выставляется, если не задан)* |
| `extra` | URL-encoded JSON с доп. настройками xhttp (`xPaddingBytes`, `xmux`, `scMaxEachPostBytes`, `noGRPCHeader`, …) | — |

### ⚠️ Про `x_padding_bytes`

На стороне сервера xray это поле задаётся как `xPaddingBytes` (например,
`"80-600"`) внутри `xhttpSettings`. Значение на клиенте (sing-box) **должно
совпадать диапазоном** — иначе sing-box молча закроет поток с ошибкой
`stream error` / `bad padding` и OpenWRT-клиент не поднимется.

Поэтому конвертер **не выдумывает дефолт**: если ни в URL, ни в `extra` JSON
значение не указано, поле `x_padding_bytes` просто отсутствует в выходном
JSON — sing-box сам возьмёт совместимый дефолт. Если же сервер действительно
форсит конкретный диапазон — обязательно проставь его в ссылке:

```
vless://…&x_padding_bytes=80-600&…
```

или упакуй в `extra`:

```
vless://…&extra=%7B%22xPaddingBytes%22%3A%2280-600%22%7D&…
```

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
