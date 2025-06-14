# Aider-Docker: AI-ассистент для разработки в Docker

Проект предоставляет удобную среду для работы с [Aider](https://github.com/Aider-AI/aider) - AI-ассистентом для программирования, использующим локальные модели через [Ollama](https://github.com/ollama/ollama).

## 🚀 Быстрый старт

1. Клонируйте репозиторий:
```bash
git clone https://github.com/HardAndHeavy/aider-docker
cd aider-docker
```

2. Настройте окружение:
```bash
make gen  # Запустит интерактивную настройку
```

3. Запустите Aider:
```bash
make run  # Запустит Aider в Docker
```

## ⚙️ Конфигурация

Проект использует Ansible для управления настройками. Основные параметры:

| Параметр       | Описание                          | Значение по умолчанию                     |
|----------------|-----------------------------------|-------------------------------------------|
| `project_dir`  | Директория с проектом            | `./app`                                   |
| `model_name`   | Модель Ollama                    | `qwen2.5-coder:32b-instruct-q4_K_M`       |
| `ollama_api`   | URL API Ollama                   | `http://host.docker.internal:11434`       |
| `conventions`  | Соглашения по коду               | `The project is being developed in python`|

Настройки сохраняются в `secure/var/` и могут быть изменены вручную.

## 📂 Структура проекта

```
.
├── ansible/            # Ansible-конфигурация
│   ├── gen.yml         # Плейбук настройки
│   └── templates/      # Шаблоны конфигов
├── config/             # Сгенерированные конфиги
├── secure/var/         # Локальные настройки
└── Makefile            # Управление проектом
```

## 🔧 Команды

- `make gen` - Настройка окружения
- `make run` - Запуск Aider
- `make init` - Создание директории проекта

## 💡 Советы

1. Для использования своих моделей Ollama:
   - Измените `secure/var/model_name`
   - Или укажите при запуске: `make gen model_name=your-model`

2. Чтобы изменить рабочую директорию:
   ```bash
   make gen project_dir=/path/to/your/project
   ```

3. Все настройки можно редактировать вручную в файлах `secure/var/*`

## 🔗 Полезные ссылки

- [Документация Aider](https://aider.chat/)
- [Ollama модели](https://ollama.ai/library)
- [Ansible документация](https://docs.ansible.com/)
