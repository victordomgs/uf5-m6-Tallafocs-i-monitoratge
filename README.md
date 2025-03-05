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

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/UDP_encapsulation.svg/1600px-UDP_encapsulation.svg.png" alt="UDP encapsulation" width="421" height="auto"/>
    <p><em>Figura 1: Encapsulació UDP. Font: Wikipedia</em></p>
  </div>

## **Les 4 capes del model TCP/IP**

L'arquitectura de TCP/IP està composta per quatre capes, cadascuna agrupant diferents protocols, i es correlaciona amb els nivells del model OSI de la següent manera:

> [!NOTE]  
> El model **Open Systems Interconnect (OSI)** és un estàndard de referència per a la interconnexió de sistemes oberts, desenvolupat per la Organització Internacional per a l’Estandardització (ISO) i introduït el 1984. Aquest model descriptiu de xarxes es divideix en set capes, cadascuna amb una funció específica. La seva creació va permetre establir un conjunt d'estàndards que van facilitar la compatibilitat i la interoperabilitat entre diferents tecnologies de xarxa desenvolupades per fabricants d’arreu del món.

### **Nivell d'aplicació**

Aquest nivell es correspon amb les capes **d'aplicació, presentació i sessió** del model OSI. La **capa d'aplicació** és aquella que els programes utilitzen per comunicar-se a través d'una xarxa amb altres aplicacions. Els processos en aquesta capa són específics de cada aplicació i passen dades en el format intern que utilitza el programa, les quals després es codifiquen seguint un protocol estàndard per garantir la interoperabilitat.

Algunes aplicacions específiques s’executen en aquest nivell, proporcionant serveis directament a les aplicacions d’usuari. Entre els protocols associats a aquesta capa es troben **HTTP (HyperText Transfer Protocol), FTP (File Transfer Protocol), SMTP (Simple Mail Transfer Protocol), SSH (Secure Shell) i DNS (Domain Name System), entre d'altres**.

Un cop les dades de l'aplicació han estat codificades segons un protocol estàndard de la capa d’aplicació, es transfereixen cap avall a la següent capa de la pila de protocols TCP/IP per continuar el procés de transmissió.

### **Nivell de transport**

Aquest nivell es correspon amb la capa de transport del model OSI. Els protocols d'aquesta capa s'encarreguen de gestionar la fiabilitat i la seguretat de la transmissió de dades, garantint que arribin al seu destí i ho facin en l'ordre correcte. En el model TCP/IP, els protocols de transport també tenen la funció de determinar a quina aplicació han de ser dirigides les dades.

Tot i que els protocols d'encaminament dinàmic operen sobre IP, tècnicament formen part de TCP/IP, però solen ser considerats part de la capa de xarxa. Un exemple és OSPF (Open Shortest Path First, protocol IP número 89).

> [!IMPORTANT]  
> Protocols principals de la capa de transport en TCP/IP:
>
> **TCP (Transmission Control Protocol):** Protocol de transport fiable i orientat a connexió que garanteix la correcta entrega i ordre de les dades. S’utilitza en aplicacions com web (HTTP/HTTPS), correu electrònic (SMTP, IMAP, POP3) i transferències de fitxers (FTP), però pot ser menys eficient en aplicacions en temps real.
>
> **UDP (User Datagram Protocol):** Protocol sense connexió i no fiable, que prioritza la velocitat sobre la fiabilitat. S'utilitza en streaming de vídeo/àudio, jocs en línia, VoIP i DNS, on la latència baixa és més important que la correcció d'errors.

**Ports TCP i UDP**

Els protocols de transport permeten a les aplicacions distingir-se mitjançant l'ús de ports. Per convenció, alguns ports són ports ben coneguts (well-known ports), que estan reservats per a aplicacions específiques. Exemples:
- Port 80 (HTTP) i 443 (HTTPS) per navegació web.
- Port 25 (SMTP) per enviament de correu electrònic.
- Port 53 (DNS) per resolució de noms de domini.

### **Nivell d'interxarxa**

Aquest nivell es correspon amb la capa de xarxa del model OSI. Originalment, aquesta capa es va dissenyar per solucionar el problema del transport de paquets a través d'una xarxa senzilla. Alguns dels primers protocols associats a aquesta capa inclouen X.25 i el Host/IMP Protocol d'ARPANET.

Amb l'aparició del concepte d'interxarxa, la funció de la capa de xarxa es va ampliar per permetre l'intercanvi de dades entre xarxes diferents. Això inclou l'encaminament de paquets a través d'una xarxa de xarxes, coneguda com Internet.

Protocols principals de la capa de xarxa en TCP/IP:

**IP (Internet Protocol)**

- És el protocol fonamental per a la transmissió de dades en Internet.
- Gestiona l'adreçament i l'encaminament dels paquets des d'un dispositiu origen fins a un dispositiu destí.
- Funciona de manera no fiable i sense connexió, és a dir, no garanteix que els paquets arribin ni en ordre ni sense errors.
- Els protocols superiors (com TCP o UDP) s'encarreguen de gestionar aquests aspectes si és necessari.
- Existeixen dues versions principals: IPv4 (amb adreces de 32 bits) i IPv6 (amb adreces de 128 bits).

**Protocols associats a IP**
- ICMP (Internet Control Message Protocol, Protocol IP número 1): Utilitzat per enviar missatges de control i diagnòstic sobre transmissions IP. Exemples d'ús: ordres com ping i traceroute.
- IGMP (Internet Group Management Protocol, Protocol IP número 2): Permet gestionar el trànsit multicast, facilitant la comunicació entre grups d’usuaris que reben el mateix flux de dades.

**Protocols d'encaminament**

A més dels protocols de transmissió de dades, a la capa de xarxa també trobem els **protocols d'encaminament**, que defineixen com els paquets troben el millor camí fins a la seva destinació:

- **BGP (Border Gateway Protocol):** Utilitzat per a l'encaminament entre sistemes autònoms en Internet.
- **OSPF (Open Shortest Path First):** Un protocol dinàmic d'encaminament per xarxes internes.
- **RIP (Routing Information Protocol):** Un dels primers protocols d'encaminament dinàmic.

Encara que alguns d'aquests protocols (com **ICMP i IGMP**) tècnicament es troben per sobre d'IP, les seves funcions són pròpies de la **capa de xarxa**, cosa que reflecteix una lleugera diferència entre el model TCP/IP i el model OSI.

### **Nivell d'enllaç**

La capa d'enllaç no forma part realment de la pila TCP/IP però és el mètode utilitzat per passar paquets de la capa Internet d'un dispositiu a la capa Internet d'un altre. Aquest procés pot ser controlat tant per programari com per maquinari (hardware). D'aquesta manera es realitzen funcions d'enllaç de dades tals com afegir una capçalera al paquet per preparar-lo per a la seva transmissió i enviar-lo posteriorment per un mitjà físic. D'altra banda, la capa d'enllaç s'encarrega de rebre trames de dades, extreure les capçaleres d'aquestes i entregar els paquets rebuts a la capa d'Internet.
