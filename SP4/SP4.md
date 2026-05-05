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

<img width="1050" height="610" alt="image" src="https://github.com/user-attachments/assets/8e40c0f7-c4a9-4181-8f21-5ac9506b1276" />


  * Inicia la màquina virtual

---

## 2. Inicialitzar i configurar els discs

1. Obre **Disk Management** (`diskmgmt.msc`)
<img width="432" height="235" alt="image" src="https://github.com/user-attachments/assets/561048b2-2219-477b-aa5f-dfa1031309db" />

2. Quan surti l’assistent, inicialitza els nous discs com a MBR o GPT (triar GPT si la mida >2TB, en aquest cas no afecta)
<img width="771" height="759" alt="image" src="https://github.com/user-attachments/assets/de5d3426-cd50-482b-a19c-a445fcad82b5" />

3. No els formatis ni creïs particions
<img width="941" height="814" alt="image" src="https://github.com/user-attachments/assets/39814cb9-656b-4b55-a8fe-dd0d5ec5d344" />

---

## 3. Crear el RAID 5 des del Gestor de discs

1. Clica amb el botó dret sobre un dels nous discos i selecciona **"New RAID-5 Volume"**
<img width="615" height="205" alt="image" src="https://github.com/user-attachments/assets/e3c2579c-c09b-4609-ba47-8ccee5bd432b" />

2. Afegeix els altres 2 discos a la configuració
<img width="587" height="491" alt="image" src="https://github.com/user-attachments/assets/9bcac05d-a6ff-450b-bada-abd0ca02c6b4" />

3. Assigna una lletra de unitat (per exemple, `R:`)
<img width="580" height="487" alt="image" src="https://github.com/user-attachments/assets/6508498d-7544-486c-b32c-6b7e0a7da768" />

4. Formata el volum amb NTFS, volum nou: `RAID5-Test`
<img width="597" height="471" alt="image" src="https://github.com/user-attachments/assets/a8edc3a2-f84f-4770-a4ef-48e6d8d7b0ef" />

5. Espera que acabi el format i verifica que apareix com a un volum únic
<img width="538" height="484" alt="image" src="https://github.com/user-attachments/assets/fecbf056-6c8e-415f-9a2d-532483e54b65" />

<img width="868" height="824" alt="image" src="https://github.com/user-attachments/assets/e989c19e-c36a-4187-8e2b-7595c53bb99c" />

<img width="657" height="597" alt="image" src="https://github.com/user-attachments/assets/e67febc6-8d57-4abc-9591-57b2502f06a7" />


---

## 4. Proves de funcionalitat

1. Copia arxius al volum `R:\` (per exemple, una carpeta amb imatges o documents)
<img width="582" height="233" alt="image" src="https://github.com/user-attachments/assets/c60b6e5c-3bc0-435b-8d39-64d647119462" />

2. Obre i comprova que els fitxers són accessibles
<img width="793" height="617" alt="image" src="https://github.com/user-attachments/assets/16436092-ff07-4d64-9075-8a3a58ba27a8" />

---

## 5. Simulació de fallada (treure un disc)

1. Torna a **Disk Management**
2. Desconnecta (botó dret → **Offline**) un dels tres discos del RAID
3. Observa que el volum segueix funcionant (estat degradat però accessible)
  <img width="959" height="646" alt="image" src="https://github.com/user-attachments/assets/c799d32c-f94a-4b4e-a1af-7988be1c6bec" />

4. Comprova que pots obrir els fitxers
<img width="785" height="632" alt="image" src="https://github.com/user-attachments/assets/92c0a70b-d5b8-48df-a835-b36fee2e9aae" />

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
<img width="308" height="131" alt="image" src="https://github.com/user-attachments/assets/5ee876b5-be27-4559-bca6-01100a2e4c53" />

2. El volum s’hauria de recuperar automàticament o entrar en procés de reconstrucció
Procés de reconstrucció en curs:
<img width="717" height="564" alt="image" src="https://github.com/user-attachments/assets/48802c82-718e-49eb-b21e-8787b8af00c2" />
Procés de reconstrucció en complet:
<img width="714" height="567" alt="image" src="https://github.com/user-attachments/assets/8ff970cf-fea7-48ff-b4f1-b20b32e1a56e" />

3. Torna a accedir als arxius i comprova la integritat
<img width="930" height="697" alt="image" src="https://github.com/user-attachments/assets/cf169044-b725-4b7c-b2c0-b3adf45c9ee7" />
Es poden accedir a les dues captures de pantalla que hi havia correctament.

---

## 8. Conclusions i observacions

* RAID 5 distribueix la paritat entre tots els discos
* Pot tolerar la fallada d’un sol disc
* No és una còpia de seguretat, però ofereix redundància
* No funciona si fallen dos discos

---
