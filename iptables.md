# Introducció a iptables

## Què és iptables?

`iptables` és una eina de línia de comandes per configurar les regles del tallafocs (firewall) del nucli de Linux. Permet controlar el tràfic de xarxa que entra i surt de l'equip, segons criteris definits per l'usuari com ara adreces IP, ports o protocols.

El funcionament d'iptables es basa en **taules** i **cadenes** (chains), on cada cadena conté un conjunt de **regles**. Cada regla especifica una acció a realitzar sobre un paquet que coincideixi amb uns criteris determinats.

## Taules principals

- **filter**: La taula per defecte. Gestiona el tràfic entrant, sortint i intern.
- **nat**: Utilitzada per a traducció d'adreces de xarxa (NAT).
- **mangle**: Permet modificar els paquets.
- **raw**: Utilitzada per configurar excepcions de seguiment de connexions.

## Cadenes comunes

- **INPUT**: Paquets que entren al sistema.
- **OUTPUT**: Paquets generats pel sistema.
- **FORWARD**: Paquets que passen pel sistema cap a una altra destinació.
- **PREROUTING**: Per modificar paquets abans que siguin encaminats.
- **POSTROUTING**: Per modificar paquets després de ser encaminats.

## Comandes bàsiques

### Llistar regles existents

```bash
sudo iptables -L -v
```

### Esborrar totes les regles

```bash
sudo iptables -F
```

### Establir la política per defecte

```bash
sudo iptables -P INPUT DROP
sudo iptables -P FORWARD DROP
sudo iptables -P OUTPUT ACCEPT
```

## Establir la política per defecte

### Permetre connexions locals (loopback)

```bash
sudo iptables -A INPUT -i lo -j ACCEPT
```

### Permetre connexions establertes

```bash
sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT
```

### Permetre connexions SSH (port 22)

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### Permetre trànsit HTTP i HTTPS

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

### Bloquejar una IP cocreta

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
