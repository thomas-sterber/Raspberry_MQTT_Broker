# Raspberry MQTT Broker Install Guide

## update Raspberry
    sudo apt-get update
    sudo apt-get upgrade

## Install Mosquitto
    sudo apt-get install mosquitto -y
    sudo apt-get install mosquitto-clients

## Configure Mosquitto.
    sudo vim /etc/mosquitto/mosquitto.conf

Copy and paste the following:

    pid_file /var/run/mosquitto.pid
    
    persistence true
    persistence_location /var/lib/mosquitto/
    
    log_dest file /var/log/mosquitto/mosquitto.log

    allow_anonymous false
    password_file /etc/mosquitto/pwfile
    
    listener 1883

write file and exit vim

    :wq!

## Setup Mosquitto credentials
    sudo mosquitto_passwd -c /etc/mosquitto/pwfile meraki
    (password: meraki123#)

## Test the Mosquitto broker 

### subscribing to a topic (mqtt/test)
    mosquitto_sub -h localhost -d -u meraki -P meraki123# -t mqtt/test
    
### publish message to the topic (mqtt/test) using a second terminal
    mosquitto_pub -h localhost -t mqtt/test -m "hello world"
    
    
## MQTT commands
### start, stop, restart, status
    sudo systemctl status mosquitto
    sudo systemctl restart mosquitto
    sudo systemctl stop mosquitto
    sudo systemctl start mosquitto
    
### stop MQTT and start in debug mode
    sudo systemctl stop mosquitto
    mosquitto -p 1883 -v
    CRTL+C to end


