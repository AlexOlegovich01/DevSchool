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
pyautogui.moveTo(x, y,duration=секунд) # Перемещает курсор в заданные координаты
pyautogui.click() # Клик мыши
pyautogui.click(x, y,duration=секунд) # Перейти в заданные координаты и кликнуть
pyautogui.doubleClick() # Двойной клик
pyautogui.write('Hello world!', interval=0.25) # Пишет заданный текст. duration - время печати.
pyautogui.press('esc') # Нажимает заданную кнопку
pyautogui.hotkey('ctrl', 'c') # Горячая клавиша
pyautogui.onScreen(x, y) # Возвращает True, если курсор находится в заданном положении.
pyautogui.PAUSE = 2.5 # Аналог time.sleep(). В данном случае указывается в секундах.
pyautogui.FAILSAFE = True # При перемещении мыши может возникнуть ошибка
pyautogui.screenshot("Название файла и директория") # Скриншот
pyautogui.dragTo(x, y,duration=секунд) # Зажимает и перемещает курсор в заданные координаты
pyautogui.rightClick(x, y,duration=секунд)
pyautogui.middleClick(x, y,duration=секунд)
pyautogui.moveTo(x, y,duration=секунд)
pyautogui.scroll(число) # Скроллинг. Если число положительное, скролл вверх.
```

Получить весь список клавиш можно так

```python
print(pyautogui.KEYBOARD_KEYS)
```

Для вызова контекстных окон

```python
pyautogui.alert(text='', title='', button='OK')
pyautogui.confirm(text='', title='', button=['but1','but2'])
pyautogui.prompt(text='', title='' , default='')
pyautogui.password(text='', title='' , default='',mask='*') # Пароль
```

Библиотека поддерживает распознавание изображений. Это может быть полезно в следующем случае... Допустим, нужно кликнуть на кнопку отправки сообщения, но постоянно высчитывать координаты - не вариант. Можно сделать скрин этой кнопки и распознать его с помощью программы.

```python
scr=pa.locateCenterOnScreen('Screenshot_3.png') # Получить картинку и ее центр координат
pa.moveTo(scr[0],scr[1],duration=3) # В данном примере перемещает мышь к центру картинки, если находит ее.
```

Так же можно передать параметр confidence=число от 0 до 1 - это точность.