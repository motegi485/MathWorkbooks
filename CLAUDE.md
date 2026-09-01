# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## プロジェクト概要

情報系の大学生・大学院進学をめざす人向けの独学用数学問題集シリーズ（線形代数／微分積分・最適化／確率・統計、全3分野・全48章・416問）。**純粋な静的HTMLサイトで、ビルド工程は一切ない。** `index.html` をブラウザで直接開けばそのまま動作する。

## リポジトリ構成

```
index.html                          トップページ（3分野へのリンクカードを描画）
linear-algebra/
  workbook.html                     問題集（全11章103問）
  solutions.html                    解答解説集
calculus-optimization/
  workbook.html                     問題集（全19章159問＋付録「主要公式集」）
  solutions.html
probability-statistics/
  workbook.html                     問題集（全18章154問＋付録「数表」）
  solutions.html
```

各HTMLファイルは完全に自己完結（`<style>` を内部に持つ）しており、外部依存は数式表示用の **MathJax CDN**（`cdnjs.cloudflare.com`、`tex-mml-chtml.min.js`）のみ。ファイル間で共有されるCSS/JSファイルは存在しない ―― `index.html` と各 `workbook.html`/`solutions.html` はそれぞれ独立してスタイルを内包しているため、デザインを一括変更する際は該当する全ファイルの `<style>` ブロックを個別に編集する必要がある。

## `.gitignore` の方針（重要）

`.gitignore` は**許可リスト方式**（`*` で全拒否した上で個別に `!` で解除）になっている。新しいファイル・ディレクトリを追加しても、この許可リストに明示的に加えない限り Git に追跡されない。新規ファイルを作成したら `git status` で追跡対象になっているか必ず確認すること。

## コンテンツの構造規約

- 各分野は「問題集」（`workbook.html`）と「解答解説集」（`solutions.html`）の2冊組で、**問題番号が完全に対応**している（例: 問 3.4 の解説は 解 3.4）。
- 問題側の `id` は `q<章番号>-<問題番号>`（例 `id="q1-1"`）、解答側は `a<章番号>-<問題番号>`（例 `id="a1-1"`）。序章（`ch0`）には問題がなく、末尾に付録がある分野は `id="appendix"` を使う。
- ただし **workbook.html と solutions.html の間に実際のハイパーリンク（アンカー参照）は張られていない**。2冊は別タブで開いて読者が手動で行き来する設計（`index.html` のリンクはすべて `target="_blank"`）。番号の対応はテキスト上の規約であり、機械的なリンクではないため、問題を追加・削除・並べ替えるときは両ファイルの番号ズレに特に注意する。
- 難易度は3段階（`lv1`＝★基礎／`lv2`＝★★標準／`lv3`＝★★★応用）で、各問題集冒頭・`index.html` の統計表示（`BOOKS` 配列の `levels` 配列）と実際の問題数が一致している必要がある。
- 解答解説集の各問は `方針 → 解答 → ポイント`（`h4` / `h4.alt`）という三段構成が基本形。
- 数式は MathJax の `\( ... \)`（インライン）／`\[ ... \]`（ディスプレイ）記法。HTML内にそのまま埋め込まれているため、バックスラッシュのエスケープ崩れに注意（特に `index.html` 内のJSテンプレートリテラル部分は該当しないが、`workbook.html`/`solutions.html` は生HTMLなのでそのまま `\(...\)` を書く）。

## `index.html` への分野追加

`index.html` 末尾の `<script>` 内 `BOOKS` 配列にオブジェクトを1つ追加するだけでトップページにカードが増える（`id` がそのままディレクトリ名になる）。対応する `<id>/workbook.html` と `<id>/solutions.html` を先に配置しておくこと。`levels` 配列や `chapters`/`problems` はカード表示の統計値であり、実際のHTML内容と手動で一致させる必要がある（自動検証は行われない）。

## 動作確認

自動テストは存在しない。変更後は対象のHTMLファイルをブラウザで直接開いて次を確認する。
- MathJax の数式が正しくレンダリングされるか
- 問題番号と解答番号の対応が崩れていないか
- `@media print` の印刷レイアウト（各冊はPDF保存を想定した印刷用スタイルを持つ）
