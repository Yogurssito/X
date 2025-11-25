




### TIC TAC TOE ( TATETI ) 
Contiene los pasos para crear un bot artificial que juega al tres en raya inteligentemente. Pruébalo:

# Tres en raya con IA (Minimax)

Este proyecto implementa el clásico **Tres en Raya / Ta--Te--Ti**
utilizando HTML, CSS y JavaScript, junto con el algoritmo **Minimax**
para que la computadora juegue de manera óptima.
<img width="485" height="649" alt="Screenshot_1" src="https://github.com/user-attachments/assets/2bb4dc2a-16ca-44f0-a345-2837741b842e" />


## ¿Qué es Minimax?
Minimax es una inteligencia artificial aplicada a juegos de dos jugadores, como el tres en raya, las damas, el ajedrez y el go. Estos juegos se conocen como juegos de suma cero, porque, en una representación matemática: un jugador gana (+1) y el otro pierde (-1) o ninguno gana (0).

## Cómo funciona
El algoritmo busca recursivamente la mejor jugada que lleve al jugador Max a ganar o no perder (empate). Considera el estado actual de la partida y las jugadas disponibles en ese estado, y luego, por cada jugada válida, realiza (alternando min y max ) hasta encontrar un estado terminal (ganar, empatar o perder).
( ejemplo sencillo )
1.  El jugador selecciona una casilla.\
2.  Se actualiza el estado del tablero.\
3.  La IA ejecuta Minimax y devuelve la mejor jugada.\
4.  Se revisa si hay victoria o empate.\
5.  El proceso continúa hasta finalizar la partida.

## Estructura del código

    /project
    │── index.html
    │── style.css
    │── script.js

### index.html

Estructura del tablero, controles y vínculo con los demás archivos.
``` <head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TicTacToe AI</title>

<link rel="stylesheet" href="style.css">
</head>

<body>
<main>
  <h1>TicTacToe</h1>

  <div class="controls">
    <label>Turno: <span id="turnLabel">X</span></label>
    <label>
      Modo:
      <select id="modeSelect">
        <option value="human-vs-ai">Humano vs IA</option>
        <option value="human-vs-human">Humano vs Humano</option>
      </select>
    </label>
    <label>
      Dificultad:
      <select id="difficulty">
        <option value="easy">Fácil</option>
        <option value="hard" selected>Difícil</option>
      </select>
    </label>
    <button id="resetBtn">Reiniciar</button>
  </div>

  <div id="board" class="board"></div>

  <div class="status">
    <p id="statusText">Haz clic en una casilla para jugar.</p>
  </div>

  <footer>
    <p>IA Minimax implementada en JavaScript.</p>
  </footer>
</main>

<script src="script.js"></script>
</body>
```

### style.css

Estilos de la interfaz, colores y diseño del tablero
``` :root{
  --bg:#0f1724;
  --panel:#0b1220;
  --accent:#06b6d4;
  --cell:#0b1626;
  --text:#e6eef6;
}
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Inter,ui-sans-serif,system-ui,-apple-system,'Segoe UI',Roboto,'Helvetica Neue',Arial;
  background:linear-gradient(180deg,var(--bg),#071025);
  color:var(--text);
  min-height:100vh;
  display:flex;
  align-items:center;
  justify-content:center;
}
main{
  width:480px;
  max-width:96%;
  background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));
  padding:20px;
  border-radius:12px;
  box-shadow:0 10px 30px rgba(2,6,23,0.6);
}
h1{margin:0 0 12px 0; font-size:24px; text-align:center; color:var(--accent)}
.controls{
  display:flex;
  gap:8px;
  align-items:center;
  justify-content:space-between;
  margin-bottom:12px;
  flex-wrap:wrap;
}
.controls label{font-size:13px; color:#bcd7df}
.controls select, .controls button{
  padding:6px 8px;
  border-radius:6px;
  border:none;
  background:#0f2531;
  color:var(--text)
}
.board{
  display:grid;
  grid-template-columns:repeat(3,1fr);
  gap:8px;
  margin:14px auto;
}
.cell{
  width:140px;
  height:140px;
  max-width:22vw;
  max-height:22vw;
  background:var(--cell);
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:72px;
  border-radius:10px;
  cursor:pointer;
  user-select:none;
  transition:transform .08s ease, background .12s;
  font-weight:900;
}
.cell:hover{transform:translateY(-4px)}
.status{margin-top:10px; text-align:center; color:#9ecadb}
footer{margin-top:12px; font-size:12px; text-align:center; color:#84b6c6}
@media (max-width:420px){
  .cell{font-size:36px}
}

.cell.x { color: #ff4d4d; }
.cell.o { color: #4da6ff; }
```


### script.js

Contiene: - Lógica del juego\
- Turnos\
- Detección de ganador\
- Implementación completa de Minimax\
- IA perfecta\
- Reinicio del tablero

## Entendiendo el algoritmo Minimax

Minimax evalúa todas las jugadas posibles y devuelve la mejor opción
posible para la IA.

### Concepto general:

-   **MAX**: la IA (O), intenta obtener el puntaje más alto\
-   **MIN**: el jugador (X), intenta minimizarlo\
-   La función recorre todo el árbol de posibilidades y evalúa los
    resultados.

### Ejemplo del código:

``` javascript
function minimax(brd, depth, isMax, player) {
  const opponent = player === 'X' ? 'O' : 'X';
  const winner = computeWinner(brd);

  if (winner === player) return 10 - depth;
  if (winner === opponent) return depth - 10;
  if (brd.every(Boolean)) return 0;

  const avail = brd.map((v,i)=>v?null:i).filter(v=>v!==null);

  if (isMax) {
    let best = -Infinity;
    for (const i of avail) {
      brd[i] = player;
      const score = minimax(brd, depth+1, false, player);
      brd[i] = null;
      best = Math.max(best, score);
    }
    return best;
```

## Arbol 
El juego utiliza un árbol de decisiones donde cada nodo representa un tablero posible y cada rama una jugada. El árbol completo del tres en raya tiene alrededor de **255.168 nodos**, aunque el código genera solo los necesarios para cada turno mediante Minimax.
El nodo raíz es el tablero vacío; sus hijos representan cada jugada posible.
El árbol sigue creciendo mientras haya casilleros libres.
Los nodos hoja aparecen cuando hay victoria o empate.
Minimax recorre el árbol probando todas las jugadas, las evalúa y selecciona la mejor opción para la IA.
ejemplo de como seria:
<img width="794" height="591" alt="tic-tac-toe-minimax-game-tree (1)" src="https://github.com/user-attachments/assets/53b62317-9d60-4fbe-b5e0-532421ebde4b" />

## Tres en raya con Refuerzo
Aunque el proyecto utiliza el algoritmo **Minimax** para tomar decisiones perfectas, el juego también puede resolverse mediante **Aprendizaje por Refuerzo (RL)**. En este enfoque, la IA no analiza todas las jugadas posibles desde el principio, sino que **aprende a jugar** a través de experiencia acumulada, partidas repetidas y retroalimentación por recompensas.

### Como funcionaría en mi codigo

El agente (la IA)

* observa el estado actual del tablero,
* elige una acción (una jugada),
* recibe una recompensa según el resultado,
* y ajusta su política para mejorar futuras decisiones.

### Recompensas comunes
* **+1** por ganar
* **0** por empatar
* **–1** por perder

Con suficiente entrenamiento, la IA aprende patrones óptimos sin necesidad de buscar todo el árbol completo como hace Minimax.

### Diferencias con mi codigo 

mi codigo:

* usa **Minimax**, que analiza todas las jugadas posibles;
* siempre toma la decisión óptima;
* no necesita entrenamiento.

El enfoque por refuerzo:

* no garantiza perfección al comienzo;
* puede mejorar con muchas partidas;
* suele usarse cuando el espacio de estados es muy grande (no es el caso de Tic Tac Toe, por eso Minimax es más eficiente).

## Ejecución

Solo abrir el archivo:

    index.html oh sino tambien este enlace https://yogurssito.github.io/X/

No requiere instalaciones de programas externos 
