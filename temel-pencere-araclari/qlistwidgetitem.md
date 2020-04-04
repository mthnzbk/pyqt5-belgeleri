# QListWidgetItem

QListWidget'i anlatırken öge olarak hep karakter dizisi ekledik ve bir Python listesi gibi sırasına göre işlem yaptık. PyQt bize QListWidget ile kullanmamız için QListWidgetItem sınıfı sağlar. Bu sınıf sayesinde hem listede görünürde karakter verisi sıralarız, hem de bu sınıf ile üreteceğimiz nesne sayesinde her QListWidgetItem ögesine farklı özellikler kazandırabiliriz.

Bir QListWidgetItem nesnesini şöyle tanımlarız:

```python
item = QListWidgetItem("Python", self.listwidget)
```

İstersek ilk parametre olan öge adını QListWidgetItem'in setText\(\) methodu ile tanımlayıp sadece self.listwidget'i parametre olarak verebiliriz:

```python
item = QListWidgetItem(self.listwidget)
item.setText("Python")
```

Bir önceki konuda QListWidget'e nasıl öge eklediğimizi öğrendik. Şimdi basit bir örnekle bu sefer karakter dizisi değil de QListWidgetItem nesnesi ekleyelim:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)
        self.listwidget.addItem(QListWidgetItem("Python"))
        self.listwidget.addItem(QListWidgetItem("Ruby"))
        self.listwidget.addItem(QListWidgetItem("Go"))
        self.listwidget.addItem(QListWidgetItem("Perl"))

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)
        self.buton.clicked.connect(self.sil)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştırdığınızda bir önceki konuda gördüğünüz aynı pencere ile karşılaşacaksınız. QListWidget sınıfının addItem\(\) methodu parametre olarak QListWidgetItem sınıfını da alır. Burada dikkat edilmesi gereken QListWidgetItem'e argüman olarak sadece öge ismi verdik. İkinci parametreye verdiğimiz ebeveyn parametresini burada kullanmaya gerek duymadık. Çünkü addItem\(\) methodu aldığı QListWidgetItem nesnesine ebeveynini tayin eder. Eğer siz addItem ile QListWidgetItem ögesini QListWidget'e eklemek istemiyorsanız konunun başında kullanımına dair verdiğimiz örneğe göre de ekleme işlemini yapabilirsiniz:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.listwidget = QListWidget(self)
        item1 = QListWidgetItem("Python", self.listwidget)
        item2 = QListWidgetItem("Ruby", self.listwidget)
        item3 = QListWidgetItem("Go", self.listwidget)
        item4 = QListWidgetItem("Perl", self.listwidget)

        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.listwidget)
        self.layout.addWidget(self.buton)

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

QListWidget'e bu şekilde öge eklediğinizde seçili olan ögeyi almak için currentRow\(\) methodu yerine currentItem\(\) methodunu kullanmak isteyebilirsiniz. Bu method size öge sırası yerine bir QListWidgetItem nesnesi döndürür. Aynı şekilde seçili olmasını istediğiniz ögenin nesnesini biliyorsanız setCurrentItem\(\) methodunu kullanabilirsiniz.

Aynı şekilde insertItem\(\) methodunu da QListWidgetItem sınıfı ile kullanabilirsiniz. Ayrıca bu sınıfın setIcon\(\) methodu ile her ögenin başına gelecek şekilde bir simge resmi koyabilirsiniz:

```python
item1.setIcon(QIcon("falanca.png"))
```

> **Note** QIcon sınıfı QtGui paketindedir.

QListWidgetItem sınıfının kullanımını gördükten sonra şimdi tekrar QListWidget pencere aracına dönelim...

QListWidget de sıralanmış ögelere **Shift** tuşuna basılı olarak tıkladığınızda birden fazla seçim yapamadığınızı fark edeceksiniz. Çünkü ön tanımlı seçim modu tekli seçimdir. QListWidget pencere aracı için tanımlı dört adet seçim modu vardır. Ayrıca seçim modu sayarsanız bir de seçilememe modu da mevcuttur.

Bir QListWidget'in öge seçim modunu düzenlemek için setSelectionMode\(\) methodu kullanılır. Kullanımını bir örnek ile görelim:

```python
self.listwidget.setSelectionMode(QAbstractItemView.ContiguousSelection)
self.listwidget.setSelectionMode(QAbstractItemView.ExtendedSelection)
self.listwidget.setSelectionMode(QAbstractItemView.SingleSelection)
self.listwidget.setSelectionMode(QAbstractItemView.MultiSelection)
```

QAbstractItemView bir sanal sınıftır. PyQt de buna benzer bir çok sanal sınıf vardır. Bu sınıflar hangi sınıf için yazıldıysa, o sınıfa bazı özelliklerin kazandırılmasını sağlar. Bu örnekte de QListWidget pencere aracına özellik kazandırılıyor.

**ContiguousSelection** özelliği ile QListWidget de bir ögeye tıklanmış ise ve sonraki ögeye basarken **Shift** tuşu basılıysa, iki öge dahil arasında kalan ögelerde seçilir.

**ExtendedSelection** özelliği ile QListWidget de bir ögeye **Ctrl** tuşu ile basılırsa seçili ise seçilme kalkar, seçili değilse seçilir. Bu şekilde tıkladığınız her öge ya seçilir, ya seçimi kalkar. **Shift** tuşuna basılı olarak tıkladığınızda ise ilk seçimle ikinci seçim arası seçilir ve **Shift** tuşuna basılıyken farklı bir öge seçerseniz ilk tıkladığınız ile bu seferki tıkladığınız dahil arasında kalan ögeler de seçilir.

**SingleSelection** özelliği ön tanımlı olarak gelir. Sadece tek seçim yapabilirsiniz.

**MultiSelection** özelliği ile her tıkladığınız öge seçili değilse seçilir, seçili ise seçilmemiş hale döner. Bu seçim modu seçildiğinde **Shift** ya da **Ctrl** tuşuna basmadan çoklu seçim yapabilirsiniz.

> **Note** QAbstractItemView sınıfı QtWidgets paketi içindedir.

