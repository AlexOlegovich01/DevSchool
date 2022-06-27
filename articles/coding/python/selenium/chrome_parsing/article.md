# Парсинг и настройки Chromedriver

На начальном этапе отличий немного, но есть на что обратить внимание.

```python
# Вместо
options=webdriver.FirefoxOptions()
# Будет так
options=webdriver.ChromeOptions()
```
И
```python
# Вместо
options.set_preference("option")
# Будет так
options.add_argument("option")
```

Далее перечислим настройки для Chromedriver. Список всех настроек можно найти [здесь](https://peter.sh/experiments/chromium-command-line-switches/).

```python
options.add_argument("headless") # запускает в фоновом режиме
options.add_argument('log-level=3') # меньше мусора в консоли
options.add_argument("user-agent = юзерагент") # меняет юзерагент
```

[:rewind:**Вернуться назад**](../../../../../README.md)