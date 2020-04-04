# Hakkında Kutusu

Hazır olarak gelen mesaj kutularından olan hakkında kutusu QMessageBox sınıfının about\(\) statik methoduyla oluşturulur. about\(\) methoduna parametre olarak aboutQt\(\)'ye ek olarak başlık ve açıklayıcı metin girilir.

```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.menubar = QMenuBar(self)
        self.setMenuBar(self.menubar)

        self.hakkindaMenusu = QMenu(self)
        self.hakkindaMenusu.setTitle("Hakkında")
        self.menubar.addMenu(self.hakkindaMenusu)

        self.hakkindaAksiyonu = QAction(self)
        self.hakkindaAksiyonu.setText("Hakkında")
        self.hakkindaMenusu.addAction(self.hakkindaAksiyonu)

        self.hakkindaAksiyonu.triggered.connect(self.hakkindaKutusuGoster)

    def hakkindaKutusuGoster(self):
        QMessageBox.about(self, "Başlık", "Programımız hakkında bilgi içeren mesaj kutusu.")


uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırıp denediğinizde "Başlık" adında başlığa sahip bir mesaj kutusu açılacaktır. Çok basit ve açıklayıcı metin uzunluğuna göre yer kaplayan bir arayüz göreceksiniz. Görünüş size kötü geliyorsa programınıza bir pencere ikonu ekleyerek hakkında mesaj kutusunda görülmesini de sağlarsınız

```python
self.setWindowIcon(QIcon("logo.png"))
```

Ana penceremize ekleyeceğimiz ikon ile daha naif bir hakkında mesaj kutusu elde edebilirsiniz.

