# QFormLayout

QFormLayout, adından da anlaşılacağı gibi formlarınız için yerleştirme işini yapar. Mesela üye kayıt formu tasarladınız: Bu tasarladığınız formda kullandığınız pencere araçlarını nasıl uygun şekilde yerleştireceksiniz? Yan yana iki adet QVBoxLayout ile mi? Tabii ki hayır! Tabii isterseniz QGridLayout ile de yapabilirsiniz, ama pencere aracı ekleme işi biraz daha zahmetli gelebilir.

QFormLayout sadece iki sütun alacak şekilde ayarlanmıştır. Yani formunuzda yer alabilecek **İsim:** yazan etiket ile sağındaki QLineEdit pencere aracı iki sütunu dolduracaktır. Her satır için iki sütun. Basit bir form ile QFormLayout sınıfını görelim:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QFormLayout(self)

        self.lineedit1 = QLineEdit(self)
        self.lineedit2 = QLineEdit(self)
        self.lineedit3 = QLineEdit(self)
        self.lineedit3.setEchoMode(QLineEdit.Password)

        self.layout.addRow("İsim:", self.lineedit1)
        self.layout.addRow("Soyad:", self.lineedit2)
        self.layout.addRow("Şifre:", self.lineedit3)


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Gördüğünüz gibi diğer pencere aracı yerleştirme sınıfları gibi oldukça basit bir kullanımı var. QFormLayout'un addRow\(\) methodu ilki etiket adı, ikincisi pencere aracı olmak üzere iki tane parametre alır. Her kullandığınız addRow\(\) methodu formunuza bir satır daha ekler.

Pencere aracı yerleşimi için QFormLayout bize başka bir seçenek daha sunar. Bu seçeneği siz daha çok **Qt Designer** uygulaması ile QFormLayout pencere aracı yerleştiricisini kullandığınızda göreceksiniz. Çünkü **.ui** uzantılı tasarım dosyasını Python betiğine dönüştürdüğünüzde bu kullanım çeşidiyle karşılaşacaksınız.

Şimdi diğer seçeneğimizi görelim:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QFormLayout(self)

        self.lineedit1 = QLineEdit(self)
        self.lineedit2 = QLineEdit(self)
        self.lineedit3 = QLineEdit(self)
        self.lineedit3.setEchoMode(QLineEdit.Password)

        self.label1 = QLabel(self)
        self.label1.setText("İsim:")
        self.label2 = QLabel(self)
        self.label2.setText("Soyad:")
        self.label3 = QLabel(self)
        self.label3.setText("Şifre:")

        self.layout.setWidget(0, QFormLayout.LabelRole, self.label1)
        self.layout.setWidget(0, QFormLayout.FieldRole, self.lineedit1)
        self.layout.setWidget(1, QFormLayout.LabelRole, self.label2)
        self.layout.setWidget(1, QFormLayout.FieldRole, self.lineedit2)
        self.layout.setWidget(2, QFormLayout.LabelRole, self.label3)
        self.layout.setWidget(2, QFormLayout.FieldRole, self.lineedit3)


uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Kodumuz oldukça uzadı değil mi?..

QFormLayout sınıfının setWidget\(\) methodu bir diğer seçenektir. Az önce dediğimiz gibi bu kullanım tarzını **Qt Designer** uygulaması ile tasarım yaptığınızda karşılaşacaksınız.

setWidget\(\) methodunun aldığı ilk parametre sizin de tahmin edeceğiniz gibi form ögelerinin sırasını belirtir.

İkinci parametrede bulunan QFormLayout sınıfının LabelRole özelliği, eklenen pencere aracının etiket özelliğinde olduğunu belirtir. Zaten son parametrelere verdiğimiz QLabel nesnelerinden de anlaşılıyordur.

FieldRole özelliği ise Türkçe anlamındaki gibi üçüncü parametreye atadığımız pencere aracının rolünü belirtiyor. QLineEdit pencere araçları formun alanında yer alırlar.

Form yerleşimi için sunulan iki seçeneği de gördünüz. Siz QFormLayout sınıfını kullanırsanız, sizin için hangisi uygunsa onu kullanacaksınız.

