# Roteiro de Configuração e Execução

## Objetivo:
* Exemplificar o passo a passo das etapas realizadas para a configuração e execução do ambiente de rede virtualizada, desde a criação da VMs até as tentativas de comunicação entre as unidades da rede virtualizada, com os testes de Ping e SSH.

## Criação das VMs

### Criação de Diretórios
#### Criação dos diretórios que comportaram a imagem OVA e a VMs.
* Logar no usuário ``redes``:
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
sudo mkdir <Estudante>
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
* Definimos o diretório ``/VM/914/<Estudante>``, no qual a VM foi salva.

## Configuração das VMs

### Inicialização das VMs
* Logar com o usuário ``administrador`` com a senha ``adminifal``.

### Instalação das ferramentas de rede nas VMS
```
sudo apt install net-tools -y
```

## Configuração da Interface de Rede

```
------------------------------------------------------------------------------------------------------------
|  DESCRICAO  |       IP         |      hostname     |               FQDN               |      aliase      |
------------------------------------------------------------------------------------------------------------
| VM1-PC1     | 192.168.14.34    |   srv-vm1-pc1     | vm01-pc1.grupo3-914.ifalara.net  |       vpn        |
| VM2-PC1     | 192.168.14.35    |   srv-vm2-pc1     | vm02-pc1.grupo3-914.ifalara.net  |       mail       |
| VM1-PC2     | 192.168.14.36    |   srv-vm1-pc2     | vm01-pc2.grupo3-914.ifalara.net  |       www        |
| VM2-PC2     | 192.168.14.37    |   srv-vm2-pc2     | vm02-pc2.grupo3-914.ifalara.net  |       file       |
| VM1-PC3     | 192.168.14.38    |   srv-vm1-pc3     | vm01-pc3.grupo3-914.ifalara.net  |       sql        |
| VM2-PC3     | 192.168.14.39    |   srv-vm2-pc3     | vm02-pc3.grupo3-914.ifalara.net  |       mint       |
| VM1-PC4     | 192.168.14.40    |   srv-vm1-pc4     | vm01-pc4.grupo3-914.ifalara.net  |       beans      |
| VM2-PC4     | 192.168.14.41    |   srv-vm2-pc4     | vm02-pc4.grupo3-914.ifalara.net  |       url        |
------------------------------------------------------------------------------------------------------------
```

## SSH-Server

### Atribuindo nome aos servidores ``hostname``, seguindo a tabela das VMs:
```
sudo hostnamectl set-hostname <hostname>
```

<p><center> Definindo o nome do hostname da VM1 e VM2 do PC1 </center></p>   
   <img src="imagens/Luiza/host.png" alt=""
	title="Definindo o nome do hostname"/>

<p><center> Definindo o nome do hostname da VM1 e VM2 do PC2 </center></p>   
   <img src="imagens/ty/hostnamety.png" alt=""
	title="Definindo o nome do hostname"/>

<p><center> Definindo o nome do hostname da VM1 e VM2 do PC3 </center></p>   
   <img src="imagens/miguel/sudohostname.png" alt=""
	title="Definindo o nome do hostname"/>

<p><center> Definindo o nome do hostname da VM1 e VM2 do PC4 </center></p>   
   <img src="imagens/gabriel/hostname.png" alt=""
	title="Definindo o nome do hostname"/>

### Instalando o servidor SSH
#### Nesta etapa instalamos e atualizamos as definições e versões de pacotes/bibliotecas dos repositórios do ubuntu, instalamos o SSH Server, verificamos os status das portas e o funcionamento de Firewall.
* Atualizando os pacotes com as definições e versões:
```
sudo apt update
sudo apt upgrade -y
```
* Instalando o SSH Server:
```
sudo apt-get install openssh-server
```
* Verificando o status das portas do sistema:
```
netstat -an | grep LISTEN.
```

* Configurando o Firewall:
```
sudo ufw allow ssh
sudo ufw enable
```

### Configurar o IP Estático na Interface de Rede
* Editar o arquivo YAML do Ubuntu, neste cado o ``01-netcfg.yaml``:
```
sudo nano /etc/netplan/01-netcfg.yaml
```

<p><center> Configuração da Interface de Rede das VMs do PC1 </center></p>   
   <img src="imagens/Luiza/IPs.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>

<p><center> Configuração da Interface de Rede das VMs do PC2 </center></p>   
   <img src="imagens/ty/NETCONFIGTY.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>

<p><center> Configuração da Interface de Rede das VMs do PC3 </center></p>   
   <img src="imagens/miguel/sudoNetplan.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>

<p><center> Configuração da Interface de Rede das VMs do PC4 </center></p>   
   <img src="imagens/gabriel/netplan.png" alt=""
	title="Arquivo 01-netcfg.yaml"/>
  
* Aplicando as configuraçães:
```
sudo netplan apply
```
 
* Configuração da Interface de Rede das VMs através do ``ifconfig -a``:

<p><center> Configuração da Interface de Rede das VM1 e VM2 do PC1 </center></p>   
   <img src="imagens/Luiza/ifconfig.png" alt=""
	title="ifconfig -a"/>

<p><center> Configuração da Interface de Rede as VM1 e VM2 do PC2 </center></p>   
   <img src="imagens/ty/IFCONFIG.png" alt=""
	title="ifconfig -a"/>

<p><center> Configuração da Interface de Rede as VM1 e VM2 do PC3 </center></p>   
   <img src="imagens/miguel/ifconfig.png" alt=""
	title="ifconfig -a"/>

<p><center> Configuração da Interface de Rede as VM1 e VM2 do PC4 </center></p>   
   <img src="imagens/gabriel/ifconfig.png" alt=""
	title="ifconfig -a"/>

### Configurando a Placa de Rede para Modo Bridge:
* Nesta etapa configuramos a placa de redes no Adaptador 1 em todas as VMs para o Modo Bridge, assim como a imagem abaixo mostra:
* Não esqueça de atualizar o endereço MAC!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

<p><center> Configurando a Placa de Rede para Modo Bridge na VM1 e VM2 do PC1 </center></p>   
   <img src="imagens/Luiza/modo bridge - vm1.png" alt=""
	title="Modo Bridge"/>
   <img src="imagens/Luiza/modo bridge - vm2.png" alt=""
	title="Modo Bridge"/> 
	
<p><center> Configurando a Placa de Rede para Modo Bridge na VM1 e VM2 do PC2 </center></p>   
   <img src="imagens/ty/MODOBRIDGE.png" alt=""
	title="Modo Bridge"/>
   <img src="imagens/ty/MODOBRIDGE.png" alt=""
	title="Modo Bridge"/> 

<p><center> Configurando a Placa de Rede para Modo Bridge na VM1 e VM2 do PC3 </center></p>   
   <img src="imagens/miguel/v1modobrigde.png" alt=""
	title="Modo Bridge"/>
   <img src="imagens/miguel/vm2mobrigde.png" alt=""
	title="Modo Bridge"/> 

<p><center> Configurando a Placa de Rede para Modo Bridge na VM1 e VM2 do PC2 </center></p>   
   <img src="imagens/gabriel/modo_bridge-VM1.png" alt=""
	title="Modo Bridge"/>
   <img src="imagens/gabriel/modo_bridge-VM2.png" alt=""
	title="Modo Bridge"/>

## Criacão dos usuários nas VMs
### Cada VM possui o usuário administrador, então criamos em cada VM mais 4 usuários com os nomes dos integrantes do grupo.
* Para isso usamos o ``sudo adduser <usuario>`` de acordo com a tabela abaixo:

```
-------------------------------------------------------------------------------------------------
|  VM1-PC1  |  VM2-PC1  |  VM1-PC2  |  VM2-PC2  |  VM1-PC3  |  VM2-PC3  |  VM1-PC4  |  VM2-PC4  |
-------------------------------------------------------------------------------------------------
|   luiza   |   luiza   |   luiza   |   luiza   |   luiza   |   luiza   |   luiza   |   luiza   |
|  rityelle |  rityelle |  rityelle |  rityelle |  rityelle |  rityelle |  rityelle |  rityelle |
|   miguel  |   miguel  |   miguel  |   miguel  |   miguel  |   miguel  |   miguel  |   miguel  |
|  gabriel  |  gabriel  |  gabriel  |  gabriel  |  gabriel  |  gabriel  |  gabriel  |  gabriel  |
-------------------------------------------------------------------------------------------------
```

* Para visualizar os usuários criados, usamos o comando ``getent passwd``

<p><center> Usuários criados nas VM1 e VM2 do PC1 </center></p>   
   <img src="imagens/Luiza/usergetent.png" alt=""
	title="getent passwd"/>

<p><center> Usuários criados nas VM1 e VM2 do PC2 </center></p>   
   <img src="imagens/ty/usuarios.png" alt=""
	title="getent passwd"/>

<p><center> Usuários criados nas VM1 e VM2 do PC3 </center></p>   
   <img src="imagens/miguel/usuarios.png" alt=""
	title="getent passwd"/>

<p><center> Usuários criados nas VM1 e VM2 do PC4 </center></p>   
   <img src="imagens/gabriel/usuariosgab.png" alt=""
	title="getent passwd"/>

## Configurando o serviço de nomes estático
```
------------------------------------------------------------------------------------------------------------
|  DESCRICAO  |       IP         |      hostname     |               FQDN               |      aliase      |
------------------------------------------------------------------------------------------------------------
| VM1-PC1     | 192.168.14.34    |   srv-vm1-pc1     | vm01-pc1.grupo3-914.ifalara.net  |       vpn        |
| VM2-PC1     | 192.168.14.35    |   srv-vm2-pc1     | vm02-pc1.grupo3-914.ifalara.net  |       mail       |
| VM1-PC2     | 192.168.14.36    |   srv-vm1-pc2     | vm01-pc2.grupo3-914.ifalara.net  |       www        |
| VM2-PC2     | 192.168.14.37    |   srv-vm2-pc2     | vm02-pc2.grupo3-914.ifalara.net  |       file       |
| VM1-PC3     | 192.168.14.38    |   srv-vm1-pc3     | vm01-pc3.grupo3-914.ifalara.net  |       sql        |
| VM2-PC3     | 192.168.14.39    |   srv-vm2-pc3     | vm02-pc3.grupo3-914.ifalara.net  |       mint       |
| VM1-PC4     | 192.168.14.40    |   srv-vm1-pc4     | vm01-pc4.grupo3-914.ifalara.net  |       beans      |
| VM2-PC4     | 192.168.14.41    |   srv-vm2-pc4     | vm02-pc4.grupo3-914.ifalara.net  |       url        |
------------------------------------------------------------------------------------------------------------
```
* Editando os arquivo /etc/hosts conforme as definições da Tabela acima:
```
sudo nano /etc/hosts
```

<p><center> Arquivo /etc/hosts da VM1 e VM2 do PC1 </center></p>   
   <img src="imagens/Luiza/nomes estaticos.png" alt=""
	title="/etc/hosts"/>

<p><center> Arquivo /etc/hosts da VM1 e VM2 do PC2 </center></p>   
   <img src="imagens/ty/etchosts.png" alt=""
	title="/etc/hosts"/>


<p><center> Arquivo /etc/hosts da VM1 e VM2 do PC3 </center></p>   
   <img src="imagens/miguel/hosts2.png" alt=""
	title="/etc/hosts"/>

<p><center> Arquivo /etc/hosts da VM1 e VM2 do PC4 </center></p>   
   <img src="imagens/gabriel/hosts.png" alt=""
	title="/etc/hosts"/>

## Configuração do HostOnly
### Configurando o acesso remoto às uma VM da rede pelo terminal do PC via ssh

### Configurando o HostOnly na VirtualBox
* Nesta etapa criamos uma interface no computador para comunicação entre o Host (PC) e a VM.
* Clicar em ``Arquivo``->``Host Network Manager``:
<p><center> Virtualbox Network Manager </center></p>   
   <img src="imagens/hostonly/adaptador.png" alt=""
	title="Virtualbox Network Manager"/>

<p><center> Configurando o servidor DHCP no adaptador VBoxNet0 </center></p>   
   <img src="imagens/hostonly/dhcp.png" alt=""
	title="Configurando o servidor DHCP no adaptador VBoxNet0"/>

* Verificando a configuração das interfaces e a existência da interface ``vboxnet0`` usando o ``Terminal`` do PC:
```
ifconfig -a       # verifique a existência da interface ``vboxnet0``
```
<p><center> Verificando a existência da interface criada no ``Terminal`` do PC1 </center></p>   
   <img src="imagens/hostonly/dhcp.png" alt=""
	title="Configurando o servidor DHCP no adaptador VBoxNet0"/>

* Adicionar um adaptador (HostOnly) na VM1 no PC1 para dar acesso a ela via rede pelo ``Terminal`` do PC:
<p><center> Adapatador 2 em modo Host-Only </center></p>   
   <img src="imagens/hostonly/adaptador2.png" alt=""
	title="Adaptador 2 da VM1 do PC1"/>

### Configurações da Interface na VM1 do PC1 para o servidor DHCP
* Ative o DHCP para o Adaptador 2 (enp0s8):
```
sudo nano /etc/netplan/01-netcfg.yaml
```
<p><center> Editando o arquivo 01-netcfg.yaml da VM1 do PC1 </center></p>   
   <img src="imagens/hostonly/netplan.png" alt=""
	title="01-netcfg.yaml"/>	

* Ativando as configurações:
```
sudo netplan apply
```

* Verificando se o IP pegou na nova interface de rede:
```
ifconfig -a
```
<p><center> IFCONFIG da VM1 do PC1 </center></p>   
   <img src="imagens/hostonly/ifconfighostonly.png" alt=""
	title="ifconfig -a"/>

## Fiação
<img src="imagens/conexões/IMG_20220826_080233.jpg" alt=""
	title="ifconfig -a"/>
<img src="imagens/conexões/IMG_20220826_080238.jpg" alt=""
	title="ifconfig -a"/>
<img src="imagens/conexões/IMG_20220826_080243.jpg" alt=""
	title="ifconfig -a"/>
<img src="imagens/conexões/IMG_20220826_080436.jpg" alt=""
	title="ifconfig -a"/>

## Acesso SSH
* Instalando o SSH Server no ``Terminal``:
```
sudo apt-get install openssh-server
```

* Acessando a VM1 do PC1 a partir do ``Terminal``:
```
ssh administrador@192.168.56.100
```
<p><center> Acesso SSH </center></p>   
   <img src="imagens/comunicações/hostonly.png" alt=""
	title="ssh administrador@192.168.56.100"/>

## Testes de Ping
* Estabelecendo conexões entre as VMs da rede:
```
ping <ip>
```

<p><center> Teste de Ping entre a VM1 e VM2 do PC1 </center></p>   
   <img src="imagens/comunicações/vm1-pc1 vm2-pc1.png" alt=""
	title="ping 192.168.14.35"/>
<p><center> Teste de Ping entre a VM1 do PC1 para a VM1 do PC2 </center></p>   
   <img src="imagens/comunicações/vm1-pc1 vm1-pc2.png" alt=""
	title="ping 192.168.14.36"/>
<p><center> Teste de Ping entre a VM1 do PC1 para a VM2 do PC2 </center></p>   
   <img src="imagens/comunicações/vm1-pc1 vm2-pc2.png" alt=""
	title="ping 192.168.14.37"/>
<p><center> Teste de Ping entre a VM1 do PC1 para a VM1 do PC3 </center></p>   
   <img src="imagens/comunicações/vm1-pc1 vm1-pc3.png" alt=""
	title="ping 192.168.14.38"/>
<p><center> Teste de Ping entre a VM1 do PC1 para a VM2 do PC3 </center></p>   
   <img src="imagens/comunicações/vm1-pc1 vm2pc3.png" alt=""
	title="ping 192.168.14.39"/>
<p><center> Teste de Ping entre a VM1 do PC1 para a VM2 do PC4 </center></p>   
   <img src="imagens/comunicações/vm1-pc1 vm2-pc4.png" alt=""
	title="ping 192.168.14.41"/>
<p><center> Teste de Ping entre a VM1 do PC2 para a VM1 do PC4 via usuário Gabriel</center></p>   
   <img src="imagens/Luiza/Captura de tela de 2022-09-02 10-51-19.png" alt=""/>
<p><center> Acesso SSH entre o usuario Luiza da VM2 do PC3 para o usuario Gabriel da VM1 do PC2</center></p>   
   <img src="imagens/Luiza/Captura de tela de 2022-09-02 10-51-07.png" alt=""/>
<p><center> Acesso SSH entre o usuario Luiza da VM2 do PC2 para o usuario Luiza da VM2 do PC3 via aliase mint</center></p>   
   <img src="imagens/Luiza/Captura de tela de 2022-09-02 10-50-43.png" alt=""/>
<p><center> Acesso SSH entre o usuario Luiza da VM2 do PC3 para o usuario Gabriel da VM1 do PC2 via hostname srv-vm1-pc2</center></p>   
   <img src="imagens/Luiza/Captura de tela de 2022-09-02 10-50-43.png" alt=""/>
<p><center> cat /etc/hosts </center></p> 
   <img src="imagens/Luiza/Captura de tela de 2022-09-02 10-50-43.png" alt=""/>
