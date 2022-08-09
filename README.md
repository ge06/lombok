# Lombok

## Nedir?

Kod tekrarını önlemek için oluşturulmuş bir kütüphanedir.

## Özellikleri

### `@Getter` ve `@Setter` Annotation

Tüm değişkenler için getter ve setter metodları oluşturur.

### `@AllArgsConstructor`, `@NoArgsConstructor` ve `@RequiredArgsConstructor`

RequiredArgsConstructor final ve @NonNull annotasyonuna sahip değişkenler için yapıcı metot oluştururken, AllArgsConstructor tüm değişkenleri parametre alan bir yapıcı metot ve NoArgsConstructor boş yapıcı metot oluşturmak için kullanılır.

### `@EqualsAndHashCode`

EqualsAndHashCode metodunu oluşturmak için kullanılır. Bu metod içerisinde yer almasını istemediğimiz değişkenler `@EqualsAndHashCode.Exclude` annotasyonu eklenmeli veya sınıfa `@EqualsAndHashCode(exclude = {"variable1", "variable2"})` şeklinde eklenmelidir. İstenilen metodlar veya değişkenler ile bir EqualsAndHashCode metodu oluşturmak isteniyorsa bu durumda `@EqualsAndHashCode.Include` eklenebilir veya `@EqualsAndHashCode(of = {"variable1", "variable2"})` şeklinde çoklu kullanılabilir.

### `@NonNull`

Bir değişken NonNull olarak işaretlenmişse Lombok null olması durumunda parametre adıyla NullPointerException hatası fırlatacaktır.

### `@Synchronized`

Instance method(Örnek metot)-Bir nesne oluşturulduğunda çağırılabilen- ve statik metotlar için kullanılır. Tüm metodlara lock değişkeni ekler(Statik için LOCK, örnek metotlar için lock).
```
import lombok.Synchronized;

public class SynchronizedExample {
  private final Object readLock = new Object();
  
  @Synchronized
  public static void i_am_a_static_method() {
    System.out.println("world");
  }
  
  @Synchronized
  public int i_am_an_instance_method() {
    return 42;
  }
  
  @Synchronized("readLock")
  public void foo() {
    System.out.println("bar");
  }
}
```

### `@ToString`

toString metodunu kullanmak amacıyla kullanılır. EqualsAndHashCode kullanımı gibi hariç veya dahil edilmesi istenen değişkenler belirlenebilir.

### `@Data`

@ToString, @EqualsAndHashCode, @Getter / @Setter and @RequiredArgsConstructor annotasyonlarının tümünü barındıran, bir pojo oluşturmak için rahatlıkla kullanılabilecek bir annotasyon.

### `@Value`

@Data annotasyonunun private ve final olması ve buna ek olarak setter olmamasıdır. Yani bu annotasyon immutable bir sınıf oluşturmanın kısayolu denebilir.

### `@With`

Immutable özelliğini korumak amacıyla setter yerine değişken değiştiğinde yeni bir sınıf dönen yapıdır.

### `@Getter(lazy=true)`

private final olarak tanımlanan değişkenler için bir kez çağırılan sonrasında belleğe alınarak kullanılan annotasyondur. Hesaplanan değerler için tekrar kullanım olduğunda kullanılabilir.

## Avantajlar ve Dezavantajlar

### Avantajlar
- Hızlı geliştirme sağlar
- Düzenli ve temiz kod yapısı
- Uzun süredir kullanılan bir kütüphane

### Dezavantajlar
- Takımlar çoğunlukla delomboking(Annotasyonların işlenmesi sonucu oluşturulan java kodları) işleminin java compiler a bağımlı olduğu ve aynı sonucun garanti edilemediği sebebiyle bu kütüphaneye uzak davranmaktadır. 
- Bazen IDE'lerden kaynaklanan getter setter eksikliği olabilmektedir.
- Kurumda yapılan işler gereği bazen get set üzerinde iş mantıkları olabiliyor veya get ve set üzerinde debug yapılması gerekebiliyor. Bu durumda lombok un doğru ve tam derlenmesine bağımlı hale gelinmektedir.
- Lombokta derlenen kodlar javadoc üzerinde görülememektedir. 
