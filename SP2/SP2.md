---
layout: default
title: "Sprint 2: Instal·lació, Configuració de Programari de Base i Gestió de Fitxers"
---

## Índex

1. [Fase 1: Preparació del Sistema](#fase-1-preparació-del-sistema)
2. [Fase 2: Quotes i Usuaris](#fase-2-quotes-i-usuaris)
3. [Fase 3: Script de Còpia i Automatització](#fase-3-script-de-còpia-i-automatització)
4. [Fase 4: Verificació i Documentació](#fase-4-verificació-i-documentació)
5. [Fase 5: Gestió de Processos i Serveis](#fase-5-gestió-de-processos-i-serveis)
6. [Fase 6: Gestió de Permisos (ACLs)](#fase-6-gestió-de-permisos-acls)

Aquí tens la documentació detallada de la **Fase 1** per al teu Sprint 2, seguint l'estructura i els passos exactes que has proporcionat.

---

# Sprint 2: Administració de Discs, Usuaris i Automatització

## Fase 1 – Preparació del sistema

En aquesta fase prepararem l'entorn de treball sobre la màquina virtual creada a l'Sprint 1, afegint emmagatzematge addicional i configurant les particions necessàries per a les dades i la portabilitat.

### Pas 1. Afegir un nou disc virtual a la màquina virtual
Amb la màquina virtual apagada, cal accedir a la configuració de l'emmagatzematge a VirtualBox i afegir un segon disc dur virtual (VDI). Aquest disc s'utilitzarà per separar el sistema operatiu de les dades de l'usuari.

<img width="617" height="421" alt="image" src="https://github.com/user-attachments/assets/1fa304b6-5643-44c6-b66d-4e36fecd97ec" />

<img width="410" height="166" alt="image" src="https://github.com/user-attachments/assets/8940647e-10b6-4392-8c72-c1f2868cbeb9" />


### Pas 2. Iniciar Windows i obrir Gestió de discs
Un cop arrencada la màquina, farem clic dret sobre el botó d'Inici i seleccionarem **Gestió de discs** (*Disk Management*).

<img width="778" height="893" alt="image" src="https://github.com/user-attachments/assets/4a45c95b-daff-445f-9272-34f4ab587f88" />

### Pas 3. Inicialitzar el disc, crear dues particions: una anomenada Dades i una en FAT32 anomenada Portable
Dins del Gestor de discs, realitzarem les següents accions sobre el disc nou:
1. **Inicialitzar el disc** (triant l'estil de partició GPT o MBR).
   <img width="819" height="850" alt="image" src="https://github.com/user-attachments/assets/6813a0be-8a67-4e19-a273-a068a0131fde" />
2. Crear un **Nou volum simple** per a la primera partició:
   * **Nom:** Dades
   * **Sistema de fitxers:** NTFS
     <img width="488" height="388" alt="image" src="https://github.com/user-attachments/assets/ff06610e-c663-4ae2-9f74-a643df2ba383" />
<img width="488" height="392" alt="image" src="https://github.com/user-attachments/assets/32d6169e-ab8d-4643-803e-b4ee7e9b55ce" />
<img width="495" height="398" alt="image" src="https://github.com/user-attachments/assets/22c2935f-5c94-4d3e-ac36-337e764180fe" />

3. Crear un **Nou volum simple** amb l'espai restant:
   * **Nom:** Portable
   * **Sistema de fitxers:** FAT32

<img width="494" height="392" alt="image" src="https://github.com/user-attachments/assets/618b7dc6-ccdf-420b-a829-701f72a4923f" />
<img width="494" height="387" alt="image" src="https://github.com/user-attachments/assets/ebc5da4c-5153-444f-a873-0f430b1e809f" />
<img width="497" height="391" alt="image" src="https://github.com/user-attachments/assets/d8276a6d-4093-4193-9153-b667486b347c" />



### Pas 4. Assignar lletres i comprovar amb diskpart la configuració
Ens assegurarem que cada partició tingui una lletra d'unitat assignada (per exemple, E: i F:).
<img width="753" height="597" alt="image" src="https://github.com/user-attachments/assets/c7923684-8fc3-4ac9-b145-6c62ecbac398" />

Després, obrirem una consola de comandes (CMD) per verificar-ho mitjançant l'eina de línia de comandes `diskpart`.

Executarem les següents comandes:
* `diskpart`
* `list volume`
<img width="675" height="309" alt="image" src="https://github.com/user-attachments/assets/bd9960fa-b052-40f5-8744-ed740e4278e9" />


---

## Fase 2 – Quotes i usuaris

En aquesta fase, configurarem restriccions d'espai en disc per evitar que un sol usuari noli tot l'emmagatzematge de la partició de dades, i gestionarem els comptes d'usuari i grups que estaran subjectes a aquestes restriccions.

### Pas 5. Activar quotes de disc a la partició Dades (NTFS)
Les quotes de disc permeten als administradors controlar l'ús de l'emmagatzematge. Per activar-les:
1. Anirem a "Aquest equip", farem clic dret sobre la unitat **Dades (E:)** i seleccionarem **Propietats**.
2. Ens desplaçarem a la pestanya **Quota** i farem clic a **Mostra la configuració de quota**.
3. Marcarem la casella **Habilita la gestió de quotes**.

<img width="643" height="551" alt="image" src="https://github.com/user-attachments/assets/932865d7-5e39-4966-93a6-8de767e6fa4a" />


### Pas 6. Establir límit de 300 MB per usuari, amb notificació d’advertència
Dins de la mateixa finestra de configuració de quotes, definirem els límits per defecte per als nous usuaris:
1. Seleccionarem l'opció **Limita l'espai de disc a** i posarem **300 MB**.
2. En el camp **Estableix el nivell d'advertiment a**, posarem un valor inferior (per exemple, **250 MB**) per tal que l'usuari rebi un avís abans d'arribar al límit.
3. Marcarem l'opció **Denega l'espai de disc als usuaris que superin el límit de quota** per fer que la restricció sigui efectiva.

<img width="368" height="456" alt="image" src="https://github.com/user-attachments/assets/2031fdf6-c2aa-4ddd-bf9e-5d02912019f5" />


### Pas 7. Crear dos usuaris locals: alumne1 i alumne2
Crearem l'usuari **alumne1** i l'usuari **alumne2** amb les seves respectives contrasenyes.
<img width="554" height="475" alt="image" src="https://github.com/user-attachments/assets/02db2bab-d938-4a68-9820-fccbcd51551c" />


### Pas 8. Afegir-los a un grup nou anomenat Limitats
Per gestionar els permisos de forma conjunta, crearem un grup:
1. Dins de `lusrmgr.msc`, anirem a la carpeta **Grups**.
2. Crearem un grup nou anomenat **Limitats**.
3. Afegirem els usuaris **alumne1** i **alumne2** com a membres d'aquest grup.

<img width="739" height="625" alt="image" src="https://github.com/user-attachments/assets/516bb16a-ea07-468e-9671-651c06e7452a" />


### Pas 9. Provar la còpia de fitxers dins Dades per veure com actuen les quotes (superar límit)
Finalment, verificarem que la configuració funciona:
1. Iniciarem sessió com a **alumne1**.
2. Intentarem copiar un fitxer o carpeta que superi els 300 MB a la unitat **Dades (E:)**.
3. El sistema hauria de mostrar un error indicant que no hi ha prou espai, tot i que el disc físic estigui buit.

<img width="865" height="555" alt="image" src="https://github.com/user-attachments/assets/f38f0df3-31b1-49bb-8ae9-cb92f3f15ff9" />


---
## Fase 3 – Script de còpia i automatització


### Pas 10. Afegir tercer disc virtual, formatar-lo en NTFS com a Backups
Repetirem el procés de la Fase 1: afegirem un tercer disc a VirtualBox i, des de la **Gestió de discs**, l'inicialitzarem i crearem un volum simple anomenat **Backups** en format **NTFS**.

<img width="804" height="691" alt="image" src="https://github.com/user-attachments/assets/ddbd00f4-a184-45f1-b7f4-32ab77e6d73f" />


### Pas 11. Crear carpeta CòpiesUsuaris dins Backups
Dins de la nova unitat, crearem una carpeta arrel per centralitzar els fitxers dels alumnes.
<img width="531" height="289" alt="image" src="https://github.com/user-attachments/assets/7c833471-8c75-435c-9ce3-ffea1a167501" />

### Pas 12. Crear un script .bat que copiï C:\Users\%USERNAME% a E:\CòpiesUsuaris\%USERNAME%
Obre el bloc de notes i crea un fitxer anomenat `copia_seguretat.bat`. Utilitzarem la variable d'entorn `%USERNAME%` perquè l'script sigui genèric per a qualsevol usuari que l'executi. La comanda recomanada és `robocopy` per la seva eficiència:

```
@echo off
robocopy "C:\Users\%USERNAME%" "F:\CòpiesUsuaris\%USERNAME%" /E /R:0 /W:0
pause
```

<img width="666" height="226" alt="image" src="https://github.com/user-attachments/assets/bed3faff-3be0-4ff8-af27-b35d991bd977" />

### Pas 13. Obre gpedit.msc → Configuració d’usuari → Scripts → Inici de sessió
Executa `gpedit.msc` per obrir l'Editor de polítiques de grup local. Navega per l'arbre de carpetes: **Configuració de l'usuari** > **Configuració de Windows** > **Scripts (Inici de sessió/Tancament de sessió)**.
<img width="682" height="320" alt="image" src="https://github.com/user-attachments/assets/5c37bb24-4631-46b4-bf7e-74143923b871" />


### Pas 14. Assigna l’script perquè s’executi automàticament quan alumne1 o alumne2 inicien sessió
1. Fes doble clic a **Inici de sessió**.
2. Fes clic a **Afegeix** i selecciona el fitxer `.bat` que has creat anteriorment.
3. Aplica els canvis. Ara, cada cop que un usuari del grup "Limitats" entri, les seves dades es copiaran al disc de Backups.

<img width="590" height="489" alt="image" src="https://github.com/user-attachments/assets/ee1ba1cd-1577-4670-91c7-c6f9e79a0367" />
