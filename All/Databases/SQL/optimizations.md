# Optimizations

### N+1 Queries

```php
$cats = load_cats();
foreach ($cats as $cat) {
  $cats_hats = load_hats_for_cat($cat);
  // ...
}
```

```
SELECT * FROM cat WHERE ...
SELECT * FROM hat WHERE catID = 1
SELECT * FROM hat WHERE catID = 2
SELECT * FROM hat WHERE catID = 3
SELECT * FROM hat WHERE catID = 4
SELECT * FROM hat WHERE catID = 5
```

Instead do 

```php
$cats = load_cats();
$hats = load_all_hats_for_these_cats($cats);
foreach ($cats as $cat) {
  $cats_hats = $hats[$cat->getID()];
}
```

```
SELECT * FROM cat WHERE ...
SELECT * FROM hat WHERE catID IN (1, 2, 3, 4, 5, ...)
```

