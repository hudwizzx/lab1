# lab1
GrentsAA2207CV2



using System; 
 
class Program
{
    static int[] arr;

    static void Main()
    {
        int choice = 0;
        while (true)
        {
            Console.WriteLine("1. Создать массив");
            Console.WriteLine("2. Вывести элемент массива");
            Console.WriteLine("3. Сортировка выбором");
            Console.WriteLine("4. Пирамидальная сортировка");
            Console.WriteLine("5. Сортировка пузырькам");
            Console.WriteLine("6. Шейкер сортировка");
            Console.WriteLine("7. Обмен двумя номерами");
            Console.WriteLine("8. Выход");

            Console.Write("Введите свой выбор:: ");
            try
            {
                choice = int.Parse(Console.ReadLine());
            }
            catch
            {
                Console.WriteLine("Неверный выбор!");
                continue;
            }

            switch (choice)
            {
                case 1:
                    CreateArray();
                    break;
                case 2:
                    DisplayArray();
                    break;
                case 3:
                    if (arr == null)
                    {
                        Console.WriteLine("Массив еще не создан!");
                        break;
                    }
                    Algorithms.SelectionSort(arr);
                    Console.WriteLine("Массив отсортирован с помощью сортировки выбором!");
                    break;
                case 4:
                    if (arr == null)
                    {
                        Console.WriteLine("Массив ещё не создан");
                        break;
                    }
                    Algorithms.PyramidSort(arr);
                    Console.WriteLine("Массив отсортирован пирамидальной сортировкой!");
                    break;
                case 5:
                    if (arr == null)
                    {
                        Console.WriteLine("Массив еще не создан!");
                        break;
                    }
                    Algorithms.BubbleSort(arr);
                    Console.WriteLine("Массив отсортирован пузырьковой сортировкой!");
                    break;
                case 6:
                    if (arr == null)
                    {
                        Console.WriteLine("Массив ещё не создан");
                        break;
                    }
                    Algorithms.ShakerSort(arr);
                    Console.WriteLine("Массив отсортирован с помощью сортировки шейкером!");
                    break;
                case 7:
                    if (arr == null)
                    {
                        Console.WriteLine("Массив ещё не создан");
                        break;
                    }
                    ExchangeNumbers();
                    break;
                case 8:
                    return;
                default:
                    Console.WriteLine("Неверный выбор!");
                    break;
            }
        }
    }

    static void CreateArray()
    {
        Console.Write("Введите размер массива:");
        int n = int.Parse(Console.ReadLine());
        arr = new int[n];
        Random r = new Random();
        for (int i = 0; i < arr.Length; i++)
        {
            arr[i] = r.Next(5, 50);
        }
        Console.WriteLine("Массив создан!");
    }

    static void DisplayArray()
    {
        if (arr == null)
        {
            Console.WriteLine("Массив еще не создан!");
            return;
        }
        Console.WriteLine("Элементы массива:");
        foreach (int element in arr)
        {
            Console.Write(element + " ");
        }
        Console.WriteLine();
    }
    static void ExchangeNumbers()
    {
        Console.Write("Введите индекс первого числа: ");
        int i = int.Parse(Console.ReadLine());
        Console.Write("Введите индекс второго числа: ");
        int j = int.Parse(Console.ReadLine());
        if (i >= 0(i >= arr.Length)(j < 0) && j < arr.Length)
        {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            Console.WriteLine("Обмен номерами!");
        }
        else
        {
            Console.WriteLine("Неверный индекс!");
            return;
        }
    }
}

class Algorithms
{
    public static void SelectionSort(int[] arr)
    {
        for (int i = 0; i < arr.Length - 1; i++)
        {
            int minIndex = i;
            for (int j = i + 1; j < arr.Length; j++)
            {
                if (arr[j] < arr[minIndex])
                {
                    minIndex = j;
                }
            }
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
    public static void PyramidSort(int[] arr)
    {
        int n = arr.Length;
        for (int i = n / 2 - 1; i >= 0; i--)
        {
            Pyramidify(arr, n, i);
        }
        for (int i = n - 1; i >= 0; i--)
        {
            int temp = arr[0];
            arr[0] = arr[i];
            arr[i] = temp;
            Pyramidify(arr, i, 0);
        }
    }

    private static void Pyramidify(int[] arr, int n, int i)
    {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        if (left < n && arr[left] > arr[largest])
        {
            largest = left;
        }
        if (right < n && arr[right] > arr[largest])
        {
            largest = right;
        }
        if (largest != i)
        {
            int temp = arr[i];
            arr[i] = arr[largest];
            arr[largest] = temp;
            Pyramidify(arr, n, largest);
        }
    }

    public static void BubbleSort(int[] arr)
    {
        int n = arr.Length;
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = 0; j < n - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }
        }
    }

    public static void ShakerSort(int[] arr)
    {
        int n = arr.Length;
        int
        left = 0;
        int right = n - 1;
        while (left <= right)
        {
            for (int i = left; i < right; i++)
            {
                if (arr[i] > arr[i + 1])
                {
                    int temp = arr[i];
                    arr[i] = arr[i + 1];
                    arr[i + 1] = temp;
                }
            }
            right--;
            for (int i = right; i > left; i--)
            {
                if (arr[i] < arr[i - 1])
                {
                    int temp = arr[i];
                    arr[i] = arr[i - 1];
                    arr[i - 1] = temp;
                }
            }
            left++;
        }
    }
}
