# RadioWave — mini-lecteur web

Ecouter **une** station de radio dans un navigateur, sans rien installer. C'est
la page qui s'ouvre quand on partage une station depuis l'application
**RadioWave** : le destinataire clique, la radio se lance.

- En ligne : <https://jmarcgwada.github.io/radiowave-listen/>
- Contenu : un seul fichier, [index.html](index.html) — environ 12 ko, sans
  dependance ni outil de construction.

## Comment on l'appelle

La station se designe par son identifiant Radio Browser, passe dans l'adresse.
Trois noms de parametre sont acceptes, le premier trouve l'emporte :

```
https://jmarcgwada.github.io/radiowave-listen/?s=<uuid>
https://jmarcgwada.github.io/radiowave-listen/?station=<uuid>
https://jmarcgwada.github.io/radiowave-listen/?uuid=<uuid>
```

Sans parametre, la page ne reste pas muette : elle explique qu'aucune station
n'a ete demandee et renvoie vers l'application.

## Ce que fait la page

1. **Retrouve la station** aupres de [Radio Browser](https://radio-browser.info),
   l'annuaire public et gratuit qui alimente aussi l'application.
2. **Lance le flux** dans le lecteur audio du navigateur.
3. **Affiche le logo** de la station. A defaut, elle tente le favicon du site de
   la radio, en passant au besoin de `http` a `https` — sans quoi le navigateur
   refuserait l'image sur une page securisee.
4. **Signale l'ecoute** a Radio Browser (`/json/url/<uuid>`), qui s'en sert pour
   son classement des stations. C'est la contrepartie d'un annuaire gratuit.
5. **Propose l'application** et le partage — WhatsApp, Facebook, lien direct.

## Trois serveurs, pas un

Radio Browser n'a pas d'adresse unique : le service est reparti sur plusieurs
miroirs (`de1`, `at1`, `nl1`). La page les essaie **a la suite** et ne declare
l'echec qu'apres les avoir tous vus. Un miroir en panne passe donc inapercu, ce
qui n'aurait pas ete le cas en visant une seule adresse.

Quand la lecture echoue malgre tout — flux mort, station qui refuse les
navigateurs —, un message le dit clairement au lieu de laisser un bouton
« lecture » sans effet.

## Modifier

Tout est dans `index.html` : styles, balises et script. Envoyer sur `main`
suffit, GitHub Pages republie.

Si vous touchez aux balises `og:` de l'en-tete, verifiez l'apercu avec le
[debogueur de partage de Facebook](https://developers.facebook.com/tools/debug/) :
ces balises ne servent qu'au moment ou quelqu'un colle le lien.

## Projets lies

- **RadioWave** — l'application mobile.
- **radiowave-promo** — la page de presentation, qui renvoie ici.
- **radiowave-legal** — la politique de confidentialite.
