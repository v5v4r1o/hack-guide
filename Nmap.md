**Nmap**  
**EJEMPLOS**

* **nmap \--script "vuln" \-p445 1.2.3.4** (Escaneo de vulnerabilidades)  
* **nmap \-p- \-sS \--min-rate 2000 \-Pn \-n \--open \-vvv 1.2.3.4 \-oG portscan** (Escanea todo el rango de puertos \-p-, con el Stealth Scan \-sS, a 200 paquetes por segundo \--min-rate 2000, sin hacer host discovery \-Pn, ni resolucion dns \-n, notificar los puertos abiertos \--open, triple verbose \-vvv, de la ip dada, guardar los resultados en formato grepeable en el archivo portscan)  
* **nmap \-p1,2,3,4 \-sCV 1.2.3.4 \-oN targeted** (Lanza un conjunto de scripts de reconocimiento para obtener versiones con \-sCV sobre los puertos obtenidos en el comando anterior \-p1,2,3,4 y exporta las evidencias en el archivo targeted en formato nmap)  
* **nmap \-sU \--top-ports 200 \--min-rate=500 \-Pn 1.2.3.4** (Escaneo de los 200 puertos más usados en udp a 5000 paquetes por segundo)  
* **nmap \-sn \-PS 10.10.10.10** (Realiza **host discovery** con ping packets con \-sn pero al utilizar **\-PS** se anula el contenido icmp de los paquetes y únicamente se envía un paquete con **SYN** al puerto 80 de la máquina en cuestión.
* **nmap \-sn \-PA 10.10.10.10** (**Host discovery** pero enviando un paquete **ACK** esperando un paquete **RST**, no es muy eficiente porque **este tipo de tráfico suele estar bloqueado.** Puede indicar que hay un **firewall por detrás si ACK está siendo bloqueado pero SYN no**)  
* **nmap \-p445 \--script smb-enum-sessions \--script-args smbusername=administrator,smbpassword=smbserver\_771 demo.ine.local** ( –script smb-enumsessions es un script que puede requerir de credenciales para enumerar sesiones del protocolo smb especificadas con: –script-args smbusername=admin,smb\_password=pass)

 

* **Parámetros:**  
  * \-F : fast scan, 100 puertos más usados  
  * \-O : Identifica el SO  
  * \-iL \<path\_to\_file\>: Permite crear una lista de ips en un archivo para analizar.  
  * –osscan-guess : Escaneo agresivo para averiguar el SO  
  * –version-intensity 8: Escaneo con agresividad 8 para ver las versiones  
  * –script=http-\* : ejecuta todos los scripts relacionados con http  
  * –script=http-enum : ejecuta el script http-enum  
  * –script=discovery : Ejecuta los scripts de la categoría discovery  
  * \-f : Fragmentación de los paquetes para evadir Firewall o IDS.  
  * –mtu 32: MTU(Maximun transmitted unit) Nos indica el tamaño máximo en bytes de paquete a enviar. Esto nos sirve a la hora de desfragmentar paquetes.  
  * –ttl: Time to live  
  * –data-length 200: El tamaño del header es de 200 bits  
  * \-D 10.10.10.1 : Spoofing con la/s ip/s indicada/s. por ejemplo el gateway. Permite pasarse por las ips como si fueran el source de la petición.  
  * \-g 1234: La petición sale del puerto 1234\. Si fuera por ejemplo en 53 podría parecer una petición DNS.  
  * \-T\<0-5\>: distintos templates de velocidad del escaneo 0 \-\> Paranoid, 5 \-\> Insane.  
  * –host-timeout 5s : Espera hasta 5 segundos por la respuesta del host.  
  * –scan-delay 10s: Tiempo de espera entre paquetes enviados.  
* **Notes:**  
  * Cuando nmap devuelve **puertos filtered** puede indicar **firewall u otra medida de seguridad**, en caso de que **no haya nada**, nmap debería de poder determinar que el puerto está **closed.**  A nivel de paquetes, si no hay un firewall el sistema debería de responder con RST para especificar que el puerto está cerrado si se trata de un SYN scan.  
  * Si se ejecuta como **root**, se realiza **por defecto un SYN scan**, si se realiza **sin privilegios** se hace un **TCP scan.**  
  * **Firewall Detection and Evasion**:  
    * Al **escanear con ACK** podemos comprobar si existe un firewall por detrás que esté filtrando los puertos. Para **evadir el firewall o IDS** podemos especificar la opción **\-f para fragmentar los paquetes**.


