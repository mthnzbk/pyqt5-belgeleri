# Basit Pencere Oluşturma

PyQt5'i daha yakından tanıyabilmek ve ilk programlarımızı yazabilmek için, çalışmalarımıza boş da olsa bir pencere tasarlayarak başlayacağız. Dilerseniz, etkileşimli kabuk üzerinde bazı denemeler yaparak pencere oluşturma sürecinin nasıl işlediğini anlamaya çalışalım. Böylece PyQt5'de boş bir pencere oluşturmak için atılması gereken adımları daha net görür, yazacağımız asıl programlar için bir ön hazırlık yapmış oluruz. Bildiğiniz gibi, ufak tefek kod parçalarını test etmek için Python’ın etkileşimli kabuğu mükemmel bir ortamdır.

Şimdi hemen etkileşimli kabuk ortamını çalıştıralım ve sırasıyla şu kodları yazalım:

```python
>>> from PyQt5 import QtWidgets
>>> import sys
```

PyQt5 ile geliştirme yaparken temel olarak iki modülü mutlaka içe aktarmamız gerekiyor. Bunlar PyQt5 modülü içindeki QtWidgets sınıfı ve gömülü modüllerden biri olan sys modülü. Bu modüllerin sunduğu işlevlerden programlarımız içinde yararlanacağımız için, bu modülleri içe aktarmayı unutmuyoruz.

Gerekli modülleri içe aktardıktan sonra yapmamız gereken ilk iş bir QApplication nesnesi oluşturmak olmalı. Dikkat:

```python
>>> uygulama = QtWidgets.QApplication(sys.argv)
```

Bu satır ilk bakışta, yapmak istediğimiz pencere oluşturma işlemi açısından gereksiz bir satırmış gibi görünebilir. Ama aslında bu kod parçası arkaplanda son derece önemli işler çevirir. Programımızla ilgili ilk ve ana ayarlar bu kod ile yerine getirilir. İlerleyen sayfalarda bu satırın tam olarak ne işe yaradığını daha iyi anlayacağız. Biz şimdilik, yazdığımız programlarda bu satırı bu şekilde kullanmamız gerektiğini bilelim yeter.

Sıra geldi penceremizi oluşturmaya. Penceremizi şu kod ile oluşturuyoruz:

```python
>>> pencere = QtWidgets.QWidget()
```

Böylece penceremizi oluşturmuş olduk. Bunun için QtWidgets modülünün QWidget\(\) adlı sınıfını parametresiz bir şekilde kullandığımıza dikkat edin. Bu sınıfı, bu şekilde parametresiz olarak kullandığımızda bir pencere oluşturmuş oluyoruz.

Ancak penceremizin ekranda görünmesi için bu kod yeterli değil. Penceremizin ekranda görünebilmesi için, pencereyi ekranda göstermek istediğimizi açık açık belirtmemiz gerekiyor. Bunun için show\(\) adlı bir metottan yararlanacağız:

```python
>>> pencere.show()
```

Bu komutu verir vermez ekranda boş bir pencere açılacaktır. Böylece PyQt5 ile ilk penceremizi oluşturmuş olduk. Gördüğünüz gibi, oluşan bu pencere, bir pencerenin sahip olması gereken bütün özellikleri taşıyor. Bu pencereyi kapatmak için pencere üzerindeki çarpı işaretine basabilirsiniz.

Etkileşimli kabuk ortamında ilk denemelerimizi başarıyla tamamladığımıza göre artık çalışmalarımızı daha ciddi bir ortama taşıyabiliriz. Şimdi boş bir metin belgesi açalım ve içine şu satırları yazalım:

```python
from PyQt5 import QtWidgets
import sys

uygulama = QtWidgets.QApplication(sys.argv)

pencere = QtWidgets.QWidget()
pencere.show()
```

Bu dosyayı masaüstüne deneme.py adıyla kaydedip, herhangi bir Python programını nasıl çalıştırıyorsak o şekilde çalıştıralım.

Ne oldu? Programı çalıştırdığınızda pencere çok hızlı bir şekilde ekranda belirip kayboldu, değil mi? Bunu engellemek için programımızın son satırına şu kodu ekleyelim:

```python
uygulama.exec_()
```

Yani kodlarımız tam olarak şöyle görünsün:

```python
from PyQt5 import QtWidgets
import sys

uygulama = QtWidgets.QApplication(sys.argv)

pencere = QtWidgets.QWidget()
pencere.show()

uygulama.exec_()
```

Artık programımızı çalıştırdığımızda, pencere açılacak ve kapanmak için bizim çarpı düğmesine basmamızı bekleyecektir.

Gördüğünüz gibi, QtWidgets adlı alt-modül büyüklü-küçüklü harflerden oluşuyor. Bu yüzden bu alt-modülü kodlarımızın her yerinde doğru bir şekilde yazmaya çalışmak ilave bir çaba gerektiriyor. İsterseniz işlerimizi kolaylaştırmak için bu sınıfı şu şekilde içe aktarabiliriz:

```python
from PyQt5.QtWidgets import *
```

Böylece kodlarımızda **QtWidgets** önekini yazmak zorunda kalmayacağız.

Gerekli modülleri içe aktardığımıza göre, ikinci adıma geçebiliriz.

İkinci adımda bir Qt uygulaması oluşturmamız gerekiyor:

```python
uygulama = QApplication(sys.argv)
```

Daha önce de söylediğimiz gibi, ilk bakışta pek belli olmasa da aslında çok önemli bir satırdır bu. Bu satır sayesinde PyQt5, programımızın başlangıcından sona erişine kadar olan bütün süreci takip edebilecek ve programımızın düzgün bir şekilde çalışıp sona ermesini sağlayabilecektir. Burada oluşturduğumuz QApplication nesnesi, programımızı çalıştırdığımız masaüstü ortamı ile programımız arasındaki ilişkiyi düzenlediği için, grafik arayüze dair başka herhangi bir kod yazmadan önce bu satırı yazmış olmamız gerekiyor. Eğer bu satırı yazmazsak, programımız zaten bizi bu satırı yazmamız gerektiği konusunda uyaracaktır:

```text
QWidget: Must construct a QApplication before a QPaintDevice
```

Bu satırın en önemli görevlerinden biri de, program çalıştırılırken komut satırında verilen parametreleri tutmasıdır. QApplication\(\) sınıfına sys.argv parametresini de zaten bu yüzden veriyoruz.

Bu durumu daha net anlayabilmek için şöyle bir program yazabilirsiniz:

```python
from PyQt5.QtWidgets import *
import sys

uygulama = QApplication(sys.argv)

print(uygulama.argv())
```

Bu programı yazıp deneme.py adıyla kaydettikten sonra şu komutu vererek programı çalıştırın:

```text
python3 deneme.py
```

Programı bu şekilde çalıştırınca şu çıktıyı alacaksınız:

```python
['deneme.py']
```

Aynı programı şimdi bir de şöyle çalıştırın:

```text
python3 deneme.py --yardim
```

Bu defa şöyle bir çıktı alacaksınız:

```python
['deneme.py', '--yardim']
```

Gördüğünüz gibi, QApplication nesnesi, yazdığımız programın çalıştırılması sırasında programa verilen parametrelerin listesini de tutuyor. Bu listeye QApplication nesnesinin argv\(\) metodu aracılığıyla ulaşabildiğimizi görüyorsunuz.

Pencere oluşturma sürecinin ikinci aşamasını da geride bıraktığımıza göre üçüncü aşamaya gelebiliriz. Bu aşamada penceremizi çizeceğiz:

```python
pencere = QWidget()
```

QtWidgets modülünün QWidget\(\) sınıfını kullanarak boş bir pencere oluşturuyoruz. Ancak bu kod pencerenin görüntülenebilmesi için yeterli değil. Penceremizi oluşturduktan sonra görüntüleyebilmek için show\(\) adlı bir metottan yararlanacağız:

```python
pencere.show()
```

Böylece dördüncü aşamayı da geride bırakıp son aşamaya gelmiş olduk. Son aşamada ana döngüyü başlatmamız gerekiyor. Bunu şu satırla hallediyoruz:

```python
uygulama.exec_()
```

Bu satır sayesinde programımız hızlı bir şekilde açılıp kapanmak yerine, kullanıcıdan gelecek emirleri beklemeye başlıyor. Böylece biz de penceremizi ekranda görebiliyoruz.

Programımızı derli toplu bir şekilde tekrar görelim:

```python
from PyQt5.QtWidgets import *
import sys

uygulama = QApplication(sys.argv)
pencere = QWidget()
pencere.show()
uygulama.exec_()
```

Gördüğünüz gibi, PyQt5 ile boş bir pencere oluşturabilmek için altı satırlık bir program yazmamız gerekiyor. Bu kodlar ilk bakışta biraz karmaşıkmış gibi görünse de, aşamaların mantığını kavradığınız zaman yazması oldukça kolaydır.

