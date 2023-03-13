# How-To-Install-Mosquitto

update and  upgrade OS
```
sudo apt update && sudo apt upgrade -y
```
Install the Mosquitto Broker
```
sudo apt install -y mosquitto mosquitto-clients
```
Make Mosquitto auto start when the server boots
```
sudo systemctl enable mosquitto.service
```
test the installation by running
```
mosquitto -v
```
### Check mosquitto version
![2023-03-11_9-25-43](https://user-images.githubusercontent.com/48780839/224460231-f0ce338d-ef49-45c9-8712-b9bba5a55ca7.png)

## Enable Remote Access/ Authentication
```
sudo mosquitto_passwd -c /etc/mosquitto/passwd YOUR_USERNAME
```
Command to edit the configuration file
```
sudo nano /etc/mosquitto/mosquitto.conf
```
Add the following line at the top
```
per_listener_settings true
```
Add the following three lines to allow connection for authenticated users and tell Mosquitto where the username/password file is located
```
allow_anonymous false
listener 1883 0.0.0.0
password_file /etc/mosquitto/passwd
```
![2023-03-11_9-33-36](https://user-images.githubusercontent.com/48780839/224460499-0e7bfe80-c568-46de-a390-46ba3944bf07.png)

Restart Mosquitto
```
sudo systemctl restart mosquitto
```
Check status
```
sudo systemctl status mosquitto
```
Test mosquitto_sub 
```
mosquitto_sub -h localhost -t testTopic -u user -P pass
```
Test mosquitto_pub 
```
mosquitto_pub -h localhost -t testTopic -p porthost -m "Hello, world!" -u user -P pass
```
## (Optional) Taking It Further – MQTT Mosquitto Broker Encrypted Requests
configuration file mosquitto
```
sudo nano /etc/mosquitto/mosquitto.conf
```
Add the next lines to make your default.conf add the Let’s Encrypt certificates.
```
allow_anonymous false
password_file /etc/mosquitto/passwd

listener 1883 localhost

listener 8883
certfile /etc/letsencrypt/live/example.com/cert.pem
cafile /etc/letsencrypt/live/example.com/chain.pem
keyfile /etc/letsencrypt/live/example.com/privkey.pem
```
Remove Mosquitto
```
sudo apt autoremove mosquitto -y & mosquitto-clients -y
sudo apt autoremove mosquitto-clients -y
sudo apt purge mosquitto -y & mosquitto-clients -y
sudo apt purge mosquitto-clients -y
```
