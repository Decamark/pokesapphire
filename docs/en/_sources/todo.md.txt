# TODO
## [`StringCopy`](https://github.com/pret/pokeruby/blob/master/src/string_util.c#L73)

```c
u8 *StringCopy(u8 *dest, const u8 *src)
{
    while (*src != EOS)
    {
        *dest = *src;
        dest++;
        src++;
    }

    *dest = EOS;
    return dest;
}
```

This function can cause an overflow as it copies `src` to `dest` until it finds `EOS`. The following is an example:

```{code-block} c
:caption: [`TVShowConvertInternationalString`](https://github.com/pret/pokeruby/blob/master/src/tv.c#L2657)

void TVShowConvertInternationalString(u8 *dest, u8 *src, u8 language)
{
    StringCopy(dest, src);
    if (language < LANGUAGE_ENGLISH)
        ConvertInternationalString(dest, LANGUAGE_JAPANESE);
}
```

TV shows can be transfered among players and a rogue save data could destroy receiver's data, theoretically. Further research required.
