using System;
using System.Globalization;

namespace FigurasYEdad
{
    internal class Program
    {
        // ---------- FUNCIONES ----------

        // Área del triángulo = (base * altura) / 2
        static double AreaTriangulo(double baseT, double altura)
        {
            return (baseT * altura) / 2;
        }

        // Área del cuadrado = lado * lado
        static double AreaCuadrado(double lado)
        {
            return lado * lado;
        }

        // Área del círculo = PI * radio^2
        static double AreaCirculo(double radio)
        {
            return Math.PI * radio * radio;
        }

        // Mensaje según la edad
        static string MensajeEdad(int edad)
        {
            if (edad >= 18)
                return $"Con {edad} años eres MAYOR de edad.";
            return $"Con {edad} años eres MENOR de edad.";
        }

        // ---------- LECTURA SEGURA ----------

        static double LeerDecimal(string mensaje)
        {
            while (true)
            {
                Console.Write(mensaje);
                string texto = (Console.ReadLine() ?? "").Replace(',', '.');
                if (double.TryParse(texto, NumberStyles.Float, CultureInfo.InvariantCulture, out double valor) && valor > 0)
                    return valor;
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine("  Valor inválido. Ingresa un número mayor que 0.");
                Console.ResetColor();
            }
        }

        static int LeerEdad()
        {
            while (true)
            {
                Console.Write("Ingresa tu edad: ");
                if (int.TryParse(Console.ReadLine(), out int edad) && edad >= 0 && edad <= 120)
                    return edad;
                Console.ForegroundColor = ConsoleColor.Red;
                Console.WriteLine("  Edad inválida. Ingresa un número entre 0 y 120.");
                Console.ResetColor();
            }
        }

        static void Resultado(string texto)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine($"\n  >> {texto}");
            Console.ResetColor();
        }

        // ---------- PROGRAMA PRINCIPAL ----------

        static void Main(string[] args)
        {
            string opcion;
            do
            {
                Console.WriteLine("\n==============================");
                Console.WriteLine("   CALCULADORA DE ÁREAS Y EDAD");
                Console.WriteLine("==============================");
                Console.WriteLine(" 1. Área del triángulo");
                Console.WriteLine(" 2. Área del cuadrado");
                Console.WriteLine(" 3. Área del círculo");
                Console.WriteLine(" 4. Verificar mayoría de edad");
                Console.WriteLine(" 5. Salir");
                Console.Write("Elige una opción (1-5): ");
                opcion = Console.ReadLine() ?? "";

                switch (opcion)
                {
                    case "1":
                        double b = LeerDecimal("Base: ");
                        double h = LeerDecimal("Altura: ");
                        Resultado($"Área del triángulo = {AreaTriangulo(b, h):F2}");
                        break;
                    case "2":
                        double lado = LeerDecimal("Lado: ");
                        Resultado($"Área del cuadrado = {AreaCuadrado(lado):F2}");
                        break;
                    case "3":
                        double r = LeerDecimal("Radio: ");
                        Resultado($"Área del círculo = {AreaCirculo(r):F2}");
                        break;
                    case "4":
                        int edad = LeerEdad();
                        Resultado(MensajeEdad(edad));
                        break;
                    case "5":
                        Console.WriteLine("\n¡Hasta luego!");
                        break;
                    default:
                        Console.ForegroundColor = ConsoleColor.Red;
                        Console.WriteLine("  Opción no válida. Intenta de nuevo.");
                        Console.ResetColor();
                        break;
                }
            } while (opcion != "5");
        }
    }
}
