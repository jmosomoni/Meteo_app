# 🌤️ Application Météo — React

Application web qui affiche la météo en temps réel d'une ville : température,
conditions, humidité et vent, avec une icône dynamique selon le temps et le
moment de la journée. Les données proviennent de l'API [WeatherAPI](https://www.weatherapi.com/).

Projet d'apprentissage front-end (React, TypeScript, Tailwind).

---

## Fonctionnalités

- Recherche de la météo par **nom de ville**
- Affichage de la **température**, du **lieu**, de l'**humidité** et du **vent**
- **Icône météo dynamique** (SVG animés) selon le code météo et jour/nuit
- Gestion des **erreurs** (ville introuvable, problème de connexion)

## Technologies

- **React 19** + **TypeScript**
- **Vite** (serveur de dev & build)
- **Tailwind CSS** + **daisyUI** (style)
- **WeatherAPI** (données météo)

---

## Obtenir une clé API WeatherAPI (gratuit)

L'application interroge l'API **WeatherAPI** pour récupérer la météo. Il faut
**ta propre clé API** (gratuite). Une clé API, c'est un **identifiant personnel**
qui t'autorise à utiliser le service.

1. Va sur **[weatherapi.com](https://www.weatherapi.com/)** → **Sign Up** (inscription gratuite).
2. Crée un compte et confirme ton email.
3. Connecte-toi et ouvre ton **tableau de bord (Dashboard)**.
4. Copie ta **clé API** (une longue suite de lettres et chiffres).

 L'offre gratuite suffit largement pour ce projet.

## 🔧 Mettre la clé dans le projet

La clé s'utilise dans **`src/App.tsx`**, dans la fonction `testMeteo`, sur la
ligne du `fetch`. Remplace la clé par la tienne (la partie après `key=`) :

```js
// src/App.tsx
const res = await fetch(
  `https://api.weatherapi.com/v1/current.json?key=TA_CLE&q=${encodeURIComponent(ville)}&lang=fr`
);
```

>  Astuce : dans VS Code, `Ctrl + F` puis cherche `key=` pour la trouver vite.

---

## Installation & lancement

```bash
# 1. Se placer dans le dossier training d'abord
cd training       

# 2. Installer les dépendances (la première fois)
npm install

# 3. Lancer le serveur de développement
npm run dev
```

L'application démarre sur **http://localhost:5173**.
Pour l'arrêter : `Ctrl + C` dans le terminal.

## Scripts disponibles

```bash
npm run dev       # serveur de développement (rechargement auto)
npm run build     # build de production
npm run preview   # prévisualiser le build
npm run lint      # analyse du code (oxlint)
```

---

## Comment ça marche (le flux)

```
Utilisateur tape une ville ──► fetch() vers WeatherAPI (avec la clé)
                                          │
                              réponse JSON (temp, humidité, vent...)
                                          │
                      React met à jour l'affichage (useState)
```

- L'état `champ` mémorise la ville tapée.
- La fonction `testMeteo()` appelle l'API et récupère les données.
- L'état `meteo` stocke le résultat → l'interface se met à jour automatiquement.
- En cas de souci, l'état `erreur` affiche un message.

## Améliorations possibles

- Prévisions sur plusieurs jours
- Géolocalisation automatique
- Indice UV et pression (icônes déjà présentes dans `public/meteo/`)
- Thème clair / sombre
