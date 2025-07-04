# wordpress_role

## Description

Ce rôle Ansible installe et configure un environnement WordPress complet sur un serveur Debian/Ubuntu ou Rocky Linux.  
Il gère l’installation des prérequis (Apache, PHP, MariaDB, etc.), la configuration et sécurisation de MariaDB, le téléchargement et la mise en place de WordPress, ainsi que la configuration d’Apache pour servir WordPress via un VirtualHost.

---

## Prérequis

- Serveur Debian/Ubuntu ou Rocky Linux accessible avec privilèges sudo.
- MariaDB nativement réinitialisé par le playbook inclus (`database.yml`).
- Accès réseau au serveur sur le port 80 (Apache).
- Python installé sur la cible (pour Ansible).

---

## Variables

Ces variables sont définies dans `defaults/main.yml` et peuvent être surchargées dans l’inventaire ou `vars/main.yml` :

| Variable              | Valeur par défaut   | Description                                   |
|-----------------------|--------------------|-----------------------------------------------|
| `mariadb_root_password`| `examplerootPW`    | Mot de passe pour l’utilisateur root MariaDB |
| `wp_db_name`          | `wordpress`        | Nom de la base de données WordPress           |
| `wp_db_user`          | `example`          | Nom d’utilisateur MySQL pour WordPress        |
| `wp_db_password`      | `examplePW`        | Mot de passe utilisateur MySQL WordPress      |
| `wp_db_host`          | `localhost`        | Adresse de la base de données (souvent localhost) |

---

## Structure du rôle

```text
wordpress_role/
├── defaults/
│   └── main.yml           # Variables par défaut
├── handlers/
│   └── main.yml           # Handlers (reload/restart Apache)
├── tasks/
│   ├── prerequisites.yml  # Installation des paquets nécessaires
│   ├── database.yml       # Réinitialisation et sécurisation MariaDB
│   ├── wordpress.yml      # Installation, configuration WordPress, et Apache
│   └── main.yml           # Point d’entrée qui inclut les autres tâches
├── vars/
│   └── main.yml           # Variables spécifiques au rôle (optionnel)
├── tests/
│   ├── inventory          # Inventaire pour tests
│   └── test.yml           # Playbook de test simple
├── meta/
│   └── main.yml           # Métadonnées du rôle (compatibilité, dépendances)
└── README.md              # Documentation du rôle
