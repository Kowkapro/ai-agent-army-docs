# Установка на VPS

## Что нужно

- VPS с Ubuntu 22.04 или 24.04 (минимум 1 CPU, 1GB RAM)
- Аккаунт Anthropic для API ключа (или другой провайдер — OpenAI, Google)
- 10 минут времени

Подойдёт любой VPS: Hetzner (~€4/мес), DigitalOcean ($6/мес), Timeweb, Selectel.

## Шаг 1. Подключиться к серверу

```bash
ssh root@ВАШ_IP_СЕРВЕРА
```

## Шаг 2. Установить Node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
node --version
```

Должно вывести `v22.x.x` или выше.

## Шаг 3. Установить OpenClaw

```bash
npm install -g openclaw
openclaw --version
```

## Шаг 4. Инициализировать

```bash
openclaw init
```

Мастер настройки спросит:
- **API ключ** — вставь ключ от Anthropic (получить на console.anthropic.com)
- **Канал** — выбери Telegram
- **Токен бота** — сюда вставишь токен который получишь на следующем шаге

## Шаг 5. Создать Telegram-бота

1. Открой Telegram, напиши [@BotFather](https://t.me/BotFather)
2. Отправь команду `/newbot`
3. Придумай имя боту (например: `Мой Агент`)
4. Придумай username (должен заканчиваться на `bot`, например: `myagent_bot`)
5. Скопируй токен вида `1234567890:ABCdef...`
6. Вставь токен в конфиг OpenClaw

## Шаг 6. Запустить агента

```bash
openclaw gateway start
```

Открой Telegram, найди своего бота, напиши что-нибудь. Агент ответит.

## Шаг 7. Запуск как системный сервис

Чтобы агент работал после перезагрузки сервера:

```bash
openclaw gateway install
systemctl enable openclaw
systemctl start openclaw
```

Проверить статус:

```bash
openclaw gateway status
```

## Готово

Агент работает. Следующий шаг — настроить его под себя.

[Первый запуск и настройка →](pervyj-zapusk.md)
