# packet-tracer-reseau-entreprise-simple

### Plan d’adressage IP
#### Réseaux
| Réseau | Sous-réseau | Passerelle |
|------|-----------|-----------|
| Ressources Humaines | 192.168.10.0/24 | 192.168.10.1 |
| Marketing | 192.168.20.0/24 | 192.168.20.1 |
| Salle serveurs | 192.168.30.0/24 | 192.168.30.1 |

#### Hôtes
| Hôte | Adresse IP |
|----|-----------|
| RH_1 | DHCP |
| RH_2 | DHCP |
| RH_3 | DHCP |
| M_1 | DHCP |
| M_2 | DHCP |
| M_3 | DHCP |
| DHCP_RH_Server | 192.168.10.253 |
| DHCP_M_Server | 192.168.20.253 |
| DNS_Server | 192.168.30.252 |

### Configuration des équipements
#### Routeur
- Un routeur a été créé et configuré avec une adresse IP sur chacune de ses interfaces.
  - L’interface GigabitEthernet0 a été configurée avec l’adresse 192.168.10.1/24
  - L’interface GigabitEthernet1 a été configurée avec l’adresse 192.168.20.1/24
  - L’interface GigabitEthernet2 a été configurée avec l’adresse 192.168.30.1/24
- La configuration a été réalisée via l’interface CLI.

###### *Ref 1: L'IOS CLI du routeur*
<img width="526" height="510" alt="PackT-Router_CLI" src="https://github.com/user-attachments/assets/130b7970-6b2f-4c6f-b93e-d74b3f27091a" />

#### Switchs
- Trois switchs ont été créés et connectés chacun à une interface du routeur à l’aide de câbles cuivre droit (straight-through).
  - Le premier switch a été nommé Switch_RH
  - Le deuxième switch a été nommé Switch_M
  - Le troisième switch a été nommé Serveur_Switch

 #### Serveurs DHCP et configuration IP des postes clients
- Deux serveurs DHCP ont été créés et nommés DHCP_RH et DHCP_M.
- Le serveur DHCP_RH a été configuré avec les paramètres suivants:
  - Adresse IP statique: 192.168.10.253
  - Masque de sous-réseau: 255.255.255.0
  - Passerelle par défaut: 192.168.10.1
  - Serveur DNS: 192.168.30.252

###### *Ref 2: Configuration du serveur DHCP_RH*
- Le service DHCP a été activé et une plage d’adresses a été créé :
  - Nom de la plage: serverPool
  - Passerelle par défaut: 192.168.10.1
  - Serveur DNS: 192.168.30.252
  - Adresse IP de début: 192.168.10.10
  - Masque de sous-réseau: 255.255.255.0
  - Nombre d’utilisateurs: 25

###### *Ref 3: Configuration de la plage du serveur DHCP_RH*
<img width="526" height="510" alt="PackT-HR_Pool" src="https://github.com/user-attachments/assets/a2390d52-9178-4e11-a6be-2e776cf47f6a" />

Une fois la configuration du DHCP termine, le serveur a été connectés au switch.
  
### Postes clients – Ressources Humaines
- Trois postes clients ont été créés pour le département Ressources Humaines et connectés au switch correspondant.
  - Ils ont été renommés RH_1, RH_2 et RH_3
  - Les trois postes ont été configurés pour obtenir automatiquement une adresse IP via DHCP.

###### *Ref 4: Configuration automatique de l'addresse IP pour l'hotes RH_1*
<img width="526" height="510" alt="PackT-PC_DHCP" src="https://github.com/user-attachments/assets/2a1ef25c-ad92-45c1-a816-f40167551747" />

### Tests de connectivité
Un test de connectivité a été effectué en envoyant un ping depuis le poste RH_1 vers le poste RH_3, confirmant le bon fonctionnement du réseau.

###### *Ref 5: Ping entre RH1 et RH3*
<img width="543" height="237" alt="PackT-PingRH1_RH3" src="https://github.com/user-attachments/assets/5f63aa57-0d4e-4b9b-a99d-5ec410dcc716" />

### Configuration du serveur DHCP_M
- Le serveur DHCP_Mr a été configuré avec les paramètres suivants :
  - Adresse IP statique: 192.168.20.253
  - Masque de sous-réseau: 255.255.255.0
  - Passerelle par défaut: 192.168.20.1
  - Serveur DNS: 192.168.30.252

###### *Ref 6: Configuration du serveur DHCP_M*
<img width="527" height="533" alt="PackT-Config_DHCP_M" src="https://github.com/user-attachments/assets/1e1efed6-8561-45e8-93dd-f5b16b003d47" />

- Un pool d’adresses DHCP a ensuite été créé avec les informations suivantes :
  - Passerelle par défaut : 192.168.20.1
  - Serveur DNS : 192.168.30.252
  - Adresse IP de début : 192.168.20.10
  - Masque de sous-réseau : 255.255.255.0
  - Nombre d’utilisateurs : 25

###### *Ref 7: Configuration de la plage du serveur DHCP_M*
<img width="526" height="510" alt="PackT-Config_Pool_DHCP_M" src="https://github.com/user-attachments/assets/97d2b72a-91fb-4fb7-8c2a-f0468642b5b1" />

Une fois la configuration du DHCP termine, le serveur a ete connectés au switch.

### Postes clients – Département Marketing
- Trois postes clients ont été créés pour le département Marketing et connectés au switch correspondant à l’aide de câbles cuivre droit (straight-through cable).
  - Les postes ont été renommés M_1, M_2 et M_3.
  - Les trois postes ont été configurés pour obtenir automatiquement une adresse IP via DHCP.

###### *Ref 8: Configuration automatique de l'addresse IP pour l'hote M_1*
<img width="526" height="510" alt="PackT-PCM1_DHCP_M" src="https://github.com/user-attachments/assets/586c293c-cb35-40ff-8687-a7424568a048" />

### Tests de connectivité
Un test de connectivité a été effectué en envoyant un ping depuis le poste M_1 vers le poste M_3, confirmant le bon fonctionnement du réseau.

###### *Ref 9: Ping entre M1 et M3*
<img width="548" height="238" alt="PackT-PingM1_M3" src="https://github.com/user-attachments/assets/2c5b4fad-dda3-4353-9073-903fc4648fff" />

