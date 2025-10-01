# Procédure de Déploiement

Décrivez ci-dessous votre procédure de déploiement en détaillant chacune des étapes. De la préparation du VPS à la méthodologie de déploiement continu.

## Préparation du VPS

Pour commencer je me suis connecté en ssh normal avec : ssh root@172.17.4.7.
Une fois connecté j'ai donc téléchargé Aappanel avec : URL=https://www.aapanel.com/script/install_7.0_en.sh && if [ -f /usr/bin/curl ];then curl -ksSO "$URL" ;else wget --no-check-certificate -O install_7.0_en.sh "$URL";fi;bash install_7.0_en.sh aapanel

Une fois installé j'ai donc reçu :
aaPanel Internet Address: https://90.80.241.65:26972/f2caf6eb
aaPanel Internal Address: https://172.17.4.7:26972/f2caf6eb
username: wurfnusj
password: d2a7973a

Je me suis rendu sur https://172.17.4.7:26972/f2caf6eb

Une fois dessus j'ai téléchargé les packages LNMP avec les configs la :
-Nginx
-Mysql 5.7
-PHP 8.3
-Phpmyadmin

J'ai ensuite ajouté un site web avec mon IP

J'ai désactivé le Anti-Xss attack



## Méthode de déploiement


Sur le serveur j'ai init le Dépôt avec :

mkdir -p /var/depot_git
cd /var/depot_git
git init --bare


Ensuite dans mon dossier j'ai init aussi le dépôt :

git init
git remote add vps root@172.17.4.7git remote add vps:/var/depot_git

Ensuite j'ai ajouté les modifs :

git add .
git commit -m "Feat: add first commit"
git push vps main

Ensuite sur le serveur j'ai été dans :

cd /www/wwwroot/137.74.43.225

Pour faire :

git --work-tree=/www/wwwroot/172.17.4.7 --git-dir=/var/depot_git checkout -f main



Ensuite sur l'url : http://172.17.4.7/dashboard

J'ai bien la possibilité de me connecter avec exemple email : admin@ht-buggy-wapp.fr  mdp : azertyuiop

J'ai bien l'interface qui s'affiche ici :

public/images/Page_admin.28.01.png
public/images/Website.28.44.png
public/images/database_phpmyadmin.29.21.png
public/images/aapannel_admin.30.00.png

J'avais des probleme avec nginx j'ai ajouté la ligne ici présente à la config  :

    location / {
        try_files $uri $uri/ /index.php$is_args$args;
    }
Que j'ai trouvé sur :

https://serverfault.com/questions/893546/nginx-try-files-location-configuration

