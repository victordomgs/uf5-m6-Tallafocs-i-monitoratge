# Introducció a iptables

## Què és iptables?

`iptables` és una eina per configurar el **firewall del sistema Linux**. Permet definir regles que **filtren el trànsit de xarxa**: quin tràfic s’accepta, es rebutja o es bloqueja completament.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/iptables.PNG" alt="IPTables" width="421" height="auto"/>
    <p><em>Figura 1: IPTables. Font: Viquipèdia</em></p>
  </div>

### Estructura de treball

#### Taules (`-t`)

| Taula      | Funció                                                                 |
|------------|------------------------------------------------------------------------|
| `filter`   | Filtrar paquets (ACCEPT, DROP, REJECT)                                 |
| `nat`      | Traducció d’adreces (NAT, DNAT, SNAT, MASQUERADE)                      |
| `mangle`   | Modificació avançada (TTL, marcatge, QoS)                              |
| `raw`      | Control previ al tracking de connexions                                |
| `security` | Integració amb SELinux (poc habitual)                                  |

Tot i així, les taules i cadenes més utilitzades són: 

- Taula **filter**, amb les cadenes:
  1. **input**: filtrat de paquets que arriben al tallafoc.
  2. **output**: filtrat de paquets de sortida.
  3. **forward**: permet el pas de paquets a una altra adreça del tallafoc.

- Taula **nat**: fa encaminament d'adreces de xarxa, modificant les adreces d'origen o destí dels paquets. Cadenes:
  1. **prerouting**: modificació abans d'encaminar (tràfic netrant i tràfic forwarded).
  2. **postrouting**: modificació després d'encaminar (tràfic sortint i tràfic forwarded).
  3. **output**: modificar només tràfic sortint, sense tocar el tràfic forwarded.  


  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/uf5-m6-Tallafocs-i-monitoratge/blob/main/images/nat_filter.PNG" alt="IPTables" width="421" height="auto"/>
    <p><em>Figura 2: Cadenes NAT i FILTER. Font: Viquipèdia</em></p>
  </div>
  
Una **regla** es compon de dues parts:

- Un **criteri** per fer buscar la coincidència amb el paquet examinat.
- Un **destí** aplicable, si coincideix amb el criteri.

Cada **cadena** d'una taula té una **llista de regles**, que s'examinen seqüencialment:

- Si la regla coincideix amb el paquet, s'aplica el destí especificat i es deixen d'examinar la resta de regles.
- Si no, s'examina la següent regla.

Quan s'arriba al final de la llista de regles, s'aplica la **política de la cadena** (política per defecte).

Els **destins** principals són:

- ACCEPT: deixar que passi el paquet.
- DROP: ignorar el paquet.
- RETURN: parar la cadena actual i aplicar la política de la cadena.

En el següent diagrama es pot veure els tres camins possibles d'un paquet:

- **destinació a la màquina**: el paquet arriba a un servei local.
- **origen a la màquina**: el paquet surt des d'un procés local cap a la xarxa externa.
- **routing**: el paquet arriba i el reencaminem a un altre destí.

## Taula Filter
### Comandes bàsiques - taula Filter

| Comanda                                                                 | Explicació                                                                 |
|-------------------------------------------------------------------------|----------------------------------------------------------------------------|
| `iptables -L`                                                           | Llista les regles (taula `filter` per defecte)                            |
| `iptables -L -v`                                                        | Mostra les regles amb informació detallada                                |
| `iptables -F`                                                           | Esborra totes les regles de la taula `filter`                             |
| `iptables -t nat -F`                                                    | Esborra totes les regles de la taula `nat`                                |
| `iptables -P INPUT DROP`                                                | Defineix la política per defecte de la cadena `INPUT` com a `DROP`        |
| `iptables -A FORWARD -i enp0s8 -o enp0s9 -j ACCEPT`                     | Accepta tràfic que entra per LAN i surt cap a DMZ                         |
| `iptables -A FORWARD -i enp0s9 -o enp0s8 -m state --state ESTABLISHED,RELATED -j ACCEPT` | Permet només les respostes del servidor                     |
| `iptables -A INPUT -p tcp --dport 22 -j ACCEPT`                         | Permet connexions SSH entrant al port 22                                  |
| `iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`                | NAT per permetre sortir a internet des de LAN/DMZ                         |

### Polítiques per defecte - taula Filter

```bash
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT
```

Això **bloqueja tot per defecte** excepte sortides, i obliga a crear regles específiques.

`iptables` pot seguir l'estat de les connexions gràcies al "**connection tracking**". Serveixen per **permetre només respostes** a connexions iniciades des de LAN, **evitar que DMZ pugui accedir a LAN directament** i establir un comportament **controlat i previst**. Això vol dir que pot saber si un paquet:
- És part d'una connexió nova.
- És una resposta.
- Està relacionat amb una connexió anterior.

Per fer servir aquests estats, fem servir: 

```bash
-m state --state ESTABLISHED,RELATED
```

| Estat        | Explicació                                                                 | Exemple pràctic                                      |
|--------------|----------------------------------------------------------------------------|------------------------------------------------------|
| `NEW`        | El paquet inicia una nova connexió                                         | CLNT1 fa un `ping` o `ssh` a SRV1                    |
| `ESTABLISHED`| El paquet forma part d'una connexió ja establerta                          | SRV1 respon al `ping` o `ssh` de CLNT1               |
| `RELATED`    | El paquet no forma part directa, però està relacionat amb una connexió     | Un error ICMP o una connexió de dades FTP secundària |

## Taula NAT
### Comandes bàsiques - taula NAT

| Comanda                                                                 | Explicació                                                                 |
|-------------------------------------------------------------------------|----------------------------------------------------------------------------|
| `iptables -t nat -L`                                                    | Llista les regles de la taula `nat`                                       |
| `iptables -t nat -L -v`                                                 | Mostra les regles de la taula `nat` amb informació detallada              |
| `iptables -t nat -F`                                                    | Esborra totes les regles de la taula `nat`                                |
| `iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE`                | Fa NAT (en concret, `masquerading`) per permetre accés a Internet         |
| `iptables -t nat -A PREROUTING -i enp0s3 -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:80` | Redirigeix connexions web entrants al port 80 cap a un servidor intern |
| `iptables -t nat -A OUTPUT -p tcp --dport 80 -j DNAT --to-destination 192.168.1.100:8080` | Redirigeix tràfic web generat localment al port 8080 del servidor intern |
| `iptables -t nat -N CUSTOM_NAT_CHAIN`                                   | Crea una nova cadena personalitzada dins la taula `nat`                   |
| `iptables -t nat -A CUSTOM_NAT_CHAIN -j LOG --log-prefix "NAT-HIT: "`   | Afegeix una regla per fer `log` del tràfic que passa per la cadena NAT    |
| `iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -o enp0s3 -j SNAT --to-source 203.0.113.5` | Fa SNAT canviant la IP d'origen a una IP pública específica             |

### Polítiques per defecte - taula NAT

| Cadena        | Funció principal                                                                 |
|---------------|-----------------------------------------------------------------------------------|
| `PREROUTING`  | Modifica paquets abans que entrin al sistema                                     |
| `POSTROUTING` | Modifica paquets després que surtin del sistema                                  |
| `OUTPUT`      | Modifica paquets generats pel mateix host abans d’enviar-los a la interfície de xarxa |
