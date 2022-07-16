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
use.Effect(     // Equivalente a componentWillUnmount(). Se ejecuta si hay cambios en el estado dependecia
  () => return {
    () => {}
  }
)
```

## Creando el store

```js

```