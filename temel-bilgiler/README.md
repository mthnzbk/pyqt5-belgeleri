# Temel Bilgiler

Genel olarak programlama dilleri, yazdığınız programlarda kullanıcılarınızla iletişimi iki farklı yoldan sağlamanıza izin verir:

1. Komut satırı arayüzü \(command-line interface\)
2. Grafik kullanıcı arayüzü \(grapfical user interface\)

Bir programlama dilinin sadece kendi imkanlarını kullanarak genellikle sadece komut satırı üzerinden çalışan programlar yazabiliriz\(İstisnalar mevcut\). Programlama dilleri ile grafik arayüzler tasarlayabilmek için o dille uyumlu harici kütüphanelerden yararlanmamız gerekir.

Bu durum Python dili için de aynen geçerlidir. Python dilinin sadece kendi imkanlarını kullanarak yalnızca komut satırı üzerinden çalışan programlar yazabiliriz. Ama Python’la uyumlu harici kütüphaneleri kullanarak grafik arayüze sahip programlar yazma imkanına da sahibiz.

Python’da grafik arayüz tasarlayabilmek için elimizde pek çok ek kütüphane seçeneği var. Bu seçeneklerin en önemlilerini şöyle sıralayabiliriz:

1. [Tkinter](http://wiki.python.org/moin/TkInter)
2. [PyQt](http://www.riverbankcomputing.co.uk)
3. [PyGObject + GTK3](http://live.gnome.org/PyGObject)
4. [wxPython](http://wxpython.org/)

Dediğimiz gibi, yukarıda saydıklarımız Python üzerinde kullanabileceğimiz grafik arayüz geliştirme kütüphanelerinin en önemlileridir. Ama aslında bunların dışında başka seçenekler de bulunur. Eğer öteki seçeneklerin ne olduğunu görmek istiyorsanız [bu](https://wiki.python.org/moin/GUI%20Programming%20in%20Python) bağlantıdan öğrenebilirsiniz.

Yukarıda saydığımız seçeneklerin en güçlülerinden biri, elinizin altındaki bu belgelendirmenin de konusunu oluşturan, PyQt5 adlı grafik arayüz kütüphanesidir. Bu bölüm de PyQt5 adlı grafik arayüz kütüphanesi hakkındaki bilgileri edinmeye çalışacağız. PyQt5’in temeli Qt adlı bir kütüphanedir. İsterseniz PyQt5 ve bunun temelini oluşturan Qt kütüphanelerinden biraz söz edelim.

