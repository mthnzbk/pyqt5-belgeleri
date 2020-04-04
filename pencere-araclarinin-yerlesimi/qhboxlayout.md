# QHBoxLayout

Bu yerleştirme aracı ise eklenen pencere araçlarını yatay olarak yerleştirir. Yukarıdaki koddan örnek olarak verelim:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QHBoxLayout()

        self.buton1 = QPushButton(self)
        self.buton1.setText("Bir")
        self.buton2 = QPushButton(self)
        self.buton2.setText("İki")
        self.buton3 = QPushButton(self)
        self.buton3.setText("Üç")
        self.buton4 = QPushButton(self)
        self.buton4.setText("Dört")

        self.layout.addWidget(self.buton1)
        self.layout.addWidget(self.buton2)
        self.layout.addWidget(self.buton3)
        self.layout.addWidget(self.buton4)

        self.setLayout(self.layout)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Gördüğünüz gibi sadece sınıf adını değiştirdik ve pencere araçları yatay olarak yerleştirildi.

