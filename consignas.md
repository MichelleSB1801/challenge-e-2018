### CASO 1

 Dada las siguientes funciones

  ```javascript
    var Foo = function( a ) {
      var baz = function() {
        return a;
      };
      this.baz = function() {
        return a;
      };
    };

    Foo.prototype = {
      biz: function() {
        return a;
      }
    };

    var f = new Foo( 7 );
    f.bar(); 
    f.baz(); 
    f.biz(); 
  ```

 1. ¿Cuál es el resultado de las últimas 3 líneas?
      	 
	`f.bar() no resuelve nada, se rompe porque la función no esta definida. `
	`f.baz() resuelve la función.`
	`f.biz() indica que A no esta definido.`
	
 2. Modificá el código de `f.bar()` para que retorne `7`?

 3. Modificá el código para que `f.biz()` también retorne `7`?
    
    ```javascript
    Foo.prototype = {
    	biz: function() {
		    return this.a;
	    },
	    bar: function() {
		    return this.a;
	    }
    };
```	


### CASO 2

Partiendo del siguiente array:

```javascript
var endorsements = [
  { skill: 'css', user: 'Bill' },
  { skill: 'javascript', user: 'Chad' },
  { skill: 'javascript', user: 'Bill' },
  { skill: 'css', user: 'Sue' },
  { skill: 'javascript', user: 'Sue' },
  { skill: 'html', user: 'Sue' }
];
```

¿Cómo podrías ordenarlo de la siguiente forma?:

```javascript
[
  { skill: 'css', users: [ 'Bill', 'Sue', 'Sue' ], count: 2 },
  { skill: 'javascript', users: [ 'Chad', 'Bill', 'Sue' ], count: 3 },
  { skill: 'html', users: [ 'Sue' ], count: 1 }
]
```

```javascript
function Reorden () {	
	var result = endorsements.reduce((newArray,object)=>{
		var hola = newArray.find((element) => {
			return element.skill == object.skill
		})
		if (hola != undefined) {
			hola.user.push(object.user)
			hola.count ++
		}else{
			newArray.push(
				{
					skill: object.skill,
					user: [object.user],
					count: 1,
				},
			);
		}	
    return newArray
  },[]);
  console.log(result)
}

Reorden()
```


### CASO 3

Tengo las siguientes funciones:

```javascript
function buscarEnFacebook(texto, callback) {
  /* Hace algunas cosas y las guarda en "result" */
  if (result.error) {
    callback(error, result.error)
  } else {
    callback(null, result.data);
  }
}
function buscarEnGithub(texto, callback) {
  /* Hace algunas cosas y las guarda en "result" */
  if (result.error) {
    callback(error, result.error)
  } else {
    callback(null, result.data);
  }
}
```

  - ¿Qué debería hacer para usar la funcionalidad con promesas y no callbacks?
```javascript
facebook () {
  async function buscarEnFacebook() {
    try {		
      let result = await  /* Hace algunas cosas y las guarda en "result" */
      return result.data
    } catch(err) {
      return result.error
    }
  }
}

Github () {
  async function buscarEnGithub() {
    try {		
      let result = await    /* Hace algunas cosas y las guarda en "result" */
      return result.data
    } catch(err) {
      return result.error
    }
  }
}
```
  - ¿Podés replicar la siguiente API?
    
    ```javascript
    buscador('hola')
    .facebook()
    .github()
    .then((data) => {
      // data[0] = data de Facebook
      // data[1] = data de GitHub
    })
    .catch(error => {
      // error[0] = error de Facebook
      // error[1] de GitHub
    })
    ```
    
    
    
    ```javascript
        class Buscador {
	constructor (texto) {
	  this.texto = texto
		this.promises = []
		this.errors = []
	}
  
	facebook () {
		async function buscarEnFacebook() {
			/* Hace algunas cosas y las guarda en "result" */
				return result.data
		}
	  this.promises.push(buscarEnFacebook(this.texto))
	  return this
	}

	Github () {
		async function buscarEnGithub() {
			/* Hace algunas cosas y las guarda en "result" */		
				return result.data
		}
	  this.promises.push(buscarEnGithub(this.texto))
	  return this
	}
  
	then (cb) {
	  return Promise
		.all(this.promises)
		.then(cb)
	}
	}
    
    ```
  - y a la solución anterior
    - ¿Cómo podrías agregarle otra búsqueda?
       ` Se agrega el llamado a la api correspondiente pusheando el resultado al array de promises para que luego pueda ser recibido por la Api `
    - ¿Cómo solucionas el problema de si una API entrega un error, mientras las otras devuelven data?
        `Realizando los llamados a las apis de las aplicaciones en funciones diferentes.`







