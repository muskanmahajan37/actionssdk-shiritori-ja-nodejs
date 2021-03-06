# しりとり AoG サンプルゲーム

## 設定

1. 「[Actions on Google](https://console.actions.google.com/)」のプロジェクトを作成する。
1. 「Action package」をアップデートする：

        gactions update --action_package action.json --project PROJECT_NAME

1. [edict2](http://www.edrdg.org/jmdict/edict_doc.html)の辞書をダウンロードする。
1. utf-8に変換する：

        iconv -f euc-jp -t utf-8 edict2 -o edict2.utf8

1. 名詞だけをフィルターする：

        cat edict2.utf8 | grep '(n)' > edict2-noun.utf8

1. 「Firebase Database」にアップロードする：

        npm --prefix script/ install
        node scripts/admin.js noun edict2-noun.utf8 /path/to/service-account
        ^C

1. 「Firebase Functions」をデプロイする。

        firebase deploy

1. [Cloud Console](https://console.cloud.google.com)で `shiritori` のRAMを512MBまで上げる。
1. [Actions on Google](https://console.actions.google.com/)「Simulator」でロケールを日本語に設定する。
1. アシスタントアプリをテストしてみる。

        > テスト用アプリにつないで

## テスト

1. [edict2](http://www.edrdg.org/jmdict/edict_doc.html)の辞書をダウンロードする。
1. utf-8に変換する：

        iconv -f euc-jp -t utf-8 edict2 -o edict2.utf8

1. 名詞だけをフィルターする：

        cat edict2.utf8 | grep '(n)' > edict2-noun.utf8

1. ローカルのコーパスを作成する：

        npm --prefix scripts/ install
        node scripts/admin.js noun edict2-noun.utf8 > functions/shiritori/corpus.json

1. ニットテスト：

        npm --prefix functions/shiritori/ install
        npm --prefix functions/shiritori/ test
        
1. スナップショットテスト：

        npm --prefix functions/ install
        npm --prefix functions/ test

1. ローカルで起動してテストする：

        npm --prefix functions/shiritori/ install
        node functions/shiritori/main.js

```
しりとり
> りんご
胡麻酢 [ごます]
> すいか
カプリチョーザ [かぷりちょうざ]
> ざるそば
バインミー [ばいんみい]
> いか
カポナータ [かぽなあた]
> たんたんめん
ざんねん。
```

## Contributing

Contributions to this repository are always welcome and highly encouraged.

See [CONTRIBUTING.md](CONTRIBUTING.md) for more information on how to get started.

## License

Copyright (C) 2018 Google Inc.

Licensed to the Apache Software Foundation (ASF) under one or more contributor
license agreements.  See the NOTICE file distributed with this work for
additional information regarding copyright ownership.  The ASF licenses this
file to you under the Apache License, Version 2.0 (the "License"); you may not
use this file except in compliance with the License.  You may obtain a copy of
the License at

  http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS, WITHOUT
WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.  See the
License for the specific language governing permissions and limitations under
the License.
