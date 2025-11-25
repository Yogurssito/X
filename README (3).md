# Tres en raya con IA (Minimax)

Este proyecto implementa el clásico **Tres en Raya / Ta--Te--Ti**
utilizando HTML, CSS y JavaScript, junto con el algoritmo **Minimax**
para que la computadora juegue de manera óptima.

## 📁 Estructura del código

    /project
    │── index.html
    │── style.css
    │── script.js

### index.html

Estructura del tablero, controles y vínculo con los demás archivos.

### style.css

Estilos de la interfaz, colores y diseño del tablero.

### script.js

Contiene: - Lógica del juego\
- Turnos\
- Detección de ganador\
- Implementación completa de Minimax\
- IA perfecta\
- Reinicio del tablero

## 🧠 Entendiendo el algoritmo Minimax

Minimax evalúa todas las jugadas posibles y devuelve la mejor opción
posible para la IA.

### Concepto general:

-   **MAX**: la IA (O), intenta obtener el puntaje más alto\
-   **MIN**: el jugador (X), intenta minimizarlo\
-   La función recorre todo el árbol de posibilidades y evalúa los
    resultados.

### Ejemplo del código:

``` javascript
function minimax(board, player) {
    let available = availableMoves(board);

    if (checkWinner(board) === "X") return { score: -10 };
    if (checkWinner(board) === "O") return { score: 10 };
    if (available.length === 0) return { score: 0 };

    let moves = [];
    for (let spot of available) {
        let move = { index: spot };
        board[spot] = player;

        move.score = player === "O"
            ? minimax(board, "X").score
            : minimax(board, "O").score;

        board[spot] = "";
        moves.push(move);
    }

    return player === "O"
        ? moves.reduce((a, b) => a.score > b.score ? a : b)
        : moves.reduce((a, b) => a.score < b.score ? a : b);
}
```

## 🎮 Funcionamiento del juego

1.  El jugador selecciona una casilla.\
2.  Se actualiza el estado del tablero.\
3.  La IA ejecuta Minimax y devuelve la mejor jugada.\
4.  Se revisa si hay victoria o empate.\
5.  El proceso continúa hasta finalizar la partida.

## 🚀 Ejecución

Solo abrir:

    index.html

No requiere servidor ni instalaciones adicionales.

## 📌 Estructura final sugerida

    /tictactoe-ai
    │── index.html
    │── style.css
    │── script.js
    │── README.md
