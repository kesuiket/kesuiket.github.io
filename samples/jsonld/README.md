# JSON-LDの外部ファイル読み込み

## [OK] インライン

## [OK] Ajax 読み込み後差し込む

```
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

ただし, 既存 `<script type="application/ld+json">` に追加すると読み込んでもらえrない

```
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

## [NG] `<script type="application/ld+json" src="data/jsonld.{js,json,jsonld}"></script>`
## [NG] `<link href="data/jsonld.{js,json,jsonld}" rel="alternate" type="application/ld+json">`
