# Journal de Bord  Projet Évolutif Sciensano

## Session 1 : Provisionnement et Déploiement Automatise LAMP avec Ansible

### 1. Ingestion & Architecture
- Configuration de l'environnement virtuel sous Oracle VirtualBox avec Ubuntu Server 24.04 LTS (LVM).
- Configuration de l'adaptateur réseau "Host-Only" (`vboxnet0`) avec l'IP statique `192.168.56.101`.
- Installation et initialisation d'Ansible v2.16.3 sur le système hôte Zorin OS.

### 2. Connectivité et Privilèges
- Génération d'une paire de clés SSH Ed25519 (`~/.ssh/id_ed25519`) et copie sur la VM cible via `ssh-copy-id`.
- Résolution des blocages d'élévation de privilèges Ansible en configurant `giovanni ALL=(ALL) NOPASSWD: ALL` dans `/etc/sudoers`.
- Validation de la communication via la commande ad-hoc `ansible webservers -i inventory.ini -m ping` (réponse `pong`).

### 3. Automatisation Playbook (`site.yml`)
- Déploiement de la pile LAMP (Apache2, PHP 8.5, `libapache2-mod-php`).
- Gestion de l'état du service systemd `apache2` (démarré et activé au boot).
- Création du fichier de test `/var/www/html/index.php` avec gestion stricte des droits Linux :
  - Propriétaire/Groupe : `www-data:www-data`
  - Permissions : `0644` (`rw-r--r--`)

### 4. Validation & Contrôle Qualité
- Vérification CLI : `curl http://192.168.56.101/index.php` (Code HTTP 200 / Rendu PHP valide).
- Vérification Système : `systemctl status apache2` sur la VM.
- Rendu Navigateur : Validation visuelle sur l'hôte.

### 5. Gestion de Version
- Initialisation du dépôt local Git sous VS Code.
- Configuration de l'identité Git (`GiovanniLhz`).
- Publication du dépôt distant sur GitHub : `https://github.com/GiovanniLhz/projet-ansible`.