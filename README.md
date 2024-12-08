---

# **Crear Máquina Virtual CentOS en Fedora**

## Descripción
Este proyecto proporciona una guía paso a paso para crear una máquina virtual CentOS en Fedora utilizando herramientas de virtualización como KVM, libvirt, y virt-install. Los comandos están diseñados para ser ejecutados directamente desde la línea de comandos.

---

## **Repositorio**
**Nombre sugerido del repositorio**: `crear-maquina-virtual-centos-en-fedora`

---

## **Pasos para Crear la Máquina Virtual**

### **1. Verificar Soporte de Virtualización**
```bash
egrep -c '(vmx|svm)' /proc/cpuinfo
lsmod | grep kvm
```

---

### **2. Instalar Herramientas de Virtualización**
```bash
sudo dnf install -y qemu-kvm libvirt virt-install bridge-utils virt-manager virt-viewer
sudo systemctl enable --now libvirtd
sudo systemctl status libvirtd
```

---

### **3. Descargar la Imagen ISO de CentOS Stream**
```bash
wget https://mirror.rabisu.com/centos/8-stream/isos/x86_64/CentOS-Stream-8-20240520.0-x86_64-dvd1.iso -P /var/lib/libvirt/images/
```

---

### **4. Crear la Máquina Virtual**
```bash
sudo virt-install \
--name centos_vm \
--ram 2048 \
--vcpus 2 \
--disk size=20,path=/var/lib/libvirt/images/centos_vm.qcow2,format=qcow2 \
--os-variant centos8 \
--cdrom /var/lib/libvirt/images/CentOS-Stream-8-20240520.0-x86_64-dvd1.iso \
--network network=default \
--graphics spice
```

---

### **5. Solucionar Problemas de Permisos**
Si aparece un error de permisos, usa los siguientes comandos para corregirlo:

```bash
sudo chmod +x /home/jimenezrosa
sudo chmod +x /home/jimenezrosa/Documents
sudo chmod +r /var/lib/libvirt/images/CentOS-Stream-8-20240520.0-x86_64-dvd1.iso
```

---

### **6. Instalar `virt-viewer`**
```bash
sudo dnf install -y virt-viewer
```

---

### **7. Administrar la Máquina Virtual**
#### Listar máquinas virtuales:
```bash
virsh list --all
```

#### Iniciar la máquina virtual:
```bash
virsh start centos_vm
```

#### Conectarse a la consola gráfica:
```bash
virt-viewer --connect qemu:///system centos_vm
```

#### Conectarse a la consola de texto:
```bash
virsh console centos_vm
```

#### Apagar la máquina virtual:
```bash
virsh shutdown centos_vm
```

#### Eliminar la máquina virtual:
```bash
virsh undefine centos_vm
sudo rm /var/lib/libvirt/images/centos_vm.qcow2
```

---

## **Autor**
**José Alejandro Jiménez Rosa**  
Administrador de Bases de Datos, Profesor y Desarrollador.

---

