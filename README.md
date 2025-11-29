# Raport Lucrare de Laborator Nr. 1

## Informații generale

**Student:** Darii Dumitru
**Grupa:** IAFR2301
**Profesor:** Borș Dumitru
**Disciplina:** Containerizare și virtualizare

---

## Tema lucrării

**Server virtual (instalarea Debian, LAMP și phpMyAdmin)**

---

## 1. Scopul și sarcinile lucrării

### Scopul lucrării
Studierea procesului de instalare și configurare a unui server virtual bazat pe sistemul de operare Debian, instalarea și configurarea pachetului LAMP (Linux, Apache, MySQL, PHP), precum și a sistemului de administrare a bazelor de date phpMyAdmin. De asemenea, familiarizarea cu utilizarea sistemului de control al versiunilor Git și a platformei GitHub.

### Sarcinile lucrării
- Instalarea și configurarea QEMU pentru virtualizare
- Crearea și configurarea unui repozitoriu pe GitHub
- Instalarea sistemului de operare Debian pe mașina virtuală
- Instalarea și configurarea pachetului LAMP (Apache, MySQL/MariaDB, PHP)
- Instalarea și configurarea phpMyAdmin
- Documentarea procesului și salvarea rezultatelor pe GitHub

---

## 2. Descrierea etapelor realizate

### 2.1 Pregătirea mediului
S-a descărcat imaginea de instalare Debian de pe site-ul oficial și s-a salvat în directorul de lucru `~/lab1/`.

### 2.2 Instalarea și configurarea QEMU
S-a instalat QEMU folosind comenzile:
```bash
sudo apt update
sudo apt install qemu qemu-kvm
```

Instalarea a fost verificată cu comanda `qemu-system-x86_64 --version`.

### 2.3 Crearea repozitoriului pe GitHub
S-a creat un repozitoriu nou cu numele `laborator1` pe GitHub. Repozitoriul a fost clonat local, s-a creat structura de directoare și fișierul `.gitignore` pentru a exclude fișierele `.iso`, `.img`, `.qcow2`, `.log`, `.tmp`.

### 2.4 Crearea discului virtual și instalarea Debian
S-a creat un disc virtual de 8 GB folosind comanda:
```bash
qemu-img create -f qcow2 debian_lab1.img 8G
```

S-a pornit procesul de instalare Debian și s-au parcurs pașii de configurare a sistemului de operare.

### 2.5 Instalarea serverului LAMP
După autentificarea în Debian, s-au instalat componentele LAMP:
- Actualizarea sistemului
- Instalarea Apache și verificarea funcționării cu `curl http://localhost`
- Instalarea MariaDB și securizarea acesteia cu `mysql_secure_installation`
- Instalarea PHP și a modulelor necesare
- Verificarea funcționării PHP prin crearea fișierului `info.php`

### 2.6 Instalarea phpMyAdmin
S-a instalat phpMyAdmin, s-a selectat serverul web Apache2 în timpul configurării, s-a configurat baza de date și s-a repornit Apache. Funcționarea a fost verificată prin accesarea interfeței web.

### 2.7 Salvarea rezultatelor pe GitHub
Toate modificările, capturile de ecran și documentația au fost adăugate în repozitoriu și trimise pe GitHub.

---

## 3. Capturi de ecran

### 3.1 Instalarea Debian

![image1](/images/image1.png)
*Ecranul de pornire al instalatorului Debian*

![image2](/images/image2.png)
*Configurarea partițiilor și a utilizatorului în timpul instalării (1)*

![image3](/images/image3.png)
*Configurarea partițiilor și a utilizatorului în timpul instalării (2)*

![image4](/images/image4.png)
*Finalizarea instalării Debian și log in cu user-ul creat*

### 3.2 Instalarea și verificarea Apache

![image5](/images/image5.png)
*Serverul LAMP funcționează - `curl http://localhost`*

### 3.3 Verificarea PHP

![image6](/images/image6.png)
*Pagina implicită Apache ("It works!") afișată în browser*

![image7](/images/image7.png)
*Pagina phpinfo() cu informațiile despre configurația PHP*

### 3.4 Interfața phpMyAdmin

![image8](/images/image8.png)
*Ecranul de login phpMyAdmin*

![image9](/images/image9.png)
*Interfața principală phpMyAdmin după autentificare*

### 3.5 Structura repozitoriului GitHub

![image10](/images/image10.png)
*Structura fișierelor și directoarelor din repozitoriul GitHub*

---

## 4. Link către repozitoriul GitHub

[Repository URL:](https://github.com/dimm-sch/laborator1)

---

## 5. Răspunsuri la întrebările de control

### 1. Ce este virtualizarea și de ce este utilizată?

Virtualizarea este o tehnologie care permite crearea unor versiuni virtuale ale resurselor hardware, cum ar fi servere, stații de lucru, sisteme de stocare sau rețele. În esență, virtualizarea ne permite să rulăm mai multe sisteme de operare și aplicații pe același hardware fizic, izolate unele de altele.

Virtualizarea este utilizată pentru:
- Optimizarea resurselor hardware prin rularea mai multor mașini virtuale pe același server fizic
- Izolarea mediilor de lucru și testare fără a afecta sistemul principal
- Reducerea costurilor prin consolidarea serverelor
- Crearea de medii sigure pentru testarea software-ului
- Facilitarea backup-ului și recuperării sistemelor

### 2. Ce funcții îndeplinește QEMU?

QEMU (Quick Emulator) este un emulator și virtualizator open-source care îndeplinește următoarele funcții:
- Emularea hardware-ului complet, permițând rularea sistemelor de operare pentru diferite arhitecturi
- Virtualizarea sistemelor, oferind performanțe apropiate de cele native când este folosit împreună cu KVM
- Crearea și gestionarea discurilor virtuale în diverse formate (qcow2, raw, etc.)
- Redirecționarea porturilor și configurarea rețelelor virtuale
- Suportul pentru diverse dispozitive virtuale (CD-ROM, hard disk-uri, interfețe de rețea)

### 3. Ce reprezintă pachetul LAMP?

LAMP este un acronim care reprezintă un stack de tehnologii open-source utilizat frecvent pentru dezvoltarea și găzduirea aplicațiilor web:
- **L**inux - sistemul de operare
- **A**pache - serverul web care procesează cererile HTTP
- **M**ySQL/MariaDB - sistemul de gestiune a bazelor de date relaționale
- **P**HP - limbajul de programare server-side pentru crearea conținutului dinamic

Acest pachet oferă toate componentele necesare pentru a rula aplicații web dinamice și a gestiona baze de date.

### 4. Cum se poate verifica funcționarea Apache și PHP?

**Verificarea Apache:**
- Din linia de comandă: `curl http://localhost` sau `systemctl status apache2`
- Din browser: accesarea adresei `http://localhost` sau `http://<ip_server>`, unde ar trebui să apară pagina implicită Apache
- Verificarea procesului: `ps aux | grep apache2`

**Verificarea PHP:**
- Crearea unui fișier de test `info.php` în directorul `/var/www/html/` cu conținutul `<?php phpinfo(); ?>`
- Accesarea în browser la adresa `http://localhost/info.php`
- Verificarea versiunii din linia de comandă: `php -v`
- Pagina phpinfo() va afișa toate informațiile despre configurația PHP, module instalate și setări

### 5. La ce folosește phpMyAdmin?

phpMyAdmin este o interfață web gratuită, scrisă în PHP, utilizată pentru administrarea bazelor de date MySQL/MariaDB. Principalele funcții includ:
- Gestionarea bazelor de date (creare, ștergere, modificare)
- Gestionarea tabelelor (creare, modificare structură, ștergere)
- Executarea interogărilor SQL direct din interfața web
- Importul și exportul datelor în diverse formate (SQL, CSV, XML, etc.)
- Gestionarea utilizatorilor și a privilegiilor
- Vizualizarea și editarea datelor din tabele într-un mod prietenos
- Monitorizarea performanțelor serverului de baze de date

Este foarte util deoarece oferă o alternativă grafică la linia de comandă MySQL, fiind mai ușor de folosit pentru majoritatea utilizatorilor.

### 6. Ce rol are fișierul .gitignore într-un proiect?

Fișierul `.gitignore` specifică ce fișiere și directoare Git trebuie să ignore (să nu le urmărească). Rolul său este:
- Excluderea fișierelor temporare și a cache-urilor care nu trebuie versionate
- Excluderea fișierelor mari (precum imagini ISO, fișiere binare) care ar îngreuna repository-ul
- Protejarea fișierelor sensibile (parole, chei API, fișiere de configurare cu date confidențiale)
- Excluderea fișierelor generate automat (log-uri, fișiere compilate)
- Menținerea repository-ului curat și ușor de gestionat

În cazul acestei lucrări, `.gitignore` exclude fișierele `.iso`, `.img`, `.qcow2`, `.log`, `.tmp` deoarece acestea sunt fie prea mari, fie temporare și nu este necesar să fie versionate.

---
