# Esquemas reutilizables

### 🎯 Enfoque progresivo: De campos simples a Schemas reutilizables

**Es importante entender que OpenAPI permite dos enfoques para definir datos:**

#### **Enfoque 1: Definición directa (para empezar)**

```yaml
paths:
  /products:
    post:
      # ... elementos anteriores ...
      requestBody:
        required: true                  # Es obligatorio enviar datos
        content:
          application/json:             # Formato de los datos
            schema:                     # Schema definido DIRECTAMENTE aquí
              type: object
              required:
                - name
                - price
                - category
              properties:
                name:
                  type: string
                  minLength: 1
                  maxLength: 200
                  example: "Laptop Gaming"
                description:
                  type: string
                  maxLength: 1000
                  example: "Laptop de alto rendimiento para gaming"
                price:
                  type: number
                  format: decimal
                  minimum: 0
                  example: 1299.99
                category:
                  type: string
                  enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
                  example: "Electronics"
```

#### **Enfoque 2: Referencia a Schema reutilizable (recomendado)**

```yaml
paths:
  /products:
    post:
      # ... elementos anteriores ...
      requestBody:
        required: true                  # Es obligatorio enviar datos
        content:
          application/json:             # Formato de los datos
            schema:
              $ref: '#/components/schemas/Product'  # Referencia al esquema
```

### 🔄 **¿Cuándo usar cada enfoque?**

#### **Usa definición directa cuando:**

- ✅ Estés aprendiendo OpenAPI
- ✅ Tengas campos únicos que no se repiten
- ✅ Prototipes rápidamente

#### **Usa referencias ($ref) cuando:**

- ✅ Los mismos campos se usan en múltiples operaciones
- ✅ Quieras mantener el código organizado
- ✅ Desarrolles APIs en producción

### 📚 **Ejemplo práctico: Evolución de campos**

Imagina que empiezas con esto:

```yaml
# ❌ PROBLEMA: Repetición en múltiples lugares
paths:
  /products:
    post:
      requestBody:
        content:
          application/json:
            schema:
              type: object
              properties:
                name:
                  type: string
                  minLength: 1
                  maxLength: 200
                price:
                  type: number
                  format: decimal
                  minimum: 0
                # ... más campos ...
    
  /products/{id}:
    put:
      requestBody:
        content:
          application/json:
            schema:
              type: object
              properties:
                name:
                  type: string
                  minLength: 1
                  maxLength: 200              # ¡REPETIDO!
                price:
                  type: number
                  format: decimal
                  minimum: 0                  # ¡REPETIDO!
                # ... mismos campos repetidos ...
```

**Entonces lo refactorizas a:**

```yaml
# ✅ SOLUCIÓN: Schema reutilizable
paths:
  /products:
    post:
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'  # Referencia
    
  /products/{id}:
    put:
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'  # Misma referencia

components:
  schemas:
    Product:                         # Definido UNA sola vez
      type: object
      required:
        - name
        - price
        - category
      properties:
        name:
          type: string
          minLength: 1
          maxLength: 200
        description:
          type: string
          maxLength: 1000
        price:
          type: number
          format: decimal
          minimum: 0
        category:
          type: string
          enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
        # ... resto de campos ...
```

---

## 📄 **Ventajas de usar referencias ($ref)**

| Aspecto                | Definición Directa              | Referencia ($ref)          |
| ---------------------- | ------------------------------- | -------------------------- |
| **Mantenimiento**      | ❌ Cambios en múltiples lugares | ✅ Cambio en un solo lugar |
| **Legibilidad**        | ❌ Código repetitivo            | ✅ Código limpio           |
| **Reutilización**      | ❌ Copy/paste manual            | ✅ Automática              |
| **Consistencia**       | ❌ Fácil de desincronizar       | ✅ Siempre consistente     |
| **Tamaño del archivo** | ❌ Más grande                   | ✅ Más compacto            |

---

## 🔍 **Cuándo convertir campos a Schemas**

### **Señales de que necesitas crear un schema:**

1. **Repetición**: Usas los mismos campos en 2+ operaciones
2. **Complejidad**: Tienes más de 3-4 campos
3. **Validaciones complejas**: Patrones, rangos, formatos específicos
4. **Evolución**: Planeas agregar más campos en el futuro

### **Proceso de conversión:**

#### **Paso 1: Identifica la repetición**

```yaml
# ¿Usas estos campos en múltiples lugares?
properties:
  idClient:
    type: string
    pattern: '^[BP]C-[0-9]{3}$'
  activity:
    type: string
    minLength: 5
    maxLength: 255
```

#### **Paso 2: Extrae a components/schemas**

```yaml
components:
  schemas:
    Product:
      type: object
      required: [name, price, category]
      properties:
        name:
          type: string
          minLength: 1
          maxLength: 200
        description:
          type: string
          maxLength: 1000
        price:
          type: number
          format: decimal
          minimum: 0
        category:
          type: string
          enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
        # ... más campos ...
```

#### **Paso 3: Reemplaza con referencias**

```yaml
# Antes:
schema:
  type: object
  properties:
    name: ...
    price: ...

# Después:
schema:
  $ref: '#/components/schemas/Product'
```

### ¿Por qué usar `$ref`?

- **Reutilización**: El mismo esquema se usa en varias operaciones
- **Mantenimiento**: Cambios en un solo lugar
- **Legibilidad**: Evita repetir código
- **Escalabilidad**: Facilita el crecimiento de la API

### ¿Por qué `$ref`?

- **Reutilización**: El mismo esquema se usa en varias operaciones
- **Mantenimiento**: Cambios en un solo lugar
- **Legibilidad**: Evita repetir código
