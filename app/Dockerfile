FROM python:3.15.2-trixie@sha256:cc8e02af50fcaf0944fd02158cd77abce78eb4b41ac0217a8434bbc475225e09

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    PIP_DISABLE_PIP_VERSION_CHECK=1

WORKDIR /app

RUN groupadd --system app \
 && useradd --system --gid app --create-home --shell /usr/sbin/nologin app

COPY requirements.txt .

RUN pip install --no-cache-dir --root-user-action=ignore -r requirements.txt \
   && pip uninstall -y --root-user-action=ignore pip

COPY --chown=app:app main.py .

USER app

EXPOSE 8080

CMD ["gunicorn", "--bind", "0.0.0.0:8080", "main:app"]