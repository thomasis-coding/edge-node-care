Markdown · README.md

# Edge Node Care

> Prototypage d'une architecture de résilience réseau sur Raspberry Pi — Proof of Concept académique (ECE Paris, 2ème année)

---

## Contexte

Ce projet explore une solution de **secours local (Edge Computing)** capable de maintenir l'accès à des données critiques lors d'une coupure réseau. L'application théorique visée est le milieu hospitalier, où la continuité d'accès aux données peut être vitale.

Il s'agit d'un **prototype fonctionnel**, pas d'un système prêt pour la production.

---

## Architecture

Le système repose sur un basculement automatisé entre deux environnements :

**Mode nominal** — le Raspberry Pi synchronise les données en tâche de fond depuis le VPS.

**Mode urgence** — le script Watchdog détecte la perte de connexion cloud et :

1. Force le Raspberry Pi à émettre son propre réseau Wi-Fi local
2. Déploie une interface web d'urgence (nommée "Ambre") accessible depuis ce réseau

---

## Stack technique

| Composant | Technologie |
| --- | --- |
| Nœud local | Raspberry Pi (Debian) |
| API secours | Python · FastAPI |
| Détection panne | Script Watchdog Python |
| Réseau | `nmcli` · gestion interfaces Linux |
| Processus | Services en arrière-plan Linux |

---

## Apprentissages

Ce projet a été l'occasion de sortir du code pur pour comprendre l'interaction entre logiciel, matériel et réseau :

- **Administration Linux/Debian** : gestion des ports TCP, manipulation des interfaces réseau (`nmcli`), cycle de vie des processus en arrière-plan
- **Conception d'API** : structuration d'une API REST avec FastAPI
- **Pilotage par l'IA** : utilisation de LLMs comme outil de déblocage technique sur les aspects réseau et système

---

## Limites connues

Ce prototype de 2ème année valide le basculement d'urgence mais présente des limites identifiées :

- **Boucle de résilience incomplète** : la détection du retour de connexion internet et la synchronisation post-crise vers le serveur principal nécessitent une intervention manuelle
- **Gestion des droits système** : les scripts de basculement réseau se heurtent aux sécurités de l'OS (`sudo`), rendant l'automatisation complète non viable sans configuration dédiée

---
