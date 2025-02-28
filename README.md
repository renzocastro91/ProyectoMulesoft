Especificación de la API (Desing Center)
openapi: 3.0.0
info:
  title: Persona API
  description: API para gestionar información de personas y consumir datos externos.
  version: 1.0.3
servers:
  - url: http://localhost:8081/api

paths:
  /persona:
    post:
      summary: Crear una nueva persona
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: "#/components/schemas/Persona"
      responses:
        "201":
          description: Persona creada exitosamente
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Persona"

  /persona/{username}:
    get:
      summary: Obtener información de una persona por username
      parameters:
        - name: username
          in: path
          required: true
          schema:
            type: string
            pattern: "^[a-zA-Z0-9_]+$"
      responses:
        "200":
          description: Persona encontrada
          content:
            application/json:
              schema:
                $ref: "#/components/schemas/Persona"
    patch:
      summary: Actualizar datos de un cliente
      parameters:
        - name: username
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                id:
                  type: integer
                  format: int64
                email:
                  type: string
                  format: string
                phone:
                  type: string
                gender:
                  type: string
                country:
                  type: string
                city:
                  type: string
                latitude:
                  type: number
                longitude:
                  type: number
                uuid:
                  type: string
                username:
                  type: string
                password:
                  type: string
                first:
                  type: string
                last:
                  type: string
      responses:
        "200":
          description: Cliente actualizado correctamente
          content:
            application/json:
              schema:
                type: object
                properties:
                  message:
                    type: string
                  updatedClient:
                    type: object
                    $ref: "#/components/schemas/Client"
        "400":
          description: Error en la solicitud
        "404":
          description: Cliente no encontrado

  /persona/external:
    get:
      summary: Obtener 5 registros filtrados desde una API externa
      responses:
        "200":
          description: Datos obtenidos exitosamente
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    name:
                      type: string
                    email:
                      type: string
                      format: email
                    city:
                      type: string
                    company:
                      type: string

components:
  schemas:
    Persona:
      type: object
      properties:
        username:
          type: string
        firstName:
          type: string
        lastName:
          type: string
        email:
          type: string
          format: email
        phone:
          type: string
          nullable: true
        city:
          type: string
        country:
          type: string
        company:
          type: string
    Client:
      type: object
      properties:
        id:
          type: integer
          format: int64
        email:
          type: string
          format: email
        phone:
          type: string
        gender:
          type: string
        country:
          type: string
        city:
          type: string
        latitude:
          type: number
        longitude:
          type: number
        uuid:
          type: string
        username:
          type: string
        password:
          type: string
        first:
          type: string
        last:
          type: string
