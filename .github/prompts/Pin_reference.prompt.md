---
name: PIN_REFERENCE
description: Définition de l'organisation hardware du PCB. 
---

<!-- Tip: Use /create-prompt in chat to generate content with agent assistance -->

CLAVIER MÉCANIQUE SPLIT ERGO TYPE CORNE
MOITIÉ GAUCHE MASTER

MCU : NRF52840_QIAA

Gestion de la batterie : nPM1100_QDAx
MODE : P1.15 / A14
Cette broche permet de choisir le mode de fonctionnement du régulateur DC/DC Buck. Une valeur basse (0) active le mode automatique/hystérétique pour une efficacité maximale à faible charge, tandis qu'une valeur haute (1) force le mode PWM pour une alimentation plus "propre" (fréquence constante).

Limitation du Courant USB
ISET : P0.29 | AIN5 / A10
Elle définit la limite du courant d'entrée provenant de VBUS. Si elle est à l'état bas (0), le courant est limité à 100 mA (mode USB SDP) ; à l'état haut (1), la limite passe à 500 mA. Notez que si un port de type CDP ou DCP est détecté automatiquement, la limite de 500 mA s'applique indépendamment de l'état de cette broche

Indicateurs d'État (LED) 
CHG : P1.13 / A16
Cette broche est une sortie à drain ouvert de 5 mA qui s'active lorsque la batterie est en cours de charge. Il faut activer la résistance pull-up interne du nRF52840 sur cette broche.

ERR : P1.10 / A20
Cette broche est aussi une sortie à drain ouvert de 5 mA, elle s'active uniquement lorsqu'une condition d'erreur survient pendant la charge. Il faut également activer la résistance pull-up interne du nRF52840 sur cette broche.

SHPACT : P0.02 / AIN0
Shipping Mode Activate : Cette broche permet d'entrer dans le mode de consommation le plus bas (Ship mode), qui isole physiquement la batterie du reste du système. Pour l'activer, il faut maintenir le pin SHPACT au niveau haut pendant au moins 200 ms alors que VBUS est déconnecté.

SHPHLD : P1.11 / B19
Shipping Mode Hold : Cette broche sert principalement à sortir du Ship mode. Pour réactiver le PMIC, il faut soit connecter une source USB sur VBUS, soit tirer SHPHLD vers le bas (masse) pendant au moins 200 ms.

BAT_MON : P0.31 | AIN7 / A8
Échantillonne la tension de la batterie pour permettre au microcontrôleur de surveiller l'état de charge (ADC). Un diviseur de tension ramène la plage de mesure de 2,8-4,2 V à 360-540 mV, ce qui correspond à une résolution d'environ 1,4 mV par unité de mesure.

BAT_MON_EN : P0.30 | AIN6 / B9
Signal de contrôle pour activer ou désactiver la surveillance de la batterie (pilotée par le firmware). Lorsque ce pin est à l'état haut, le circuit de mesure de la tension de la batterie est activé, permettant au microcontrôleur de lire les données via BAT_MON. Lorsqu'il est à l'état bas, le circuit est désactivé pour économiser de l'énergie.

SWDIO : AC24
Signal d'entrée/sortie de données série pour l'interface de débogage et de programmation SWD (Serial Wire Debug). Il permet une communication bidirectionnelle entre votre J-Link EDU Mini et le microcontrôleur pour accéder à la mémoire flash et aux registres. Le chip intègre une résistance de tirage vers le haut (pull-up) interne sur cette ligne.

SWDCLK : AA24
Entrée d'horloge pour l'interface de débogage SWD
. Ce signal synchronise les transferts de données sur la ligne SWDIO lors du flashage du bootloader ou du firmware ZMK. Il possède une résistance de rappel à la masse (pull-down) interne de 13 kΩ.

P0.18/RESET : P0.18 | nRESET / AC13
Pin de réinitialisation matérielle (nRESET), configurable par logiciel via le registre PSELRESET. Lorsqu'il est tiré vers le bas, il déclenche un reset complet du système, ce qui est indispensable pour garantir que le J-Link puisse prendre le contrôle du processeur avant de lancer la procédure de programmation.

SWO : P1.00 | TRACEDATA0 / AD22
Sortie de trace série (Serial Wire Output) multiplexée avec le GPIO P1.00. Elle permet de transmettre des logs de débogage en temps réel via l'unité ITM (Instrumentation Trace Macrocell) vers votre debugger. Contrairement aux logs USB, cette méthode est non intrusive et n'impacte pas le timing du processeur ou des piles Bluetooth/USB.

LEDs : un strip de 4 LEDs RGB adressables SK6812_EC15 utilisé pour donner des indications visuelles sur l'état de la batterie et du bluetooth.
LEDs état : P1.09 / R1
LEDs data : P0.12 / U1

MATRICE DU CLAVIER : 4x6
Ligne 1 (en partant du haut) > P1.12 / B17
Ligne 2 > P1.14 / B16
Ligne 3 > P1.28 | AN4 / B11
Ligne 4 > P1.08 / N1

Colonne 1 (en partant de la gauche) > P0.27 / H2
Colonne 2 > P0.26 / G1
Colonne 3 > P0.04 | AIN2 / B11
Colonne 4 > P0.07 / M2
Colonne 5 > P0.11 / T2
Colonne 6 > P0.06 / L1

