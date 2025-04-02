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
      - [3.1.2. Tipus de tallafocs](#312-tipus-de-tallafocs)
   - [3.2. Sistema de detecció d'intrusos](#32-sistema-de-detecció-dintrusos)
   - [3.3. sistema de prevenció d'intrusos](#33-sistema-de-prevenció-dintrusos)

[4. Monitoratge](#4-monitoratge)
   - [4.1. Inventari](#41-inventari)
   - [4.2. SNMP](#42-SNMP)
      - [4.2.1. Components bàsics](#421-components-bàsics)
      - [4.2.2. Base de dades d’informació d’administració](#422-base-de-dades-dinformació-dadministració)

[5. Sniffers](#5-sniffers)
   - [5.1. Wireshark](#51-wireshark)
   - [5.2. TCPDump](#52-TCPDump)

[6. Seguretat en xarxes sense fils](#6-seguretat-en-xarxes-sense-fils)
   - [6.1. Hotspots](#61-hotspots)
   - [6.2. Protocols de seguretat wifi](#62-protocols-de-seguretat-wifi)
      - [6.2.1. WEP](#621-wep)
      - [6.2.2. WPA](#622-wpa)
      - [6.2.3. WPA2](#623-wpa2)
      - [6.2.4. WPA3](#624-wpa3)
   - [6.3. Atac a les xarxes wifi](#63-atac-a-les-xarxes-wifi)
   - [6.4. VPN](#64-vpn)

## 1. Introducció a TCP/IP
El model **TCP/IP** (Transmission Control Protocol / Internet Protocol) és un conjunt de protocols de comunicació que permeten la connexió i transmissió de dades entre dispositius en una xarxa, incloent Internet. Aquest model es basa en una arquitectura en capes, on cada capa té funcions específiques per garantir una comunicació eficient i fiable.

TCP/IP és el model en què es basa Internet i està format per **4 capes**, que s’encarreguen de diferents aspectes de la transmissió de dades.

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3b/UDP_encapsulation.svg/1600px-UDP_encapsulation.svg.png" alt="UDP encapsulation" width="421" height="auto"/>
    <p><em>Figura 1: Capes TCP/IP. Font: Wikipedia</em></p>
  </div>

## 2. Les 4 capes del model TCP/IP

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

## 3. Seguretat perimetral

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
> 
> **- INPUT:** Els paquets que arriba desde una xarxa externa.
> 
> **- OUTPUT:** El tràfic generat en el propi sistema i que marxa cap a les xarxes externes a l'organització.
> 
> **- FORWARD:** Són paquets que atravesen el tallafocs pero sobre els cuals s'han definit normes d'enrutament. En realitat, el tallafocs funciona com si fos un router.


  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/ip_tables_process.png" alt="IP tables" width="520" height="auto"/>
    <p><em>Figura 3: IP Tables. Font: Pròpia</em></p>
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

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/intranet_org.png" alt="INTRANET d'una organització" width="640" height="auto"/>
    <p><em>Figura 4: Intranet d'una organització. Font: Pròpia</em></p>
  </div>

### 3.2. El sistema de detecció d'intrusos

Un **Sistema de Detecció d'Intrusos o SDI** (o **IDS** de les seves sigles en anglès Intrusion Detection System) és un programa de detecció d'accessos no autoritzats a un computador o a una xarxa.

El SDI sol tenir sensors virtuals (per exemple, un sniffer o analitzador de paquets de xarxa) amb els quals el nucli de l'SDI pot obtenir dades externes (generalment sobre el tràfic de xarxa). L'SDI detecta, gràcies a aquests sensors, les anomalies que poden ser indici de la presència d'atacs i falses alarmes.

#### Funcionament 

El funcionament d'aquestes eines es basa en l'anàlisi detallada del tràfic de xarxa, el qual en entrar a l'analitzador és comparat amb signatures d'atacs coneguts, o comportaments sospitosos, com pot ser l'escaneix de ports, paquets malformats, etc. El SDI no només analitza què tipus de tràfic és, sinó que també revisa el contingut i el seu comportament.

Normalment aquesta eina s'integra amb un tallafoc. El detector d'intrusos és incapaç de detenir els atacs per si només, excepte els quals treballen conjuntament en un dispositiu de porta d'enllaç amb funcionalitat de tallafoc, convertint-se en una eina molt poderosa, ja que s'uneix la intel·ligència del SDI i el poder de bloqueig del tallafoc, a l'ésser el punt on forçosament han de passar els paquets i poden ser bloquejats abans de penetrar a la xarxa.

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
 
## 4. Monitoratge
El **monitoratge de servidors d'Internet** consisteix en la vigilància de tots els serveis actius que una màquina ofereix per Internet. Els serveis poden ser: web, correu electrònic, missatgeria instantània, etc.

El monitoratge pot ser tant **intern** com **extern**. En el cas de l'intern, la vigilància es realitza des de la mateixa xarxa on està instal·lat el servidor. Quan el monitoratge és extern, s'utilitza una plataforma d'un proveïdor de serveis que es troba fora de la nostra xarxa (normalment és una xarxa d'equips distribuïda per tot el món). El monitoratge extern és molt més fiable, perquè és independent dels problemes que pot haver dins de la xarxa on es troba l'equip a vigilar. Una altra raó per la qual és més fiable és que els sistemes comercials compten amb sistemes compostos per servidors distribuïts per tot el món i, per tant, menys sensibles a problemes puntuals en alguna de les xarxes on es troben instal·lats. El monitoratge es pot fer al núvol.

### 4.1. Inventari
Abans de començar amb un "monitoratge" més complet, farem primer una visualtizació de programari dedicat a realitzar **inventari**. Aquest inventari és molt important ja que ens permet tenir un gran recull d'informació de tots els dispositius informàtics, especialment en xarxes on el número de dispostius comença a ser elevat. Per això utilitzarem a mode d'exemple el **OCSInventory**.

**Open Computer and Software Inventory Next Generation (OCS)** és un programari lliure que permet als Administradors de TI gestionar l'inventari dels seus actius informàtics. OCS-NG recull informació sobre el maquinari i programari d'equips que hi ha a la xarxa que executen el programa de client OCS ("agent d'inventari OCS"). OCS pot utilitzar-se per visualitzar l'inventari mitjançant una interfície web. A més, OCS permet instal·lar aplicacions als equips segons un determinat criteri de cerca. Té moltes opcions més com rastrejar la xarxa mitjançant IPDiscovery, o instal·lar aplicacions remotament.

  <div style="text-align: center;">
    <img src="https://ocsinventory-ng.org/wp-content/uploads/2022/02/banniere-ocs-without-ng-01-1-300x136.png" alt="OCS" width="152" height="auto"/>
    <p><em>Figura 6: OCSInventory. Font: OCSInventory.</em></p>
  </div>

> [!NOTE]
> Pàgina oficial de [OCSInventory](https://ocsinventory-ng.org/).

### 4.2. SNMP
El **Protocol simple d'administració de xarxa** o **SNMP (Simple Network Management Protocol)** és un protocol de la capa d'aplicació que facilita l'intercanvi d'informació d'administració entre dispositius de xarxa. Forma part del conjunt de protocols TCP/IP. SNMP permet als administradors supervisar el funcionament de la xarxa, cercar i resoldre els seus problemes, i planificar el seu creixement.

Les versions de SNMP més utilitzades són dues: SNMP versió 1 (SNMPv1) i SNMP versió 2 (SNMPv2). Les dues versions tenen característiques en comú, però SNMPv2 ofereix millores com, per exemple, operacions addicionals.

SNMP disposa d'una última versió (SNMPv3) que ofereix canvis significatius en relació als seus predecessors, sobretot en aspectes de seguretat. Tot i això, no ha estat gaire acceptat per la indústria.

### 4.2.1. Components bàsics
Els dispositius administrats són supervisats i controlats utilitzant quatre comandes bàsiques SNMP: lectura, escriptura, notificació i operacions transversals.

- La **comanda de lectura** és utilitzada per un NMS per supervisar elements de la xarxa. El NMS examina diferents variables que són mantingudes pels dispositius administrats.
- La **comanda d'escriptura** és feta servir per un NMS per controlar elements de la xarxa. El NMS canvia els valors de les variables emmagatzemades dins dels dispositius administrats.
- La **comanda de notificació** és feta servir pels dispositius administrats per a reportar esdeveniments de forma asíncrona a un NMS.
- Les **operacions transversals** són usades pel NMS per determinar quines variables suporten dispositius administrats i per recollir seqüencialment informació de les taules de variables, com per exemple, una taula de rutes.

### 4.2.2. Base de dades d’informació d’administració
Una base de dades d'informació d'administració és una col·lecció d'informació organitzada jeràrquicament. Les MIB són accedides fent servir un protocol d'administració de xarxa, com per exemple, SNMP.

Un objecte administrat és una característica específica d'un dispositiu que SNMP pot monitorejar o administrar. Cada dispositiu de xarxa (com un router, switch o computadora) té múltiples característiques que SNMP pot supervisar. 

Cada un d'aquests objectes s'emmagatzemen en la base de dades (MIB).

> [!NOTE]
> Existeixen dos tipus principals d'objectes administrats:
> 
> **1. Objectes escalars:** representen un únic valor.
> **2. Objectes tabulars:** representen múltiples valors organitzats en forma de taula.

**Missatges en la comunicació SNMP:**

Per a la comunicació entre l’administrador i l'agent, el protocol SNMP especifica una sèrie de missatges, entre els quals trobem:

Ordres que llança el gestor sobre l'agent SNMP:

- **Sol·licitud GET:** missatge enviat per l’administrador a l'agent per a recuperar un registre de dades particular en el dispositiu de xarxa. Petició d'un valor específic d'un objecte de la MIB de l'agent. Aquesta ordre és utilitzada pel gestor per monitoritzar els dispositius a gestionar.
- **Sol·licitud GETNEXT:** missatge si es volen consultar registres de dades consecutives al missatge GET anterior, per exemple, dades en taules.
- **Sol·licitud SET:** missatge si es volen canviar el valor d'un objecte de la MIB de l'agent, en cas que l'objecte tingui habilitada la lectura i escriptura del seu valor. Degut a la limitada seguretat de SNMP, la majoria dels objectes de la MIB només tenen accés de lectura. Amb aquesta ordre el gestor pot controlar els dispositius a gestionar.

Ordres de resposta de l'agent SNMP:

- **Resposta GET:** l'agent respon a la Sol·licitud GET amb missatges de Resposta GET que contenen les dades sol·licitades.
- **SNMP trap:** missatges enviats pels agents sense ser requerits per l’administrador. Succeeix quan es produeix una cosa imprevista.

Exemple de comunicació per recuperar la informació sobre la descripció hardware del dispositiu:

Sol·licitud GET:

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/sol_GET.png" alt="Wireshak" width="670" height="auto"/>
    <p><em>Figura 7: Wireshark. Font: Pròpia</em></p>
  </div>

Resposta GET:
  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/res_GET.png" alt="Wireshak" width="670" height="auto"/>
    <p><em>Figura 8: Wireshark. Font: Pròpia</em></p>
  </div>

## 5. Sniffers

Un **analitzador de paquets** és un programa informàtic de captura de les trames d'una xarxa d'ordinadors. És un fet comú que, per topologia de xarxa i necessitat material, el mitjà de transmissió sigui compartir per diversos ordinadors i dispositius de xarxa, fet que possibilita que un ordinador capturi les trames d'informació no li són destinades.

Per aconseguir-ho, l'analitzador posa la targeta de xarxa en un estat conegut com "mode promiscu" en la capa d'enllaç de dades del qual no es descarten les trames no destinades a l'adreça MAC de la targeta, d'aquesta manera es pot capturar (sniff, “ensumar”) tot el trànsit que viatja per la xarxa.

Els analitzadors de paquets tenen diversos usos, com ara monitorar xarxes per detectar errors i analitzar-los, o per enginyeria inversa en protocols de xarxa. També és habitual el seu ús per a fins maliciosos, com ara robar contrasenyes, interceptar correus electrònics, espiar converses de xat, etc.

### 5.1.1. Wireshark

**Wireshark** és un programari lliure i de codi obert amb la funcionalitat d'analitzador de paquets de xarxes de comunicació. Wireshark s'empra per a solucionar problemes en xarxes, desenvolupament i anàlisi de programari i tasques educatives.

**Característiques:**
- Wireshark és un programa que captura els paquests de diferents protocols.
- Els paquests es poden visualitzar aplicant diversos filtres.
- Es poden afegir plug-ins.

### 5.1.2. TCPDump

**Tcpdump** és una eina que té la utilitat principal d'analitzar el tràfic que circula per la xarxa.

## 6. Seguretat en xarxes sense fils

Les **xarxes sense fil (en anglès wireless)** són aquelles que es comuniquen per un medi de transmissió no guiat (sense cables) mitjançant ones electromagnètiques. La transmissió i la recepció es realitza a través d'antenes.

En l’actualitat, les **xarxes sense fils (Wi-Fi)** s’han convertit en un dels mitjans de connexió més comuns tant en entorns domèstics com professionals. La seva facilitat d'ús, mobilitat i abast han contribuït a la seva popularitat. Tot i això, aquestes xarxes també presenten vulnerabilitats específiques que les fan especialment atractives per a possibles atacants.

La seguretat en les xarxes Wi-Fi és fonamental perquè, a diferència de les xarxes cablejades, les dades es transmeten per l’aire i poden ser interceptades fàcilment si no estan protegides correctament. És per això que cal conèixer els mecanismes que permeten xifrar les dades, autenticar els usuaris i evitar accessos no autoritzats.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/Wifi_certified_logo.png" alt="Wifi" width="180" height="auto"/>
    <p><em>Figura 9: Wifi certified logo. Font: Wikipedia</em></p>
  </div>

## 6.1. Hotspots

Un hotspot (literalment "punt calent" en anglès) és una zona de cobertura Wi-Fi, en el qual un punt d'accés (access point) o diversos proveeixen serveis de xarxa a través d'un proveïdor de serveis d'internet sense fils (WISP). Els hotspots es troben en llocs públics, com aeroports, biblioteques, centres de convencions, cafeteries, hotels, etcètera. Aquest servei permet mantenir-se connectat a Internet en llocs públics. Aquest servei pot brindar-se de manera gratuïta o pagant una suma que depèn del proveïdor.

Els dispositius compatibles amb Wi-Fi i accés sense fils permeten connectar PDAs, ordinadors i telèfons mòbils, entre d'altres.

Les xarxes públiques són enormement insegures. Encara que utilitzem connexions segures amb https hi ha mètodes que permeten adulterar aquestes connexions i conèixer el contingut de la informació malgrat estar xifrada (per exemple l'atac conegut com a **SSLStrip**).

> [!IMPORTANT]
> **En cap cas hauríem d'utilitzar aquestes xarxes per consultar dades o pàgines web amb continguts personals o confidencials, a menys que utilitzem eines com les VPN** (xarxes privades virtuals) que sí ens garanteixen una seguretat màxima.

## 6.2. Protocols de seguretat wifi

Un **protocol de seguretat Wi-Fi** és un conjunt de regles i tecnologies que s’utilitzen per protegir les **connexions sense fils** entre dispositius (com portàtils, mòbils, impressores…) i un punt d'accés Wi-Fi (normalment un router o AP).

Aquest protocol té dues funcions principals:

1. 🔐 **Xifrar les dades** que viatgen per la xarxa per evitar que qualsevol persona que estigui a prop pugui interceptar i llegir la informació.
2. ✅ **Autenticar** els dispositius que es connecten a la xarxa per assegurar-se que només usuaris autoritzats hi tenen accés.

### 6.2.1. WEP

WEP, acrònim de **Wired Equivalent Privacy** o "Privadesa Equivalent a Cablejat", és el sistema de xifrat inclòs en l'estàndard IEEE 802.11 com protocol per a xarxes Wireless que permet xifrar la informació que es transmet. Proporciona un xifrat a nivell 2, basat en l'algorisme de xifrat **RC4** que utilitza claus de 64 bits (40 bits més 24 bits del vector d'iniciació IV) o de 128 bits (104 bits més 24 bits del IV).

### 6.2.2. WPA

**WPA** (acrònim de Wi-Fi Protected Access - 1995 - Accés Protegit Wi-Fi) és un sistema per a protegir les xarxes sense fils (Wi-Fi); creat per a corregir les deficiències del sistema previ WEP (Wired Equivalent Privacy - Privadesa Equivalent a Cablejat).

WPA adopta l'autentificació d'usuaris mitjançant l'ús d'un servidor, on s'emmagatzemen les credencials i contrasenyes dels usuaris de la xarxa. Per no obligar a l'ús d'aquest servidor per al desplegament de xarxes, WPA permet l'autentificació mitjançant clau compartida (PSK, Pre-Shared Key), que d'una manera similar al WEP, requereix introduir la mateixa clau en tots els equips de la xarxa.

### 6.2.3. WPA2

Una vegada finalitzat el nou estàndard 802.11i es crea el **WPA2** basat en aquest. WPA es podria considerar de "migració", mentre que WPA2 és la versió certificada de l'estàndard de la IEEE.

Tant la versió 1 de WPA, com la denominada versió 2 de WPA, es basen en la transmissió de les autenticacions suportades en l'element d'informació corresponent, en el cas de WPA 1, en el tag propietari de Microsoft, i en el cas de WPA2 en el tag estàndard 802.11i RSN. Durant l'intercanvi d'informació en el procés de connexió RSN, si el client no suporta les autentificacions que especifica l'AP, serà desconnectat podent sofrir d'aquesta manera un atac de denegació de servei (DoS) específic a WPA.

A més, també existeix la possibilitat de capturar el "4way" handshake que s'intercanvia durant el procés d'autenticació en una xarxa amb seguretat robusta. Les claus pre-compartides PSK (Pre Shared Key) són vulnerables a atacs de diccionari, però no les empresarials, ja que el servidor RADIUS generarà de manera aleatòria dites claus.

### 6.2.4. WPA3

**WPA3 (Wi-Fi Protected Access 3)**, en español «Acceso Wi-Fi protegido 3», es el sucesor de WPA2[1]​[2]​ que fue anunciado en enero de 2018, por la Wi-Fi Alliance. El nuevo estándar utiliza cifrado de 128 bits en modo WPA3-Personal (192 bits en WPA3-Enterprise)[3]​ y confidencialidad de reenvío.[4]​ El estándar WPA3 también reemplaza el intercambio de claves pre-compartidas con la autenticación simultánea de iguales, lo que resulta en un intercambio inicial de claves más seguro en modo personal.

## 6.3. Atac a les xarxes wifi

La majoria d'atacs es basen en el fet que alguns paquets de gestió no estan xifrats i per tant són susceptibles de ser utilitzats per un atacant. Molts d'aquests atacs són molt més difícils si s'utilitzen els protocols més recents i segurs (WPA2 i posteriors).


#### Atac de Suplantació de SSID
Es tracta d'habilitar un punt d'accés amb el mateix nom (**SSID**) que el de la xarxa a atacar. Qualsevol usuari pot connectar-se a aquest punt d'accés "pirata" pensant que està connectat a la xarxa autèntica.
Aquest és un risc en qualsevol xarxa pública. És tan fàcil com fer-ho des d'un mòbil.

#### Atac de Segrest de sessió (hijacking)
L'atacant pot capturar les credencials amb les que s'identifica i accedeix a una pàgina web i més tard pot suplantar a l'usuari víctima. Per protegir-se d'aquest atac cal assegurar-se de que s'utilitza el protocol WPA2 i navegar només a pàgines segures https.

#### Atac de Denegació de servei (DoS)
Es tracta d'inhabilitar la xarxa wifi mitjançant la injecció massiva de paquets ilegítims. 

## 6.4. VPN

Una **xarxa privada virtual, XPV** o **VPN** (de les inicials de **virtual private network**) és una tecnologia de xarxa que permet una extensió de la xarxa local sobre una xarxa pública o no controlada, com per exemple Internet.

#### Tipus de VPN

Bàsicament hi ha tres arquitectures de connexió VPN:

**VPN d'accés remot:** És potser el model més utilitzat actualment. **Permet als usuaris connectar-se amb l'empresa des de llocs remots (oficines comercials, domicilis, hotels, avions preparats, etc.) utilitzant Internet.** Una vegada autenticats tenen un nivell d'accés molt similar al que tenen en la xarxa local de l'empresa. Moltes empreses han reemplaçat amb aquesta tecnologia la seva infraestructura dial-up (mòdems i línies telefòniques).

**VPN punt a punt:** Aquest esquema s'utilitza per connectar oficines remotes amb la seu central de l'organització. **El servidor VPN, que posseeix un vincle permanent a Internet, accepta les connexions via Internet provinents dels llocs i estableix el túnel VPN.** Els servidors de les sucursals es connecten a Internet utilitzant els serveis del seu proveïdor local d'Internet, típicament mitjançant connexions de banda ampla. Això permet eliminar els costosos vincles punt a punt tradicionals (realitzats comunament mitjançant connexions de cable físiques entre els nodes), sobretot en les comunicacions internacionals. El més comú utilitzar la tecnologia de túnel o tunneling.

**VPN over LAN:** Aquest esquema és el menys difós però un dels més poderosos per utilitzar dins de l'empresa. **És una variant del tipus "accés remot" però, en comptes d'utilitzar Internet com a mitjà de connexió, utilitza la mateixa xarxa d'àrea local (LAN) de l'empresa.** Serveix per aïllar zones i serveis de la xarxa interna. Aquesta capacitat el fa molt convenient per millorar les prestacions de seguretat de les xarxes sense fils (WiFi).

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/vpn.PNG" alt="VPN" width="640" height="auto"/>
    <p><em>Figura 10: VPN. Font: Wikipedia</em></p>
  </div>
