# QLineEdit

QLineEdit kısaca tek satırlık bir metin düzenleyici pencere aracıdır. Bu tek satırlık alanda girilen metni kesebilir, kopyalayabilir, silebilir ve hatta sürükle bırak işlemi gerçekleştirebilirsiniz. Kullanıcıdan veri almak için en temel pencere aracıdır. Kullanımı oldukça basittir:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        lineEdit = QLineEdit(self)


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

QLineEdit pencere aracını kendi kullanım amacımıza göre özelleştirebiliriz. Örneğin kullanıcı giriş ekranı yazdığımızı varsayalım... Bize gereken şifre giriş kısmında her karakterin yerini yıldız\(\*\) karakteriyle değiştirecek bir QLineEdit pencere aracı:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        lineEdit = QLineEdit(self)
        lineEdit.setEchoMode(QLineEdit.Password)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Böylelikle kullanıcının girdiği karakter dizisinin şifre olduğunu ve bu karakter dizisinin yerine yıldız\(\*\) karakterinin yansıtılmasını sağladık. Zaten Echo da Türkçe'de yansıtmak anlamına gelmektedir.

Eğer biz QLineEdit'in düzenlenebilir özelliğini engellemek istersek tek satırlık bir kod yazmamız yeterli olacaktır:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        lineEdit = QLineEdit(self)
        lineEdit.setText("Bu metin düzenlenemez!")
        lineEdit.setReadOnly(True)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

setReadOnly\(\) methodu sayesinde QLineEdit pencere aracının düzenleme özelliğini engellemiş olduk. Kodu çalıştırdığınızda QLineEdit içerisinde yazan "Bu metin düzenlenemez!" metnini hiç bir şekilde değiştiremeyiz. Tabii yazacağınız ufak bir kodla setReadOnly\(\) methoduna **False** değerini argüman olarak vererek düzenlenebilir yapabilirsiniz.

Şimdi isterseniz QLineEdit pencere aracının önemli iki sinyaline değinelim... Uygulamamıza bir adet QLabel, bir adet de QPushButton ekleyelim:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        layout = QVBoxLayout(self)
        self.lineEdit = QLineEdit(self)
        self.buton = QPushButton(self)
        self.buton.setText("Tamam")
        self.label = QLabel(self)
        self.label.setText("Burası değişecek!")

        layout.addWidget(self.lineEdit)
        layout.addWidget(self.buton)
        layout.addWidget(self.label)

        self.lineEdit.returnPressed.connect(self.rengiDegistir)
        self.lineEdit.textChanged.connect(self.labeleYaz)

    def rengiDegistir(self):
        self.buton.animateClick()
        self.label.setStyleSheet("color:red")

    def labeleYaz(self, metin):
        self.label.setText(metin)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Bu örnekte yeni bilgilerle karşılaşıyoruz. QVBoxLayout\(\) pencere aracı, pencere araçlarını dikey olarak yerleştiren bir sınıftır. Bu pencere aracı her ne kadar QtWidgets paketinde olsa da gözle görünür değildir. Bu sınıfın addWidget\(\) methodu ile QLineEdit'i, QPushButton'u ve QLabel'i alt alta sıralamış olduk. Pencereyi genişlettiğinizde orantılı bir şekilde pencere araçlarının da genişlediğini göreceksiniz.

> **Note** QVBoxLayout gibi pencere yerleştirme sınıflarını ileriki konularda işleyeceğiz.

QLineEdit, içerisindeki karakter dizisi her değiştiğinde textChanged\(\) sinyali çalışır. bu sinyal QLineEdit pencere aracında değişim sonucunda oluşan metni sinyal aracılığı ile yayar. Yukarıdaki örnekte yuva olarak kullandığımız labeleYaz\(\) methodunu yazarken de **metin** adında bir parametre belirledik. textChanged\(\) sinyali ile yayılan karakter dizisi, labeleYaz\(\) methoduna verdiğimiz parametreye argüman olarak arka planda atanır. Sonuç olarak kullanıcı QLineEdit'in içeriğini her değiştirdiğinde labeleYaz\(\) methodu-yuvası da çalışacak ve bu method sayesinde elde edilen karakter dizisi QLabel pencere aracına anlık olarak yazılacaktır.

Klavye tuşunda **Enter** tuşuna bastığınız da ise QLineEdit returnPressed\(\) sinyalini yayar. Bu sinyal her hangi bir veri içermez... Yukarıdaki örnekte biz bu sinyali renginiDegistir\(\) methoduna-yuvasına bağladık. Bu method QLabel içerisindeki metni kırmızı renge boyar. setStyeSheet\(\) methoduna CSS kodu yazılmak suretiyle QLabel içerisindeki metnin özelliklerini düzenler.

QPushButton'un animateClick\(\) methodu da bir slot-yuvadır. Bu method ile QLineEdit içindeyken **Enter** tuşuna basıldığında fare imleciyle bu butona tıklanmış gibi görsel bir olay gösterilmesini sağlarız.

