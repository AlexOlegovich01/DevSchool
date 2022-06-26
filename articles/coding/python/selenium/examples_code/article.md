# Приемы работы в Selenium

Здесь будем рассматривать различные приемы работы при парсинге сайтов. Статья будет постоянно пополняться.

### Скроллинг

```python
from selenium.webdriver.common.keys import Keys
# Фрагмент кода
scroll=driver.find_element_by_xpath("//*")
for i in range(100):
		scroll.send_keys(Keys.DOWN)
		time.sleep(1/60)
```

### Выводим отловленную ошибку в консоль

```python
import traceback
try:
	print(qwerty)
except:
	print(traceback.format_exc())
```