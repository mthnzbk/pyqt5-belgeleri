# QMainWindow

QMainWindow sınıfı, öteki iki sınıfa kıyasla daha ayrıntılı bir pencere yapısı oluşturmamızı sağlar. Bu sınıfı da şu şekilde kullanıyoruz:

```python
from PyQt5.QtWidgets import *
import sys

class YeniPencere(QMainWindow):
    def __init__(self):
        super().__init__()

uygulama = QApplication(sys.argv)
pencere = YeniPencere()
pencere.show()
uygulama.exec_()
```

Boş haliyle belli olmasa da aslında QMainWindow şu yapıya sahip bir pencere oluşturur:

![http://qt-project.org/doc/qt-5.0/qmainwindow.html\#details](https://github.com/mthnzbk/pyqt5-belgelendirmesi/tree/ac3b99083a31c230d378981fac186e01fcfe0f1f/pyqt5-giris/ana-pencere-turleri/images/mainwindowlayout.png)

Gördüğünüz gibi, bu pencerede menü çubuğu **QMenuBar**, araç çubukları **QToolBar**, ayrılabilen pencere araçları **QDockWidget** orta pencere aracı **QWidget** ve durum çubuğu **QStatusBar** için önceden belirlenmiş alanlar var. Dolayısıyla mesela bu pencereye ait metotları kullanarak oluşturacağınız bir durum çubuğu pencerenin alt tarafında kendisine ayrılan konuma yerleşecektir. Tabii bu pencere araçlarını kullanmak sizin kararınıza bağlı olmaktadır.

Yazdığınız programlarda ihtiyacınıza göre bu üç pencereden birini veya birkaçını kullanabilirsiniz.

Temel PyQt5 bilgileri üzerine konuşurken, PyQt5'in mevcut kütüphaneler arasında en güçlü grafik arayüz geliştirme kütüphanelerinden biri olduğunu söylemiştik hatırlarsanız. Gerçekten de PyQt5 aklınıza gelebilecek her türlü grafik arayüzü tasarlamanızı sağlayacak araçlara ve metotlara sahiptir. Mesela biraz önce, farklı sınıfları kullanarak oluşturduğumuz boş pencereleri ele alalım. PyQt5 bize bu boş pencerelerin pek çok niteliği üzerinde değişiklik yapma imkanı verir. PyQt5 ile oluşturduğunuz bir pencere ile neler yapabileceğinizi görmek için bu pencerenin hangi metotlara sahip olduğunu [Qt5 belgelerini](http://doc.qt.io/qt-5/classes.html) inceleyerek kontrol edebilirsiniz.

