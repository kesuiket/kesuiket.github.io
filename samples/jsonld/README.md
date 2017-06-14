# JSON-LDの外部ファイル読み込み
Google 構造化データテストツールで正しく認識されるかどうかをテスト

## [OK] インライン

```html
<script type="application/ld+json">
{
  ...
}
</script>
```

## [OK] Ajax 読み込み後差し込む

```html
<script>
  $.ajax({
    url: 'path/to/data',
    type: 'get',
    dataType: 'json'
  }).then(function(data) {
    var s = document.createElement('script')
    s.type = 'application/ld+json'
    s.textConent = JSON.stringify(data)
    document.appendChild(s)
  })
</script>
```

ただし, 既存の `<script type="application/ld+json">` に追加すると認識してもらえなかった

```html
<script type="application/ld+json"></script>
<script>
  var s = document.querySelector('[type="application/ld+json"]')
  $.ajax({
    ...
  }).then(function(data) {
    s.textContent = JSON.stringify(data)
  })

</script>
```

## [NG] `<script>` で外部ファイルを読み込む
拡張子がなんであってもだめなものはだめ

```html
<script type="application/ld+json" src="data/jsonld.{js, json, jsonld}"></script>
```

## [NG] `<link>` で外部ファイルを読み込む
これも拡張子がなんであってもだめなものはだめ

```html
<link href="data/jsonld.{js,json,jsonld}" rel="alternate" type="application/ld+json">
```
