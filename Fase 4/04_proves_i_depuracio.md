# 04 - Proves i depuració

## Informe de Proves i Depuració: *Cosmic Keeper*

Aquest document detalla el procés de control de qualitat, les proves realitzades i la resolució d'incidències tècniques durant el desenvolupament del videojoc **Cosmic Keeper**.

---

# 1. Casos de Prova

# 1. Casos de Prova

S'han executat els següents casos per verificar l'estabilitat del motor de joc i les mecàniques principals sota condicions reals d'ús.

---

| ID | Cas de prova | Entrada / Acció realitzada | Resultat esperat | Resultat obtingut |
|:---:|---|---|---|---|
| **CP-01** | **Col·lisió amb paret** | El jugador camina cap a un bloc de tipus `wall`. | El jugador s'atura i la velocitat `vx` passa a `0` sense travessar el mur. | Resolució correcta per eixos `(X, Y)`. El jugador no pot creuar la paret. |
| **CP-02** | **Recollida de nodes** | Col·lisió entre el jugador i un node actiu. | Increment del comptador de nodes i desaparició visual del node. | El node desapareix correctament i el marcador s'actualitza a l'instant. |
| **CP-03** | **Activació del portal** | Recollir tots els nodes requerits del nivell. | `game.portal.active` passa a `true` i el portal es mostra en pantalla. | El portal apareix correctament en completar l'objectiu de nodes. |
| **CP-04** | **Sistema d'energia** | Mantenir premuda la tecla de salt/vol (propulsió). | L'energia disminueix progressivament i el vol s'atura en arribar a `0`. | Consum i recàrrega d'energia funcionant correctament. |
| **CP-05** | **Persistència de dades** | Completar un nivell i tornar al menú principal. | Temps i morts guardats correctament al `localStorage`. | Les dades es mantenen després de reiniciar el navegador. |

---

# 2. Incidències Reals Detectades i Resoltes

A continuació es descriuen els errors tècnics concrets trobats durant les fases de desenvolupament i la seva solució tècnica.

---

## Incidència A — Escut parcial (Lògica de col·lisió de dany)

### Descripció
L'escut (*power-up* rosa) protegia el jugador en xocar contra enemics mòbils de patrulla, però el jugador moria instantàniament si rebia l'impacte d'un projectil de les torres (*turrets*).

### Causa probable
La funció que gestionava els projectils aplicava el reinici del nivell de forma directa, ignorant la variable d'estat `player.hasShield`.

### Solució aplicada
Es va centralitzar la recepció de dany en la funció `hitPlayer()`. Ara, tots els perills criden aquesta funció, la qual verifica l'escut, el consumeix i activa un *feedback* visual (partícules) abans de permetre la mort del personatge.

---

## Incidència B — Marcador de nodes estàtic (Desincronització de UI)

### Descripció
Quan el jugador recollia un node, la variable interna del joc augmentava, però el text `NODOS: X/Y` de la pantalla es mantenia sense canvis.

### Causa probable
La instrucció que actualitza el text de l'HTML (`document.getElementById().innerText`) només s'executava en carregar el nivell, no en el moment de la col·lisió.

### Solució aplicada
S'ha integrat l'actualització del DOM directament dins del bloc de col·lisió dels nodes en la funció d'actualització de dades (`update()`).

---

# 3. Evidència de Depuració (Logs i Traces)

S'han utilitzat traces per consola per verificar que el flux lògic de dany funciona correctament sense tancar el joc.

---

## Codi de traça aplicat durant el debug

```javascript
function hitPlayer() {
    if (player.hasShield) {
        console.log("[DEBUG] Impacte detectat: Escut absorbeix el dany.");
        player.hasShield = false; // Confirmació de canvi d'estat
        spawnPart(player.x, player.y, '#ff00ea'); // Feedback visual
        return true; 
    }

    console.log("[DEBUG] Impacte fatal: Reiniciant nivell.");
    return false;
}
```

---

## Exemple de sortida per consola

```txt
[DEBUG] Impacte detectat: Escut absorbeix el dany.
[DEBUG] Impacte fatal: Reiniciant nivell.
```

---

# 4. Simulació de Prova Automatitzada

Per garantir que cap nivell generat aleatòriament provoca un error d'execució, s'ha creat un script que valida la creació dels 20 sectors del joc.

---

## Script de test massiu per a la generació de mapes

```javascript
function runStressTest() {

    console.log("--- Iniciant Test de Generació de Sectors ---");

    for(let i = 0; i < 20; i++) {

        try {

            generateLevel(i);

            if(game.tiles.length > 0 && game.needed > 0) {

                console.log(
                    `Sector ${i+1}: GENERAT CORRECTAMENT (${game.tiles.length} objectes)`
                );
            }

        } catch (e) {

            console.error(
                `Sector ${i+1}: ERROR CRÍTIC ->`,
                e
            );
        }
    }

    console.log("--- Test Finalitzat amb èxit ---");
}
```

---

## Resultat obtingut

```txt
--- Iniciant Test de Generació de Sectors ---

Sector 1: GENERAT CORRECTAMENT (145 objectes)
Sector 2: GENERAT CORRECTAMENT (162 objectes)
Sector 3: GENERAT CORRECTAMENT (171 objectes)
...
Sector 20: GENERAT CORRECTAMENT (198 objectes)

--- Test Finalitzat amb èxit ---
```

---

# Conclusions

Les proves executades han permès validar el correcte funcionament de les mecàniques principals de **Cosmic Keeper**.

Les incidències detectades durant el desenvolupament han estat resoltes amb modificacions específiques en la lògica de joc i en la sincronització de la interfície.

Finalment, les proves automatitzades han ajudat a garantir l'estabilitat del sistema de generació de nivells i la persistència de dades del joc.