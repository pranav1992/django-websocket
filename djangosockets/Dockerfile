FROM python:3.11-slim
# Install system deps
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y --no-install-recommends build-essential gcc libpq-dev curl \
    && rm -rf /var/lib/apt/lists/*
# Create app directory and user
WORKDIR /app
# Install dependencies
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

# Copy app files
COPY . .
RUN chmod +x /app/entrypoint.sh
# Expose port
EXPOSE 8000


ENTRYPOINT ["/app/entrypoint.sh"]
CMD ["gunicorn", "djangosockets.asgi:application", "-k", "uvicorn.workers.UvicornWorker", "-b", "0.0.0.0:8000", "-w", "4"]

# CMD ["gunicorn", "djangosockets.asgi:application", "-k", "uvicorn.workers.UvicornWorker"]
# Run app
# CMD ["daphne","-b","0.0.0.0","-p","8000","djangosockets.asgi:application"]
