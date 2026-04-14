---
layout: default
title: "Sprint 1: Instal·lació, Configuració Inicial i Programari de Base"
---

# Sprint 1: Instal·lació, Configuració Inicial i Programari de Base (WINDOWS)
## Índex

## Índex
1. [Fase 1: Instal·lació del Sistema Operatiu](#fase-1-instal·lació-del-sistema-operatiu)
2. [Fase 2: Punts de Restauració](#fase-2-punts-de-restauració)
3. [Fase 3: Llicències de Windows](#fase-3-llicències-de-windows)
4. [Fase 4: Gestor d'Arrencada](#fase-4-gestor-darrencada)
5. [Fase 5: Xarxa Bàsica](#fase-5-xarxa-bàsica)
6. [Fase 6: Comandes Generals](#fase-6-comandes-generals)
7. [Fase 7: Instal·lació d'Aplicacions](#fase-7-instal·lació-daplicacions)


## Fase 1: Instal·lació del sistema operatiu

### 1.1 Creació de la màquina virtual

El primer pas és definir una nova instància a **VirtualBox**. En el procés de creació, seleccionem el tipus de sistema operatiu i la versió corresponent. També aprofitem per carregar la **ISO de Windows 10/11**.

<img width="874" height="642" alt="image" src="https://github.com/user-attachments/assets/1e39e580-b9e9-4af3-ac06-42d54c18f458" />

### 1.2 Assignació de recursos

Per garantir un rendiment òptim del sistema operatiu, assignem un mínim de **4 GB de memòria RAM** i un disc dur virtual de **40 GB**.

<img width="756" height="343" alt="image" src="https://github.com/user-attachments/assets/7a43509d-8ee9-49dc-902f-9776e71b298d" />

### 1.3 Selecció del medi d'instal·lació

Verifiquem que la imatge ISO del sistema s'ha muntat correctament a la unitat òptica virtual abans d'iniciar l'arrencada.

<img width="716" height="500" alt="image" src="https://github.com/user-attachments/assets/344282de-a626-4abb-8767-4ed6e4e3b46a" />

### 1.4 Inici de l'assistent i configuració regional

Arrenquem la màquina i seguim els primers passos de l'assistent d'instal·lació de Windows, on definim l'idioma i el format de regió.

<img width="639" height="490" alt="image" src="https://github.com/user-attachments/assets/aa18e788-5250-402b-b81e-29c8082cf01c" />

### 1.5 Tipus d'instal·lació

L'assistent ens ofereix dues vies: Actualització o Personalitzada. Per a una instal·lació neta des de zero, seleccionem l'opció **Personalitzada**.

<img width="662" height="647" alt="image" src="https://github.com/user-attachments/assets/328d2678-4874-469d-8f36-75cc2c303861" />

### 1.6 Gestió de particions

Triem l'espai sense assignar del disc virtual (els 40 GB prèviament creats) per procedir amb la instal·lació dels fitxers del sistema.

<img width="678" height="639" alt="image" src="https://github.com/user-attachments/assets/5e62d3e9-e7bd-42e2-95c5-0f753f2430ce" />

### 1.7 Procés de còpia de fitxers

Esperem que el sistema completi la còpia, preparació i instal·lació de les característiques i actualitzacions inicials.

<img width="643" height="645" alt="image" src="https://github.com/user-attachments/assets/50b07487-5a62-4b43-84bb-5c336a5b2b30" />

### 1.8 Configuració post-instal·lació

Un cop finalitzada la càrrega de fitxers, seleccionem la regió final i la distribució del teclat (Espanyol/Català) per adaptar l'entorn a l'usuari.

<img width="1024" height="771" alt="image" src="https://github.com/user-attachments/assets/1253adeb-d1c8-49c6-9e98-fcd67835b393" />

### 1.9 Creació del compte d'usuari

Configurem el nom d'usuari principal i establim una contrasenya segura per accedir al sistema.

<img width="630" height="612" alt="2026-04-14\_09-27" src="https://github.com/user-attachments/assets/29d87898-9189-49f6-8267-cf9064917f59" />

### 1.10 Verificació final

Un cop acabada la configuració de privadesa i perfil, comprovem que el sistema arriba a l'escriptori i funciona correctament.

<img width="1025" height="827" alt="image" src="https://github.com/user-attachments/assets/4dbd4b19-ac24-4ef9-946a-ff1d655ed77c" />

-----

## Fase 2: Punts de restauració

Creació de punts de seguretat per poder revertir el sistema a un estat anterior en cas d'error o canvis no desitjats.

  * **Pas 6:** Cercar "Crear un punt de restauració" al menú d'inici.
    <img width="823" height="336" alt="image" src="https://github.com/user-attachments/assets/9c00f4d5-e13c-4a57-a50e-9e79c5e7e137" />

  * **Pas 7:** Activar la protecció del sistema al disc C:.
   <img width="796" height="601" alt="image" src="https://github.com/user-attachments/assets/eacf48ff-2705-4498-89b7-12227f4e00e5" />

  * **Pas 8:** Crear manualment un punt de restauració identificant-lo amb un nom clar (ex: "Post-instal·lació").
   <img width="516" height="549" alt="image" src="https://github.com/user-attachments/assets/5c60c9b2-d767-4432-a149-d9d5d852d60e" />

  * **Pas 9:** Realitzar una modificació (instal·lació d'un petit programa).
   <img width="787" height="395" alt="image" src="https://github.com/user-attachments/assets/12498296-60d6-462a-a1f9-dd29c3709ce7" />

  * **Pas 10:** Restaurar el sistema i verificar que el canvi s'ha desfet.
<img width="697" height="668" alt="image" src="https://github.com/user-attachments/assets/31e28ba5-7e1b-4258-b72a-6fdf20f67d2a" />

I tal com es veu es s'ha restaurat correctament:
<img width="512" height="266" alt="image" src="https://github.com/user-attachments/assets/ff14c6d1-f391-4b7b-8cca-f820838171da" />


-----

## Fase 3: Llicències de Windows

Anàlisi del mètode d'activació i tipologia de llicència instal·lada.

  * **Pas 11 i 12:** Verificar l'estat d'activació a "Configuració" \> "Sistema" \> "Activació".
   <img width="567" height="695" alt="image" src="https://github.com/user-attachments/assets/465e3534-35e1-4ef7-9e79-f13d3ea9cf2d" />

  * **Pas 13:** Executar `slmgr /xpr` al Símbol del sistema per veure la data de caducitat o si l'activació és permanent.
 <img width="604" height="308" alt="image" src="https://github.com/user-attachments/assets/74f86249-8616-47bb-a072-60e0a3148480" />

  * **Pas 14:**  Investigar les diferències entre llicències

Les llicències de Windows es divideixen en diferents categories segons la seva flexibilitat, com s'adquireixen i el seu públic objectiu

| Tipus de Llicència | Característiques Principals |
| :--- | :--- |
| **OEM** | Queda lligada al maquinari (placa base) on s'instal·la per primer cop. No es pot transferir a un altre PC. Sol ser més econòmica i venir preinstal·lada. |
| **Retail** | Comprada a botigues o a la web oficial. És flexible: es pot transferir d'un PC a un altre (desactivant-la prèviament del vell). |
| **Volum** | Pensada per a grans empreses o institucions. Una mateixa clau pot activar múltiples equips de la mateixa organització. No es ven a usuaris particulars. |

---

  * **Pas 15:**  Consultar el cost de mercat de la versió instal·lada

El preu d'una llicència de Windows depèn de l'edició instal·lada i d'on es realitzi la consulta (botiga oficial de Microsoft o distribuïdors autoritzats). A continuació es mostren els preus orientatius actuals de la botiga oficial:

| Edició de Windows | Preu aproximat (Web oficial de Microsoft) |
| :--- | :--- |
| **Windows 11 Home** | ~145 € |
| **Windows 11 Pro** | ~259 € |
| **Windows 11 Pro for Workstations** | ~439 € |

-----

## Fase 4: Gestor d'arrencada

Estudi de la configuració del BCD (Boot Configuration Data).

  * **Pas 16 i 17:** Executar `bcdedit` amb permisos d'administrador.
 <img width="758" height="687" alt="image" src="https://github.com/user-attachments/assets/7aa46914-8c04-4d0a-924a-712da743e755" />

  * **Pas 18:** Identificar el **Boot Manager** (gestiona l'elecció de SO) i el **Boot Loader** (carrega el kernel del SO triat).
  * **Pas 19:** Analitzar camps com `timeout` (temps d'espera) i `path` (fitxer d'arrencada com `winload.efi`).
  * **Pas 20 i 21:** Respondre a les qüestions tècniques sobre la ubicació de la partició d'arrencada i els fitxers crítics detectats.

-----

## Fase 5: Xarxa bàsica

Configuració i test de connectivitat.

  * **Pas 23:** Visualitzar la configuració actual amb `ipconfig`.
  * **Pas 24:** Configurar el mode DHCP per rebre paràmetres automàtics de VirtualBox.
  * **Pas 25:** Provar la configuració d'una IP estàtica dins del mateix rang de xarxa.
  * **Pas 26:** Utilitzar `ping google.com` per validar la sortida a l'exterior.

-----

## Fase 6: Comandes generals

| Comanda | Acció |
| :--- | :--- |
| `dir` | Veure fitxers. |
| `mkdir` | Crear carpeta. |
| `tasklist` | Veure processos. |
| `taskkill /IM notepad.exe /F` | Tancar procés forçat. |
| `systeminfo` | Informació del sistema. |
| `netstat -an` | Connexions obertes. |
| `tree` | Estructura de directoris. |
| `shutdown /s /t 0` | Apagar l'equip. |


Ús de la CLI (Command Line Interface) per a la gestió del sistema.

  * **Pas 28:** Comparar `cmd` vs `PowerShell` (PowerShell permet treballar amb objectes i és el substitut modern).
  * **Pas 29 a 32:** Explorar comandes de fitxers (`dir`, `mkdir`, `del`), de sistema (`tasklist`, `systeminfo`, `hostname`) i de xarxa (`netstat`).
  * **Pas 33:** Interpretar les dades de rendiment i processos obtingudes.

-----

## Fase 7: Instal·lació d'aplicacions

Gestió del programari de l'estació de treball.

  * **Pas 34 a 36:** Descarregar i instal·lar programari extern (ex: VS Code o Chrome) mitjançant el navegador.
  * **Pas 37:** Utilitzar la Microsoft Store per instal·lar una eina nativa.
  * **Pas 39 i 40:** Realitzar el procés de desinstal·lació i verificar a la llista de programes que no queden residus.





