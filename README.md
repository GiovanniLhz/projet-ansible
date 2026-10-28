# Automatisation d'une pile LAMP avec Ansible

L'objectif de ce projet est de déployer et configurer de manière automatisée un serveur web Apache et son interpréteur PHP sur une VM Ubuntu Server, en s'appuyant sur un playbook Ansible. Le détail complet de ma démarche se trouve dans le [JOURNAL.md](JOURNAL.md).

## Fichiers

* `inventory.ini` : fichier d'inventaire ciblant l'adresse IP de la machine distante et l'utilisateur.
* `site.yml` : playbook Ansible regroupant les tâches d'installation (mise à jour des paquets, installation d'Apache et PHP, configuration du service et copie de la page de test).
* `index.php` : page de test PHP déployée automatiquement dans le répertoire web pour valider le bon fonctionnement.
* `JOURNAL.md` : mon journal de bord détaillé.

## Lancer le projet

Vérifier la connexion (Ping) :
```bash
ansible webservers -i inventory.ini -m ping
