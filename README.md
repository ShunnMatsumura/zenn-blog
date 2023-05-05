# zenn-blog
# Tips
## 新規の記事作成
```
$ npx zenn new:article --slug 記事のスラッグ --title タイトル --type idea --emoji ✨
```

## 新規の本を作成
```
$ zenn new:book
```

## プレビュー
```
$ npx zenn preview
```

VSCodeの Zenn Editorで十分。

## 公開の時間指定
```
published: true # trueを指定する
published_at: 2050-06-12 09:03 # 未来の日時を指定する
```

詳細は[こちら](https://zenn.dev/zenn/articles/zenn-cli-guide#%E6%97%A5%E6%99%82%E3%82%92%E6%8C%87%E5%AE%9A%E3%81%97%E3%81%A6%E8%A8%98%E4%BA%8B%E3%82%92%E5%85%AC%E9%96%8B%E3%81%99%E3%82%8B%EF%BC%88%E5%85%AC%E9%96%8B%E4%BA%88%E7%B4%84%E3%81%99%E3%82%8B%EF%BC%89)