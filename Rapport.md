










<h1><center> SWI </center></h1>

<h1><center> Laboratoire 3 WPA - Entreprise </center></h1>







<h2><center> Nuno Miguel Cerca Abrantes Silva, Elie N'djoli </center></h2>

<div style="page-break-after:always;"></div>

### Partie 1

Dans cette première partie on va passer en revue les trames reçu lors d'une authentification EAP-TLS.

Voici l'ensemble des trames:

![1558459838002](./Images/1558459838002.png)

#### Phase d’initiation. Identité du client

Les premières trames d'authentification capturées contiennent les identifiant de l'authentificateur et du suppliant.

![1558459969147](./Images/1558459969147.png)



La trame Request identity envoyé par authentificateur contient les données lié à l'AP :

![1558460113083](./Images/1558460113083.png)



La trame de réponse contient l'identité du suppliant :

![1558460207719](./Images/1558460207719.png)



#### Phase hello

![1558460559839](./Images/1558460559839.png)

- Version TLS

On retrouve dans la trame Cient Hello le numéro de version du protocol TLS

![1558460603177](./Images/1558460603177.png)

- Sélection de la méthode d’authentification

  ![1558526156219](./Images/1558526156219.png)

- Liste des cipher proposées par le client (trame Client Hello)

![1558461045500](./Images/1558461045500.png)

- Cipher accepté par l’AP (trame server Hello)

  ![1558461213141](./Images/1558461213141.png)

- Nonces

  La valeur Random ci-dessous représente le Nonce

  ![1558461444840](./Images/1558461444840.png)

- Session ID (trame Server Hello)  (les Session ID du client Hello est vide)

  ![1558461716583](./Images/1558461716583.png)



#### Phase de transmission de certificats

Certificat serveur (Trame server Hello)

![1558462128904](./Images/1558462128904.png)

- Change cipher spec

  ![1558526764111](./Images/1558526764111.png)

#### Authentification interne et transmission de la clé WPA (échange chiffré, vu comme « Application data »)

![1558462265780](./Images/1558462265780.png)

#### 4-way handshake

![1558460779129](./Images/1558460779129.png)