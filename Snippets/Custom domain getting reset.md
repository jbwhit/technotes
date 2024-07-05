
I have a quarto blog (via nbdev) that I post to a custom URL. It kept getting reset to the default github url. 

https://github.com/jbwhit/website/commit/e9eed1ba133cd1680608ca293d1da4fddfd4f753

I had to change the `settings.ini` at the root

Looks like this has worked so far: 

```
custom_domain = jonathanwhitmore.com
```


Wasn't enough, https://github.com/fastai/nbdev/issues/1033 suggests putting CNAME in nbs folder.

Trying that next. 

