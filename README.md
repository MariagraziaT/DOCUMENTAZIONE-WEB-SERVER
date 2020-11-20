PROCESSO DA ATTUARE 
per far si che si ottenga il risultato richiesto, usufruisco di una macchina virtuale di tipo Ubuntu 20-04 64 Bit.
la prima operazione che eseguo e il login (adminuser e password:adminuser)
Successivamente abilito tramite il comando sudo -i ; la funzione amministratore, che mi da tutti i permessi.
Modifico la mia macchina(CONFIGURAZIONE DHCP4), aggiungendo un  ip statico, con i comando nano /etc/netplan/00-installer-config.yaml  apro il file di configurazione e lo modifico a dovere.
poi dopo aver modificto il file testo se le modifiche applicate funzio nino tramite i due comandi:sudo netpaln try.
come secondo passo installo apache sudo apt-get install apache2;
successivamente procedo con la creazioe dei 3 siti, A B e C.

cd /etc/apache2/sites-available
sudo cp 000-deafult.conf 001-default.conf
sudo nano 001-deafult.conf      //APRO IL FILE 

//BISOGNA MODIFICARE IN QUESTO MODO IL FILE 
     DocumentRoot /var/www/SitoA/web
     ServerName sitoa-113.virtual.marconi
     ErrorLog /var/www/SitoA/log/error.log
     CustomLog /var/www/SitoA/log/access.log combined
  
sudo systemctl reload apache2
sudo a2ensite 001-default.conf

cd /var/www/ //ENTRO NELLA CARTELLA WWW
sudo mkdir SitoA  //CREO CARTELLA A
sudo mkdir log  //CREO CATELLA LOG

cd /var/www/SitoA/web/ //NELLA CARTELLLA 
sudo nano HTML1.html  //CERO IL FILE RELATIV

Questi comandi devono essere ripetuti anche per il sito B e C

Adesso per gestire l'accesso da parte di un utente alla cartella sel sito utilizzo il comando:
sudo useradd -s /bin/bash -d /var/www/SitoA -m usersitoX
sudo passwd usersitoX





--------------------------------------------------
per creare utenti

sudo useradd -s /bin/bash -d /var/www/sitoa -m usersitoa
sudo passwd usersitoa

contenuto del file di configurazione di vsftp

listen=yes

listen_ipv6=NO

anonymous_enable=NO

local_enable=YES

write_enable=YES

local_umask=022

dirmessage_enable=YES

use_localtime=YES

xferlog_enable=YES

connect_from_port_20=YES
 
xferlog_file=/var/log/vsftpd.log

xferlog_std_format=YES

ftpd_banner=Welcome to our  FTP service.

chroot_local_user=YES

local_root=/var/www/$USER

user_sub_token=$USER

allow_writeable_chroot=YES

secure_chroot_dir=/var/run/vsftpd/empty

pam_service_name=vsftpd

rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem

rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key

ssl_enable=NO

session_support=YES

log_ftp_protocol=YES
