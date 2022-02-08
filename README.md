# arenametrix

## Project setup
```
npm install
```

### Comment ça marche?
Vue3

Un composant FormComponent qui contient tous les champs indiqués dans le JSON avec un bouton submit pour envoyer les données.
On récupère les ressources via axios avec des ref(), qui servent a gérer les états de nos variables.
On bind toutes les champs sur les propriétés de notre objet Data, puis le bouton Envoyer se charge d'envoyer la requête POST.
Penser a changer l'url dans la requête post, elle a été testée au préalable avec un autre url fonctionnel mais que je n'ai pas indiqué.
