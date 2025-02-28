# 1D-Reversi1次元リバーシのルールに従って、C言語でCLIアプリを実装する方法を解説します。

問題の整理
 1. 初期状態：左が黒 (b)、右が白 (w) の2つの石がある。
 2. 操作：
 • R → 右側に石を置く
 • L → 左側に石を置く
 • 石を置くたびに、直近の同じ色の石までの間にある石をすべてひっくり返す（ただし、隣接する石が同色の場合はひっくり返さない）。
 • 黒 (b) と白 (w) を交互に置く。

実装方針
 1. 配列を使って盤面を管理
 • 盤面を char board[20000] のような配列で管理（最大 10000 + 初期配置 2 くらいを想定）。
 • 初期配置は board[mid] = 'b', board[mid + 1] = 'w' で中央付近に設置。
 2. 操作を順番に適用
 • R の場合：右側 (right) に新しい石を置く
 • L の場合：左側 (left) に新しい石を置く
 • 石を置いた後、最も近い同じ色の石までの間の石をひっくり返す。
 3. 最終的な b と w の数をカウント

コードのポイント
 1. 固定長の配列 board[MAX_SIZE] を用意
 • mid = MAX_SIZE / 2 の位置に初期配置 (b と w)
 • left と right を用いて配置の範囲を管理
 2. L と R による処理
 • L なら left-- して石を置く
 • R なら right++ して石を置く
 • 石を置いた後、間の石をひっくり返す
 3. 最終的な b と w をカウント
 • left から right の範囲を走査し、b と w の数をカウント

入出力例

入力

RRLL

処理の流れ

初期:  bw
1手目:  bbbw   (Rでb)
2手目:  bbbww  (Rでw)
3手目:  bbbwww (Lでb)
4手目:  wwwwww (Lでw) ← ひっくり返る

出力

0 6

計算量と効率
 • O(N) で処理可能（N は棋譜の長さ）
 • board は最大 10000 + 2 なので十分なメモリを確保

このコードを main.c に書いてコンパイル (gcc main.c -o myApp) すれば、

./myApp < input.in

のように実行できます。