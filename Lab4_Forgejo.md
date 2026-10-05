# Lab 4 : Déploiement de Forgejo avec Docker et Publication

## 1. Déploiement de Forgejo via Docker

### Préparation de l'environnement Docker
```bash
sudo apt update
sudo apt install docker.io -y
sudo systemctl enable --now docker
```[cite: 37]

### Lancement du conteneur Forgejo
```bash
# Création du volume persistant
docker volume create forgejo_data

# Lancement du conteneur Forgejo (Ports 3000 Web et 2222 SSH)
docker run -d --name forgejo \
  -p 3000:3000 -p 2222:22 \
  -v forgejo_data:/data \
  codeberg.org/forgejo/forgejo:latest
```[cite: 37]

---

## 2. Configuration et Liaison Git - Forgejo

1. Accéder à l'interface Web : `http://<IP_VM>:3000` et finaliser l'installation[cite: 37].
2. Créer un nouveau dépôt nommé `tp-forgejo` depuis l'interface Web[cite: 37].

### Liaison du dépôt local à Forgejo
```bash
git remote add origin http://<IP_VM>:3000/utilisateur/tp-forgejo.git
```[cite: 37]

---

## 3. Réalisation des Commits et Publication

### Commit 1 : Initialisation
```bash
touch file1.txt file2.txt
git add .
git commit -m "Commit 1 : Initialisation du projet"
```[cite: 37]

### Commit 2 : Modification du fichier 1
```bash
echo "Contenu pour le commit 2" >> file1.txt
git add file1.txt
git commit -m "Commit 2 : Mise a jour de file1.txt"