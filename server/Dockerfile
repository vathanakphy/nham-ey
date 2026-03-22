# Use Python 3.11 slim
FROM python:3.11-slim

# Set environment
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN curl -sSL https://install.python-poetry.org | python3 -

# Add Poetry to PATH
ENV PATH="/root/.local/bin:$PATH"

# Set workdir
WORKDIR /app

# Copy project files
COPY pyproject.toml poetry.lock /app/

# Install dependencies
RUN poetry install --no-root

# Copy rest of the code
COPY . /app/

# Expose port
EXPOSE 8000

# Run Django server
CMD ["poetry", "run", "uvicorn", "nhamey.asgi:application", "--host", "0.0.0.0", "--port", "8000", "--reload"]