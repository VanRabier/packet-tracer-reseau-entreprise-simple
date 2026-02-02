# Cisco Packet Tracer Lab – Réseau d’Entreprise Simple

## Présentation du projet
Ce projet a pour objectif de concevoir et configurer un réseau d’entreprise simple à l’aide de Cisco Packet Tracer.  Le réseau est segmenté en plusieurs départements et intègre des services centralisés tels que le DHCP, le DNS et un serveur Web HTTP.

## Compétences développées
- Adressage IP et sous-réseaux
- Routage réseau
- Configuration DHCP
- Configuration DNS
- Architecture client-serveur
- Utilisation de Cisco Packet Tracer

## Environnement & outils
- Cisco Packet Tracer
  - Routeur Cisco
  - Switchs Cisco
  - Postes clients (PC)
  - Serveurs (DHCP, DNS, HTTP)

## Topologie du réseau
Le réseau est composé des éléments suivants :
- 1 routeur
- 3 switchs
- 2 serveurs DHCP
- 1 serveur DNS
- 1 serveur Web (HTTP)
- 6 postes clients

## Plan d’adressage IP
### Réseaux
| Réseau | Sous-réseau | Passerelle |
|------|-----------|-----------|
| Ressources Humaines | 192.168.10.0/24 | 192.168.10.1 |
| Marketing | 192.168.20.0/24 | 192.168.20.1 |
| Salle serveurs | 192.168.30.0/24 | 192.168.30.1 |

### Hôtes
| Hôte | Adresse IP |
|----|-----------|
| RH_1 | DHCP |
| RH_2 | DHCP |
| RH_3 | DHCP |
| M_1 | DHCP |
| M_2 | DHCP |
| M_3 | DHCP |
| DHCP_RH | 192.168.10.253 |
| DHCP_M | 192.168.20.253 |
| SVR_DNS | 192.168.30.252 |
| SVR_Web | 192.168.30.251 |

## Configuration des équipements
### Routeur
- Un routeur a été créé et configuré avec une adresse IP sur chacune de ses interfaces.
  - L’interface GigabitEthernet0 a été configurée avec l’adresse 192.168.10.1/24
  - L’interface GigabitEthernet1 a été configurée avec l’adresse 192.168.20.1/24
  - L’interface GigabitEthernet2 a été configurée avec l’adresse 192.168.30.1/24
- La configuration a été réalisée via l’interface CLI.

###### *Ref 1: L'IOS CLI du routeur*
<img width="526" height="510" alt="PackT-Router_CLI" src="https://github.com/user-attachments/assets/130b7970-6b2f-4c6f-b93e-d74b3f27091a" />

### Switchs
- Trois switchs ont été créés et connectés chacun à une interface du routeur.
  - Le premier switch a été nommé Switch_RH
  - Le deuxième switch a été nommé Switch_M
  - Le troisième switch a été nommé Serveur_Switch

### Serveurs DHCP et configuration IP des postes clients
#### DHCP_RH
- Un serveur DHCP nommé DHCP_RH a été créé et configuré avec les paramètres suivants :
  - Adresse IP statique: 192.168.10.253
  - Masque de sous-réseau: 255.255.255.0
  - Passerelle par défaut: 192.168.10.1
  - Serveur DNS: 192.168.30.252

###### *Ref 2: Configuration du serveur DHCP_RH*
<img width="526" height="510" alt="PackT-Config_DHCP_RH" src="https://github.com/user-attachments/assets/a5a636d0-7da1-4680-b279-1b8a04ee2113" />

- Le service DHCP a été activé et une plage d’adresses a été créée:
  - Nom de la plage: serverPool
  - Passerelle par défaut: 192.168.10.1
  - Serveur DNS: 192.168.30.252
  - Adresse IP de début: 192.168.10.10
  - Masque de sous-réseau: 255.255.255.0
  - Nombre d’utilisateurs: 25

###### *Ref 3: Configuration de la plage du serveur DHCP_RH*
<img width="526" height="510" alt="PackT-HR_Pool" src="https://github.com/user-attachments/assets/a2390d52-9178-4e11-a6be-2e776cf47f6a" />

- Une fois la configuration du DHCP termine, le serveur a été connectés au Switch_RH.
  
### Postes clients – Ressources Humaines
- Trois postes clients ont été créés pour le département Ressources Humaines et connectés au switch correspondant.
  - Ils ont été renommés RH_1, RH_2 et RH_3
  - Les trois postes ont été configurés pour obtenir automatiquement une adresse IP via DHCP.

###### *Ref 4: Configuration automatique de l'addresse IP pour l'hotes RH_1*
<img width="526" height="510" alt="PackT-PC_DHCP" src="https://github.com/user-attachments/assets/2a1ef25c-ad92-45c1-a816-f40167551747" />

### Tests de connectivité - Réseau Resources Humaines
- Un test de connectivité a été effectué en envoyant un ping depuis le poste RH_1 vers le poste RH_3, confirmant le bon fonctionnement du réseau.

###### *Ref 5: Ping entre RH1 et RH3*
<img width="543" height="237" alt="PackT-PingRH1_RH3" src="https://github.com/user-attachments/assets/5f63aa57-0d4e-4b9b-a99d-5ec410dcc716" />

#### DHCP_M
- Un deuxieme serveur DHCP nommé DHCP_M a été créé et configuré avec les paramètres suivants :
  - Adresse IP statique: 192.168.20.253
  - Masque de sous-réseau: 255.255.255.0
  - Passerelle par défaut: 192.168.20.1
  - Serveur DNS: 192.168.30.252

###### *Ref 6: Configuration du serveur DHCP_M*
<img width="527" height="533" alt="PackT-Config_DHCP_M" src="https://github.com/user-attachments/assets/1e1efed6-8561-45e8-93dd-f5b16b003d47" />

- Un plage d’adresses DHCP a ensuite été créé avec les informations suivantes :
  - Passerelle par défaut : 192.168.20.1
  - Serveur DNS : 192.168.30.252
  - Adresse IP de début : 192.168.20.10
  - Masque de sous-réseau : 255.255.255.0
  - Nombre d’utilisateurs : 25

###### *Ref 7: Configuration de la plage du serveur DHCP_M*
<img width="526" height="510" alt="PackT-Config_Pool_DHCP_M" src="https://github.com/user-attachments/assets/97d2b72a-91fb-4fb7-8c2a-f0468642b5b1" />

- Une fois la configuration du DHCP termine, le serveur a ete connectés au switch.

### Postes clients – Département Marketing
- Trois postes clients ont été créés pour le département Marketing et connectés au switch correspondant.
  - Les postes ont été renommés M_1, M_2 et M_3.
  - Les trois postes ont été configurés pour obtenir automatiquement une adresse IP via DHCP.

###### *Ref 8: Configuration automatique de l'addresse IP pour l'hote M_1*
<img width="526" height="510" alt="PackT-PCM1_DHCP_M" src="https://github.com/user-attachments/assets/586c293c-cb35-40ff-8687-a7424568a048" />

### Tests de connectivité
- Un test de connectivité a été effectué en envoyant un ping depuis le poste M_1 vers le poste M_3, confirmant le bon fonctionnement du réseau.

###### *Ref 9: Ping entre M1 et M3*
<img width="548" height="238" alt="PackT-PingM1_M3" src="https://github.com/user-attachments/assets/2c5b4fad-dda3-4353-9073-903fc4648fff" />

### Test de connectivité inter-départements
- Un ping a été effectué depuis le poste client RH_1 (Ressources Humaines) vers le poste M_1 (Marketing) afin de vérifier la communication entre les différents sous-réseaux.

###### *Ref 10: Ping entre RH2 et M2*

#### Serveur Web
- Un serveur Web nommé SVR_Web a été créé et configuré avec:
	- Adresse IP statique : 192.168.30.252
	- Masque de sous-réseau : 255.255.255.0
	- Passerelle par défaut : 192.168.30.1
	
###### *Ref 11: Configuration du serveur web*
<img width="527" height="533" alt="PackT-Config_SVR_web" src="https://github.com/user-attachments/assets/40114ee1-8927-4c96-997a-03c05cb07331" />

- Depuis l’onglet Services, section HTTP, les services HTTP et HTTPS ont été activés.
- Le serveur a ensuite été connecté au switch de la salle serveurs.
	
### Test du serveur Web
- Depuis le poste client RH_2, le navigateur Web a été ouvert et l’adresse IP du serveur Web (192.168.30.251) a été saisie pour vérifier l’accès au service HTTP.

###### *Ref 12: Test a l'acces*
<img width="526" height="510" alt="PackT-Test_SVR_web" src="https://github.com/user-attachments/assets/d804b65a-02d2-4824-9eca-12948242891b" />

#### Serveur DNS 
- Un serveur DNS nommé SVR_DNS a été créé et configuré avec: 
	- Adresse IP statique : 192.168.30.252
	- Masque de sous-réseau : 255.255.255.0
	- Passerelle par défaut : 192.168.30.1
	
###### *Ref 13: Configuration du serveur DNS*
<img width="527" height="533" alt="PackT-Config_SVR_DNS" src="https://github.com/user-attachments/assets/f8c87823-de58-4d2b-9b95-a2fa37a573e0" />

- Depuis l’onglet Services, section DNS, le service DNS a été activé.  Un enregistrement DNS pour le site Web, www.ciscopackettracer.com, a été créé associant le nom de domaine à l’adresse IP du serveur Web.
	
###### *Ref 14: PackT-Add_web*
<img width="526" height="510" alt="PackT-Config_Add_Web" src="https://github.com/user-attachments/assets/f6e9425a-ff5e-43df-871f-023b031302e2" />

- Le serveur DNS a ensuite été connecté au switch de la salle serveurs.

### Test du serveur DNS
- Depuis le poste client M_2, le navigateur Web a été ouvert et le nom de domaine www.ciscopackettracer.com a été saisi afin de vérifier la résolution DNS.

###### *Ref 15: Test Resolution DNS*
<img width="526" height="510" alt="PackT-Test_SVR_DNS" src="https://github.com/user-attachments/assets/fc4bffbd-4c33-4b6b-a042-dd6ea321f93d" />
