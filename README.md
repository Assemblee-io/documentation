# Intégration du service Visioconference.me

## **Création de l'accès API**


Rendez vous sur https://visioconference.me/app/integration afin de créer votre clé API

![apikey](cleapi.png)

Cette clé API est privée, ne la partagez pas.

Une fois votre clé d'accès obtenue, vous pouvez demander la création de salons de visioconférence (voir documentation API ([documentation](https://api.visioconference.me/api/v1/enterprise_doc/)) :


### Exemple cURL: 
```
curl --location --request POST 'https://api.visioconference.me/api/v1/entreprise/visio' \
--header 'X-Token: API_KEY' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "ROOM_NAME"
}'
```

### Exemple JS (Fetch):
```js
const headers = new Headers({
    "X-Token": API_KEY, //Remplacer par votre clé API
    "Content-Type": "application/json"
})

var options = {
  method: 'POST',
  headers: headers,
  body: JSON.stringify({ "name": ROOM_NAME });, // Remplacer ROOM_NAME par le nom de votre visioconférence
  redirect: 'follow'
};

fetch("https://api.visioconference.me/api/v1/entreprise/visio", options)
  .then(response => response.json())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```

### Réponse de l'API
```json
{
    "code": 201,
    "data": {
        "iframe": "<iframe allow='camera; microphone; fullscreen; display-capture' src='https://visioconference.me/meet/XXXXXXXX' style='height: 100%; width: 100%; border: 0px;'/>",
        "uniqid": "XXXXXXXX",
        "url": "https://visioconference.me/meet/XXXXXXXX" 
    },
    "message": ""
}
```

L'API vous fournira directement le code HTML necessaire pour integrer l'iFrame, ainsi qu'un lien web pouvant directement être utilisé par vos utilisateurs.
