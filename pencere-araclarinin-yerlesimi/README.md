# Pencere Araçlarının Yerleşimi

Bir PyQt penceresinde yer alan pencere araçlarını yerleştirmek için bir çok alternatif vardır. Şimdiye kadar işlediğimiz konularda pencere aracı yerleşimi olarak bir tek QVBoxLayout sınıfını pek değinmeden kullandık. Ancak pencere aracını, pencerenin istediğimiz her hangi bir yerine yerleştirebiliriz. Bunu sağlayan her pencere aracının setGeometry\(\) methodudur. Bu method tercihinize göre ya QRect sınıfını ya da dört adet integer veriyi parametre alır:

```python
self.buton = QPushButton(self)
self.buton.setGeometry(QRect(10, 10, 100, 25))
self.buton.setGeometry(10, 10, 100, 25)
```

> **Note** QRect sınıfı QtCore paketindedir.

Gördüğünüz gibi oldukça kolay. Burada ilk parametre pencerenin ne kadar sağında yer alacağını, ikinci parametre ne kadar aşağıda kalacağını belirler. Diğer iki parametre ise pencere aracının boyutunu ayarlar. Tabii isterseniz pencere aracının sadece konumunu da belirtebilirsiniz. daha önceki konularda gördüğümüz move\(\) methodu bu işe yarar. Bu şekilde bir kullanım tercih edilirse pencere aracının boyutları ön tanımlı olarak gelen boyutta pencereye çizilir. Ayrıca boyutunu ayarlamak isterseniz de resize\(\) methodunu kullanabilirsiniz. Bu methodun kullanımını da daha önceki konularda öğrenmiştik.

Bir çok programa baktığımızda; pencere boyutunu fare kullanarak büyültüp küçülttüğümüzde pencere araçlarınında duruma göre konum ve boyutlarının değiştiğini görürüz. Eğer biz uygulamamızı bu şekilde olmasını istiyorsak setGeometry\(\) methodunu kullanmamalıyız. Eğer bu şekilde penceremize pencere araçlarını konumlandırırsak ekranı büyülttüğümüzde ya da küçülttüğümüzde pencere araçlarının olduğu gibi kaldığını görürüz. İyi tasarlanmış ve gelişmiş uygulamalar bu tarz bir tasarımdan kaçınırlar. Ayrıca kullandığımız grafik arayüz kütüphaneleri bunun için gerekli pencere aracı yerleştirme sınıflarını da sağlarlar.

Kullanımı oldukça basit olan bu yerleştirme araçlarını görelim...

