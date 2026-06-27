# TAHLIL TAÂLIM 🎓
### Système de Prédiction du Décrochage Universitaire

![F1-macro](https://img.shields.io/badge/F1--macro-0.8959-brightgreen)
![AUC-ROC](https://img.shields.io/badge/AUC--ROC-0.9453-blue)
![Deployed](https://img.shields.io/badge/API-Live%20on%20Railway-purple)
![PFE](https://img.shields.io/badge/Note%20PFE-18%2F20-gold)

> Projet de Fin d'Études — Licence MSDI, FSTM Mohammedia 2026  
> Encadré par **Pr. Youssef Fakir**

---

## 🎯 Problématique

47,2% des étudiants marocains quittent l'université sans diplôme.  
TAHLIL TAÂLIM est un système intelligent qui anticipe ces départs 
grâce à l'analyse de données pour permettre des interventions précoces.

---

## 🏗️ Architecture

| Composant | Technologie | Rôle |
|---|---|---|
| Stockage | HDFS | Données étudiants |
| Traitement | Apache Spark | Feature engineering |
| Modèle | Random Forest (Spark MLlib) | Prédiction risque |
| API | FastAPI + Railway | Endpoint /predict |
| Orchestration | n8n (3 workflows) | Automatisation |
| Interface | Botpress + Groq AI | Chatbot conseiller |
| Logs | Google Sheets | Suivi prédictions |

---

## 📊 Résultats
<img width="1440" height="900" alt="Capture d’écran 2026-06-27 à 19 39 57" src="https://github.com/user-attachments/assets/475b4f29-81bb-45b3-8316-c90b27283904" />

| Métrique | Score |
|---|---|
| F1-macro | **0.8959** |
| AUC-ROC | **0.9453** |
| Décrocheurs détectés | **83%** (236/284) |
| Fausses alertes | **27** (vs 37 pour GBT) |

---

## ⚖️ Fairness by Design
<img width="1440" height="900" alt="Capture d’écran 2026-06-27 à 19 40 15" src="https://github.com/user-attachments/assets/54e657a0-3a63-4cc7-9f29-413ac1c4bf8c" />

- **0/10 prédictions** modifiées quand la région change seule
- Test contrefactuel sur 4 régions marocaines
- `region_origine` exclue des explications retournées au conseiller
- Biais Marrakech-Safi documenté et assumé (+6,3%)

---

## 🤖 Démo API
<img width="2048" height="1161" alt="c1" src="https://github.com/user-attachments/assets/b13099f7-e3e6-45cc-87c9-5fa642363797" />

**Endpoint live :**  
🔗 https://tahlil-taalim-api-production.up.railway.app

**Input (8 variables) :**
```json
{
  "note_bac": 11.5,
  "moyenne_s1": 8.2,
  "nb_echecs_partiels": 4,
  "taux_absenteisme": 25,
  "statut_bourse": 0,
  "premier_emploi": 1,
  "region_origine": "Casablanca-Settat",
  "filiere_bac": "PC"
}
```

**Output :**
```json
{
  "prediction": 1,
  "probability": 0.9902,
  "risk_level": "Élevé",
  "top_features": {...}
}
```

---

## 🔄 Workflows n8n
<img width="1440" height="814" alt="n1" src="https://github.com/user-attachments/assets/cf882a71-34a7-47dc-9264-21cbee63e979" />

- **Workflow A** — Réception profil → API → log Google Sheets
- **Workflow B** — Rapport hebdomadaire automatique chaque lundi 8h via Groq AI
- **Workflow C** — Monitoring mensuel du drift → alerte email

---

## 🛠️ Stack technique

`Python` `Apache Spark` `PySpark` `HDFS` `FastAPI` `Railway`  
`n8n` `Botpress` `Groq AI` `Google Sheets` `Scikit-learn` `SMOTENC`

---

## 👩‍💻 Auteure

**Camelea Ariri** — Étudiante Licence MSDI, FSTM Mohammedia  
🔗 [LinkedIn](https://linkedin.com/in/camelea-ariri) · [GitHub](https://github.com/1camelea)

> Code source disponible sur demande
