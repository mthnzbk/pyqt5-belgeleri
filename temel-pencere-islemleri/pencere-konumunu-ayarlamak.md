# Pencere Konumunu Ayarlamak

## Pencere Konumunu Ayarlamak

Oluşturduğumuz uygulamayı her çalıştırdığımız da penceremizin ekranda farklı yerlerde çizildiğini fark etmiş olabilirsiniz. Yazdığınız bir uygulamanın ekrann neresinde açılacağını da belirlemek istiyorsanız move\(\) methodundan faydalanabilirsiniz:

```python
from PyQt5.QtWidgets import *
from PyQt5.QtCore import QPoint
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.resize(640, 480)
        self.move(300, 300)
        # veya
        self.move(QPoint(300, 300))

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Burada yazdığımız self.move\(300, 300\) satırı, pencerenin X düzleminde\(soldan sağa\) 300px, Y düzleminde ise \(yukarıdan aşağıya\) 400px den itibaren görüntülenmesini sağlıyor. move\(\) methodu da resize\(\) methodunda olduğu gibi iki ayrı integer değer ya da resize\(\) methodunun aldığı QSize\(\) sınıfı gibi bir sınıfı argüman olarak alabilir. Bu da örnek kodda görüldüğü üzere QPoint\(\) sınıfıdır. Bu sınıf da QtCore paketinin içinde bulunmaktadır.

## Pencere Başlığını Ayarlamak

Yazdığımız uygulamaya verdiğimiz adın ne olduğunu başlık çubuğunda mutlaka görmek isteriz değil mi? QDialog olsun, QWidget olsun, QMainWindow olsun, bu tarz pencere sınıflarında ortak olan bir method olan setWindowTitle\(\) methoduna verdiğimiz karakter dizisinden oluşan argüman ile pencere başlığımızı ayarlayabiliriz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.resize(640, 480)
        self.move(300, 300)
        self.setWindowTitle("Pencere Uygulaması")

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Gayet basit değil mi? methodun adından da anlaşıldığı üzere\(Window=Pencere, Title=Başlık\) girdiğimiz karakter dizisi ile pencere başlığımızı belirledik.

