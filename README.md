# Intégration du service Visioconference.me

## **Création de l'accès API**


Rendez vous sur https://visioconference.me/app/integration afin de créer votre clé API :

[![N|Solid](https://i.imgur.com/cXkgANu.jpg)](https://visioconference.me/app)

Cette clé API est privée, ne la partagez pas.

Une fois votre clé d'accès obtenue, vous pouvez demander la création de salons de visioconférence (voir documentation API : https://api.visioconference.me/api/v1/enterprise_doc/


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

### Exemple PHP (curl):
```php
<?php

$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => 'https://api.visioconference.me/api/v1/entreprise/visio',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
    "name": "ROOM_NAME"
}',
  CURLOPT_HTTPHEADER => array(
    'X-Token: API_KEY',
    'Content-Type: application/json',
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
?>
```


## Réponse de l'API
```json
{
    {
    "code": 201,
    "data": {
        "iframe": "<iframe allow='camera; microphone; fullscreen; display-capture' src='https://visioconference.me/meet/XXXXXXX' style='height: 100%; width: 100%; border: 0px;'/>",
        "uniqid": "XXXXXXX",
        "url": "https://visioconference.me/meet/XXXXXXX",
        "room": {
            "id": "Qogny8tSpLybQCkaRFSriB",
            "id_team": "FGe1cF8Ukn2V1E1A6zwbFp",
            "id_user": "RTk9Y7yBdAA12x72wNrnGA",
            "name": "test",
            "slot": 100,
            "uniquename": "XXXXXXX",
            "template": "meet",
            "moderator_token": "NTSIFSMV",
            "password_token": "ZWGN5XI5",
            "updatedAt": "2021-02-22T12:29:06.708Z",
            "createdAt": "2021-02-22T12:29:06.708Z"
        }
    },
    "message": ""
}
}
```

L'API vous fournira directement le code HTML necessaire pour integrer l'iFrame, ainsi qu'un lien web pouvant directement être utilisé par vos utilisateurs.

## **Paramètre d'URL**

Vous pouvez envoyer certain paramètre dans l'URL de l'iframe visioconference.me:
| Paramètre  | Effet |
| :--------------- | :--- |
| m  | Permet l'envoi du moderator_token, connecte l'utilisateur en temps que modérateur |
| name  | Permet l'envoi d'un nom, applique le nom a l'utilisateur dans la salle de connection |

### **Exemple**
```
# Connection en temps que modérateur
https://visioconference.me/meet/XXXXXXX?m=NTSIFSMV

# Connection sans droit
https://visioconference.me/meet/XXXXXXX

# Connection nommé et modérateur
https://visioconference.me/meet/XXXXXXX?m=NTSIFSMV&name=John
```


## **Utilisation du service**


[![N|Solid](https://i.imgur.com/95YNKJb.png)](https://visioconference.me)


