# COSMIC KEEPER  
## Disseny de Sistema i Abast del Projecte

**Autor:** Izan de Maya

---

## 1. Components principals del joc

El joc no és només el que es veu, per sota hi ha vàries peces funcionant:

- **El dibuix (Canvas):** Fa servir `HTML5` per a que tot es mogui fluid a **60 fotos per segon**.
- **Les físiques:** Un codi que calcula la gravetat, els xocs contra les parets i com rebota el personatge.
- **Guardat de dades:** Faig servir el `localStorage` del navegador per a que, si tanques la pestanya, no perdis els nivells que ja has passat.
- **La cara del joc (UI):** Tota la part dels menús i les barres de vida feta amb `Tailwind CSS`.

---

## 2. Entitats identificades

Aquestes són les "coses" que existeixen dins del meu joc:

- **Jugador:** L'astronauta que controles tu.
- **Enemics:** Els dolents (n'hi ha que et persegueixen, altres que patrullen i torretes).
- **Projectils:** Les bales que et tiren les torretes.
- **Recollibles:** Els nodes per passar de nivell i els *power-ups* de velocitat o escut.
- **Portal:** La meta final de cada pantalla.
- **Entitat Base:** Una plantilla que faig servir per a que tots els personatges s'assemblin en com es mouen.

---

## 3. Atributs clau de cada entitat

Cada cosa té les seves pròpies dades:

### Jugador
- Energia per volar
- Velocitat
- Si porta l'escut activat
- Quina millora té ara mateix

### Enemics
- Quin tipus de dolent és
- Fins on veu
- La seva posició inicial

### Nivells
- En quin número de mapa estàs
- Quants nodes falten
- El color del bioma

### Entitat
- Posició `x`
- Posició `y`
- Amplada
- Alçada

---

## 4. Accions, mètodes o funcions principals

Què fa cada part del codi?

### `update()`
Calcula on s'ha de moure cada cosa abans de dibuixar-la.

### `draw()`
Pinta els personatges i el mapa a la pantalla.

### `checkCollision()`
Mira si t'has xocat amb una paret o si un enemic t'ha tocat.

### `generateLevel()`
Munta el mapa de forma aleatòria cada vegada que canvies de sector.

---

## 5. Explicació del diagrama de classes

Aquest esquema és com el mapa de les peces del joc:

- He posat el **MotorJoc** al mig perquè és qui mana sobre la resta.
- He fet servir la **herència**: el jugador i els enemics "neixen" de la mateixa base (`Entitat`) per no haver de repetir codi de físiques.
- S'entén que el **GestorNivells** és qui crea els objectes que vas trobant pel camí.

---

## 6. Explicació del diagrama de comportament

Aquí es veu què passa cada vegada que el joc fa un "tic":

- El motor mira quines tecles toques
- Mou l'astronauta
- Mira si has tocat algun node o enemic

Si agafes tots els nodes, el flux canvia i s'obre el portal de sortida.

Al final de tot:
- es guarda el temps que has trigat
- es dibuixa la pantalla nova

---

## 7. Correspondència entre diagrames i codi futur

He fet que el disseny i el codi de l'`index.html` vagin de la mà:

- Les funcions del codi es diuen igual que les del diagrama (`update`, `draw`)
- Els objectes que he creat en JavaScript tenen les mateixes propietats (`energy`, `speed`) que vaig planejar al model

---

## 8. Estructura inicial del repositori

Ho tinc tot endreçat per a que no sigui un embolic:

- **`index.html`** → té tot el joc que es pot jugar
- **`/docs`** → fitxers d'explicació i documentació
- **`/assets`** → imatges dels diagrames

---

## 9. Primer commit i README inicial

Per començar el projecte vaig fer:

### Primer commit
Vaig pujar:
- el motor bàsic
- el personatge que vola
- les col·lisions que funcionen bé

### README
Una presentació on explico:
- que el joc va d'un astronauta
- com es controla amb el teclat
- quines eines he fet servir (`Canvas` i `Tailwind`)