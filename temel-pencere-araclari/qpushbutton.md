# QPushButton

Bir grafik arayüzünün olmazsa olmazlarından biri şüphesiz butonlardır. PyQt de penceremize buton yerleştirmek için QPushButton pencere aracını sağlar. Kullanımı oldukça basit:

```python
from PyQt5.QtWidgets import *
import sys

class ButonluPencere(QWidget):
    def __init__(self):
        super().__init__()
        buton = QPushButton(self)
        buton.setText("Tıklayın!")

uygulama = QApplication(sys.argv)
pencere = ButonluPencere()
pencere.show()
uygulama.exec_()
```

Örnek kodda görüldüğü gibi QLabel pencere aracıyla aynı yazıma sahip. QLabel örneğinde olduğu gibi **self'i** ikinci argüman yapıp QPushButton'un içeriğini ilk parametreye de yazabiliriz. Ancak daha hoş yazım tarzı istiyorsak yukarıdaki gibi olanı tercih etmeniz daha iyi olacaktır:

```python
buton = QPushButton("Tıklayın!", self)
```

Genellikle bir butonu kullanma amacımız butona tıklandığında istenilen bazı işlemleri yapmasıdır. QPushButton da bu işlemi gerçekleştirmenin yolu oldukça kolay ve yazım tarzı da Pythoniktir:

```python
from PyQt5.QtWidgets import *
import sys

class ButonluPencere(QWidget):
    def __init__(self):
        super().__init__()
        buton = QPushButton(self)
        buton.setText("Tıklayın!")

        buton.clicked.connect(self.close)


uygulama = QApplication(sys.argv)
pencere = ButonluPencere()
pencere.show()
uygulama.exec_()
```

Örneği çalıştırıp butona tıklayınız. Butona tıkladığınızda pencerenin kapandığını göreceksiniz. Şimdi bu görevi yapan kodu inceleyelim:

```python
buton.clicked.connect(self.close)
```

Bir PyQt uygulamasında kullanıcının eylemi ya da uygulama da gerçekleşen bir durum değişikliği durumunda pencere araçları çeşitli sinyaller yayar. Örnek kodumuzda kullandığımız QPushButton pencere aracına kullanıcı tıkladığında clicked\(\) adında bir sinyal yayılır. Yayılan sinyali kullanabilmek için de **slot** yani **yuva**ya bağlamamız gerekir. Yuva dediğimiz terim ise bas bayağı bir methoddur. Bu methodu yukarıdaki örnekte olduğu gibi sinyalin connect\(\) methoduna argüman olarak vererek bağlarız. close\(\) methodu QWidget adlı pencere uygulamasını kapatmaya yarar. Siz butona tıkladığınızda bu method çalışacak ve uygulanızı kapatacaktır. Sinyal-yuva kavramı şimdilik kafanızı karıştırmasın. İleriki konularda fazlasıyla kullanacağız ve aklınızda daha iyi yer edecektir.

> **Warning** Sinyal ve yuvayı yazarken parantezleri kulanmayacağımızı unutmayın!

