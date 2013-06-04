quran
==========

node.js interface to Holy Quran

Installation
------------

npm install quran

Usage
-----

var quran = require('quran');

Fetch the first verse of second chapter

```
quran.get(2,1,function(err,verse) {
  if (!err) {
    console.log('Verse 1: Chapter 1: ' + verse.arabic);
  }
});
```

Fetch the first chapter

```
quran.get(1,function(err,verses) {
  if (!err) {
    console.log('Chapter 1: ' + verses.join(','));
  }
});
```
verses is an array, so you can join them in the above.

.get is simply a wrapper on select, so you can directly invoke it
and do advanced filtering, like getting verse 2-4 of first chapter.

```
quran.select({ chapter: 1}, { offset: 1, limit: 3}, function(err,verses) {
  if (!err) {
    console.log(verses);
  }
});

[
  { chapter: 1,
    verse: 1,
    ar: 'بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ' },
  { chapter: 1,
    verse: 2,
    ar: 'ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ' },
  { chapter: 1, verse: 3, ar: 'ٱلرَّحْمَٰنِ ٱلرَّحِيمِ' } 
]
```
verses is an array of objects, and has additional info (chapter number, verse number).

The second argument to select is optional. 

If you want to fetch multiple verses, not necessarily in sequence, use an array to specify this.

```
quran.select({ chapter: 1, verse: [ 2, 4, 6 ]}, function(err,verses) {
  if (!err) {
    console.log(verses);
  }
});

[ { chapter: 1,
    verse: 2,
    ar: 'ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ'
  },
  { 
    chapter: 1, 
    verse: 4, 
    ar: 'مَٰلِكِ يَوْمِ ٱلدِّينِ' 
  },
  { chapter: 1,
    verse: 6,
    ar: 'ٱهْدِنَا ٱلصِّرَٰطَ ٱلْمُسْتَقِيمَ'
  } 
]

```

Currently, only arabic text and english, hindi and urdu translations are supported, to limit package size.

To fetch both the arabic text and translation, set the language option to en.

```
quran.select({ chapter: 1}, { offset: 1, limit: 3, language: 'en'}, function(err,verses) {
  if (!err) {
    console.log(verses);
  }
});
```
Similarly for hindi

```
Code:
quran.select({ chapter: 1}, { offset: 1, limit: 3, language: 'hi'}, function(err,verses) {
  if (!err) {
    console.log(verses);
  }
});
Output
[ 
  { chapter: 1,
    verse: 1,
    ar: 'بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ',
    hi: 'अल्लाह के नाम से जो रहमान व रहीम है।',
    translator: 'hindi' },
  { chapter: 1,
    verse: 2,
    ar: 'ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ',
    hi: 'तारीफ़ अल्लाह ही के लिये है जो तमाम क़ायनात का रब है।',
    translator: 'hindi' },
  { chapter: 1,
    verse: 3,
    ar: 'ٱلرَّحْمَٰنِ ٱلرَّحِيمِ',
    hi: 'रहमान और रहीम है।',
    translator: 'hindi' } 
]
```

Want multiple translations at once? Use an array when specifying language

```
quran.select({ chapter: 1, verse: [ 2, 4, 6 ]}, 
             { language: ['ur', 'en ] }, function(err,verses) {
  if (!err) {
    console.log(verses);
  }
});

[ { chapter: 1,
    verse: 2,
    ar: 'ٱلْحَمْدُ لِلَّهِ رَبِّ ٱلْعَٰلَمِينَ',
    en: 'All praise is due to Allah, the Lord of the Worlds.',
    ur: 'ساری تعریف اللہ کے لئے ہے جو عالمین کا پالنے والا ہے'
  },
  { chapter: 1,
    verse: 4,
    ar: 'مَٰلِكِ يَوْمِ ٱلدِّينِ',
    en: 'Master of the Day of Judgment.',
    ur: 'روزِقیامت کا مالک و مختار ہے' 
  },
  { chapter: 1,
    verse: 6,
    ar: 'ٱهْدِنَا ٱلصِّرَٰطَ ٱلْمُسْتَقِيمَ',
    en: 'Keep us on the right path.',
    ur: 'ہمیں سیدھے راستہ کی ہدایت فرماتا رہ' 
  } 
] 
```

You can also fetch meta data about a chapter 

```
quran.chapter(1,function(err,info) {
  if (!err) {
    console.log(info);
  }
});
```
Or all the chapters, by omitting the optional argument

```
quran.chapter(function(err,info) {
  if (!err) {
    console.log(info);
  }
});

```

Credits
-------

This work is based on Quran Text and Translations made available by http://tanzil.net. 

Sites using this package
------------------------

http://duas.mobi/quran.

To add yours, submit a pull request.
