using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ConsoleApp5
{
    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("=== SIMULADOR DE VENTAS CON DESCUENTOS ===");

            int n = 0;
            bool valido = false;

            while (!valido)
            {
                Console.Write("¿Cuántos productos desea ingresar?: ");

                if (int.TryParse(Console.ReadLine(), out n) && n > 0)
                {
                    valido = true;
                }
                else
                {
                    Console.WriteLine("Dato inválido. Debe ingresar un número entero positivo.\n");
                }
            }

            double[] precios = new double[n];

            for (int i = 0; i < n; i++)
            {
                valido = false;

                while (!valido)
                {
                    Console.Write($"Ingrese el precio del producto {i + 1}: S/ ");
                    string entrada = Console.ReadLine();

                    if (double.TryParse(entrada, out double precio) && precio >= 0)
                    {
                        precios[i] = precio;
                        valido = true;
                    }
                    else
                    {
                        Console.WriteLine("Dato inválido. Ingrese un número válido y positivo.\n");
                    }
                }
            }


            double total = CalcularTotal(precios);
            double descuento = AplicarDescuento(total);


            MostrarRecibo(total, descuento);

            Console.WriteLine("\nGracias por su compra. ¡Vuelva pronto!");

        }

        static double CalcularTotal(double[] precios)
        {
            double total = 0;
            for (int i = 0; i < precios.Length; i++)
            {
                total += precios[i];
            }
            return total;
        }


        static double AplicarDescuento(double total)
        {
            double descuento = 0;

            if (total < 50)
                descuento = 0;
            else if (total >= 50 && total < 100)
                descuento = total * 0.05;
            else if (total >= 100 && total < 200)
                descuento = total * 0.10;
            else if (total >= 200)
                descuento = total * 0.15;

            return descuento;
        }

        static void MostrarRecibo(double total, double descuento)
        {
            double montoFinal = total - descuento;

            Console.WriteLine("\n*** RECIBO FINAL ***");
            Console.WriteLine($"Total de compra: S/ {total:F2}");
            Console.WriteLine($"Descuento aplicado: S/ {descuento:F2}");
            Console.WriteLine($"Monto a pagar: S/ {montoFinal:F2}");
            Console.WriteLine("");
            Console.WriteLine("");
        }
    }
}



