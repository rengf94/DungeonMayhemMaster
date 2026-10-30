# 🎲 Dungeon Mayhem - Ayudante de Juego (PWA)

Aplicación web progresiva (PWA) para jugar **Dungeon Mayhem** con tus cartas físicas.  
La app se encarga de todo lo que es "azar y seguimiento": robar salas, encuentros, jefes, tirar el D6, llevar los HP (D10) y el registro de turnos. Tú usas tus cartas de jugador físicas sobre la mesa.

## 📁 Estructura del proyecto

```
DungeonMaster/
├── index.html          # Pantalla principal
├── style.css           # Estilos
├── app.js              # Lógica del juego
├── cards.json          # Catálogo de cartas (mapeo imagen → datos)
├── manifest.json       # Manifiesto PWA
├── sw.js               # Service Worker (offline)
├── make-icons.html     # Generador de iconos PIN (ábralo en el navegador)
├── README.md           # Este archivo
└── Cards/              # Tus imágenes de cartas físicas (ya las tenés)
    ├── Encounter (1).png … (20).png
    ├── Dungeon (1).png … (22).png
    └── Boss (1).png … (3).png
```

## 🚀 Cómo usarlo

1. Abrí `index.html` en cualquier navegador moderno (Chrome, Edge, Firefox).
2. Seleccioná la cantidad de jugadores y el personaje de cada uno.
3. Hacé clic en **Iniciar Aventura**.
4. En cada turno:
   - **Robar Carta**: anotá que robás 1 carta de tu baraja física.
   - **Robar Sala**: la app elige una carta de mazmorra al azar de tu carpeta `Cards/`.
   - **D6**: tira el dado para acciones enemigas / del jefe.
   - **Resolver**: cuando vencés un monstruo o trampa, la app la devuelve al mazo.
   - **Siguiente Turno**: pasa al siguiente jugador.
5. Los HP se manejan con el dial circular de cada jugador (toque para editar si querés ajustar manualmente — *próxima versión*).

## 📲 Instalar como APP en la PC (PWA → .exe)

### Opción A: Chrome / Edge (más fácil)
1. Abrí `index.html` en Chrome o Edge.
2. En la barra de direcciones aparecrá un ícono de **instalar** (computadora con flecha) o ir al menú ⋮ > **Instalar "Dungeon Mayhem"**.
3. Se crea un acceso directo en el escritorio y menú de inicio que se abre como ventana independiente (sin barra de direcciones), igual a un `.exe`.

### Opción: PWABuilder (generar .exe real)
1. Iden a [pwabuilder.com](https://www.pwabuilder.com).
2. Ingresá la URL de tu `index.html` (o subí la carpeta).
3. Seleccioná **Windows** → generá el paquete `.msix` o `.exe`.
4. Instalalo en tu PC.

> Nota: por ahora los iconos PNG no están generados. Abrí `make-icons.html` en el navegador, haga clic en **Descargar todos los PNG** y copie los archivos `icon-*.png` a la raíz del proyecto para que la instalación PWA se vea completa.

## 🃏 ¿Qué hace la app por vos?

| Componente | ¿Quién lo maneja? |
|------------|-------------------|
| Player Deck (cartas de personaje) | **Tú** (cartas físicas en la mesa) |
| HP inicial 10 | App (dial por jugador) |
| Robar 3 cartas al inicio | App (registro) + tú (físicas) |
| Robar 1 carta por turno | App (botón "Robar Carta") |
| Dungeon Deck (salas) | App (roba aleatoriamente de `Cards/Dungeon`) |
| Encounter Deck (monstruos/trampas) | App (roba de `Cards/Encounter`) |
| Boss Deck | App (elige al azar de `Cards/Boss`) |
| D6 (acción enemiga) | App (botón D6) |
| D10 (HP) | App (dial visual por jugador) |
| Primera instancia / First Strike | App (lo indica en la carta de encuentro) |
| Trampa vuelve al mazo | App (automático al resolver) |

## 🛠 Reglas asumidas (estándar)

- Los monstruos tienen **1 HP por jugador**. Cuando los derrotás con tus cartas físicas, volvés a tirar la carta al mazo de encuentro.
- Las trampas dan daño **una vez** y vuelven al mazo de encuentro.
- El jefe tiene **10 HP por jugador**.
- Si una sala sellaría todos los caminos antes del boss, descartala y robá otra (la app te deja aceptar o descartar la sala dibujada).
- Cada jugador usa su propia baraja física; la app solo lleva la cuenta de cuántas cartas tenés en mano.

## 💾 Guardar / Cargar partida

Desde el menú (☰) podés **Exportar Estado** (guarda un JSON) e **Importar Estado** para continuar una partida otra vez.

---

¿Necesitás que agregue algo? Por ejemplo: editor manual de HP, sonido de dados, o exportar a PDF. ¡Avísame!