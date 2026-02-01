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
- La configuration a été réalisée via l’interface CLI à l’aide des commandes suivantes :
    enable
configure terminal
interface (nom de l’interface)
ip address (adresse IP) (masque)
no shutdown

###### *Ref 1: L'IOS CLI du routeur*
<img width="526" height="510" alt="PackT-Router_CLI" src="https://github.com/user-attachments/assets/130b7970-6b2f-4c6f-b93e-d74b3f27091a" />

#### Switchs
- Trois switchs ont été créés et connectés chacun à une interface du routeur à l’aide de câbles cuivre droit (straight-through).
  - Le premier switch a été nommé Switch_RH
  - Le deuxième switch a été nommé Switch_M
  - Le troisième switch a été nommé Serveur_Switch

 #### Serveurs DHCP et configuration IP des postes clients
- Deux serveurs DHCP ont été créés et nommés DHCP_RH_Server et DHCP_M_Server.
  - Configuration du serveur DHCP_RH_Server
    - Adresse IP statique : 192.168.10.253
    - Paramètres configurés :
      - Masque de sous-réseau : 255.255.255.0
      - Passerelle par défaut : 192.168.10.1
      - Serveur DNS : 192.168.30.252

  - Le service DHCP a été activé et un pool d’adresses a été créé :
    - Nom du pool : serverPool
    - Passerelle par défaut : 192.168.10.1
    - Serveur DNS : 192.168.30.252
    - Adresse IP de début : 192.168.10.10
    - Masque de sous-réseau : 255.255.255.0
    - Nombre d’utilisateurs : 25

###### *Ref 2: Configuration de la plage DHCP*
<img width="526" height="510" alt="PackT-HR_Pool" src="https://github.com/user-attachments/assets/a2390d52-9178-4e11-a6be-2e776cf47f6a" />

### Postes clients – Ressources Humaines
- Trois postes clients ont été créés pour le département Ressources Humaines et connectés au switch correspondant à l’aide de câbles cuivre droit.
  - Ils ont été renommés RH_1, RH_2 et RH_3
  - Les trois postes ont été configurés pour obtenir automatiquement une adresse IP via DHCP

###### *Ref 3: Configuration automatique de l'addresse IP pour les hotes*
<img width="526" height="510" alt="PackT-PC_DHCP" src="https://github.com/user-attachments/assets/2a1ef25c-ad92-45c1-a816-f40167551747" />

### Tests de connectivité
Un test de connectivité a été effectué en envoyant un ping depuis le poste RH_1 vers le poste RH_3, confirmant le bon fonctionnement du réseau.

###### *Ref 4: *

