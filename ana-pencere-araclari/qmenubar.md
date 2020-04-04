# QMenuBar

QMenuBar ile menülerden oluşan bir menü çubuğu oluştururuz. Menüler QMenu sınıfı ile oluşturulur. Menülerde bulunan ögeler de Aksiyon adı verilen QAction sınıfı ile oluşturulur. İsterseniz öncelikle QMenuBar pencere aracımızı, penceremize yerleştirelim:

```python
from PyQt5.QtWidgets import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.menuBar = QMenuBar(self)
        self.setMenuBar(self.menuBar)


uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

En sade şekliyle bir QMainWindow'a QMenuBar bu şekilde eklenir. Unutmayın ki; QMainWindow, özelliği nedeniyle kendi içerisinde bazı pencere araçları için yer ayrılmış bir pencere aracıdır. Bir QMainWindow'a QPushButton gibi pencere araçları eklemek istiyorsanız öncelikle bir QWidget pencere aracını tanımlayıp setCentralWidget\(\) methodu ile QMainWindow'a tanıtmalısınız. Aynı Şekilde QMenuBar da QMainWindow'un üst kısmı için ayarlandığı için eklediğimiz QMenuBar üst kısımda görülecektir. Görüldüğü üzere bu pencere aracını da QMainWindow'un setMenuBar\(\) methodu ile tanıttık. Tabii bu haliyle menü çubuğunu görmek mümkün değil. Bu yüzden menu çubuğuna QMenu ya da QAction eklememiz gerekir.

