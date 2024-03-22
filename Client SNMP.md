# Configuration du client
Installer les paquets snmp et snmpd:
``` shell
sudo apt update
sudo apt-get install snmpd snmp
```
Fichier snmp.conf -> Configuration des MIBS à utiliser  
Fichier snmpd.conf -> Configuration du démon snmpd


https://www.zabbix.com/documentation/6.4/fr/manual/config/items/itemtypes/snmp?hl=SNMP

## Configuration "miniale" de /etc/snmp/snmp.conf
Au minimum votre fichier snmp.conf devra contenir:
 - `agentAddress udp:161,udp6:[::1]:161` 
 - `syslocation Mon_Serveur` Emplacement système (syslocation) :
 - `syscontact admin@mondomaine.lab` Un mail d'adminsitrateur
 - `rocommunity  public default` 


Faire en sorte que le daemon snmpd soit à l'écoute sur le réseau:
``` shell
sudo nano /etc/snmp/snmpd.conf
```
Faite les modification nécessaires  

Redémarrez le service SNMPD et vérifiez son status
``` shell
sudo systemctl restart snmpd
sudo systemctl status snmpd
```

Vérifiez les ports et les service à l'écoute :
``` shell
sudo netstat -tulpn
```
Vous devevriez voir ces lignes. Indique que daemon snmpd est maintenant a l'écoute sur le port 161 sur les réseaux IPv4 et IPv6;
``` shell
udp        0      0 0.0.0.0:161             0.0.0.0:*                           123863/snmpd        
udp6       0      0 ::1:161                 :::*                                123863/snmpd  
```
Affichez la MIB du client  
``` shell
snmpwalk -c public -v 2c localhost
```

## Testez la communication entre votre agent et le manager
Depuis le client  
``` shell
snmpstatus -c public <IP DU MANAGER>
```

Depuis le manager  
``` shell
snmpstatus -c public <IP DU CLIENT>
```
# Depuis l'interface Zabbix
## Créez un hote
## Créer un élément (item)
