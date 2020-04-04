# QRadioButton

QRadioButton radyo butonları oluşturmanızı sağlar. Bu pencere aracını; özellikle internette kayıt yaparken, anket doldururken görürüz. QRadioButton'un bizim için faydası kullanıcıya sunulan seçeneklerden birini seçmesi sağlanır. Ancak tek başına bir QRadioButton bir işe yaramadığı gibi birden fazla QRadioButton ise kontrol edeceğimiz bir yapı olmadan bize sıkıntı yaratacaktır. Örneğin:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)
        self.radyobuton1 = QRadioButton(self)
        self.radyobuton1.setText("Kadın")
        self.radyobuton2  = QRadioButton(self)
        self.radyobuton2.setText("Erkek")
        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.radyobuton1)
        self.layout.addWidget(self.radyobuton2)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.hangiButon)

    def hangiButon(self):
        if self.radyobuton1.isChecked():
            print(self.radyobuton1.text())
        elif self.radyobuton2.isChecked():
            print(self.radyobuton2.text())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Bu kodla radyo butonlardan birini seçip **Tamam** butonuna tıkladığınızda seçili radyo butonunun metnini konsola yazdırır. Burada bu görevi hangiButon\(\) methodu üstleniyor. QRadioButton'un isChecked\(\) methodu radyo butonuna tıklanmış mı, tıklanmamış mı, True ya da False olarak değer döndürür. Yalnız sıkıntılı bir durum var! Fark ettiniz mi?.. Diğelim ki bir anket oluşturdunuz ve seçenek olarak beş, on ya da daha fazla QRadioButton kullandınız. Şimdi sıkıntıyı fark ettiniz mi? Eminim etmişsinizdir. Eğer böyle bir durumla karşılaşırsak hangiButon\(\) methodunda bir o kadar **if**, **elif** sorgusu kullanmak zorunda kalırdık. Kalırdık, çünkü öyle bir sorunu gidermek için PyQt bize bir sınıf sunar: QButtonGroup.

QButtonGroup, adından da anlaşılacağı gibi butonları gruplamamızı sağlar. Bu pencere aracına eklenen radyo butonlarından hangisinin seçili olduğunu tek method ile öğrenebiliriz. Bu da bize daha temiz ve kısa kod yazmamızı sağlar:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)
        self.radyobuton1 = QRadioButton(self)
        self.radyobuton1.setText("Kadın")
        self.radyobuton2  = QRadioButton(self)
        self.radyobuton2.setText("Erkek")
        self.radyobuton3  = QRadioButton(self)
        self.radyobuton3.setText("Yaşlı")
        self.radyobuton4  = QRadioButton(self)
        self.radyobuton4.setText("Çocuk")
        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.butongrup = QButtonGroup(self)
        self.butongrup.addButton(self.radyobuton1)
        self.butongrup.addButton(self.radyobuton2)
        self.butongrup.addButton(self.radyobuton3)
        self.butongrup.addButton(self.radyobuton4)

        self.layout.addWidget(self.radyobuton1)
        self.layout.addWidget(self.radyobuton2)
        self.layout.addWidget(self.radyobuton3)
        self.layout.addWidget(self.radyobuton4)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.hangiButon)

    def hangiButon(self):
        if self.butongrup.checkedButton():
            print(self.butongrup.checkedButton().text())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Daha iyi bir örnek olması için radyo butonların sayısını artırdık. QButtonGroup sınıfını tanımladık ve bu sınıfın addButton\(\) methodu yardımıyla QRadiButton'ları grupladık. hangiButon\(\) methodunu da iki satırlık kodla düzenledik. QButtonGroup sınıfının checkedButton\(\) methodu tıklanmış radyo butonun kendisini döndürür. Biz burada **if** ile seçilmiş radyo buton var mı diye sorgulayıp, varsa print\(\) ile radyo butonunun metninin çıktısını yazdırmasını sağladık. Eğer **if** ile denetlemeseydik seçim yok iken **Tamam** butonuna tıklayınca hata çıktısıyla karşılaşırdık:

```python
Traceback (most recent call last):
  File "/home/metehan/deneme.py", line 34, in hangiButon
    print(self.butongrup.checkedButton().text())
AttributeError: 'NoneType' object has no attribute 'text'
```

