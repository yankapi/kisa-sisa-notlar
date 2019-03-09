# GO NOTLARIM

## Hello World

Geleneksel hello world programı

```go
// tek satırlık yorum satırı.

/*
çok satırlık yorum satırları.
*/

// programın ana paketi
package main

// fmt paketini import ediyoruz
import "fmt"

// main programı. Program buradan çalışmaya başlar.
func main() {
    // ekrana "hello world" yazdırır.
    fmt.Println("hello world")
}
```

Terminalden programımızı çalıştıralım.

```bash
$ go run hello-world.go
hello world

$ go build hello-world.go
$ ls
hello-world hello-world.go

$ ./hello-world
hello world
```

* `go run` programı derler ve çalıştırır. Fakat derlenmiş dosyayı kaydetmez.
* `bo build` programı derler ve derlenmiş dosyayı kaydeder.

## Paketler

Her go programı paketlerden oluşur. Programlar main paketinden çalışmay başlar. Ayrıca go biçok pakete sahiptir. Bu paketleri `import` ile programımıza dahil edebiliriz.

```go
// paketleri ayrı ayrı dahil et
import "fmt"
import "math"

// paketleri tek import ile programa dahil et.
import (
    "fmt"
    "math"
)
```

Aynı şekilde paketlerdeki isimleri içe aktardığımız gibi dışa katarmakta vardır. Dışa aktaracağımız isimlerin ilk harfini büyük harfle başlaması gerekir. örneğin `math.Pi` de olduğu gibi.

## Değişkenler ve Değerler

`var` anahtar kelimesi değişken tanımlamaya yarar. Tür bilgisi değişkenin sonuna yazılır.

```go
// tek değişken tanımlanırken.
var a int

// aynı türde çok değişken tanımlanırken
var c, python, java int

// değişkenleri ilklendirme
var i, j int = 1, 2
var x, y = 2, 4

// değişkende ilklendirme varsa o zaman tip belirtimi atlanabilir.
// Bu durumda değişkenin türü ilklendirme türü ile aynı olacaktır
x := 3
// Dikkat!!! fonksiyon alanı dışında kullanılamaz.
// main de bir fonksiyon alanıdır.

// birden çok değişkeni tanımlamanın başka bir yolu
var (
    ToBe   bool   = false
    MaxInt uint64 = 1<<64 - 1
)
```

### Değişlen Türleri

Go çesitli veri tiplerine sahiptir. Go dili statik bir dildir. Yani değişkenin tipi sabittir değiştirilemez.

```text
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // diğer adıyla uint8

rune // diğer adıyla int32
     // Unicode karakter kodlarını ifade eder

float32 float64

complex64 complex128
```

* `int*` türleri işaretli sayılardır. -2 2 -4 6 gibi.
* `uint*` tipleri ise işaretsiz yani pozitif sayılardır. 0 1 2 5 gibi.
* `int` `uint` `uintptr` platform bağımlı tiplerdir. Makinenin çalıştığı platforma göre değişir.
* `NaN` Not a number.( 0/0 durumlarında). (sonsuzluk durumlarında).

Ayrıca bu değişkenlerin kendilerine ait "sıfır değerleri" vardır. Bu değerler şunlardır:

* `0` Sayı türleri için.
* `false` mantıksal (boolean) türü için.
* `""` string türü için.

### Tür Dönüşümleri

T(v) ifadesi v değerini T türüne dönüştürür.

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```

### Sabitler

Sabitler `const` ile tanımlanır.

```go
const Pi float64 = 3.14
const Pi = 3.14

// birden fazla sabit tanımlama
const (
    Big = 1 << 100
    Small = Big >> 99
)
```

## Koşul İfadeleri (if else switch)

Go da `if` deyiminde parantez `( )` kullanılmaz ve süslü parantezler `{ }` zorunludur.

```go
if i < 10{
    // ...
}
```

if de koşuldan önce çalıştırılacak kısa bir deyim bulunabilir. Bu değişken sadece if koşulu içinde ve else içinde tanımlıdır.

```go
i := 14
if x := 3; i < 10 {
    fmt.Println(x, " ", i)
} else if 10 <= i && i < 20 {
    fmt.Println(x, " ", i)
} else {
    fmt.Println(x, " ", i)
}
```

Go da `switch` yapısı şu şekildedir.

```go
switch os := runtime.GOOS; os {
case "darwin":
    fmt.Println("OS X.")
case "linux":
    fmt.Println("Linux.")
default:
    fmt.Printf("%s.", os)
}
```

`switch` işlenirken `case` lerden biri doğrulandığında geri kalan `switch` ifadesi atlanır.

Eğer `switch` yapısında koşul belirtilmez ise bu ifade `switch true` ile eşdeğerdir. Bu uzun if-then-else ifadelerine göre daha temizdir.

```go
t := time.Now()
switch {
case t.Hour() < 12:
    fmt.Println("Good morning!")
case t.Hour() < 17:
    fmt.Println("Good afternoon.")
default:
    fmt.Println("Good evening.")
}
```

## Döngüler

Go dilinde sadece `for` döngüsü vardır. `for` döngüsü noktalı virgüller ayrılmış üç kısımdan oluşur:

* ilklendirme deyimi: ilk döngüden önce çalıştırılır. Genellikle sadece döngü içinde geçerli olacak değerler tanımlanır.
* koşul ifadesi: her döngüden önce değerlendirilir.
* sonlandırma deyimi: her döngünün sonunda çalıştırılır.

Go dilinde döngü koşulunda parantez `( )` kullanılmaz ve döngünün gövdesi süslü parantezler `{ }` ile belirtilmek zorundadır.

```go
// örek bir for döngüsü
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

// birinci ve üçüncü kısımlar boş kalabilir.
sum := 1
for ; sum < 1000; {
    sum += sum
}
```

Go da for döngüsündeki noktalı virgülleri atabiliriz. Bu da diğer dillerdeki `while` döngüsüne eşdeğerdir.

```go
sum := 1
for sum < 1000 {
    sum += sum
}
```

Eğer döngü koşulu belirtilmez ise sonsuz döngü oluşacaktır.

```go
for {

}
```

## Fonksiyonlar

### Defer

## İşaretçiler, Diziler ve Dilimler

### İşaretçiler (pointers)

Go dilinde pointer vardır ve değişkenin bellekte saklandığı adresi turar. `0` değeri `nil` dir.

```go
var p *int
```

`&` operatörü başına geldiği değerin göstericisini oluşturur. `*` ise göstericinin gösterdiği değişkenin değerini turar. Buna dolaylı yoldan erişim denir.

```go
i := 42 // i 42 değerini alır.
p = &i // & operatörü i nin göstericisini oluşturur.
fmt.Println(*p) // gösterici üzerinden i nin değerini oku
*p = 21 // gösterici üzerinden i nin değerini
```

### Diziler (array)

Diziler aynı türde eleman tutan değişkenlerdir ve sabit uzunluktadırlar.

```go
// array tanımlaması
var a [5]int
b := [5]int{1, 2, 3, 4, 5}
var twoD [2][3]int

// herhangi bir elemanına ulaşma veya değiştirme
a[4] = 100
```

### Dilimler (slices)

Dizilerin dinamik boyutlu ve esnek yansımasıdır. Eleman barındırmazlar, sadece arka plandaki dizinin bir kısmını nitelerler. Bu nedenle bir dilimin bir elemanının değeri değiştiğinde arka plandaki dizinin elemanıda değişir. Bu değişim aynı diziyi kullanan diğer dilimlerdede görülür.

```go
var a [10]int

// a dizisinin ilk 5 elemanına ait dilim
a[0:5]

// diziyi tamamen dilimleyen ifadeler.
a[0:10]
a[:10]
a[0:]
a[:]
// burada 1. kısım dahil, 2. kısım değildir.
```

Bir dilimin 2 özelliği vardır:

* Uzunluk: dilimdeki eleman sayısıdır. `len()` fonksiyonu ile öğrenilir.
* Kapasite: `cap()` fonksiyonu ile öğrenilir.

Boş bir dilim `nil` değerini alır, uzunluk ve kapasitesi de 0 dır.

Dilimler ayrıca `make()` fonksiyonu ile oluşturulabilir.

```go
a := make([]int, 5)  // len(a)=5

// append fonksiyonu ile eleman eklenebilir.
a = append(a, 2)
```

Dilimler `range` deyimi ile döngülerde şu şekilde kullanılabilirler.

```go
var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
for i, v := range pow {
    fmt.Printf("2**%d = %d\n", i, v)
}
// 2**0 = 1
// 2**1 = 2
// 2**2 = 4
. . .

for i := range pow {
} // sadece indisi kullanmak istediğinde.
```

Bir dilim üzerinde dolaşılırken her seferinde iki değer dönülür. İlki indis, ikincisi o indisli elemanın bir kopyası.

### Yapılar (struct)

Struct alanlardan oluşan veri topluluğudur. `type` anahtar kelimesi ile tanımlanır.

```go
type Vertex struct {
    X int
    Y int
}

//bir tane vertex oluştur ve başlangıç değerlerini ver
v := Vertex{1, 2}

v.X = 4
v.Y = 12

fmt.Println(v.X) // 4
fmt.Println(v.Y) // 12
```

### Map ler

Bir `map` anahtarları değerlere eşler. Bir `map` in sıfır değeri `nil` dir. `nil` eşlemde anahtar bulunmaz. Ayrıca anahtarda oluşturulamaz.

```go
m = make(map[string]Vertex) // map oluştur.
m["Bell Labs"] = Vertex{ // map'a değer ata.
    40.68433, -74.39967,
}

m[key] = elem // map'a eleman ekle
elem = m[key] // map in elemanına ulaş
delete(m, key) // map tan eleman sil

elem, ok := m[key] // bu atama ile ok değişkeni elemanın var olup olmadığına göre değer alır.
// var ise true, yok ise false
//eğer yok ise elem değişkeni türüne göre 0 değerini alır.
```

```go
var m = map[string]Vertex{
    "Bell Labs": Vertex{
        40.68433, -74.39967,
    },
    "Google": Vertex{
        37.42202, -122.08408,
    },
}

var m = map[string]Vertex{
    "Bell Labs": {40.68433, -74.39967},
    "Google":    {37.42202, -122.08408},
}
```

## Metodlar ve Arayüzler

### Metodlar

Go dilinde sınıf yapısı bulunmaz. Buna karşın türler üzerinde foksiyonlar tanımlanabilir.

```go
type Vertex struct {
    X, Y float64
}

// vertex için fonksiyon tanımladık.
func (v Vertex) Abs() float64 {
    return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

v := Vertex{3, 4}
fmt.Println(v.Abs()) // bu fonksiyonu vertex türü üzerinden çağırdık
```

### Arayüzler



## Eşzamanlılık
