# Journal de Bord du Projet Ansible

## Automatisation du déploiement de la pile LAMP avec Ansible

### 1. Objectif & Environnement du Projet

* **But du Projet** : À partir d'une VM Ubuntu Server **26.04.1 LTS** (Long Term Support) installée sur l'hyperviseur VirtualBox[cite: 18, 22], l'objectif est de déployer la pile LAMP de manière automatisée avec Ansible[cite: 18]. 
* **Automatisation** : Permet de refaire la même installation sans erreur, à chaque fois que j'en aurai besoin, au lieu de tout reconfigurer à la main[cite: 18]. Grâce à un playbook, on peut mettre à jour les paquets du serveur, installer Apache2 pour le serveur web et PHP pour l'interpréteur[cite: 18]. Pour prouver son bon fonctionnement, on crée une page web en PHP interprétée par PHP et déployée sur le port 80 via Apache[cite: 18].
* **Environnement** : 
  * OS : Ubuntu Server 26.04.1 LTS (version de long terme offrant sécurité, corrections de bugs et support technique)[cite: 22].
  * Hyperviseur : VirtualBox (type 2)[cite: 23].
  * Version d'Ansible : `2.16.3` (installée via la bibliothèque du serveur Ubuntu, fournissant l'interpréteur et le moteur d'exécution pour faire fonctionner les modules à distance via SSH de manière compatible avec Python)[cite: 23].

---

### 2. Réseau & Connexion

* **Configuration Réseau (Netplan)** :
  * **1ère carte (en NAT)** : `enp0s3` avec DHCP activé (`true`), utilisée pour donner l'accès Internet à la VM (via l'IP `10.0.2.15/24`)[cite: 20, 21].
  * **2ème carte (en Host-Only)** : `enp0s8` avec DHCP désactivé (`false`), configurée avec l'adresse IP statique `192.168.56.101/24` (masque `255.255.255.0`) pour permettre au client (machine hôte) de se connecter à distance[cite: 20, 21, 23].
* **Connexion SSH** : 
  * Commande depuis la machine hôte vers la VM : `ssh giovanni@192.168.56.101`[cite: 23].

---

### 3. Structure & Configuration du Projet Ansible

Le projet s'articule autour de deux fichiers principaux :

#### A. L'inventaire (`inventory.ini`)
* **Rôle** : Indique à Ansible où sont les machines cibles pour exécuter les tâches du playbook (adresse IP, utilisateur, et éventuellement clé privée d'authentification)[cite: 24].
* **Contenu** :
  ```ini
  [webservers]
  192.168.56.101 ansible_user=giovanni
