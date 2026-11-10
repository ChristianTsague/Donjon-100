# Transformation du telephone en station technique (TERMUX)

Auteur : ==🟣`Christian Tsague @ G1M1`==  
Date de debut : 2026-11-09
Statut :  ==🟢terminer==


## Termux c'est quoi

si comme moi vous aimer la vue du terminal, les lignes de commandes, et cette impression de garder le controle de votre machine, Termux risque vous plaire 
Mais au dela de de son apparence de terminal, Termux permet de transformer un simple android en un veritable environnement linux
l'objectif ici n'est pas seulement de d'installer quelque outil, mais de comprendre comment fonctionne cet environnement, ce qu'il permet de faire, et comment l'exploiter pour aprendre, experimenter et administrer des systeme

**Bienvenue dans ma formation du telephone en station technique**

attacher a ce document vous verez un pdf du nom de [[Catalogue-100-TPS-CK_237.pdf]]  qui montre la liste des defi que je me suis fixé pour mieux évouer donc cete doccu est principalement fait pour l'étape 0 mais je vien de le remarquer que c'est aussi le tp 11 donc on vas faire d'une piere deux coups 

## Rappel du TP 

configurer Termux comme console d'administration complète. Validation : connexion SSH par clé depuis le téléphone sans mot de passe. Livrable : guide d'installation publié (super contenu débutant Cyberkid237).

## ⚠️ Minimum a connaitre 

il faut savoir que ==🟢Termux== n'est pas une aplication pour IOS donc si jamais vous suivez ce guide avec un iphone vous ne pourez pas pratiquer ce que vous verez en reseaux, la plus part des outils sont disponible uniquement sous android. il y a un moyen pour faire tourner des fochier APK sur iphone mais c'est trop de contrainte et c'est pas l'objectif de la docu. Maintenant que tout est dit, on peut commencer a grubouiller 

### C'est quoi SSH

SSH (_Secure Shell_) est un protocole qui definit en gros comment deux machine communique de facon sécuriser pour vous donnez de quoi visualisé le truc, lorsque deux personne (noeuds) communique entre eux, il es possible pour un attaquant de recupérer le trafic grace a un renifleur comme wireshark et donc de voir ce que vous faite il est pareille que le protocole TELNET mais en plus sur de facon a ce que si une personne snife votre reseaux, il vera un bruit illisible du charabiat en gros 
le protocole ==🟢SSH== a principalement trois fonction qui lui ai propre 
1. **Terminal distant** : tapé des commande sur un terminal a distance.
c'est exactement ce qu'on essayera de faire dans ce tp, le but de ce mini travaille est de pouvoir trasformer notre telephone en terminal distant pour pouvoir manipuler notre pc sur notre android 
2. **Transfert de fichier** :  grace a SCP, RSYNC, ou encorre SFTP, il est posside de transferer les donnée de facons securisé avec le protocole ssh 
d'ailleur je me rapelle que le logiciel ==🟢NETCAT== me permetais d'envoyer des message entre deux pc directement sur le terminal, le logiciel permetais aussi de se transferer les donner mais le seul bemole etais que le trafic etais en claire genre en analysant le trafic du reseaux on voyais clairement ce qu'on se disais mais c'étais plutot cool 
3. **Tunneling/port forwading** : en gros il permet de faire transiter d'autre connexion dans le tunel sécurisé (un exercice du genre est present dans le pdf [[Cyberdid_TPS/Catalogue-100-TPS-CK_237.pdf|Catalogue-100-TPS-CK_237]] en TP 69 
### Le premier concept a retenir 

 le protocolle ssh est basé sur un modèle client serveur il fonctionne comme un appel telephonique il faut un appelant et un recepteur le protocole fonctionne sur une architecture **client/serveur** 

**Serveur SSH** : Ton PC,  sshd est le logiciel utilisé pour pour serveur ssh (_le « d » = daemon, programme qui tourne en arrière-plan_) Il écoute sur le port 22 et attend des connexions

**Client SSH** Ton téléphone (_Termux_) ssh Il initie la connexion vers le serveur

### Conséquence logique, très importante :

1. Le client n'a besoin d'aucun privilège, d'aucun root, d'aucune configuration spéciale. Il se contente de « sonner à la porte ».
2. Le serveur doit : (1) avoir le programme sshd installé, (2) être démarré, (3) être joignable sur le réseau.

## Installation et constat

avant d'entamer cette section je tien a precesé que tout ce qui suit se fait sous un environnement linux, non pas que le systeme windows n'est pas adapter mais la plus part des tache en reseaux ou cyber sécuriter se font sur des os lunux a cause de sa compatibiliter et de sa customisation je vous invite donc a
travailler sous un environement linux soit en dual boot, en virtuel ou comme moi en tant qu'OS principal.

**1. installer termux 

le terminal termux est disponible sur le playstore telecharger et ouvrez le 
![[Screenshot_2026-11-09-16-30-58-737_com.android.vending.jpg|281]]![[Screenshot_2026-11-09-16-35-53-809_com.termux.jpg|281]]

ah la beauter du terminal sous android il y a rien de mieux pour faire des test

**2. lancer le premiere commande 

l'une des bonne pratique quand on manipule les terminal linux c'est de constament faire des mis a jour et notre terminal mobile n'échape pas a la regle donc voila la commande pour la faire 

```bash
pkg update && pkg upgrade
```
ici on utilise pas le module APT comme sur un linux clasic a la place on passe par un PKG

une fois les mis a jour terminer on passe a l'installation de notre service SSH tout en profitant pour installer des paquet dont nous aurons surement besoins pour les autre TP

```bash
pkg install openssh nmap netcat socat git curl wget nano jq
python
```

avec ca votre telephone commance a devenir un veritable lab pour vos futur test mais c'est pas encore terminer il vous reste a installer le fameux #serveur car rapeller vous que termux étais juste la pour etre le client 
![[Screenshot_2026-11-09_16-47-33.png]]

evidemant moi je l'ai deja installer donc on vas directement le configurer 

### la methode d'authentification 

**1.methode par clé publique

le protocole fonctionne grace a des clé d'authentification. une clé dite ==🟠clé_public== et une autre dute ==🟠clé_privé== (_c'est la methode la plus propre pour innitier un acces SSH_)

Le principe est une paire de fichiers générés ensemble :
• Clé privée ( ~/.ssh/id_ed25519 ) : reste sur le CLIENT, ne se partage jamais. C'est ton identité.
• Clé publique ( ~/.ssh/id_ed25519.pub ) : se copie sur le SERVEUR, dans ~/.ssh/authorized_keys du compte visé. Tu peux la diffuser librement, d'où son nom. 

j'ai compris le principe de la maniere suivante : **L'analogie du cadenas** la clé publique est un cadenas ouvert que tu fabriques toi-même. Tu en poses une
copie sur le serveur. Quand tu te connectes, le serveur te défie de prouver que tu possèdes la clé privée correspondante, par un calcul cryptographique
(_encore un truc ou les maths intervienent sans qu'on ne comprend jamais vraiment pourquoi_) partant de ce principe on peut donc en deduire que si cette echange de clé se fait une fois on aurai plus besoin de retaper le mot de passe de la session a chaque fois pour ce conecter vue que c'est la preuve qui vas a chaque fois transiter entre les deux appareille 

**2.methode par mot de passe (_la plus basique_)

l'authentification peut aussi ce faire par le mot de passe du compte utilisateur distant : le client demande une ouverture de session et le serveur dit en gros, "oui la session est bien dispo, donne mois juste sont mot de passe avant de continuer"
cette methode est tres utiliser mais les inconvenient que je la trouve sont les suivant 
1. il es vulnerable au brute force et si vous regardez le pdf des exercice, vous verez que le TP 2 est porter justement dessus
2. il faut retaper le mot de passe a chaque fois 

donc vue que on a telecharger termux, on vas donc tester la methode des clé

tout d'abord vous devez conecter votre tellephone au meme reseaux wifi que votre machine, et reperer l'adresse ip de votre carte reseaux. sous linux, voila des exemple d'appelation clasic des carte reseaux en fonction des diffrente distribution 
	• wlp3s0 , wlan0, ensp33 → Wi-Fi
	• enp2s0 , eth0 → câble Ethernet
	• usb0 → tethering USB
	• docker0 , vmnet1 → cartes virtuelles créées par Docker/VMware
pour voir l"adresse ip de votre pc taper la commande `ip a` noté qu'une machine peut avoir plusieurs interfaces, donc plusieurs IP simultanées
![[Screenshot_2026-11-09_21-57-12.png]]
mois dans mon cas l'adresse ip a utiliser serais l'ip 192.168.100.199 celui de ma carte reseau ethernet
![[Screenshot_2026-11-09-22-00-19-214_com.termux.jpg|318]]vous pouvez voir que le ping entre le telephone et le pc passe a merveille donc il sont bien sur le meme reseaux 
ok on vas tester vite fait l'autentification par mot de passe pour voir si tout marche corectement la commande estla suivante 
```bash
ssh nom_utilisateur@address_ip
#mon nom d'utilisateur est g1m1 et mon ip est le 192.168.100.199 donc la commande pour moi est 
ssh g1m1@192.168.100.199
```

![[Screenshot_2026-11-09-22-30-25-862_com.termux.jpg|323]]ah la magie de l'informatique vous voyez que j'ai mis cette image en gros caractere pour que vous voyer bien; sur cette page, je peut literalement tout faire ce que je fait sur mon pc pop_os mais etant sur mon telephone et le plus dingue c'est que rien ne ce vois directement sur le pc c'est pas un projecteur de l'ecrant en fait 
bon comme je lais dit cette methode marche du feux de Dieu mais elle est sensible au brute force, et aussi a chaque fois je suis obliger de metre mon mot de passe la chose que j'ai remarquer aussi et pas des moindre c'est que l'adresse ip de ma machine est configurer de maniere **dynamique** ca pose un probleme enorme car au prochain redemarage ou a la prochaine reconexion du pc a ce wifi ou un autre wifi, l'ip changera et il faudra refaire la meme chose a chaque fois  mais il y a trois solution pour resoudre ca 
1. **Réservation DHCP** : la box s'engage à toujours donner la même IP à cette adresse MAC (_l'identifiant unique de la carte réseau_). mais, je ne suis pas sur que toute les box peuvent le faire 
2. **IP statique** : tu désactives DHCP pour cette interface et tu écrris l'IP à la main. Puissant, mais risque de conflit si tu choisis une IP déjà utilisée, ou hors de la plage.
les deux methode sont faisable mais elle inclus soit d'avoir un acces physique a la box (_ce qui n'est pas toujour le cas_), ou alors de creer un conflit ce qui m'amene a la troisieme solution
3. **l'utilisation d'un mSNS**: une grande entreprise du nom de  ==🔵AVAHI== a eu (je crois) a rencontrer le meme probleme que nous et il sais dit "etant donné que ca fait quelque caprice avec l'adresse IP, et si on remplacais l'IP par le nom de notre machine" c'est donc comme ca que Chaque machine annonce son nom sur le réseau, et tu peux la joindre par **nom.local** au lieu de l'IP. Le nom suit la machine même si son IP change. un géni ce gars
**regle de nomage du pc:

pas de tiret bas `_` , pas d'espaces, pas de majuscules recommandées. 
Un tiret `-` est correct. (Un nom avec `_` peut refuser de se résoudre.)
si vous ne connaisé pas le nom de votre pc, taper juste sur votre terminal la commande
```bash
hostname #et la vous verez le nom de votre pc 
```

![[Screenshot_2026-11-09-23-06-09-000_com.termux.jpg|277]]evidement ca marche parfaitement sa n'a rien a y voir mais je crois que je soufre d'insomnie il est 23 heure et moi je suis en train de taper sur mon clavier comme malade
bonjour, bonsoir et bon aprem a vous hier il étais tres tard du coup bienvenue dans cette nouvelle journée 
hier on a vue comment relier avec le hostname et l'addresse ip maintenant on verra comment s'authentifier avec des clé public 
je ne l'ai jamais faire a vrai dire donc pour moi aussi ca sera une premiere donc allons y

Bon on ne vas faire de la magie, quand on ne connais pas on ce renseigne et moi je me renseigne et moi je me renseigne au pres de mistral c'est mon nouveaux meilleur amis pour etudier vue que claude ma lacher a cause de mon age 
afin de rendre tout au propre, parton du fait qu'on vien a l'instant d'instaler termux less etape a suivre sont les suivant 
1. preparer le logiciel 
sur termux, executer les commande suivant

```bash
pkg update && pkg upgrade # met a jour les registre 
pkg install openssh # installation du chient ssh
termux-wake-lock # permet de faire en sorte que votre telephone ne pars pas en mode veille en travaillant :)
```

2.il nous faut fabriquer une paire de clés  sur le telephone c'est ca qui vas etre utiliser pour pouvoir conecter 

```bash
ssh-keygen -t ed25519
```



![[Screenshot_2026-11-10-12-43-01-001_com.termux.jpg|300]]comme vous le voyer on nous renvoie un message bizzare mais pas de panique ce message nous demande juste l'emplacement pour stocker la clé mais en fait je ne connais pas trop les emplacement sous android donc on apuis juste sur suivant pour qu'il le gère par defaut
le prochain message encore bizarre nous demande de creer un mot de passe bon je le met on se sais jamais mon mot de passe est le suivant `********`
:) 
![[Screenshot_2026-11-10-12-58-41-381_com.termux.jpg|291]]La clé a bien ete crée et stocker avant de passe a l'étape suivant, verifier si les fichier existe grace a la comande 
```bash
ls ~/.ssh
# vous devez voir : id_ed25519  et  id_ed25519.pub
```
3. deposé la clé sur le pc 
en fait c'est ici que je me suis embrouiller la derniere fois que je travaillais dessu j'avais oublier de faire ce depot donc rapeler vous bien que sans le depot, la connexion ne marchera pas la commande pour le depot est 
```bash
ssh-copy-id g1m1@192.168.X.X
```
`g1m1` : est mon nom d'utilisateur donc remplace le par le votre 
`192.168.X.X` : est l'addresse ip de votre carte reseaux si vous ne la connaisser pas encore la commande pour verifier est `ip a` (notons que nous faisons ce tp sur linux donc les commande sont des commande llinux)
une fois copier il vas vous demander le mot de passe pour la derniere fois 
sur certain appareille, `ssh-copy` n'existe pas si c'est le cas pour vous, faite la copie manuelement 
```bash
cat ~/.ssh/id_ed25519.pub | ssh g1m1@192.168.X.X \
  'mkdir -p ~/.ssh && chmod 700 ~/.ssh && cat >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys'
```
tout est bon passons au test 
```bash 
ssh g1m1@192.168.X.X
```
et voila la votre telephone se conectera automatiquement si c'est pas le cas chez vous, les cause a verifier peuvent etre 
1. le parefeux
2. le serveur eteint
3. les clé qui n'ont pas été copier
4. la conexion entre le telephone et le pc interompu

ok tout marche du mois je l'espere pour vous mais une derniere question se pose **l'adresse IP vas changer si on change de reseaux** c'est corect donc on vas faire un carnet d'adresse pour creer une variable que je vais appeler `PC` et ratacher mes parametre dont le ==🟢hostname== (_nom du PC_) a cette variable 
1) coriger le nom du pc 
```bash 
sudo hostnamectl set-hostname pop-os #remplace pop-os par le nom de votre chois mais rapeler vous des regle de AVAHI
systemctl status avahi-daemon
```
 2) modifier le carnet d'adresse sous ==🟠termux==

```bash
nano ~/.ssh/config
```

entrez la valleur suivante 

```text
Host pc
    HostName pop-os.local
    User g1m1
```

Android n'a pas de résolution mDNS native, donc la résolution de notre nom **depuis Termux ne marche pas toujour** selon la version d'Android et le réseau.

```bash
ssh pc
```

- ✅ Si ça connecte : tu as la solution universelle, garde-la.
- ❌ Si tu obtiens `Could not resolve hostname pop-os.local` : ton réseau/Android ne fait pas de mDNS c'est le cas de mon coté . Dans ce cas, revenez à l'IP dans le carnet d'adresses, et gère le changement de réseau ainsi : une ligne `HostName` à éditer à chaque nouveau réseau (10 secondes avec `nano`), ou mieux, la **réservation DHCP dans ta box** qui rend l'IP stable chez toi — et le carnet d'adresses n'a plus jamais besoin d'être touché.
sur ce cette reussite marque la fin de notre TP sa realisation a été tres tres facile mais ca reste neanmoin tres interessant 
si j'ai voulu commancer par celui la c'est parcequ'il ferai une superbe base pour la suite des TPs bonne continuation a vous et j'espere que ce guide vous sera utile



















