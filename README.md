# Лабораторная работа №3: Массивы и Функции в PHP

## Цель работы
В этой лабораторной работе я освоил работу с массивами в PHP, научился применять различные операции: создание, добавление, удаление, сортировка и поиск. Также я закрепил навыки работы с функциями, включая передачу аргументов, возвращаемые значения и анонимные функции.

## Выполнение заданий

### Задание 1. Работа с массивами

#### 1.1 Подготовка среды
- Убедился, что у меня установлен PHP 8+.
- Создал файл `index3.php`.
- Включил строгую типизацию:

```php
<?php

declare(strict_types=1);
```

#### 1.2 Создание массива транзакций
Создал массив `$transactions`, содержащий банковские транзакции, каждая из которых представлена ассоциативным массивом:

```php
$transactions = [
    [
        "id" => 1,
        "date" => "2019-01-01",
        "amount" => 100.00,
        "description" => "Payment for groceries",
        "merchant" => "SuperMart",
    ],
    [
        "id" => 2,
        "date" => "2020-02-15",
        "amount" => 75.50,
        "description" => "Dinner with friends",
        "merchant" => "Local Restaurant",
    ],
    [
        "id" => 4,
        "date" => "2022-11-22",
        "amount" => 50.00,
        "description" => "Taxi fare",
        "merchant" => "City Taxi",
    ],
];
```

#### 1.3 Вывод списка транзакций
Использовал `foreach` для вывода списка транзакций в HTML-таблице:

```php
    <table border="1" width="100%" cellpadding="5" cellspacing="0">
        <thead>
            <tr>
                <th>ID</th>
                <th>Дата</th>
                <th>Сумма ($)</th>
                <th>Описание</th>
                <th>Получатель</th>
                <th>Дней назад</th>
            </tr>
        </thead>
        <tbody>
        <?php foreach ($transactions as $transaction): 
            $formattedDate = (new DateTime($transaction["date"]))->format("d-m-Y");
            $daysAgo = daysSinceTransaction($transaction["date"]);
        ?>
            <tr>
                <td><?= ((string) $transaction["id"]) ?></td>
                <td><?= ($formattedDate) ?></td>
                <td align="right"><?= number_format($transaction["amount"], 2) ?></td>
                <td><?= ($transaction["description"]) ?></td>
                <td><?= ($transaction["merchant"]) ?></td>
                <td align="center"><?= $daysAgo ?> дней</td>
            </tr>
        <?php endforeach; ?>
        </tbody>
    </table>

    <h3>Общая сумма: <?= number_format(calculateTotalAmount($transactions), 2) ?> $</h3>

</body>
</html>

```

#### 1.4 Реализация функций

- **`calculateTotalAmount(array $transactions): float`** — вычисляет общую сумму транзакций.
- **`findTransactionByDescription(string $descriptionPart)`** — ищет транзакцию по части описания.
- **`findTransactionById(int $id)`** — ищет транзакцию по идентификатору (реализовал через `foreach` и `array_filter`).
- **`daysSinceTransaction(string $date): int`** — вычисляет количество дней с момента транзакции.
- **`addTransaction(int $id, string $date, float $amount, string $description, string $merchant): void`** — добавляет новую транзакцию.

#### 1.5 Сортировка транзакций
- Отсортировал транзакции по дате с использованием `usort()`.
- Отсортировал транзакции по сумме (по убыванию).

### Задание 2. Работа с файловой системой

1. Создал директорию `image` и добавил 20-30 изображений `.jpg`.
2. Создал страницу `index.php`, которая выводит изображения из `image` в виде галереи.

Пример кода для вывода изображений:

```php
<?php
$dir = 'image/'; // Папка с изображениями
$files = scandir($dir);

if ($files === false) {
    die("Ошибка чтения директории.");
}

echo "<table border='1'><tr>";

$col = 0; // Количество колонок в таблице
$maxCols = 5; // Максимальное количество колонок в строке

foreach ($files as $file) {
    if ($file !== '.' && $file !== '..' && preg_match('/\.(jpg|jpeg|png|gif)$/i', $file)) {
        if ($col % $maxCols == 0 && $col != 0) {
            echo "</tr><tr>"; // Начало новой строки после 5 изображений
        }
        echo "<td><img src='$dir$file' width='150' height='100' alt=''></td>";
        $col++;
    }
}
```

## Документация кода
Я задокументировал код с использованием PHPDoc, описав параметры, возвращаемые значения и функциональность.

## Контрольные вопросы
1. Что такое массивы в PHP?
2. Каким образом можно создать массив в PHP?
3. Для чего используется цикл `foreach`?

## Вывод
В ходе лабораторной работы я изучил массивы, функции и работу с файлами в PHP. Реализовал операции управления транзакциями и сортировки данных, а также создал галерею изображений.

