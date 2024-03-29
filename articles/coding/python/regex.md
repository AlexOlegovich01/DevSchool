# Регулярные выражения

Нужны для углубленного поиска по текстовым данным, а, сочетая с программированием, еще и автоматический поиск.

## Синтаксис

#### Спец символы

|Символ|Описание|Пример использования
|---|---|---
|**.**|Любой символ, кроме переноса строки|К примеру и. будет искать слова, в которых есть буква и и еще один символ.
|**[Мм]**|В данном случае ищет и большую букву м и маленькую, так как регулярные выражения чувствительны к регистру.|---
|**[а-е]**|Диапазон. В данном случае ищет все буквы от а до е. Работает и с числами.|---
|**р$**|Поиск в конце строки. В примере щет букву р, если она в конце строки.|---
|**^П**|Поиск с начала строки. В примере ищет начало строки, начинающееся на букву П.|---
|**/.**|Экранирование. В примере ищет точки.|---
|**[^св]**|Исключение. Ищет все, кроме символов с и в в данном примере.|---
|**\d**|Любая единичная цифра.|---
|**\D**|Исключает цифры|---
|**\s**|Пробелы|---
|**\S**|Исключение пробелов|---
|**\w**|Любая буква|---
|**\W**|Исключение букв|---
|**\b\w\w\w\b**|\b - граница слова. В примере ищет слова из 3х букв.|---
|**\B\w\w\w\B**|\B исключает границу слова. В примере исключает границу слов из 3х букв.|---
|**\b\w{3}\b**|граница слова. В примере ищет слова из 3х букв используя квантификатор.|---
|**р{1,4}**|Ищет символ Р, который повторяется от 1 до 4 раз.|---
|**р***|Ищет символ Р, который повторяется от 0 раз.|---
|**р+**|Ищет символ Р, который повторяется от 1 раза.|---
|**{\s\|-}**|Группировка. В примере ищет или пробел или дефис.|---|---