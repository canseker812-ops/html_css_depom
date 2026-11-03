Nesne Yönelimli Programlama (Java) -- Çalışma Notları
> **Ders kapsamı:** Yüklenen `NYP_Hafta3.pdf`, `NYP_Hafta3.1.pdf` ve
> `NYP_4.pdf` dosyalarındaki konu başlıkları esas alınmıştır.\
> **Önemli:** Öğretmeninizin açıklamasına göre I/O (girdi-çıktı) konusu
> sınav kapsamı dışındadır. Bu nedenle `Scanner`, `System.out`, dosya
> okuma-yazma gibi konular çalışma kapsamına alınmamıştır. Kod
> örneklerindeki `System.out.println` yalnızca çıktıyı göstermek için
> kullanılmıştır; I/O konusu olarak öğretilmemektedir.
İçindekiler
Sınıf (Class) ve Nesne (Object)
Encapsulation (Kapsülleme)
Constructor (Yapıcı Metot)
Method Overloading (Metot Aşırı Yükleme)
Array (Dizi)
ArrayList
Inheritance (Kalıtım)
Method Overriding (Metot Ezme)
Exception Handling (İstisna Yönetimi)
Abstract Class ve Abstract Method
Sık Karıştırılan Kavramlar
Sınav Öncesi Kontrol Listesi
Karma Alıştırmalar ve Cevap Anahtarı
---
1. Sınıf (Class) ve Nesne (Object)
1.1. Class nedir?
Class, nesnelerin hangi özelliklere (field/attribute) ve davranışlara
(method) sahip olacağını tanımlayan bir şablondur. Tek başına bir sınıf
tanımlamak, o sınıftan mutlaka bir nesne oluşturulduğu anlamına gelmez.
Örneğin bir öğrenci sınıfında öğrencinin numarası, adı ve yaşı özellik;
ders çalışma veya bilgileri gösterme ise davranış olabilir.
``` java
class Ogrenci {
    String ad;
    int numara;
    int yas;

    void bilgileriGoster() {
        System.out.println(ad + " - " + numara + " - " + yas);
    }
}
```
`class Ogrenci`: Ogrenci isimli sınıfı tanımlar.
`ad`, `numara`, `yas`: Nesnenin durumunu tutan alanlardır (field).
`bilgileriGoster()`: Sınıfın davranışını tanımlayan metottur.
1.2. Object nedir?
Object, bir sınıftan oluşturulan somut örnektir. Java'da genellikle
`new` anahtar kelimesiyle nesne oluşturulur.
``` java
Ogrenci ogr1 = new Ogrenci();
ogr1.ad = "Ali";
ogr1.numara = 101;
ogr1.yas = 20;

Ogrenci ogr2 = new Ogrenci();
ogr2.ad = "Ayse";
ogr2.numara = 102;
ogr2.yas = 21;
```
`ogr1` ve `ogr2`, aynı sınıftan oluşturulmuş fakat birbirinden ayrı iki
nesnedir. Bir nesnenin alanındaki değişiklik diğer nesnenin alanını
kendiliğinden değiştirmez.
1.3. Nesne üzerinden metoda erişmek
``` java
class HesapMakinesi {
    int topla(int a, int b) {
        return a + b;
    }
}

class Main {
    public static void main(String[] args) {
        HesapMakinesi hesap = new HesapMakinesi();
        int sonuc = hesap.topla(5, 12);
    }
}
```
`hesap.topla(5, 12)` ifadesi, `hesap` nesnesinin `topla` metodunu
çağırır. Metot iki parametre alır ve toplamı döndürür.
1.4. Referans kavramı
Java'da sınıf türündeki değişkenler, nesnenin kendisini doğrudan değil,
nesneye ulaşmayı sağlayan referansı tutar.
``` java
Ogrenci a = new Ogrenci();
Ogrenci b = a;

b.ad = "Mehmet";
```
Burada `a` ve `b` aynı nesneyi işaret eder. Bu nedenle `b.ad`
değiştirildiğinde `a.ad` üzerinden bakıldığında da aynı nesnenin güncel
değeri görülür.
`new Ogrenci()` ile ikinci bir nesne oluşturulsaydı iki değişken farklı
nesneleri gösterebilirdi.
1.5. Sınıf ve nesne arasındaki fark
---
Class                               Object
---
Şablondur/tanımdır.                 Sınıftan üretilen örnektir.
Özellik ve metotları tanımlar.      Tanımlanan özellik ve metotları
kullanır.
`class Ogrenci` ile tanımlanır.     `new Ogrenci()` ile
oluşturulabilir.
Tek sınıftan birden fazla nesne     Her nesnenin kendi örnek alanları
üretilebilir.                       bulunur.
Kendini dene
Class nedir? Object nedir?
Bir sınıftan birden fazla nesne oluşturulabilir mi?
`new` anahtar kelimesinin görevi nedir?
Field ile method arasındaki fark nedir?
Aşağıdaki kodda kaç sınıf ve kaç nesne oluşturulmuştur?
``` java
class Araba {
    String marka;
}

class Main {
    public static void main(String[] args) {
        Araba a1 = new Araba();
        Araba a2 = new Araba();
        Araba a3 = a1;
    }
}
```
Cevap: İki sınıf tanımı (`Araba`, `Main`) vardır. `new` ile iki
nesne oluşturulmuştur. `a3`, yeni nesne oluşturmaz; `a1` ile aynı
nesneye referans verir.
---
2. Encapsulation (Kapsülleme)
2.1. Kapsülleme nedir?
Kapsülleme, bir sınıfın verilerini ve bu veriler üzerinde çalışan
metotları bir arada tutmak ve nesnenin iç ayrıntılarına erişimi
kontrollü hâle getirmektir. Amaç, alanların her yerden gelişigüzel
değiştirilmesini önlemek ve kontrollü erişim sağlamaktır.
Örneğin yaş bilgisinin negatif girilmesini istemiyorsak alanı `private`
yapıp değer atamasını bir setter metodu üzerinden kontrol edebiliriz.
2.2. Erişim belirleyiciler
Java'da temel erişim belirleyiciler şunlardır:
---
Belirleyici                         Genel anlamı
---
`public`                            Her yerden erişime açıktır.
`private`                           Yalnızca tanımlandığı sınıfın
içinden erişilebilir.
`protected`                         Aynı paket içinden ve farklı
paketteki alt sınıflardan
erişilebilir.
Belirleyici yazılmaması             Aynı paket içinden erişilebilir.
(package-private)
PDF notu: `NYP_Hafta3.pdf` içinde `internal` da listelenmiştir.
`internal`, Java'nın erişim belirleyicisi değildir; C# dilinde
kullanılır. Java için yukarıdaki dört erişim seviyesi esas alınmalıdır.
2.3. Getter ve Setter
Getter: `private` alandaki değeri okumak için kullanılan
metottur.
Setter: `private` alana kontrollü biçimde değer atamak için
kullanılan metottur.
``` java
class Ogrenci {
    private String ad;
    private int yas;

    public String getAd() {
        return ad;
    }

    public void setAd(String yeniAd) {
        ad = yeniAd;
    }

    public int getYas() {
        return yas;
    }

    public void setYas(int yeniYas) {
        if (yeniYas >= 0) {
            yas = yeniYas;
        }
    }
}
```
Kullanımı:
``` java
Ogrenci ogr = new Ogrenci();
ogr.setAd("Deniz");
ogr.setYas(20);

String isim = ogr.getAd();
int yasBilgisi = ogr.getYas();
```
`yas` alanı `private` olduğu için sınıf dışından `ogr.yas = -5;`
şeklinde doğrudan erişilemez. Setter üzerinden kontrol uygulanabilir.
2.4. Kapsüllemenin faydaları
Veriye erişim kontrol altına alınır.
Geçersiz değer atamalarının önüne geçilebilir.
Sınıfın iç uygulama ayrıntıları gizlenebilir.
Kodun bakımı ve değiştirilmesi kolaylaşabilir.
Kendini dene
Encapsulation ne amaçla kullanılır?
`private` alanlara sınıf dışından doğrudan erişilebilir mi?
Getter ve Setter arasındaki fark nedir?
Setter içerisinde koşul kontrolü yapılabilir mi?
`protected` ile `private` arasındaki temel fark nedir?
---
3. Constructor (Yapıcı Metot)
3.1. Constructor nedir?
Constructor, bir sınıftan nesne oluşturulduğunda çalışan özel yapıcı
metottur. Genellikle nesnenin ilk değerlerini belirlemek için
kullanılır.
Constructor'ın: - Adı sınıf adıyla aynı olmalıdır. - Java'da dönüş tipi
yazılmaz; `void` da yazılmaz. - Nesne oluşturulurken çağrılır. -
Parametreli veya parametresiz biçimde tanımlanabilir. - Bir sınıfta
farklı parametre listelerine sahip birden fazla constructor bulunabilir.
``` java
class Ogrenci {
    String ad;
    int numara;

    Ogrenci() {
        ad = "Belirtilmedi";
        numara = 0;
    }
}
```
Nesne oluşturulması:
``` java
Ogrenci ogr = new Ogrenci();
```
`new Ogrenci()` çalıştığında parametresiz constructor çağrılır.
3.2. Parametreli constructor
``` java
class Ogrenci {
    String ad;
    int numara;

    Ogrenci(String ogrenciAdi, int ogrenciNo) {
        ad = ogrenciAdi;
        numara = ogrenciNo;
    }
}
```
Kullanımı:
``` java
Ogrenci ogr = new Ogrenci("Ece", 105);
```
Nesne oluşturulurken verilen değerler constructor parametrelerine
aktarılır.
3.3. `this` anahtar kelimesi
`this`, o anda işlem yapılan nesneyi ifade eder. Parametre adı ile alan
adı aynı olduğunda ayrım yapmak için sık kullanılır.
``` java
class Ogrenci {
    String ad;
    int yas;

    Ogrenci(String ad, int yas) {
        this.ad = ad;
        this.yas = yas;
    }
}
```
`this.ad`: Nesnenin alanı.
`ad`: Constructor'a gelen parametre.
`this.yas`: Nesnenin alanı.
`yas`: Parametre.
3.4. Default constructor ve parametresiz constructor
Programcı bir sınıfa hiçbir constructor yazmazsa Java derleyicisi
varsayılan parametresiz constructor'ı sağlar. Ancak programcı herhangi
bir constructor tanımlarsa derleyici otomatik varsayılan constructor'ı
artık eklemez.
``` java
class Araba {
    Araba(String marka) {
    }
}
```
Bu sınıfta `new Araba()` çağrısı hata verir; çünkü parametresiz
constructor tanımlanmamıştır. `new Araba("Toyota")` kullanılabilir.
3.5. Constructor overloading
Farklı parametre listeleriyle birden fazla constructor tanımlanabilir.
``` java
class Kitap {
    String ad;
    int sayfa;

    Kitap() {
        ad = "İsimsiz";
        sayfa = 0;
    }

    Kitap(String ad) {
        this.ad = ad;
        sayfa = 0;
    }

    Kitap(String ad, int sayfa) {
        this.ad = ad;
        this.sayfa = sayfa;
    }
}
```
Sık yapılan hata
Aşağıdaki tanım constructor değildir; çünkü `void` yazılmıştır. Bu,
dönüş tipi `void` olan normal bir metottur.
``` java
class Ogrenci {
    void Ogrenci() {
    }
}
```
Doğru constructor:
``` java
class Ogrenci {
    Ogrenci() {
    }
}
```
PDF notu: Ders PDF'sinde constructor için "void'tir ancak void
yazılmaz" ifadesi yer alıyor. Java açısından daha doğru ifade şudur:
Constructor'ın dönüş tipi yoktur; `void` yazılmaz. Ayrıca constructor'ın
mutlaka `public` olması gerekmez; erişim belirleyicisi ihtiyaca göre
seçilebilir.
Kendini dene
Constructor ne zaman çalışır?
Constructor'ın adı nasıl belirlenir?
Constructor neden dönüş tipi almaz?
Default constructor ne zaman otomatik sağlanır?
Parametreli constructor varsa `new Sinif()` çağrısı her zaman
çalışır mı?
`this` neyi gösterir?
---
4. Method Overloading (Metot Aşırı Yükleme)
4.1. Overloading nedir?
Aynı sınıf içerisinde aynı isimli birden fazla metot tanımlanmasına,
metotların parametre listeleri farklı olmak şartıyla, Method
Overloading denir.
Parametre listesi şu şekillerde farklı olabilir: - Parametre sayısı -
Parametre türleri - Parametrelerin sırası
``` java
class Hesap {
    int topla(int a, int b) {
        return a + b;
    }

    int topla(int a, int b, int c) {
        return a + b + c;
    }

    double topla(double a, double b) {
        return a + b;
    }
}
```
Üç metot da `topla` adını taşır; ancak parametre listeleri farklıdır.
4.2. Yalnızca dönüş tipini değiştirmek yeterli mi?
Hayır. Metotların parametre listesi aynıysa yalnızca dönüş tipini
değiştirmek overloading oluşturmaz.
Hatalı örnek:
``` java
class Ornek {
    int hesapla(int a) {
        return a;
    }

    double hesapla(int a) {
        return a;
    }
}
```
Bu kod derleme hatası verir.
4.3. Hangi metot çağrılır?
Java, metot çağrısındaki argümanların tür ve sayısına uygun metodu
seçer.
``` java
class Yazdir {
    void yaz(int x) {
        System.out.println("int");
    }

    void yaz(double x) {
        System.out.println("double");
    }

    void yaz(String x) {
        System.out.println("String");
    }
}
```
Örnek çağrılar: - `yaz(5)` → `int` - `yaz(5.5)` → `double` -
`yaz("Merhaba")` → `String`
Kendini dene
Method Overloading nedir?
Parametre sayısı değiştirilerek overloading yapılabilir mi?
Parametre türü değiştirilerek overloading yapılabilir mi?
Yalnızca dönüş tipini değiştirmek yeterli midir?
Aşağıdaki çağrı hangi metodu seçer?
``` java
void test(int x) { }
void test(double x) { }
void test(String x) { }

// test(8);
```
---
5. Array (Dizi)
5.1. Dizi nedir?
Dizi, aynı türden birden fazla değeri tek bir değişken adı altında
tutmaya yarayan veri yapısıdır. Dizi oluşturulurken uzunluğu belirlenir
ve sonradan değiştirilemez.
``` java
int[] sayilar = new int[5];
```
Bu ifade 5 elemanlı bir `int` dizisi oluşturur. İndeksler `0` ile `4`
arasındadır.
Diziye başlangıç değerleriyle de değer verilebilir:
``` java
int[] notlar = {70, 85, 90, 60, 100};
```
5.2. Elemanlara erişme
``` java
int ilkNot = notlar[0];
notlar[1] = 95;
```
Dizilerde indeksleme sıfırdan başlar. Var olmayan bir indekse erişmek
çalışma zamanında `ArrayIndexOutOfBoundsException` hatasına neden olur.
5.3. Dizi uzunluğu
Dizinin eleman sayısı `length` alanıyla öğrenilir:
``` java
int adet = notlar.length;
```
`length` bir metot değildir; parantez kullanılmaz.
5.4. Dizi üzerinde döngü
``` java
int[] sayilar = {3, 6, 9, 12};
int toplam = 0;

for (int i = 0; i < sayilar.length; i++) {
    toplam += sayilar[i];
}
```
Döngü, indeksleri sırasıyla dolaşır ve elemanları toplar.
5.5. En büyük elemanı bulma
``` java
int[] sayilar = {14, 7, 28, 3, 19};
int enBuyuk = sayilar[0];

for (int i = 1; i < sayilar.length; i++) {
    if (sayilar[i] > enBuyuk) {
        enBuyuk = sayilar[i];
    }
}
```
İlk eleman başlangıçta en büyük kabul edilir. Diğer elemanlar
incelenerek daha büyük bir değer bulunduğunda değişken güncellenir.
5.6. Varsayılan değerler
Java'da dizi oluşturulduğunda elemanlar türlerine göre varsayılan değer
alır: - `int` → `0` - `double` → `0.0` - `boolean` → `false` - Referans
türleri → `null`
Kendini dene
Dizi nedir?
Dizi indeksleri kaçtan başlar?
`length` ne verir?
Dizi uzunluğu oluşturulduktan sonra değiştirilebilir mi?
`int[] a = new int[4];` dizisinin elemanları başlangıçta hangi
değerdedir?
`a[4]` erişimi neden hatalıdır?
---
6. ArrayList
6.1. ArrayList nedir?
`ArrayList`, Java'da eleman sayısı ihtiyaç oldukça artıp azalabilen bir
liste yapısıdır. Array'den farklı olarak sabit uzunlukla çalışmak
zorunda değildir.
Kullanmak için `java.util.ArrayList` sınıfı gerekir. Bu bölümde yalnızca
veri yapısı ve metotları ele alınmaktadır; I/O konusu değildir.
``` java
import java.util.ArrayList;

ArrayList<String> isimler = new ArrayList<>();

isimler.add("Ali");
isimler.add("Ayşe");
isimler.add("Deniz");
```
6.2. Temel ArrayList metotları
---
Metot                               Görevi
---
`add(eleman)`                       Listenin sonuna eleman ekler.
`get(indeks)`                       Belirtilen indeksteki elemanı
döndürür.
`set(indeks, eleman)`               Belirtilen indeksteki elemanı
değiştirir.
`remove(indeks)`                    Belirtilen indeksteki elemanı
siler.
`size()`                            Listedeki eleman sayısını döndürür.
`contains(eleman)`                  Elemanın listede bulunup
bulunmadığını kontrol eder.
Örnek:
``` java
ArrayList<String> meyveler = new ArrayList<>();

meyveler.add("Elma");
meyveler.add("Armut");
meyveler.add("Muz");

String ikinci = meyveler.get(1); // Armut
meyveler.set(1, "Kiraz");        // Armut yerine Kiraz
meyveler.remove(0);              // Elma silinir

int adet = meyveler.size();
```
Son durumda liste `["Kiraz", "Muz"]` olur ve `size()` değeri `2`
döndürür.
6.3. Array ve ArrayList karşılaştırması
---
Array                               ArrayList
---
Uzunluğu oluşturulurken belirlenir. Eleman sayısı değişebilir.
`length` kullanılır.                `size()` kullanılır.
İlkel türleri doğrudan tutabilir.   Genel kullanımda nesne türleri
tutar; `Integer`, `Double` gibi
sarmalayıcı türler kullanılır.
İndeks ile elemana erişilir.        İndeks ile elemana erişilir.
Örnek: `ArrayList<int>` geçerli değildir; `ArrayList<Integer>`
kullanılır.
Kendini dene
ArrayList'in Array'den temel farkı nedir?
`add()` ne yapar?
`get(2)` ne döndürür?
`set()` ile `remove()` arasındaki fark nedir?
Array'de uzunluk, ArrayList'te eleman sayısı nasıl öğrenilir?
`ArrayList<int>` neden geçerli değildir?
---
7. Inheritance (Kalıtım)
7.1. Kalıtım nedir?
Kalıtım, bir sınıfın başka bir sınıfın erişilebilir özellik ve
metotlarını devralarak yeni bir sınıf oluşturmasını sağlar. Amaç ortak
özellikleri tekrar tekrar yazmamak ve sınıflar arasında bir üst
sınıf-alt sınıf ilişkisi kurmaktır.
Üst sınıf (superclass): Özellikleri devralınan sınıf.
Alt sınıf (subclass): Üst sınıftan türetilen sınıf.
Java'da sınıf kalıtımı `extends` ile belirtilir.
``` java
class Hayvan {
    String ad;

    void hareketEt() {
        System.out.println("Hareket ediyor");
    }
}

class Kedi extends Hayvan {
    void miyavla() {
        System.out.println("Miyav");
    }
}
```
Kullanımı:
``` java
Kedi kedi = new Kedi();
kedi.ad = "Tekir";
kedi.hareketEt();
kedi.miyavla();
```
`Kedi`, `Hayvan` sınıfından türediği için erişilebilir `ad` alanını ve
`hareketEt()` metodunu kullanabilir. Ayrıca kendi `miyavla()` metoduna
sahiptir.
7.2. `super` anahtar kelimesi
`super`, alt sınıftan üst sınıfın üyelerine veya constructor'ına erişmek
için kullanılır.
Üst sınıf constructor'ını çağırma:
``` java
class Hayvan {
    String ad;

    Hayvan(String ad) {
        this.ad = ad;
    }
}

class Kedi extends Hayvan {
    Kedi(String ad) {
        super(ad);
    }
}
```
`super(ad)` üst sınıfın parametreli constructor'ını çağırır. Java'da
constructor içindeki `super(...)` çağrısı ilk ifade olmalıdır.
7.3. Kalıtımda erişim
`public` üyeler erişim kurallarına uygun biçimde kullanılabilir.
`protected` üyeler alt sınıflar tarafından erişilebilir.
`private` üyeler alt sınıf tarafından doğrudan erişilemez.
Üst sınıfın constructor'ı alt sınıftan nesne oluşturulurken
constructor zinciri içinde çalışır.
7.4. Java'da çoklu sınıf kalıtımı
Java'da bir sınıf doğrudan birden fazla sınıfı `extends` ile miras
alamaz. Bir sınıf tek bir sınıfı genişletebilir. Birden fazla arayüz
(interface) uygulayabilmesi ayrı bir konudur.
Kendini dene
Inheritance nedir?
`extends` ne işe yarar?
Üst sınıf ve alt sınıf ne demektir?
`super` hangi amaçlarla kullanılır?
Alt sınıf `private` alanlara doğrudan erişebilir mi?
Java'da bir sınıf iki sınıfı aynı anda `extends` edebilir mi?
---
8. Method Overriding (Metot Ezme)
8.1. Overriding nedir?
Overriding, alt sınıfın üst sınıftan devraldığı bir metodu kendi
ihtiyacına uygun biçimde yeniden tanımlamasıdır. Metot imzası (metot adı
ve parametre listesi) üst sınıftaki metotla uyumlu olmalıdır.
``` java
class Hayvan {
    void sesCikar() {
        System.out.println("Hayvan sesi");
    }
}

class Kedi extends Hayvan {
    @Override
    void sesCikar() {
        System.out.println("Miyav");
    }
}
```
``` java
Hayvan h = new Kedi();
h.sesCikar();
```
Bu çağrıda nesnenin gerçek türü `Kedi` olduğu için `Kedi` sınıfındaki
override edilmiş metot çalışır. Bu davranış çalışma zamanı çok
biçimliliğinin (polymorphism) temel örneklerindendir.
8.2. `@Override` ne işe yarar?
`@Override`, metodu bilerek üst sınıftaki bir metodu ezmek amacıyla
yazdığımızı belirtir. Derleyicinin yanlış imzayı fark etmesine yardımcı
olur. Kullanılması önerilir.
8.3. Overloading ve Overriding farkı
---
Overloading                         Overriding
---
Aynı isimli metotların parametre    Alt sınıf, üst sınıftaki metodu
listeleri farklıdır.                yeniden tanımlar.
Kalıtım zorunlu değildir.           Sınıflar arasında kalıtım ilişkisi
gerekir.
Parametre sayısı/türü/sırası farklı Metot imzası uyumlu olmalıdır.
olabilir.
Derleme zamanında uygun metot       Nesnenin gerçek türüne göre çalışma
seçilir.                            zamanında metot seçimi yapılır.
Kendini dene
Overriding nedir?
Override için kalıtım ilişkisi gerekir mi?
`@Override` ne işe yarar?
Overloading ve Overriding arasındaki iki farkı yaz.
`Hayvan h = new Kedi();` ifadesinde `h.sesCikar()` çağrısında hangi
metot çalışır?
---
9. Exception Handling (İstisna Yönetimi)
9.1. Exception nedir?
İstisnalar (exceptions), program çalışırken normal akışı bozan anormal
durumlardır. Java'da istisna yönetimi temel olarak `try`, `catch` ve
`finally` bloklarıyla yapılır.
Örneğin sıfıra bölme veya olmayan bir dizi indeksine erişme çalışma
zamanında istisna oluşturabilir.
9.2. try-catch
`try`: İstisna oluşma ihtimali bulunan kod yazılır.
`catch`: Belirtilen türde istisna oluşursa çalıştırılacak kod
yazılır.
``` java
class Ornek {
    public static void main(String[] args) {
        try {
            int sonuc = 10 / 0;
        } catch (ArithmeticException e) {
            System.out.println("Aritmetik hata oluştu");
        }
    }
}
```
Sıfıra bölme nedeniyle `ArithmeticException` oluşur ve ilgili `catch`
bloğu çalışır.
9.3. finally
`finally` bloğu, normal tamamlanma veya yakalanan istisna gibi olağan
kontrol akışlarında genellikle çalıştırılır. İstisna oluşsa da oluşmasa
da yürütülmesi beklenen temizlik işlemleri için kullanılır.
``` java
try {
    int sonuc = 10 / 2;
} catch (ArithmeticException e) {
    System.out.println("Hata");
} finally {
    System.out.println("Finally çalıştı");
}
```
9.4. Birden fazla catch
Farklı istisna türleri için birden fazla `catch` yazılabilir.
``` java
try {
    int[] sayilar = {10, 20};
    int sonuc = sayilar[3];
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Dizi indeksi hatalı");
} catch (Exception e) {
    System.out.println("Başka bir istisna oluştu");
}
```
Daha özel istisna türleri, daha genel türlerden önce yazılmalıdır. Çünkü
`Exception` gibi genel bir tür önce yazılırsa altındaki daha özel
`catch` bloklarına ulaşılamaz ve derleme hatası oluşur.
Kendini dene
Exception nedir?
`try` bloğunun görevi nedir?
`catch` hangi durumda çalışır?
`finally` ne amaçla kullanılır?
Birden fazla `catch` yazılabilir mi?
Daha genel `Exception` catch bloğu neden genellikle sona yazılır?
---
10. Abstract Class ve Abstract Method
10.1. Abstract class nedir?
Abstract class (soyut sınıf), doğrudan nesnesi oluşturulamayan ve
genellikle ortak özellikleri tanımlamak veya alt sınıflara bir şablon
sunmak için kullanılan sınıftır.
``` java
abstract class Sekil {
    abstract double alanHesapla();
}
```
Bu sınıftan doğrudan `new Sekil()` ile nesne oluşturulamaz.
10.2. Abstract method nedir?
Abstract method, gövdesi bulunmayan ve alt sınıfların gerçekleştirmesi
beklenen metottur. Java'da abstract metot tanımı noktalı virgülle biter.
``` java
abstract class Sekil {
    abstract double alanHesapla();
}
```
10.3. Alt sınıfta abstract metodu gerçekleştirme
``` java
abstract class Sekil {
    abstract double alanHesapla();
}

class Dikdortgen extends Sekil {
    double en;
    double boy;

    Dikdortgen(double en, double boy) {
        this.en = en;
        this.boy = boy;
    }

    @Override
    double alanHesapla() {
        return en * boy;
    }
}
```
`Dikdortgen`, abstract olmayan somut bir sınıf olduğu için üst sınıftaki
abstract metodu gerçekleştirmelidir.
10.4. Abstract class içinde neler bulunabilir?
Abstract class: - Normal alanlar (field) içerebilir. - Constructor
içerebilir. - Gövdeli normal metotlar içerebilir. - Abstract metotlar
içerebilir.
Bir abstract class'ın mutlaka abstract metot içermesi gerekmez. Ancak
abstract metot içeren bir sınıf abstract olarak tanımlanmalıdır.
Kendini dene
Abstract class nedir?
Abstract sınıftan doğrudan nesne oluşturulabilir mi?
Abstract method'un gövdesi bulunur mu?
Alt sınıf abstract metodu gerçekleştirmek zorunda mıdır?
Abstract class normal metot içerebilir mi?
Abstract class constructor içerebilir mi?
---
11. Sık Karıştırılan Kavramlar
11.1. Class -- Object
Class: Şablon/tanım.
Object: Sınıftan oluşturulan örnek.
11.2. Constructor -- Normal metot
---
Constructor                         Normal metot
---
Sınıfla aynı adı taşır.             İstediğimiz geçerli bir adı
olabilir.
Dönüş tipi yazılmaz.                Dönüş tipi belirtilir (`void`
dahil).
Nesne oluşturulurken çağrılır.      Çağrıldığı zaman çalışır.
İlk değer atamak için sık           Bir davranışı/işlemi
kullanılır.                         gerçekleştirir.
11.3. Getter -- Setter
Getter değeri okur.
Setter değeri değiştirir veya değiştirmeyi kontrol eder.
11.4. Array -- ArrayList
Array sabit uzunlukludur ve `length` kullanır.
ArrayList dinamik eleman sayısına sahiptir ve `size()` kullanır.
11.5. Overloading -- Overriding
Overloading: Aynı isim, farklı parametre listesi.
Overriding: Alt sınıfta miras alınan metodun yeniden tanımlanması.
11.6. Abstract class -- Normal class
Normal sınıftan nesne oluşturulabilir (sınıfın erişim ve constructor
koşulları uygunsa).
Abstract sınıftan doğrudan nesne oluşturulamaz.
Abstract sınıf ortak davranış ve zorunlu alt sınıf davranışları
tanımlayabilir.
11.7. `this` -- `super`
`this`: Mevcut nesneyi ifade eder.
`super`: Üst sınıfın üyelerine veya constructor'ına erişmek için
kullanılır.
---
12. Sınav Öncesi Kontrol Listesi
Her maddeyi kendi başına açıklayabiliyor veya kod üzerinde
uygulayabiliyorsan tamamlandı olarak işaretle.
[ ] Class ve Object arasındaki farkı açıklayabiliyorum.
[ ] `new` ile nesne oluşturabiliyorum.
[ ] Field ve method ayrımını yapabiliyorum.
[ ] Referans değişkenlerinin aynı nesneyi gösterebildiğini
biliyorum.
[ ] `public`, `private`, `protected` erişimlerini ayırt
edebiliyorum.
[ ] Getter ve Setter yazabiliyorum.
[ ] Parametresiz ve parametreli constructor yazabiliyorum.
[ ] Constructor ile normal metot arasındaki farkı biliyorum.
[ ] Constructor overloading yapabiliyorum.
[ ] Method overloading kurallarını biliyorum.
[ ] Array oluşturup indeksleriyle işlem yapabiliyorum.
[ ] Array ile ArrayList farkını biliyorum.
[ ] ArrayList'in `add`, `get`, `set`, `remove`, `size` metotlarını
kullanabiliyorum.
[ ] `extends` ile kalıtım kurabiliyorum.
[ ] `this` ve `super` farkını biliyorum.
[ ] Override yapabiliyorum.
[ ] Overloading ve Overriding farkını açıklayabiliyorum.
[ ] try-catch-finally akışını yorumlayabiliyorum.
[ ] Abstract class ve abstract method tanımlayabiliyorum.
---
13. Karma Alıştırmalar
Önce soruları cevaplamaya çalış. Ardından cevap anahtarını kontrol et.
A. Teorik sorular
Sınıf ve nesne arasındaki fark nedir?
Java'da sınıf türündeki değişkenler neyi tutar?
`private` değişkenlere kontrollü erişim hangi metotlarla sağlanır?
Constructor'ın dönüş tipi nedir?
Programcı bir constructor yazarsa derleyici otomatik parametresiz
constructor ekler mi?
Overloading için yalnızca dönüş tipinin değişmesi yeterli midir?
Array indeksleri kaçtan başlar?
Array ile ArrayList'in uzunluk yönetimi nasıl farklıdır?
Kalıtım hangi anahtar kelimeyle kurulur?
Override için alt sınıfın üst sınıftan türemiş olması gerekir mi?
Abstract sınıftan doğrudan nesne oluşturulabilir mi?
`finally` bloğunun temel amacı nedir?
B. Kod çıktısı / yorumlama
Soru 1
``` java
class Kisi {
    String ad = "Ada";
}

class Main {
    public static void main(String[] args) {
        Kisi k1 = new Kisi();
        Kisi k2 = k1;
        k2.ad = "Ece";
        // k1.ad değeri nedir?
    }
}
```
Soru 2
``` java
class Deneme {
    Deneme() {
        // A
    }

    Deneme(int x) {
        // B
    }
}
```
`new Deneme(5)` hangi constructor'ı çağırır?
Soru 3
``` java
class Hesap {
    int topla(int a, int b) {
        return a + b;
    }

    int topla(int a, int b, int c) {
        return a + b + c;
    }
}
```
`topla(2, 3, 4)` çağrısının sonucu nedir?
Soru 4
``` java
int[] a = {4, 8, 12};
int toplam = 0;

for (int i = 0; i < a.length; i++) {
    toplam += a[i];
}
```
`toplam` kaç olur?
Soru 5
``` java
class A {
    void yaz() {
        System.out.println("A");
    }
}

class B extends A {
    @Override
    void yaz() {
        System.out.println("B");
    }
}
```
`A nesne = new B(); nesne.yaz();` çağrısında hangi metot çalışır?
C. Kod yazma
`Ogrenci` sınıfı oluştur. `ad` ve `yas` alanlarını `private`
tanımla. Getter ve Setter metotlarını yaz.
`Araba` sınıfına parametresiz ve `marka` parametreli iki constructor
ekle.
Aynı isimli, iki ve üç parametre alan `topla` metotlarını yaz.
Beş elemanlı bir `int` dizisindeki sayıların toplamını bulan kodu
yaz.
`Hayvan` üst sınıfı ve ondan türeyen `Kedi` alt sınıfı oluştur.
`sesCikar()` metodunu alt sınıfta override et.
`Sekil` abstract sınıfı ve `alanHesapla()` abstract metodunu
oluştur. `Dikdortgen` sınıfında metodu gerçekleştir.
Sıfıra bölme hatasını `try-catch` ile yakalayan bir örnek yaz.
---
14. Karma Alıştırmalar -- Cevap Anahtarı
A. Teorik cevaplar
Class şablondur; object o sınıftan oluşturulan örnektir.
Nesneye ulaşmayı sağlayan referansı tutarlar.
Getter ve Setter metotlarıyla.
Constructor'ın dönüş tipi yoktur; `void` yazılmaz.
Hayır. Programcı bir constructor tanımladıysa otomatik varsayılan
constructor eklenmez.
Hayır. Parametre listesi farklı olmalıdır.
Sıfırdan başlar.
Array sabit uzunlukludur; ArrayList'in eleman sayısı değişebilir.
`extends`.
Evet, override kalıtım ilişkisi içinde yapılır.
Hayır.
Olağan kontrol akışında istisna oluşsa da oluşmasa da yürütülmesi
beklenen kodları çalıştırmaktır.
B. Kod cevapları
`"Ece"`; çünkü `k1` ve `k2` aynı nesneye referans verir.
Parametreli `Deneme(int x)` constructor'ı, yani B.
`9`.
`24`.
`B` sınıfındaki override edilmiş metot çalışır.
C. Kod yazma soruları için kontrol ölçütleri
Alanlar `private` olmalı; getter değer döndürmeli, setter değer
atamalı.
Constructor adı `Araba` olmalı; dönüş tipi yazılmamalı.
Metot isimleri aynı, parametre listeleri farklı olmalı.
Döngü sınırı `i < dizi.length` olmalı; toplam değişkeni sıfırdan
başlamalı.
`Kedi extends Hayvan` olmalı ve metot imzası uyumlu biçimde override
edilmeli.
`Sekil` abstract olmalı; somut `Dikdortgen` sınıfı abstract metodu
gerçekleştirmeli.
Bölme işlemi `try` içinde, `ArithmeticException` yakalama işlemi
`catch` içinde olmalı.
---
Son Hatırlatmalar
Kod sorularında önce sınıf ilişkisini, sonra metot imzalarını ve en
son kodun çalışma sırasını incele.
Dizi sorularında indeksin `0`'dan başladığını unutma.
Constructor tanımında dönüş tipi yazma.
Overloading sorularında parametre listelerini karşılaştır.
Overriding sorularında üst sınıf-alt sınıf ilişkisini kontrol et.
`private` alanlara sınıf dışından doğrudan erişilemeyeceğini unutma.
Abstract sınıflardan doğrudan nesne oluşturulamaz.
Öğretmeniniz I/O konusunu kapsam dışında bıraktığı için bu notlarda
I/O alıştırması bulunmamaktadır.
Önerilen çalışma sırası: Önce 1--3. bölümleri öğren; ardından 4--6.
bölümleri çalış; sonra 7--10. bölümleri tamamla. Son olarak 11--14.
bölümleri kullanarak kendini sınav formatında test et.
