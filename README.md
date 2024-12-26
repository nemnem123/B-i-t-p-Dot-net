using System;

class Approximation
{
    static void Main(string[] args)
    {
        Console.Write("nhap gia tri epsilon : ");
        if (double.TryParse(Console.ReadLine(), out double epsilon) && epsilon > 0 && epsilon < 1)
        {
            Console.WriteLine($"xap xi π: {ApproximatePi(epsilon):F6}");
            Console.Write("nhap gia tri x cho sin(x): ");
            double x = double.Parse(Console.ReadLine());
            Console.WriteLine($"xap xi sin({x}): {ApproximateSin(x, epsilon):F6}");
            Console.Write("nhap gia tri x cho ln(1+x): ");
            double xLn = double.Parse(Console.ReadLine());
            Console.WriteLine($"xap xi ln(1+{xLn}): {ApproximateLn(xLn, epsilon):F6}");
            Console.Write("nhap gia tri x cho cos(x): ");
            double xCos = double.Parse(Console.ReadLine());
            Console.WriteLine($"xap xi cos({xCos}): {ApproximateCos(xCos, epsilon):F6}");
        }
        else
        {
            Console.WriteLine("hay nhap so hop le (0 < epsilon < 1).");
        }
    }

    static double ApproximatePi(double epsilon)
    {
        double sum = 0;
        double term;
        int n = 0;
        do
        {
            term = Math.Pow(-1, n) / (2 * n + 1);
            sum += term;
            n++;
        } while (Math.Abs(term) >= epsilon);

        return sum * 4;
    }

    static double ApproximateSin(double x, double epsilon)
    {
        double sum = 0;
        double term = x;
        int n = 1;

        while (Math.Abs(term) >= epsilon)
        {
            sum += term;
            n++;
            term *= -x * x / ((2 * n - 2) * (2 * n - 1)); 
        }

        return sum;
    }

    static double ApproximateLn(double x, double epsilon)
    {
        double sum = 0;
        double term = x;
        int n = 1;

        while (Math.Abs(term) >= epsilon)
        {
            sum += term;
            n++;
            term *= -x * (n - 1) / n; 
        }

        return sum;
    }

    static double ApproximateCos(double x, double epsilon)
    {
        double sum = 0;
        double term = 1;
        int n = 0;

        while (Math.Abs(term) >= epsilon)
        {
            sum += term;
            n++;
            term *= -x * x / ((2 * n - 1) * (2 * n)); 
        }

        return sum;
    }
}
