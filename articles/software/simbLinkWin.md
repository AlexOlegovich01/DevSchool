# Символьные ссылки в Windows

Символьные ссылки бывают полезны в многих ситуациях, например, если нужно перенести программы с системного диска на другой. Простое копирование тут не поможет.

Для создания символьной ссылки на папку нужно сначала скопировать папку с системного диска на другой. Далее открыть командную строку от имени администратора и ввести команду `mklink /D "СистемныйДиск\Целеваяпапка" "ДругойДиск\ЦелеваяПапка"`. Перед запуском программы удалите с системного диска целевую папку.