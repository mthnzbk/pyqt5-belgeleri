# Pencere Boyutunu Ayarlamak

PyQt5 ile boş bir pencerenin nasıl oluşturulduğunu öğrendiğimize göre artık bu pencerenin bazı özellikleri üzerinde oynamalar yaparak yolumuza devam edebiliriz. Mesela önceki konularda verdiğimiz kod örneğini çalıştırdığımızda pencerenin boyutunun ön tanımlı değerlere göre oluştuğunu görürüz. Biz bunu istediğimiz şekilde değiştirme imkanına sahibiz. Bakınız:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.resize(640, 480)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Pencere\(\) adını verdiğimiz penceremizin boyutunu resize\(\) methodu aracılığıyla 640px genişliğinde, 480px yüksekliğinde olacak şekilde ayarlıyoruz. Bu resize\(\) methoduna örnekte olduğu gibi ya iki adet integer değer veriyoruz ya da QtCore paketinde bulunan QSize\(\) sınıfını tek argüman olarak atıyoruz:

```python
from PyQt5.QtWidgets import *
from PyQt5.QtCore import QSize
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.resize(QSize(640, 480))

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Oldukça basit... resize methoduna iki ayrı argüman yazmak yerine QSize\(\) sınıfına bu değerleri atayarak QSize\(\) sınıfını tek argüman olarak atayabiliriz. Hangisini tercih edeceğiniz size kalıyor.

