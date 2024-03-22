Outils SNMP:
 - snmp-bridge-mib : Ceci est une MIB (Management Information Base) spécifique pour les ponts réseau (bridges). Elle contient des informations sur les ponts réseau, telles que les adresses MAC, les statistiques de trafic, etc.
 - snmpconf : Outil qui permet de configuration du démon SNMP (snmpd) -> /etc/snmp/snmpd.conf.
 - snmpget : Envoie une requête de type "GET" à un agent SNMP pour récupérer la valeur d'une variable MIB spécifique.
 - snmpping : Envoie une requête de type "PING" à un périphérique SNMP capable de répondre à ces requêtes. Cela permet de vérifier la connectivité et la disponibilité du périphérique.
 - snmptable :Affiche une table SNMP, ce qui est utile pour afficher des données tabulaires structurées telles que les interfaces réseau, les adresses IP, etc.
 - snmptrap : Envoie des notifications SNMP (traps) à un gestionnaire SNMP pour informer des événements tels que les pannes, les erreurs, etc.
 - snmpbulkget :Récupére un grand volume de données SNMP en une seule requête.
 - snmpd : Il s'agit du démon SNMP.
 - snmpstatus:
``` sql  
user@zabbix:/etc/snmp$ snmpstatus -v 2c -c public 192.168.1.82 
```
 - snmptranslate : Traduire les OID (Object Identifiers) SNMP en noms symboliques et vice versa, facilite la compréhension des informations.
 - snmpwalk : Parcours la MIB d'un agent SNMP et afficher les valeurs de toutes les valeurs accessibles.
``` sql
snmpwalk -v 2c -c public 192.168.1.82
```
