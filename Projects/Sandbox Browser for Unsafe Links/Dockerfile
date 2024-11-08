# Base Image: Uses Debian Slim as the base image, which provides a stable environment for Chrome.
FROM debian:bullseye-slim

# Dependencies: Installs dependencies for Chrome, Selenium, and a minimal X11 environment.
RUN apt-get update && \
    apt-get install -y \
    curl \
    unzip \
    gnupg \
    ca-certificates \
    supervisor \
    xvfb \
    x11vnc \
    openjdk-11-jre-headless \
    --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

# Chrome and ChromeDriver: Downloads and installs the latest stable version of Google Chrome and ChromeDriver, which is essential for Selenium to interact with Chrome.
RUN curl -sSL https://dl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    echo "deb [arch=amd64] https://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
    apt-get update && \
    apt-get install -y google-chrome-stable --no-install-recommends && \
    rm -rf /var/lib/apt/lists/*

RUN CHROME_DRIVER_VERSION=$(curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE) && \
    curl -sS -o /tmp/chromedriver.zip "https://chromedriver.storage.googleapis.com/${CHROME_DRIVER_VERSION}/chromedriver_linux64.zip" && \
    unzip -q /tmp/chromedriver.zip -d /usr/local/bin/ && \
    rm /tmp/chromedriver.zip

# Selenium Server: Downloads and sets up the Selenium Server JAR, allowing remote WebDriver commands.
RUN SELENIUM_VERSION=4.0.0 && \
    curl -sS -o /opt/selenium-server.jar "https://selenium-release.storage.googleapis.com/${SELENIUM_VERSION}/selenium-server-${SELENIUM_VERSION}.jar"

# Expose ports for Selenium (4444) and VNC (5900).
EXPOSE 4444 5900

# Supervisor Configuration: Manages Xvfb and Selenium.
COPY <<EOF /etc/supervisor/conf.d/supervisord.conf
[supervisord]
nodaemon=true

[program:xvfb]
command=Xvfb :99 -screen 0 1280x1024x24
autostart=true
autorestart=true

[program:selenium]
command=java -jar /opt/selenium-server.jar
environment=DISPLAY=:99
autostart=true
autorestart=true

[program:x11vnc]
command=x11vnc -display :99 -forever -nopw -listen 0.0.0.0 -xkb
autostart=true
autorestart=true
EOF

# Command to run Supervisor and manage all services.
CMD ["supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]