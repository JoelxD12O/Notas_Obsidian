
forward_list:
**TEORIA**
```cpp
#include <forward_list>
#include <iostream>
using namespace std;

int main() {
    forward_list<int> fl = {1, 2, 3};

    // ==============================
    // INSERTAR
    // ==============================
    fl.push_front(0);              // [0 1 2 3]
    fl.emplace_front(-1);          // [ -1 0 1 2 3 ] (construye in-place)

    auto it = fl.begin();          // apunta a -1
    fl.insert_after(it, 100);      // [-1 100 0 1 2 3]
    fl.emplace_after(it, 200);     // [-1 200 100 0 1 2 3]

    // insert_after con rango o lista
    fl.insert_after(it, {7, 8, 9}); // [-1 7 8 9 200 100 0 1 2 3]

    // ==============================
    // ELIMINAR
    // ==============================
    fl.pop_front();                // elimina primer elemento [-1] → [7 8 9 200 100 0 1 2 3]

    fl.erase_after(it);            // elimina después de it (borra el 7) [8 9 200 100 0 1 2 3]

    fl.remove(100);                // elimina todas las ocurrencias de 100
    fl.remove_if([](int x){ return x % 2 == 0; }); // elimina pares

    fl.clear();                    // elimina todo → lista vacía

    // ==============================
    // ASIGNACIÓN Y REEMPLAZO
    // ==============================
    fl.assign({1,2,3,4});          // [1 2 3 4]
    fl.assign(5, 10);              // [10 10 10 10 10]

    fl = {1,2,3};                  // operador =

    // ==============================
    // ACCESO / INFO
    // ==============================
    cout << "Primer elem: " << fl.front() << endl;  // 1

    cout << "Lista: ";
    for (int x : fl) cout << x << " ";  // 1 2 3
    cout << endl;

    // ==============================
    // ORDEN Y UNIÓN
    // ==============================
    fl = {5, 2, 9, 1};
    fl.sort();                      // [1 2 5 9]
    fl.reverse();                   // [9 5 2 1]

    forward_list<int> fl2 = {3, 4};
    fl.merge(fl2);                  // fusiona listas ordenadas

    // ==============================
    // SPLICE (mover elementos)
    // ==============================
    forward_list<int> fl3 = {10, 20};
    fl.splice_after(fl.before_begin(), fl3); 
    // mueve [10, 20] de fl3 a fl → [10 20 9 5 2 1]

    cout << "Final: ";
    for (int x : fl) cout << x << " ";
    cout << endl;
}
```
# Complejidad de operaciones en `std::forward_list`

| Operación                       | Complejidad | Comentario |
|---------------------------------|-------------|------------|
| Acceso por índice (i-ésimo)     | O(n)        | No hay acceso aleatorio, se debe recorrer |
| Recorrer toda la lista          | O(n)        | Va de nodo en nodo hasta el final |
| Insertar al frente (`push_front`)| O(1)       | Directo sobre `head` |
| Insertar después de un iterador (`insert_after`) | O(1) | Si ya tienes el iterador |
| Eliminar después de un iterador (`erase_after`) | O(1) | Si ya tienes el iterador |
| Borrar el primero (`pop_front`) | O(1)        | Directo sobre `head` |
| Buscar por valor (`find`)       | O(n)        | Debe recorrer la lista |
| Tamaño de la lista (`distance`) | O(n)        | `forward_list` **no guarda tamaño** |
| Invertir la lista (`reverse`)   | O(n)        | Reorganiza punteros uno por uno |
| Ordenar (`sort`)                | O(n log n)  | Implementado con merge sort |
| Eliminar duplicados (`unique`)  | O(n)        | Solo funciona en listas ordenadas |

---

📌 **Nota clave**:  
- `forward_list` es **lista enlazada simple**, no tiene puntero al anterior, por eso muchas operaciones solo funcionan en O(1) si ya tienes un **iterador previo**.  
- No tiene `.size()` (sería O(n)), mientras que `list` sí lo guarda en O(1).  
--------------------------------------------------------------------------
`LISTAS ENLAZADAS`

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next; // puntero al siguiente nodo
};

int main() {
    // Crear nodos manualmente
    Node* n1 = new Node{1, nullptr};
    Node* n2 = new Node{2, nullptr};
    Node* n3 = new Node{3, nullptr};

    // Enlazar nodos
    n1->next = n2;
    n2->next = n3;

    // Recorrer la lista
    Node* head = n1;
    while (head != nullptr) {
        cout << head->data << " ";
        head = head->next;
    }
    // salida: 1 2 3
}
## 📊 Complejidad típica

- **Insertar al frente**: O(1).
    
- **Insertar en medio (con puntero al nodo anterior)**: O(1).
    
- **Buscar por valor**: O(n).
    
- **Acceso aleatorio (posición i)**: O(n), porque hay que recorrer.
  
  ## 🔑 Comparación con vector

- `vector`: acceso rápido por índice (`O(1)`), pero insertar en medio puede costar caro (`O(n)`).
    
- `lista enlazada`: acceso secuencial lento (`O(n)`), pero inserciones/borrados en medio son rápidos (`O(1)`).
```


array simple 
-ventajas:
	-acceso aleatorio/directo a una celda
	array[i],array[i+1],array[i-1]
-desventajas:
	 -requiere redimensionar 0(n)
	 -eliminar o insertar al inicio 0(n)
	 -eliminar o insertar en una posicion K 0(n)
	 - int* array=new int [1000];

si tienes un contenedor lineal que no cambiara y conozco el tamaño y se va mover es un array 

tareas crear propio forward list con nodos punteros, hacer los ejercicios 