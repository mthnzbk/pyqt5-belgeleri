# QStatusBar

QStatusBar, QMainWindow penceresinin en altında yatay şekilde konumlanan bir pencere aracıdır. Bu pencere aracı ile geçici bilgi mesajlarının yanı sıra durum çubuğunun bir kısmını kaplayan pencere araçları içerebilir. Bunlar isteğe göre gizlenebilecek şekilde ayarlanabildiği gibi gizlenemeyen, kalıcı durum mesajları da koyulabilir.

Bir QStatusBar sınıfını QMainWindow'a tanıtmak için bu sınıfın setStatusBar\(\) methodu kullanılır:

```python
from PyQt5.QtWidgets import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.statusBar = QStatusBar(self)
        self.setStatusBar(self.statusBar)
        self.statusBar.showMessage("Merhaba!", 3000)

uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırdığınızda basit bir pencere açılacaktır. Alt kısmında belli-belirsiz bir durum çubuğu olacak ve **Merhaba!** yazısı bu durum çubuğunda 3 saniye kadar gözükecektir. Evet, QStatusBar'ın showMessage\(\) methodu ile durum çubuğumuzda mesaj gösteriyoruz. Gösterilecek süreyi de milisaniye cinsinden giriyoruz. Tabii süre belirtmek zorunda değilsiniz.

Geliştirilen yazılımlarda fare ile bir pencere aracının üzerine gelindiğinde durum çubuğunda geliştiricilerin istediği bir mesaj görünür. Biz de bunu yapmak istersek eğer çok basit bir yolu var. Böylece fazladan kod yazmamız veya takla atmamız gerekmez:

```python
from PyQt5.QtWidgets import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.buton = QPushButton(self.widget)
        self.buton.setText("Buton")
        self.buton.setStatusTip("Fare butonun üzerinde.")

        self.statusBar = QStatusBar(self)
        self.setStatusBar(self.statusBar)

uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Hemen her pencere aracında bulunan setStatusTip\(\) methodu ile QMainWindow'a tanıttığımız QStatusBar pencere aracımıza bilgi mesajı gösterebiliyoruz. Kullanıcı ilgili pencere aracına fare imlecini üstünde tuttuğu sürece gösterilecek bir mesaj belirtmiş olduk.

Konunun başında gizlenebilen ya da kalıcı pencere araçlarını da durum çubuğunda konumlandırabileceğimizi söylemiştik. Eğer bir pencere aracının sabit olarak durum çubuğunda kalmasını istiyorsak addParmanentWidget\(\) methodunu kullanırız. Eğer durum mesajı geldiğinde var olan pencere aracının bu mesajı engellemesini istemiyorsak addWidget\(\) methodunu kullanırız.

addWidget\(\) ile eklenen pencere araçları durum çubuğunun solunda konumlanır. addParmanentWidget\(\) ile eklenen pencere araçları sağ tarafa yaslanacak şekilde konumlanır. Bir örnek ile pekiştirelim:

```python
from PyQt5.QtWidgets import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.buton = QPushButton()
        self.buton.setText("Buton")
        self.buton.setStatusTip("Fare butonun üzerinde.")

        self.buton2 = QPushButton()
        self.buton2.setText("Buton2")

        self.statusBar = QStatusBar(self)
        self.setStatusBar(self.statusBar)

        self.statusBar.addWidget(self.buton2)
        self.statusBar.addPermanentWidget(self.buton)

uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırdığınızda iki adet butonun durum çubuğunda göründüğünü göreceksiniz. Eğer sağdaki butona fare imlecini getirirseniz durum mesajının solda göründüğünü ve ikinci butonun gizlendiğini göreceksiniz. Durum mesajı ne kadar uzun olursa olsun, sağdaki buton hep görülür olarak kalacaktır.

addWidget\(\) ve addParmanentWidget\(\) methodları ikinci bir parametre daha alır. Bu parametreler varsayılan olarak 0\(sıfır\)'dır. Eğer bu parametreyi 1 olarak girersek eklediğimiz pencere aracı durum çubuğunu kaplayacaktır. Tabii başka pencere araçları var ise onların minimum boyutlara düşürüp kalan boşluğu kendine alacaktır.

