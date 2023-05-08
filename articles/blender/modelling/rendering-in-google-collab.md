# Рендеринг в Google Collab

Этот материал будет полезен тем, кто обладает слабым ПК или встроенной в процессор видеокартой.

## Что нужно сделать?

1. Должен быть аккаунт гугл и диск.
2. Перейти в [Google Collab](https://colab.research.google.com/) и нажать Создать блокнот.
3. Нажать Изменить/Настройки блокнота. Выбрать GPU и поставить галочку напротив Исключить выходные данные кодовой ячейки при сохранении блокнота.
4. Вставить код и нажать на выполнение. Этот код даст информацию о выделенных ресурсах.

```python
import psutil
def get_size(bytes, suffix="B"):
    factor = 1024
    for unit in ["", "K", "M", "G", "T", "P"]:
        if bytes < factor:
            return f"{bytes:.2f}{unit}{suffix}"
        bytes /= factor
print("="*40, "Memory Information", "="*40)
svmem = psutil.virtual_memory()
print(f"Total: {get_size(svmem.total)}") ; print(f"Available: {get_size(svmem.available)}")
print(f"Used: {get_size(svmem.used)}") ; print(f"Percentage: {svmem.percent}%")
```

5. Далее нажать кнопку Код, чтобы добавить следующий блок кода. После, так же запустить. Этот код представит информацию о графическом ускорителе.

```python
! nvidia-smi
```

6. Добавить код. После вставки код преобразуется в форму, где нужно выбрать версию блендера.

```python
#@title Select Blender Version (used for rendering) then execute the cell{ display-mode: "form" }
Blender_Version = 'Blender 2.90' #@param ["Blender 2.79b", "Blender 2.80", "Blender 2.81", "Blender 2.82a", "Blender 2.83.0", "Blender 2.83.3", "Blender 2.90alpha (expiremental)", "Blender 2.90"]

def path_leaf(path):
  import ntpath
  head, tail = ntpath.split(path)
  return tail or ntpath.basename(head)

dl_link = {
    "Blender 2.79b": "https://download.blender.org/release/Blender2.79/blender-2.79b-linux-glibc219-x86_64.tar.bz2",
    "Blender 2.80": "https://download.blender.org/release/Blender2.80/blender-2.80-linux-glibc217-x86_64.tar.bz2",
    "Blender 2.81": "https://download.blender.org/release/Blender2.81/blender-2.81-linux-glibc217-x86_64.tar.bz2",
    "Blender 2.82a": "https://download.blender.org/release/Blender2.82/blender-2.82a-linux64.tar.xz",
    "Blender 2.83.0": "https://download.blender.org/release/Blender2.83/blender-2.83.0-linux64.tar.xz",
    "Blender 2.83.3": "https://download.blender.org/release/Blender2.83/blender-2.83.3-linux64.tar.xz",
    "Blender 2.90alpha (expiremental)": "https://blender.community/5edccfe69c122126f183e2ad/download/5ef635439c12214ca244be6b",
    "Blender 2.90" : "https://download.blender.org/release/Blender2.90/blender-2.90.0-linux64.tar.xz"
}


dl = dl_link[Blender_Version]
filename = path_leaf(dl)

if (Blender_Version == "Blender 2.90alpha (expiremental)"):
  !wget $dl
  !sudo apt-get install p7zip-full
  !7z x $filename
  !mv blender_290bM_e935447a5370-20200625-1857 blender



else:
  !wget -nc $dl
  !mkdir ./blender && tar xf $filename -C ./blender --strip-components 1



!apt install libboost-all-dev
!apt install libgl1-mesa-dev
!apt install libglu1-mesa libsm-dev


data = "import re\n"+\
    "import bpy\n"+\
    "scene = bpy.context.scene\n"+\
    "scene.cycles.device = 'GPU'\n"+\
    "prefs = bpy.context.preferences\n"+\
    "prefs.addons['cycles'].preferences.get_devices()\n"+\
    "cprefs = prefs.addons['cycles'].preferences\n"+\
    "print(cprefs)\n"+\
    "# Attempt to set GPU device types if available\n"+\
    "for compute_device_type in ('CUDA', 'OPENCL', 'NONE'):\n"+\
    "    try:\n"+\
    "        cprefs.compute_device_type = compute_device_type\n"+\
    "        print('Device found',compute_device_type)\n"+\
    "        break\n"+\
    "    except TypeError:\n"+\
    "        pass\n"+\
    "# Enable all CPU and GPU devices\n"+\
    "for device in cprefs.devices:\n"+\
    "    if not re.match('intel', device.name, re.I):\n"+\
    "        print('Activating',device)\n"+\
    "        device.use = True\n"
with open('setgpu.py', 'w') as f:
    f.write(data)
```

7. Добавить код. После его исполнения появится поле, куда нужно ввести пароль аутентификации и ссыока.

```python
from google.colab import drive
drive.mount('/gdrive')
```

После ввести и выполнить

```python
from google.colab import drive
drive.mount('/content/drive')
```

8. Не закрывая Коллаб, перейти в Гугл диск и перенести туда .blend файл, который надо отрендерить. Если в файле есть текстуры, нужно запаковать все текстуры в файл перед отправкой на диск. После отправки, в Диске, нажать ПКМ по файлу и выбрать Открыть доступ. Открыть доступ к файлу для всех, у кого есть ссылка и сменить Читатель на Редактор. Сохранить.
9. Перейти в Коллаб и ввести код ниже. Заменить имя файла и имя картинки. -f - кадр.

```python
!sudo ./blender/blender -P setgpu.py -b '/content/drive/My Drive/имя файла.blend' -o '/content/drive/My Drive/имя картинки.png' -f 1
```

10. Если нужно отрендерить анимацию, то нужно ввести нижележащий код. Обратите внимание на решетки в имени выходного файла - это счетчик. s 1 -e 5 - первый и последний кадр.

```python
!sudo ./blender/blender -P setgpu.py -b '/content/drive/My Drive/untitled.blend' -o '/content/drive/My Drive/untitled_####.png' -s 1 -e 5 -a
```