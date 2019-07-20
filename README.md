# SemanticNovel

`SemanticNovel` is markup format for [TypeNovel](https://github.com/tategakibunko/TypeNovel) to write novel with plenty of semantic context informations.

## Markup

### Scene

#### summary

Markup for writing scene.

#### markup map

```javascript
{
  "tagName": "div",
  "className": "scene"
}
```

#### precedent

Every semantic value starts with `'?'` is treated as `undefined` value in reader app.

This is usefull when you want to annotate some constraint, but keep the value ambigous to readers or ui of reader app.

Note that constraint value `'?'` in TypeNovel is not validation target of annotation, but constraint value that starts with '?'(like `?23:00`) is validation target of annotation.

```javascript
@scene({
  time: '?23:30' // time is 23:30, but keep it secret to readers.
}){
}
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

##### era

value: `ancient` | `modern` | `middle-ages` | `future`

##### date

value: `01/01` - `12/31`

### speak

Markup for writing speech text.

#### format

```javascript
@speak('Michael Jackson'){ This is it! }
```

#### markup map

```javascript
{
  "tagName": "div",
  "className": "speak",
  "attributes": {
    "data-character": "<arg1>"
  }
}
```

## External data schema

External data is stored as `data.json` in [TypeNovel](https://github.com/tategakibunko/TypeNovel).

Usually, this data is used by reader app of TypeNovel.

### Title

Set novel title.

```javascript
{
  title: "This is my novel title"
}
```

### Characters

Set characters of novel.

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

##### names

`first name`,` family name` array.

Order is not specified (both [`family name`, ` first name`] and  [`first name`, ` family name`] are OK).

#### description

Description of character.
