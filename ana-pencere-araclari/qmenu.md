# QMenu

Menü çubuğuna bir menü eklemek için yapmamız gereken şey çok basit:

```python
self.menu = QMenu(self.menuBar)
self.menu.setTitle("Dosya")
self.menuBar.addMenu(self.menu)
```

self.menu adında bir QMenu nesnesi tanımladık. Menünün adını setTitle\(\) methodu ile "Dosya" olarak belirttik ve QMenuBar'ın addMenu\(\) methodu ile menü çubuğumuza menümüzü ekledik. addMenu\(\) methoduna isterseniz QMenu'yu isterseniz karakter dizisini argüman olarak girerek menü ekleyebilirsiniz:

```python
self.menuBar.addMenu(self.menu)
#ya da
self.menuBar.addMenu("Dosya")
```

Tabii kullanım amacınıza göre menülerin başına simge resmi ekleyebilirsiniz:

```python
self.menuBar.addMenu(QIcon("simge.png"), "Dosya")
```

Alternatif olarak da QMenu sınıfının setIcon\(\) methodunu kullanabiliriz:

```python
self.menu.setIcon(QIcon("simge.png"))
```

QMenu aracında eklediğimiz QAction ögelerinin arasına çizgi ekleyip bir QAction grubunu diğer bir gruptan ayırmak istersek de QMenu sınıfının addSeperator\(\) methodunu gerekli yere yazmamız yeterlidir:

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

        self.menu = QMenu(self.menuBar)
        self.menu.setTitle("Dosya")
        self.menuBar.addMenu(self.menu)
        self.action1 = QAction(self.menu)
        self.action1.setText("Aç")
        self.menu.addAction(self.action1)
        self.menu.addSeparator()
        self.action2 = QAction(self.menu)
        self.action2.setText("Kaydet")
        self.menu.addAction(self.action2)
        self.action3 = QAction(self.menu)
        self.action3.setText("Farklı Kaydet")
        self.menu.addAction(self.action3)

uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Örnek kodu çalıştırdığınızda "Dosya" menüsünde bulunan "Aç" adlı QAction ögesinden sonra diğer QActionlardan ayıran bir çizgi eklendiğini göreceksiniz.

