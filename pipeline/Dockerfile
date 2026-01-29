# Start with slim Python 3.13 image
FROM python:3.13.11-slim

# Copy uv binary from official uv image (multi-stage build pattern)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# Set working directory
WORKDIR /app

# Add virtual environment to PATH so we can use installed packages or use host machine (:$PATH for fallback)
ENV PATH="/app/.venv/bin:$PATH"

# Copy dependency files first (better layer caching)
COPY pyproject.toml .python-version uv.lock ./

# Create virtual environment using .python-version and pyproject.toml file if none exists
# and install dependencies from lock file (ensures reproducible builds)
RUN uv sync --locked

COPY ingest_data.py .

ENTRYPOINT ["python", "ingest_data.py" ]