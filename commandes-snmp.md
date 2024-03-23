# Outils SNMP
**snmpstatus**: Tente d'établir une connexion avec un agent sur le port UDP:161 de l'hôte spécifié.
``` bash  
snmpstatus -v 2c -c public 192.168.1.82 
```
**snmpget** : Envoie une requête de type "GET" à un agent SNMP pour récupérer la valeur d'un OID.
``` bash  
snmpget -c public -v 2c localhost .1.3.6.1.2.1.1.1
```
**snmpwalk** : Parcours la MIB d'un agent SNMP et afficher toutes OID et valeurs accessibles.
``` bash
snmpwalk -v 2c -c public 192.168.1.82
```
 **snmptable** :Certain OID font référence à des données stockées sous forme de tableau comme les interfaces réseau, les points de montage, etc.
``` bash  
snmptable -c public -v 2c localhost  .1.3.6.1.2.1.2.2
```
**snmptranslate** : Traduire les OID (Object Identifiers) SNMP en noms symboliques et vice versa  

**snmp-bridge-mib** : Collecte des informations sur un pont réseaux Linux et exporte ces données afin qu'elles puissent être interrogées à distance via SNMP. Nécessite l'utisation de l'agentx.
``` bash  
perl /usr/bin/snmp-bridge-mib <NOM DU PONT>
```

**snmpconf** : Outil qui permet de configuration du démon SNMP (snmpd) -> /etc/snmp/snmpd.conf.  

**snmpping** : Envoie une requête de type "PING" à un périphérique SNMP capable de répondre à ces requêtes. Cela permet de vérifier la connectivité et la disponibilité du périphérique.  


**snmptrap** : Envoie des notifications SNMP (traps) à un gestionnaire SNMP pour informer des événements tels que les pannes, les erreurs, etc.  
**snmpbulkget** :Récupére un grand volume de données SNMP en une seule requête.  



