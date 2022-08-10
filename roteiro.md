# Roteiro de Configuração e Execução

## Objetivo:
* Exemplificar o passo a passo das etapas realizadas para a configuração e execução do ambiente de rede virtualizada, desde a criação da VMs até as tentativas de comunicação entre as unidades da rede virtualizada, com os testes de Ping e SSH.

## Criação das VMs

### Criação de Diretórios
#### Criação dos diretórios que comportaram a imagem ISO e a VMs.
* Logar no usuário ``redes`` com a senha ``admin@Lab92``:
```
su redes
```
* Criar a pasta ``labredes`` no diretório raiz ``/``:
```
cd /
sudo mkdir labredes
```
* Criar os diretórios de ``labredes``. Neste caso, são: ``images/original`` e o ``VM/914/<Estudante>``:
```
cd /labredes
sudo mkdir images
cd images
sudo mkdir original

cd /labredes
sudo mkdir VM
cd VM
sudo mkdir 914
cd 914
sudo mkdir Gabriel
```

### Usuários e Permissões
#### Concessão de permissões para os diretórios, arquivos e pastas.
* Adicionar o usuário ``aluno`` ao grupo ``redes``:
```
sudo usermod -aG redes aluno
```
* Modificar as permissões do diretório ``/labredes``:
```
sudo chown -R nobody:nogroup /labredes
sudo chgrp -R redes /labredes
sudo chmod -R 771 /labredes
```

### Baixar a imagem ISO do Ubuntu Server
* Baixar a imagem ``ubuntu-22.04-live-server-amd64.iso`` do PC do Professor Alaelson:
```
scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-22.04-live-server-amd64.iso /labredes/images/original
```

### Instalar o Virtualbox Extension Pack
* Instalar o pacote para a extensão do VirtualBox:
```
sudo apt install virtualbox-ext-pack
```


## Configuração das VMs

### Update/Upgrade

### sudo apt-get install openssh-server

### Staus da Porta 22 (netstat -an | grep LISTEN.)

### Firewall (sudo ufw allow ssh.) (sudo ufw enable)

### sudo nano /etc/netplan/01-netcfg.yaml

### sudo hostnamectl set-hostname srv-vm1-pc1

### sudo nano /etc/hosts

### adduser
* Em cada vm deve ter o usuário administrador e os usuários com os nomes dos integrantes do grupo.

### Modo Bridge

### Criação do HostOnly

## Testes dde Ping e Acessso SSH

###  Resultados dos testes de Ping e acesso SSH utilizando os usuários criados nas VMs e os nomes dos hosts.
