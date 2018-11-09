# PDate
Persian aka Jalali or Shamsi or Hijri Shamsi  library using php intl extension 

what PDate can do?
* convert Gregorian to persian date
* convert Persian to gregorian date
* get current Persian date
* check Persian leap year
* check Gregorian leap year
* get start and end of each Persian month in gregorian date (used for Jalali/Persian archive or monthly report)

default config is
```
[
    'dateTime'  => null,
    'y'         => null,
    'm'         => null,
    'd'         => null,
    'h'         => 0,
    'i'         => 0,
    's'         => 0,
    'inFormat'  => 'Y-m-d',
    'outFormat' => 'y-M-d',
    'local'     => null,
    'calendar'  => 'persian',
    'timeZone'  => null,
];
```
*`null` values replace with ini default values.*

**priority of input date is with `dateTime` in `$config` `parameters`, it means if you set `dateTime`, then `y`, `m`, `d` have no affect**

`inFormat` is only available when you set `dateTime` parameter and use `g2p()`.
if you want to pass date and/or outFormat directy to `g2o()` and `p2g()` you have to use one of following chatecters as delimiter between date, month, day, hour, minute and second:
`-`, `:`, ` `(white space), `/`
examples of acceptable formats:
2018-10-9
2018/5/11 18:30:58
1397/5/11 18:30


you can set last `pArchive()` output date by set `$tillNow` parameter to `false` and set `Y-m-d`(in Persian date) as last date in third argument.
by default `$tillNow` is `true`
example
```php
$pDate = new PDate();
$archive = $pDate->pArchive(3, false, [1397,4,31]); //start of archive is on 1397-1-1, end on 1397-4/31
var_dump($archive);
/**
output:
array (size=3)
  0 => 
    array (size=4)
      0 => string '2018-6-22' (length=9) //1397-4-1
      1 => string '2018-7-22' (length=9) //1397-4-31
      'year' => int 1397
      'month' => int 4
  1 => 
    array (size=4)
      0 => string '2018-5-22' (length=9) //1397-3-1
      1 => string '2018-6-21' (length=9) //1397-3-31
      'year' => int 1397
      'month' => int 3
  2 => 
    array (size=4)
      0 => string '2018-4-21' (length=9) //1397-2-1
      1 => string '2018-5-21' (length=9) //1397-2-31
      'year' => int 1397
      'month' => int 2
*/
```

possible `outFormat` values are documented at
[http://userguide.icu-project.org/formatparse/datetime](http://userguide.icu-project.org/formatparse/datetime).

possible `inFormat` values are documented at
[http://uk3.php.net/manual/en/function.date.php](http://uk3.php.net/manual/en/function.date.php).
