# Uyarı Mesajı Kutusu

Hazır olarak gelen mesaj kutularından olan uyarı mesajı kutusu QMessageBox sınıfının warning\(\) statik methoduyla oluşturulur. information\(\) ile aynı parametreler girilir.

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

        self.uyariMenusu = QMenu(self)
        self.uyariMenusu.setTitle("Uyarı")
        self.menubar.addMenu(self.uyariMenusu)

        self.uyariAksiyonu = QAction(self)
        self.uyariAksiyonu.setText("Uyarı")
        self.uyariMenusu.addAction(self.uyariAksiyonu)

        self.uyariAksiyonu.triggered.connect(self.uyariKutusuGoster)

    def uyariKutusuGoster(self):
        QMessageBox.warning(self, "Başlık", "Kullanıcı için uyarı içeren mesaj kutusu.")


uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırıp denediğinizde "Başlık" adında başlığa sahip bir uyarı mesaj kutusu açılacaktır. Çok basit ve açıklayıcı metin uzunluğuna göre yer kaplayan bir arayüz göreceksiniz. information\(\) da olduğu gibi warning\(\) de ek parametre alarak mesaj kutunuzda arzunuza göre ek butonlar göstermenize olanak tanır. [Bu](http://doc.qt.io/qt-5/qmessagebox.html#StandardButton-enum) adresden edineceğiniz bilgiyle hangi butonları koyabileceğinizi öğrenebilirsiniz. Python da yazarken de :: karakterini nokta \(.\) ile değiştirmeniz gerekiyor. NoButton ifadesi herhangi bir buton göstermemesi gerekirken benim bilgisayarımda **Tamam** butonu yine de görünmektedir. Ekleyeceğiniz birden fazla buton varsa her birini \| karakteriyle ayırmalısınız. Örnek:

```python
QMessageBox.warning(self, "Başlık", "Kullanıcı için uyarı içeren mesaj kutusu.",
                  QMessageBox.Close|QMessageBox.Help)
```

