# React tutorial

[tutorial de react](https://es.reactjs.org/tutorial/tutorial.html)

### 1. Configuración
```bash
npx create-react-app react-tutorial  
cd react-tutorial
cd src
rm -f *
cd ..
cat << 'EOF' >> src/index.html
<div id="errors" style="
  background: #c00;
  color: #fff;
  display: none;
  margin: -20px -20px 20px;
  padding: 20px;
  white-space: pre-wrap;
"></div>
<div id="root"></div>
<script>
window.addEventListener('mousedown', function(e) {
  document.body.classList.add('mouse-navigation');
  document.body.classList.remove('kbd-navigation');
});
window.addEventListener('keydown', function(e) {
  if (e.keyCode === 9) {
    document.body.classList.add('kbd-navigation');
    document.body.classList.remove('mouse-navigation');
  }
});
window.addEventListener('click', function(e) {
  if (e.target.tagName === 'A' && e.target.getAttribute('href') === '#') {
    e.preventDefault();
  }
});
window.onerror = function(message, source, line, col, error) {
  var text = error ? error.stack || error : message + ' (at ' + source + ':' + line + ':' + col + ')';
  errors.textContent += text + '\n';
  errors.style.display = '';
};
console.error = (function(old) {
  return function error() {
    errors.textContent += Array.prototype.slice.call(arguments).join(' ') + '\n';
    errors.style.display = '';
    old.apply(this, arguments);
  }
})(console.error);
</script>
EOF
cat << 'EOF' >> src/index.css
body {
  font: 14px "Century Gothic", Futura, sans-serif;
  margin: 20px;
}

ol, ul {
  padding-left: 30px;
}

.board-row:after {
  clear: both;
  content: "";
  display: table;
}

.status {
  margin-bottom: 10px;
}

.square {
  background: #fff;
  border: 1px solid #999;
  float: left;
  font-size: 24px;
  font-weight: bold;
  line-height: 34px;
  height: 34px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 34px;
}

.square:focus {
  outline: none;
}

.kbd-navigation .square:focus {
  background: #ddd;
}

.game {
  display: flex;
  flex-direction: row;
}

.game-info {
  margin-left: 20px;
}
EOF
cat << 'EOF' >> src/index.js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {/* TODO */}
      </button>
    );
  }
}

class Board extends React.Component {
  renderSquare(i) {
    return <Square />;
  }

  render() {
    const status = 'Next player: X';

    return (
      <div>
        <div className="status">{status}</div>
        <div className="board-row">
          {this.renderSquare(0)}
          {this.renderSquare(1)}
          {this.renderSquare(2)}
        </div>
        <div className="board-row">
          {this.renderSquare(3)}
          {this.renderSquare(4)}
          {this.renderSquare(5)}
        </div>
        <div className="board-row">
          {this.renderSquare(6)}
          {this.renderSquare(7)}
          {this.renderSquare(8)}
        </div>
      </div>
    );
  }
}

class Game extends React.Component {
  render() {
    return (
      <div className="game">
        <div className="game-board">
          <Board />
        </div>
        <div className="game-info">
          <div>{/* status */}</div>
          <ol>{/* TODO */}</ol>
        </div>
      </div>
    );
  }
}

// ========================================

ReactDOM.render(
  <Game />,
  document.getElementById('root')
);
EOF
yarn install
yarn start
```