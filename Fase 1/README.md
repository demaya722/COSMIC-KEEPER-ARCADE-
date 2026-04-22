# 🎮 Disseny del Joc: Sistema de Joc i Mecàniques

---

## 1. Objectiu del joc
L'objectiu principal és restaurar la xarxa d'energia galàctica a través de diversos sectors espacials.  
El jugador ha de recollir tots els nodes d'energia (cel·les) dispersos per cada nivell per activar el portal de salt i avançar al següent sector.

---

## 2. Rol del jugador
El jugador controla un **Keeper**, un robot de manteniment espacial equipat amb un jetpack.

### Mecàniques principals:
- **Moviment lateral:** Basat en una inèrcia realista que requereix precisió per evitar col·lisions.
- **Jetpack:** Permet elevar-se i mantenir el vol amb consum d'energia limitat.
- **Gestió de recursos:** L'energia del jetpack es recarrega automàticament quan el personatge està en contacte amb el terra.

---

## 3. Regles bàsiques i condicions

### Condicions de victòria
- **Per nivell:** Recollir tots els nodes d'energia requerits i accedir al portal de sortida.
- **Final del joc:** Superar els 20 sectors de la campanya.

### Condicions de derrota
- Col·lisionar amb un enemic o obstacle perillós (reinici del nivell).
- La manca d'energia en moments crítics pot dificultar la recuperació, però no implica derrota immediata si es pot aterrar amb seguretat.

---

## 4. Bucle principal (Core Loop)

El joc es basa en un cicle de joc estructurat en tres fases:

1. **Exploració i maniobra**  
   Navegació per l'entorn utilitzant el jetpack mentre s'eviten obstacles i enemics.

2. **Recol·lecció**  
   Obtenció dels nodes d'energia distribuïts pel nivell.

3. **Extracció**  
   Activació del portal i transició cap al següent sector un cop completada la recol·lecció.

---

## 5. Repte i dificultat

### Repte principal
El domini de les físiques (inèrcia i gravetat) combinat amb el comportament dels enemics.

### Escalat de dificultat
- Increment de la mida i complexitat dels nivells.
- Augment progressiu de la velocitat dels enemics.
- Major quantitat de nodes d'energia a recollir.
- Variació visual dels biomes per enriquir l'experiència.

---

## 6. Limitacions del sistema

Per mantenir un enfocament clar i centrat en la jugabilitat arcade:

- **Sense combat directe:** El jugador no pot atacar; el repte és l'evasió.
- **Sense guardat persistent:** Experiència basada en sessions curtes (estil arcade).
- **Sense inventari:** No hi ha gestió d'objectes.
- **Un sol jugador:** No hi ha funcionalitat multijugador.

---

## 7. Riscos tècnics identificats

- **Col·lisions i físiques:** Possibles errors com vibracions o bloquejos en entorns de tiles (AABB).
- **Rendiment:** Caigudes de FPS en nivells amb alta càrrega d'elements visuals.
- **Generació procedural:** Dificultat per garantir nivells sempre completables.

---

## 8. Exploració amb IA

### Prompt 1
> "Dissenya una mecànica de risc/recompensa per a un joc de jetpack amb energia limitada."

**Resultat:**  
Introducció de *bateries sobrecarregades* que proporcionen velocitat il·limitada durant 5 segons, amb una penalització posterior.

### Prompt 2
> "Proposa enemics passius que dificultin el moviment sense atacar."

**Resultat:**  
- **Imants:** Atrauen el jugador cap a zones perilloses.  
- **Ventiladors:** Alteren la trajectòria i la inèrcia del moviment.

---

## 9. Proposta final i justificació

S'adopta una mecànica basada en **inèrcia pura amb recàrrega terrestre**.

**Justificació:**  
Aquesta solució és òptima per a un MVP, ja que redueix la complexitat tècnica (sense combat ni IA avançada) i centra l'experiència en el control i la sensació de moviment, clau en jocs arcade.

---

## 10. Pla de treball

| Fase | Descripció |
|------|-----------|
| **Fase 1** | Sistema de moviment, Canvas i col·lisions bàsiques |
| **Fase 2** | Implementació de càmera, tiles i nodes d'energia |
| **Fase 3** | Desenvolupament d'enemics i variació de biomes |
| **Fase 4** | Poliment visual, partícules i ajust de dificultat |

---

## 11. Eines previstes

- **IDE:** Visual Studio Code  
- **Tecnologies:** JavaScript, HTML i CSS  
- **Execució:** Navegador web (sense dependències externes)  
- **Intel·ligència Artificial:** Gemini (suport en codi i disseny)  
- **Disseny gràfic:** Aseprite / Piskel (pixel-art)

---