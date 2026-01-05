FROM python:3.13.3-slim-bookworm

WORKDIR /usr/src/app

COPY --from=ghcr.io/astral-sh/uv:0.9.21 /uv /uvx /bin/

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV UV_PROJECT_ENVIRONMENT=/usr/src/app/.venv
ENV UV_NO_CACHE=true
ENV UV_LINK_MODE=copy

RUN apt-get update \
  && apt-get -y install netcat-traditional gcc postgresql \
  && apt-get clean

COPY pyproject.toml uv.lock ./
RUN uv sync

COPY . .

COPY ./entrypoint.sh .

RUN chmod +x /usr/src/app/entrypoint.sh

ENTRYPOINT [ "/usr/src/app/entrypoint.sh" ]
