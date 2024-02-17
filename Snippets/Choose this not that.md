
Order left to right 1, 2, 3 is natural, so choose `<` over `>` -- these lists are living in a state of sin.

- choose `.casefold()` over `.lower()` when needing to do case-insensitive matching. 

From Matt Harrison's [[Effective Pandas 2 -- Notes]]
- Ranking of pandas methods: `.case_when` > `.where` > `.apply` when possible
- Use `.loc` > `.iloc` -- "advise you not iloc for prod code"

