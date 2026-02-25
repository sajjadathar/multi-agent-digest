FROM python:3.12.3-slim

# Standard performance/logging tweaks
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1

WORKDIR /app

# Leverages build cache for dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Copy only what you need
COPY app.py .

CMD ["python", "app.py"]