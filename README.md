<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Calculadora Científica</title>
  <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
  <style>
    body {
  font-family: Arial, sans-serif;
  background-color: #5a67d8;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 40px;
  height: 100vh;
  margin: 0;
}

.container {
  background-color: white;
  padding: 24px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.2);
  width: 100%;
  max-width: 460px;
}

h2 {
  margin-bottom: 20px;
  font-size: 24px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 12px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
  font-size: 16px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 10px;
}

.button {
  background-color: #007bff;
  color: white;
  padding: 14px 0;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 18px;
  flex: 1 1 22%;
  text-align: center;
  transition: background-color 0.2s ease;
}

.button:hover {
  background-color: #0056b3;
}

.result {
  margin-top: 20px;
  font-weight: bold;
  font-size: 18px;
}

  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    const { useState } = React;
    

    function ScientificCalculator({ title = "Calculadora Científica" }) {
      const [value1, setValue1] = useState('');
      const [value2, setValue2] = useState('');
      const [result, setResult] = useState('');

      const parse = (val) => parseFloat(val) || 0;

      const calculate = (operation) => {
        const a = parse(value1);
        const b = parse(value2);
        let res = '';

        switch (operation) {
          case '+': res = a + b; break;
          case '-': res = a - b; break;
          case '*': res = a * b; break;
          case '/': res = b !== 0 ? a / b : 'Error: ÷0'; break;
          case 'sin': res = Math.sin(a * Math.PI / 180);break
          case 'cos': res = Math.cos(a * Math.PI /180); break;
          case 'tan': res = Math.tan(a * Math.PI /180); break;
          case '√': res = Math.sqrt(a); break;
          case 'pow': res = Math.pow(a, b); break;
          case 'clear':
            setValue1('');
            setValue2('');
            res = '';
            break;
          default: res = 'Operación no válida';
        }

        setResult(res.toString());
      };

      return (
        <div className="container">
          <h2>{title}</h2>
          <input type="number" placeholder="Valor 1" value={value1} onChange={(e) => setValue1(e.target.value)} />
          <input type="number" placeholder="Valor 2 (opcional)" value={value2} onChange={(e) => setValue2(e.target.value)} />
          
          <div className="row">
            {['+', '-', '*', '/'].map(op => (
              <div key={op} className="button" onClick={() => calculate(op)}>{op}</div>
            ))}
          </div>

          <div className="row">
            {['sin', 'cos', 'tan', '√'].map(op => (
              <div key={op} className="button" onClick={() => calculate(op)}>{op}</div>
            ))}
          </div>

          <div className="row">
            <div className="button" onClick={() => calculate('pow')}>^</div>
            <div className="button" onClick={() => calculate('clear')}>C</div>
          </div>

          <div className="result">Resultado: {result || 'Ingresa ambos valores'}</div>
        </div>
      );
    }

    ReactDOM.createRoot(document.getElementById('root')).render(<ScientificCalculator />);
  </script>
</body>
</html>
