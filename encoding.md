# Encoding

## UTF-8

> A variable-length encoding of Unicode code points as bytes. It uses between 1 and 4 bytes to represent each rune, but only 1 byte for ASCII characters.
> The high-order bits of the first byte of the encoding for a rune indicate how many bytes follow.

```shell
0xxxxxxx                            # A high-order 0 indicates 7-bit ASCII; 0-127
110xxxxx 10xxxxxx                   # A high-order 110 indicates the rune tasks 2 bytes; the second byte begins with 10; 128-2047
1110xxxx 10xxxxxx 10xxxxxx          # 2048-65535
11110xxx 10xxxxxx 10xxxxxx 10xxxxxx # 65536 - 0x10ffff
```

Ref: The Go Programming Language

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
