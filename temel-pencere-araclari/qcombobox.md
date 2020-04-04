# QComboBox

Bu pencere aracında liste halinde verilen karakter dizilerinin grafik arayüz üzerinde kullanabilmenize imkan sağlar. Girdiğiniz veriye göre kullanıcı bu pencere aracına tıklayarak seçimini yapar ve buna göre uygulamanızın ne yapacağını ayarlarsınız. Ufak bir örnekle QComboBox pencere aracını giriş yapalım:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)
        self.comboBox = QComboBox(self)
        self.comboBox.addItem("Metehan")
        self.comboBox.addItems(["Ahmet", "Mehmet", "Banu", "Konuray"])

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.comboBox)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.hangiButon)

    def hangiButon(self):
        print(self.comboBox.currentIndex(), self.comboBox.currentText())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

self.comboBox adında bir QComboBox nesnesi tanımladık. QComboBox'un addItem\(\) methodu ile **Metehan** adlı karakter dizisini ekledik. Eğer istersek addItems\(\) methodu ile liste halinde vereceğimiz karakter dizilerini de çoklu olarak ekleyebiliriz. Örnekte; Ahmet, Mehmet, Banu, Konuray isimlerini de Metehan'dan sonrasına eklemiş olduk.

Yine butonumuzun clicked\(\) sinyaline bağladığımız hangisi\(\) yuvasıyla bazı işlemler gerçekleştiriyoruz. currentIndex\(\) methodu seçili olan karakter dizisinin sırasını, currentText\(\) methodu ise seçili olan karakter dizisinin kendisini verir. Uygulamayı çalıştırıp QComboBox pencere arasından **Mehmet**'i seçip **Tamam** butonuna tıkladığınızda:

`2 Mehmet`

çıktısını alacaksınız. Python'da listeleri bildiğinizi varsayarak bu işlemin de aynı listeden seçilen ögeyi getirmek gibi olduğunu anlayacaksınızdır.

Mesela uygulamanız için tema özelliği getirdiniz ve seçili olan temanın QComboBox da varsayılan olarak gösterilmesini istiyorsunuz. Normalde QComboBox pencere aracı ilk sırada hangi veri varsa onu gösterir, ama biz istediğimizin gösterilmesini basitçe ayarlayabiliriz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)
        self.comboBox = QComboBox(self)
        self.comboBox.addItem("Metehan")
        self.comboBox.addItems(["Ahmet", "Mehmet", "Banu", "Konuray"])

        self.comboBox.setCurrentText("Ahmet")
        # ya da
        self.comboBox.setCurrentIndex(1)

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.comboBox)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.hangiButon)

    def hangiButon(self):
        print(self.comboBox.currentIndex(), self.comboBox.currentText())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

İki basit method ile istersek karakter dizisi ile ya da karakter dizisinin sırası ile başlangıçta seçili gelecek karakter dizisini ayarlıyoruz. Bizim için bunu setCurrentText\(\) ve setCurrentIndex\(\) methodu sağlıyor.

Daha görsel bir kullanıma ihtiyacınız olursa, her liste öğesinin başına simge resmi koyabilirsiniz:

```python
self.comboBox.setItemIcon(1, QIcon("falanca.png"))
```

> **Warning** QIcon sınıfının QtGui paketinde olduğunu unutmayın.

setItemIcon\(\) methodu ilk parametreye listedeki elemanın sırasını alır ve ikinci parametrede belirtilen simge resmini bu elemanın başında uygun çözünürlükte gösterir. İkinci parametre yukarıda görüldüğü gibi bir QIcon sınıfı alıyor. Bu sınıfı daha önceki konularda da nasıl kullandığımızı gördük.

Şimdi de son olarak öğrenmesi basit, ama kullanımı görsel olarak oldukça şıklık katan bir sınıfa değineceğiz. QCompleter! Bu anlatacağımız QCompleter sınıfını QLineEdit pencere aracında da kullanabileceğinizi de söyleyelim...

Bazı uygulamalarda QLineEdit gibi pencere araçlarına karakter dizisi yazarken aşağı doğru açılan, yazdığınız metne göre size sonuç listelendiğini görmüşsünüzdür. Örneğin; artık internet tarayıcılarının adres çubuğuna aramak istediğimiz sözcükleri yazarken bize "bu mu?" der gibi ilgili arama seçenekleri sunar. Biz de basitçe buna benzer bir uygulama geliştireceğiz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        isim_listesi = ["Ahmet", "Mehmet", "Banu", "Konuray", "Metehan", "Aleyna", "Melahat", "İlhan", "İdris"]
        self.tamamlayici = QCompleter(isim_listesi, self)

        self.comboBox = QComboBox(self)
        self.comboBox.setEditable(True)
        self.comboBox.addItems(isim_listesi)
        self.comboBox.setCompleter(self.tamamlayici)

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.comboBox)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.hangiButon)

    def hangiButon(self):
        print(self.comboBox.currentIndex(), self.comboBox.currentText())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Burada isim\_listesi adında bir liste oluşturduk ve bir kaç tane isim girdik. Tamamlayıcı sınıfımız QCompleter'e ilk parametre olarak bu listeyi girdik ve QComboBox sınıfının setCompleter\(\) methodu ile bu QCompleter sınıfını QComboBox'a tanıttık. Tamamlayıcının çalıştığını görebilmek için de QComboBox pencere aracını düzenlenebilir olmasını sağlayan setEditable\(\) methodunu kullandık.

Uygulamayı çalıştırdığınızda QComboBox pencere aracında Ahmet yazacaktır. Bu ismi silip listeye göre yeni isimler girdiğinizde girdiğiniz her karaktere göre isimleri listeleyecektir. Misal ilk iki harfi **Me** girerseniz tamamlayıcı bize **Mehmet**, **Metehan** ve **Melahat** isimlerini gösterecektir. Eğer üçüncü harf olarak **h** yazarsanız sadece **Mehmet** görünecektir. Uygulamayı çalıştırarak test ettiğinizde, bu kadar basit bir uygulama ile nasıl görsellik kattığınızı görüp memnun olacaksınız.

> **Note** QLineEdit ile kullanmak için, QComboBox'daki gibi QLineEdit'in setCompleter\(\) methodunu kullanmalısınız.

