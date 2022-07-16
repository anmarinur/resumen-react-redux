# Resumen React Redux

## React routing

### Importaciones
```js
import { BrowserRouter } from 'react-router-dom';
```

```js
import { Route } from 'react-router-dom';
```

```js
import { Link } from 'react-router-dom';
```

### Usualmente en el index

```js
<BrowserRouter>
  ... // El componente principal
</BrowserRouter>
```

### Creación del link

```js
<Link to='/'>Home</Link>    // Link a home
<Link to='/about'>About</Link>    // Link a /about
<Link to='/user/:id'>User</Link>    // Link a una ruta dinámica
```

### Creación de rutas

```js
return {
  <Nav />   // Se renderiza siempre
  <Route exact path={'/'} component={Home}/>    // Se renderiza en el home (no tiene parámetros)
  <Route path={'/about'} render={
      () => <About name={'Anderson'}>   // Tiene parámetros
    }/>
  <Route>
    <User id={id}/>
  </Route>
}
```

## Creando estados locales

### Componente clase

```js
class Home extends React.component {

  constructor(props){
    super(props);
    this.state = {
      state = []
    }

    // Solo se puede modificar el estado con this.setState y se modifica todo el estado

  }

}
```

### Componente funcional (Hook)

```js
function Home(props) {
  const [state, setState] = React.useState([]);   // Permite modificar individualmente los keys de un estado con setState
}
```

## Ciclos de vida de un componente

### Componente de clase

```js
componentDidMount()
componentDidUpdate()
componentWillUnmount();
```

### Componente funcional (Hooks)

```js
use.Effect(     // Equivalente a componentDidMount()
  () => {}, []
)

use.Effect(     // Equivalente a componentDidUpdate(). Se ejecuta si hay cambios en el estado dependecia
  () => {}, [dependencia]
)
```

```js
use.Effect(     // Equivalente a componentWillUnmount(). Se ejecuta el return cuando se desmonte el componente
  () => return {
    () => {}
  }
)
```

## Creando el store

### Método 1

```js
import { createStore, applyMiddleware, compose } from "redux";
import Reducer from "./rutaDelReducer.js";
import thunk from "redux-thunk";

const composeEnhacer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;  // Para conectarme a la herramienta del navegador (extensión Chrome)

const store = createStore(
  rootReducer,
  composeEnhacer(applyMiddleware(thunk)),
);

export default store;
```

```js
import { createStore, applyMiddleware, compose } from "redux";
import Reducer from "./rutaDelReducer.js";
import thunk from "redux-thunk";

const composeEnhacer = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;  // Para conectarme a la herramienta del navegador (extensión Chrome)

const store = createStore(
    Reducer,
    compose(
        applyMiddleware(thunk), //Necesario para hacer acciones asincrónicas
        window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
    )
)

export default store;
```

## Conectando componentes al estado global

Con esto los estados y las funciontes pasan como parámetros al componente. Si es de clase this.props y si es funcional props o por destruture (no estoy seguro como se escribe)

## Componente de clase

### Método 1
```js
import { connect } from 'react-redux'

const mapStateToProps = (state) => {
  return {
    nombreCualquira: state.name
  }
}

export default connect(mapStateToProps, { functionCreator })(NombreDelComponente);  
```

### Método 2

```js
import { connect } from 'react-redux'

const mapStateToProps = (state) => {
  return {
    nombreCualquira: state.name
  }
}

const mapDispatchToProps(dispatch) {
  return {
    funcionX: paramX => dispatch(funcionCreadora(paramX)),
    funcionY: paramY => dispatch(funcionCreadora(paramY))
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(NombreDelComponente);  
```

## Componentes funcionales (Hooks)

```js
import { useDispatch, useSelector} from 'react-redux'

const dispatch = useDispatch();
const nombreCualquiera = useSelector(state => state.name);

...

Para usar el dispatch simplemente se invoca con la función creadora

```js
<div onClick={
  () => dispatch(funcionCreadora(name))
}>Botón</div>
```

```