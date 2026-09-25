1. Configuració d'Apache i VirtualHosts (HTTP)

L'objectiu d'un VirtualHost és ensenyar a l'Apache a allotjar i separar múltiples llocs web diferents dins del mateix ordinador.

Estructura: Creem una carpeta pròpia per al projecte web dins de la ruta pública d'Apache (/var/www/html/pc8).

Arxiu de configuració: Creem un fitxer .conf a la ruta /etc/apache2/sites-available/. Dins d'ell declarem que escolte pel port 80, li assignem el nom de domini amb ServerName i li indiquem on estan els arxius amb DocumentRoot.

Activació: Usem l'orde a2ensite per a encendre la configuració i reiniciem el servei d'Apache perquè els canvis facen efecte.

Resolució local: Per a poder entrar escrivint el nom del domini en compte de la IP, editem l'arxiu del sistema /etc/hosts i emparellem la nostra IP local amb el domini (ex. pc8.daw).



2. Seguretat HTTPS i Certificats Autofirmats
Per a protegir el tràfic de dades, activem l'encriptació en el nostre servidor.

Creació de claus: Habilitem el mòdul de seguretat d'Apache (a2enmod ssl). Després usem OpenSSL per a generar el nostre propi certificat de seguretat casolà, creant una clau privada (.key) i un certificat públic (.crt).

VirtualHost Segur: Dupliquem l'arxiu de configuració anterior i adaptem la còpia perquè escolte pel port segur 443. A l'interior, afegim l'orde SSLEngine on i les rutes cap als dos arxius de seguretat que acabem de crear.

Redirecció Forçada: Obrim l'arxiu antic del port 80 i afegim la línia Redirect permanent / [https://pc8.daw/](https://pc8.daw/). Així garantim que qualsevol visita que arribe per HTTP siga expulsada automàticament cap a la versió xifrada.



3. Gestió amb phpMyAdmin
Instal·lem esta interfície gràfica a través de la terminal per a administrar les bases de dades còmodament des del navegador, evitant haver de picar codi SQL a la consola constantment.

Instal·lació: Usem el gestor de paquets APT per a descarregar-lo al costat de les extensions necessàries de PHP.

Enllaç amb Apache: Durant l'assistent d'instal·lació és obligatori seleccionar apache2 marcant-lo amb la barra d'espai perquè s'integre amb el nostre servidor.

Configuració Interna: Acceptem l'ús de dbconfig-common per a que el propi phpMyAdmin cree les seues taules de funcionament internes.

Accés Final: Reiniciem l'Apache i accedim a http://localhost/phpmyadmin utilitzant les credencials del nostre usuari root de MySQL.