# Linux Dağıtımları

PyQt5’i Linux dağıtımlarına kurmanın en kolay ve zahmetsiz yolu, kullandığınız dağıtımın paket yönetim sistemini kullanmaktır. Dağıtımınızın deposunda yalnızca Python’un 2.x sürümleriyle uyumlu PyQt5 paketleri yer alıyor olabilir\(Python 3.x sürümü için yoksa 2.x sürümüyle uyumlu PyQt5 paketini de kurabilirsiniz.\). Ubuntu ve Ubuntu tabanlı dağıtımlara Python3 ile uyumlu PyQt5 paketini kurmak için şu komutu kullanabilirsiniz:

`sudo apt-get install python3-pyqt5`

Pardus tabanlı\(Pardus 2011\) Pisi Linux 1.2 dağıtımına PyQt5 kurmak için ise şu komutu kullanabilirsiniz:

`sudo pisi it python3-qt5`

Bu komutu verdiğinizde PyQt5 ve bununla ilgili bütün bağımlılıklar sadece Pisi Linux da sisteminize kurulacaktır. Ubuntu ve türevi dağıtımlarda QtMultimedia gibi modüller ayrı paketlere ayrılmıştır. Dağıtımın paket yöneticilerininde arama yaparak ek paketleri kodlarınızda kullanıyorsanız kurabilirsiniz.

Eğer kurulum sırasında herhangi bir hata almadıysanız PyQt5 ile grafik arayüz tasarlamaya hazırsınız demektir. Birazdan PyQt5'i sistemimize doğru bir şekilde kurup kuramadığımızı denetleyeceğiz.

