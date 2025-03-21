# Instalación de Ansible y Configuración de VM con Terraform

## 1. Instalación de Ansible en Ubuntu

Para instalar Ansible en Ubuntu:

```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

## 2. Creación de la Máquina Virtual en Azure con Terraform


### Pasos para desplegar la VM

1. **Clonar el repositorio donde se encuentra la estructura de la VM**

   ```bash
   git clone https://github.com/jpnino1018/vm-terraform.git
   cd vm-terraform.git
   ```

2. **Nos autenticamos con el cliente de Azure y corremos los siguientes comandos para aplicar la estructura y subir la VM**

   ```bash
   terraform init
   terraform plan
   terraform apply
   ```
   

## 3. Configuración de Ansible para la VM

### Configurar el archivo de hosts

En `inventory/hosts.ini`, se agrega la IP de la VM:

En mi caso:
```
[azure_vm]
51.136.24.86 ansible_user=adminuser ansible_ssh_pass=Password*#123
```


## 4. Ejecución de Playbooks de Ansible

Para instalar Docker en la VM:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/install_docker.yml
```

Para ejecutar el contenedor de Mario Bros:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/run_container.yml
```

Verificar que el contenedor está en ejecución:

```bash
ssh azureadmin@51.136.24.86
sudo docker ps
```


## 5. Acceder a Mario Bros en la VM

Una vez el contenedor está en ejecución, acceder al juego desde el navegador:

```
http://51.136.24.86:8787
```
[![image](https://github.com/jpnino1018/training-ansible/blob/main/mario.png)]



