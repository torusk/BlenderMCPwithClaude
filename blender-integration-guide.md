# Mac ユーザーの個人的体験：BlenderMCP と Claude.ai の連携で遭遇した問題と解決策

！！この文章は Claude.ai に概要を書いててもらっています！！
こんにちは！Mac ユーザーとして Claude.ai と Blender を BlenderMCP で連携させようとして、いくつかの壁にぶつかりました。この記事では、実際に遭遇した問題点とその解決策、そして得た教訓を共有します。

## 遭遇した問題点と解決策

### 1. 初手で詰む：developer ボタンがない問題

まず、初手で詰んだのがこれ。Claude.ai の Mac アプリの設定画面に developer ボタンが見当たらないんですよね。README には「Go to Claude > Settings > Developer > Edit Config」って書いてあるのに、そもそも Developer の項目がない！

**解決策：** ネットで「Claude developer mode enable」で検索したら、ヘルプメニューから「Enable Developer Mode」を選択する必要があるとわかりました。これ、ドキュメントに書いておいてほしかった...

### 2. Blender アドオンのセットアップ

次に、Blender にアドオンをインストールする際に少し迷いました。addon.py ファイルをダウンロードした後、どうやって Mac の Blender にインストールするの？という。

**解決策：** Blender の「Edit > Preferences > Add-ons」から「Install...」ボタンをクリックしてダウンロードしたファイルを選択するだけでした。そして「Interface: Blender MCP」にチェックを入れて有効化。

### 3. 設定ファイル問題：間違った JSON を編集していた

これが一番厄介でした。README の指示通りに「developer_settings.json」を編集したのに、ハンマーアイコンが全然表示されない！何度 Claude.ai を再起動しても変わらず...

**解決策：** Mac の場合、正しく編集すべきファイルは「claude_desktop_config.json」でした。これは完全に盲点でした。ファイルパスは「~/Library/Application Support/Claude/claude_desktop_config.json」です。

```json
{
  "mcpServers": {
    "blender": {
      "command": "uvx",
      "args": ["blender-mcp"]
    }
  }
}
```

### 4. 最後の関門：接続許可

やっとハンマーボタンが表示されたと思ったら、今度は動かない。「Could not connect to Blender」エラーばかり。Mac のファイアウォールかな？と思ったけど違いました。

**解決策：** ハンマーの横にある小さなソケットマークをクリックして、MCP の接続を許可する必要がありました。これも公式ドキュメントに書いておいてほしかった...

## Mac ユーザーとしての教訓

この一連の作業から、Mac ユーザーとしていくつかの重要な教訓を得ました：

1. **AI に全部聞くよりも検索が早いケースがある**  
   特に「developer mode の有効化方法」などの具体的な情報は、ネット検索の方が圧倒的に早く見つかりました。

2. **動画の情報価値は高い**  
   文字だけのドキュメントでは伝わりにくい操作手順も、動画だと一目瞭然。特に GitHub の README に貼られていた解説動画は非常に参考になりました。

3. **Mac 特有の設定ファイルパスに注意**  
   Mac の場合、`~/Library/Application Support/` 以下に設定ファイルがあることが多いです。Windows とは異なるため、この点は注意が必要です。

4. **自分で考える部分は残る**  
   どんなに AI が進化しても、完全に情報伝達できない部分は残ります。最終的には自分の頭で考えて試行錯誤する必要があります。

5. **JSON ファイル編集の際は注意**  
   構文エラーに気をつけるのはもちろん、そもそも正しいファイルを編集しているか確認することが重要です。

## Mac での簡単セットアップ手順（まとめ）

1. Claude.ai の Mac アプリでヘルプメニューから開発者モードを有効化
2. `~/Library/Application Support/Claude/claude_desktop_config.json` を正しく編集
3. Blender にアドオンをインストール・有効化
4. Blender でサーバーを起動（「BlenderMCP」タブの「Start MCP Server」）
5. Claude.ai でハンマーアイコンの横のソケットマークをクリックして接続許可

今回の経験が、同じように Mac で BlenderMCP のセットアップに苦戦している人の助けになれば幸いです！
