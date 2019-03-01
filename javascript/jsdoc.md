---
title: "JsDoc Notlar"
Authors: "Süleyman ERGEN, Hüseyin ALTUNKAYNAK"
Date: 1 Mart 2019
License: CC BY-NC-SA
---

# JSDOC NOTLAR

Bu döküman jsdoc ile alakalı kısa notlardan oluşmaktadır. jsdoc javascript dosyalarını dökümante etmek için kullanılan bir araçtır. Bu döküman sizlere jsdoc'a hıslı bir giriş sağlayacaktır.

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

## Bazı taglar

* `@fileOverview` tüm js dosyası hakkında bilgi verir.
* `@author` Dosyayı kodlayan kişi.
* `@version` dosyanın versiyon bilgisi.
* `@deprecated` bir değişkenin artık testeklenmediğini belirtir.
* `@example` örnek bir kod gösterir.

```javascript
/**
 * @fileOverview çeşitli fonksiyonlar.
 * @author <a href="mailto:jd@example.com">John Doe</a>
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
 * @see The <a href="http://example.com">Example Project</a>.
 */
```

* `@since` dökümante edilmiş nesnenin hangi sürümden beri var olduğunu belirtir.

```javascript
/**
 * @since 10.2.0
 */
```

## Javascript Fonksiyonlar ve Metodlar

Fonksiyonlar için `jsdoc` şu şekildedir.

* İlk satırlar genellikle fonksiyonun ne yaptığını açıklayan birkaç satır içerir.
* `@param` tagı ile fonksiyon parametreleri ve parametreye ait türü ve açıklaması belirtilir.
    * `@param name` türünü belirtmeden kullanım.
    * `@param {string} name` sıtandart kullanım.
    * `@param {string|number} name` birden çok tip belirtir.
    * `@param {string[]} name` string arrayi olduğunu belirtir.
    * `@param {number} [time=1]` parametreye default deger verir.
* `@returns` gereye dönen değerin türü ve açıklaması belirtilir.
* `@throws` fonksiyonun çalışması sırasında oluşacak exception türünü belirtir.

Bir örnek vermek gerekirse:

```javascript
/**
 * Hello "isim"
 *
 * @param {string} isim hello diyeceğiniz kişi/varlık.
 * @returns {string} Hello + isim
 */
function hello(isim) {
  return "Hello "+isim +"!";
}
```

## variables ve fields

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
     * @param {number} x=1 - x değeri.
     * @param {number} [y=2] - y değeri.
     */
    constructor(x, y) {
        // ...
    }
}

/**
 * Dot sınıfını belirtir.
 * @extends Point
 */
class Dot extends Point {

}
```

## Meta-tags

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