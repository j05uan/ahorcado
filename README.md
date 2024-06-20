# ahorcado

~~~java
import java.util.Scanner;

public class Ahorcado {

    private static String palabraSecreta;
    private static StringBuilder palabraConGuiones;
    private static int intentosRestantes;
    private static final int MAX_INTENTOS = 6;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Inicializar el juego
        inicializarJuego();

        // Bucle principal del juego
        while (intentosRestantes > 0 && palabraConGuiones.indexOf("_") != -1) {
            mostrarTablero();
            System.out.println("Ingrese una letra:");
            String letra = scanner.nextLine().toLowerCase();

            if (letra.length() == 1 && Character.isLetter(letra.charAt(0))) {
                comprobarLetra(letra.charAt(0));
            } else {
                System.out.println("Por favor, ingrese una letra válida.");
            }
        }

        // Juego terminado: mostrar resultado
        if (intentosRestantes > 0) {
            System.out.println("¡Felicidades! Has adivinado la palabra: " + palabraSecreta);
        } else {
            System.out.println("¡Oh no! Has perdido. La palabra era: " + palabraSecreta);
        }

        scanner.close();
    }

    private static void inicializarJuego() {
        palabraSecreta = seleccionarPalabra();
        palabraConGuiones = new StringBuilder("_".repeat(palabraSecreta.length()));
        intentosRestantes = MAX_INTENTOS;
    }

    private static void mostrarTablero() {
        System.out.println("Palabra: " + palabraConGuiones);
        System.out.println("Intentos restantes: " + intentosRestantes);
    }

    private static String seleccionarPalabra() {
        // Aquí puedes tener un array de palabras o seleccionar una al azar
        String[] palabras = {"computadora", "programacion", "java", "ahorcado", "openai"};
        return palabras[(int) (Math.random() * palabras.length)];
    }

    private static void comprobarLetra(char letra) {
        boolean letraEncontrada = false;
        for (int i = 0; i < palabraSecreta.length(); i++) {
            if (palabraSecreta.charAt(i) == letra) {
                palabraConGuiones.setCharAt(i, letra);
                letraEncontrada = true;
            }
        }
        if (!letraEncontrada) {
            intentosRestantes--;
            System.out.println("Letra incorrecta. Intentos restantes: " + intentosRestantes);
        }
    }
}
~~~
