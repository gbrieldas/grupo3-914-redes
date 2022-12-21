# Roteiro

su redes

openvpn3 session-start --config vpn914.labredes

ssh admnistrador@10.9.14.1<aluno>

## Configurando o ENS192 nas 4 VMs do grupo 3
  
  sudo hostnamectl set-hostname <hostname>
  
  sudo nano /etc/netplan/00-installer-config.yaml
  
  prints
  
## Configurando o Gateway na VM1
  
  sudo ufw enable
  
  sudo ufw allow ssh
  
  sudo vi /etc/ufw/sysctl.conf
  
  ifconfig -a
