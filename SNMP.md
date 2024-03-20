# Zabbix et SNMP
## Installation le paquet client SNMP
``` shell
sudo apt update
sudo apt-get install snmpd
```

## Configuration "miniale" de /etc/snmp/snmp.conf
Au minimum votre fichier snmp.conf devra contenir:
 - `SNMPDRUN=yes` Pour démarrer le service SNMP
 - `rocommunity public` La communauté SNMP en lecture seule. Rapeller vous la caumunauté agit comme mot de passe 
 - `syslocation Mon_Serveur` Emplacement système (syslocation) :
 - `syscontact admin@mondomaine.lab` Un mail d'adminsitrateur

Testez cette configuration
``` shell
sudo systemctl restart snmpd
```
# Amélioration de la configuration
## Installation des MIBS supplémentaire

## Ajout de fonctionnalité du fichier /etc/snmp/snmp.conf

Nous devons configurer ces options:
 - export MIBDIRS= définit le répertoire où sont stocké les MIBs
 - SNMPDRUN= active ou désactive le service SNMP
 - SNMPDOPTS= options de démarrage du daemon SNMPD
 - TRAPDRUN= active ou désactive le service de capture des traps SNMP
 - TRAPDOPTS= options de démarrage de daemon SNMPTRAPD

``` shell
# This file controls the activity of snmpd and snmptrapd

# MIB directories.  /usr/share/snmp/mibs is the default, but
# including it here avoids some strange problems.
export MIBDIRS=/usr/share/snmp/mibs

# snmpd control (yes means start daemon).
SNMPDRUN=yes

# snmpd options (use syslog, close stdin/out/err).
SNMPDOPTS='-Lsd -Lf /dev/null -u snmp -g snmp -I -smux -p /var/run/snmpd.pid '

# snmptrapd control (yes means start daemon).  As of net-snmp version
# 5.0, master agentx support must be enabled in snmpd before snmptrapd
# can be run.  See snmpd.conf(5) for how to do this.
TRAPDRUN=no

# snmptrapd options (use syslog).
TRAPDOPTS='-Lsd -p /var/run/snmptrapd.pid'

# create symlink on Debian legacy location to official RFC path
SNMPDCOMPAT=yes

# Alerte pour le disque dur :
disk / 100000

rocommunity  public # public à remplacer par sa communauté
syslocation  Mon_Ordinateur
syscontact  mon_courriel@fai.fr
``` shell


