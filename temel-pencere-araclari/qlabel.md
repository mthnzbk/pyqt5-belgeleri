# QLabel

QLabel adlı pencere aracı, tasarladığımız grafik arayüzler üzerinde etiketler oluşturmamızı sağlar. Yani bu pencere aracını kullanarak, program penceremiz üzerinde kullanıcılarımıza programımızla ilgili mesajlar gösterebiliriz.

Bu pencere aracını şu şekilde oluşturuyoruz:

```python
from PyQt5.QtWidgets import *
import sys

class EtiketliPencere(QWidget):
    def __init__(self):
        super().__init__()
        etiket = QLabel("Programa hoşgeldiniz!", self)

uygulama = QApplication(sys.argv)
pencere = EtiketliPencere()
pencere.show()
uygulama.exec_()
```

Burada QLabel pencere aracını oluşturmamızı sağlayan satır şu:

```python
etiket = QLabel("Programa hoşgeldiniz!", self)
```

QLabel sınıfına verdiğimiz parametrelere dikkat edin. İlk parametre etiket içeriğinin ne olacağını, ikinci parametre ise, oluşturduğumuz bu etiketin nerede yer alacağını gösteriyor. Buna göre etiketimizin içeriği **Programa hoşgeldiniz!** adlı karakter dizisi olacak. Oluşturduğumuz bu etiket ise ana penceremiz **self** üzerinde yer alacak.

Bu noktada önemli bir konuya değinelim. PyQt5’te pencere araçlarını herhangi bir ana pencere üzerine yerleştirmek zorunda değilsiniz. Mesela şu kodları dikkatlice inceleyin:

```python
from PyQt5.QtWidgets import *
import sys

class EtiketliPencere(QLabel):
    def __init__(self):
        super().__init__("Programa hoşgeldiniz!")

uygulama = QApplication(sys.argv)
pencere = EtiketliPencere()
pencere.show()
uygulama.exec_()
```

Burada QWidget sınıfı yerine QLabel sınıfını miras aldık. Bu sınıfın **init**\(\) metodunu çağırırken de parametre olarak etiket içeriğini yazdık. Gördüğünüz gibi, biz QLabel aracını herhangi bir ana pencere üzerine yerleştirmemiş olsak da, etiketimiz kendi kendine bir pencere üzerine yerleşti. Çünkü QLabel diğer pencere araçları gibi QWidget'i miras alır. Ancak yazdığınız programlarda pencere araçlarını daha kolay kontrol edebilmek için bunları bir ana pencere üzerine yerleştirmek iyi bir fikirdir.

QLabel sınıfı yukarıdaki yazım tarzı dışında ilk argümanı **self** de alabilir. Etiket içeriğini QLabel sınıfına argüman olarak vermek zorunda değiliz. QLabel de bulunan setText\(\) methodu etiketimizin içeriğini belirlemede bir diğer tercihimizdir:

```python
from PyQt5.QtWidgets import *
import sys

class EtiketliPencere(QWidget):
    def __init__(self):
        super().__init__()
        etiket = QLabel(self)
        etiket.setText("Programa hoşgeldiniz!")

uygulama = QApplication(sys.argv)
pencere = EtiketliPencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırdığınızda önceki örnekteki ile aynı sonucu elde edeceksiniz.

QLabel sınıfı sadece metin göstermek için kullanılmaz. QLabel pencere aracına html etiketleri ile biçimlendirebilirsiniz. Şu örneğe bakalım:

```python
from PyQt5.QtWidgets import *
import sys

class EtiketliPencere(QWidget):
    def __init__(self):
        super().__init__()
        etiket = QLabel(self)
        etiket.setText("<p style='color:red; font-weight:bold; font-size:14pt>Programa hoşgeldiniz!</p>")

uygulama = QApplication(sys.argv)
pencere = EtiketliPencere()
pencere.show()
uygulama.exec_()
```

Eğer html kodlamasından anlıyorsanız setText\(\) methoduna atadığımız argümanın ne yaptığını anlarsınız. Ancak html bilmeyenler için burada ne yaptığımızı açıklayalım. `<p>` etiketinin style özelliğine css kodu yazarak "Programa hoşgeldiniz!" metnini kırmızı renkte, kalın ve 14 punto büyüklüğünde olmasını sağladık. Eğer isterseniz `<img>` etiketiyle resim de gösterebilirsiniz:

```python
etiket.setText("<img src='resimler/falanca.png'>")
```

Bunun yerine alternatif isterseniz şöyle yapabilirsiniz:

```python
from PyQt5.QtWidgets import *
from PyQt5.QtGui import QPixmap
import sys

class EtiketliPencere(QWidget):
    def __init__(self):
        super().__init__()
        etiket = QLabel(self)
        etiket.setPixmap(QPixmap("resimler/falanca.png"))

uygulama = QApplication(sys.argv)
pencere = EtiketliPencere()
pencere.show()
uygulama.exec_()
```

setPixmap methodu argüman olarak bir QPixmap sınıfı alır. QPixmap sınıfı da aynı QIcon gibi, resim dosyasını QLabel'in anlayacağı şekilde ayarlar. Bu method sayesinde QLabel sınıfıyla metin dışında resim dosyası da gösterebiliyoruz.

> **Note** setPixmap\(\) methodu ile resim gösterdiğinizde setText\(\) methodunu kullanarak karakter dizisi girseniz de pencerede sadece resim gösterilecektir.

