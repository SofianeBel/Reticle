# 🎯 Reticle - MVP v0.1

## 🧠 One-liner
Reticle est un overlay local d’analyse d’aim pour les joueurs FPS, qui affiche en temps réel leur précision et temps de réaction à partir d’une capture GPU et d’un modèle IA léger.

---

## ✅ Features du MVP v0.1 (version testable)

- [ ] Capture d’écran in-game via DXGI sur Kovaak’s
- [ ] Détection de click souris et position dans le temps
- [ ] Calcul du temps entre apparition de cible et click (naïf)
- [ ] Affichage overlay avec % de précision et temps de réaction moyen
- [ ] Export d’un fichier JSON avec données de la session
- [ ] Internal instrumentation (logging every captured frame and click event to debug.log)

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
- IA : Moteur heuristique C++ (analyse statistique, pas de ML pour le MVP)
- Capture : DXGI (avec fallback en screen capture)
- Front : aucun, tout est overlay local

---

## 🤖 Modèle IA du MVP (Clarification)

Pour le MVP, le "modèle IA" est un moteur **heuristique et statistique**, et non un modèle de deep learning entraîné. Il est conçu pour être léger, rapide et fournir une valeur immédiate.

*   **Ce qu'il fait :** Le modèle analyse en temps réel les données de la souris et des cibles pour calculer :
    *   La précision globale (%).
    *   L'overaim / underaim (analyse des tirs manqués pour voir si vous visez trop loin ou pas assez loin).
    *   Le temps de réaction.
    *   Il fournit des conseils basiques basés sur ces patterns pour aider le joueur à devenir plus constant.

*   **Sur quoi il est basé :** Il n'est pas "entraîné". C'est un ensemble de règles logiques et de calculs (géométrie, stats) qui tournent localement. Il est donc déterministe et optimisé pour les cibles simples des aim trainers (formes géométriques).

*   **Son utilité pour le MVP :** Il fournit la valeur principale du produit (un feedback actionnable) sans la complexité ou la latence d'un vrai modèle IA. C'est la fondation parfaite pour des analyses plus poussées dans le futur.

---

## 🗺️ Roadmap brutale (6 semaines)

**Semaine 1 (jusqu’au 6 juillet)**  
- Écrire cette doc ✅  
- Créer repo + structurer les répertoires ✅  
- Prototype de capture DXGI → fichier PNG ✅  

**Semaine 2 (jusqu’au 13 juillet)**  
- Créer le serveur Discord “Reticle Devlog” et poster le premier update de développement.
- Définir et versionner le format de données dans `data_format.md`.
- Ajouter détection de clic souris + position curseur  
- Créer un export brut en JSON (avec coordonnées normalisées et heatmap buckets).
- Implémenter le moteur heuristique de base (précision, temps de réaction).

**Semaine 3 (jusqu’au 20 juillet)**  
- Ajouter overlay avec stats affichées  
- Créer build Windows exécutable  
- Préparer un Google Form de feedback (guide de test, questions ciblées, upload du JSON)
- Trouver 3 testeurs (Discord ou Twitter)
- Mener et enregistrer (screen-record + micro) au moins une session de test utilisateur commentée.

**Semaine 4 (jusqu’au 27 juillet)**  
- Collecter les feedbacks structurés via le Form
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
> - **Description :** L'overlay disparaît quand on ALT+TAB.
> - **Comportement attendu :** L'overlay doit rester visible ("always-on-top").
> - **Tentatives :** `SetWindowPos` avec `HWND_TOPMOST`, flag `WS_EX_TOOLWINDOW` testé.
> - **Priorité :** Haute

---

## 🚀 Vision & Features Post-MVP (v0.2 et au-delà)

L'objectif du MVP est de valider le concept de base avec un moteur local. Une fois cette base solide et validée par les utilisateurs, la priorité sera d'intégrer une IA plus puissante.

-   **Intégration d'un LLM (Gemini 2.5 Pro / OpenAI) :**
    -   **Objectif :** Fournir des conseils en langage naturel, des analyses de sessions complètes, et des plans d'entraînement personnalisés.
    -   **Fonctionnement :** Les données brutes (position, clics, cibles) collectées localement seraient envoyées à l'API de Gemini pour une analyse approfondie. Le résultat serait affiché dans l'overlay ou dans un résumé post-session.
    -   **Challenges à adresser :** Gestion de la latence de l'API, coûts, et confidentialité des données.
    -   **Prototype de Prompt (à valider dès la première session exportée) :**
        ```text
        Prompt:
        "Agis comme un coach e-sport professionnel spécialisé dans les FPS. Analyse la session d'entraînement suivante, issue de mon logiciel Reticle. Identifie les 2 points forts principaux, les 3 points faibles les plus critiques, et propose un plan d'amélioration concret en 3 étapes pour la prochaine session. Sois direct, concis et utilise un langage encourageant."

        [Contenu du fichier session_data.json ici]
        ```
