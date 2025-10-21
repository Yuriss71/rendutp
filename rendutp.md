# 🧠 TP Réseau — Accès externe & firewall Linux

## 🎯 Objectifs
- Apprendre à exposer un service d’une VM vers l’extérieur (port forwarding / bridged).  
- Mettre en place un pare-feu Linux qui filtre et journalise le trafic.  
- Comprendre la notion de DMZ et de routage entre hôte, VM et Internet.  

## 🧩 Phase 1 — Préparer une VM accessible depuis l’extérieur

### Situation de départ

Une VM linux, un serveur web (python par exemple).
Le but : Rendre accessible ce service à son binôme via le LAN de l'école

### Indices

- Réfléchir au **mode réseau VirtualBox** : lequel permet que d’autres machines voient la VM ?

le mode NAT 


- Si le mode NAT ne suffit pas, que faut-il faire ?  

du port forwarding


- Qu’est-ce qu’un “port” et comment le rediriger ?

dans une adresse ip un port est celui qui vient ouvrir d'autre services a cette meme adresse donc services différents, et la redirection de port c'est une règle qui fait passer les connexions venant d’un port d’une machine vers une autre machine du réseau interne


- Sur la machine hôte (Windows/macOS/Linux), il y a une interface “physique” : comment s’assurer que la VM y est visible ?

faut qu'elle soit dans le même réso

- Comment tester si le service est bien accessible (outil : navigateur, curl, ping, nmap ?)  



- Comment vérifier si la connexion arrive dans la VM (log serveur, netstat, ss ?)  

### Résultat attendu
- Le binome peut taper dans son navigateur l’adresse IP LAN de son collegue et voir la page web hébergée dans sa VM.  
- Le service est fonctionnel et isolé.

## 🧩 Phase 2 — Ajouter un pare-feu / routeur Linux en frontal

### Nouvelle architecture

```bash
[Machine hôte] → [VM Firewall/Routeur] → [VM Serveur web]
```

### Indices

- Comment faire pour que le trafic puisse passer du réseau “externe” vers le réseau “interne” ?  
- Comment une machine peut-elle filtrer des paquets selon leur destination ou protocole ?  
- Comment un pare-feu peut “enregistrer” les connexions (logs) ?  
- Comment vérifier que les logs montrent bien les connexions entrantes ?  
- Que faut-il changer dans VirtualBox pour que le serveur web reste accessible via le firewall ?

### Résultat attendu

- Le site reste accessible depuis l’extérieur, **mais** le trafic passe désormais par la VM Firewall.  
- Le firewall **log** les connexions entrantes et peut bloquer certaines tentatives (par exemple ping ou SSH).  

## 🧩 Phase 3 — Analyse & durcissement

### Indices
- Comment savoir si le firewall bloque ou autorise une requête ?  
- Comment prouver que la connexion passe par la VM Firewall ?  
- Comment autoriser seulement HTTP/HTTPS mais pas SSH ?  
- Quelles commandes permettent de visualiser les compteurs de paquets ou les logs ?  
- Comment tester un pare-feu (scan de ports, ping, curl, etc.) ?  

## 🧩 Phase 4 — Observation et rapport (BONUS)
Chaque binôme doit :
- faire un schéma de son architecture (interfaces, IPs, modes réseau) ;  
- indiquer les ports ouverts et leur fonction ;  
- expliquer comment ils ont testé la connectivité ;  
- montrer un extrait de log prouvant le passage du flux via le firewall ;  
- proposer **au moins une règle de sécurité** ajoutée à la configuration (ex. blocage ping ou SSH).

## ✅ Résultat final attendu
Un mini-système fonctionnel et observable :  
- Hebergement d'un service réel,  
- Service accessible à d’autres,  
- Protection du service et log du trafic **en n’utilisant que du Linux et VirtualBox**.