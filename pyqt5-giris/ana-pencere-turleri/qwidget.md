# QWidget

QWidget sınıfı, öteki bütün pencere sınıflarının atasıdır. Öteki bütün pencere sınıfları QWidget sınıfını miras alır. Daha önce verdiğimiz örneklerden de bildiğimiz gibi, bu sınıf yardımıyla, bir pencerenin sahip olması gereken her türlü temel araca ve işleve sahip pencereler oluşturabiliyoruz:

```python
from PyQt5.QtWidgets import *
import sys

class YeniPencere(QWidget):
    def __init__(self):
        super().__init__()

uygulama = QApplication(sys.argv)
pencere = YeniPencere()
pencere.show()
uygulama.exec_()
```

Bu sınıfın oluşturduğu pencereyi, içi bomboş bir dikdörtgen olarak düşünebilirsiniz. Gördüğünüz gibi, QWidget sınıfını miras alarak oluşturduğumuz pencere, bir pencerenin sahip olması gereken, büyütme küçültme düğmesi, kapatma düğmesi, başlık çubuğu gibi araçlara ve kenarından tutup çekildiğinde büyüyüp küçülme, ekran üzerinde fare ile sürüklenerek taşınabilme gibi işlevlere sahip.

