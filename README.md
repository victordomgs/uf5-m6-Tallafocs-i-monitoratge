## **Índex**
1. [Introducció a TCP/IP](#introducció-a-tcpip)
2. [Les 4 capes del model TCP/IP](#les-4-capes-del-model-tcpip)
   - [Capa d'Accés a la Xarxa (Network Access Layer)](#capa-daccés-a-la-xarxa-network-access-layer)
   - [Capa d'Internet (Internet Layer)](#capa-dinternet-internet-layer)
   - [Capa de Transport (Transport Layer)](#capa-de-transport-transport-layer)
   - [Capa d'Aplicació (Application Layer)](#capa-daplicació-application-layer)

## **Introducció a TCP/IP**
El model **TCP/IP** (Transmission Control Protocol / Internet Protocol) és un conjunt de protocols de comunicació que permeten la connexió i transmissió de dades entre dispositius en una xarxa, incloent Internet. Aquest model es basa en una arquitectura en capes, on cada capa té funcions específiques per garantir una comunicació eficient i fiable.

TCP/IP és el model en què es basa Internet i està format per **4 capes**, que s’encarreguen de diferents aspectes de la transmissió de dades.

## **Les 4 capes del model TCP/IP**

### **Capa d'Accés a la Xarxa (Network Access Layer)**
- També coneguda com a **capa d'enllaç** o **capa física i d’enllaç de dades**.
- S’encarrega de la transmissió física de dades entre dispositius.
- Defineix com es transmeten els bits a través del medi físic (cables, Wi-Fi, fibra òptica, etc.).
- Protocols associats: **Ethernet, Wi-Fi, ARP (Address Resolution Protocol)**.

📌 **Exemple:** Quan un ordinador envia un paquet de dades, aquesta capa s’encarrega de convertir la informació en senyals elèctriques, òptiques o de ràdio.

---

### **Capa d'Internet (Internet Layer)**
- Gestiona l’adreçament i l’encaminament dels paquets de dades a través de la xarxa.
- Defineix com es comuniquen els dispositius en una xarxa i en diferents xarxes interconnectades.
- Protocols associats: **IP (Internet Protocol), ICMP (Internet Control Message Protocol), ARP**.

📌 **Exemple:** Quan enviem un correu electrònic, aquesta capa s’encarrega de trobar el camí més eficient per fer arribar el missatge al destinatari.

---

### **Capa de Transport (Transport Layer)**
- Assegura que les dades es transmetin de manera fiable entre origen i destinació.
- Controla el flux de dades, maneja errors i garanteix la correcta entrega dels paquets.
- Protocols associats:
  - **TCP (Transmission Control Protocol)**: Connexió fiable, garanteix l'ordre dels paquets i la seva entrega sense errors.
  - **UDP (User Datagram Protocol)**: Connexió no fiable, envia paquets sense garantir la recepció.

📌 **Exemple:** Quan visualitzem un vídeo en streaming, es pot utilitzar **UDP** per evitar retards, mentre que per descarregar un fitxer es fa servir **TCP** per assegurar-ne la integritat.

---

### **Capa d'Aplicació (Application Layer)**
- Proporciona serveis directament als usuaris i aplicacions.
- Inclou els protocols que permeten la comunicació entre programes.
- Protocols associats: **HTTP, HTTPS, FTP, SSH, DNS, SMTP, POP3, IMAP, Telnet**.

📌 **Exemple:** Quan accedim a una pàgina web, el navegador utilitza el protocol **HTTP/HTTPS** per sol·licitar i rebre la informació del servidor.

---
