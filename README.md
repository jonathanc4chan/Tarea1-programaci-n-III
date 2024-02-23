# Tarea1-programaciOn-III


import java.util.*;

// Implementación de lista enlazada

class ListaEnlazada<T> {

    static class Nodo<T> {
        T valor;
        Nodo<T> siguiente;

        Nodo(T item) {
            valor = item;
            siguiente = null;
        }
    }

    Nodo<T> cabeza;

    ListaEnlazada() {
        cabeza = null;
    }

    public void agregarAlFinal(T item) {
        if (cabeza == null) {
            cabeza = new Nodo<>(item);
        } else {
            Nodo<T> temp = cabeza;
            while (temp.siguiente != null) {
                temp = temp.siguiente;
            }
            temp.siguiente = new Nodo<>(item);
        }
    }

    public void imprimir() {
        Nodo<T> temp = cabeza;
        while (temp != null) {
            System.out.print(temp.valor + " ");
            temp = temp.siguiente;
        }
        System.out.println();
    }
}

// Implementación de pila usando lista enlazada
class Pila<T> {
    private ListaEnlazada.Nodo<T> cabeza;

    Pila() {
        cabeza = null;
    }

    public void push(T item) {
        ListaEnlazada.Nodo<T> nuevoNodo = new ListaEnlazada.Nodo<>(item);
        nuevoNodo.siguiente = cabeza;
        cabeza = nuevoNodo;
    }

    public T pop() {
        if (cabeza == null) {
            throw new NoSuchElementException("La pila está vacía");
        }
        T valor = cabeza.valor;
        cabeza = cabeza.siguiente;
        return valor;
    }

    public boolean isEmpty() {
        return cabeza == null;
    }
}

// Implementación de cola usando lista enlazada
class Cola<T> {
    private ListaEnlazada.Nodo<T> cabeza;
    private ListaEnlazada.Nodo<T> cola;

    Cola() {
        cabeza = null;
        cola = null;
    }

    public void enqueue(T item) {
        ListaEnlazada.Nodo<T> nuevoNodo = new ListaEnlazada.Nodo<>(item);
        if (cabeza == null) {
            cabeza = nuevoNodo;
            cola = nuevoNodo;
        } else {
            cola.siguiente = nuevoNodo;
            cola = nuevoNodo;
        }
    }

    public T dequeue() {
        if (cabeza == null) {
            throw new NoSuchElementException("La cola está vacía");
        }
        T valor = cabeza.valor;
        cabeza = cabeza.siguiente;
        return valor;
    }

    public boolean isEmpty() {
        return cabeza == null;
    }
}

// Implementación de árbol binario
class ArbolBinario<T> {
    static class Nodo<T> {
        T valor;
        Nodo<T> izquierdo;
        Nodo<T> derecho;

        Nodo(T valor) {
            this.valor = valor;
            izquierdo = null;
            derecho = null;
        }
    }

    private Nodo<T> raiz;

    ArbolBinario() {
        raiz = null;
    }

    public void insertar(T valor) {
        raiz = insertarRec(raiz, valor);
    }

    private Nodo<T> insertarRec(Nodo<T> nodo, T valor) {
        if (nodo == null) {
            return new Nodo<>(valor);
        }
        if (valor.hashCode() < nodo.valor.hashCode()) {
            nodo.izquierdo = insertarRec(nodo.izquierdo, valor);
        } else if (valor.hashCode() > nodo.valor.hashCode()) {
            nodo.derecho = insertarRec(nodo.derecho, valor);
        }
        return nodo;
    }

    public void preorden() {
        preordenRec(raiz);
    }

    private void preordenRec(Nodo<T> nodo) {
        if (nodo != null) {
            System.out.print(nodo.valor + " ");
            preordenRec(nodo.izquierdo);
            preordenRec(nodo.derecho);
        }
    }

    public void inorden() {
        inordenRec(raiz);
    }

    private void inordenRec(Nodo<T> nodo) {
        if (nodo != null) {
            inordenRec(nodo.izquierdo);
            System.out.print(nodo.valor + " ");
            inordenRec(nodo.derecho);
        }
    }

    public void postorden() {
        postordenRec(raiz);
    }

    private void postordenRec(Nodo<T> nodo) {
        if (nodo != null) {
            postordenRec(nodo.izquierdo);
            postordenRec(nodo.derecho);
            System.out.print(nodo.valor + " ");
        }
    }
}

public class tarea_1 {
    public static void main(String[] args) {
        // Prueba de lista enlazada
        System.out.println("Lista enlazada:");
        ListaEnlazada<Integer> lista = new ListaEnlazada<>();
        lista.agregarAlFinal(1);
        lista.agregarAlFinal(2);
        lista.agregarAlFinal(3);
        lista.agregarAlFinal(4);
        lista.agregarAlFinal(5);
        lista.agregarAlFinal(6);
        lista.agregarAlFinal(7);
        lista.agregarAlFinal(8);
        lista.agregarAlFinal(9); // Agregamos más elementos
        lista.agregarAlFinal(10);
        lista.imprimir();

        // Prueba de pila
        System.out.println("\nPila:");
        Pila<Integer> pila = new Pila<>();
        pila.push(1);
        pila.push(2);
        pila.push(3);
        pila.push(4);
        pila.push(5);
        pila.push(6);
        pila.push(7);
        pila.push(8);
        pila.push(9); // Agregamos más elementos
        pila.push(10);
        while (!pila.isEmpty()) {
            System.out.print(pila.pop() + " ");
        }
        System.out.println();

        // Prueba de cola
        System.out.println("\nCola:");
        Cola<Integer> cola = new Cola<>();
        cola.enqueue(1);
        cola.enqueue(2);
        cola.enqueue(3);
        cola.enqueue(4);
        cola.enqueue(5);
        cola.enqueue(6);
        cola.enqueue(7);
        cola.enqueue(8);
        cola.enqueue(9); // Agregamos más elementos
        cola.enqueue(10);
        while (!cola.isEmpty()) {
            System.out.print(cola.dequeue() + " ");
        }
        System.out.println();

        // Prueba de árbol binario
        System.out.println("\nÁrbol binario:");
        ArbolBinario<Integer> arbol = new ArbolBinario<>();
        arbol.insertar(5);
        arbol.insertar(3);
        arbol.insertar(7);
        arbol.insertar(2);
        arbol.insertar(4);
        arbol.insertar(6);
        arbol.insertar(8);
        arbol.insertar(1);
        arbol.insertar(9); // Agregamos más nodos al árbol
        arbol.insertar(10);
        System.out.print("Preorden: ");
        arbol.preorden();
        System.out.print("\nInorden: ");
        arbol.inorden();
        System.out.print("\nPostorden: ");
        arbol.postorden();
        System.out.println();
    }
}
