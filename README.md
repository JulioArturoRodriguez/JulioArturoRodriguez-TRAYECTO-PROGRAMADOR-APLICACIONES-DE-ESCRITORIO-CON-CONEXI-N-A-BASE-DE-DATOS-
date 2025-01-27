openapi: 3.0.0
info:
  title: Gestión Comercial
  description: |
    **Gestión Comercial** es una aplicación de escritorio desarrollada en Java (última versión) utilizando programación orientada a objetos.
    Esta aplicación permite gestionar diferentes aspectos comerciales, como:
    - Registro de asistencia
    - Manejo de inventario y stock
    - Gestión de ventas
    - Administración de usuarios y permisos
    - Control de entradas y salidas de ventas del día
    - Gestión de quejas y recomendaciones

    **Tecnologías utilizadas**:
    - Base de datos: MySQL (gestionada con Workbench).
    - Desarrollo de interfaz gráfica: Modelado de software.
    - Entorno de desarrollo: Apache NetBeans.
  version: 1.0.0
servers:
  - url: http://localhost:8080/api
    description: Servidor local para las APIs de Gestión Comercial
paths:
  /productos:
    get:
      summary: Obtener todos los productos
      description: Devuelve una lista de todos los productos en el inventario.
      responses:
        '200':
          description: Lista de productos obtenida exitosamente.
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    idProducto:
                      type: integer
                      description: ID del producto.
                    nombre:
                      type: string
                      description: Nombre del producto.
                    cantidad:
                      type: integer
                      description: Cantidad disponible en stock.
                    precio:
                      type: number
                      format: float
                      description: Precio del producto.
    post:
      summary: Crear un nuevo producto
      description: Registra un nuevo producto en el inventario.
      requestBody:
        description: Detalles del nuevo producto.
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                nombre:
                  type: string
                  description: Nombre del producto.
                cantidad:
                  type: integer
                  description: Cantidad inicial del producto en stock.
                precio:
                  type: number
                  format: float
                  description: Precio del producto.
      responses:
        '201':
          description: Producto creado exitosamente.
          content:
            application/json:
              schema:
                type: object
                properties:
                  idProducto:
                    type: integer
                    description: ID del nuevo producto.
                  nombre:
                    type: string
                    description: Nombre del producto.
                  cantidad:
                    type: integer
                    description: Cantidad inicial del producto.
                  precio:
                    type: number
                    format: float
                    description: Precio del producto.
  /productos/{id}:
    get:
      summary: Obtener un producto específico
      description: Devuelve los detalles de un producto específico por su ID.
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: integer
          description: ID del producto.
      responses:
        '200':
          description: Producto encontrado exitosamente.
          content:
            application/json:
              schema:
                type: object
                properties:
                  idProducto:
                    type: integer
                    description: ID del producto.
                  nombre:
                    type: string
                    description: Nombre del producto.
                  cantidad:
                    type: integer
                    description: Cantidad disponible en stock.
                  precio:
                    type: number
                    format: float
                    description: Precio del producto.
        '404':
          description: Producto no encontrado.
    put:
      summary: Actualizar un producto
      description: Actualiza los detalles de un producto existente.
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: integer
          description: ID del producto a actualizar.
      requestBody:
        description: Detalles actualizados del producto.
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                nombre:
                  type: string
                  description: Nombre del producto.
                cantidad:
                  type: integer
                  description: Cantidad del producto en stock.
                precio:
                  type: number
                  format: float
                  description: Precio del producto.
      responses:
        '200':
          description: Producto actualizado exitosamente.
          content:
            application/json:
              schema:
                type: object
                properties:
                  idProducto:
                    type: integer
                    description: ID del producto.
                  nombre:
                    type: string
                    description: Nombre del producto.
                  cantidad:
                    type: integer
                    description: Cantidad del producto.
                  precio:
                    type: number
                    format: float
                    description: Precio del producto.
        '404':
          description: Producto no encontrado.
    delete:
      summary: Eliminar un producto
      description: Elimina un producto del inventario por su ID.
      parameters:
        - in: path
          name: id
          required: true
          schema:
            type: integer
          description: ID del producto a eliminar.
      responses:
        '204':
          description: Producto eliminado exitosamente.
        '404':
          description: Producto no encontrado.
