# PulseCast Backend Dockerfile
# Multi-stage build for production optimization

# Stage 1: Builder stage
FROM python:3.11-slim as builder

# Set environment variables
ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1
ENV PIP_NO_CACHE_DIR=1
ENV PIP_DISABLE_PIP_VERSION_CHECK=1

# Install system dependencies for building
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    && rm -rf /var/lib/apt/lists/*

# Create and set the working directory
WORKDIR /app

# Copy requirements first for better Docker layer caching
COPY requirements.txt .

# Create a virtual environment and install dependencies
RUN python -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Upgrade pip and install dependencies
RUN pip install --upgrade pip \
    && pip install -r requirements.txt

# Stage 2: Production stage
FROM python:3.11-slim as production

# Set environment variables
ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1
ENV PATH="/opt/venv/bin:$PATH"

# Install only runtime system dependencies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

# Create a non-root user for security
RUN groupadd -r pulsecast && useradd -r -g pulsecast pulsecast

# Create necessary directories with proper permissions
RUN mkdir -p /app /app/logs /app/models /app/config \
    && chown -R pulsecast:pulsecast /app

# Copy virtual environment from builder stage
COPY --from=builder /opt/venv /opt/venv

# Set working directory
WORKDIR /app

# Copy application code
COPY --chown=pulsecast:pulsecast . .

# Copy config files
COPY --chown=pulsecast:pulsecast ../config ./config

# Switch to non-root user
USER pulsecast

# Expose the application port
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

# Default command
CMD ["python", "main.py"]

# Labels for better maintainability
LABEL maintainer="PulseCast Team"
LABEL version="1.0.0"
LABEL description="PulseCast Event Sentiment Tracker Backend"
LABEL org.opencontainers.image.source="https://github.com/Srimadhav-Seebu-Kumar/PulseCast-Event-Sentiment-Tracker"
