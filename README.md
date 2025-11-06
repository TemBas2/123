using System;
using System.IO;
using System.Text;

class Program
{
    static void Main()
    {
        string filePath = @"\\10.5.6.2\студент\ИСП-32КО\Овсепян Исмаилов\input.txt";
        
        try
        {
            // Чтение файла
            string text = File.ReadAllText(filePath, Encoding.UTF8);
            
            // Вывод исходного текста
            Console.WriteLine("Исходный текст:");
            Console.WriteLine(text);
            Console.WriteLine();
            
            // Обработка текста
            int firstPlusIndex = text.IndexOf('+');
            if (firstPlusIndex != -1)
            {
                // Заменяем цифры перед первым '+' на '*'
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
            
            // Вывод результата
            Console.WriteLine("Результат:");
            Console.WriteLine(text);
        }
        catch (FileNotFoundException)
        {
            Console.WriteLine($"Файл не найден по пути: {filePath}");
            Console.WriteLine("Убедитесь, что:");
            Console.WriteLine("1. Файл input.txt существует в указанной папке");
            Console.WriteLine("2. Сетевой ресурс доступен");
            Console.WriteLine("3. У вас есть права доступа к файлу");
        }
        catch (UnauthorizedAccessException)
        {
            Console.WriteLine("Ошибка доступа: нет прав для чтения файла");
        }
        catch (IOException ex)
        {
            Console.WriteLine($"Ошибка ввода-вывода: {ex.Message}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Произошла ошибка: {ex.Message}");
        }
        
        Console.WriteLine("\nНажмите любую клавишу для выхода...");
        Console.ReadKey();
    }
}
