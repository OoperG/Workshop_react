# Readme for React Project

## Objectif du Workshop

Le but de ce workshop est de vous faire découvrir React, une bibliothèque JavaScript 
populaire utilisée pour construire des interfaces utilisateur interactives.

- Nous allons voir comment créer un projet React et comment le lancer.

- Comment créer un formulaire avec un input et un bouton.

- Comment utiliser le hook useState pour gérer l'état local d'un composant.

- Comment faire des requêtes HTTP avec React en utilisant Fetch. (oui j'aime pas axios)

## React ?

React est une bibliothèque JavaScript populaire utilisée pour construire des interfaces 
utilisateur interactives. Il a été développé par Facebook et est maintenant utilisé par 
de nombreuses entreprises et développeurs pour créer des applications web à fort impact 
visuel.

React se concentre sur la création de composants réutilisables, qui sont des éléments 
individuels de l'interface utilisateur tels que les boutons, les formulaires et les 
cartes. Les composants peuvent être combinés pour créer des pages et des applications 
complexes.

Aujourd'hui, React est l'une des bibliothèques JavaScript les plus populaires et est 
utilisée par de nombreuses entreprises telles que Netflix, Airbnb, Uber, Twitter, 
Facebook, Instagram, Pinterest, etc. Les développeurs React sont très demandés sur 
le marché du travail.

## Prérequis

Installez Node.js et npm (gestionnaire de paquets Node) sur votre ordinateur.

Lien : https://nodejs.org/en/

## Installation

Utilisez la commande npx create-react-app my-app pour créer un nouveau projet 
React nommé "my-app".

```bash
npx create-react-app my-app
```

Vous pouver nommer votre projet comme vous le souhaitez.

## Modification du fichier App.js

Remplacez le contenu du fichier src/App.js par celui-ci :

```javascript
import React, { useState } from "react";

function App() {
    
    return (
        <div>
            <h1>Hello World</h1>
        </div>
    );
}

export default App;
```

## Modification du fichier index.js

Remplacez le contenu du fichier src/index.js par celui-ci :

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
);

reportWebVitals();
```

## Lancement du projet

Utilisez la commande suivante pour lancer le projet :
    
```bash
npm start
```

Accédez à l'application en accédant à l'URL http://localhost:3000/ dans votre navigateur.

Vous devriez voir une page blanche avec le titre "Hello Word".

## 1/ UseState et input

Nous allons maintenant créer un formulaire avec un input et un bouton. Lorsque 
l'utilisateur tape quelque chose dans l'input et clique sur le bouton, nous allons 
afficher le texte dans la page.

useState est un hook (crochet) React qui permet de gérer l'état local d'un composant. 
L'état d'un composant est une donnée qui peut être mise à jour au fil du temps et qui 
est nécessaire pour la mise à jour de l'interface utilisateur.

L'utilisation de useState est très simple. Il suffit de déclarer une variable d'état 
en utilisant useState à l'intérieur d'un composant et de lui assigner une valeur initiale.
Par exemple :

```javascript
const [city, setCity] = useState("");
```

Pour le moment, la variable city est vide. Nous allons maintenant créer un input et 
un bouton. Lorsque l'utilisateur tape quelque chose dans l'input et clique sur le 
bouton, nous allons mettre à jour la variable city avec la valeur de l'input.

```javascript
<form onSubmit={handleSubmit}>
    <input
        type="text"
        placeholder="Enter city name"
        value={city}
        onChange={handleChange}
    />
    <button type="submit">Get Weather</button>
</form>
```

Pour le moment, la fonction handleChange n'existe pas. Nous allons la créer. 
La fonction handleChange va mettre à jour la variable city avec la valeur de l'input
en utilisant la fonction setCity. 

Souvenez-vous que la fonction setCity est une fonction
que nous avons déclarée avec useState.

```javascript
const handleChange = (event) => {
    setCity(event.target.value);
};
```

La fonction handleSubmit n'existe pas non plus. Nous allons la créer dans l'étape suivante.

## 2/ Fetch

La fonction handleSubmit va permettre d'envoyer la valeur de la variable city à l'API 
openweathermap. Pour cela, rendez-vous sur le site https://openweathermap.org/api et 
créez un compte et recupérez votre clé API.

Nous allons maintenant créer la fonction handleSubmit. La fonction handleSubmit va 
envoyer la variable city vers l'API openweathermap.

```javascript
const handleSubmit = event => {
    event.preventDefault();
    fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=YOUR_API_KEY`
    )
        .then(response => response.json())
        .then(data => {
            setWeather(data);
        })
        .catch(error => {
            console.error("Error:", error);
        });
};
```

Dans la requête HTTP, n'oublier pas de remplacer YOUR_API_KEY par votre clé API !

N'oublier de créer la variable weather et la fonction setWeather comme pour la variable city.

Quelques explications sur le code :

- La fonction fetch permet d'envoyer une requête HTTP vers l'API openweathermap.
- La fonction then permet de récupérer la réponse de l'API sous forme de JSON.
- La deuxième fonction then permet de mettre à jour la variable weather avec la réponse de l'API.
- La fonction catch permet de gérer les erreurs.

## 3/ Affichage des données

Nous allons maintenant afficher les données de la variable weather dans la page.

```javascript
{weather.main ? (
    <div>
        <p>La température à {city} est de {temperature.toFixed(2)}°C</p>
        <p>Humidity: {weather.main.humidity}</p>
    </div>
) : (
    <p>No weather data</p>
)}
```

Maintenant, lorsque l'utilisateur tape quelque chose dans l'input et clique sur 
le bouton, nous allons afficher la température et l'humidité de la ville dans la page.

## 4/ Ajout d'une image

Nous allons maintenant ajouter une image en fonction du temps qu'il fait dans la ville.

Pour cela, nous allons utiliser la variable weather.weather[0].main qui contient 
le temps qu'il fait dans la ville.

```javascript
{weather.main ? (
    <div>
        <p>La température à {city} est de {temperature.toFixed(2)}°C</p>
        <p>Humidity: {weather.main.humidity}</p>
        <img src={`http://openweathermap.org/img/w/${weather.weather[0].icon}.png`} alt="weather icon" />
    </div>
) : (
    <p>No weather data</p>
)}
```

Nous avons maintenant une application qui affiche la température, l'humidité et un visuel
du temps qu'il fait dans la ville.

## BONUS

Si vous avez le temps, vous pouvez ajouter un input pour choisir l'unité de mesure 
(°C ou °F) et ajouter un input pour choisir le pays.

Vous pouvez aussi donner un style à votre application.
