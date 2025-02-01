FROM ubuntu

WORKDIR /app

# Install Python, pip, and venv
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv && \
    apt-get clean

# Create and activate a virtual environment
RUN python3 -m venv /app/venv

# Copy the requirements.txt and install dependencies inside the virtual environment
COPY requirements.txt /app
RUN /app/venv/bin/pip install --upgrade pip && \
    /app/venv/bin/pip install --break-system-packages -r requirements.txt

# Copy the rest of the app (including `devops` directory)
COPY devops /app/devops

# Apply database migrations (automatically)
RUN /app/venv/bin/python manage.py migrate

# Start the Django development server
CMD ["/app/venv/bin/python", "manage.py", "runserver", "0.0.0.0:8000"]
