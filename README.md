# Déploiement automatisé d'un serveur LAMP avec Ansible

Ce projet automatise la mise en place d'un serveur web Apache + PHP sur Ubuntu Server 24.04 avec Ansible. J'ai fait ça pour apprendre à configurer un serveur sans tout installer à la main. Le détail de ma démarche, avec les étapes et les problèmes rencontrés, est dans [JOURNAL.md](JOURNAL.md).

## Objectif

Partir d'une VM Ubuntu vierge et la configurer entièrement avec un playbook : mise à jour des paquets, installation d'Apache2 et de PHP, démarrage du service et création d'une page de test avec des droits Linux maîtrisés.

## Environnement

- Ansible 2.16.3 sur ma machine hôte (Zorin OS)
- VM Ubuntu Server 24.04 sous VirtualBox, en réseau Host-Only (192.168.56.101)
- Connexion SSH avec une clé Ed25519

## Structure du projet

- `inventory.ini` : la liste des machines cibles
- `site.yml` : le playbook qui contient les tâches
- `JOURNAL.md` : mon journal de bord

## Lancer le projet

Vérifier que la machine répond :

```bash
ansible webservers -i inventory.ini -m ping
```

Lancer le déploiement :

```bash
ansible-playbook -i inventory.ini site.yml
```

Tester le résultat :

```bash
curl http://192.168.56.101/index.php
```

## Notes

Si tu testes chez toi, pense à changer l'adresse IP et l'utilisateur dans `inventory.ini`.
