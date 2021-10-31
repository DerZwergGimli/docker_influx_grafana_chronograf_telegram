# Cretae a telegraf container containing python and later install own application
#FROM debian
FROM ubuntu
#ARG DEBIAN_FRONTEND=noninteractive
ENV TZ Europe/Berlin
RUN apt-get update 
RUN apt-get install -y --no-install-recommends apt-utils
RUN apt-get upgrade -y && apt-get install -y python3 python3-pip cron nano
#RUN apk update && apk upgrade && apk add python3 pip3 cron nano
#RUN apk --update add --no-cache g++


RUN python3 -V

RUN pip3 -V

# SETUP CRON

#RUN mkdir /home/python
#ADD Viessmann_API_InfluxDB_Logger/python_viessmannapi.py /home/python/Viessmann_API_InfluxDB_Logger/python_viessmannapi.py
ADD Viessmann_API_InfluxDB_Logger /home/python/Viessmann_API_InfluxDB_Logger
RUN pip3 install -r /home/python/Viessmann_API_InfluxDB_Logger/requirements.txt
#COPY cronjob /etc/cron.d/cronjob
#RUN chmod 0644 /etc/cron.d/cronjob
#RUN crontab /etc/cron.d/cronjob

#CMD cron && tail -f /home/log.log
#CMD cron -l 2 -f
#CMD service cron restart
#CMD /bin/sh

# Add files
ADD runViessmann.sh /runViessmann.sh
ADD watchdog.sh /watchdog.sh
ADD entrypoint.sh /entrypoint.sh
 
RUN chmod +x /runViessmann.sh /watchdog.sh /entrypoint.sh

ENTRYPOINT /entrypoint.sh