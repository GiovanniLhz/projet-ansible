# Automatisation d'une pile LAMP avec Ansible

À partir d'une VM Ubuntu Server installée sur l'hyperviseur VirtualBox, ce projet permet de déployer la pile LAMP de manière automatisée avec Ansible. L'automatisation permet de refaire la même installation sans erreur et à chaque fois que j'en aurai besoin, au lieu de tout reconfigurer à la main. Le détail complet de ma démarche se trouve dans le [JOURNAL.md](JOURNAL.md).

## Environnement

* **OS :** Ubuntu Server 26.04.1 LTS (Long Term Support)
* **Hyperviseur :** VirtualBox (type 2)
* **Outil d'automatisation :** Ansible (version 2.16.3)
* **Réseau :** Configuration de deux cartes réseau (NAT pour l'accès Internet et Host-Only avec IP statique `192.168.56.101` pour la connexion SSH du client vers la VM).

## Fichiers

* `inventory.ini` : fichier d'inventaire ciblant l'adresse IP de la machine distante et l'utilisateur.
* `site.yml` : playbook Ansible regroupant les tâches d'installation (mise à jour des paquets, installation d'Apache et PHP, configuration du service et copie de la page de test).
* `index.php` : page de test PHP déployée automatiquement dans le répertoire web pour valider le bon fonctionnement.
* `JOURNAL.md` : mon journal de bord détaillé.

## Lancer le projet

Vérifier la connexion (Ping) :
```bash
ansible webservers -i inventory.ini -m ping
