***DOOCUMENTAZIONE WEB-SERVER***
>Come creare un _WEB-SERVER_  utilizzando una macchina Linux (in questo caso una macchina virtuale di tipo Ubuntu 20-04 64 Bit).

**Passaggi da seguire** 	:clipboard: 

:one: [Log-in](#**login**)	:unlock: <br>
:two: [Pacchetti da installare](#**PACCHETTI-DA-INSTALLARE**) :package: <br>
:three:[Configurazione DHCP](#**CONFIGURAZIONE-DHCP4**) 	:gear:<br>
:four:[Creazione sito](#**CREAZIONE-SITO**) :hammer_and_wrench:  <br>
:five:[Abilitazione sito](#**ABILITO-I-SITI**):heavy_check_mark:<br>
:six: [Creazione nuovi utenti](#**CREAZIONE-UTENTI**) :busts_in_silhouette:<br>


la prima operazione che eseguo e il ##**login** (adminuser e password:adminuser), bisogna utilizzare un utente di tipo root. 

Successivamente abilito tramite il comando `sudo -i` ; la funzione amministratore, che mi da tutti i 
permessi.

## **PACCHETTI DA INSTALLARE**

I pacchetti da installare sono; 

:small_orange_diamond: ssh:
 
 >apt-get install openssh-server.
 
:small_orange_diamond: apache2 :  
 
 > apt-get install apache2
 
Eseguendo questo comando verrà installato il web-server Apache.

:small_orange_diamond: FTP: 

>apt-get install vsftpd
 
Questo comando permettera l'istallazione di un client FTP e di usufruire dei comandi FTP da remoto.


Un metodo di ***verifica*** è inserire nel URL di un qualsiasi broswere l'indirizo ip della macchina, di default dovrebbe caicarsi la pagina index di apache2.


## **CONFIGURAZIONE DHCP4**

Modifico la mia macchina, aggiungendo un  ip statico, con il comando;

     >nano /etc/netplan/00-installer-config.yaml 
     
apro il file di configurazione e lo modifico a dovere;

Nel mio caso ad esempio;

>network:
>  renderer: networkd
>  ethernets:
>    enp0s3:
>      addresses: [172.16.29.122/16]
>      gateway4: 172.16.1.7
>      nameservers:
>        search: [virtual.marconi]
>        addresses: [172.16.1.18, 172.16.1.10] 
>  version: 2

Applico le modifiche con comando;

>sudo netplan apply 

Verifichare se le modifiche applicate funzionino con il comando:

> netpaln try
         
Per ***verificare*** che i comandi siano applicati in modo giusto, quindi che la configurazione è andata a buon fine, digito il comando:

>ip address

Che mi mostra l'IP.
 
## **CREAZIONE SITO**

>cd /var/www/ 

ENTRO NELLA CARTELLA WWW

>sudo mkdir SitoX  

CREO CARTELLA sitoX DOVE VERRANNO CREATE ALTRE DUE CARTELLE UNA PER IL LOG UNA PER WEB
 
>sudo mkdir /var/www/SitoX log  

CREO CATELLA LOG

>sudo mkdir /var/www/SitoX web 

CREO LA CARTELLA WEB ALL'INTERNO METTERO IL FILE.HTML CHE CONTERRA L'HTML DEL SITO

>cd /var/www/SitoX/web/ 

ENTRO NELLA CARTELLLA WEB

>sudo nano HTML1.html  

CERO IL FILE html


Per ***verificare*** ese i comandi sono stati eseguiti correttamente basta utilizzare il comando `ls` all interno delle cìvarie cartelle e vedere se sono presenti i file/le cartelle create. 

## **ABILITO I SITI**

>cd /etc/apache2/sites-available

Visualizzo quali siti di apache sono abilitati
 
 >sudo cp 000-default.conf 001-default.conf
 
 Copio il contenuto di in 
  
  >sudo nano 001-deafult.conf  
  
  tramite nano modifico il contenuto del file,
  
  Nel mio caso le modifiche sono queste:
 
  >   DocumentRoot /var/www/SitoX/web
  >  ServerName sitoa-122.virtual.marconi
  >   ErrorLog /var/www/SitoX/log/error.log
  >  CustomLog /var/www/SitoX/log/access.log combined
  
sudo systemctl reload apache2
sudo a2ensite 001-default.conf

per ***verificare***  se il sito creato e stato abilitato, inserisco nel URL di un broswew qualsiasi 

il ServerName, nel mio caso;

>ServerName sitoa-122.virtual.marconi

 ## **CREAZIONE UTENTI**

Per creare un utente che anno accesso alla cartells del sitoX si utilizza il comando :

   >sudo useradd -s /bin/bash -d /var/www/Sitox -m usersitoX

poi successivamente per modificare la password dell utente creato si usa il comando:

>sudo passwd usersitoX

per ***verificare*** se l'utente e stato creato, accedo alla macchina con nuovo utente e passuord .




--------------------------------------------------


>https://wiki.ubuntu-it.org/Server/Samba#Installazione

***SAMBA***<br>
:diamond_shape_with_a_dot_inside: [cos'è samba?](#**SAMBA**) :question:<br>
:diamond_shape_with_a_dot_inside: [installazione](#**INSTALLAZIONE**) 	:package: <br>
:diamond_shape_with_a_dot_inside: [configurazione](#**CONFIGURAZIONE**) :gear:<br>
:diamond_shape_with_a_dot_inside: [come gestire la condivisione](#**GESTIONE-DELLA-CONDIVISIONE**) :computer:<br>

## **SAMBA**<br>
Samba è una suit di strumenti, che permette tramite rti sia windows che linux la condivisione 

## **INSTALLAZIONE** 
Assicurarsi prima di installare il pacchetto di samba, che sì sia fatto l'aggiornamento della propria macchina, tramite il comando `sudo apt-get update`.<br>
Procediamo poi con l'installazione del pacchetto

 >sudo apt-get install samba
## **CONFIGURAZIONE**

## **GESTIONE DELLA CONDIVISIONE**

