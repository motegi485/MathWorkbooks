# 情報系のための数学 問題集シリーズ

情報系の大学生・大学院進学をめざす人のための、独学用の数学問題集です。
各分野は『問題集』と『解答解説集』の2冊組で、問題番号が完全に対応しています（問 3.4 の解説は 解 3.4）。

**公開 URL**: （Cloudflare Pages のプロジェクト作成後に記入）

## 収録タイトル

| 分野 | 規模 | 難易度内訳（★/★★/★★★） | 付録 |
|---|---|---|---|
| [線形代数](linear-algebra/workbook.html) | 全11章・103問 | 41 / 38 / 24 | — |
| [微分積分・最適化](calculus-optimization/workbook.html) | 全19章・159問 | 48 / 76 / 35 | 主要公式集 |
| [確率・統計](probability-statistics/workbook.html) | 全18章・154問 | 52 / 62 / 40 | 数表 |

合計 3分野・全48章・416問。

## 構成

```
index.html                        トップページ（3分野へのリンク）
linear-algebra/
  workbook.html                   線形代数 問題集
  solutions.html                  線形代数 解答解説集
calculus-optimization/            微分積分・最適化
probability-statistics/           確率・統計
```

各 HTML は完全に自己完結しています（数式表示に MathJax の CDN を使う以外、外部依存はありません）。
`index.html` をブラウザで開けばそのまま読めます。ビルド作業はありません。

## 配信

Cloudflare Pages で静的ファイルをそのまま配信します。プロジェクト設定は次のとおり:

- フレームワークプリセット: **None**
- ビルドコマンド: **なし**
- ビルド出力ディレクトリ: **`/`（リポジトリルート）**

ディレクトリ名・ファイル名はすべて小文字とハイフンで統一しています。Cloudflare Pages は
大文字小文字を区別するため、追加するときもこの規則を守ってください。

## 分野を追加するには

1. 小文字ハイフンのディレクトリを作り、`<id>/workbook.html` と `<id>/solutions.html` を置く。
2. `index.html` 内の `BOOKS` 配列にブロックを1つ足す（`id` はディレクトリ名と一致させる）。

```js
{
  id: "discrete-math",              // ディレクトリ名
  subject: "離散数学",
  series: "情報系のための離散数学",
  chapters: 12, problems: 110,
  levels: [40, 45, 25],             // ★ / ★★ / ★★★ の問題数
  appendix: "記号表",               // 付録が無ければこの行ごと省略
  summary: "……",
  topics: ["……", "……"]
}
```

カードの描画・リンク先（`<id>/workbook.html`、`<id>/solutions.html`）は自動で組み立てられます。
`index.html` 末尾の `<noscript>` にも1行足しておくと、JavaScript を無効にしている環境でも開けます。
