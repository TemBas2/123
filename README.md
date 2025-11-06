\\10.5.6.2\студент\ИСП-32КО\Овсепян Исмаилов

using System;
using System.IO;
using System.Text;

class Program
{
    static void Main()
    {
        string inputPath = "input.txt";
        string text = File.ReadAllText(inputPath, Encoding.UTF8);
        
        Console.WriteLine("Исходный текст:");
        Console.WriteLine(text);
        
        int firstPlusIndex = text.IndexOf('+');
        if (firstPlusIndex != -1)
        {
            char[] chars = text.ToCharArray();
            for (int i = 0; i < firstPlusIndex; i++)
            {
                if (char.IsDigit(chars[i]))
                {
                    chars[i] = '*';
                }
            }
            text = new string(chars);
        }
        
        Console.WriteLine("\nРезультат:");
        Console.WriteLine(text);
    }
}
