# QListWidget

Bu pencere aracı verilerinizi listelemeye yarayan bir sınıftır. Klasik liste mantığında olduğu gibi ekleme, çıkarma yapabilirsiniz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Bu kod pencereye boş bir QListWidget ve QPushButton çizer. Bir QListWidget'e öge eklemek istersek addItem\(\) methodunu kullanırız:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)
        self.listwidget.addItem("Python")
        self.listwidget.addItem("Ruby")
        self.listwidget.addItem("Go")
        self.listwidget.addItem("Perl")

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Yukarı da dört adet öge ekledik. Kodu çalıştırdığınızda QListWidget'de bu ögelerin listelendiğini görürsünüz. Eğer istersek bu dört ögeyi tek seferde de ekleyebiliriz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)
        self.listwidget.addItems(["Python","Ruby","Go","Perl"])


        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

addItems\(\) methodu liste olarak verilen karakter dizilerini QListWidget'de sırayla sıralayacaktır.

Bir QListWidget deki öge sayısını öğrenmek istersek bu sınıfın count\(\) methodunu kullanırız. Bu method bize kaç adet öge olduğunu integer olarak verir.

QListWidget'deki ögelerden tıklanmış olan ögenin sırasını öğrenmek istersek currentRow\(\) methodunu kullanırız. currentRow\(\) methodu tıklanmış ögenin integer olarak sırasını verir. Yalnız unutmayın ki her zamanki gibi sıranın başında olan öge her zaman sıfırıncı sıradadır...

Eğer ön tanımlı olarak seçili olmasını istediğimiz bir öge varsa da setCurrentRow\(\) methodu kullanılır. Bu method integer değer alır. Bu integer değer de seçili olmasını istediğiniz ögenin QListWidget'teki sırasıdır.

Listelerde bir listenin her hangi bir yerine nasıl veri eklediğimizi biliyorsunuzdur. QListWidget de bu işlem için insertItem\(\) methodu kullanır. İlk parametreye eklenecek ögenin sırası, ikinci parametreye ise ögenin kendisini yazarız:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)
        self.listwidget.addItem("Python")
        self.listwidget.addItem("Ruby")
        self.listwidget.addItem("Go")
        self.listwidget.addItem("Perl")


        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.ekle)

    def ekle(self):
        self.listwidget.insertItem(1, "JavaScript")


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Örnek kodda **Tamam** butonuna basıldığında birinci sıraya **JavaScript** ögesi ekleniyor. Uygulama çalıştığında liste sıralaması şöyle iken:

```python
Ruby
Go
Perl
```

**Tamam** butonuna tıklanınca şöyle olur:

```python
JavaScript
Go
Perl
```

Aynı şekilde birden fazla veriyi liste arasına eklemek isterseniz insertItems\(\) methodunu kullanabilirsiniz.

Öge eklemenin yanı sıra yeri geldiğinde öge de silmemiz gerekir. QListWidget ile öge silmenin yolu takeItem\(\) methodudur. Kullanımı da gayet basit:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)
        self.listwidget.addItem("Python")
        self.listwidget.addItem("Ruby")
        self.listwidget.addItem("Go")
        self.listwidget.addItem("Perl")


        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.sil)


    def sil(self):
        self.listwidget.takeItem(self.listwidget.currentRow())


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

takeItem\(\) methodu parametre olarak verilen ögenin sırasını alır ve bu method çalıştığında sırası belirtilen ögeyi listeden çıkarır. sil\(\) yuvasında ise QListWidget pencere aracında tıklanmış bir öge varsa o ögeyi parametre olarak takeItem\(\) methoduna veriyoruz ve **Tamam** butonuna basılmasıyla seçili ögeyi listeden çıkarıyoruz. Oldukça basit değil mi?

