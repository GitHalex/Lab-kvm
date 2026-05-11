# Laboratorio de KVM practico

1. Instalacion de KVM

```sh
sudo dnf install qemu-kvm libvirt virt-install
# verificar que esta corriendo el sistema
sudo systemctl start libvirtd
sudo systemctl enable libvirtd
sudo systemctl status libvirtd
```

2. Validar requisitos del host

```sh
virt-host-validate
```

![Validacion](imagenes/validacion.png)

3. Configuracion del servidor VNC de qemu

```sh
#Se necesita habilitar el servidor vnc de quemu para que escuche las peticiones en cualquier interfaz de red
sudo vi /etc/libvirt/qemu.conf
#en el archivo descomentamos la opcion de vnc_listen = "0.0.0.0"
sudo systemctl restart libvirtd
#el servidor vnv escucha peticiones el el puerto 5900
# es por eso que se require dar de alta en el firewall
sudo firewall-cmd --add-service=vnc-server --permanent
# recargar las regalas del firewall
sudo firewall-cmd --reload

```

4. Transferir la imagen ISO de Centos yo lo esotoy descargadno directamente en la ubicacion

```sh
# agregar las imagenes iso en la carpeta
/var/lib/libvirt/images

```

5. Creación de una mauina virtual (virt-install)

```sh
# agregar las imagenes iso en la carpeta
sudo virt-install \
--name debian-vm \
--memory 2048 \
--vcpus 2 \
--disk size=10,format=qcow2 \
--cdrom /var/lib/libvirt/images/debian-netinst.iso \
--os-variant debian11 \
--network bridge=virbr0 \
--graphics spice

```

6. Instalacion de alpine como tambien el de debian
7. Componenetes de una maquina virtual en KVM
8. Tipos de redes de KVM
9. Crear una interfaz en modo puente
10. Agregar una nueva red en KVM
