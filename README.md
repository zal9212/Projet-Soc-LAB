SOC Lab Conteneurisé
Projet de fin de module — Cloud et Infrastructures Virtuelles
L2 SIMAC | Dr GUEYE


Stack
ServiceRôlePortWazuh ManagerSIEM & détection d’intrusion55000Wazuh IndexerBase de données des alertes9200Tableau de bord WazuhInterface de visualisation443SuricataIDS réseau—GrafanaTableaux de bord3000TheHiveGestion des incidents9000DVWACible d’attaque8080

Prérequis

Docker >= 24.0 et Docker Compose >= 2.0
RAM minimum : 8 Go
Linux (testé sur Kali Linux)


Installation
Bash# 1. Cloner le dépôt
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

Accès
ServiceURLIdentifiantsTableau de bord Wazuhtableau de bord, grafana, thehive, dvwaadmin / voir .envGrafanaWazuh-Manager, Wazuh-indexer, CassandraCritiques des stagiaires servicesTheHivehttp://localhost:9000admin@thehive.local / secretDVWAhttp://localhost:8080admin / mot de passe

Structure
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

Sécurité

Docker >= 24,0
Deux réseaux isolés : soc-frontend et soc-backend
Aucun mot de passe en dur dans docker-compose.yml# Projet-Soc-LAB
