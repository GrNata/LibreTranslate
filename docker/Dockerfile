# Используем официальный Python образ
FROM python:3.11.11-slim-bullseye AS builder

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем все файлы проекта в контейнер
COPY . .

# Создаём виртуальное окружение и активируем его
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Устанавливаем pip и зависимости
RUN pip install --upgrade setuptools wheel pip

# Устанавливаем проект
RUN pip install 

# Устанавливаем и выводим версии
RUN python --version
RUN pip --version

# # Устанавливаем необходимые пакеты
# RUN pip install -r requirements.txt

# Финальная стадия
FROM python:3.11.11-slim-bullseye

WORKDIR /app

# Копируем всё с этапа сборки
COPY --from=builder /app /app

# Устанавливаем зависимости и запускаем приложение
RUN pip install -r requirements.txt

# Открываем порты
EXPOSE 5000

# Запуск приложения
CMD ["./venv/bin/libretranslate", "--host", "*"]


# FROM python:3.11.11-slim-bullseye AS builder

# WORKDIR /app

# ARG DEBIAN_FRONTEND=noninteractive
# RUN apt-get update -qq \
#   && apt-get -qqq install --no-install-recommends -y pkg-config gcc g++ \
#   && apt-get upgrade --assume-yes \
#   && apt-get clean \
#   && rm -rf /var/lib/apt

# # RUN python -mvenv venv && ./venv/bin/pip install --no-cache-dir --upgrade pip
# # Создаём виртуальное окружение
# RUN python -m venv venv

# # Выводим версии Python и pip
# RUN python --version
# RUN pip --version

# # Обновляем зависимости для сборки
# RUN ./venv/bin/pip install --upgrade build setuptools hatchling

# # Устанавливаем пакеты
# RUN ./venv/bin/pip install --no-cache-dir --upgrade pip
# RUN ./venv/bin/pip install



# # Install package from source code, compile translations
# RUN ./venv/bin/pip install Babel==2.12.1 && ./venv/bin/python scripts/compile_locales.py \
#   && ./venv/bin/pip install torch==2.0.1 --extra-index-url https://download.pytorch.org/whl/cpu \
#   && ./venv/bin/pip install "numpy<2" \
#   && ./venv/bin/pip install . \
#   && ./venv/bin/pip cache purge

# FROM python:3.11.11-slim-bullseye

# ARG with_models=false
# ARG models=""

# RUN addgroup --system --gid 1032 libretranslate && adduser --system --uid 1032 libretranslate && mkdir -p /home/libretranslate/.local && chown -R libretranslate:libretranslate /home/libretranslate/.local
# USER libretranslate

# COPY --from=builder --chown=1032:1032 /app /app
# WORKDIR /app

# COPY --from=builder --chown=1032:1032 /app/venv/bin/ltmanage /usr/bin/

# RUN if [ "$with_models" = "true" ]; then  \
#   # initialize the language models
#   if [ ! -z "$models" ]; then \
#   ./venv/bin/python scripts/install_models.py --load_only_lang_codes "$models";   \
#   else \
#   ./venv/bin/python scripts/install_models.py;  \
#   fi \
#   fi

# EXPOSE 5000
# ENTRYPOINT [ "./venv/bin/libretranslate", "--host", "*" ]
