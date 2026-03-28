# SOC Lab Conteneurisé

Projet de fin de module — Cloud et Infrastructures Virtuelles
L2 SIMAC | Dr GUEYE

---

## Stack

| Service | Rôle | Port |
|---|---|---|
| Wazuh Manager | SIEM & détection d'intrusion | 55000 |
| Wazuh Indexer | Base de données des alertes | 9200 |
| Wazuh Dashboard | Interface de visualisation | 443 |
| Suricata | IDS réseau | — |
| Grafana | Tableaux de bord | 3000 |
| TheHive | Gestion des incidents | 9000 |
| DVWA | Cible d'attaque | 8080 |

---

## Prérequis

- Docker >= 24.0 et Docker Compose >= 2.0
- RAM minimum : 8 Go
- Linux (testé sur Kali Linux)

---

## Installation
```bash
# 1. Cloner le dépôt
git clone https://github.com/zal9212/Projet-Soc-LAB.git
cd Projet-Soc-LAB

# 2. Configurer les variables d'environnement
cp .env.example .env

# 3. Paramètre système obligatoire pour OpenSearch
sudo sysctl -w vm.max_map_count=262144
echo 'vm.max_map_count=262144' | sudo tee -a /etc/sysctl.conf

# 4. Démarrer la stack
docker compose up -d

# 5. Vérifier l'état des services
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
```

---

## Accès

| Service | URL | Identifiants |
|---|---|---|
| Wazuh Dashboard | https://localhost | admin / voir .env |
| Grafana | http://localhost:3000 | admin / voir .env |
| TheHive | http://localhost:9000 | admin@thehive.local / secret |
| DVWA | http://localhost:8080 | admin / password |

---

## Structure
```
.
├── docker-compose.yml
├── .env.example
├── .gitignore
├── config/
├── wazuh/
├── suricata/
├── grafana/
├── thehive/
└── rapport/
```

---

## Sécurité

- Les secrets sont externalisés dans `.env` (non commité)
- Deux réseaux isolés : `soc-frontend` et `soc-backend`
- Aucun mot de passe en dur dans `docker-compose.yml`
