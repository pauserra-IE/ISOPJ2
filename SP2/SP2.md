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

---

## Fase 4 – Verificació i documentació

L'objectiu d'aquesta fase és validar que totes les configuracions de discs, quotes d'usuari i automatització mitjançant scripts funcionen correctament i de forma integrada.

### Pas 15. Verificació del sistema
Per comprovar que el sistema està ben configurat, realitzarem les següents accions:

1.  **Comprovació de l'script de còpia:** Iniciarem sessió amb l'usuari **alumne1**. En entrar, s'ha d'obrir automàticament una finestra de consola executant el fitxer `.bat`. Un cop tancada, anirem a la unitat de **Backups** i verificarem que s'ha creat una carpeta amb el nom de l'usuari que conté els seus fitxers personals.

<img width="465" height="168" alt="image" src="https://github.com/user-attachments/assets/d2de44e4-07a4-4c87-8d43-00951489de89" />

   
2.  **Comprovació de la quota de disc:** Dins de la sessió d'alumne1, anirem a la unitat **Dades**. Intentarem copiar un fitxer gran (superior a 300 MB). El sistema ha de llançar un avís d'espai insuficient, demostrant que la quota està operativa tot i que el disc tingui espai físic real.

<img width="567" height="463" alt="image" src="https://github.com/user-attachments/assets/e3b6de61-1229-4fad-976f-de5b3b1972aa" />


---

## Fase 5 – Gestió de processos i serveis

En aquesta fase analitzarem el consum de recursos del sistema i aprendrem a optimitzar-lo eliminant processos que no són necessaris per al treball diari.

### Pas 19. Llistar processos actius
Iniciarem sessió com a **alumne1** i obrirem una consola de comandes (CMD). Executarem la comanda `tasklist` per veure tots els processos en execució. Per guardar aquesta informació, bolcarem el resultat en un fitxer de text dins de la carpeta de l'usuari:
`tasklist > C:\Users\alumne1\processos_inici.txt`
<img width="534" height="79" alt="image" src="https://github.com/user-attachments/assets/71db388f-552a-4c19-8e0c-095d072b7ff6" />
<img width="744" height="946" alt="image" src="https://github.com/user-attachments/assets/5856aac9-f8c9-4db6-8785-87e2c46c2160" />

### Pas 20. Identificar processos prescindibles
Analitzarem la llista per detectar aplicacions que consumeixen memòria RAM innecessàriament en una màquina virtual.

| Nom del procés | Justificació per eliminar-lo |
| :--- |:--- |
| `OneDrive.exe` | No s'utilitza emmagatzematge al núvol en aquest exercici. |
| `Teams.exe` |  Consum molt elevat de recursos; innecessari per a l'administració de discs. |
| `SkypeApp.exe` |  Servei de missatgeria que s'inicia per defecte i resta agilitat al sistema. |

### Pas 21. Eliminar processos manualment
Utilitzarem la comanda `taskkill` per tancar un procés de forma forçada i comprovar-ne l'efecte.
* **Comanda:** `taskkill /IM OneDrive.exe /F`

<img width="726" height="201" alt="image" src="https://github.com/user-attachments/assets/5d55cf7a-21bf-4563-84d1-b4357727506d" />

### Pas 22. Automatitzar-ho a l’inici de sessió
Perquè la neteja de recursos sigui automàtica, editarem l'script `.bat` creat a la fase anterior. Afegirem les comandes `taskkill` per a OneDrive i Teams. D'aquesta manera, quan **alumne2** iniciï sessió, aquests processos es tancaran sols.

<img width="775" height="218" alt="image" src="https://github.com/user-attachments/assets/90c47ed8-9fb2-4f69-bdda-1a66d4946037" />

I tal com es veu en la seguent captura en reengegar amb alumne2 no s'han executat
<img width="746" height="317" alt="image" src="https://github.com/user-attachments/assets/c3eb1358-fad9-44fb-bc31-25ed47cb7af0" />



### Pas 23. Documentació i reflexió
* **Procés crític:** Si matem el procés `explorer.exe`, la interfície gràfica (escriptori, barra de tasques) desapareixerà. Això ensenya la diferència entre processos d'usuari i processos del sistema.
* **Rendiment:** Eliminar processos prescindibles permet que la màquina virtual funcioni amb més fluïdesa, reduint la càrrega sobre la CPU i la memòria RAM de l'equip amfitrió.
---

## Fase 6 – Gestió de permisos (ACLs)

En aquesta fase configurarem permisos especials per a carpetes, anant més enllà dels permisos de grup per aplicar restriccions a usuaris específics dins d'un mateix grup.

### Què són les ACLs i com funcionen a Windows
A Windows, cada fitxer i carpeta té una llista de control d'accés (ACL). Aquesta llista defineix quina identitat (usuari o grup) té afectació i quins permisos té (lectura, escriptura, control total, etc.). Les ACLs permeten una granularitat molt més alta que els permisos compartits estàndard.

### Pas 24. Crear la carpeta
Iniciarem sessió com a **administrador** i crearem una carpeta anomenada **Projectes** dins de la partició **Dades (D:)**.
<img width="693" height="212" alt="image" src="https://github.com/user-attachments/assets/d35ccf05-7557-452a-a839-283a60ba081a" />

### Pas 25. Assignar permisos normals al grup
Configurarem la carpeta perquè el grup tingui el control inicial:
1. Farem clic dret a `D:\Projectes` -> **Propietats** -> pestanya **Seguretat**.
2. Farem clic a **Avançat** i després a **Desactiva l'herència**, triant l'opció de conservar els permisos existents per poder-los modificar.
   <img width="746" height="949" alt="image" src="https://github.com/user-attachments/assets/9c2a2c49-05e1-4509-92e4-a5f4d4141163" />
   <img width="510" height="338" alt="image" src="https://github.com/user-attachments/assets/b30b5e4b-54de-42f5-bce1-2c3fb91dc12c" />

   
3. Eliminarem qualsevol entrada d'usuaris genèrics com "Usuaris" o "Tothom".
4. Afegirem el grup **Limitats** i li assignarem **Control total**.
<img width="783" height="497" alt="image" src="https://github.com/user-attachments/assets/bf86a192-2122-4c04-8227-4f17456c11ae" />
<img width="764" height="383" alt="image" src="https://github.com/user-attachments/assets/efa89482-49b8-4436-ae0c-9023c610a58f" />



### Pas 26. Comprovar accés amb alumne1
Iniciarem sessió com a **alumne1**:
1. Entrarem a `D:\Projectes`.
2. Crearem un fitxer de text, el modificarem i l'esborrarem.
<img width="604" height="202" alt="image" src="https://github.com/user-attachments/assets/62c64d0b-16f6-4804-9d84-e9dacd2a27ce" />
<img width="565" height="461" alt="image" src="https://github.com/user-attachments/assets/01469f36-19a5-4953-bc3e-48d5e63a01b5" />
<img width="567" height="279" alt="image" src="https://github.com/user-attachments/assets/182afba7-f708-4c28-8f26-d14456b47427" />


3. Com que som membres de "Limitats", el sistema ens ha de permetre fer totes aquestes operacions sense restriccions.

### Pas 27. Aplicar excepció per alumne2
Ara aplicarem una restricció específica per a un membre del grup. Com a **administrador**, obrirem la consola i executarem:
`icacls "D:\Projectes" /grant:r alumne2:(R)`

Aquesta comanda substitueix els permisos heretats de l'alumne2 i li assigna exclusivament permisos de **Lectura (R)**.

<img width="760" height="197" alt="image" src="https://github.com/user-attachments/assets/5cf8b39b-647c-4c7b-8a3f-61177f905045" />



### Pas 28. Comprovar l'excepció amb alumne2
Iniciarem sessió com a **alumne2** per verificar l'eficàcia de l'ACL:
1. Intentarem obrir un fitxer existent a `D:\Projectes`: el sistema ens ha de deixar llegir-lo.
2. Intentarem crear un fitxer nou o modificar un existent: Windows ens ha de mostrar un missatge de **"Accés denegat"**.

<img width="570" height="394" alt="image" src="https://github.com/user-attachments/assets/9fdeec28-bdb7-49ac-875f-ad1ecb725371" />


### Pas 29. Consultar els permisos aplicats
Finalment, verificarem l'estat final de les ACLs des de la línia de comandes com a administrador executant:
`icacls "E:\Projectes"`

<img width="725" height="204" alt="image" src="https://github.com/user-attachments/assets/e11603f9-2fa2-4622-910d-fd09c889426e" />

Explicació dels codis que apareixeran:
(R): Permís de només lectura per a l'alumne2.

(RX): Permís de lectura i execució per al grup (no poden escriure ni esborrar).

(OI)(CI): Indica que els permisos s'heretaran automàticament a tots els fitxers i carpetes que es creïn dins de "Projectes" en un futur.


