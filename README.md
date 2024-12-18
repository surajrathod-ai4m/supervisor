# Supervisor Configuration for Python Applications

This repository contains Supervisor configurations for managing Python applications. Supervisor ensures your applications are running continuously and restarts them automatically if they crash.

## Installation

### Ubuntu
```bash
sudo apt-get update
sudo apt-get install supervisor
```

### Fedora
```bash
sudo dnf install supervisor
```

## Configuration

### Ubuntu Configuration
Create a new configuration file:
```bash
sudo nano /etc/supervisor/conf.d/your_apps.conf
```

### Fedora Configuration
Create a new configuration file:
```bash
sudo nano /etc/supervisord.d/your_apps.ini
```

## Basic Configuration Template

```ini
[program:your_program_name]
command=/usr/bin/python3 /path/to/your/script.py
directory=/path/to/working/directory
user=your_username
autostart=true
autorestart=true
startsecs=10
startretries=999
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/your_program.err.log
stdout_logfile=/var/log/your_program.out.log
```

## Web Interface Setup

### Enable Web Interface (Ubuntu)
Edit the supervisor configuration:
```bash
sudo nano /etc/supervisor/supervisord.conf
```

Add:
```ini
[inet_http_server]
port=*:9001
username=your_username
password=your_password
```

### Enable Web Interface (Fedora)
Edit the supervisor configuration:
```bash
sudo nano /etc/supervisord.conf
```

Add the same [inet_http_server] section as above.

## Common Commands

Start supervisor:
```bash
# Ubuntu
sudo service supervisor start

# Fedora
sudo systemctl start supervisord
```

Control programs:
```bash
# Read new/changed config files
sudo supervisorctl reread

# Activate new/changed config files
sudo supervisorctl update

# Start a program
sudo supervisorctl start program_name

# Stop a program
sudo supervisorctl stop program_name

# Restart a program
sudo supervisorctl restart program_name

# Get status of all programs
sudo supervisorctl status
```

## Logging

Logs are stored in:
- Ubuntu: typically in `/var/log/supervisor/`
- Fedora: typically in `/var/log/supervisor/`

View logs:
```bash
# Error logs
tail -f /var/log/your_program.err.log

# Output logs
tail -f /var/log/your_program.out.log
```

## Security Considerations

1. Use strong passwords for web interface
2. Consider using `127.0.0.1:9001` instead of `*:9001` for local-only access
3. Configure firewall rules if needed
4. Use appropriate file permissions for log files
5. Run programs under specific non-root users

## Troubleshooting

1. If program won't start:
   - Check logs in `/var/log/`
   - Verify paths in configuration
   - Check permissions
   - Ensure Python path is correct

2. If web interface isn't accessible:
   - Check if supervisor is running
   - Verify port isn't blocked by firewall
   - Ensure configuration is correct

3. Common error solutions:
   - "BACKOFF": Check command path and permissions
   - "FATAL": Check program exists and is executable
   - "EXITED": Check program logs for crash details

## Example Configuration

Here's a complete example for a Python web application:

```ini
[program:web_app]
command=/usr/bin/python3 /home/user/web_app/app.py
directory=/home/user/web_app
user=web_user
autostart=true
autorestart=true
startsecs=10
startretries=999
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/web_app.err.log
stdout_logfile=/var/log/web_app.out.log
environment=PORT="8000",DEBUG="False"
```
