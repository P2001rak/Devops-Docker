FROM ubuntu

WORKDIR /app

# Install Python, pip, and venv
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv && \
    apt-get clean

# Create and activate a virtual environment
RUN python3 -m venv /app/venv

# Activate venv and install dependencies
COPY requirements.txt /app
RUN /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install --break-system-packages -r requirements.txt

# Set the working directory to devops
WORKDIR /app/devops
COPY devops /app/devops

# Use virtual environment Python
ENTRYPOINT ["/app/venv/bin/python"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]





