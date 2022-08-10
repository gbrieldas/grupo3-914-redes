# Roteiro de Configuração e Execução

## Objetivo:
* Exemplificar o passo a passo das etapas realizadas para a configuração e execução do ambiente de rede virtualizada, desde a criação da VMs até as tentativas de comunicação entre as unidades da rede virtualizada, com os testes de Ping e SSH.

## Criação das VMs

### Criação de Diretórios
#### Criação dos diretórios que comportaram a imagem OVA e a VMs.
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

### Baixar a imagem OVA do Ubuntu Server
* Baixar a imagem ``ubuntu-22.04-live-server-amd64.iso`` do PC do Professor Alaelson para o diretório ``/labredes/images/original``:
```
scp aluno@192.168.101.10:~/Public/iso-images/ubuntu-server-mini.ova /labredes/images/original
```

### Instalar o Virtualbox Extension Pack
* Instalar o pacote para a extensão do VirtualBox:
```
sudo apt install virtualbox-ext-pack
```

### Criação e Configuração das VMs no VirtualBox
#### Nesta etapa criamos todas as 8 VMs distribuídas nos 4 PCs.
* Importamos o arquivo OVA a partir da opção ``Importar Appliance``; e
* Definimos o diretório ``/VM/914/Gabriel``, no qual a VM foi salva.

## Configuração das VMs

### Inicialização das VMs
* Logar com o usuário ``administrador`` com a senha ``adminifal``.

### Instalação das ferramentas de rede nas VMS
```
sudo apt install net-tools -y
```

## Configuração da Interface de Rede

### Configurar o IP Estático na Interface de Rede
* Editar o arquivo YAML do Ubuntu, neste cado o ``01-netcfg.yaml``:
```
sudo nano /etc/netplan/01-netcfg.yaml
```

<p><center> Configuração da Interface de Rede das VMs do PC1 </center></p>   
   <img src="imagens/gabriel/netplan.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>
  
<br>

<p><center> Configuração da Interface de Rede das VMs do PC2 </center></p>   
   <img src="imagens/gabriel/netplan.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>
  
<br>

<p><center> Configuração da Interface de Rede das VMs do PC3 </center></p>   
   <img src="imagens/gabriel/netplan.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>
  
<br>

<p><center> Configuração da Interface de Rede das VMs do PC4 </center></p>   
   <img src="imagens/gabriel/netplan.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>
  
* Aplicando as configuraçães:
```
sudo netplan apply
```
 
* Configuração da Interface de Rede das VMs através do ``ifconfig -a``:

<p><center> Configuração da Interface de Rede das VM1 do PC1 </center></p>   
   <img src="imagens/luiza/ifconfig.png" alt=""
	title="ifconfig -a"/>
  
<br>

<p><center> Configuração da Interface de Rede das VM1 do PC3 </center></p>   
   <img src="imagens/luiza/ifconfig.png" alt=""
	title="ifconfig -a"/>
  
<br>

<p><center> Configuração da Interface de Rede das VM2 do PC3 </center></p>   
   <img src="imagens/luiza/ifconfig.png" alt=""
	title="ifconfig -a"/>
  
<br>

<p><center> Configuração da Interface de Rede das VM2 do PC4 </center></p>   
   <img src="imagens/luiza/ifconfig.png" alt=""
	title="ifconfig -a"/>

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
