# 📊 Dashboards

Bienvenue dans l'espace dédié aux designs de cartes ! Vous trouverez ici les cartes pour rendre votre interface Home Assistant plus esthétique et fonctionnelle.

---

### 📂 Parcourir les catégories

!!! info "Navigation"
    Sélectionnez une carte ci-dessous pour accéder au code YAML et aux instructions d'installation.

| Catégorie | Lien 1 | Lien 2 (Si disponible) |
| :--- | :--- | :--- |
| **Humidité 💦** | [Accéder Mode Standard ➡️](humidite.md) | [Accéder Mode Graphique 📈](humidite-graphique.md) |
| **Température 🌡️** | [Accéder Mode Standard ➡️](temperature.md) | [Accéder Mode Graphique 📈](temperature-graphique.md) |
| **Imprimante 🖨️** | [Noir & Blanc 👤](imprimante-nb.md) | - |
| **Boîte aux lettres 📬** | [Accéder ➡️](boite-aux-lettres.md) | - |
| **Réservoir d'eau 💧** | [Accéder ➡️](reservoir.md) | - |
| **Contact 🚪 (Porte)** | [Accéder ➡️](contact (porte).md) | - |
| **Détecteur de mouvement 💨** | [Accéder ➡️](detecteur-de-mouvement.md) | - |
| **Éclairement ☀️** | [Accéder ➡️](eclairement.md) | - |
| **Sonnette 🔔** | [Accéder ➡️](sonnette.md) | - |

---

### 🎨 Réglage du Thème (Crucial)
!!! danger "Attention : Ne pas utiliser de thème"
    Pour que l'effet Liquid Glass et les transparences fonctionnent, vous ne devez appliquer aucun thème sur votre page ou votre profil.
    > Réglage requis : Sélectionnez "Home Assistant" ou "Utiliser le thème par défaut" dans vos paramètres.
    > Pourquoi ? Les thèmes tiers bloquent les modifications CSS de card-mod et cassent le design visuel des cartes.

---

### 🛠️ Prérequis Généraux
Pour utiliser ces cartes, assurez-vous d'avoir installé les éléments suivants via **HACS** :

* [**button-card**](https://github.com/custom-cards/button-card) Le moteur principal pour le design et les animations.
* [**card-mod**](https://github.com/thomasloven/lovelace-card-mod) Indispensable pour les effets (CSS).
* [**Mushroom Cards**](https://github.com/piitaya/lovelace-mushroom) Pour des icônes et un style moderne épuré.
* [**vertical stack In Card**](https://github.com/ofekashery/vertical-stack-in-card) Pour grouper vos cartes sans bordures visibles.
* [**Mini graph card**](https://github.com/kalkih/mini-graph-card) Pour des graphiques compacts et stylés.

!!! info "Astuce"
    Après l'installation, faites **CTRL + F5** pour actualiser le cache.

!!! tip "TIP"
    **Toutes les cartes sont compatible en mode sombre comme en mode clair (Sauf indication contraire).** 
