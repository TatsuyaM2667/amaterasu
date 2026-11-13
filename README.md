# amaterasu

画面の明るさを読む・変える・覚えて戻す小さなコマンド(brightnessctl の代わり。root なしで logind 経由)。

[ame-shell](https://github.com/TatsuyaM2667/ame-shell)(Wayland のデスクトップシェル)の一部を、単独で使えるように切り出したものです。
ame-shell は画面の要らない仕事を、1 つのことをして標準入出力でやりとりする小さなコマンドに分けています。これはその 1 つです。

## 使い方

```text
amaterasu: 画面の明るさを読む / 変える(brightnessctl の代わり)。
名前は光の神、天照大神(あまてらす)から。

  amaterasu                 今の明るさ(0〜100 の数)を 1 行
  amaterasu set 40          40% に(40% とも書ける)
  amaterasu set +5 / -5     5% 明るく / 暗く(brightnessctl の 5%+ / 5%- の書き方も読む)
  amaterasu restore         最後に set した明るさに戻す(起動時。カーネルは再起動のたびにファームウェアの値に戻すので)

set した明るさ(%)は $XDG_STATE_HOME/ame-shell/light に覚える。

/sys/class/backlight の最初の機器を使う。書き込めればそこへ直接、書き込めなければ(ふつうは root だけ)
logind(elogind)の Session.SetBrightness に頼む(ログイン中の人なら root なしで変えられる)。
真っ暗で戻せなくならないよう 1% より下にはしない。
終了コード: 0 できた / 1 バックライトが無い・変えられない / 2 使い方の誤り
```

## ビルド

```sh
zig build -Doptimize=ReleaseSafe   # zig-out/bin/amaterasu(Zig 0.13、libc と libdbus)
zig build test
```

## このリポジトリについて

正本は ame-shell の `src/cmd/amaterasu.zig` です。このリポジトリは `scripts/split-repos.sh` が生成して同期しています。
直したいところがあれば ame-shell の方へお願いします。

ライセンス: GPL-3.0(ame-shell と同じ)
