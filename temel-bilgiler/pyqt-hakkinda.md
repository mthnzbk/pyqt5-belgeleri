# PyQt Hakkında

Dediğimiz gibi Qt, C++ adlı programlama dili ile geliştiriliyor. O yüzden, normal şartlar altında Qt’yi ancak C++ ile birlikte kullanabiliriz. Qt adlı bu arayüz kütüphanesini Python ile birlikte de kullanabilmek için, PyQt adlı bir ara katmandan yararlanmamız gerekiyor.

Herhangi bir dille yazılmış bir kütüphanenin başka bir dille birlikte de kullanılabilmesini sağlayan bu tür ara katmanlara teknik dilde ‘bağlayıcı’ **binding** adı verilir. Mesela Tkinter; aslında Tcl adlı bir programlama dili ile geliştirilen Tk adlı arayüz kütüphanesinin Python ile birlikte de kullanılabilmesini sağlamak için yazılmış bir bağlayıcıdır. Yani, nasıl Tkinter, Tcl adlı programlama dili ile geliştirilen Tk adlı arayüz kütüphanesini Python’a bağlıyorsa\(Python3'de tkinter\), aynı şekilde PyQt de, C++ adlı programlama dili ile geliştirilen Qt adlı grafik arayüz kütüphanesini Python’a bağlar.

PyQt5 ise, yukarıda bahsettiğimiz bu PyQt adlı bağlayıcının 5 numaralı ve şu an ki en son sürümüdür\(Qt'nin 5x sürümünü kapsar\).

> **Note** Python programlama dili altında grafik arayüz geliştirebileceğimiz ana seçeneklerden Tkinter ve PyGObject-pygtk2 tamamen özgür lisanslar ile dağıtılan kütüphanelerdir. Bu kütüphaneleri kullanarak hem özgür, hem özgür olmayan; hem açık, hem de kapalı kaynaklı yazılımlar geliştirebiliriz. Ancak PyQt5 de bu geçerli değildir.
>
> Eğer PyQt5 ile geliştireceğiniz program GPL lisansı altında dağıtılan bir özgür yazılımsa PyQt5’i herhangi bir lisans ücreti ödemeden ücretsiz olarak indirip kullanabilirsiniz. Ama eğer geliştireceğiniz yazılım özgür değilse bu durumda PyQt5 için bir lisans satın almanız gerekiyor. Yani, PyQt5 için herhangi bir lisans ücreti ödeyip ödemeyeceğiniz, yazdığınız programın ücretli veya ücretsiz olmasına değil, özgür veya özgür olmamasına bağlıdır. Eğer özgür ama ücretli bir yazılım geliştiriyorsanız PyQt5 lisansı satın almanıza gerek yok.
>
> PyQt5’in lisansı hakkında daha ayrıntılı bilgi edinmek için [burayı](http://www.riverbankcomputing.com/commercial/license-faq) ziyaret edebilirsiniz.

