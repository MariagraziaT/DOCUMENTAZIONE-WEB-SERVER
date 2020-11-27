#Come creare un WEB-SERVER  utilizzando una macchina Linux (in questo caso una macchina virtuale di 

tipo Ubuntu 20-04 64 Bit).

##PROCESSO DA ATTUARE 

la prima operazione che eseguo e il login (adminuser e password:adminuser)

Successivamente abilito tramite il comando sudo -i ; la funzione amministratore, che mi da tutti i 

permessi.
##1.PACCHETTI DA INSTALLARE
Ipacchetti da installare sono; 
apache2 comandi:
    
    sudo apt-get install apache2

##2.CONFIGURAZIONE IP
Modifico la mia macchina(CONFIGURAZIONE DHCP4), aggiungendo un  ip statico, con il comando;
     nano /etc/netplan/00-installer-config.yaml 
apro il file di configurazione e lo modifico a dovere.
: warning:  per verifichare se le modifiche applicate funzionino uso il comando:
     
     sudo netpaln try
     
se non funziona utilizzo il comando :
     
     sudo netplan apply
Un ulteriore metodo di verifica è inserire nel URL di un qualsiasi broswere  l'indirizo ip della macchina, di default dovrebbe caicarsi la pagina index di apache2
   
#3.CREAZIONE SITI

     cd /etc/apache2/sites-available
     sudo cp 000-default.conf 001-default.conf
     sudo nano 001-deafult.conf  
     
 Il file 001-default.conf che è la copia del file 000-default.conf deve essere modificato così:
 
     DocumentRoot /var/www/SitoA/web
     ServerName sitoa-113.virtual.marconi
     ErrorLog /var/www/SitoA/log/error.log
     CustomLog /var/www/SitoA/log/access.log combined
  
sudo systemctl reload apache2
sudo a2ensite 001-default.conf

cd /var/www/ //ENTRO NELLA CARTELLA WWW
sudo mkdir SitoX  //CREO CARTELLA X
sudo mkdir log  //CREO CATELLA LOG

cd /var/www/SitoA/web/ //NELLA CARTELLLA 
sudo nano HTML1.html  //CERO IL FILE RELATIV

##4.CREAZIONE UTENTI
Adesso per gestire l'accesso da parte di un utente alla cartella sel sito utilizzo il comando:
     
     sudo useradd -s /bin/bash -d /var/www/SitoA -m usersitoX
     sudo passwd usersitoX





--------------------------------------------------
