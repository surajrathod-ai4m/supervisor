# supervisor
Create supervisor for python files


1. First install supervisor:bash
sudo dnf install supervisor
2. The config file location on Fedora is:bash
sudo nano /etc/supervisord.d/dash_apps.ini(Note: it's .ini not .conf on Fedora, and it's in supervisord.d folder)

3. The configuration content remains same:ini
[program:random_1]
command=/usr/bin/python3 "/home/ai4m/Desktop/Programs/HUL Haridwar/System_architecture/random_1.py"
directory=/home/ai4m/Desktop/Programs/HUL Haridwar/System_architecture
user=ai4m
autostart=true
autorestart=true
startsecs=10
startretries=999
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/random_1.err.log
stdout_logfile=/var/log/random_1.out.log

[program:random_shit]
command=/usr/bin/python3 "/home/ai4m/Desktop/Programs/HUL/python_backup/HUL_Hridwar/2_Program/random_shit.py"
directory=/home/ai4m/Desktop/Programs/HUL/python_backup/HUL_Hridwar/2_Program
user=ai4m
autostart=true
autorestart=true
startsecs=10
startretries=999
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/random_shit.err.log
stdout_logfile=/var/log/random_shit.out.log
4. Start and enable the supervisor service:bash
sudo systemctl start supervisord
sudo systemctl enable supervisord
5. The commands to control supervisor are the same:bash
sudo supervisorctl reread
sudo supervisorctl update
sudo supervisorctl start random_1
sudo supervisorctl start random_shit
sudo supervisorctl status
Key differences from Ubuntu:
Config directory is /etc/supervisord.d/ (not /etc/supervisor/conf.d/)
Files end with .ini (not .conf)
Service name is supervisord (not supervisor)
Log files typically go in /var/log/supervisor/ by default
