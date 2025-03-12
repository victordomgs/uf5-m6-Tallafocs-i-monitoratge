## **Índex**
[1. Introducció a TCP/IP](#1-introducció-a-tcpip)

[2. Les 4 capes del model TCP/IP](#2-les-4-capes-del-model-tcpip)
   - [2.1. Capa d'Accés a la Xarxa (Network Access Layer)](#21-capa-daccés-a-la-xarxa-network-access-layer)
   - [2.2. Capa d'Internet (Internet Layer)](#22-capa-dinternet-internet-layer)
   - [2.3. Capa de Transport (Transport Layer)](#23-capa-de-transport-transport-layer)
   - [2.4. Capa d'Aplicació (Application Layer)](#24-capa-daplicació-application-layer)

[3. Seguretat perimetral](#3-seguretat-perimetral)
   - [3.1. Tallafocs](#31-tallafocs)
        - [3.1.1. Polítiques de seguretat dels tallafocs](#311-polítiques-de-seguretat-dels-tallafocs)
        - [3.1.2. Tipus de tallafocs](#31-tipus-de-tallafocs)
   - [3.2. Sistema de detecció d'intrusos](#32-sistema-de-detecció-dintrusos)
   - [3.3. sistema de prevenció d'intrusos](#33-sistema-de-prevenció-dintrusos)

## **1. Introducció a TCP/IP**
El model **TCP/IP** (Transmission Control Protocol / Internet Protocol) és un conjunt de protocols de comunicació que permeten la connexió i transmissió de dades entre dispositius en una xarxa, incloent Internet. Aquest model es basa en una arquitectura en capes, on cada capa té funcions específiques per garantir una comunicació eficient i fiable.

TCP/IP és el model en què es basa Internet i està format per **4 capes**, que s’encarreguen de diferents aspectes de la transmissió de dades.

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/UDP_encapsulation.svg/1600px-UDP_encapsulation.svg.png" alt="UDP encapsulation" width="421" height="auto"/>
    <p><em>Figura 1: Capes TCP/IP. Font: Wikipedia</em></p>
  </div>

## **2. Les 4 capes del model TCP/IP**

L'arquitectura de TCP/IP està composta per quatre capes, cadascuna agrupant diferents protocols, i es correlaciona amb els nivells del model OSI de la següent manera:

> [!NOTE]  
> El model **Open Systems Interconnect (OSI)** és un estàndard de referència per a la interconnexió de sistemes oberts, desenvolupat per la Organització Internacional per a l’Estandardització (ISO) i introduït el 1984. Aquest model descriptiu de xarxes es divideix en set capes, cadascuna amb una funció específica. La seva creació va permetre establir un conjunt d'estàndards que van facilitar la compatibilitat i la interoperabilitat entre diferents tecnologies de xarxa desenvolupades per fabricants d’arreu del món.

### **2.1. Nivell d'aplicació**

Aquest nivell es correspon amb les capes **d'aplicació, presentació i sessió** del model OSI. La **capa d'aplicació** és aquella que els programes utilitzen per comunicar-se a través d'una xarxa amb altres aplicacions. Els processos en aquesta capa són específics de cada aplicació i passen dades en el format intern que utilitza el programa, les quals després es codifiquen seguint un protocol estàndard per garantir la interoperabilitat.

Algunes aplicacions específiques s’executen en aquest nivell, proporcionant serveis directament a les aplicacions d’usuari. Entre els protocols associats a aquesta capa es troben **HTTP (HyperText Transfer Protocol), FTP (File Transfer Protocol), SMTP (Simple Mail Transfer Protocol), SSH (Secure Shell) i DNS (Domain Name System), entre d'altres**.

Un cop les dades de l'aplicació han estat codificades segons un protocol estàndard de la capa d’aplicació, es transfereixen cap avall a la següent capa de la pila de protocols TCP/IP per continuar el procés de transmissió.

### **2.2. Nivell de transport**

Aquest nivell es correspon amb la capa de transport del model OSI. Els protocols d'aquesta capa s'encarreguen de gestionar la fiabilitat i la seguretat de la transmissió de dades, garantint que arribin al seu destí i ho facin en l'ordre correcte. En el model TCP/IP, els protocols de transport també tenen la funció de determinar a quina aplicació han de ser dirigides les dades.

Tot i que els protocols d'encaminament dinàmic operen sobre IP, tècnicament formen part de TCP/IP, però solen ser considerats part de la capa de xarxa. Un exemple és OSPF (Open Shortest Path First, protocol IP número 89).

> [!IMPORTANT]  
> Protocols principals de la capa de transport en TCP/IP:
>
> **TCP (Transmission Control Protocol):** Protocol de transport fiable i orientat a connexió que garanteix la correcta entrega i ordre de les dades. S’utilitza en aplicacions com web (HTTP/HTTPS), correu electrònic (SMTP, IMAP, POP3) i transferències de fitxers (FTP), però pot ser menys eficient en aplicacions en temps real.
>
> **UDP (User Datagram Protocol):** Protocol sense connexió i no fiable, que prioritza la velocitat sobre la fiabilitat. S'utilitza en streaming de vídeo/àudio, jocs en línia i VoIP, on la latència baixa és més important que la correcció d'errors.

**Ports TCP i UDP**

Els protocols de transport permeten a les aplicacions distingir-se mitjançant l'ús de ports. Per convenció, alguns ports són ports ben coneguts (well-known ports), que estan reservats per a aplicacions específiques. Exemples:
- Port 80 (HTTP) i 443 (HTTPS) per navegació web.
- Port 25 (SMTP) per enviament de correu electrònic.
- Port 53 (DNS) per resolució de noms de domini.

### **2.3. Nivell d'interxarxa**

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

### **2.4. Nivell d'enllaç**

La capa d'enllaç no forma part realment de la pila TCP/IP però és el mètode utilitzat per passar paquets de la capa Internet d'un dispositiu a la capa Internet d'un altre. Aquest procés pot ser controlat tant per programari com per maquinari (hardware). D'aquesta manera es realitzen funcions d'enllaç de dades tals com afegir una capçalera al paquet per preparar-lo per a la seva transmissió i enviar-lo posteriorment per un mitjà físic. D'altra banda, la capa d'enllaç s'encarrega de rebre trames de dades, extreure les capçaleres d'aquestes i entregar els paquets rebuts a la capa d'Internet.

## **3. Seguretat perimetral**

La **seguretat perimetral informàtica** consisteix a establir un conjunt de controls de seguretat al voltant d'una estructura tecnològica, amb l'objectiu de garantir la protecció adequada davant atacs o accessos procedents d'intrusos o xarxes no confiables.

L'element més utilitzat per assegurar el perimetre és el **tallafoc** (firewall), que és un element de maquinari o programari utilitzat en una xarxa d'equips informàtics per controlar les comunicacions, permetent-les o prohibint-les segons les polítiques de xarxa que hagi definit l'organització responsable de la xarxa. 

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/eb/Gateway_firewall.svg/1280px-Gateway_firewall.svg.png" alt="Firewall" width="630" height="auto"/>
    <p><em>Figura 2: Tallafocs. Font: Wikipedia</em></p>
  </div>

La posició habitual d’un tallafoc és al punt de connexió entre la xarxa interna de l’organització i la xarxa externa, generalment Internet. Això permet protegir la xarxa interna d’intents d’accés no autoritzats des de l’exterior que podrien explotar vulnerabilitats dels sistemes interns.

A més, és comú que el tallafoc connecti una tercera xarxa anomenada **zona desmilitaritzada (DMZ)**, on es situen els servidors de l’organització que han de ser accessibles des de l’exterior.

Encara que un tallafoc ben configurat millora la seguretat d’una infraestructura informàtica, no és suficient per garantir una protecció completa.

### 3.1. Tallafocs

Com ve hem vist abans, un tallafocs és un sistema que analitza i supervisa els paquets que entran i surten per les seves interfícies de xarxa, és a dir el trànsit d'informació, i els accepta o refusa en funció d'un conjunt de regles que ha definit l'administrador. 

> [!NOTE] 
> En el context de **Linux**, aquestes regles venen definides per el que es coneix com **iptables**. Un sistema de filtrat de paquets. Les connexions d'aquest sistema es divideixen en:
> **- INPUT:** Els paquets que arriba desde una xarxa externa.
> **- OUTPUT:** El tràfic generat en el propi sistema i que marxa cap a les xarxes externes a l'organització.
> **- FORWARD:** Són paquets que atravesen el tallafocs pero sobre els cuals s'han definit normes d'enrutament. En realitat, el tallafocs funciona com si fos un router.


  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/ip_tables_process.png" alt="IP tables" width="520" height="auto"/>
    <p><em>Figura 3:IP Tables. Font: Pròpia</em></p>
  </div>

Quan arriba un intent de connexió el tallafoc pot: 

**- Permetre (ACCEPT):** Accepta la connexió.
**- Denegar (DENY):** Rebutja la connexió.
**- Ignorar (DROP):** Ignora la petició de connexió (l'origen que demana la connexió no sap si ha estat ignorada o el destinatari no respon).

### 3.1.1. Polítiques de seguretat dels tallafocs

Existeixen dos tipus de política diferents, les dues en realitat tenen el mateix objectiu i el mateix resultat si han estat correctament configurades: 

**- Restrictiva:** Es rebutja tot el trànsit excepte el que està expressament permès. És la política més segura: cada servei potencialment perillós ha de ser permès explícitament. 
**- Permissiva:** Es permet tot el trànsit excepte el que està expressament denegat. Té el risc que per defecte s'hagi permès trànsit potencialment perillós. 

### 3.1.2. Tipus de tallafocs

#### Tallafoc de capa de xarxa o de filtratge de paquets

Opera en el **nivell 3** del model TCP/IP, actuant com un filtre de paquets IP. Permet establir regles de filtratge basades en camps com **l’adreça IP d’origen i destinació**. En molts casos, també pot aplicar filtres en **nivells superiors**, com el **nivell de transport (nivell 4)**, on es poden filtrar ports d'origen i destinació, o fins i tot en **nivell d’enllaç de dades (nivell 2)**, utilitzant adreces **MAC**.

#### Tallafoc de capa d'aplicació

Funciona en el **nivell 4** del model TCP/IP, permetent un control més detallat sobre els protocols d’aplicació. Això significa que pot filtrar trànsit en funció de **característiques específiques dels protocols**, com HTTP, bloquejant o permetent l'accés a determinades **URL**. Un exemple comú d’aquest tipus de tallafoc és el **Proxy**, que permet gestionar i controlar l’accés a Internet des d’una xarxa corporativa.

#### Tallafoc personal
És una solució de seguretat que es desplega en forma de programari dins d’un ordinador, filtrant tant les connexions entrants com les sortints. Aquest tipus de tallafoc ofereix protecció individualitzada, bloquejant comunicacions no autoritzades i evitant possibles intrusions des de la xarxa.

### 3.2. El sistema de detecció d'intrusos

Un **Sistema de Detecció d'Intrusos o SDI** (o **IDS** de les seves sigles en anglès Intrusion Detection System) és un programa de detecció d'accessos no autoritzats a un computador o a una xarxa.

El SDI sol tenir sensors virtuals (per exemple, un sniffer o analitzador de paquets de xarxa) amb els quals el nucli de l'SDI pot obtenir dades externes (generalment sobre el tràfic de xarxa). L'SDI detecta, gràcies a aquests sensors, les anomalies que poden ser indici de la presència d'atacs i falses alarmes.

#### Funcionament 

El funcionament d'aquestes eines es basa en l'anàlisi detallada del tràfic de xarxa, el qual en entrar a l'analitzador és comparat amb signatures d'atacs coneguts, o comportaments sospitosos, com pot ser l'escaneix de ports, paquets malformats, etc. El SDI no només analitza què tipus de tràfic és, sinó que també revisa el contingut i el seu comportament.

Normalment aquesta eina s'integra amb un tallafoc. El detector d'intrusos és incapaç de detenir els atacs per si només, excepte els quals treballen conjuntament en un dispositiu de porta d'enllaç amb funcionalitat de tallafoc, convertint-se en una eina molt poderosa, ja que s'uneix la intel·ligència del SDI i el poder de bloqueig del tallafoc, a l'ésser el punt on forçosament han de passar els paquets i poden ser bloquejats abans de penetrar a la xarxa.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/intranet_org.png" alt="INTRANET d'una organització" width="640" height="auto"/>
    <p><em>Figura 4:Intranet d'una organització. Font: Pròpia</em></p>
  </div>

#### Tipus d'SDI

Existeixen dos tipus de sistemes de detecció d'intrusos:

1. **HIDS (HostIDS):** el principi de funcionament d'un HIDS, depèn de l'èxit dels intrusos, que generalment deixessin rastres de les seves activitats en l'equip atacat, quan intenten ensenyorir-se del mateix, amb propòsit de dur a terme altres activitats. El HIDS intenta detectar tals modificacions en l'equip afectat, i fer un reporti de les seves conclusions.

2. **NIDS (NetworkIDS):** un SDI basat en la xarxa, detectant atacs a tot el segment de la xarxa. La seva interfície ha de funcionar en manera promíscua capturant així tot el tràfic de la xarxa.

### 3.3. Sistema de prevenció d'intrusos

Un **sistema de prevenció d'intrusions (o per les seves sigles en anglès, IPS)** és un programari que exerceix el control d'accés en una xarxa informàtica per protegir els sistemes computacionals d'atacs i abusos. La tecnologia de prevenció d'intrusions és considerada per alguns com una extensió dels sistemes de detecció d'intrusions (IDS), però en realitat és un altre tipus de control d'accés, més proper a les tecnologies de tallafocs.

La principal diferència entre un IDS (Sistema de Detecció d'Intrusions) i un IPS (Sistema de Prevenció d'Intrusions) és la seva funció dins de la seguretat de la xarxa. Un IDS només monitora i detecta activitats sospitoses o atacs dins de la xarxa, alertant els administradors però sense prendre acció directa. En canvi, un IPS no només detecta les amenaces, sinó que també bloqueja o mitiga automàticament els atacs abans que puguin afectar el sistema. És a dir, un IDS observa i avisa, mentre que un IPS actua i protegeix en temps real.

  <div style="text-align: center;">
    <img src="https://cdn.prod.website-files.com/5ff66329429d880392f6cba2/623d90f1f7c8acbcd68f2095_IDS%20vs%20IPS.jpg" alt="IDS vs IPS" width="630" height="auto"/>
    <p><em>Figura 5: IDS vs IPS. Font: Wallarm</em></p>
  </div>
 
