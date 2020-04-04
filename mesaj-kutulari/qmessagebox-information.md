# Bilgi Mesajı Kutusu

Hazır olarak gelen mesaj kutularından olan bilgi mesajı kutusu QMessageBox sınıfının information\(\) statik methoduyla oluşturulur. information\(\) methoduna parametre olarak about\(\) daki ile aynı parametreler girilir.

```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.menubar = QMenuBar(self)
        self.setMenuBar(self.menubar)

        self.bilgiMenusu = QMenu(self)
        self.bilgiMenusu.setTitle("Bilgi")
        self.menubar.addMenu(self.bilgiMenusu)

        self.bilgiAksiyonu = QAction(self)
        self.bilgiAksiyonu.setText("Bilgi")
        self.bilgiMenusu.addAction(self.bilgiAksiyonu)

        self.bilgiAksiyonu.triggered.connect(self.bilgiKutusuGoster)

    def bilgiKutusuGoster(self):
        QMessageBox.information(self, "Başlık", "Kullanıcı için bilgi içeren mesaj kutusu.")


uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırıp denediğinizde "Başlık" adında başlığa sahip bir mesaj kutusu açılacaktır. Çok basit ve açıklayıcı metin uzunluğuna göre yer kaplayan bir arayüz göreceksiniz. about\(\)'un aksie information\(\) ek parametre alarak mesaj kutunuzda arzunuza göre ek butonlar göstermenize olanak tanır. [Bu](http://doc.qt.io/qt-5/qmessagebox.html#StandardButton-enum) adresden edineceğiniz bilgiyle hangi butonları koyabileceğinizi öğrenebilirsiniz. Python da yazarken de :: karakterini nokta \(.\) ile değiştirmeniz gerekiyor. NoButton ifadesi herhangi bir buton göstermemesi gerekirken benim bilgisayarımda **Tamam** butonu yine de görünmektedir. Ekleyeceğiniz birden fazla buton varsa her birini \| karakteriyle ayırmalısınız. Örnek:

```python
QMessageBox.information(self, "Başlık", "Kullanıcı için bilgi içeren mesaj kutusu.",
                  QMessageBox.Close|QMessageBox.Help)
```

