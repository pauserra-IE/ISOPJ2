---
layout: default
title: "Sprint 5: Monitoratge, Auditories i Programari Client/Servidor"
---

## Índex

- **1a Part - Autorització i auditories en Windows**
  - [Introducció](#introduccio-autoritzacio-i-auditories)
  - [Pràctica](#practica-autoritzacio-i-auditories)

- **2a Part - Monitorització**
  - [Introducció](#introduccio-monitoritzacio)
  - [Pràctica](#practica-monitoritzacio)
  
# Autorització i auditories en Windows

## Introducció autoritzacio i auditories

En aquesta pràctica es treballa la configuració de permisos i auditories dins de Windows Server. L’objectiu és entendre com el sistema controla l’accés dels usuaris als recursos i com es poden registrar les diferents accions que es fan dins del sistema.

L’autorització permet definir quins usuaris poden accedir a carpetes, fitxers o recursos determinats i quines accions poden realitzar, com llegir, modificar o eliminar contingut. Aquesta configuració es gestiona des dels permisos de seguretat de Windows.

Per altra banda, les auditories serveixen per guardar un registre de les activitats del sistema. Gràcies a això es poden detectar accessos correctes, errors d’inici de sessió, modificacions d’arxius o altres accions importants relacionades amb la seguretat.

Tota aquesta informació queda enregistrada al Visor d’esdeveniments de Windows, on cada acció apareix associada a un identificador concret (Event ID). Això facilita el seguiment i el control de l’activitat dels usuaris dins del servidor.

## Pràctica autoritzacio i auditories

1. Primer obrim les **Directives de seguretat local** i accedim a **Directives locals > Directiva d’auditoria**. Aquí habilitem les opcions **“Auditar eventos de inicio de sesión”** i **“Auditar el acceso a objetos”** perquè Windows registri els inicis de sessió i els accessos als recursos del sistema.

<img width="822" height="854" alt="image" src="https://github.com/user-attachments/assets/9820988d-f275-4994-9443-f7223b1ec5a2" />

2. Un cop activades les auditories, iniciem sessió amb qualsevol compte d’usuari. Si el procés és correcte, al Visor d’esdeveniments apareixerà l’**Event ID 4624**, que indica un inici de sessió satisfactori.

<img width="606" height="944" alt="image" src="https://github.com/user-attachments/assets/8c111449-e3de-4a7a-8a23-0c6dbec22dea" />

3. Seguidament creem una carpeta nova i configurem la seva auditoria. Dins les propietats de la carpeta afegim l’usuari **Pau** amb permisos de lectura perquè el sistema registri les seves accions.

<img width="386" height="576" alt="image" src="https://github.com/user-attachments/assets/47456132-2ed1-471b-96aa-d0788596e8b8" />

<img width="921" height="596" alt="image" src="https://github.com/user-attachments/assets/a99ee78e-0c0b-410d-88f3-c00e12a11a70" />

4. També incorporem l’usuari **Administrador** amb control total sobre la carpeta per poder realitzar diferents proves d’accés i modificació.

<img width="909" height="582" alt="image" src="https://github.com/user-attachments/assets/857edacc-fe76-4992-9b20-523541b4134d" />

<img width="767" height="516" alt="image" src="https://github.com/user-attachments/assets/071ed0a7-6d98-4ca6-b238-79b4e6bf0c46" />

5. Quan es creen, modifiquen o consulten fitxers dins la carpeta auditada, Windows genera l’**Event ID 4663**, que indica que s’ha produït un accés a un objecte del sistema.

<img width="624" height="658" alt="image" src="https://github.com/user-attachments/assets/1a72c543-ccbb-4053-ace4-57d8ea9c1b7c" />

6. A continuació activem l’opció **“Auditar el seguimiento de procesos”**. Per comprovar-ne el funcionament obrim un programa, per exemple el Paint. Aquesta acció genera l’**Event ID 4688**, relacionat amb l’inici d’un procés.

<img width="613" height="540" alt="image" src="https://github.com/user-attachments/assets/889ee98d-3527-4e8d-9af6-4c6acdf366ca" />

<img width="650" height="649" alt="image" src="https://github.com/user-attachments/assets/50e3beb9-cc56-42d7-97e3-c89f241058a2" />

7. Si tanquem el programa des de l’Administrador de tasques, es registrarà l’**Event ID 4689**, que indica la finalització del procés.

<img width="662" height="474" alt="image" src="https://github.com/user-attachments/assets/9da8ea76-9d29-4721-b29f-21586fdba357" />

8. Després habilitem l’auditoria de **“Administración de cuentas”**. Per provar-la, creem un usuari nou. Aquesta operació genera els esdeveniments **4720** (creació del compte) i **4722** (activació del compte).

<img width="603" height="572" alt="image" src="https://github.com/user-attachments/assets/a0ba1145-2ec4-481f-9b87-8ad82fd6c65d" />

<img width="443" height="373" alt="image" src="https://github.com/user-attachments/assets/ddbd5a4d-3a70-40ad-a871-b6b1bc61571c" />

<img width="616" height="487" alt="image" src="https://github.com/user-attachments/assets/dc50230b-31f8-428a-b2bb-475305596474" />

10. Si posteriorment desactivem aquest usuari, el sistema registrarà l’**Event ID 4725**, corresponent a la desactivació del compte.

<img width="443" height="342" alt="image" src="https://github.com/user-attachments/assets/895ef15e-8f6d-4b14-8292-9d0adea3c965" />

<img width="628" height="657" alt="image" src="https://github.com/user-attachments/assets/b125678c-ad6c-4e4d-ae88-e0eb6c06e0a4" />

11. Finalment, eliminem l’usuari creat anteriorment. Aquesta acció queda registrada amb l’**Event ID 4726**, que identifica l’eliminació d’un compte d’usuari.

<img width="370" height="505" alt="image" src="https://github.com/user-attachments/assets/7a432a94-f1fd-4d5f-b422-67bd38cc9217" />

<img width="614" height="470" alt="image" src="https://github.com/user-attachments/assets/b776fff0-b992-4fdb-82bb-263933315863" />


---

# Monitorització

## Introducció monitoritzacio

La monitorització del sistema permet controlar l’estat i el rendiment dels recursos d’un ordinador en temps real. Amb eines com l’Administrador de tasques o el Monitor de recursos es pot observar el consum de CPU, memòria, disc i xarxa, així com detectar possibles problemes de rendiment o processos sospitosos.

### CPU

La CPU mostra els processos que s’estan executant i el percentatge de processador que consumeix cadascun. També es poden veure dades com el PID, el nombre de fils o els serveis relacionats amb cada procés.

**Aspectes importants:**
- **Ús de CPU (%):** indica la càrrega que genera un procés sobre el processador. Un consum molt elevat durant molta estona pot afectar el rendiment del sistema.
- **PID (Process ID):** identificador únic de cada procés.
- **Nom del procés:** ajuda a identificar aplicacions conegudes o detectar activitats anormals.

### Memòria RAM

Aquest apartat permet veure quanta memòria utilitza cada aplicació i l’estat general de la RAM del sistema.

**Aspectes importants:**
- **Memòria en ús:** RAM que està ocupant un procés.
- **Memòria disponible:** memòria lliure que el sistema pot utilitzar.
- **Memòria virtual:** combinació entre la RAM física i el fitxer de paginació del disc.

### Disc

La monitorització del disc mostra els processos que estan llegint o escrivint dades i la velocitat amb què ho fan.

**Aspectes importants:**
- **Lectura i escriptura (B/s):** quantitat de dades transferides al disc.
- **Temps de resposta:** temps que tarda el disc a respondre una petició.
- **Cua de disc:** indica si el disc està saturat de processos.

### Xarxa

L’apartat de xarxa permet controlar les connexions actives i les aplicacions que estan enviant o rebent dades.

**Aspectes importants:**
- **Ús de xarxa (%):** càrrega de la connexió.
- **Ports locals i remots:** ports utilitzats per les aplicacions.
- **IP remota:** servidor o dispositiu amb qui es comunica el sistema.

## Pràctica monitorització

1. Primer obrim l’**Administrador de tasques** utilitzant la combinació de tecles **Ctrl + Shift + Esc**.

<img width="669" height="650" alt="image" src="https://github.com/user-attachments/assets/06259640-e14e-4f77-878a-d7e1d16a57eb" />

2. Dins l’Administrador de tasques podem observar el consum de recursos de totes les aplicacions i serveis actius del sistema. També és possible veure la informació separada per usuaris.

<img width="674" height="596" alt="image" src="https://github.com/user-attachments/assets/5418a4a1-cf69-418c-b4b1-607146d6fc0f" />

<img width="685" height="650" alt="image" src="https://github.com/user-attachments/assets/a47f2177-165c-42c0-80fa-864177af56e7" />

<img width="668" height="657" alt="image" src="https://github.com/user-attachments/assets/40de3f0a-204f-471d-b443-2b1cce28d8a5" />

3. Una altra eina molt útil és el **Monitor de recursos**, que ofereix informació més detallada sobre el funcionament dels processos, serveis i recursos del sistema.

<img width="785" height="644" alt="image" src="https://github.com/user-attachments/assets/a98d96ff-dfa8-4237-be2e-d5dcf518da7d" />

4. A la pestanya de CPU podem consultar els processos actius, el percentatge de processador que consumeixen i altres dades relacionades amb el rendiment.

<img width="774" height="664" alt="image" src="https://github.com/user-attachments/assets/da3ff1d1-dd64-4898-8796-cf6b4dbc0b1b" />

5. A l’apartat de memòria es mostra l’ús de la RAM i l’estat de la memòria disponible del sistema.

<img width="767" height="660" alt="image" src="https://github.com/user-attachments/assets/3593fe5b-8256-40b2-92e5-7b95bef51745" />

6. També podem consultar l’activitat del disc, observant els processos que estan llegint o escrivint dades.

<img width="795" height="630" alt="image" src="https://github.com/user-attachments/assets/45aa5c32-6309-4e71-a400-b0dfe811adf8" />

7. Finalment, a la secció de xarxa es poden veure les connexions actives i l’ús de la xarxa de cada aplicació.

<img width="776" height="674" alt="image" src="https://github.com/user-attachments/assets/5e2b4319-9683-4379-9b16-b5b9320743f6" />
