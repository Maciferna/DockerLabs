Maquina "AnonymousPingu" de [DockerLabs](https://dockerlabs.es)

Autor: [El Pingüino de Mario](https://www.youtube.com/channel/UCGLfzfKRUsV6BzkrF1kJGsg)

Dificultad: Fácil

![dock](./img/dock.png)

# RECONOCIMIENTO

Comenzamos haciendo un escaneo de `nmap`:

```css
nmap -p- -n -vvv -sSVC -Pn --open --min-rate 5000 <ip> -oN escaneo.txt
```

```ruby
# Nmap 7.94SVN scan initiated Mon Sep  9 23:17:04 2024 as: nmap -p- -n -vvv -sSVC -Pn --open --min-rate 5000 -oN escaneo.txt 172.17.0.2
Nmap scan report for 172.17.0.2
Host is up, received arp-response (0.000016s latency).
Scanned at 2024-09-09 23:17:05 -03 for 8s
Not shown: 65533 closed tcp ports (reset)
PORT   STATE SERVICE REASON         VERSION
21/tcp open  ftp     syn-ack ttl 64 vsftpd 3.0.5
| ftp-syst: 
|   STAT: 
| FTP server status:
|      Connected to ::ffff:172.17.0.1
|      Logged in as ftp
|      TYPE: ASCII
|      No session bandwidth limit
|      Session timeout in seconds is 300
|      Control connection is plain text
|      Data connections will be plain text
|      At session startup, client count was 4
|      vsFTPd 3.0.5 - secure, fast, stable
|_End of status
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
| -rw-r--r--    1 0        0            7816 Nov 25  2019 about.html
| -rw-r--r--    1 0        0            8102 Nov 25  2019 contact.html
| drwxr-xr-x    1 0        0             118 Jan 01  1970 css
| drwxr-xr-x    1 0        0               0 Apr 28 18:28 heustonn-html
| drwxr-xr-x    1 0        0             574 Oct 23  2019 images
| -rw-r--r--    1 0        0           20162 Apr 28 18:32 index.html
| drwxr-xr-x    1 0        0              62 Oct 23  2019 js
| -rw-r--r--    1 0        0            9808 Nov 25  2019 service.html
|_drwxrwxrwx    1 33       33              0 Sep 10 02:07 upload [NSE: writeable]
80/tcp open  http    syn-ack ttl 64 Apache httpd 2.4.58 ((Ubuntu))
|_http-title: Mantenimiento
| http-methods: 
|_  Supported Methods: GET POST OPTIONS HEAD
|_http-server-header: Apache/2.4.58 (Ubuntu)
MAC Address: 02:42:AC:11:00:02 (Unknown)
Service Info: OS: Unix

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Mon Sep  9 23:17:13 2024 -- 1 IP address (1 host up) scanned in 9.18 seconds
```

Como vemos tenemos el puerto 80 abierto y el ftp, el cual tiene login anonimo y además parece que estamos dentro de la propia página, para confirmarlo podemos hacer uso de `gobuster` y ver que directorios o archivos tiene la máquina:

```css
 gobuster dir -u http://<ip> -w <wordlist> -x php,html,txt
```

```ruby
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://172.17.0.2
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,txt,php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 275]
/.php                 (Status: 403) [Size: 275]
/index.html           (Status: 200) [Size: 20162]
/images               (Status: 301) [Size: 309] [--> http://172.17.0.2/images/]
/about.html           (Status: 200) [Size: 7816]
/contact.html         (Status: 200) [Size: 8102]
/upload               (Status: 301) [Size: 309] [--> http://172.17.0.2/upload/]
/service.html         (Status: 200) [Size: 9808]
/css                  (Status: 301) [Size: 306] [--> http://172.17.0.2/css/]
/js                   (Status: 301) [Size: 305] [--> http://172.17.0.2/js/]
Progress: 166877 / 882244 (18.92%)
===============================================================
Finished
===============================================================
```

Como podemos ver estamos en la propia página, por lo que teniendo en cuenta que la carpeta `upload` es accesible desde el navegador y que podemos escribir en ella con ftp, tenemos que subir a traves de ftp un php malicioso que nos permita ejecutar comandos dentro de la máquina. Para esto podemos usar el script que hice para esta máquina:

[script](https://github.com/Maciferna/Dockerlabs/blob/main/maquina-anonymouspingu/scrips/intrusion.sh)