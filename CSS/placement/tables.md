# Tables

## Col Syntax

```html
<table>
    <caption>2017-18: Tennis</caption>
    <colgroup>
        <col class="week"/>
        <col class="player"/>
        <col class="club"/>
        <col class="stat"/>
    </colgroup>
</table>
```

Setting styles will change the entire column, but limited attributes allowed

## Caption

- specifies title of table, always first child, inherits from table, good for accessibility 
- styled with **caption-side**, can be top, bottom; experimental in firefox is left, or right

```css
table {
    caption-side: top;
}
caption {
   color: #CC0000; 
}
```

## Border

If you want real table dividing, then

```css
table, th, td {border: 1px solid}
```

Could just add padding to th and td 

### Border-spacing

2 values: horizontal and vertical padding 

If you make entire tr color, spacing wouldn't be color

### Border-collapse

seperate(default), collapse(spacing irrelevant)

## Other

#### Empty-Cell

```css
table { //can also be on td
    empty-cell: show | hide;
}
//equivalent to
Td:empty, Th:empty {
	visibility: none

}
```

#### Vertical Align

```css
Vertical-align: baseline | sub |super |text-top | text-bottom | middle | top | bottom | <percentage> | <length>
```

Recall baseline means have all the bottom first text line be aligned( significant if multiple font sizes)

## General Beauty

```css
td, th { 
	padding: 5px 0 5px 10px;
}
table {
    border: 1px solid; 
    border-collapse: collapse;
}
thead tr th { 
    border-bottom: 1px solid; 
	background-color: #dedede;
}
tbody tr:nth-of-type(even){
    background-color: #00000010; 
    //add black with hgih alpha to every other row in body
}

```







