# Référentiel technique

Portail de documentation d'architecture et d'exploitation, organisé par technologie.

**Accès :** https://siradio.github.io/ressources/

## Contenu

| Technologie | Documents |
|---|---|
| Talend | Remote Engine en production · Talend Runtime ESB |

Le portail est prévu pour accueillir d'autres technologies : chaque entrée du menu
est une technologie, chaque sous-entrée un document, et chaque document expose ses
chapitres en troisième niveau.

## Accès protégé

Le contenu de `index.html` est **chiffré** :

- AES-256-GCM ;
- clé dérivée de l'identifiant et du mot de passe par PBKDF2-HMAC-SHA256, 310 000 itérations ;
- déchiffrement réalisé dans le navigateur via WebCrypto.

Le fichier publié ne contient donc aucun texte lisible : sans le mot de passe, il n'y a
rien à extraire du code source de la page.

**Les identifiants ne figurent pas dans ce dépôt.** Ils sont transmis séparément.

## Prérequis navigateur

WebCrypto exige un contexte sécurisé. La page fonctionne servie en **https**
(GitHub Pages) ou depuis `localhost`. Ouverte directement en `file://`, le
déchiffrement est indisponible et la page l'indique explicitement.

## Limites à connaître

- Ce dépôt est public : le fichier chiffré est téléchargeable par tous. La confidentialité
  repose entièrement sur la robustesse du mot de passe, une attaque hors ligne restant
  toujours possible. Pour une confidentialité forte, utiliser un dépôt privé.
- Toute personne disposant du mot de passe accède à l'intégralité du contenu et peut
  le rediffuser.
- Le mécanisme protège le contenu au repos, il ne constitue pas un contrôle d'accès
  par utilisateur : il n'y a ni comptes distincts, ni révocation individuelle, ni
  journal d'accès.

## Régénérer le document

Le générateur et les sources non chiffrées sont conservés hors de ce dépôt.
Changer le mot de passe consiste à relancer la génération puis à remplacer `index.html`.
