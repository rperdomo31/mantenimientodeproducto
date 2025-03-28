# Mantenimiento de Producto
Trabajo final 2 para PYT- 01/Programación Python - PYT-01 VIERNES 5-7 PM MARZO - ABRIL 2022 - Prof. Francis Fulgencio

#Code
class Categoria:
    def __init__(self, id, nombre):
        self.id = id
        self.nombre = nombre
    
    def __str__(self):
        return f"ID: {self.id}, Nombre: {self.nombre}"

class Producto:
    def __init__(self, id, nombre, precio, categoria):
        self.id = id
        self.nombre = nombre
        self.precio = precio
        self.categoria = categoria
    
    def __str__(self):
        return f"ID: {self.id}, Nombre: {self.nombre}, Precio: ${self.precio}, Categoría: {self.categoria.nombre}"

class Mantenimiento:
    def __init__(self):
        self.categorias = [Categoria(i, f"Categoría{i}") for i in range(1, 6)]
        self.productos = [
            Producto(i, f"Producto{i}", round(10 + i * 2.5, 2), self.categorias[i % 5])
            for i in range(1, 11)
        ]
    
    def agregar_categoria(self):
        while True:
            id = input("Ingrese ID de la categoría: ")
            nombre = input("Ingrese Nombre de la categoría: ")
            self.categorias.append(Categoria(id, nombre))
            
            otro = input("¿Desea agregar otra categoría? (s/n): ").lower()
            if otro != 's':
                break
    
    def agregar_producto(self):
        while True:
            id = input("Ingrese ID del producto: ")
            nombre = input("Ingrese Nombre: ")
            precio = float(input("Ingrese Precio: "))
            print("Categorías disponibles:")
            for c in self.categorias:
                print(c)
            categoria_id = input("Ingrese ID de la categoría del producto: ")
            categoria = next((c for c in self.categorias if c.id == categoria_id), None)
            if categoria:
                self.productos.append(Producto(id, nombre, precio, categoria))
                print("Producto agregado correctamente.")
            else:
                print("Categoría no encontrada.")
            
            otro = input("¿Desea agregar otro producto? (s/n): ").lower()
            if otro != 's':
                break
    
    def buscar(self, lista, tipo):
        criterio = input(f"Buscar {tipo} por (1) ID o (2) Nombre: ")
        if criterio == "1":
            id_buscar = input("Ingrese ID: ")
            resultados = [e for e in lista if e.id == id_buscar]
        elif criterio == "2":
            nombre_buscar = input("Ingrese Nombre: ")
            resultados = [e for e in lista if nombre_buscar.lower() in e.nombre.lower()]
        else:
            print("Opción inválida.")
            return
        
        if resultados:
            for e in resultados:
                print(e)
        else:
            print(f"{tipo} no encontrado.")
    
    def actualizar(self, lista, tipo):
        id_buscar = input(f"Ingrese ID del {tipo} a actualizar: ")
        for e in lista:
            if e.id == id_buscar:
                e.nombre = input(f"Ingrese nuevo Nombre del {tipo}: ")
                if isinstance(e, Producto):
                    e.precio = float(input("Ingrese nuevo Precio: "))
                    print("Categorías disponibles:")
                    for c in self.categorias:
                        print(c)
                    categoria_id = input("Ingrese nuevo ID de la categoría: ")
                    e.categoria = next((c for c in self.categorias if c.id == categoria_id), e.categoria)
                print(f"{tipo} actualizado correctamente.")
                return
        print(f"{tipo} no encontrado.")
    
    def borrar(self, lista, tipo):
        id_buscar = input(f"Ingrese ID del {tipo} a borrar: ")
        for e in lista:
            if e.id == id_buscar:
                lista.remove(e)
                print(f"{tipo} eliminado correctamente.")
                return
        print(f"{tipo} no encontrado.")
    
    def listar(self, lista, tipo):
        if lista:
            for e in lista:
                print(e)
        else:
            print(f"No hay {tipo}s guardados.")
    
    def menu(self):
        while True:
            print("\n--- Mantenimiento de Productos y Categorías ---")
            print("1. Agregar Categoría")
            print("2. Agregar Producto")
            print("3. Buscar Categoría")
            print("4. Buscar Producto")
            print("5. Actualizar Categoría")
            print("6. Actualizar Producto")
            print("7. Borrar Categoría")
            print("8. Borrar Producto")
            print("9. Listar Categorías")
            print("10. Listar Productos")
            print("11. Salir")
            
            opcion = input("Seleccione una opción: ")
            
            if opcion == "1":
                self.agregar_categoria()
            elif opcion == "2":
                self.agregar_producto()
            elif opcion == "3":
                self.buscar(self.categorias, "Categoría")
            elif opcion == "4":
                self.buscar(self.productos, "Producto")
            elif opcion == "5":
                self.actualizar(self.categorias, "Categoría")
            elif opcion == "6":
                self.actualizar(self.productos, "Producto")
            elif opcion == "7":
                self.borrar(self.categorias, "Categoría")
            elif opcion == "8":
                self.borrar(self.productos, "Producto")
            elif opcion == "9":
                self.listar(self.categorias, "Categoría")
            elif opcion == "10":
                self.listar(self.productos, "Producto")
            elif opcion == "11":
                print("Saliendo...")
                break
            else:
                print("Opción inválida. Intente de nuevo.")

if __name__ == "__main__":
    mantenimiento = Mantenimiento()
    mantenimiento.menu()
