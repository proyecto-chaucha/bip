# bip
Análisis de funcionamiento de la Tarjeta BIP!

El presente estudio se basó en información de público conocimiento que fue 
recopilada entre los años 2014 y la actualidad, y su publicación y distribución 
se realizó sólo con fines educacionales.

Proyecto Chaucha no se hace responsable ni avala ningun tipo de acción
realizada en base a la información presente en este repositorio.

## libnfc

```
sudo apt-get update
sudo apt-get -y install subversion autoconf debhelper flex libusb-dev libpcsclite-dev libpcsclite1 libccid pcscd pcsc-tools libpcsc-perl libusb-1.0-0-dev libtool libssl-dev cmake checkinstall
wget https://github.com/nfc-tools/libnfc/releases/download/libnfc-1.7.0-rc7/libnfc-1.7.0-rc7.tar.gz
tar -xvzf libnfc-1.7.0-rc7.tar.gz
cd libnfc-1.7.0-rc7
./configure --with-drivers=acr122_usb
make
sudo make install
```

## Blacklist 


```
sudo nano /etc/modprobe.d/blacklist-libnfc.conf

```

Agregar estas dos lineas al archivo blacklist-libnfc.conf


```
blacklist pn533
blacklist nfc
```

y despues ejecutar modprobe


```
sudo modprobe -r pn533 nfc
```

## mfterm

```
cd mfterm
autoreconf -is
./configure
make
```

## Leer tarjeta

```
./mfterm
keys load keys.txt
read
print
save tarjeta.dmp
exit
```


## Leer dump
```
cd mfdread
python3 mfdread.py tarjeta.dmp -1
```