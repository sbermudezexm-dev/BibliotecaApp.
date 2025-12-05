import javax.swing.*;
import java.util.*;

// Clase Autor
class Autor {
    private String nombre;
    private String nacionalidad;
    private Date fechaNacimiento;

    public Autor(String nombre, String nacionalidad, Date fechaNacimiento) {
        this.nombre = nombre;
        this.nacionalidad = nacionalidad;
        this.fechaNacimiento = fechaNacimiento;
    }

    public String getNombre() {
        return nombre;
    }

    @Override
    public String toString() {
        return nombre + " (" + nacionalidad + ")";
    }
}

// Clase Libro
class Libro {
    private String titulo;
    private String isbn;
    private int año;
    private Autor autor;

    public Libro(String titulo, String isbn, int año, Autor autor) {
        this.titulo = titulo;
        this.isbn = isbn;
        this.año = año;
        this.autor = autor;
    }

    public String getTitulo() {
        return titulo;
    }

    @Override
    public String toString() {
        return titulo + " (" + año + ") - " + autor.getNombre();
    }
}

// Clase Biblioteca
class Biblioteca {
    private String nombre;
    private String direccion;
    private List<Libro> listaLibros;

    public Biblioteca(String nombre, String direccion) {
        this.nombre = nombre;
        this.direccion = direccion;
        this.listaLibros = new ArrayList<>();
    }

    public void agregarLibro(Libro libro) {
        listaLibros.add(libro);
    }

    public List<Libro> listarLibros() {
        return listaLibros;
    }
}

// Clase BibliotecaUI (interfaz gráfica)
class BibliotecaUI {
    private Biblioteca biblioteca;
    private DefaultListModel<String> modeloLista;
    private JList<String> listaLibros;

    public BibliotecaUI(Biblioteca biblioteca) {
        this.biblioteca = biblioteca;
        this.modeloLista = new DefaultListModel<>();
        this.listaLibros = new JList<>(modeloLista);
    }

    public void mostrarVentana() {
        JFrame frame = new JFrame("Biblioteca - Mi Librería");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 300);

        for (Libro libro : biblioteca.listarLibros()) {
            modeloLista.addElement(libro.toString());
        }

        frame.add(new JScrollPane(listaLibros));
        frame.setVisible(true);
    }
}

// Clase principal Main
public class BibliotecaApp {
    public static void main(String[] args) {
        Biblioteca biblioteca = new Biblioteca("Mi Librería", "Calle Principal 123");

        Autor autor1 = new Autor("Gabriel García Márquez", "Colombiano", new Date());
        Autor autor2 = new Autor("Isabel Allende", "Chilena", new Date());

        Libro libro1 = new Libro("Cien años de soledad", "123456", 1967, autor1);
        Libro libro2 = new Libro("La casa de los espíritus", "789101", 1982, autor2);

        biblioteca.agregarLibro(libro1);
        biblioteca.agregarLibro(libro2);

        BibliotecaUI ui = new BibliotecaUI(biblioteca);
        ui.mostrarVentana();
    }
}

