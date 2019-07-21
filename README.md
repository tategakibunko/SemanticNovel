# SemanticNovel

`SemanticNovel` is markup format for [TypeNovel](https://github.com/tategakibunko/TypeNovel) to write novel with plenty of semantic context informations.

## precedent

- Every semantic value that **is** `'?'` is not validated by TypeNovel compiler and treated as `undefined` value in reader app.

```javascript
@scene({
  time: '?' // time is ambigous and secret to reader app.
}){
  // time is not annotated in text-field, but it's not an error.
}
```

- Every semantic value **starts with** `'?'` is treated as `undefined` value in reader app.

```javascript
@scene({
  time: '?23:30' // time is 23:30, but keep it secret to readers.
}){
}
```

This is usefull when you want to annotate some constraint, but keep the value ambigous to readers or ui of reader app.

Note that constraint value `'?'` in TypeNovel is not validation target of annotation, but constraint value that starts with '?'(like `?23:00`) is validation target of annotation.

<!----------------------------------------------------->

## Markup

You can see all markup definition in [init.tnconfig.json](https://github.com/tategakibunko/TypeNovel/blob/master/Tools/init.tnconfig.json).

### @scene

Markup to write some scene with some constraints.

```javascript
@scene({
  place: "Japan",
  season: "summer"
}){
  @scene({
    date: "8/1"
  }){
    @scene({
      time: "9:00"
    }){
       $time("good morning!")
    }
    @scene({
      time: "12:00"
    }){
       $time("lunch time!")
    }
    @scene({
      time: "22:00"
    }){
       $time("good night!")
    }
  } // date:"8/1"
} // place:"Japan", season:"summer"
```

#### constraints

##### time

value: `'00:00'` - `23:00`

```javascript
@scene({time:"09:00"}){ $time() }
```

##### season

value: `spring` | `summer` | `autumn` | `winter`

```javascript
@scene({season:"summer"}){ $time() }
```

##### date

value: `01/01` - `12/31`

<!----------------------------------------------------->


### @speak

Markup for writing speech text.

```javascript
@speak('Michael Jackson'){ This is it! }
```

### @tip

Markup to write some `tip` content.

```javascript
@tip("IMO"){ Abbreviation of 'In My Opinion' }, it's correct.
```

<!----------------------------------------------------->

### @notes

Markup to write some `notes`(footnote) content.

```javascript
This game is inspired by "街" @notes(){ 1998 Chunsoft.inc }
```

<!----------------------------------------------------->

### $ruby

Inline markup to write `ruby` in CJK text.

```javascript
$ruby("漢字", "かんじ")
```

<!----------------------------------------------------->

### $tcy

Inline markup to write `tate-chu-yoko` in `vertical` writing-mode.

```javascript
あのソフトは$tcy("UI")が素晴らしい。
```

<!----------------------------------------------------->

## External data schema

External data is stored as `data.json` in [TypeNovel](https://github.com/tategakibunko/TypeNovel).

Usually, this data is used by reader app of TypeNovel.

### title

Title of the novel.

```javascript
{
  title: "This is my novel title"
}
```

### writingMode

Writing mode of novel. `vertical-rl` or `horizontal-tb` is supported.

```javascript
{
  writingMode: "horizontal-tb"
}
```

### characters

Characters of novel.

#### Example

```javascript
"characters": {
  "taro": {
    "names": ["山田", "太郎"],
    "description": "desc of taro"
  },
  "michael": {
    "names": ["Michael", "Jackson"],
    "description": "desc of michael"
  }
}
```

#### Schema

```typescript
{
  [characterKey]: characterData
}
```

#### characterKey

Unique character key.

#### characterData

Character detail.

##### names

`first name`,` family name` array.

Order is not specified (both [`family name`, ` first name`] and  [`first name`, ` family name`] are OK).

#### description

Description of character.
