# React Calculator App

Create a file called `Calculator.js`:

```jsx
import React, { useState } from "react";

const Calculator = () => {
  const [displayValue, setDisplayValue] = useState("0");
  const [firstOperand, setFirstOperand] = useState(null);
  const [operator, setOperator] = useState(null);
  const [waitingForSecondOperand, setWaitingForSecondOperand] = useState(false);

  const inputDigit = (digit) => {
    if (waitingForSecondOperand) {
      setDisplayValue(digit);
      setWaitingForSecondOperand(false);
    } else {
      setDisplayValue(displayValue === "0" ? digit : displayValue + digit);
    }
  };

  const inputDecimal = () => {
    if (!displayValue.includes(".")) {
      setDisplayValue(displayValue + ".");
    }
  };

  const clearDisplay = () => {
    setDisplayValue("0");
    setFirstOperand(null);
    setOperator(null);
    setWaitingForSecondOperand(false);
  };

  const performOperation = (nextOperator) => {
    const inputValue = parseFloat(displayValue);

    if (firstOperand === null) {
      setFirstOperand(inputValue);
    } else if (operator) {
      const result = calculate();
      setDisplayValue(String(result));
      setFirstOperand(result);
    }

    setWaitingForSecondOperand(true);
    setOperator(nextOperator);
  };

  const calculate = () => {
    const inputValue = parseFloat(displayValue);

    if (operator === "+") {
      return firstOperand + inputValue;
    } else if (operator === "-") {
      return firstOperand - inputValue;
    } else if (operator === "*") {
      return firstOperand * inputValue;
    } else if (operator === "/") {
      return firstOperand / inputValue;
    }

    return inputValue;
  };

  return (
    <div className="calculator">
      <div className="display">{displayValue}</div>
      <div className="keypad">
        <button onClick={clearDisplay}>AC</button>
        <button onClick={() => inputDigit("7")}>7</button>
        <button onClick={() => inputDigit("8")}>8</button>
        <button onClick={() => inputDigit("9")}>9</button>
        <button onClick={() => performOperation("/")}>÷</button>
        <button onClick={() => inputDigit("4")}>4</button>
        <button onClick={() => inputDigit("5")}>5</button>
        <button onClick={() => inputDigit("6")}>6</button>
        <button onClick={() => performOperation("*")}>×</button>
        <button onClick={() => inputDigit("1")}>1</button>
        <button onClick={() => inputDigit("2")}>2</button>
        <button onClick={() => inputDigit("3")}>3</button>
        <button onClick={() => performOperation("-")}>-</button>
        <button onClick={() => inputDigit("0")}>0</button>
        <button onClick={inputDecimal}>.</button>
        <button onClick={() => performOperation("+")}>+</button>
        <button onClick={() => performOperation("=")}>=</button>
      </div>
    </div>
  );
};

export default Calculator;
```
