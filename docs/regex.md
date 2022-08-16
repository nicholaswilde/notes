# Regex

## [Accented Characters][1]

```regex
[A-zÀ-ú] // accepts lowercase and uppercase characters
[A-zÀ-ÿ] // as above, but including letters with an umlaut (includes [ ] ^ \ × ÷)
[A-Za-zÀ-ÿ] // as above but not including [ ] ^ \
[A-Za-zÀ-ÖØ-öø-ÿ] // as above, but not including [ ] ^ \ × ÷
```

## References
- <https://regex101.com/>

[1]: <https://stackoverflow.com/a/26900132/1061279>
