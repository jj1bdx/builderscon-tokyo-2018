theme: Simple, 2
footer: Kenji Rikitake / Builderscon Tokyo 2018 7-SEP-2018
slidenumbers: true
autoscale: true

<!-- Use Deckset 2.0, 4:3 aspect ratio -->

![](theodore-palser-tv-noise.jpg)

# [fit] Safe randomness: theory and practice
# [fit] 安全なランダムネスの理論と実践

---

![right, fit](kenji-20180530-stockholm.jpg)

# [fit] Kenji Rikitake
# [fit] りきたけ けんじ

7-SEP-2018
Builderscon Tokyo 2018
Kyoseikan, Keio University
Yokohama City, Kanagawa, Japan
@jj1bdx

---

# [fit] Give the feedback via the feedback form
# [fit] Use the feedback form QR code on your name card
# [fit] フィードバックをおねがいします
# [fit] ネームカードのQRコードを使ってください

---

# [fit] In this talk I'm going to talk about
# [fit] Randomness
# [fit] この発表ではランダムネスについて話します

---

# [fit] What is randomness?
# [fit] ... unpredictability
# [fit] ランダムネスとは予測不能性のことです

---

# [fit] In algorithm, randomness is represented as:
# [fit] Random numbers
# [fit] アルゴリズムでのランダムネスは
# [fit] **乱数** によって表現します

---

# [fit] My works on random numbers
# [fit] 乱数について何をやってきたか

---

# Software contribution to Erlang/OTP

- Improve the random number algorithms
- 乱数アルゴリズムの改善

- [Erlang/OTP rand module](http://erlang.org/doc/man/rand.html)
- [SFMT for Erlang/OTP](https://github.com/jj1bdx/sfmt-erlang/)
- [TinyMT calculation of 256M keys](https://github.com/jj1bdx/tinymtdc-longbatch)

---

# Bad algorithm example (JS V8)

![inline fit](v8-random-pattern.png)

---

# Legacy Erlang/OTP random module

- A 1980s algorithm called AS183
- [Can be fully scanned in 8 hours](https://github.com/jj1bdx/as183-c)
- Became a security issue - deprecated since OTP 19 (June 2016)
- 8時間で全数検索できてしまう
- セキュリティ問題になりOTPバージョン19（2016年6月）より非推奨

---

# [fit] ... And hardware contribution
# [fit] because software is not enough
# [fit] ソフトだけでは不十分なのでハードもやってます

---

# Why hardware?

- Computers are *programmed* and *predictive* machines; finding randomness inside computers is *extremely difficult*
- コンピュータはプログラムされた通りに、予想通りに動く→コンピュータの中でランダムネスを見つけるのは非常に難しい

---

# Randomness sources in a computer

- CPU clock jitter / CPUクロックの揺れ
- Keyboard timing / キーボード打鍵のタイミング
- Network packet timing / パケットのタイミング
- Storage seeking timing / ストレージのタイミング
- ... Those sources are highly predictive
- … これらのソースは予測可能

---

# [fit] We need additional randomness
# [fit] 追加のランダムネスが必要

---

# Why? Because:
# [fit] Security depends on unpredictability
# [fit] Secure operations consume randomness
# [fit] Availability of randomness is limited
# [fit] セキュリティは予測不能性に依存している
# [fit] 安全な処理はランダムネスを消費する
# [fit] 使えるランダムネスは有限

---

# When randomness needed
# ランダムネスが必要な時

- Password/key generation / パスワードや鍵の生成
- Timing obfuscation / 処理時間を隠す
- Using multiple resources equally but unpredictably / 複数の資源を同じように、しかし予測されないように使いたい

---

# Physical randomness source
# 物理的なランダムネス源

- Thermal noise / 熱雑音
- Avalanche noise of semiconductor junctions / 半導体接合部のなだれ降伏雑音
- Timing jitter of oscillation circuits / 発振回路のタイミングの揺れ

---

![original, right](avrdice-snapshot-cropped.jpg)

# Physical random number generator with Arduino UNO

Displayed at Maker Faire Tokyo 2016

This implementation is working as a dice: generating numbers of 1~6 / サイコロ同様に1から6までの数字を生成する

Generating ~10kbytes/sec

---

![](avrhwrng-v2rev1fix1.png)

---
![fit,right](infinite-noise-crowdsupply.jpg)

#[fit] Infinity Noise TRNG [^1][^2]

- Thermal noise based
- USD35/device
- Public domain, no patent
- No MCU on the device / デバイスはMCUを持たない
- ~40Kbytes/sec

[^1]: <https://github.com/13-37-org/infnoise>

[^2]: [Crowd Supply product page of Infinity Noise TRNG](https://www.crowdsupply.com/13-37/infinite-noise-trng)

---

# Infinity Noise TRNG schematics

` `

![original, fit](infnoise-schematics.png)

---

# How to inject external randomness to the operating systems

- Linux: random(4) ioctl() of RNDGETENTCNT, RNDADDENTROPY (User accessible)
- FreeBSD: random_harvest(9) (Accessible from kernel modules only) [^3]
- Other proprietary OSes: unable to find the same functions / その他の独自OSでは外部からランダムネスを注入できない

[^3]: [My FreeBSD randomness injection device driver](https://github.com/jj1bdx/freebsd-dev-trng)

---

![original, fit](os-prng-flow-en.png)

# Randomness processing flow

` `

---

![right, fit](prng-hashing-en.png)

# For using the external randomness safely

- Whitening. a process of making the output uniformly dispersed to all the value range with a cryptographic hash function, is required; implemented in the driver or the post-processing software
- 暗号化ハッシュ関数を適用して出力の分布を一様化する処理が必要


---

# Summary/まとめ

- Good randomness is hard to obtain
- External physical random number generator is essential for secure operation
- Do not invent your own methods; stick to the defacto standards
- 良いランダムネスを得るのは難しい
- 安全な運用には外部の物理乱数装置が不可欠
- 自己流でやらない

---

# [fit] Before finishing the talk:
# [fit] Give the feedback please
# [fit] Use the QR code on your name card
# [fit] フィードバックをおねがいします
# [fit] ネームカードのQRコードを使ってください

---

# [fit] Thanks
# [fit] Questions?


<!--
Local Variables:
mode: markdown
coding: utf-8
End:
-->
