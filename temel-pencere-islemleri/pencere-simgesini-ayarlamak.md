# Pencere Simgesini Ayarlamak

## Pencere Simgesini Ayarlamak

Şimdi de geliştirdiğimiz uygulamamıza pencere simgesi ekleyelim. Çok basit:

```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import QIcon
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.resize(640, 480)
        self.move(300, 300)
        self.setWindowTitle("Pencere Uygulaması")
        self.setWindowIcon(QIcon("pencere_simgesi.png"))

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Burada iki yeni bilgiyle karşılaştık. setWindowIcon\(\) methodu ve QIcon\(\) sınıfı. setWindowIcon\(\) methodu argüman olarak QIcon\(\) nesnesi alır. QIcon\(\) sınıfı da adı argüman olarak verilen simge dosyasını yükler ve PyQt'nin kullanabileceği hale getirir. setWindowIcon\(\) methodu da aldığı bu argümanla pencere simgesi olarak neyin belirlendiğini bu QIcon\(\) nesnesi yardımıyla anlar ve pencere çubuğuna çizer. Eğer biz QIcon\(\) sınıfını kullanmadan doğrudan setWindowIcon\(\) methoduna simge dosyasının adını verirsek PyQt bize hata yaptığımızı gösterecektir.

> **Note** Qt 5x sürümüyle beraber pencere araçlarını QtWidgets paketi altında toplamıştır. QtGui paketinde ise QIcon gibi grafik arayüze etki eden sınıflar olduğu gibi bırakılmıştır.

> **Warning** Kullandığınız GNU/Linux dağıtımının tema ayarları nedeniyle pencere simgelerini göremiyor olabilirsiniz. Örneğin Ubuntu GNU/Linux dağıtımında hiçbir programın simgesi pencere üzerinde görünmez.

## Pencere Özelliklerini Sorgulamak

Yukarıda anlatılan belli başlı methodlarla bir pencerede yapılan en temel düzenlemeleri öğrendik. Şimdi de yeri geldiğinde kullanacağımız pencerenin özelliklerini sorgulayan belli başlı methodları görelim.

Bir ekranın boyutunu, ekrandaki konumunu nasıl ayarlayacağımızı öğrendik. Eğer istediğimiz bunları ayarlamaktan ziyade sorgulamaksa şu methodlardan yararlanırız:

```python
height() #Yükseklik
width() #Genişlik
x() #X düzlemi
y() #Y düzlemi
```

Bu metotların nasıl kullanıldığını ve ne işe yaradığını göstermek için şöyle bir örnek verebiliriz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()

        print("Pencere genişliği: {}".format(self.width()))
        print("Pencere yüksekliği: {}".format(self.height()))
        print("Pencerenin x düzelemdeki yeri: {}".format(self.x()))
        print("Pencerenin y düzelemdeki yeri: {}".format(self.y()))

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Tabii siz PyQt5 de geliştikçe print\(\) fonksiyonu dışında pencere ekranında da gösterebilecek bilgiye sahip olacaksınız.

Bir pencerenin başlığını ayarlamak için setWindowTitle\(\) adlı bir methoddan yararlanabileceğimizi öğrenmiştik. Eğer amacımız başlık belirlemek değil de, o andaki mevcut başlığın ne olduğunu sorgulamak ise windowTitle\(\) adlı bir metottan yararlanabiliriz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()

        print("Pencere başlığı: {}".format(self.windowTitle()))


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Böylece temel pencere metotlarını öğrenmiş olduk. En başta da dediğimiz gibi, bu metotlar bütün pencere sınıflarında ortaktır.

