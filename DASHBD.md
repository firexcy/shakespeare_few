# Dashboard

## Today

### New Words

```dataview
table title as "Title"
from "words"
where learned_on = date(today)
sort title
```

### Reviewed Words

```dataview
table title as "Title"
from "words"
where reviewed_on = date(today)
sort title
```

## Refresher

### 1 Day

```dataview
table title as "Title"
from "words"
where learned_on = date(today) - dur(1 day)
sort title
```

### 3 Days

```dataview
table title as "Title"
from "words"
where learned_on = date(today) - dur(3 day)
sort title
```

### 6 Days

```dataview
table title as "Title"
from "words"
where learned_on = date(today) - dur(6 day)
sort title
```