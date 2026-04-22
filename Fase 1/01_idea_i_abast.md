# COSMIC KEEPER
**Disseny de Sistema i Abast del Projecte**
*Autor: Izan de Maya*

---

## Índex
1. [Objectiu del joc](#1-objectiu-del-joc)
2. [Rol del jugador](#2-rol-del-jugador)
3. [Regles bàsiques i condicions](#3-regles-bàsiques-i-condicions)
4. [Bucle principal (Core Loop)](#4-bucle-principal-core-loop)
5. [Repte i dificultat](#5-repte-i-dificultat)
6. [Limitacions explícites](#6-limitacions-explícites)
7. [Riscos tècnics identificats](#7-riscos-tècnics-identificats)
8. [Exploració amb IA](#8-exploració-amb-ia)
9. [Proposta final i justificació](#9-proposta-final-i-justificació)
10. [Mini pla de treball](#10-mini-pla-de-treball)
11. [Eines previstes](#11-eines-previstes)

---

## 1. Objectiu del joc
L'objectiu principal és **restaurar la xarxa d'energia galàctica** a través de diversos sectors espacials. El jugador ha de recollir tots els nodes d'energia (cel·les) dispersos per cada nivell per activar el portal de salt i avançar al següent sector.

## 2. Rol del jugador
El jugador controla un **Keeper**, un robot de manteniment espacial equipat amb un jetpack.

* **Moviment Lateral:** Inèrcia realista que requereix precisió per evitar col·lisions.
* **Jetpack:** Permet elevar-se i mantenir el vol, amb un consum d'energia limitat.
* **Gestió de Recursos:** Vigilància constant de la barra d'energia; aquesta es recarrega automàticament en entrar en contacte amb el terra.

## 3. Regles bàsiques i condicions

### Condicions de Victòria
* **Per Nivell:** Recollir el nombre requerit de nodes i creuar el portal de sortida.
* **Final del Joc:** Superar els **20 sectors** de la campanya.

### Condicions de Derrota
* Col·lidir amb un enemic o obstacle perillós (provoca el reinici immediat del nivell).
* *Nota:* La manca d'energia no és derrota instantània, però pot provocar caigudes fatals.

---

## 4. Bucle principal (Core Loop)
El joc es basa en un cicle repetitiu de tres fases:
1.  **Exploració i Maniobra:** Navegació per l'entorn esquivant enemics i perills.
2.  **Recol·lecció:** Obtenció dels nodes d'energia repartits per l'escenari.
3.  **Extracció:** Un cop recollits tots els nodes, arribar al portal per saltar de bioma.

## 5. Repte i dificultat
* **Repte Principal:** El domini de les físiques (inèrcia i gravetat) en un entorn hostil.
* **Escalat de Dificultat:**
    * Nivells més grans i laberíntics.
    * Increment de la velocitat dels enemics per cada sector.
    * Major quantitat de nodes requerits.
    * Variació visual i ambiental dels biomes.

## 6. Limitacions explícites
Per garantir un enfocament arcade pur, **no s'inclourà**:
* **Combat Directe:** No es pot disparar; el focus és l'evasió.
* **Guardat Permanent:** Experiència de "sessió única".
* **Inventari:** Sense gestió d'objectes complexa.
* **Multijugador:** Disseny exclusiu per a un sol jugador.

---

## 7. Riscos Tècnics Identificats
* **Gestió de Físiques (AABB):** Evitar vibracions o que el personatge es quedi travat en les parets del *tileset*.
* **Rendiment:** Mantenir una taxa de frames estable al Canvas malgrat l'augment de partícules i enemics.
* **Generació Procedural:** Validació algorítmica per assegurar que tots els nivells generats siguin completables.

## 8. Exploració amb IA (Prompts)
> **Prompt 1:** *"Dissenya una mecànica de risc/recompensa per a un joc de jetpack on l'energia és limitada."*
> * **Resultat:** "Bateries Sobrecarregades" que atorguen velocitat infinita (5s) seguit d'un bloqueig del jetpack (2s).

> **Prompt 2:** *"Proposa tipus d'enemics passius que dificultin el moviment sense atacar directament."*
> * **Resultat:** Enemics tipus "Imant" (atracció) i "Ventiladors" (alteració de la inèrcia).

---

## 9. Proposta Final i Justificació
S'ha triat la **mecànica d'inèrcia pura amb recàrrega terrestre**.
* **Justificació:** És la opció més viable per a un MVP (Producte Mínim Viable). Centra la diversió en el "feel" del control i redueix la complexitat de sistemes de combat o IA avançada.

## 10. Mini Pla de Treball
| Fase | Títol | Tasques Clau |
| :--- | :--- | :--- |
| **Fase 1** | Fonaments | Configuració Canvas, moviment i col·lisions. |
| **Fase 2** | Entorn | Càmera (scroll), generació de rajoles i nodes. |
| **Fase 3** | Enemics | Patrons de moviment, IA bàsica i biomes. |
| **Fase 4** | Poliment | Partícules, menús i ajust de dificultat. |

## 11. Eines Previstes
* **IDE:** Visual Studio Code.
* **Llenguatge:** JavaScript, HTML5 Canvas i CSS3.
* **IA:** Gemini (depuració i ideació).
* **Disseny Gràfic:** Aseprite / Piskel (Pixel-art).