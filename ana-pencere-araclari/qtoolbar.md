# QToolBar

Bu pencere aracı adından da anlaşılacağı üzere araç çubuğu oluşturmamıza yarar. Ofis programramlarında gördüğünüz "Kaydet", "Aç", "Yazdır", gibi butonların bulunduğu şerit şeklindeki alan PyQt5 de QToolBar ile yapılır.

QToolBar pencere aracına isterseniz QAction, QMenu ya da diğer pencere araçlarını ekleyebilirsiniz:

```python
from PyQt5.QtWidgets import *
from PyQt5.QtCore import *
import sys

class AnaPencere(QMainWindow):
    def __init__(self):
        super().__init__()
        self.widget = QWidget(self)
        self.setCentralWidget(self.widget)

        self.toolBar = QToolBar(self)
        self.addToolBar(Qt.TopToolBarArea, self.toolBar)

        self.pushButton1 = QPushButton()
        self.pushButton1.setText("Aç")
        self.toolBar.addWidget(self.pushButton1)

        self.toolBar.addSeparator()
        self.pushButton2 = QPushButton()
        self.pushButton2.setText("Kaydet")
        self.toolBar.addWidget(self.pushButton2)

        self.pushButton3 = QPushButton()
        self.pushButton3.setText("Farklı Kaydet")
        self.toolBar.addWidget(self.pushButton3)

uygulama = QApplication(sys.argv)
pencere = AnaPencere()
pencere.show()
uygulama.exec_()
```

Bu örnekte QToolBar'ın addWidget\(\) methodu ile üç adet QPushButton pencere aracı ekledik. **Aç** butonundan sonraki butonları ayrı tutmak için QToolBar'ın addSeparator\(\) methodunu kullandık. Bu method QMenu de olduğu gibi kullanıldığı yerden önceki ve sonraki pencere araçları arasına çizgi çeker.

Bir QToolBar'ı QMainWindow'a yerleştirmek için QMainWindow'un addToolBar\(\) methodunu kullanılır. Bu methodun ilk parametresi QToolBar'ın pencere üzerindeki konumunu\(sağ-sol-yukarı-aşağı\) belirtir, ikinci parametreye ise QToolBar sınıfının örneği yazılır. Yukarıdaki örnek kodda biz QToolBar'ı pencerenin üst kısmına yerleştirdik. Eğer farklı bir konuma yerleştirmek isterseniz:

```python
Qt.LeftToolBarArea
Qt.RightToolBarArea
Qt.BottomToolBarArea
```

> **Note** Qt sınıfı QtCore paketinde bulunur.

Genelde QToolBar pencere aracında QPushButton yerine QAction kullanılır. QMenu de tanımlanan bu sınıfları fazladan QAction oluşturmadan QToolBar'da da kullanabiliriz. Bir QAction sınıfı QToolBar'ın addAction\(\) methodu ile eklenir:

```python
self.action = QAction()
self.action.setText("Aç")
self.toolBar.addAction(self.action)
```

Yukarıda QToolBar pencere aracının hangi konuma yerleştirileceğini öğrendik. Varsayılan olarak bir QToolBar pencere aracı fare sürüklemesi ile farklı konumlara taşınabildiği gibi ayrı çerçevesiz bir pencerede duracak şekilde ayarlıdır. QToolBar'ın taşınabilmesine olanak sağlayan bu sınıfın setMovable\(\) methodudur. Bu methodun varsayılan parametresi **True** dur. Eğer siz bu methoda **False** parametresini verirseniz QToolBar pencere aracı taşınamaz olacaktır. Eğer taşınabilir olmasında bir sakınca yoksa, ama uygun yere koyulmama durumunda ayrı bir pencere gibi durmasını engellemek istiyorsak setFloatable\(\) methodunu kullanacağız. Bu method da varsayılan olarak **True** dur ve siz bu methoda **False** parametresi girerseniz QToolBar pencere aracı sadece QMainWindow içerisinde barınabilecektir.

