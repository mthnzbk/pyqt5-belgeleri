# QVBoxLayout

Bu yerleştirme aracı eklediğiniz pencere araçlarını dikey olarak yerleştirir:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

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


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Örnek kodda dört adet butonu dikey olarak yerleştirdik. Bunu sağlayan QVBoxLayout sınıfının addWidget\(\) methodudur. Gördüğünüz gibi oldukça basit bir kullanımı var.

Biz yukarıdaki örnekte QVBoxLayout sınıfının ilk parametresini **self** yaparak ebeveyninin QWidget olduğunu belirttik. Bunun yerine QWidget'in setLayout\(\) methodu ile QVBoxLayout sınıfına hiç parametre girmeden de tanıtabiliriz. Ayrıca bu method ile self.layout ile örneğini aldığımız QVBoxLayout yerleştirme aracını da QWidget'e bu pencerenin yerleştirme yöneticisi olduğunu belirtmiş oluyoruz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout()

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

