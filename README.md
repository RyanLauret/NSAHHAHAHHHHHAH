# T-NSA-700-RUN_2

Le groupe réalisant ce projet est composé de :

- [Jeremy Lebon](https://www.linkedin.com/in/jeremy-lebon/ "Profil LinkedIn")
- [Pierre Hung Tsang-tung](https://www.linkedin.com/in/hung-tsang-tung/ "Profil LinkedIn")
- [Ryan Lauret](https://www.linkedin.com/in/ryan-lauret-232559197/ "Profil LinkedIn")


# Installation de Gitlab sur Google Cloud

I) Prérequis 

  1) Connexion avec un compte Google
  2) Accepte les conditions pour les 60 jours d'essai
  3) Creation d'un Virtual Machine
 
II) Creation d'une machine 

  1) Aller sur  https://console.cloud.google.com/compute/instances
  2) Selectionner Create
  3) Configuerer la machine 
  
   ![image](https://user-images.githubusercontent.com/72122216/217456031-69eda552-dc0a-433f-9625-bbdab20c2aad.png)![image](https://user-images.githubusercontent.com/72122216/217456093-6666a262-ee4e-4eb0-8858-07585e672c80.png)
![image](https://user-images.githubusercontent.com/72122216/217456203-1a66a695-fb27-4bf7-b760-678c26c01cd4.png)
![image](https://user-images.githubusercontent.com/72122216/217456729-f864edd0-34e6-46cf-87f8-d225de06aa18.png)
![image](https://user-images.githubusercontent.com/72122216/217456804-000357a9-9f87-4ebd-9584-91fd416082ba.png)

  4) Une fois la machine crée récuperer External IP
  5) mettre en SSH
  
  ![image](https://user-images.githubusercontent.com/72122216/217458627-1947bd9e-aef3-45e4-9561-cdc050f267d6.png)

III) Installation de Gitlab

  1) Telechargement des mises à jours, openssh et postfix
  
    sudo apt-get update
    sudo apt-get install -y curl openssh-server ca-certificates perl
    sudo apt-get install -y postfix

  2) Recherche des packages de Gitlab
  
    curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
    
  3) Installation gitlab
  
    sudo EXTERNAL_URL="https://'mettre_son_external_ip" apt-get install gitlab-ee

  4) Une fois installer, changer l'external_url dans le fichier "/etc/gitlab/gitlab.rb"
  
    sudo nano /etc/gitlab/gitlab.rb

  5) Chercher la ligne "external_url"
  
    external_url "https://'mettre_son_external_ip'"
  
  6) Reconfigurer gitlab
  
    sudo gitlabctl reconfigure

IV) Changement de mot de passe Gitlab

  1) Interraction avec Gitlab en ligne de commande
  
    gitlab-rails console -e production
  
  
  2) chercher l'utilisateur "root"
  
    u = User.where(id:1).first
    
  3) Changement de mot de passe
    
    u.password = 'le mot de passe'
    
   4) Confirmation du changement mot de passe
   
     u.password_confirmation = 'le mot de passe'
     
   5) sauvegarder
   
     u.save!
      
