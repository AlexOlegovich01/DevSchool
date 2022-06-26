# Имитация пользователя
Большинство сайтов собирают различную информацию о пользователе. Это может быть IP фдрес, геолокация, user-agent, язык системы, разрешение экрана и так далее. Некоторым сайтам необходима эта информация для гибкой подстройки под пользователя и рекламы, но есть у этого и обратная сторона.

Многие сайты любят пользователей и недолюбливают всяких роботов и всячески мешают им нормально работать. Могут и блокнуть. Абсолютной защиты от такого нет, но в этой статье разберем несколько настроек, чтобы походить на реального пользователя и обмануть браузер.

## user-agent

Для наглядности зайдем на сайт [Headless Detector](https://infosimples.github.io/detect-headless/). Он больше подходит для Chrome, но нам нужен параметр **User Agent**.

Напомню код

```python
from selenium import webdriver
import time
options=webdriver.FirefoxOptions()
#...опции...
driver=webdriver.Firefox(options=options)
try:
	driver.get("https://infosimples.github.io/detect-headless/")
	time.sleep(30)
except:
	pass
finally:
	driver.close()
	driver.quit()
```

Там, где оставлен комментарий *опции*, впишем опцию

```python
options.set_preference("general.useragent.override","юзер агент")
```

Запустим программу и увидим, что напротив User-Agent будет надпись **юзер агент**.

Но с таким юзер-агентом браузеры легко спалят то, что это не от браузера, поэтому рассмотрим библиотеку **fake-useragent**, при помощи которой будем генерировать фейковые юзер-агенты. Для начала ее установим.

```
pip install fake-useragent
```

```python
from fake_useragent import UserAgent
ua = UserAgent()
# Имеются варианты
ua.ie
ua.msie
ua.opera
ua.chrome
ua.google
ua.firefox
ua.ff
ua.random
```

А теперь просто подставляем нужный юзер-агент

```python
options.set_preference("general.useragent.override",ua.opera)
```

## Отключение режима Вебдрайвера

На данный момент для Firefox опция не работает, поэтому дополню статью, когда найду решение.

[:rewind:**Вернуться назад**](../../../../../README.md)