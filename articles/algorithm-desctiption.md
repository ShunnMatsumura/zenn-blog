---
title: "アルゴリズム入門：基本的な概念とコードサンプル（幅優先探索）"
emoji: "🐥"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["algorithm", "幅優先探索"]
published: true
published_at: 2023-05-06 09:00
---
# アルゴリズムとは
アルゴリズムとは、解が定まっている「計算可能」問題に対して、その解を正しく求める手続きをさす。あるいはそれを形式的（formal）に表現したもの。

参考: [Wikipedia](https://ja.wikipedia.org/wiki/%E3%82%A2%E3%83%AB%E3%82%B4%E3%83%AA%E3%82%BA%E3%83%A0)

アルゴリズムを調べてみたが、色々あってどれもきちんと説明できないなと思ったのでブログに書き起こす。

# 幅優先探索
幅優先探索（Breadth-First Search, BFS）は、グラフや木構造の探索アルゴリズムの一種です。このアルゴリズムは、探索の開始ノードから最も近いノードを優先して探索し、徐々に距離の遠いノードへと進む特徴があります。幅優先探索は、キュー（FIFO: First-In-First-Out）データ構造を用いて実装されることが一般的。キューとは、探索候補のノードを記録しておく場所のことです。

例えば以下のようなグラフにおいて、出発点Aから終点Fまでの最短経路を導くのによく使われているようです。

![幅優先探索](/images/algorithm-desctiption/breadth-first-search-graph.png)

これをJavaScriptでChatGPT（GPT-4）に書かせ、コードから理解を深める。

```bash:プロンプト
幅優先探索を利用し、以下のノードに対する最短経路をJavaScriptを用いて説明してください。

/**
 * key: nodeの頂点
 * value: 隣接ノード
 */
const graph = {
  A: ['B', 'C'],
  B: ['D', 'E'],
  C: ['F'],
  D: [],
  E: ['F'],
  F: []
}
```

```javascript:breadth-first-search.js
/**
 * key: nodeの頂点
 * value: 隣接ノード
 */
const graph = {
  A: ['B', 'C'],
  B: ['D', 'E'],
  C: ['F'],
  D: [],
  E: ['F'],
  F: []
}

const bfs = (graph, startNode, endNode) => {
  const visited = new Set()
  const queue = [
    [ startNode, [] ]
  ]

  while (queue.length > 0) {
    // キューの先頭を取得し
    const [currentNode, path] = queue.shift()

    if (!visited.has(currentNode)) {
      visited.add(currentNode)

      if (currentNode === endNode) {
        return [...path, currentNode]
      }

      const neighbors = graph[currentNode]
      for (const neighbor of neighbors) {
        if (!visited.has(neighbor)) {
          queue.push([neighbor, [...path, currentNode]])
        }
      }
    }
  }

  return null
}

const findShortestPath = (graph, startNode, endNode) => {
  const result = bfs(graph, startNode, endNode)
  return `
    最短ルート: ${result.join(" -> ")}
    最短ステップ数: ${result.length}
  `
}

console.log(findShortestPath(graph, 'A', 'F'))

===結果===
最短ルート: A -> C -> F
最短ステップ数: 3
```

## コードからの解釈
- スタート地点であるAをキューに入れる
- 隣接しているノードを見つつ、未訪問の場合はキューに以下の情報を貯める
  - 探索対象ノード（neighbor）
  - 今まで通ってきたノード（path）
- スタート地点から隣接しているノードの隣接ノードをぐるぐる見て行って、一番早く目的地となる"F"と探索中ノードが一致した場合、最短経路です。という感じ
- ただ、上記コードだと最短ステップ数は取得できる。しかし、複数の最短経路が存在する場合に対応できていない。

## 本当にあってるのか確認
[こちら](https://qiita.com/drken/items/996d80bcae64649a6580)の記事が非常にわかりやすかったです。なんならこの記事見た方が早い。深掘りもたくさんしてるし結局今この記事を見ている。
見た感じだと、概念的にはあってそう。小学校でやる迷路問題はこれだったのかと17越しに理解。

# 最後に
次回は「深さ優先探索」をやる。