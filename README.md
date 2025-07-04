# 🎯 Reticle

Reticle est un assistant d'entraînement à l'aim en temps réel pour les joueurs FPS. Il capture l'écran, analyse vos tirs et vous fournit un feedback immédiat via un overlay local.

## 🚀 Objectif MVP

Créer un overlay local affichant :
- % de précision
- temps de réaction
- export JSON de session

## 📦 Stack

- C++ (DXGI, ImGui)
- Heuristiques maison (pas de deep learning pour le MVP)
- Pas de backend, pas de dépendance réseau

## 📁 Structure

- `/capture` → capture d’écran via DXGI
- `/overlay` → overlay ImGui
- `/analysis` → moteur d’analyse local
- `/logs` → fichiers de debug + données JSON

## ✅ Avancement

Voir le fichier [`MVP.md`](./MVP.md)

## 💬 Devlog

Discord : *[à venir]*  
Twitter / X : *[à venir]* 