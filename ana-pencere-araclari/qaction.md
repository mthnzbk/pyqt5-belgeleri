# QAction

QAction pencere araçlarına eklenebilen soyut bir kullanıcı arabirimi eylemi sağlar. Uygulamalarda menülerde, araç çubuğunda kullanılabilir ve klavye kısayolları ile çağırılabilirler.

Kullanımı oldukça basittir... Bir QAction nesnesini üç farklı şekilde tanımlayabilirsiniz:

```python
self.action = QAction(self)
self.action = QAction("Aç", self)
self.action = QAction(QIcon("simge.png"), "Aç", self)
```

İsterseniz ilk seçenekteki gibi nesneyi yaratıp adı için setText\(\) methodundan, ikon resmi için ise setIcon\(\) methodundan faydalanabilirsiniz ya da diğer seçeneklerdeki gibi bir tanımlama yaparak fazladan method kullanmaktan kaçınabilirsiniz.

Genelde QAction nesnesi eklendiği menü örneğini argüman alır. Yani:

```python
self.menu = QMenu(self.menuBar)
self.action = QAction(self.menu)
```

Ayrıca bir QAction'ı QCheckBox gibi kullanabilmeniz için setCheckable\(\) methodu barındırır. Bu methoda **True** değeri girilirse QAction nesnesinin eklendiği menü de isminin baş kısmında kutucuk belirir.

Bir QAction nesnesini bir menüye, menünün addAction\(\) methodu ile ekleyebileceğiniz gibi QAction sınıfında bulunan setMenu\(\) methodu ile bu methoda argüman olarak gireceğiniz QMenu örneği ile QAction nesneniz ilgili menüye dahil olacaktır.

Her işletim sisteminde ya da Linux dağıtımında çalışmasa da bir QAction'a kısayol atayarak, bu kısayol sayesinde QAction'a tıklanma olayı gerçekleştirilebilir:

```python
self.action.setShortcut("Ctrl+O")
```

Görüldüğü gibi karakter dizisi ile kısayol atamasını yaptık. Artık uygulamanız açıkken Ctrl + O tuşuna bastığınızda **Aç** isimli QAction'a fare ile tıklanmış gibi işlem yapılacak. Yalnız Ubuntu üzerinden bu kısayol olayı çalışmıyor...

Şimdi basit bir örnekle kısayol olayını pekiştirelim:

```python
from PyQt5.QtWidgets import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.menuBar = QMenuBar(self)
        self.setMenuBar(self.menuBar)

        self.menu = QMenu(self.menuBar)
        self.menu.setTitle("Dosya")
        self.menuBar.addMenu(self.menu)
        self.action = QAction(self.menu)
        self.action.setText("Aç")
        self.action.setShortcut("Ctrl+O")
        self.menu.addAction(self.action)

        self.action.triggered.connect(self.dialogAc)

    def dialogAc(self):
        dosya = QFileDialog.getOpenFileName(self, "Dosya Dialogu", "/home", "Text dosyası (*.txt)")

uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

QAction arayüzüne tıklandığında ya da kısayol atadıysak ve bu kısayol tuşlarına bastiysak triggered\(\) sinyali yayılır. Örnekte de görüldüğü gibi bu sinyali dialogAc\(\) methoduna bağladık. Eğer bu kodu kısayolu çalıştıran bir işletim sistemi ya da masaüstü ortamında çalıştırıp denerseniz QAction arayüzüne tıkladığınızda ya da kısayol tuşlarına bastığınız da bir dosya seçim penceresi açılacaktır.

QAction'ın triggered sinyali ile bu arayüze tıklanıldığında yapılmasını istediğiniz her türlü işlemi halledebilirsiniz. Oldukça basit bir kullanımı var değil mi?

