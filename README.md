Bir yazılımcının sık sık karşılaştığı hatalardan birisidir "NullPointerException". Bu hata Java 8 ile önlenebilir hale gelmiştir.
Bu repository de Optional sınıfını inceleyeceğiz.

Optional sınıfı 15 adet metot barındırmaktadır. İşte bu metotlar sayesinde NullPointerException hatasının önüne geçebiliyoruz. Hadi gelin işimizi kolaylaştıran bu 15 metottan 11 tanesini tanıyalım.

İlk metodumuz "of" metodu: <br />
Of metodu optional türde olmayan herhangi bir nesneyi optional türüne çevirmek için kullanıyoruz. Bir nesneye bir değer atamamız gerekiyor tabiki. NullPointerException hatası ile karşılaşmak istiyorsak of metodumuzun içerisine null değerini atamamız gerekiyor.
Hadi gelin örnek ile daha iyi pekiştirelim :)

  ```ruby
Optional<String> elma = Optional.of("Kırmızı elma");
```

İkinci metodumuz "ofNullable" metodu: <br />
ofNullable metodu Optional türde olmayan bir nesneyi Optional türüne çevirmek için kullanırız. Adından da anlaşıldığı üzere nesneye atanan değer null olabilir. ofNullable metodunu of metodundan ayıran özelliği de null değer verdiğimiz zaman NoSuchElementException hatası ile karşılaşabiliriz.

Üçüncü metodumuz "get" metodu: <br />
get metodu Optional sınıfı içerisinde oluşturulan generic(T) tipindeki nesneye ulaşmak için kullanırız.
 Örnek verecek olursak da az önce oluşturduğumuz elma nesnesini ekrana yazdıralım.
   ```ruby
   System.out.println(elma.get());
```
	
Dördüncü metodumuz "empyt" metodu:<br />
empyt metodu boş bir optional nesnesi oluşturmamıza olanak sağlıyor. <br />
Hadi gelin boş bir nesne oluşturalım.
   ```ruby
   Optional<String> elma = Optional.empyt();
```
Not: Boş bir optional nesnesini get etmeye kalkarsak NoSuchElementException hatası ile karşılaşırız. Bu hata ile karşılaştığınızda bilin ki nesneye herhangi bir değer atamamış olmalısınız.

Beşinci metodumuz "ifPresent" metodu: <br />
ifPresent metodu optional türde bir nesne için tanımlıysa içerisinde işlem yapmasına izin verir. Örnek olarak: 
```ruby
List<String> list = new ArrayList<>();
list.add("Seyit Uludağ");
list.add("Emirhan Doğandemir");
list.add("Sahil Rzayev");
Optional<List<String>> optList = Optional.of(list);
optList.ifPresent(System.out::println);
```

Altıncı metodumuz "isPresent" metodu: <br />
isPresent  metodu optional türde olan bir nesnenin tanımlı olup olmadığını gösterir bize. Tanımlı ise bize "true" değerini değil ise de "false" değerini döndürür.
Örneğimiz de şu şekilde:
   ```ruby
   Optional<String> chuck = Optional.of("Chuck Norris");
System.out.println(chuck.isPresent() ? "Chuck" : "Norris");
```

Yedinci metodumuz "map" metodu: <br />
map metodu optional türdeki nesne üzerinde işlemler yapmamıza yardımcı oluyor. Örnek: <br />
  ```ruby
List<String> meyveler = new ArrayList<>();
meyveler.add("Elma");
meyveler.add("Armut");
Optional<List<String>> optList = Optional.of(meyveler);
optList.map(List::size).get();
System.out.println(optList);
```
Sekizinci metodumuz "filter" metodu: <br />
filter metodu optional türdeki nesne üzerinde filtreleme yapmamıza yardımcı oluyor. Örnek: <br />
  ```ruby
Optional<String> elma = Optional.of("Kırmızı elma");
elma.filter(e -> "Kırmızı elma".equals(e)).ifPresent(System.out::println);
```

Dokuzuncu metodumuz "orElse" metodu: <br />
orElse metodu optional türde oluşturulan nesne ister tanımlı ister tanımlı olmasız bize verilen değeri döndürür. Örnek: <br />
  ```ruby
  private static String testOrElse(){
    System.out.println("Yeşil ışık");
}

  Optional<String> kımızıİsik = Optional.of("Kırmızı ışık");
System.out.println(chuck.orElse(testOrElse()));
```
Bu örnekde konsola ilk önce "Yeşil ışık" değerini ondan sonra ise "Kırmızı ışık" değerini dönecektir.

Onuncu metodumuz "orElseGet" metodu: <br />
orElseGet metodu yukarıdaki orElse methodundan farklı olarak orElse içerisindeki değer Optional’ın empty olup olmasına bakmaksızın direk çalışır. orElseGet ise Optional empty ise çalışır. <br /> <br />
Onbirinci metodumuz "orElseThrow" metodu: <br />
orElseGet metodu Optional türde oluşturulan bir nesne için gerekli durumda exception fırlatır. Örnek olarak: <br />
```ruby
Optional<String> str = Optional.empty();
System.out.println(str.orElseThrow(IllegalArgumentException::new));
```

## Stream() Method

```ruby
public Stream<T> stream()
```
Parametreler: Stream metodu herhangi bir parametre kabul etmez. <br />
Dönüş Değeri: Stream metodu isteğe bağlı örnekte bulunan tek değerin sıralı akışını döndürür. Bu İsteğe bağlı örnekte hiçbir değer yoksa, bu yöntem boş bir Stream döndürür.

Kod Parçacığı 1 :
```ruby
// Nesneyi Optional nesnesine dönüştürüyoruz
        Optional<Integer> op = Optional.of(9455);
  
// Değeri ekrana yazdırıyoruz
        System.out.println("Optional: " + op);
  
// Streami almak
        System.out.println("Stream:");
        op.stream().forEach(System.out::println);
```
Çıktı:
```ruby
Optional: Optional[123]
Stream:
123
```

Kod Parçacığı 2 :
```ruby
// Nesneyi Optional nesnesine dönüştürüyoruz
        Optional<Integer> op = Optional.empty();
  
// Değeri ekrana yazdırıyoruz
        System.out.println("Optional: " + op);
  
 try {
  
            // Streami almak
            System.out.println("Stream: ");
            op.stream().forEach(System.out::println);
        }
        catch (Exception e) {
            System.out.println(e);
        }

```
Çıktı:
```ruby
Optional: Optional.empty
Stream: 
```
