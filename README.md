using System;
using System.IO;
using System.Text;

class Program
{
    static void Main()
    {
        // Пробуем разные возможные расположения файла
        string[] possiblePaths = {
            @"\\10.5.6.2\студент\ИСП-32КО\Овсепян Исмаилов\input.txt", // Ваш сетевой путь
            "input.txt",
            @"..\..\..\input.txt", // Для структуры папок Visual Studio
            Path.Combine(Environment.CurrentDirectory, "input.txt"),
            Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "input.txt")
        };
        
        string text = "";
        string usedPath = "";
        
        foreach (string path in possiblePaths)
        {
            try
            {
                if (File.Exists(path))
                {
                    text = File.ReadAllText(path, Encoding.UTF8);
                    usedPath = Path.GetFullPath(path);
                    break;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Ошибка при доступе к {path}: {ex.Message}");
                continue;
            }
        }
        
        if (string.IsNullOrEmpty(text))
        {
            Console.WriteLine("Файл input.txt не найден!");
            Console.WriteLine("Проверьте следующие расположения:");
            foreach (string path in possiblePaths)
            {
                Console.WriteLine($"  {Path.GetFullPath(path)}");
            }
            Console.WriteLine("\nУбедитесь, что:");
            Console.WriteLine("1. Сетевой ресурс доступен");
            Console.WriteLine("2. У вас есть права доступа к папке");
            Console.WriteLine("3. Файл input.txt существует в указанной папке");
            return;
        }
        
        Console.WriteLine($"Файл найден: {usedPath}");
        Console.WriteLine("\nИсходный текст:");
        Console.WriteLine(text);
        
        // Обработка текста
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
        
        // Пауза для просмотра результата
        Console.WriteLine("\nНажмите любую клавишу для выхода...");
        Console.ReadKey();
    }
}
