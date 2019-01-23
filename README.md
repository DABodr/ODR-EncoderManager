# ODR-EncoderManager RaspberryPi version

OpenDigitalRadio Encoder Manager is a tools to run and configure ODR Encoder easly with a WebGUI.
This configuration ensure your user is "pi"

# INSTALLATION

  * Install requirement : `sudo apt install python-cherrypy3 python-jinja2 python-serial supervisor`
  * Add pi user to dialout group : `sudo usermod -a -G dialout pi`
  * Add pi user to audio group : `sudo usermod -a -G audio pi`
  * Got to pi user home : `cd /home/pi/`
  * Clone git repository : `git clone https://github.com/DABodr/ODR-EncoderManager`
  * Rename sample config : `mv /home/pi/ODR-EncoderManager/config.json.sample /home/pi/ODR-EncoderManager/config.json`
  * Make the symlink: `sudo ln -s /home/pi/ODR-EncoderManager/supervisor-encoder.conf /etc/supervisor/conf.d/odr-encoder.conf`
  * Make the symlink: `sudo ln -s /home/pi/ODR-EncoderManager/supervisor-gui.conf /etc/supervisor/conf.d/odr-gui.conf`
  * Edit `/etc/supervisor/supervisord.conf` and add this section :
```
[inet_http_server]
port = 8001
username = odr ; Auth username
password = odr ; Auth password
```
  * Restart supervisor : `sudo /etc/init.d/supervisor restart`
  * Start WEB server : `sudo supervisorctl reread & sudo supervisorctl update ODR-encoderManager`
  * Go to : `http://<ip_address>:8080`



# CONFIGURATION
  * You can edit global configuration, in particular path in this files :
    * config.json
    * supervisor-gui.conf
  * If you want to change supervisor XMLRPC login/password, you need to edit `/etc/supervisor/supervisord.conf` and `config.json` files

# ADVANCED
  * To use the reboot api (/api/reboot), you need to allow pi user to run shutdown command by adding the line bellow at the end of /etc/sudoers file :
```
pi     ALL=(ALL) NOPASSWD: /sbin/shutdown
```
