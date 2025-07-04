# 🎯 Coach Gaming IA - MVP v0.1

## 🧠 One-liner
Coach Gaming IA est un overlay local d’analyse d’aim pour les joueurs FPS, qui affiche en temps réel leur précision et temps de réaction à partir d’une capture GPU et d’un modèle IA léger.

---

## ✅ Features du MVP v0.1 (version testable)

- [x] Capture d’écran in-game via DXGI sur Kovaak’s
- [ ] Détection de click souris et position dans le temps
- [ ] Calcul du temps entre apparition de cible et click (naïf)
- [ ] Affichage overlay avec % de précision et temps de réaction moyen
- [ ] Export d’un fichier JSON avec données de la session

---

## ❌ Features hors-scope (à ignorer pour le MVP)

- Détection d’ennemis via deep learning
- Tracking multi-joueurs ou mouvements 3D
- Synchronisation cloud ou base de données
- UI animée ou stylisée
- Compatibilité avec tous les jeux FPS

---

## ⚙️ Stack technique choisie (figée)

- Langage principal : C++ (pour perf + overlay + DXGI natif)
- Overlay : Dear ImGui (fenêtre always-on-top avec transparence)
- IA : ONNX Runtime (modèle linéaire local pour début)
- Capture : DXGI (avec fallback en screen capture)
- Front : aucun, tout est overlay local

---

## 🗺️ Roadmap brutale (6 semaines)

**Semaine 1 (jusqu’au 6 juillet)**  
- Écrire cette doc ✅  
- Créer repo + structurer les répertoires ✅  
- Prototype de capture DXGI → fichier PNG ✅  

**Semaine 2 (jusqu’au 13 juillet)**  
- Ajouter détection de clic souris + position curseur  
- Créer un export brut en JSON (timestamp, position, click)  
- Implémenter modèle ONNX simple (calcul précision naïve)

**Semaine 3 (jusqu’au 20 juillet)**  
- Ajouter overlay avec stats affichées  
- Créer build Windows exécutable  
- Trouver 3 testeurs (Discord ou Twitter)

**Semaine 4 (jusqu’au 27 juillet)**  
- Feedbacks utilisateurs  
- Ajout d’un heatmap basique (par zone de click)  
- Debug et polish UI minimal

**Semaine 5-6 (jusqu’au 10 août)**  
- Démo publique (X ou vidéo courte)  
- Build téléchargeable (itch.io ou lien direct)  
- Préparation du scope v1.0

---

## ⚠️ Risques techniques majeurs

1. DXGI bloqué ou inaccessible sur certains jeux avec anti-cheat → fallback ?
2. Overlay mal affiché ou bloqué par le jeu → testing multi-écrans
3. Latence entre capture/click/IA → optimisation nécessaire sous 50ms

---

## 🎯 Critères de succès MVP

- [ ] Une build testée par 3 à 5 joueurs réels
- [ ] 3 feedbacks exploitables
- [ ] Une vidéo ou GIF montrant la valeur de l’outil (avant/après session)

---

## 🔥 Fichier de suivi bugs à maintenir : `BUGS.md`
> Format :  
> - **Description :** overlay disparaît quand on ALT+TAB  
> - **Comportement attendu :** reste en top layer  
> - **Tentatives :** SetWindowPos, WS_EX_TOOLWINDOW testé  
> - **Priorité :** Moyenne
