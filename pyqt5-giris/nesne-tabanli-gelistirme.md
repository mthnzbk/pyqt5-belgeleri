# Nesne Tabanlı Geliştirme

Yukarıda örneklerini verdiğimiz şekilde, PyQt5 ile prosedür tabanlı \(yordamsal\) programlama ilkelerine uygun bir geliştirme sürecini takip edebilirsiniz. Ancak hem kullanışlılık açısından, hem de internet üzerinde bulacağınız örnek programların yapısı nedeniyle prosedür tabanlı programlama yerine nesneye yönelik programlama tarzını benimsemenizi tavsiye ederim.

Bir örnek verelim.

Bildiğiniz gibi, PyQt5’te boş bir pencereyi şu kodlarla oluşturuyoruz:

```python
from PyQt5.QtWidgets import *
import sys

uygulama = QApplication(sys.argv)
pencere = QWidget()
pencere.show()

uygulama.exec_()
```

Burada programımız, karşısına çıkan kodları belli bir prosedürü takip ederek tek tek çalıştırıyor. Ancak internet üzerinde veya başka kaynaklarda bu şekilde yazılmış kod pek göremezsiniz. Hem daha kullanışlı olması, hem de kodların bakımını kolaylaştırması nedeniyle grafik arayüz tasarlanırken genellikle nesneye yönelik programlama tarzını takip etmek çok daha mantıklı olacaktır. Dolayısıyla yukarıdaki kodları şu şekilde yazabiliriz:

```python
from PyQt5.QtWidgets import *
import sys

class YeniPencere(QWidget):
    def __init__(self):
        QWidget.__init__(self)

uygulama = QApplication(sys.argv)
pencere = YeniPencere()
pencere.show()
uygulama.exec_()
```

Eğer taban sınıfı \(QWidget\) iki kez yazmak istemiyorsanız super\(\) fonksiyonundan yararlanabilirsiniz:

```python
from PyQt5.QtWidgets import *
import sys

class YeniPencere(QWidget):
    def __init__(self):
        super(YeniPencere, self).__init__()

uygulama = QApplication(sys.argv)
pencere = YeniPencere()
pencere.show()
uygulama.exec_()
```

Hatta, Python3 ile gelen yeni bir özellikten yararlanarak, ne taban sınıfı, ne de sınıf adını iki kez belirtmeyi tercih edebilirsiniz:

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

Bu şekilde, aynı şeyleri tekrar tekrar yazma zahmetinden kurtulmanın yanısıra, sınıf adında veya miras alınan taban sınıfta bir değişiklik yapmanız gerektiğinde **init**\(\) metodunun içeriğini de uygun bir şekilde değiştirme derdini bertaraf etmiş olursunuz.

