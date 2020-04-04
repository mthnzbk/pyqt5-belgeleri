# QGridLayout

Grid, Türkçe de ızgara anlamına gelir. QGridLayout'a pencere aracı yerleşiminde de mantık ızgara üzerine et yerleştirmek gibidir. İster köfte gibi tek bir noktayı işgal etsin, ister pirzola gibi birden fazla köftenin işgal ettiği yeri işgal etsin. Yerleştireceğiniz pencere araçlarını isteğinize göre tek satır ve sütuna koyabileceğiniz gibi birden fazla sütuna ve/veya satıra sığacak şekilde de koyabilirsiniz. Örnek olarak şöyle bir penceremiz olduğunu düşünelim:

![&#xD6;rnek Izgara G&#xF6;r&#xFC;n&#xFC;m&#xFC;](https://github.com/mthnzbk/pyqt5-belgelendirmesi/tree/ac3b99083a31c230d378981fac186e01fcfe0f1f/pencere-araclarinin-yerlesimi/images/gridlayout.png)

Kırmızı çerçeveli alan bizim ızgaramız oluyor. Bu ızgarada birer adet QTextEdit, QPushButton, QLineEdit ve QLabel var. Dikkatli bakarsanız her pencere aracını birbirinden ayıran yeşil çizgiler var. Bu yeşil çizgilerden anlayacağımız şey, ızgaramızın üç satırdan ve iki sütundan oluştuğudur. QTextEdit sıfırıncı satırda bulunur ve iki sütunu da kaplar. Aynı şekilde QLabelde ikinci satırda bulunur ve iki sütunu da kaplar. QPushButton ve QLineEdit ise birinci satırda birer sütun işgal ederler.

> **Warning** Python'un saymaya sıfırdan başladığını unutmayalım.

Dikkatinizi sütunlardaki eşitsizlik çekmiş olabilir. Bunun sebebi de pencere aracı olarak yerleştirdiklerimizin kapladıkları alana göre şekil almasıdır.

Şimdi de kod olarak nasıl olduğunu görelim:

```python
gridLayout = QGridLayout(self)

gridLayout.addWidget(textEdit, 0, 0, 1, 2)
gridLayout.addWidget(pushButton, 1, 1, 1, 1)
gridLayout.addWidget(lineEdit, 1, 0, 1, 1)
gridLayout.addWidget(label, 2, 0, 1, 2)
```

Diğer yerleşim sınıflarında olduğu gibi QGridLayout sınıfının da addWidget\(\) methodunu pencere aracı yerleştirmek için kullanırız. Yalnız diğer methodlardan farkı aldığı parametrelerdir. Hatırlayın!.. QTextEdit sıfırıncı satırda birinci ve ikinci sütunu kaplıyordu. Yukarıdaki kodda göreceğiniz gibi ilk iki sıfır rakamı sıfırıncı satır ve sıfırıncı sütunu temsil ediyor. Sonraki "1" rakamı kaplayacağı satır sayısını, "2" rakamı ise kaplayacağı sütun sayısını temsil ediyor.

Aynı şekilde QLabel de ikinci satırın sıfırıncı sütununda bulunuyor ve tek satır ile iki sütunu kaplıyor.

QLineEdit birinci satırda ve sıfırıncı sütunda bulunup, tek satır ve tek sütunluk bir yer kaplıyor. QPushButton ise birinci satır ve sütunda yer alıp QLineEdit gibi tek satır ve sütunluk yer kaplıyor.

Anlamakta güçlük çekiyor olabilirsiniz. Ben bile ızgara yerleşimini kullanırken kafam karışabiliyor. Siz de bu sınıfı ne kadar sık kullanır ve yanılıp hatanızı düzeltirseniz o kadar iyi kavrarsınız.

QGridLayout, diğer sınıfların aksine daha fazla method barındırır. Yalnız fazla bilgiyle kafa karışıklığı yaratmamak için kullanacağımız en sık methodu anlattık.

Bunun yanı sıra bu konu altında anlatılan her yerleşim sınıfında olan bir methodu da açıklayalım:

Bir zaman gelir ve birden fazla yerleşim sınıfını başka bir yerleşim sınıfı altında birleştirmek isteyebilirsiniz. Nasıl bir pencere aracını addWidget\(\) ile ekliyorsak bir yerleşim sınıfını da bu şekilde ekleyebiliriz. Tabii bu işi addWidget\(\) methodu yerine addLayout\(\) methodu ile yaparız.

addLayout\(\) methodu her sınıfın addWidget\(\) methodu ile aynı işlevselliği barındırır. Tek fark addLayout ile bir yerleşim sınıfı ekliyoruz. Küçük bir örnek ile konuyu kapatalım:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.vlayout = QVBoxLayout(self)

        self.hlayout = QHBoxLayout(self)
        buton1 = QPushButton("Sol üst", self)
        buton2 = QPushButton("Sağ üst", self)
        self.hlayout.addWidget(buton1)
        self.hlayout.addWidget(buton2)

        self.hlayout2 = QHBoxLayout(self)
        buton3 = QPushButton("Sol alt", self)
        buton4 = QPushButton("Sağ alt", self)
        self.hlayout2.addWidget(buton3)
        self.hlayout2.addWidget(buton4)

        self.vlayout.addLayout(self.hlayout)
        self.vlayout.addLayout(self.hlayout2)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

