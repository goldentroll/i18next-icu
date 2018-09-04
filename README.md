# Introduction

[![Travis](https://img.shields.io/travis/i18next/i18next-icu/master.svg?style=flat-square)](https://travis-ci.org/i18next/i18next-icu)
[![Coveralls](https://img.shields.io/coveralls/i18next/i18next-icu/master.svg?style=flat-square)](https://coveralls.io/github/i18next/i18next-icu)
[![npm version](https://img.shields.io/npm/v/i18next-icu.svg?style=flat-square)](https://www.npmjs.com/package/i18next-icu)
[![David](https://img.shields.io/david/i18next/i18next-icu.svg?style=flat-square)](https://david-dm.org/i18next/i18next-icu)

This changes i18n format from i18next json to ICU using [yahoo/intl-messageformat](https://github.com/yahoo/intl-messageformat)

# Getting started

Source can be loaded via [npm](https://www.npmjs.com/package/i18next-icu) or [downloaded](https://github.com/i18next/i18next-icu/blob/master/i18nextICU.min.js) from this repo.

```
# npm package
$ npm install i18next-icu
```

Wiring up:

```js
import i18next from "i18next";
import ICU from "i18next-icu";

i18next.use(ICU).init(i18nextOptions);
```

- As with all modules you can either pass the constructor function (class) to the i18next.use or a concrete instance.
- If you don't use a module loader it will be added to `window.i18nextICU`

## Plural Support

- While on node.js all plurals will work out of the box in browser you will need to load additional locale data files like:

```js
import i18next from 'i18next';
import ICU from 'i18next-icu';

import fr from 'i18next-icu/locale-data/fr';

i18next
  .use(ICU)
  .init({
    i18nFormat: {
      localeData: fr // you also can pass in array of localeData
      formats: {
        // https://github.com/yahoo/intl-messageformat#user-defined-formats
      }
    }
  });

// or for react-i18next when using SSR
import i18next from 'i18next';
import ICU from 'i18next-icu';
import fr from 'i18next-icu/locale-data/fr';

const icu = new ICU();
icu.addLocaleData(fr);
icu.addUserDefinedFormats({ /* https://github.com/yahoo/intl-messageformat#user-defined-formats */ })

i18next
  .use(icu)
  .init({
    i18nFormat: {}
  });
```

## Backend Options

```js
{
  // per default icu functions are parsed once and cached for subsequent calls
  memoize: true,

  // memoize if not having a lookup and just using the key fallback as value
  memoizeFallback: false,

  // array or single object of loaded 'i18next-icu/locale-data
  localeData: null
}
```

Options can be passed in by setting options.i18nFormat in i18next.init:

```js
import i18next from "i18next";
import ICU from "i18next-icu";

i18next.use(ICU).init({
  i18nFormat: options
});
```

### more complete sample

```js
import i18next from "i18next";
import ICU from "i18next-icu";

i18next.use(ICU).init({
  lng: "en",
  resources: {
    en: {
      translation: {
        key:
          "You have {numPhotos, plural, " +
          "=0 {no photos.}" +
          "=1 {one photo.}" +
          "other {# photos.}}"
      }
    }
  }
});

i18next.t("key", { numPhotos: 1000 }); // -> You have 1,000 photos.
```

---

<h3 align="center">Gold Sponsors</h3>

<p align="center">
  <a href="https://locize.com/" target="_blank">
    <img src="https://raw.githubusercontent.com/i18next/i18next/master/assets/locize_sponsor_240.gif" width="240px">
  </a>
</p>
