# Son Hazırlıklar

Yukarıda anlattığımız bütün kurulum işlemlerinden sonra PyQt5'i gerçekten doğru bir şekilde kurup kuramadığınızı test etmek için Python3’ün etkileşimli kabuğunda şu komutu verin:

```python
import PyQt5
```

Eğer bu komutu verdikten sonra hiçbir şey olmadan alt satıra geçiliyorsa PyQt5'i başarıyla kurdunuz demektir. Ama eğer yukarıdaki komuttan **ImportError: No module named PyQt5** gibi bir çıktı aldıysanız PyQt5'i düzgün bir şekilde kuramadınız demektir. Bu durumda başa dönüp nerede hata yaptığınızı bulmaya çalışabilir veya ilgili forumlara uğrayarak yardım isteyebilirsiniz. Biz kurulumu doğru bir şekilde yapabildiğinizi varsayarak yolumuza devam edelim.

PyQt5 adlı grafik arayüz kütüphanesini başarıyla bilgisayarınıza kurdunuz. Artık bu kütüphaneyi kullanarak grafik arayüzler tasarlamaya hazırsınız. Biz bu süreçte, karşılaştığınız sorunları çözebilmeniz için, elinizdeki belgeler aracılığıyla size mümkün olduğunca yardımcı olmaya çalışacağız. Ancak PyQt5 ile grafik arayüz tasarlarken bu belgelerin yeterli gelmediği durumlarla da karşılaşabilirsiniz. Öyle bir durumda ya forumlardan yardım isteyeceksiniz ya da deneme yanılma ile doğru yolu bulacaksınız.

> **Note** Bir Qt sınıfı ile ilgili bir bilgi arıyorsanız Qt'nin kendi belgelerine bakarak aradığınızı bulma ihtimaliniz oldukça yüksektir. Qt ile PyQt'nin kullanıldığı diller farklı olsa da aralarında çok az fark vardır. PyQt5'i öğrenip takıldığınızda araştırma yaparken de fark edeceksiniz. Qt5 belgelerine [buradan](http://doc.qt.io/qt-5.5/classes.html) ulaşabilirsiniz.

