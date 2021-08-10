# Examples pour démontrer les capacités de contrôle de Advanced Cluster Security

### Exemple 1 - Refuser le déploiement du tag Latest dans projet integrations-prod

- 1 - Créer la policy policies/block-tag-latest.json dans ACS

- 2 - Créer le deploiement manifests/deployment-latest.yaml dans le projet integrations-prod

- 3 - Observer le deploiment qui scale à 0

### Exemple 2 - Refuser le déploiement d'une image contenant un CVE précis (RHSA-2017:1364)

- 1 - Créer la policy policies/block-cve-RHSA-2017:1364.json dans ACS

- 2 - Créer le deploiement manifests/deployment-old-centos.yaml dans le projet integrations-prod

- 3 - Observer le deploiment qui scale à 0

### Exemple 3 - Blocker l'exécution du processus SSHD dans un conteneur

- 1 - Créer la policy policies/block-sshd-process.json dans ACS

- 2 - Créer le service account manifests/serviceaccount-passoire.yaml dans le projet integrations-prod

- 3 - Permettre l'exécution Root du service account passoire
```
oc adm policy add-scc-to-user anyuid -z passoire
```

- 4 - Créer le deploiement manifests/deployment-passoire.yaml dans le projet integrations-prod

- 5 - Exécuter un terminal (console ou rsh) vers le pod passoire-*

- 6 - Générer les clés SSH
```
ssh-keygen -A
```

- 7 - Démarrer le processus SSHD 
 ```
 /usr/sbin/sshd -D
 ```

- 8 - Le POD sera automatiquement détruit par ACS 


