# Configuration du client
Installer les paquets snmp et snmpd:
``` shell
sudo apt update
sudo apt install snmpd snmp
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
   
Faite les modifications nécessaires  
``` shell
sudo nano /etc/snmp/snmpd.conf
```

Redémarrez le service SNMPD et vérifiez son status
``` shell
sudo systemctl restart snmpd
sudo systemctl status snmpd
```

Vérifiez que le port 161 soit à l'écoute :
``` shell
sudo netstat -tulpn
```
Vous devriez voir ces lignes. Indique que daemon snmpd est maintenant a l'écoute sur le port 161 sur les réseaux IPv4 et IPv6;
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
 1. Depuis le menu de gauche, séletionnez "Surveillance" -> "Hôte"
 2. Cliquez sur le bouton "Créer un hôte" (complètement en haut à droite) ![image](https://github.com/ornech/Supervision-zabbix/assets/101867500/35cb1694-f611-429c-88a4-82ba86297e26)
 3. Renseignez les champs "Nom de l'hôte", "Groupes"
 4. Ajouter une interface SNMP (l'IP étant celle de votre client SNMP) ![image](https://github.com/ornech/Supervision-zabbix/assets/101867500/70070581-f216-40b4-b7c6-0ee605a56ebb)


## Créer un élément (item)

> :warning: L'interrogation d'un client (un GET) passe toujours par la transmission d'un OID. Donc vous devez avant tout trouver l'IOD correspondant à ce que vous souhaitez monitorer. C'est là que le ennuis commence ...
 
