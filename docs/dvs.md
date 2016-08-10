#DVS 128

## Instalacion


Crear el archivo Dockerfile con el contenido correspndiente, descargar la carpeta rules y colocarla en la carpeta donde se encuentra el archivo Dockerfile.

### Dockerfile
´´´
FROM java:7
RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install udev
RUN apt-get install subversion
ADD ./rules/65-inilabs.rules /etc/udev/rules.d/65-inilabs.rules
ADD ./rules/66-inilabs_dev.rules /etc/udev/rules.d/66-inilabs_dev.rules
RUN cd /usr/src/
RUN svn checkout https://svn.code.sf.net/p/jaer/code
WORKDIR /usr/src/code/jAER/trunk/
CMD ["udevadm control --reload"]
´´´

Para crear la imagen lo hacemos con el siguiente comando
´´´
docker build -t dvs .
´´´

Cabe destacar que el nombre de la imagen esta puesto como dvs a modo de ilustracion.

Luego para correrlo como contenedor lo podemos hacer con el siguiente comando:
´´´
docker run -d -t -it --net host -v /dev/dri:/dev/dri:rw -v /tmp/.X11-unix:/tmp/.X11-unix:rw -v /dev/snd:/dev/snd --privileged -e DISPLAY=$DISPLAY dvs

´´´

Para correr la imagen como docker-compose lo hacemos de la siguiente manera:

### docker-compose.yml

´´´
version: '2'

services:
  dvs:
    image: dvs
    volumes:
      - ./DVS/:/root/dvs
      - /dev/dri:/dev/dri:rw
      - /tmp/.X11-unix:/tmp/.X11-unix:rw
      - /dev/snd:/dev/snd:rw
    environment:
      - DISPLAY=$DISPLAY
    network_mode: "host"
    privileged: true
    devices:
      - "/dev/ttyUSB0:/dev/ttyUSB0"
    command: ./jAERViewer1.5_linux.sh

´´´

