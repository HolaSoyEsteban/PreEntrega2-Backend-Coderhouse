# Pre Entrega 2 de Backend

## Objetivos generales

En este proyecto, el objetivo principal es desarrollar una aplicación que permita gestionar productos y carritos utilizando MongoDB como sistema de persistencia principal. Para lograr esto, implementaremos todos los endpoints necesarios para realizar operaciones CRUD en productos y carritos.

## Objetivos específicos

- Profesionalizar las consultas de productos con filtros, paginación y ordenamientos.
- Implementar la gestión de carritos con los últimos conceptos aprendidos.

## Entrega del proyecto

Para entregar el proyecto, realizaremos los siguientes cambios:

### Endpoints de productos

Modificaremos el método `GET /api/products` para que cumpla con los siguientes puntos:

- Se podrá recibir por query params un `limit` (opcional), una `page` (opcional), un `sort` (opcional) y un `query` (opcional).
- El `limit` permitirá devolver solo el número de elementos solicitados al momento de la petición, en caso de no recibir `limit`, este será de 10.
- La `page` permitirá devolver la página que queremos buscar, en caso de no recibir `page`, esta será de 1.
- El `query` permitirá filtrar los productos por categoría o por disponibilidad, en caso de no recibir `query`, se realizará una búsqueda general.
- El `sort` permitirá realizar un ordenamiento ascendente o descendente por precio, en caso de no recibir `sort`, no se realizará ningún ordenamiento.

El método `GET /api/products` deberá devolver un objeto con el siguiente formato:

```json
{
  "status": "success/error",
  "payload": "Resultado de los productos solicitados",
  "totalPages": "Total de páginas",
  "prevPage": "Página anterior",
  "nextPage": "Página siguiente",
  "page": "Página actual",
  "hasPrevPage": "Indicador para saber si la página previa existe",
  "hasNextPage": "Indicador para saber si la página siguiente existe.",
  "prevLink": "Link directo a la página previa (null si hasPrevPage=false)",
  "nextLink": "Link directo a la página siguiente (null si hasNextPage=false)"
}
```

### Endpoints de carritos

Agregaremos los siguientes endpoints al router de carritos:

- `DELETE /api/carts/:cid/products/:pid`: Eliminará del carrito el producto seleccionado.
- `PUT /api/carts/:cid`: Actualizará el carrito con un arreglo de productos con el formato especificado.
- `PUT /api/carts/:cid/products/:pid`: Podrá actualizar SOLO la cantidad de ejemplares del producto por cualquier cantidad pasada desde `req.body`.
- `DELETE /api/carts/:cid`: Eliminará todos los productos del carrito.

Además, en el modelo de Carts, la propiedad `products` deberá contener IDs que hagan referencia al modelo de Products. Modificaremos la ruta `/:cid` para que, al traer todos los productos, se realice un "populate" para obtener los productos completos mediante sus IDs.

### Vistas

Crearemos una vista en el router de vistas `/products` para visualizar todos los productos con su respectiva paginación. Cada producto mostrado podrá resolverse de dos formas:

1. Llevar a una nueva vista con el producto seleccionado, mostrando su descripción completa, detalles de precio, categoría, etc. Además de un botón para agregar al carrito.
2. Contar con el botón de "agregar al carrito" directamente, sin necesidad de abrir una página adicional con los detalles del producto.

Además, agregaremos una vista en `/carts/:cid` para visualizar un carrito específico, donde se listarán SOLO los productos que pertenezcan a dicho carrito.

## Sugerencias

- Habilitar comentarios en el archivo para facilitar la comprensión del código.
- Mantener la lógica del negocio existente y enfocarse en la persistencia de datos.
- Los nuevos endpoints deben seguir la misma estructura y lógica que hemos utilizado hasta ahora.