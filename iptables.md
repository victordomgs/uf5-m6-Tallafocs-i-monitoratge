# Introducció a iptables

## Què és iptables?

`iptables` és una eina per configurar el **firewall del sistema Linux**. Permet definir regles que **filtren el trànsit de xarxa**: quin tràfic s’accepta, es rebutja o es bloqueja completament.

### Estructura de treball

#### Taules (`-t`)

| Taula      | Funció                                                                 |
|------------|------------------------------------------------------------------------|
| `filter`   | Filtrar paquets (ACCEPT, DROP, REJECT)                                 |
| `nat`      | Traducció d’adreces (NAT, DNAT, SNAT, MASQUERADE)                      |
| `mangle`   | Modificació avançada (TTL, marcatge, QoS)                              |
| `raw`      | Control previ al tracking de connexions                                |
| `security` | Integració amb SELinux (poc habitual)                                  |


#### Cadenes (chains)

- `INPUT`: tràfic **que entra al propi sistema.**
- `OUTPUT`: tràfic **que surt del sistema.**
- `FORWARD`: tràfic **que passa pel sistema.** (entre interfícies)

### Comandes bàsiques

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

### Polítiques per defecte

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
