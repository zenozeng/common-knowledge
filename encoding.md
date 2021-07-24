# Encoding

## Base32

https://en.wikipedia.org/wiki/Base32

> Base32 has a number of advantages over Base64:
> - The resulting character set is all one case, which can often be beneficial when using a case-insensitive filesystem, DNS names, spoken language, or human memory.
> - The result can be used as a file name because it cannot possibly contain the '/' symbol, which is the Unix path separator.
> - The alphabet can be selected to avoid similar-looking pairs of different symbols, so the strings can be accurately transcribed by hand. (For example, the RFC 4648 symbol set omits the digits for one, eight and zero, since they could be confused with the letters 'I', 'B', and 'O'.)
> - A result excluding padding can be included in a URL without encoding any characters.

## Base64

https://developer.mozilla.org/en-US/docs/Glossary/Base64

## Geohash

Base32 分格子，格子再分格子

https://www.elastic.co/guide/cn/elasticsearch/guide/current/geohashes.html

## Roaring Bitmap

> It divides the data into chunks of 2<sup>16</sup> integers (e.g., [0, 2<sup>16</sup>), [2<sup>16</sup>, 2 x 2<sup>16</sup>), …). Within a chunk, it can use an uncompressed bitmap, a simple list of integers, or a list of runs. Whatever format it uses, they all allow you to check for the present of any one value quickly (e.g., with a binary search).

http://roaringbitmap.org/about/
