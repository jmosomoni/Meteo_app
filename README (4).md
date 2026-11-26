# 🌤️ Application Météo — React

Application web qui affiche la météo en temps réel d'une ville : température,
conditions, humidité et vent, avec une icône dynamique selon le temps et le
moment de la journée. Les données proviennent de l'API [WeatherAPI](https://www.weatherapi.com/).

Projet d'apprentissage front-end (React, TypeScript, Tailwind).

---

## ✨ Fonctionnalités

- Recherche de la météo par **nom de ville**
- Affichage de la **température**, du **lieu**, de l'**humidité** et du **vent**
- **Icône météo dynamique** (SVG animés) selon le code météo et jour/nuit
- Gestion des **erreurs** (ville introuvable, problème de connexion)

## 🛠️ Technologies

- **React 19** + **TypeScript**
- **Vite** (serveur de dev & build)
- **Tailwind CSS** + **daisyUI** (style)
- **WeatherAPI** (données météo)

---

## 🔑 Obtenir une clé API WeatherAPI (gratuit)

L'application interroge l'API **WeatherAPI** pour récupérer la météo. Pour que
ça marche, il faut **ta propre clé API** (gratuite). C'est quoi une clé API ?
C'est un **mot de passe personnel** qui t'autorise à utiliser le service.

Étapes :

1. Va sur **[weatherapi.com](https://www.weatherapi.com/)** et clique sur **Sign Up** (inscription gratuite).
2. Crée un compte (email + mot de passe) et confirme ton email.
3. Une fois connecté, va sur ton **tableau de bord (Dashboard)**.
4. Ta **clé API** (API Key) y est affichée — une longue suite de lettres et chiffres.
5. **Copie** cette clé : c'est elle qu'on va mettre dans le projet (voir ci-dessous).

> 💡 L'offre gratuite suffit largement pour ce projet (météo actuelle, plusieurs
> milliers d'appels par mois).

---

## 🔒 Configurer la clé dans le projet (sans l'exposer)

⚠️ **Règle d'or : la clé ne doit JAMAIS être écrite en dur dans le code.**
Si elle est dans un fichier publié sur GitHub, n'importe qui peut la voler et
l'utiliser à ta place. On la met donc dans un fichier **`.env`**, qui n'est
**pas** envoyé sur GitHub (il est ignoré par `.gitignore`).

1. À la racine du projet, copie le fichier d'exemple :
   ```bash
   cp .env.example .env
   ```
2. Ouvre `.env` et colle ta clé :
   ```
   VITE_WEATHER_API_KEY=ta_cle_copiee_depuis_weatherapi
   ```
   *(le préfixe `VITE_` est obligatoire pour que Vite rende la variable
   accessible côté navigateur.)*
3. Dans le code, la clé est lue **depuis cette variable** (jamais écrite en dur) :
   ```js
   const cle = import.meta.env.VITE_WEATHER_API_KEY;
   const res = await fetch(
     `https://api.weatherapi.com/v1/current.json?key=${cle}&q=${ville}&lang=fr`
   );
   ```

> 🛡️ Si ta clé a déjà été exposée (collée quelque part de public, poussée sur
> GitHub…), considère-la comme **compromise** : régénère-en une nouvelle depuis
> le dashboard WeatherAPI.

---

## 🚀 Installation & lancement

```bash
# 1. Installer les dépendances (la première fois)
npm install

# 2. Configurer la clé API (voir sections ci-dessus)
cp .env.example .env     # puis éditer .env avec ta clé

# 3. Lancer le serveur de développement
npm run dev
```

L'application démarre sur **http://localhost:5173**.

## 📦 Scripts disponibles

```bash
npm run dev       # serveur de développement (rechargement auto)
npm run build     # build de production
npm run preview   # prévisualiser le build
npm run lint      # analyse du code (oxlint)
```

---

## 🧠 Comment ça marche (le flux)

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

## 📚 Ce que j'ai appris

- Les **composants** React et les **hooks** (`useState`)
- Les **appels API** asynchrones (`fetch`, `async/await`) et la gestion d'erreurs
- Le **typage** des données avec TypeScript
- La mise en page avec **Tailwind CSS**
- L'importance de **ne pas exposer une clé API** (variables d'environnement `.env`)

## 🔜 Améliorations possibles

- Prévisions sur plusieurs jours
- Géolocalisation automatique
- Indice UV et pression (icônes déjà présentes dans `public/meteo/`)
- Thème clair / sombre
