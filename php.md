# PHP

## Hakkında

Bu döküman Goalkicker php kitabının özetidir.

## 1 PHP Başlarken

Php web server tarafından işlenerek html çıktısı üretilir.

```php
<!DOCTYPE html>
<html>
    <head>
        <title>PHP!</title>
    </head>
    <body>
        <p><?php echo "Hello world!"; ?></p>
    </body>
</html>
```

```php
// echo nun yazılışı. 1.si daha kısa ve özel.
<?= "Hello world!" ?>
<?php echo "Hello world!"; ?>
```

### echo print

`echo` ve `print` ekrana bir yazı basar. İkiside dil yapısıdır, fonksiyon değil! Farkları ise `echo` geriye `void` deger döndürür. `print` ise 1 döndürür. `echo` çok sayıda argüman alabilir. `print` ise yalnızca 1 argüman alır. `echo`, `print` den birazcık daha hızlıdır.

```php
echo "Hello, World!\n";
print "Hello, World!\n";
printf("%s\n", "Hello, World!"); // C tarzı print
```

### Headers

`header()` fonksiyonu ile request header larını değiştirebilirsiniz. Ayrıca web server'ın default headerlarınıda değiştirebilirsiniz.

```php
// web serverin default contant type ı değiştirdik.
// basen json plaintext gönderirken gerekebilir.
header("Content-Type: text/plain");
header("Content-Type: application/json");
```

`header()` fonksiyonu php kodunda herhangi bir çıktıdan önce çağrılmalıdır. Aksi halde hata verir. Çünkü web server çoktan header ları belirlemiştir. Bu yüzden hu fonksiyonu kodun başında kullanmak iyi bir alışkanlıktır.

### Built-in web server

Geliştirme aşamasındayden php nin built-in serverini kullanabiliriz.

```text
php -S <host/ip>:<port>
php -S localhost:8080

# kök dizini belirlemek için:
php -S <host/ip>:<port> -t <directory>
```

bu komut localhost ta 8080 portunu dinleyen bir web server çalıştıracaktır. Php dosyalarınızın olduğu dizinde bu komutu çalıştırın ve tarayıcıdan localhost 8080 portuna gidin. Php çıktısını görmeniz gerekiyor. Ayrıca her requestin hatanın çıktı loglarınıda bu serverın konsolundan görebilirsiniz.

### Php CLI

```bash
# pipeline ile php ye komut gönderme
'<?php echo "Hello world!";' | php

# -r parametresi ile komut göndermek
php -r 'echo "Hello world!";'

# dosya verebiliriz.
php hello_world.php

# php interactive shell
php -a
```

### Php Tagleri

```php
<?php
echo "Hello World";
?>

<?= "Hello World" ?> // sısa echo
```

## 2 Değişkenler

Php de dinemik değişkenler vardır.

```php
$variableName = 'foo';
$foo = 'bar';

// aşağıdakilerin hepsi denktir, ve çıktısı"bar":
echo $foo;
echo ${$variableName};
echo $$variableName;
//similarly,

$variableName = 'foo';
$$variableName = 'bar';

// aşağıdakiler şu çıktıyı verir: 'bar'
echo $foo;
echo $$variableName;
echo ${$variableName};
//süslü parantez zorunlu değil opsiyoneldir.

// eğer bir ifade var ise o zaman zorunludur.
${$variableNamePart1 . $variableNamePart2} = $value;
```

### Php5 ve php7 farkları

```php
$$foo['bar']['baz']
    ${$foo['bar']['baz']}
    ($$foo)['bar']['baz']
$foo->$bar['baz']
    $foo->{$bar['baz']}
    ($foo->$bar)['baz']
$foo->$bar['baz']()
    $foo->{$bar['baz']}()
    ($foo->$bar)['baz']()
Foo::$bar['baz']()
    Foo::{$bar['baz']}()
    (Foo::$bar)['baz']()
```

### veri türleri

Değişik amaçlar ve php veri türleri mevcuttur. Php de açık bir tür tanımlaması yoktur. Değerine göre türü değişir.

```php
// # null
// herhangi bir değişkene atanabilir ve o değişkenin değerini olmadığını belirtir.
$foo = null;

// # Boolean
$foo = true;
$bar = false;

// # Integer sayılar için kullanılır.
$foo = -3; // negatif
$foo = 0; // sıfır (null yada false (boolean olarak)
$foo = 123; // pozitif
$bar = 0123; // octal = 83 decimal
$bar = 0xAB; // hexadecimal = 171 decimal
$bar = 0b1010; // binary = 10 decimal
var_dump(0123, 0xAB, 0b1010); // çıktı: int(83) int(171) int(10)

// # Float
$foo = 1.23;
$foo = 10.0;
$bar = -INF;
$bar = NAN;

// Array # indexlerine göre erişilen yapı
$foo = array(1, 2, 3);
$bar = ["A", true, 123 => 5];
echo $bar[0];   //Returns "A"
echo $bar[1];   //Returns true
echo $bar[123]; //Returns 5
echo $bar[1234];//Returns null

$bar["hello"] = "world";
echo $bar["hello"]; // world

// String # karakter array leri gibidir.
$foo = "bar";
echo $foo[0]; // 'b'

// Object # bir sınıfın örneğidir.
$foo = new stdClass(); // stdClass dan nesne oluştur, öntanımlı boş bir sınıftır
$foo->bar = "baz";
echo $foo->bar; // "baz"

// bir arrayı object e cast etmek
$quux = (object) ["foo" => "bar"];
echo $quux->foo; // "bar".

//  değişkenleri veritabanı, dosya, stream gibi şeyleri tutan özel değişkenlerdir
$fp = fopen('file.ext', 'r'); // resource olarak diskten dosya açar.
var_dump($fp);
```

Bir değişkenin türünü `gettype()` ile alabiliriz.

```php
echo gettype(1); // "integer"
echo gettype(true); // "boolean"
```

### Superglobal variables

Bu global değişkenler php-öntanımlı özel değişkenlerdir ve php kodunda her yerden erişilebilirler. Fonksiyon scope'ından erişmek içinde `global` deyimine ihtiyaç duymazlar.

* `$GLOBALS`
* `$_SERVER`
* `$_REQUEST`
* `$_POST`
* `$_GET`
* `$_FILES`
* `$_ENV`
* `$_COOKIE`
* `$_SESSION`

## Değişkenlerin Default değerleri

* `null` tanımlanmadan kullanılan.
* `""` stringlerde
* `0` integer
* `0.0` float
* `false` boolean
* arraylarde boş array
* `$unset_obj->foo = 'bar';` böyle bir ifadede boş nesnedir.

Default değerlere güvenmeyin. Bazen problemlere neden olabilirler.

## Değişken Doğtuluğu

Php de non-boolean değişkenlerin bile doğruluk değeri vardır.

```php
if ($var == true) { /* açık */ }
if ($var) { /* $var == true gizli */ }
```

* `string` sıfırdan farılı uzunluktaysa  `true` ya eşit, boş string `false` eşittir.
* `Integer` ların değeri `0` ise `false`, aksi taktirde `true` dur.
* `null` değeri `false` eşittir.
* `"0"` yani 0 string de `false` eşittir.
* Float değerler 0 a eşit olmadığı sürece `false` dır.
    * `NAN` yani "not a number" `true` ya eşittir.
    * `floatval('0') == floatval('-0')` eşittir `true`. Çünkü php `0` ile `-0` ı birbirinden ayırmaz.
        * aslında `floatval('0') === floatval('-0')`
        * `floatval('0') == false` ve `floatval('0') == false`

```php
$var = NAN;
$var_is_true = ($var == true); // true
$var_is_false = ($var == false); // false

$var = floatval('-0');
$var_is_true = ($var == true); // false
$var_is_false = ($var == false); // true

$var = floatval('0') == floatval('-0');
$var_is_true = ($var == true); // true
$var_is_false = ($var == false); // false
```

### Kimlik Operatörü (identical operator) (===)

`===` operatörü değişkenin referans değeri ile aynı olup olmadığını kontrol eder. `!==` aynı işlemin tersi.

```php
$var = null;
$var_is_null = $var === null; // true
$var_is_true = $var === true; // false
$var_is_false = $var === false; // false
```

### `strpos()` Kullanımı

`strpos($haystack, $needle)` fonksiyonu `$needle` nin `$hatstack` te ilk geçtiği yerin indexini döner. Bu fonksiyon büyük-küçük harf duyarlıdır. `stripos()` ise büyük-küçük duyarsız. Ayrıca bu fonksiyonlar 3. parametre olarak bir offset alırlar (opsiyonel).

* `0` başlangıçta bulundu.
* non-zero needle nin geçtiği index
* `false` bulunamadı.

## 