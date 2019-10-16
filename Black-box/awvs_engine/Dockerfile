FROM ubuntu

RUN mkdir /awvs_data
WORKDIR /awvs_data

# RUN apt-get update -y
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y sudo systemd net-tools cron
RUN apt-get install -y libxdamage1 libgtk-3-0 libasound2 libnss3 libxss1 libx11-xcb1
CMD update-alternatives --install /usr/bin/python python /usr/bin/python3 1

COPY acunetix12.sh .
RUN chmod +x acunetix12.sh
# RUN sh -c '/bin/echo -e "\nyes\n"| ./acunetix12.sh --engineonly'
RUN sh -c '/bin/echo -e "\nyes\nawvsmanagement\nadmin@admin.com\nadmin888?\nadmin888?\n"| ./acunetix12.sh'

WORKDIR /home/acunetix/.acunetix/v_190902105/scanner
COPY patch .
COPY patch.dat .

USER root
RUN chmod +x ./patch
RUN chmod +x /home/acunetix/.acunetix/start.sh

# USER acunetix
RUN sh -c '/bin/echo -e "1111-1111-1111-1111\nawvs12\nadmin\n13333333333\nadmin@admin.com\nawvs12\n9999\n9999\n"| ./patch'
CMD touch /home/acunetix/.acunetix/data/license/wa_data.dat

USER acunetix
CMD /home/acunetix/.acunetix/start.sh

EXPOSE 3443
