# Use a specific Python version instead of "latest" to ensure stability
FROM python:3.11-slim as backend

# Install only necessary dependencies (no unnecessary utilities)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Poetry
RUN pip install --no-cache-dir poetry

# Set the working directory
WORKDIR /app

# Copy only the necessary files for dependency installation
COPY pyproject.toml poetry.lock ./

# Install dependencies (use --no-root to avoid installing the project itself as a package)
RUN poetry install --no-root --no-dev

# Copy the remaining application files
COPY . .

# Expose the port FastAPI runs on
EXPOSE 8000

# Run the FastAPI app
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]
