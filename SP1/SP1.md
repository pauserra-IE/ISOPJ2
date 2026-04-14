---
layout: default
title: "Sprint 1: Instal·lació, Configuració Inicial i Programari de Base"
---

#Sprint 1: Instal·lació, Configuració Inicial i Programari de Base (WINDOWS)

---
layout: default
title: "Sprint 1: Instal·lació, Configuració Inicial i Programari de Base"
---

# Sprint 1: Instal·lació, Configuració Inicial i Programari de Base

## Índex
1. [Introducció](#introducció)
2. [Fase 1: Instal·lació del Sistema Operatiu](#fase-1-instal·lació-del-sistema-operatiu)
3. [Fase 2: Punts de Restauració](#fase-2-punts-de-restauració)
4. [Fase 3: Llicències de Windows](#fase-3-llicències-de-windows)
5. [Fase 4: Gestor d'Arrencada](#fase-4-gestor-darrencada)
6. [Fase 5: Xarxa Bàsica](#fase-5-xarxa-bàsica)
7. [Fase 6: Comandes Generals](#fase-6-comandes-generals)
8. [Fase 7: Instal·lació d'Aplicacions](#fase-7-instal·lació-daplicacions)

---

## Introducció
Aquest document detalla el procés d'instal·lació i configuració inicial d'un entorn Windows. L'objectiu és establir una base sòlida de treball, assegurant la recuperació del sistema, la legalitat del programari i el control mitjançant línia de comandes.

---

## Fase 1: Instal·lació del Sistema Operatiu
Preparació de l'entorn virtualitzat i desplegament del sistema.

### Pas 1-5: Configuració de la Màquina Virtual
1. Crear una nova màquina a **VirtualBox**.
2. Assignar un mínim de **4 GB de RAM** i un disc dur de **40 GB**.
3. Carregar la imatge **ISO** de Windows 10 o 11.

> **[CAPTURA DE PANTALLA: Propietats de la MV a VirtualBox amb la RAM i el disc destacats]**

### Pas 6: Procés d'instal·lació
1. Arrencar la màquina i seguir l'assistent (idioma, regió).
2. Crear l'usuari principal amb la seva contrasenya.
3. Finalitzar la instal·lació fins a arribar a l'escriptori.

> **[CAPTURA DE PANTALLA: Escriptori de Windows operatiu]**

---

## Fase 2: Punts de Restauració
Gestió de la seguretat davant de canvis crítics.

### Pas 6-8: Activació i creació
1. Cercar "Crear un punt de restauració" al menú Inici.
2. **Activar la protecció** per a la unitat C:.
3. Crear un punt manualment anomenat "Post-Instal·lació".

> **[CAPTURA DE PANTALLA: Finestra de Protecció del sistema mostrant el punt creat]**

### Pas 9-10: Prova de restauració
1. Instal·lar qualsevol aplicació de prova.
2. Executar la restauració del sistema per verificar que l'aplicació desapareix i el sistema torna a l'estat anterior.

---

## Fase 3: Llicències de Windows
Verificació del tipus de contracte i activació.

### Pas 11-13: Verificació
1. Consultar l'estat a **Configuració > Sistema > Activació**.
2. Executar `slmgr /xpr` al CMD per veure la caducitat de la llicència.

> **[CAPTURA DE PANTALLA: Resultat de la comanda slmgr /xpr]**

### Pas 14-15: Recerca
* Identificar si la llicència és Retail, OEM o Volum.
* Consultar el preu actual oficial segons la versió (Home/Pro).

---

## Fase 4: Gestor d'Arrencada
Configuració del llançament del sistema.

### Pas 16-21: BCDEDIT
1. Obrir CMD com a administrador.
2. Executar `bcdedit` per analitzar el **Boot Manager** i el **Boot Loader**.
3. Identificar el fitxer de càrrega (`winload.efi`) i el temps d'espera (`timeout`).

> **[CAPTURA DE PANTALLA: Terminal amb la sortida de la comanda bcdedit]**

---

## Fase 5: Xarxa Bàsica
Connectivitat i diagnòstic inicial.

### Pas 22-26: Configuració IP
1. Utilitzar `ipconfig` per veure els paràmetres actuals.
2. Validar si s'usa DHCP o IP fixa.
3. Fer un `ping google.com` per confirmar la navegació.

> **[CAPTURA DE PANTALLA: Terminal fent ping correctament]**

---

## Fase 6: Comandes Generals
Eines d'administració per terminal.

### CMD vs PowerShell
* **CMD:** Consola d'ordres clàssica.
* **PowerShell:** Entorn de scripting avançat per a automatització.

### Comandes principals
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

---

## Fase 7: Instal·lació d'Aplicacions
Desplegament del programari de l'usuari.

### Pas 34-40: Gestió de programari
1. Instal·lar eines essencials (Chrome, VS Code) des del navegador.
2. Utilitzar la **Microsoft Store** per a aplicacions de confiança.
3. Provar de desinstal·lar una aplicació des del panell de configuració.

> **[CAPTURA DE PANTALLA: Llista d'aplicacions instal·lades a la Configuració]**
