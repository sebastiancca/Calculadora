# Calculadora
package calculadora;
public class Logica {

    public Logica() 
    {
    }
    public double suma(double numero1, double numero2) //una varible numero1 y variable numero2,para realizar una suma
    {
        return numero1 + numero2; //devolver una varibale y la sumamos con otra variable
    }

    public double resta(double numero1, double numero2) //una variable numero1 y variable numero2,para realizar una resta
    {
        return numero1 - numero2; //devolver una varibale y la restamos con otra variable
    }

    public double modulo(double numero1, double numero2)  //una varible numero1 y variable numero2,para realizar un modulo
    {
        double respuesta = numero1; //la variable respuesta es igual ala variable numero1
        double memoria = numero1; //la variable memoria es igual ala variable numero1
        while (memoria >= 0)  //la variable memoria tiene que ser igual a 0 o mayor que cero
        {
            respuesta = memoria; //la variable respuesta 
            memoria = resta(respuesta, numero2); //la variable meoria es igual a varible respuesta y numero2
        }
        return respuesta; //devolver la variable respuestas 
    }

    public double multiplicacion(double numero1, double numero2) //una varible numero1 y variable numero2, para realizar una multiplicacion en forma recursiva
    {
        double respuesta = 0; //la variable respuesta es igual a 0
        if (numero2 < 0)  //si numero2 es menor a 0
        {
            respuesta = (multiplicacionAuxiliar(numero1, numero2 * -1) * -1); 
        } else 
        {
            respuesta = multiplicacionAuxiliar(numero1, numero2);
        }
        return respuesta; //devolver la variable respuesta
    }

    private double multiplicacionAuxiliar(double numero1, double numero2) 
    {
        double acumulador = 0;
        for (int i = 0; i < numero2; i++) // ciclo para una suma
        {
            acumulador += numero1; // la variable acumulador para que valla aumentando con numero1
        }
        return acumulador; //devolver la variable acumulador
    }

    public static double division(double num1, double num2)  //una variable num1 y variable num, donde se va a realizar una division
    {
        if (num2 != 0)  // si num2 es diferente de 0 , una condicion para que no halla indeterminacion
        {
            return num1 / num2; //retomamos num1 y dividimos  con num2
        } else 
        {
            return Double.NaN; //retomamos ek error.NaN indicando que no hay indeterminacion
        }
    }

    private int divisionPaso1(double dividendo, double divisor) // se va a realizar una division paso 1
    {
        int respuesta = 0; //la variable respuesta tiene que ser igual a 0
        while (multiplicacion(respuesta, divisor) <= dividendo) 
        {
            respuesta++; 
        }
        return respuesta - 1;
    }

    public double factorial(double numero)  // se va a realizar un factorial
    {
        if (numero == 0)  //condicion cuando el numero es menor que 1
        {
            return 1; //retoma el 1
        } else // si cumple la condicion
        {
            return multiplicacion(numero, factorial(numero - 1)); // se devuvuelve la multplicacion con un numero y el facotia
        }
    }

    public double potencia(double base, double exponente) // potencia 
    {
        double resultado = base; // la condicion el resultado tiene que ser igual a 0
        for (int i = 1; i < exponente; i++)  // una sumatoria
        {
            resultado = resultado * base; 
        }
        if (exponente == 0) 
        {
            resultado = 1;
        }
        return resultado;
    }

    public double seno(double n, double x)  // Seno de la forma de taylor
    {
        double sumatoria = 0;
        for (int i = 0; i < n; i++) // una sumatoria
        {
            sumatoria = division(potencia(x, i), factorial(i)); //sumatoria es igual ala division y llamamos ala potencia  y un factorial
        }
        return sumatoria; //retomamos la sumatoria
    }

    public double coseno(double n, double x) // coseno de taylor
    {
        double sumatoria = 0;
        for (int i = 0; i < n; i += 2) // una sumatoria
        {
            sumatoria = division(potencia(x, i), factorial(i)); //sumatoria es igual ala division y llamamos ala potencia  y un factorial
        }
        return sumatoria;  //retomamos la sumatoria
    }

    public double integral(double inicio, double fin, double paso) //integral 
    {
        double acum = 0;
        for (double i = 0; i < fin; i += paso) //una sumatoria 
        {
            acum += (paso * potencia(i,2)); // paso multiplicado por una potencia 
        }
        return acum;
    }

    public double cuadraticaPositiva(double a, double b, double c) //formula cuadratica con el valor positivo
    {
        return division(suma(multiplicacion(b, -1), Math.sqrt(resta(multiplicacion(b, b), multiplicacion(4, multiplicacion(a, c))))), multiplicacion(2, a));
    }

    public double cuadraticaNegativa(double a, double b, double c) //formula cuadratica con el valor negativo
    {
        return ((b * -1) - Math.sqrt((b * b) - 4 * a * c)) / (2 * a);
    }

}



package calculadora;
import java.io.*;
public class GI {

    public static BufferedReader br;
    public static BufferedWriter bw;

    public GI() {
        this.br = new BufferedReader(new InputStreamReader(System.in)); //ler
        this.bw = new BufferedWriter(new OutputStreamWriter(System.out)); // escribir
    }

    public void mostrarMenu() throws IOException {
        double opciones; //opcion
        double[] parametros; // parametros
        opciones = getOptions();
        parametros = getParametros(opciones); //condicion
        makeOperation(opciones, parametros);
        mostrarMenu();
    }

    private double getOptions() throws IOException  // opciones del menu
    { 
        bw.write(""
                + "\nselecione el numero de la operacion que desa realizar"
                + "\n 1 suma"
                + "\n 2 resta"
                + "\n 3 modulo"
                + "\n 4 multiplicacion"
                + "\n 5 divicion"
                + "\n 6 factorial"
                + "\n 7 potencia"
                + "\n 8 seno"
                + "\n 9 coseno"
                + "\n 10 cuadratica"
                +"\n 11 integral"
                + "\n 12 salir");
        bw.flush();

        int option = Integer.parseInt(br.readLine());
        return option; //retomar option
    }

    private double[] getParametros(double opcion) throws IOException {
        double[] paramet = null; 
        switch ((int) opcion) //Switch de 11 case 
        {
            case 1: //Suma 
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de suma. \n"); //moostar en consola
                bw.write("Ingrese el primer numero:"); //ingresar el primer numero y mostrar en consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine()); // parametro

                bw.write("\nIngrese el segundo numero:"); // ingresar el otro numero mostrado por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 2: //Resta 
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de resta. \n"); //escribir
                bw.write("Ingrese el primer numero:"); //ingresar el primer numero mostrado por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\nIngrese el segundo numero:");// ingresar el segundo numero y mostrado por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 3: //Modulo
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de modulo. \n"); //escribir
                bw.write("Ingrese el primer numero:"); //ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\nIngrese el segundo numero:"); //ingresar el segundo numero y mostrarlo por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 4: //Multiplicacion
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de multiplicacion. \n"); //escribir
                bw.write("Ingrese el primer numero:"); // ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\nIngrese el segundo numero:"); // ingresar el segundo numero y mostrarlo por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 5: //Division 
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de division.");
                bw.write("\nIngrese el primer numero:"); // ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\nIngrese el segundo numero:"); // ingresar el segundo numero y mostrarlo por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 6: //Factorial 
            {
                paramet = new double[1];
                bw.write("\nA acontinuacion se va a realizar una operacion de factorial. \n");
                bw.write("Ingrese el primer numero:"); // ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());
                break;
            }
            case 7: //Potencia 
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de potencia. \n");
                bw.write("Ingrese el primer numero:"); // ingresar el primer numero y mostrarlo por consola
                bw.flush(); 

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el segundo numero:");  // ingresar el segundo numero y mostrarlo por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 8: //seno  
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de seno. \n");
                bw.write("Ingrese el primer numero:"); // ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el segundo numero:");// ingresar el segundo numero y mostrarlo por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 9: //coseno
            {
                paramet = new double[2];
                bw.write("\nA acontinuacion se va a realizar una operacion de coseno. \n");
                bw.write("Ingrese el primer numero:");// ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el segundo numero:"); // ingresar el segundo numero y mostrarlo por consola
                bw.flush();
                paramet[1] = Double.parseDouble(br.readLine());
                break;
            }
            case 10: //Cuadratica  
            {
                paramet = new double[3];
                bw.write("\nA acontinuacion se va a realizar una operacion de cuadratica. \n");// consola cuando muestra que se va a realizar la operacion
                bw.write("Ingrese el primer numero de la letra a:");// ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el segundo numero de la letra b:"); // ingresar el segundo numero y mostrarlo por consola
                bw.flush();

                paramet[1] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el tercer numero de la letra c:"); // ingresar el tercer numero y mostrarlo por consola
                bw.flush();

                paramet[2] = Double.parseDouble(br.readLine());
                break;
            }
            case 11: //Integral
            {
                paramet = new double[3];
                bw.write("\nA acontinuacion se va a realizar una operacion de integral. \n");
                bw.write("Ingrese el primer numero:"); // ingresar el primer numero y mostrarlo por consola
                bw.flush();

                paramet[0] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el segundo numero:"); // ingresar el segundo numero y mostrarlo por consola
                bw.flush();

                paramet[1] = Double.parseDouble(br.readLine());

                bw.write("\n Ingrese el tercer numero:"); // ingresar el tercero numero y mostrarlo por consola
                bw.flush();

                paramet[2] = Double.parseDouble(br.readLine());
                break;
            }
            default: //Salir
            
            {
                System.exit(0);
            }

        }
        return paramet; //retomar paraet
    }

    private void makeOperation(double opcion, double[] parametros) throws IOException {
        Logica lo = new Logica();
        switch ((int) opcion) {
            case 1: //Suma 
            {
                bw.write("\nEl resultado de la suma es: " + lo.suma(parametros[0], parametros[1])); // el resultado de la suma con los dos parametros
                bw.flush();
                break;
            }
            case 2: //Resta
            {
                bw.write("\nEl resultado de la resta es: " + lo.resta(parametros[0], parametros[1])); // el resultado de la resta con los dos parametros
                bw.flush();
                break;
            }
            case 3: //Modulo
            {
                bw.write("\nEl resultado del modulo es:" + lo.modulo(parametros[0], parametros[1]));// el resultado de la modulo con los dos parametros y lo muestra por consola
                bw.flush();
                break;
            }
            case 4: //Multiplicacion
            {
                bw.write("\nEl resultado de la multiplicaion es:" + lo.multiplicacion(parametros[0], parametros[1]));// el resultado de la multiplicacion con los dos parametros y lo muestra por consola
                bw.flush();
                break;
            }
            case 5: //Division
            {
                bw.write("\nEl resultado de la division es:" + lo.division(parametros[0], parametros[1]));// el resultado de la division con los dos parametros y lo muestra por consola
                bw.flush();
                break;
            }
            case 6: //Factorial
            {
                bw.write("\nEl resultado del factorial es:" + lo.factorial(parametros[0])); // el resultado de lafactorial con el  parametros y lo muestra por consola
                bw.flush();
                break;
            }
            case 7: //Potencia
            {
                bw.write("\nEl resultado de la potencia es:" + lo.potencia(parametros[0], parametros[1])); // el resultado de la potencia con los dos parametros y lo muestra por consola
                bw.flush();
                break;
            }
            case 8: //Seno
            {
                bw.write("\nEl resultado del seno es:" + lo.seno(parametros[0], parametros[1]));// el resultado de la seno con los dos parametros y lo muestra en consola
                bw.flush();
                break;
            }
            case 9: //Coseno
            {
                bw.write("\nEl resultado del coceno es:" + lo.coseno(parametros[0], parametros[1]));// el resultado de la coceno con los dos parametros y lo muestra en consola
                bw.flush();
                break;
            }
            case 10: //Cuadratica
            {
                bw.write("\nEl resultado de la cuadratica positiva es:" + lo.cuadraticaPositiva(parametros[0], parametros[1], parametros[2])); // el resultado de la cuadratica positiva con los tres parametros y lo muestra en consola
                bw.write("\nEl resultado de la cuadratica negatica es:" + lo.cuadraticaNegativa(parametros[0], parametros[1], parametros[2]));// el resultado de la cuadratica negativa con los tres parametros y lo muestra en consola
                bw.flush();
                break;
            }
            case 11: //Integral
            {
                bw.write("\nEl resultado de la integral es:" + lo.integral(parametros[0], parametros[1], parametros[2])); // el resultado de la integral con los tres parametros y lo muestra en consola
                bw.flush();
                break;
            }
            
        }
    }
}


package calculadora;
import java.io.IOException;
public class Calculadora 
{
    public static void main(String[] args) throws IOException 
    {
        GI graficos = new GI(); //llamo ala clase Gi graficos
        graficos.mostrarMenu(); //muesta el menu y se ejecuta

    }
    
}
