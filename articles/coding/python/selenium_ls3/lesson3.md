# Полезные настройки. Работа вебдрайвера

Оазберем некоторые настройки для работы нашего парсера.

Внимание! Статья будет со временем пополняться.

```python
from selenium import webdriver
import time
options=webdriver.FirefoxOptions()
#...опции...
driver=webdriver.Firefox(options=options)
try:
	driver.get("https://www.amazon.com/")
	time.sleep(10)
except:
	pass
finally:
	driver.close()
	driver.quit()
```

Разберем некоторые опции. Список будет пополняться.

```python
options.set_preference("dom.webdriver.enabled",False) #отключает режим вебдрайвера
options.set_preference("dom.webnotifications.enabled",False) #отключает уведомления
options.set_preference("media.vilume_scale","0.0") #выключает звук
options.set_preference("general.useragent.override","юзер агент") #подмена юзер агента
options.headless=True #фоновый режим
permissions.default.image 1 #отключить изображения
javascript.enabled=False #отключает js
```

[:rewind:**Вернуться назад**](../../../../README.md)