---
layout: default
title: "Sprint 4: Configuració del Programari de Base i Sistemes d’Emmagatzematge en Windows "
---

## Índex

- **Pràctica RAID 5 amb Windows Server 2022**
  - [1. Preparació de la màquina virtual](#1-preparació-de-la-màquina-virtual)
  - [2. Inicialitzar i configurar els discs](#2-inicialitzar-i-configurar-els-discs)
  - [3. Crear el RAID 5 des del Gestor de discs](#3-crear-el-raid-5-des-del-gestor-de-discs)
  - [4. Proves de funcionalitat](#4-proves-de-funcionalitat)
  - [5. Simulació de fallada (treure un disc)](#5-simulació-de-fallada-treure-un-disc)
  - [6. Simulació de segona fallada](#6-simulació-de-segona-fallada)
  - [7. Recuperació](#7-recuperació)
  - [8. Conclusions i observacions](#8-conclusions-i-observacions)


---

# Pràctica RAID 5 amb Windows Server 2022

## 1. Preparació de la màquina virtual

* A la màquina virtual amb Windows Server 2022:

  * Afegeix 3 discs addicionals (mínim) per fer el RAID 5 (igual mida, per exemple 10 GB cadascun)
    **[captura de la configuració dels discos a la VM]**
  * Inicia la màquina virtual

---

## 2. Inicialitzar i configurar els discs

1. Obre **Disk Management** (`diskmgmt.msc`)
   **[captura del gestor de discs obert]**
2. Quan surti l’assistent, inicialitza els nous discs com a MBR o GPT (triar GPT si la mida >2TB, en aquest cas no afecta)
   **[captura de la finestra d’inicialització dels discos]**
3. No els formatis ni creïs particions
   **[captura dels discos sense format ni particions]**

---

## 3. Crear el RAID 5 des del Gestor de discs

1. Clica amb el botó dret sobre un dels nous discos i selecciona **"New RAID-5 Volume"**
   **[captura del menú contextual amb l’opció RAID-5]**
2. Afegeix els altres 2 discos a la configuració
   **[captura de la selecció dels discos]**
3. Assigna una lletra de unitat (per exemple, `R:`)
   **[captura de l’assignació de lletra]**
4. Formata el volum amb NTFS, volum nou: `RAID5-Test`
   **[captura de la configuració del format]**
5. Espera que acabi el format i verifica que apareix com a un volum únic
   **[captura del volum RAID 5 creat]**

---

## 4. Proves de funcionalitat

1. Copia arxius al volum `R:\` (per exemple, una carpeta amb imatges o documents)
   **[captura copiant fitxers al volum]**
2. Obre i comprova que els fitxers són accessibles
   **[captura obrint fitxers]**

---

## 5. Simulació de fallada (treure un disc)

1. Torna a **Disk Management**
   **[captura del gestor de discs]**
2. Desconnecta (botó dret → **Offline**) un dels tres discos del RAID
   **[captura posant un disc en Offline]**
3. Observa que el volum segueix funcionant (estat degradat però accessible)
   **[captura del volum en estat degradat]**
4. Comprova que pots obrir els fitxers
   **[captura accedint als fitxers]**

---

## 6. Simulació de segona fallada

1. Posa **Offline** un segon disc del RAID
   **[captura del segon disc en Offline]**
2. Ara el volum deixarà de funcionar (RAID 5 només tolera una fallada)
   **[captura del volum inaccessible]**
3. Comprova que no pots accedir als arxius
   **[captura error d’accés]**

---

## 7. Recuperació

1. Torna a posar **Online** un dels discos que havies desconnectat
   **[captura posant el disc en Online]**
2. El volum s’hauria de recuperar automàticament o entrar en procés de reconstrucció
   **[captura del procés de reconstrucció]**
3. Torna a accedir als arxius i comprova la integritat
   **[captura accedint als fitxers recuperats]**

---

## 8. Conclusions i observacions

* RAID 5 distribueix la paritat entre tots els discos
* Pot tolerar la fallada d’un sol disc
* No és una còpia de seguretat, però ofereix redundància
* No funciona si fallen dos discos

---
