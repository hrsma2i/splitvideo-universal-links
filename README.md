# SplitVideo Universal Links

SplitVideo アプリを https URL で起動するための Universal Links 設定ファイル。

## ユースケース

- Notion などの Web サービスで SplitVideo のディープリンクを共有したい
- https URL で SplitVideo アプリを起動したい

## 手順書

### GitHub Pages へのデプロイ

1. リポジトリを GitHub にプッシュ

```bash
cd /Users/hiroshi.matsui/splitvideo-universal-links
git add .
git commit -m "initial commit"
git remote add origin https://github.com/yourusername/splitvideo-universal-links.git
git push -u origin main
```

2. GitHub の Settings → Pages で公開
   - Source: Deploy from a branch
   - Branch: main / (root)

3. 公開される URL: `https://yourusername.github.io/splitvideo-universal-links/`

### Xcode での設定

1. Target → Signing & Capabilities
2. `+ Capability` をクリック
3. `Associated Domains` を追加
4. `applinks:yourusername.github.io` を追加

### 使い方

デプロイ後、以下の URL でアプリを起動できます：

```
https://yourusername.github.io/splitvideo-universal-links/play?videoId=b5elNhsQ980&start=10&end=20
```

この URL は：
- Notion の URL カラムに貼り付け可能
- Web ブラウザでも開ける（アプリ未インストール時はメッセージを表示）
- iOS がアプリと関連付けを認識すれば、自動的にアプリを起動

## 技術スタック

- HTML/JavaScript (フォールバック用)
- apple-app-site-association (iOS Universal Links 設定)
- GitHub Pages (ホスティング)

## アーキテクチャ

```
.
├── .well-known/
│   └── apple-app-site-association  # iOS が読み込む設定ファイル
├── index.html                       # フォールバック用 Web ページ
└── README.md                        # ドキュメント
```

- `.well-known/apple-app-site-association`: iOS がアプリと URL の関連付けを認識するための設定ファイル
- `index.html`: Web ブラウザで開いた場合のフォールバック（custom URL scheme にリダイレクト）
