
# Start by pulling the Python image
FROM python:3.8-alpine
RUN sed -i 's/dl-cdn.alpinelinux.org/dl-4.alpinelinux.org/' /etc/apk/repositories

# Set environment variable for unbuffered logging (useful in Docker)
ENV PYTHONUNBUFFERED=1

# Copy the requirements file into the Docker image
COPY requirements.txt /requirements.txt


# Install build dependencies and libraries
RUN apk add --update --no-cache --virtual .tmp-build-deps \
    gcc libc-dev linux-headers postgresql-dev libffi-dev \
    && python -m pip install --no-cache-dir --disable-pip-version-check --requirement /requirements.txt \
    && apk del .tmp-build-deps

# Expose the application port (adjust as needed)
EXPOSE 5005

# Default command to start the app
CMD ["gunicorn", "--config", "CPSC/gunicorn-cfg.py", "CPSC.run:app"]