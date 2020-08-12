# server_admin

Une compilation de bonnes pratiques à réaliser sur un serveur en production. Les topics sont ajoutés au fur et à mesure de mes recherches et sont non exaustives. L'ordre suis juste le fil de mes envies. Pour des guides plus complets regarder sur le site de l'ANSSI entre autres.

Tout les tests sont réalisés sur une Machine Virtuelle Ubuntu Server 18.04 LTS.

# Principes de bases (NSA)

-> Encrypter les données envoyés par le réseau dès que possibles, même sur un réseau local. L'encryption des mots de passe est très important.
-> Installer le minimum de logiciels pour minimiser le risque de vulnérabilités.
-> Quand possible, faire tourner différents service réseau sur differents serveurs.
-> Configurer des outils de sécurité pour augmenter la sécurité.
-> Minimiser les privilèges.

# Configuration de l'OS

## Bootloader

-> Le bootloader devrait contenir/demander un mot de passe.

## Partitionnement du Disque

-> Il faudrait penser a créer une partition séparé ou un Volume Logique pour /tmp et /var (10G environs, en fonctions des besoins des logiciels)
-> Créer une partition pour /var/log et /var/log/audit est aussi une bonne idée (taille en fonction des logs a sauvegarder).
-> Pareil pour /home, sauf si c'est destiné a etre monté en NFS.

## Network Devices

On devrait ne pas utiliser DHCP dès que possible. Aussi désactiver IPV4 (non commun) et IPV6 quand ce n'est pas necessaire.

## Software Installation

On ne devrait installer aucun software proposé de base par l'installeur.

# Mises à jour

Les mises à jour devraient être automatisés. Cron peut aider à cette tache.

Je ne parle pas ici de la mises en place de serveurs relais pour la récupération des mises à jour.

On peut utiliser le script "autoupdate" dans le repo et le mettre dans /etc/cron.daily

Pour modifier l'heure d'execution des scripts dans /etc/cron.daily, on peut modifier les valeurs dans /etc/crontab

# Sources

Guide de l'ANSSI : 	https://www.ssi.gouv.fr/uploads/2015/02/guide_admin_securisee_si_anssi_pa_022_v2.pdf
Guide de la NSA :	https://apps.nsa.gov/iaarchive/customcf/openAttachment.cfm?FilePath=/iad/library/ia-guidance/security-configuration/operating-systems/assets/public/upload/Guide-to-the-Secure-Configuration-of-Red-Hat-Enterprise-Linux-5.pdf&WpKes=aF6woL7fQp3dJi2xMC9B8KwKRXpapz3fm9KrBe

Cron, Update, Upgrade :	https://help.ubuntu.com/community/AutoWeeklyUpdateHowTo
