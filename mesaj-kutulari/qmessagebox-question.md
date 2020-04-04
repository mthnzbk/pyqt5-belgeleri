# Sorun Mesajı Kutusu

Hazır olarak gelen mesaj kutularından olan sorun mesajı kutusu QMessageBox sınıfının question\(\) statik methoduyla oluşturulur. critical\(\) ile aynı parametreler girilir.

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

        self.sorunMenusu = QMenu(self)
        self.sorunMenusu.setTitle("Sorun")
        self.menubar.addMenu(self.sorunMenusu)

        self.sorunAksiyonu = QAction(self)
        self.sorunAksiyonu.setText("Sorun")
        self.sorunMenusu.addAction(self.sorunAksiyonu)

        self.sorunAksiyonu.triggered.connect(self.sorunKutusuGoster)

    def sorunKutusuGoster(self):
        QMessageBox.question(self, "Başlık", "Kullanıcı için sorun mesajı içeren mesaj kutusu.")


uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırıp denediğinizde "Başlık" adında başlığa sahip bir sorun mesajı, mesaj kutusu açılacaktır. Çok basit ve açıklayıcı metin uzunluğuna göre yer kaplayan bir arayüz göreceksiniz. [Bu](http://doc.qt.io/qt-5/qmessagebox.html#StandardButton-enum) adresden edineceğiniz bilgiyle hangi butonları koyabileceğinizi öğrenebilirsiniz. Python da yazarken de :: karakterini nokta \(.\) ile değiştirmeniz gerekiyor. NoButton ifadesi herhangi bir buton göstermemesi gerekirken benim bilgisayarımda **Tamam** butonu yine de görünmektedir. Ekleyeceğiniz birden fazla buton varsa her birini \| karakteriyle ayırmalısınız. Örnek:

```python
QMessageBox.question(self, "Başlık", "Kullanıcı için sorun mesajı içeren mesaj kutusu.",
                  QMessageBox.Close|QMessageBox.Help)
```

Sorun mesajı mesaj kutusunda diğerlerinin aksine **Tamam** Butonu yerine **Evet** ve **Hayır** butonları mevcuttur. Özel buton tanımladığınızda bunlar görünmez. Bu durumu göz alarak uygulamanızı geliştiriniz.

Göreceğiniz üzere statik methodların kullanım açısından birbirinden pek bir farkı yok. Gözle görülen tek fark kutumuzun solunda çıkan simgedir. Arka planda ise birbirleri arasında fark yoktur. Ama siz gerekli gördüğünüzde koyduğunuz butonlara ilgili slotları bağlayarak işlev kazandırabilirsiniz. Böylece farkı daha da belirginleştirmiş olursunuz.

