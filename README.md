I assign information into different cache levels -- L1, L2, L3 and so on. 

| Level | Description | Example |
| ---- | ---- | ---- |
| 0 | I better not forget this or I'm in deeper trouble than whatever results from missing this specific fact. | My name, `import pandas as pd`, etc. |
| 1 | Stuff that I want to know at my fingertips: Anki-able | That I can do: `pd.... (axis='columns')` |
| 2 | Stuff that I want autoexpanded or templated | Something that I know, but I have to often do something with. ```fig, ax = plt.subplots(figsize=(10, 6))<br>fig.patch.set_facecolor('w')<br>fig.tight_layout()``` |
| 3 | Stuff that I want to be *very fast* to look up. | That I have a snippet for `read_csv`, so when I search for it, I find: <br>```df = pd.read_csv(filename, dtype_backend='pyarrow', engine='pyarrow')<br>``` |
| 4 | Stuff that I want to look up at the speed of Google or stackoverflow. | I know there's a way to... |
| 5 | Stuff that I would look up if I knew more | Say you didn't know how to get rid of the Unnamed 0 column, but you created a fix. But there's a right way. |
