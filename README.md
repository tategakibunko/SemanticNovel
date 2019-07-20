# SemanticNovel

`SemanticNovel` is markup format for [TypeNovel](https://github.com/tategakibunko/TypeNovel) to write novel with plenty of semantic context informations.

## Scene

### summary

Markup for writing scene.

### markup map

```javascript
{
  "tagName": "div",
  "className": "scene"
}
```

### precedent

Every semantic value starts with `'?'` is treated as `undefined` value in reader app.

This is usefull when you want to annotate some constraint, but keep the value ambigous to readers or ui of reader app.

Note that constraint value `'?'` in TypeNovel is not validation target of annotation, but constraint value that starts with '?'(like `?23:00`) is validation target of annotation.

```javascript
@scene({
  time: '?23:30' // time is 23:30, but keep it secret to readers.
}){
}
```

### constraints

#### time

value: `'00:00'` - `23:00`

```javascript
@scene({time:"09:00"}){ $time() }
```

#### season

value: `spring` | `summer` | `autumn` | `winter`

```javascript
@scene({season:"09:00"}){ $time() }
```

#### era

value: `ancient` | `modern` | `middle-ages` | `future`

#### date

value: `01/01` - `12/31`

## speak

### summary

Markup for writing speech text.

### format

```javascript
@speak('Michael Jackson'){ This is it! }
```

### markup map

```javascript
{
  "tagName": "div",
  "className": "speak",
  "attributes": {
    "data-character": "<arg1>"
  }
}
```

## External Data Schema

External data is stored as `data.json` in [TypeNovel](https://github.com/tategakibunko/TypeNovel).

Usually, this data is extra resource used by reader app of TypeNovel.

### Title

Set novel title.

```javascript
{
  title: "This is my novel title"
}
```

### Characters

Set characters of your novel.

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
  [CharacterKey]: CharacterData
}
```

#### CharacterKey

Unique character key.

#### CharacterData

##### names

First name, family name array.

Order is not specified([family name, first name], [first name, family name]).

#### description

Description of character.
