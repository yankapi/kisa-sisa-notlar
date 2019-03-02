---
title: "JsDoc Notlar"
Authors: "Süleyman ERGEN, Hüseyin ALTUNKAYNAK"
Date: 1 Mart 2019
License: CC BY-NC-SA
---

# JSDOC NOTLAR

Bu döküman jsdoc ile alakalı kısa notlardan oluşmaktadır. Jsdoc javascript dosyalarını dökümante etmek için kullanılan bir araçtır. Bu döküman sizlere jsdoc'a hızlı bir giriş sağlayacaktır.

## Kurulum

Javascript paket yöneticisi olan `npm` ile kurabilirsiniz.

```text
npm install jsdoc
```

## Kullanım

`jsdoc` komutu ile kullanılmalıdır. Bu kamut js dosyalarınızdan döküman oluşturacaktır. İşlem bittikten sonra `out` isminde bir dizin oluşturacaktır.

```text
jsdoc file.js
```

Dökümantasyona ulaşmak için `out/index.html` dosyasını tarayıcıda açın.

## Syntax

Dökümantasyon oluşturmak için __özel yorum satırları__ kullanılır. Bu yorum satırlarından faydalanarak `jsdoc` dökümantasyonu oluşturacaktır.

Döküman için kullanılan yorum satırı `/**` ile başlar ve `*/` ile biter. Genellikle ideler text editörler otomatik tamamlama ile aşağıdakine benzer bir yorum satırları oluştururlar.

```javascript
/**
 *
 */
```

Bu yorum satırları arasına dökümantasyon için gereken detayları yazabilirsiniz.

## Bazı Taglar

* `@fileOverview` tüm js dosyası hakkında bilgi verir.
* `@author` Dosyayı/fonskiyonu/sınıfı kodlayan kişi.
* `@version` dosyanın versiyon bilgisi.
* `@deprecated` bir değişkenin artık testeklenmediğini belirtir.
* `@example` örnek bir kod gösterir.

```javascript
/**
 * @fileOverview çeşitli fonksiyonlar.
 * @author <a href="mailto:example@example.com">İsim Soyisim</a>
 * @version 3.1.2
 */
```

```javascript
/**
 * @example
 * var str = "abc";
 * console.log(repeat(str, 3)); // abcabcabc
 */
```

* `@see` ilgili bir kaynağı gösterir.

```javascript
/**
 * @see MyClass#myInstanceMethod
 * @see The <a href="http://example.com">Örnek Proje</a>.
 */
```

* `@since` dökümante edilmiş nesnenin hangi sürümden itibaren var olduğunu belirtir.

```javascript
/**
 * @since 10.2.0
 */
```

## Javascript Fonksiyonlar ve Metodlar

Fonksiyonlar için `jsdoc` şu şekildedir.

* İlk satırlar genellikle fonksiyonun ne yaptığını açıklayan birkaç satır içerir.
* `@param` tagı ile fonksiyon parametreleri ve parametreye ait türü ve açıklaması belirtilir.
    * `@param name` parametre türünü belirtmeden kullanım.
    * `@param {string} name` standart kullanım.
    * `@param {string} name - açıklama` açıklama ile beraber. `-` okunurluğu arttırmak için. Yani zorunlu değil.
    * `@param {string|number} name` birden çok tip belirtir.
    * `@param {string[]} name` string arrayi olduğunu belirtir. Başka tipler içinde uygulanabilir.
    * `@param {number} [time=1]` parametrenin default değerini belirtir.
* `@returns` veya `@return` gereye dönen değerin türü ve açıklaması belirtilir.
* `@throws` fonksiyonun çalışması sırasında oluşacak exception türünü belirtir.

Bir örnek vermek gerekirse:

```javascript
/**
 * Merhaba "isim"
 *
 * @param {string} isim merhaba diyeceğiniz kişi/varlık.
 * @returns {string} Merhaba + isim
 */
function hello(isim) {
  return "Merhaba "+isim +"!";
}
```

Bazen parametre olarak bir object vermemiz gerekebilir. İşte bu nokrada `@param` tagı ile objenin ögelerinide belirtebiliriz.

```javascript
/**
 * Personele proje ata.
 *
 * @param {Object} employee - Projeden sorumlu personel.
 * @param {string} employee.name - Personelin ismi.
 * @param {string} employee.department - Personelin departmanı.
 */
Project.prototype.assign = function(employee) {
    // ...
};
```

Aynı işlem Object array'leri içinde geçerlidir.

```javascript
/**
 * Projeyi personel listerine ata.
 *
 * @param {Object[]} employees - Projeden sorumlu personeller.
 * @param {string} employees[].name - Personelin ismi.
 * @param {string} employees[].department - Personelin departmanı.
 */
Project.prototype.assign = function(employees) {
    // ...
};
```

Birden fazla türde parametre alabilen fonksiyonlarda şu şekilde kullanım vardır.

* `@param {(string|string[])} [somebody=John Doe] - Somebody's name, or an array of names.`

```javascript
/**
 * @param {(string|string[])} [somebody=John Doe] - Birinin ismi yada isimler listesi
 * @param {*} somebody - Herhangi bir tip. Yani ne istersen.
 */
```

## Variables ve Fields

Alanlar, işlev dışı değerleri olan özelliklerdir. Örnek alanlar genellikle bir kurucu içinde oluşturulduğundan, onları orada belgelemeniz gerekir.

* `@type` değişkenin türü

```javascript
/** @constructor */
function Car(make, owner) {
    /** @type {string} */
    this.make = make;

    /** @type {Person} */
    this.owner = owner;
}
```

* `@constant` değişkenin `const` olduğunu belirtir.
* `@default` değişkenin default değerini belirtir.

```javascript
/** @constructor */
function Page(baslik) {
    /**
     * @default "basliksiz"
     */
    this.baslik = baslik || "basliksiz";
}
```

* `@property` sınıf içindeki örnek değişkenini belirtir.

```javascript
/**
 * @class
 * @property {string} isim Kişinin ismi.
 */
function Person(isim) {
    this.isim = isim;
}
```

## Sınıflar

```javascript
/**
 * Bu sınıf bir noktayı temsil eder..
 */
class Point {
    /**
     * Bir tane point oluştur.
     *
     * @param {number} x=1 - x değeri.
     * @param {number} [y=2] - y değeri.
     */
    constructor(x, y) {
        // ...
    }
}

/**
 * Dot sınıfını belirtir.
 *
 * @extends Point
 */
class Dot extends Point {

}
```

## Meta-Tags

Meta taglar çeşitli değişkenlere eklenen taglardır. `/**#@+` ile başlar ve `/**#@-*/` ile biter.

```javascript
/**#@+
 * @private
 * @memberOf Foo
 */

function baz() {}
function zop() {}
function pez() {}

/**#@-*/
```

## Kaynaklar

* [2ality](http://2ality.com/2011/08/jsdoc-intro.html) Dr. Axel Rauschmayer blog sayfası
* [jsdoc](http://usejsdoc.org/) resmi sitesi.
* [learn jsdoc-github](https://github.com/dwyl/learn-jsdoc)
* [Wikipedia Jsdoc](https://tr.wikipedia.org/wiki/JSDoc)