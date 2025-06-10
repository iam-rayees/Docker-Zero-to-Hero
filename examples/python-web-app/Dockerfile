FROM ubuntu:latest

WORKDIR /app

# Copy only what's needed first (faster rebuilds)
COPY requirements.txt .

# Install Python and pip
RUN apt-get update && \
    apt-get install -y python3 python3-pip

# Install Python dependencies
RUN pip install --no-cache-dir --break-system-packages -r requirements.txt

# Now copy the rest of your app (this avoids re-copying if requirements don't change)
COPY devops /app/devops

# Set working directory to devops (optional, if that's where manage.py is)
WORKDIR /app/devops

# Run the Django app
ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
