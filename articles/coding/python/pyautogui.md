# PyAutoGUI

Данная библиотека автоматизирует некоторые процессы пользователя такие как ввод с клавиатуры, создание скриншотов и так далее.

Установка

```
pip install pyautogui
```

Базовые возможности

```python
pyautogui.size() # размер экрана
pyautogui.position() # Положение курсора мыши
pyautogui.moveTo(x, y) # Перемещает курсор в заданные координаты
pyautogui.click() # Клик мыши
pyautogui.click(x, y) # Перейти в заданные координаты и кликнуть
pyautogui.moveTo(x, y) # Перемещает курсор относительно его положения
pyautogui.doubleClick() # Двойной клик
pyautogui.write('Hello world!', interval=0.25) # Пишет заданный текст. duration - время печати.
pyautogui.press('esc') # Нажимает заданную кнопку
pyautogui.hotkey('ctrl', 'c') # Горячая клавиша
pyautogui.onScreen(x, y) # Возвращает True, если курсор находится в заданном положении.
pyautogui.PAUSE = 2.5 # Аналог time.sleep(). В данном случае указывается в секундах.
pyautogui.FAILSAFE = True # При перемещении мыши может возникнуть ошибка
pyautogui.screenshot("Название файла и директория") # Скриншот
```