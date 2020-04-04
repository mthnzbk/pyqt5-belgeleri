# QTextEdit

QTextEdit pencere aracı, hem düz, hem zengin metin görüntülemeye yarar. Şöyle ki; saf düz yazı dışında html içerik de görüntüleyebilmektedir. QLabel konusunda nasıl html kullandıysak QTextEdit pencere aracı ile de biraz daha fazlasını kullanabiliriz. En basitinden QTextEdit kullanarak html düzenleyici yapabiliriz. Yeteri kadar kendimizi geliştirirsek kod renklendirmeli bir Python düzenleyicisi de yapabilirsiniz. Bu sizin hayal gücünüze bağlı bir durum.

QTextEdit sınıfı, burada açıklayamayacağımız kadar fazla method, özellik içerir. Bu konuda en temel işlevlere değinip bu konuyu tamamlayacağız.

> **Note** Eğer zengin metin içeriği kullanmayacaksanız QPlainTextEdit pencere aracını kullanabilirsiniz.

QTextEdit pencere aracını olduğu gibi uygulamaya koyduğumuzda sadece düz yazı yazabiliriz. Metin renklendirmesi, font biçimlendirmeleri gibi bir çok özelliği yazacağımız kodlarla kullanılabilir yaparız. İlk olarak QLineEdit ile yazacağımız html kodunu QTextEdit üzerinde biçimlendirilmiş halini gösterelim:

```python
from PyQt5.QtWidgets import *
import sys

class Pencere(QWidget):
    def __init__(self):
        super().__init__()
        self.layout = QVBoxLayout(self)

        self.textedit = QTextEdit(self)
        self.lineedit = QLineEdit(self)
        self.buton = QPushButton(self)
        self.buton.setText("Tamam")

        self.layout.addWidget(self.textedit)
        self.layout.addWidget(self.lineedit)
        self.layout.addWidget(self.buton)

        self.buton.clicked.connect(self.htmlYaz)

    def htmlYaz(self):
        self.textedit.setHtml(self.lineedit.text())

uygulama = QApplication(sys.argv)
pencere = Pencere()
pencere.show()
uygulama.exec_()
```

Kodu çalıştıralım ve QLineEdit üzerine **`<h1>PyQt5 Belgelendirmesi</h1>`** yazıp **Tamam** butonuna tıklayalım. QTextEdit üzerinde göreceğiniz gibi boyutu büyük harflerle **PyQt5 Belgelendirmesi** yazacaktır.

**`<h1 style='color:red'>PyQt5 Belgelendirmesi</h1>`** yazıp tekrar butona tıklarsak bu sefer kırmızı renkte **PyQt5 Belgelendirmesi** görünecektir.

Yazdığımız kodda göreceğiniz gibi butonun clicked\(\) sinyalini htmlYaz\(\) yuvasına bağladık. Bu yuvada QTextEdit sınıfının setHtml\(\) methoduna QLineEdit'in text\(\) methodunu argüman olarak verdik. Biz butona tıkladığımızda o an QLineEdit üzerinde ne yazıyorsa QTextEdit üzerine html olarak biçimlendirilerek yazılır. Eğer hatalı bir html kodu ise doğal olarak doğru bir biçimlendirme olmayacaktır.

Uygulamayı denedikçe fark edeceksiniz ki, QLineEdit üzerindeki metni değiştirmemize rağmen QTextEdit üzerinde ekleme yapmak yerine sıfırdan yazacaktır. Eğer biz her yazdığımızı buton ile QTextEdit'e yolladığımızda sonrasına eklenmesini istersek append\(\) methodunu kullanacağız:

```python
def htmlYaz(self):
    self.textedit.append(self.lineedit.text())
```

Aynı şekilde insertHtml\(\) methodunu da kullanabilirsiniz, ama göreceksiniz ki biçimlenen metin yazdığınız koda aykırı olarak bir öncekinin hemen sonrasına yazılacaktır.

QLineEdit ile QTextEdit içerisine girdiğiniz html kodlarını QTextEdit'in toHtml\(\) methodu ile alabilirsiniz. Ancak aldığınız çıktıdan da anlayacağınız gibi yazdığınız kodlarla alakasız bir html kodu alacaksınız. Örneğin QTextEdit'e sadece **`<h1>PyQt5 Belgelendirmesi</h1>`** yazıp çıktısına baktığımızda şöyle bir html kodu görürüz:

```markup
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0//EN" "http://www.w3.org/TR/REC-html40/strict.dtd">
<html><head><meta name="qrichtext" content="1" /><style type="text/css">
p, li { white-space: pre-wrap; }
</style></head><body style=" font-family:'Oxygen-Sans'; font-size:9pt; font-weight:400; font-style:normal;">
<p style=" margin-top:18px; margin-bottom:12px; margin-left:0px; margin-right:0px; -qt-block-indent:0; text-indent:0px;"><span style=" font-size:xx-large; font-weight:600;">PyQt5 Belgelendirmesi</span></p></body></html>
```

Yazdığımız dışında kalan gereksiz html kodlarını bir tarafa bırakırsak bizi ilgilendiren html kodu şudur:

```markup
<span style=" font-size:xx-large; font-weight:600;">PyQt5 Belgelendirmesi</span>
```

Gördüğünüz gibi biz `<h1>` etiketini kullanmış olmamıza rağmen QTextEdit aracı `<span>` etiketi kullanmış. Neden böyle olduğunu henüz bilmiyorum...

Gelelim sinyallere... QTextEdit sınıfının iki önemli sinyali vardır. Diğer sinyallerin kullanımı konumuzun dışında kalıyor. Bu sinyallerden ilki QLineEdit sınıfında da olan textChanged\(\) sinyalidir. QLineEdit konusunu okuduğunuzu varsayarak bu sinyalin ne işe yaradığını da bildiğinizi varsayıyorum.

İkinci sinyalimiz olan cursorPositionChanged\(\), QTextEdit üzerindeyken kaybolup, beliren imlecimizin konumu her değiştiğinde çalışarak sinyal yayar. textChanged\(\) ile benzer tarafı ise siz karakter dizisi girdikçe imlecinde ilerlemesidir. Bu durumda her iki sinyalde çalışır. Tabii biz klavye tuşlarıyla ya da fare ile imlecin yerini değiştirirsek sadece cursorPositionChanged\(\) sinyali, sinyal yayar.

Bu sinyalin ne işimize yarayacağını da siz düşünün :\)

