# Notas

Este repositorio contiene varios customHooks para ayudarme a mi y a quien le sirva estos hooks.

También la idea es que yo no quiero volver a escribirlos!

# useCounter

Sirve para hacer un contador. Contiene 3 funciones

useCounter = (initialState = 10) => {
  const [counter, setCounter] = useState(initialState);

1. Para incrementar
  const increment = () => {
      setCounter(counter +1);
  }


2. Para decrementar
  const decrement = () => {
      setCounter(counter -1);
  }

2. Para resetear el valor predeterminado
  const reset = () => {
      setCounter(initialState);
  }


  return {
      counter,
      increment,
      decrement,
      reset
  }