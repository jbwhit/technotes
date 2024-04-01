
Order left to right 1, 2, 3 is natural, so choose `<` over `>` -- these lists are living in a state of sin.

- choose `.casefold()` over `.lower()` when needing to do case-insensitive matching. 

From Matt Harrison's [[Effective Pandas 2 -- Notes]]
- Ranking of pandas methods: `.case_when` > `.where` > `.apply` when possible
- Use `.loc` > `.iloc` -- "advise you not iloc for prod code"


Try to avoid pandas `apply` as much as possible. 
Do this
```python
(pres
    .select_dtypes('number')
    .pipe(lambda df_: df_.max(axis='columns') - df_.min(axis='columns'))
    .rename('range')
)

```
not this: 
```python
(pres
    .select_dtypes('number')
    .apply(lambda row: row.max(axis='columns') - row.min(axis='columns'))
    .rename('range')
)
```
