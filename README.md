# Notas

Este repositorio contiene varios customHooks para ayudarme a mi y a quien le sirva estos hooks.

También la idea es que yo no quiero volver a escribirlos!

# useCounter

Sirve para hacer un contador. Contiene 3 funciones

useCounter = (initialState = 10) => {
  const [counter, setCounter] = useState(initialState);

1. Para incrementar

```
  const increment = () => {
      setCounter(counter +1);
  }
  ```


2. Para decrementar
```
  const decrement = () => {
      setCounter(counter -1);
  }
  ```

2. Para resetear el valor predeterminado

```
  const reset = () => {
      setCounter(initialState);
  }
  ```

```
  return {
      counter,
      increment,
      decrement,
      reset
  }

  ```


# useFetch

Hook para hacer peticiones ajax y renderizarlo en el componente donde se invocó

Devuelve 3 elementos:
    Data: datos de la petición
    loading: true o false en función si terminó de hacer la petición
    error: mensaje de error si ha ocurrido algún error, null en caso contrario

    (Hay que programarlo dependiendo de lo que quieras que devuelva)

```
useFetch = (url) => {

    const isMounted = useRef(true)

    const [state, setstate] = useState({ data: null, loading: true, error: null });

    useEffect(() => {
        return () => {
            isMounted.current = false;
        }
    }, []);
    useEffect(() => {
        setstate({ data: null, loading: true, error: null });
        fetch(url)
            .then(resp => resp.json())
            .then(data => {
                if (isMounted.current) {

                    setstate({
                        loading: false,
                        error: null,
                        data
                    });
                }

            })
            .catch(() => {
                setstate({
                    data:null,
                    loading: false,
                    error: 'No se pudo cargar la info'
                });
            });
    }, [url]);

    return state;
}
```
# useForm

Hook para formularios. 


```
useForm = (initialState = {}) => {
   
    const [values, setValues] = useState(initialState);

    const reset = () =>{
        setValues(initialState);
    }
    const handleInputChange = ({target}) => {
        setValues({
            ...values,
            [target.name]: target.value
        });
    }

    return [values, handleInputChange, reset];
}
```