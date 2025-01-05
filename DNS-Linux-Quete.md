# DNS sur Linux - Quête

Voici les différentes étapes, qui suivent le tuto proposé sur le site Linux Techi. Toutes les actions se font en tant que root sur un Debian 12 CLI.

1) D'abord on s'assure qu'internet soit disponible avant de lancer le téléchargement de Bind9. Dans notre cas a fallu ajouter la passerelle dans le fichier ``/etc/network/interfaces.d/`` pour qu'internet fonctionne :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/cbfa9995-6c4d-481b-8982-801b0582fde1" alt=""></p><br><br><br>

2) Lancer les commandes ``apt update`` et ``apt install -y bind9 bind9utils bind9-doc dnsutils`` pour installer Bind9 :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/334246a7-201e-4db2-95b8-09314d560ac6" alt=""></p><br><br><br>

3) Modifier le fichier ``/etc/bind/named.conf.options`` comme indiqué dans le tuto, en personnalisant avec les paramètres de la quête :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/be921cef-aa8d-47a1-964b-d05b7e6cbcaf" alt=""></p><br><br><br>

4) Modifier le fichier ``/etc/bind/named.conf.local`` comme indiqué dans le tuto, en personnalisant avec les paramètres de la quête :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/5c5febea-5664-4375-a704-ee67a2f9129f" alt=""></p><br><br><br>

5) Dans le dossier ``/etc/bind/``, copier le fichier ``db.local`` et le modifier comme indiqué dans le tuto, en personnalisant avec les paramètres de la quête :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/d3e7ad91-8043-42c8-a702-6880a481ebf2" alt=""></p><br><br><br>

6) Même procédure que le point n°5, cette fois avec la  copie du fichier ``db.127`` puis sa modification, tel qu'indiqué dans le tuto :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/ee3a471f-b105-41ca-a31b-b8c04844c4d5" alt=""></p><br><br><br>

7) Dans le fichier ``/etc/default/named``, on ajoute la prise en compte de l'IPv4 dans les paramètres de Bind
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/7ace2e38-bd9c-4ffc-83df-d1d919269cc2" alt=""></p><br><br><br>

8) On active ensuite le service Bind et on vérifie le statut : ici il y a un souci, l'IPv4 semble ne pas être pris en compte par Bind :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/b0904100-f29c-4181-9407-5e02af474ee6" alt=""></p><br><br><br>

9) Le reboot de la machine corrige ce problème :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/1a880909-f32c-4fe0-b06d-7607f0803385" alt=""></p><br><br><br>

10) On autorise ensuite l'utilisation du port 53, pour que la commande fonctionne il a fallu préalablement installer le service ufw avec la commande ``apt install ufw`` :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/b8a1f0e0-6ed7-4388-8e84-538f87f0da69" alt=""></p><br><br><br>

11) Pour vérifier la syntaxe des fichiers de zones de recherche directe et inversée, on utilise la commande ``named-checkzone`` et on vérifier qu'elle renvoie ``OK``
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/615b56af-4e14-44d9-aab2-1f433dc77121" alt=""></p><br><br><br>

12) Dans le fichier ``/etc/resolv.conf``, on ajoute les infos telles qu'indiquées par le tuto :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/b5342ae2-f46f-43ff-931c-603123c02c42" alt=""></p><br><br><br>

13) On utilise la commande ``dig`` et ``dig -x`` pour vérifier que les paramètres DNS sont bons :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/fa6ccabc-67e6-4cb2-8105-e4068689aea4" alt=""></p><br><br><br>

14) On fait de même avec la commande ``nslookup`` :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/55edb657-14e3-4461-a0fd-d8ba5d03d9fa" alt=""></p><br><br><br>

15) Sur une VM Ubuntu, on met à jour les paramtères IPv4 pour que le serveur DNS soit bien pris en compte par la machine :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/ce6852d5-bc5f-40ff-b933-6b41b3255760" alt=""></p><br><br><br>

16) On teste enfin que tout est OK avec des commandes ``ping`` et ``nslookup`` :
<br><p align="center"><img width="70%" src="https://github.com/user-attachments/assets/5e9f01ea-2291-42c3-ba95-4eaf2f34b767" alt=""></p><br><br><br>

