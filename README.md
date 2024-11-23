## Отчет по лабораторной работе № 2

#### № группы: `ПМ-2402`

#### Выполнила: `Трофимова Виктория Алексеевна`

#### Вариант: `26`

### Cодержание:

- [Постановка задачи](#1-постановка-задачи)
- [Входные и выходные данные](#2-входные-и-выходные-данные)
- [Математическая модель](#25-математическая-модель).
- [Выбор структуры данных](#3-выбор-структуры-данных)
- [Алгоритм](#4-алгоритм)
- [Программа](#5-программа)
- [Анализ правильности решения](#6-анализ-правильности-решения)

### 1. Постановка задачи

Напишите программу на Java, которая выполняет следующие действия
с двумерным массивом строк, представляющих даты:
1. Считывает с консоли размеры массива N и M, затем элементы
массива размером N × M (каждый элемент — дата в формате
«dd.MM.yyyy HH:mm»).
2. Сортирует строки массива по возрастанию дат. Если даты равны,
сортирует по возрастанию времени, если время указано.
3. Находит и выводит самую раннюю и самую позднюю дату в массиве.
4. Выводит элементы массива, форматируя даты в виде «yyyy-MMdd».
5. Добавляет к каждой дате один день и выводит обновлённый массив.
#### Подробное описание задачи

- Программа должна запрашивать у пользователя количество строк и столбцов двумерного массива.
- Затем пользователь вводит даты для каждой ячейки массива.
- Программа должна разобрать введенные строки в массивы компонентов дат (день, месяц, год, час, минута).
- Далее выполняется сортировка массива дат по возрастанию с учетом всех компонентов (год, месяц, день, час, минута).
- После выводится отсортированный массив, а также минимальная и максимальная дата.
- Далее выводятся все даты в формате `yyyy-MM-dd`.
-  В конце программа добавляет 1 день к каждой дате и выводит полученный массив.

### 2. Входные и выходные данные

#### Входные данные:
|                | Тип              | min значение     | max значение     |
|----------------|------------------|------------------|------------------|
| N (Число 1)    | Целое число      |1                 | 10^9             |
| M (Число 2)    | Целое число      |1                 | 10^9             |
| mass[i][j]     | Строка           |"01.01.0000 00:00"|"31.12.9999 23:59"|

#### Выходные данные:
Отсортированный массив дат   
Самая ранняя дата
Самая поздняя дата                     
Массив дат в формате `yyyy-MM-dd`      
Массив с датами, увеличенными на 1 день

### 2,5. Математическая модель

#### 1. Заполнение массива строк:
- Создается двумерный массив `mass` размером N*M, где N — количество строк (рядов), а M — количество столбцов.
- В каждом элементе этого массива хранится строка, представляющая дату в формате "dd.MM.yyyy HH:mm".
  
  Ввод для каждой ячейки:
  - Дата вводится пользователем с клавиатуры для каждой ячейки массива, и сохраняется в строковом формате.

#### 2. Разбиение даты на компоненты:
- Создается трехмерный массив `mass1`, который имеет размеры N * M * 5, где:
  - N — количество строк,
  - M — количество столбцов,
  - 5 — количество компонентов для каждой даты (день, месяц, год, час, минута).
  
- Для каждого элемента из массива `mass` извлекаются компоненты даты:
  - День (первая и вторая цифры, символы на позиции 0 и 1).
  - Месяц (третья и четвертая цифры, символы на позиции 3 и 4).
  - Год (состоящий из 4 цифр, символы на позиции 6-9).
  - Час (символы на позиции 11-12).
  - Минута (символы на позиции 14-15).

  Каждый компонент даты преобразуется в целое число и сохраняется в массив `mass1`.

#### 3. Сортировка массива по дате и времени:
- Используется сортировка пузырьком для сортировки элементов в строках двумерного массива `mass1`. Сортировка происходит по следующим компонентам:
1. Год (по возрастанию),
2. Месяц (по возрастанию, если год одинаков),
3. День (по возрастанию, если год и месяц одинаковы),
4. Час (по возрастанию, если год, месяц и день одинаковы),
5. Минута (по возрастанию, если предыдущие компоненты одинаковы).

- При этом для каждой строки и для каждого столбца проверяется, нужно ли поменять местами элементы массива. Если условие выполнения сортировки выполняется, то элементы меняются местами.

#### 4. Вывод отсортированного массива:
- После выполнения сортировки выводится отсортированный массив дат в исходном формате (dd.MM.yyyy HH:mm).

#### 5. Поиск минимальной и максимальной даты:
  - Для поиска минимальной и максимальной даты:
  - Перебираются элементы массива, для каждого элемента (в строках и столбцах) производится разбор даты на компоненты (день, месяц, год, час, минута).
  - Каждая часть даты сравнивается с соответствующими частями текущей минимальной и максимальной даты.
  - Если найдена более ранняя дата (для минимальной) или более поздняя дата (для максимальной),то обновляется результат.

#### 6. Перевод дат в формат yyyy-MM-dd:
- Каждый элемент в массиве `mass1` преобразуется в формат "yyyy-MM-dd", где:
  - Год (`mass1[i][j][2]`),
  - Месяц (`mass1[i][j][1]`),
  - День (`mass1[i][j][0]`).

  Каждая дата выводится в строку в формате "yyyy-MM-dd".

#### 7. Добавление 1 дня ко всем датам:
- Для каждой даты добавляется 1 день. В случае, если новый день выходит за пределы месяца (например, 31 января + 1 день = 1 февраля), происходит проверка на количество дней в текущем месяце. Массив `den` используется для хранения количества дней в каждом месяце.
- Если добавление дня приводит к переходу на следующий месяц или год, корректируются месяц и год.
- Все обновленные даты выводятся в исходном формате "dd.MM.yyyy HH:mm".

### 3. Выбор структуры данных
|      | Тип               |
|------|-------------------|
| N    | integer           |
| M    | integer           |
| mass | String[][]        |
| mass1| int[][][]         |
| maxs | String            |
| mins | String            |
| den  | int[]             |

- **N** и **M** - это целые числа, так как они представляют размеры матрицы (количество рядов и столбцов соответственно).
- **mass** - двумерный массив строк (String[][]), так как хранит даты в виде строк.
- **mass1** - трехмерный массив целых чисел (int[][][]), так как используется для хранения разбитых числовых значений дат (день, месяц, год, час, минута).
- **maxs** и **mins** - строки (String), так как хранят дату в исходном формате для поиска самой ранней и самой поздней даты.
- **den** - одномерный массив целых чисел (int[]), так как хранит количество дней в месяцах для расчета корректности даты при добавлении дня.

### 4. Алгоритм

1. Программа начинается с ввода количества строк и столбцов массива.
2. Далее пользователю предлагается ввести даты для каждой ячейки массива в формате `dd.MM.yyyy HH:mm`.
3. Каждая дата разбивается на компоненты (день, месяц, год, час, минута), которые сохраняются в трехмерном массиве.
4. Затем выполняется сортировка массива по компонентам даты. Сортировка происходит по принципу пузырьковой сортировки: начиная с самого младшего компонента (год), до самого старшего (минута).
5. После сортировки выводится отсортированный массив.
6. Программа находит минимальную и максимальную даты.
7. Далее выводятся все даты в формате `yyyy-MM-dd`.
8. Программа добавляет 1 день к каждой дате, проверяя, не выходят ли даты за пределы месяца и года.
9. В конце выводится обновленный массив дат с добавленными днями.

### 5. Программа

```java
import java.io.PrintStream;
import java.util.Scanner;
public class Main {
    public static Scanner in = new Scanner(System.in);
    public static PrintStream out = System.out;
    public static void main(String[] args) {
        // Ввод размеров массива
        System.out.println("Количество рядов:");
        int N = in.nextInt(); // Ввод количества рядов (строк) массива
        System.out.println("Количество столбцов:");
        int M = in.nextInt(); // Ввод количества столбцов массива
        in.nextLine();
        // Ввод строк с датами
        String[][] mass = new String[N][M]; // Создаем двумерный массив строк для хранения дат
        for (int i = 0; i < N; i++) { // Перебираем все строки
            for (int j = 0; j < M; j++) { // Перебираем все столбцы
                System.out.println("Дата в формате dd.MM.yyyy HH:mm:"); // Просим пользователя ввести дату
                mass[i][j] = in.nextLine(); // Считываем строку с датой и записываем в массив
            }
        }

        // Разбиение дат на числовые значения
        int[][][] mass1 = new int[N][M][5]; // Создаем трехмерный массив для хранения компонентов дат
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                // Разбираем строку с датой на компоненты (день, месяц, год, час, минута)
                mass1[i][j][0] = (mass[i][j].charAt(0) - '0') * 10 + (mass[i][j].charAt(1) - '0'); // День
                mass1[i][j][1] = (mass[i][j].charAt(3) - '0') * 10 + (mass[i][j].charAt(4) - '0'); // Месяц
                mass1[i][j][2] = (mass[i][j].charAt(6) - '0') * 1000 + (mass[i][j].charAt(7) - '0') * 100 +
                        (mass[i][j].charAt(8) - '0') * 10 + (mass[i][j].charAt(9) - '0'); // Год
                mass1[i][j][3] = (mass[i][j].charAt(11) - '0') * 10 + (mass[i][j].charAt(12) - '0'); // Час
                mass1[i][j][4] = (mass[i][j].charAt(14) - '0') * 10 + (mass[i][j].charAt(15) - '0'); // Минута
            }
        }

        // Сортировка массива
        // Сортировка массива по дате и времени
        for (int i = 0; i < N; i++) { // Перебираем строки
            for (int k = 0; k < M; k++) {
                for (int j = 0; j < M - 1; j++) { // Сравниваем текущий элемент с каждым последующим
                    boolean x = false; // Флаг, указывающий, нужно ли менять местами элементы

                    // Проверяем, нужно ли поменять местами элементы
                    if (mass1[i][j][2] > mass1[i][j+1][2]) {
                        x = true;
                    } else if (mass1[i][j][2] == mass1[i][j+1][2]) {
                        // Если года одинаковые, проверяем месяц
                        if (mass1[i][j][1] > mass1[i][j+1][1]) {
                            x = true;
                        } else if (mass1[i][j][1] == mass1[i][j+1][1]) {
                            // Если месяц одинаковый, проверяем день
                            if (mass1[i][j][0] > mass1[i][j+1][0]) {
                                x = true;
                            } else if (mass1[i][j][0] == mass1[i][j+1][0]) {
                                // Если день одинаковый, проверяем час
                                if (mass1[i][j][3] > mass1[i][j+1][3]) {
                                    x = true;
                                } else if (mass1[i][j][3] == mass1[i][j+1][3]) {
                                    // Если час одинаковый, проверяем минуту
                                    if (mass1[i][j][4] > mass1[i][j+1][4]) {
                                        x = true;
                                    }
                                }
                            }
                        }
                    }

                    // Если нужно поменять местами, сортируем пузырьком
                    if (x) {
                        String max = mass[i][j];
                        mass[i][j] = mass[i][j+1];
                        mass[i][j+1] = max;
                        int [] max1 = mass1[i][j];
                        mass1[i][j] = mass1[i][j+1];
                        mass1[i][j + 1] = max1;
                    }
                }
            }
        }
        out.println("Отсортированный массив:");
        // Вывод отсортированного массива
        for (int i = 0; i < N; i++) { // Перебираем все строки
            for (int j = 0; j < M; j++) { // Перебираем все столбцы
                out.print(mass[i][j] + " "); // Выводим дату в строку
            }
            out.println(); // Переходим на новую строку после каждого ряда
        }

        // Ввод переменных для поиска минимальной и максимальной даты
        String maxs = mass[0][0];
        String mins = mass[N - 1][M - 1];

        // Поиск самой ранней даты
        for (int i = 0; i < N; i++) {
            int date = mass1[i][0][0];
            int month = mass1[i][0][1];
            int year = mass1[i][0][2];
            int hour = mass1[i][0][3];
            int minute = mass1[i][0][4];

            // Разбираем строку минимальной даты
            int minDate = (mins.charAt(0) - '0') * 10 + (mins.charAt(1) - '0');
            int minMonth = (mins.charAt(3) - '0') * 10 + (mins.charAt(4) - '0');
            int minYear = (mins.charAt(6) - '0') * 1000 + (mins.charAt(7) - '0') * 100 +
                    (mins.charAt(8) - '0') * 10 + (mins.charAt(9) - '0');
            int minHour = (mins.charAt(11) - '0') * 10 + (mins.charAt(12) - '0');
            int minMinute = (mins.charAt(14) - '0') * 10 + (mins.charAt(15) - '0');

            // Если текущая дата меньше минимальной, обновляем минимальную
            if (year < minYear || (year == minYear && month < minMonth) ||
                    (year == minYear && month == minMonth && date < minDate) ||
                    (year == minYear && month == minMonth && date == minDate && hour < minHour) ||
                    (year == minYear && month == minMonth && date == minDate && hour == minHour && minute < minMinute))
                mins = mass[i][0];
        }

        // Поиск самой поздней даты
        for (int i = 0; i < N; i++) {
            int date = mass1[i][M - 1][0];
            int month = mass1[i][M - 1][1];
            int year = mass1[i][M - 1][2];
            int hour = mass1[i][M - 1][3];
            int minute = mass1[i][M - 1][4];

            // Разбираем строку максимальной даты
            int maxDate = (maxs.charAt(0) - '0') * 10 + (maxs.charAt(1) - '0');
            int maxMonth = (maxs.charAt(3) - '0') * 10 + (maxs.charAt(4) - '0');
            int maxYear = (maxs.charAt(6) - '0') * 1000 + (maxs.charAt(7) - '0') * 100 +
                    (maxs.charAt(8) - '0') * 10 + (maxs.charAt(9) - '0');
            int maxHour = (maxs.charAt(11) - '0') * 10 + (maxs.charAt(12) - '0');
            int maxMinute = (maxs.charAt(14) - '0') * 10 + (maxs.charAt(15) - '0');

            // Если текущая дата больше максимальной, обновляем максимальную
            if (year > maxYear || (year == maxYear && month > maxMonth) ||
                    (year == maxYear && month == maxMonth && date > maxDate) ||
                    (year == maxYear && month == maxMonth && date == maxDate && hour > maxHour) ||
                    (year == maxYear && month == maxMonth && date == maxDate && hour == maxHour && minute > maxMinute))
                maxs = mass[i][M - 1];
        }

        out.println("Самая ранняя дата: " + mins);
        out.println("Самая поздняя дата: " + maxs);

        // Вывод дат в формате yyyy-MM-dd
        out.println("Формат yyyy-MM-dd:");
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                out.printf("%04d-%02d-%02d ", mass1[i][j][2], mass1[i][j][1], mass1[i][j][0]);
            }
            out.println();
        }

        // Добавление 1 дня ко всем датам
        out.println("Добавляем 1 день к каждой дате:");
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                // Извлекаем компоненты даты
                int day = mass1[i][j][0];
                int month = mass1[i][j][1];
                int year = mass1[i][j][2];
                int hour = mass1[i][j][3];
                int min = mass1[i][j][4];

                // Массив с количеством дней в месяце (для обычного года)
                int[] den = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

                // Високосный год
                if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0))
                    den[1] = 29; // Для февраля в високосный год устанавливаем 29 дней

                // Добавление 1 дня
                day++;

                // Проверка, не вышли ли за пределы дней месяца
                if (day > den[month - 1]) {  // Если день больше количества дней в месяце
                    day = 1;  // Сбрасываем день на 1
                    month++;  // Переходим к следующему месяцу

                    // Если месяц превышает 12, переходим на следующий год
                    if (month > 12) {
                        month = 1;
                        year++;
                    }
                }

                // Форматируем и обновляем дату
                mass[i][j] = String.format("%02d.%02d.%04d %02d:%02d", day, month, year, hour, min);
            }
        }

        // Выводим обновленные даты
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < M; j++) {
                out.print(mass[i][j] + " ");
            }
            out.println();
        }
    }
}
```
### 6. Анализ правильности решения


1. Проверим работу программы с 1 датой

    - **Input**:
        ```
        Количество рядов:
        1
        Количество столбцов:
        1
        Дата в формате dd.MM.yyyy HH:mm:
        12.09.2004 23:45
        ```

    - **Output**:
        ```
        Отсортированный массив:
        12.09.2004 23:45 
        Самая ранняя дата: 12.09.2004 23:45
        Самая поздняя дата: 12.09.2004 23:45
        Формат yyyy-MM-dd:
        2004-09-12 
        Добавляем 1 день к каждой дате:
        13.09.2004 23:45
        ```

2. Проверим работу программы с несколькими датами
    - **Input**:
        ```
        Количество рядов:
        2
        Количество столбцов:
        3
        Дата в формате dd.MM.yyyy HH:mm:
        12.09.2093 12:34
        Дата в формате dd.MM.yyyy HH:mm:
        09.09.3812 12:35
        Дата в формате dd.MM.yyyy HH:mm:
        01.01.2031 17:54
        Дата в формате dd.MM.yyyy HH:mm:
        01.03.0009 12:56
        Дата в формате dd.MM.yyyy HH:mm:
        08.09.2093 17:09
        Дата в формате dd.MM.yyyy HH:mm:
        01.10.2004 12:33
        ```

    - **Output**:
        ```
        Отсортированный массив:
        01.01.2031 17:54 12.09.2093 12:34 09.09.3812 12:35 
        01.03.0009 12:56 01.10.2004 12:33 08.09.2093 17:09 
        Самая ранняя дата: 01.03.0009 12:56
        Самая поздняя дата: 09.09.3812 12:35
        Формат yyyy-MM-dd:
        2031-01-01 2093-09-12 3812-09-09 
        0009-03-01 2004-10-01 2093-09-08 
        Добавляем 1 день к каждой дате:
        02.01.2031 17:54 13.09.2093 12:34 10.09.3812 12:35 
        02.03.0009 12:56 02.10.2004 12:33 09.09.2093 17:09
        ```

3. Проверим, работает ли сортировка по времени

    - **Input**:
        ```
        Количество рядов:
        1
        Количество столбцов:
        3
        Дата в формате dd.MM.yyyy HH:mm:
        12.09.1111 12:09
        Дата в формате dd.MM.yyyy HH:mm:
        12.09.1111 12:10
        Дата в формате dd.MM.yyyy HH:mm:
        12.09.1111 11:59
        ```

    - **Output**:
        ```
        Отсортированный массив:
        12.09.1111 11:59 12.09.1111 12:09 12.09.1111 12:10 
        Самая ранняя дата: 12.09.1111 11:59
        Самая поздняя дата: 12.09.1111 12:10
        Формат yyyy-MM-dd:
        1111-09-12 1111-09-12 1111-09-12 
        Добавляем 1 день к каждой дате:
        13.09.1111 11:59 13.09.1111 12:09 13.09.1111 12:10
        ```

4. Рассмотрим случай, когда месяц и год должны измениться(последний день месяца/года)

    - **Input**:
        ```
        Количество рядов:
        1
        Количество столбцов:
        2
        Дата в формате dd.MM.yyyy HH:mm:
        31.12.2000 12:32
        Дата в формате dd.MM.yyyy HH:mm:
        31.01.1999 12:09
        ```

    - **Output**:
        ```
       Отсортированный массив:
        31.01.1999 12:09 31.12.2000 12:32 
        Самая ранняя дата: 31.01.1999 12:09
        Самая поздняя дата: 31.12.2000 12:32
        Формат yyyy-MM-dd:
        1999-01-31 2000-12-31 
        Добавляем 1 день к каждой дате:
        01.02.1999 12:09 01.01.2001 12:32 
        ```

5. Рассмотри случай с високосным и невисокосным годом

    - **Input**:
        ```
        Количество рядов:
        1
        Количество столбцов:
        2
        Дата в формате dd.MM.yyyy HH:mm:
        28.02.1982 12:32
        Дата в формате dd.MM.yyyy HH:mm:
        28.02.2004 14:33
        ```

    - **Output**:
        ```
        Отсортированный массив:
        28.02.1982 12:32 28.02.2004 14:33 
        Самая ранняя дата: 28.02.1982 12:32
        Самая поздняя дата: 28.02.2004 14:33
        Формат yyyy-MM-dd:
        1982-02-28 2004-02-28 
        Добавляем 1 день к каждой дате:
        01.03.1982 12:32 29.02.2004 14:33 
        ```


