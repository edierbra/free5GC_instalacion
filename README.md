# free5GC instalacion

## Por: Edier Dario Bravo Bravo

# Instalación

## A. Requisitos previos

1. Versión del núcleo de Linux

    - Para usar el elemento UPF, debe usar la versión 5.0.0-23-generico 5.4.xdel kernel de Linux. free5gc usa el [módulo del kernel gtp5g]
    (https://github.com/free5gc/gtp5g), que ha sido probado y compilado solo con esas versiones del kernel. Si instaló Ubuntu 20.04, la versión parece 5.4.x. Para determinar la versión del kernel de Linux que está utilizando:

    ```bash
    $ uname -r
    5.4.0-65-generic
    ```

    No podrá ejecutar la mayoría de las [pruebas](https://github.com/free5gc/free5gc/wiki/Test) en la sección Prueba a menos que implemente un UPF.

2. Version Golang

    - Como se indicó anteriormente, free5gc está construido y probado con Go 1.17.8

    Como se indicó anteriormente, free5gc está construido y probado con Go 1.17.8

    - Para verificar la versión de Go en su sistema, desde un símbolo del sistema:

    ```bash
    go version
    ```

    - Si tiene una versión de Go instalada, elimine la versión existente e instale Go 1.17.8:

    ```bash
    # this assumes your current version of Go is in the default location
    sudo rm -rf /usr/local/go

    wget https://dl.google.com/go/go1.17.8.linux-amd64.tar.gz

    sudo tar -C /usr/local -zxvf go1.17.8.linux-amd64.tar.gz
    ```

    - Si Go no está instalado en su sistema
        
    ```bash
    wget https://dl.google.com/go/go1.17.8.linux-amd64.tar.gz
    sudo tar -C /usr/local -zxvf go1.17.8.linux-amd64.tar.gz
    mkdir -p ~/go/{bin,pkg,src}
    # The following assume that your shell is bash
    echo 'export GOPATH=$HOME/go' >> ~/.bashrc
    echo 'export GOROOT=/usr/local/go' >> ~/.bashrc
    echo 'export PATH=$PATH:$GOPATH/bin:$GOROOT/bin' >> ~/.bashrc
    echo 'export GO111MODULE=auto' >> ~/.bashrc
    source ~/.bashrc
    ```

    Más información e instrucciones de instalación `golang` están disponibles en el [sitio oficial de golang](https://go.dev/doc/install).

## B. Maquina virtual

1. Se instala ubuntu 20.04 en VirtualBox

    Se verifican los requisitos previos

2. Se crea un snapshots a la maquina y se hace un clon con nombre `free5gc` que esta vinculado a dicha maquina.

    ![snapshots](https://github.com/edierbra/free5GC_instalacion/blob/main/images/snapshots.png?raw=true)

    ![clone parte 1](https://github.com/edierbra/free5GC_instalacion/blob/main/images/clone.png?raw=true)

    ![clone parte 2](https://github.com/edierbra/free5GC_instalacion/blob/main/images/clone2.png?raw=true)

3. Cambiando IP

- Se edita el archivo /etc/hostname

    ![hostname](https://github.com/edierbra/free5GC_instalacion/blob/main/images/hostname.png?raw=true)

- Se edita el archivo /etc/hosts

    ![hosts](https://github.com/edierbra/free5GC_instalacion/blob/main/images/hosts.png?raw=true)

- Se ingresa al directorio `/etc/netplan` y se modifica el archivo alojado ahi. La direccion ip corresponde a la maquina clonada (la inicial)

    ![netplan](https://github.com/edierbra/free5GC_instalacion/blob/main/images/netplan.png?raw=true)

- Se ejecuta el siguiente comando para aplicar temporalmente la nueva configuración de red y verificar que todo funciona correctamente antes de aplicarla permanentemente, luego debmos precionar ENTER para aplicar los cambios

    ```bash
    sudo netplan try
    ```

- Luego se ejecuta el siguiente comando para aplicar la configuración de red creada en el archivo de configuración de Netplan.

    ```bash
    sudo netplan apply
    ```

Con esto al ejecutar `ifconfig` se vera que la IP de la interfaz ethernet **enp0s8** ha sido midificada a `192.168.56.101`

Y al ingresar por ssh a `ssh 198.168.56.101 -l ubuntu1`, debe aparecer de la siguiente manera

![netplan](https://github.com/edierbra/free5GC_instalacion/blob/main/images/ssh1.png?raw=true)

si no aparece con el nombre **fre5gc** reiniciar la maquina o ejecutar el siguiente comando

```bash
sudo shutdown -r now
```










