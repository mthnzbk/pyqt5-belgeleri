# QDialog

QDialog sınıfı da, tıpkı QWidget sınıfı gibi pencere oluşturmak için kullanılabilir. Örneğin:

```python
from PyQt5.QtWidgets import *
import sys

class YeniPencere(QDialog):
    def __init__(self):
        super().__init__()

uygulama = QApplication(sys.argv)
pencere = YeniPencere()
pencere.show()
uygulama.exec_()
```

Gördüğünüz gibi, bu defa QWidget sınıfını değil, QDialog sınıfını miras aldık. Bu kodlar ile oluşturulan pencerenin, görünüş olarak QWidget ile oluşturulan pencereden farklı olduğuna dikkat edin. Bu tür pencerelerde büyütme-küçültme-kapatma düğmeleri standart değildir. Mesela bazı işletim sistemlerinde bir kapatma düğmesi ve bir de ‘bu nedir?’ düğmesi yer alırken, bazı işletim sistemlerinde kapatma ve büyütme düğmeleri, başka işletim sistemlerinde ise sadece kapatma düğmesi bulunur.

PyQt5 de QDialog sınıfı miras alan kullanıma hazır bir takım sınıflar da mevcuttur. Sırası geldiği zaman bunlara da değineceğiz.

