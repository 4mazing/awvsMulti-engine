FROM ubuntu

RUN mkdir /awvs_data/
WORKDIR /awvs_data/

# RUN apt-get update -y
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y sudo systemd net-tools cron curl
RUN apt-get install -y libxdamage1 libgtk-3-0 libasound2 libnss3 libxss1 libx11-xcb1

COPY acunetix12.sh .
RUN chmod +x acunetix12.sh
RUN sh -c '/bin/echo -e "\nyes\n"| ./acunetix12.sh --engineonly'
# RUN sh -c '/bin/echo -engine "\nyes\nadministrator\nadmin@a.com\nadmin\nadmin\n"| ./acunetix12.sh'

WORKDIR /home/acunetix/.acunetix/v_190902105/scanner
COPY patch .
COPY patch.dat .

USER root
RUN chmod u+x ./patch
RUN chmod u+x /home/acunetix/.acunetix/start.sh
RUN sh -c '/bin/echo -e "\n1111-1111-1111-1111\nawvs\nadmin\n13333333331\nadmin@qq.com\nchina\n99999\n99999"| ./patch'

USER acunetix
# CMD update-alternatives --install /usr/bin/python python /usr/bin/python3 1
CMD /home/acunetix/.acunetix/start.sh

EXPOSE 3443
