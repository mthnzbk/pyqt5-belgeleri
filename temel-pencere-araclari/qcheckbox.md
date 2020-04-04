# QCheckBox

Onay butonu, yani QCheckBox pencere aracı, QRadioButton ile hemen hemen aynı bir sınıftır. QRadioButton'dan ayrılan tarafı şekli karedir ve birden fazla seçim yapılacak durumlarda kullanılır. Yalnız bu pencere aracını gruplayan bir sınıf yoktur. Yani QButtonGroup ile seçili QRadioButton'u aldığınız gibi QCheckBox\(lar\)ı alamazsınız. Tabii ki QButtonGroup'u QCheckBox ile kullanabilirsiniz, ama seçim yapmaya kalktığınızda sadece bir tanesinin seçilebileceğini göreceksiniz. Eğer bir çok QCheckBox pencere aracı kullanırsanız hangilerinin seçili olduğunu tek tek kontrol ederek öğrenmek zorundasınız. Kullanımına gelince:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)
        self.checkbox1 = QCheckBox(self)
        self.checkbox1.setText("Ev")
        self.checkbox2  = QCheckBox(self)
        self.checkbox2.setText("Araba")
        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.checkbox1)
        self.layout.addWidget(self.checkbox2)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.hangiButon)

    def hangiButon(self):
        if self.checkbox1.isChecked():
            print(self.checkbox1.text())
        if self.checkbox2.isChecked():
            print(self.checkbox2.text())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Oldukça basit...

