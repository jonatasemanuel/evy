FROM python:3.9-alpine3.13

ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY requirements.txt /app/requirements.txt

RUN python -m venv /py && \
  /py/bin/pip install --upgrade pip && \
  apk add --update --no-cache postgresql-client && \
  apk add --update --no-cache --virtual .tmp-build-deps \
  build-base postgresql-dev musl-dev && \
  /py/bin/pip install -r /app/requirements.txt  

COPY . /app

ENV PATH="/py/bin:$PATH"

CMD gunicorn --bind 0.0.0.0:8000 app:app
