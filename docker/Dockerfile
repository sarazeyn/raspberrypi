# Iot Solution ARM32 docker
FROM python:3.9-slim

# The service name for TML solution
# ARG service_name


# Transactional Machine Learning (TML) with Kafka/Java/Python for ARM 32
# install java
ARG CHIP
ENV CHIP=${CHIP}

#ARG CHIP="ARM32"
#CHIP="ARM64"
#CHIP="AMD64"

#echo "Updating package index files"
RUN apt update
RUN apt install -y wget
RUN apt-get -y install git
RUN apt-get -y install unzip
RUN apt-get -y install vim
RUN apt-get -y install nano


RUN echo "Downloading and Installing TML technologies "
RUN echo "Downloading and Installing VIPER"
RUN mkdir Viper
RUN chmod -R +x Viper
WORKDIR Viper

RUN git clone --depth 1 https://github.com/smaurice101/transactionalmachinelearning.git
RUN echo "*******************Viper for $CHIP**********************"

RUN if [ "$CHIP" = "ARM32" ] ; \
  then \
  unzip transactionalmachinelearning/ARM-Chipset/MAADS-VIPER\ *\ Linux\ ARM.zip && \
  chmod 755 viper-linux-arm ; \
elif [ "$CHIP" =  "ARM64" ] ; \
  then \
  unzip transactionalmachinelearning/ARM64-Chipset/MAADS-VIPER\ *\ Linux\ ARM64.zip && \
  chmod 755 viper-linux-arm64 ; \
elif [ "$CHIP" = "AMD64" ] ; \
  then \
  unzip transactionalmachinelearning/MAADS-VIPER\ *\ Linux\ AMD64.zip && \
  chmod 755 viper-linux-amd64 ; \ 
fi

RUN rm -rf transactionalmachinelearning
WORKDIR /
RUN chmod -R +x Viper

RUN echo "*********************Downloading and Installing VIPERviz Visualization****************"
RUN mkdir Viperviz
RUN mkdir Viperviz/viperviz
RUN mkdir Viperviz/viperviz/views
RUN chmod -R +x Viperviz

WORKDIR Viperviz

RUN git clone --depth 1 https://github.com/smaurice101/transactionalmachinelearning.git

#RUN unzip transactionalmachinelearning/ARM-Chipset/MAADS-VIPERviz\ *\ Linux\ ARM.zip || true
RUN if [ "$CHIP" = "ARM32" ] ; \
  then \
  unzip transactionalmachinelearning/ARM-Chipset/MAADS-VIPERviz\ *\ Linux\ ARM.zip || true ; \
elif [ "$CHIP" = "ARM64" ] ; \
  then \
  unzip transactionalmachinelearning/ARM64-Chipset/MAADS-VIPERviz\ *\ Linux\ ARM64.zip || true ; \
elif [ "$CHIP" = "AMD64" ] ; \
  then \
  unzip transactionalmachinelearning/MAADS-VIPERviz\ *\ Linux\ AMD64.zip || true ; \ 
fi


RUN if [ "$CHIP" = "ARM32" ] ; \
  then \
  chmod 755 viperviz-linux-arm ; \
elif [ "$CHIP" = "ARM64" ] ; \
  then \
  chmod 755 viperviz-linux-arm64 ; \
elif [ "$CHIP" = "AMD64" ] ; \
  then \
  chmod 755 viperviz-linux-amd64 ; \ 
fi

RUN rm -rf transactionalmachinelearning
WORKDIR /
RUN chmod -R +x Viperviz

RUN echo "*********************Downloading and Installing HPDE AutoML********************"
RUN mkdir Hpde
RUN chmod -R +x Hpde
WORKDIR Hpde

RUN git clone --depth 1 https://github.com/smaurice101/transactionalmachinelearning.git

RUN if [ "$CHIP" = "ARM32" ] ; \
  then \
  unzip transactionalmachinelearning/ARM-Chipset/MAADS-HPDE\ *\ Linux\ ARM.zip || true ; \
elif [ "$CHIP" = "ARM64" ] ; \
  then \
  unzip transactionalmachinelearning/ARM64-Chipset/MAADS-HPDE\ *\ Linux\ ARM64.zip || true ; \
elif [ "$CHIP" = "AMD64" ] ; \
  then \
  unzip transactionalmachinelearning/MAADS-HPDE\ *\ Linux\ AMD64.zip || true ; \
fi

RUN if [ "$CHIP" = "ARM32" ] ; \
  then \
  chmod 755 hpde-linux-arm ; \
elif [ "$CHIP" = "ARM64" ] ; \
  then \
  chmod 755 hpde-linux-arm64 ; \
elif [ "$CHIP" = "AMD64" ] ; \
  then \
  chmod 755 hpde-linux-amd64 ; \ 
fi

RUN rm -rf transactionalmachinelearning

RUN echo "Downloading and Installing KAFKA"
WORKDIR /
RUN chmod -R +x Hpde

RUN mkdir Kafka
RUN chmod -R +x Kafka

WORKDIR Kafka

RUN wget -O kafka_2.13-3.0.0.tgz https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz
RUN chmod +x kafka_2.13-3.0.0.tgz

RUN tar xzf kafka_2.13-3.0.0.tgz

RUN export KAFKA_HEAP_OPTS="-Xmx512M -Xms512M"
RUN export PWD=`pwd`
RUN export CHIP="$CHIP"

RUN export PATH="$PATH:$PWD/Kafka/kafka_2.13-3.0.0/bin"

RUN rm -rf kafka_2.13-3.0.0.tgz
WORKDIR /
RUN chmod -R +x Kafka

RUN echo "Install TMUX"
RUN apt -y install tmux
RUN mkdir tmux

RUN echo "Install Mariadb"
RUN apt -y install mariadb-server || true
# sudo mysql_secure_installation
# RUN: sudo mysql -u root
# Execute: SET PASSWORD FOR 'root'@'localhost' = PASSWORD('raspberry'); 
# GRANT ALL PRIVILEGES on *.* to 'root'@'localhost' IDENTIFIED BY 'raspberry'; 
# FLUSH PRIVILEGES;

RUN echo "Replace VIPER.ENV"
RUN git clone --depth 1 https://github.com/smaurice101/raspberrypi.git

RUN chmod -R +x raspberrypi

RUN cp -rf raspberrypi/viper-env-file/viper.env Viper/viper.env
RUN cp -rf raspberrypi/viper-env-file/viper.env Viperviz/viper.env

RUN echo "Copy the IotSolution Scripts"

RUN mkdir IotSolution
RUN cp -rf raspberrypi/iotsolution-scripts-data/* IotSolution/

################# IOT DATA
WORKDIR IotSolution

RUN wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1yRgDYrWnHu74NYX9GMAVDjR10ZyfoZvh' -O IoTData.zip
RUN chmod +x IoTData.zip
RUN unzip IoTData.zip

RUN wget --no-check-certificate 'https://docs.google.com/uc?export=download&id=1_RICecxEZUjuCfm_MxPGwrOXxQ5w179O' -O dsntmlidmain.csv
RUN chmod +x dsntmlidmain.csv
RUN rm -rf IoTData.zip

WORKDIR /

RUN cp -rf raspberrypi/tmux-shell-script/tmux-docker.sh tmux/tmux-docker.sh

RUN cp -rf raspberrypi/iot-dashboard-html/viperviz.zip Viperviz/viperviz.zip
RUN chmod -R +x IotSolution
RUN chmod -R +x Viperviz
RUN chmod -R +x tmux

WORKDIR Viperviz
RUN unzip Viperviz/viperviz.zip || true

WORKDIR /

RUN rm -rf raspberrypi

RUN echo "Installing Java"
RUN apt -y install default-jdk || true

RUN echo "PIP Install TML core packages"
RUN pip install maadstml
RUN pip install requests
RUN pip install nest_asyncio
RUN pip install joblib
RUN pip install asyncio

ENTRYPOINT ["/bin/bash","-c","while true; do sleep 1; done | ./tmux/tmux-docker.sh"]