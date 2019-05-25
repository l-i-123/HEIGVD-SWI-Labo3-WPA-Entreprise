










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

### Partie 2

##### Modification du fichier hostapd-wpe.conf

Le fichier hostpad-wpe.conf à été mis à jour afin qu'un AP nommée WinternetIsComing soit créé.

![1558793685583](./Images/1558793685583.png)

De plus, il a été nécessaire d'adapter le nom de l'interface

![1558796949124](./Images/1558796949124.png)

##### Lancement de hostpad-wpe

Après la mise à jour du fichier hostapd-wpe.conf on a pu lancer lancer l'AP avec la commande `sudo hostapd-wpe hostapd-wpe.conf`. Après un temps d'attente l'utilisateur "Elie" à tenté de se connecter à l'AP

![SWI_1](./Images/SWI_1.PNG)

On a pu récupéré son challenge et sa response pour récupérer son mot de passe avec l'outil asleap et avons trouvé son mot de passe qui est "hello"

![SWI_2](./Images/SWI_2.PNG)

Il est aussi possible d'utiliser john de ripper pour effectuer cette étape. Pour cela, il faut mettre le "jrt NETNLM" récupéré avec hostapd-wpe dans un fichier texte et de lancer la commande suivante `john --format=netntlm fichier_texte.txt` 

#### Méthode d'autentification géré par hostapd-wpe

Les méthode d'authentification ci-dessous sont géré par hostpad-wpe:

1. EAP-FAST/MSCHAPv2 (Phase 0)
2. PEAP/MSCHAPv2
3. EAP-TTLS/MSCHAPv2
4. EAP-TTLS/MSCHAP
5. EAP-TTLS/CHAP
6. EAP-TTLS/PAP

##### Source

<https://warroom.rsmus.com/evil-twin-attack-using-hostapd-wpe/>