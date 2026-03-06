---
draft: false
date: 2026-03-05
title: "KVM-GO DP/VGA 発熱対策 – エンジニアリングログ"
description: "KVM-GO の DP および VGA 発熱問題を詳細に検証し、測定データ、PCB 変更、機械的対策によりファンなしで過熱を解消した経緯を記録。"
keywords: "KVM-GO thermally fix, DP 発熱, VGA 発熱, KVM-over-USB エンジニアリング, PCB レイアウト, 熱管理, Openterface, engineering log"
author: "TechxArtisan Studio"
category: "Product Updates"
tags: ["KVM-GO", "Thermal", "Engineering Log", "Product Design"]
featured: false
social:
  image: "https://assets.openterface.com/images/kvm-go/thermal-fix.webp"
  title: "KVM-GO DP/VGA 発熱の解決"
  description: "レイアウト改善と熱伝導経路の強化により、KVM-GO の DP・VGA 版の過熱を解消しました。"
---

# Engineering Log: KVM-GO の DP/VGA 発熱を追跡し、最終的に有効だった対策まで

## 記録 1：「普通に温かい」では済まないと気づいた瞬間
KVM-GO の開発中期、典型的な「小型機器が温まる」想定と異なる熱挙動が現れました。問題が出たのは DisplayPort（DP）と VGA の 2 種だけで、HDMI 版は想定どおりの範囲に収まっていました。

当初の症状は単純でした。筐体温度が想定より早く不快になる。懸念していたのは快適性ではなく、内部温度が民生品の許容範囲を大幅に超えている可能性でした。


---

## 記録 2: なぜ DP と VGA だけか
各バージョンのビデオ経路設計をたどると、パターンが見えてきました。

- HDMI: MS2130S を用いた 1 段変換（HDMI → USB 動画）
- DP: IT6563 + MS2130S の 2 チップで DP → USB 動画に変換
- VGA: MS9288C + MS2109S の 2 チップで VGA → USB 動画に変換

2 チップ構成は部品が増えるだけでなく、電力消費と局所的なホットスポットも増加させます。KVM-GO のようなサイズでは、それらが広がる余地がほとんどありません。

次に制約になったのが表面積です。KVM-GO はサイズを極限まで抑えているため、PCB 面積と有効な放熱面積の両方が小さくなっています。

最後に、レイアウト上の制約が実際の設計トレードオフになりました。2 つの発熱チップを同じ面に置くのは熱的には理想的ですが、ピン配置と高速配線の要件から、その実装は難しい判断となりました。1 つをより内側に置くと配線と信号整合性は有利になりますが、筐体内部に熱がこもる結果になりました。

![Original-PCB-layout](https://assets2.openterface.com/images/Original-PCB-layout.webp)

*オリジナル PCB レイアウト*

![original-Wiring](https://assets2.openterface.com/images/original-Wiring.webp)

*オリジナル高速配線*

![KVM-Go-tructure](https://assets2.openterface.com/images/KVM-Go-tructure.webp)


*KVM-GO 内部スタックレイアウト*

---

## 記録 3: 本質的な指標の計測——内部温度 vs 表面温度
推測をやめ、内外の温度を計測することにしました。外側・内側それぞれの温度測定ポイントを設け、長時間負荷試験を実施しました。

特に VGA で結果は衝撃的でした。

約 1 時間の連続運転後：
- 表面温度は約 65°C に達した
- 内部温度はピーク約 115°C

民生品の多くは最大動作温度が 85°C 前後（部品とグレードによる）です。内部が 3 桁の温度ということは、「触ると熱い」だけではなく、製品寿命の短縮や環境差による不安定な挙動につながり得るレベルでした。 

![Original-emperature-test](https://assets2.openterface.com/images/Original-emperature-test.webp)

*ベースライン温度試験（内部 vs 表面）*

---

## 記録 4: クイック sanity check——強制空冷は効く（が製品解ではない）
何かを再設計する前に、まず検証したかったこと——熱を速く逃がせば、温度は十分下がるか？

DIY ファンを使ったシンプルな強制空冷を試しました。物理法則どおり、温度は目に見えて下がり、試験では約 15°C 低下しました。問題が熱ボトルネックであること、計測誤差やソフトウェアではないことが確認できました。

もう一点はっきりしたのは、ファンは我々の目指す製品形態に合わないということです。KVM-GO はコンパクトで静音、自立型である必要があります。強制空冷は診断ツールにとどめ、最終解とはしませんでした。

![Fan-1png](https://assets2.openterface.com/images/Fan-1png.webp)

*DIY ファン冷却セットアップ*

![Fan-2](https://assets2.openterface.com/images/Fan-2.webp)

*DIY ファン冷却、別アングル*

![Temperature-test-fan](https://assets2.openterface.com/images/Temperature-test-fan.webp)

*ファン冷却時の温度試験*

---

## 記録 5: 対策 1——発熱源を外側へ（信号整合性を損なわずに）
最初の実質的な対策は PCB 上で行いました。2 つの発熱チップをできる限り外側寄りに配置するようレイアウトを詰めました。

「部品を動かすだけ」ではありません。DP と VGA では配線制約が厳しく、特に差動ペアといった高速信号の品質維持は必須です。両チップを外側に置くと配線は難しくなり、信号整合性を落とさないよう慎重に調整しました。

新旧のレイアウトと配線を比較し、実機を組み立てて挙動を確認しました。 

![New-PCB-ayout](https://assets2.openterface.com/images/New-PCB-ayout.webp)

*改訂 PCB レイアウト（チップを外側へ）*

![Wiring-layout-modification](https://assets2.openterface.com/images/Wiring-layout-modification.webp)

*改訂配線（1 パス）*

![Wiring-layout-modification-2](https://assets2.openterface.com/images/Wiring-layout-modification-2.webp)

*改訂配線（重要エリア）*

![PCB-ayout-modifications](https://assets2.openterface.com/images/PCB-ayout-modifications.webp)

*改訂 PCB、検証用に実装*

### 対策 1 後の変化
熱は改善しましたが、二次的な問題が判明しました。温度が筐体へ十分に伝わっておらず、一部エリアが想定より高温のままでした。熱画像では筐体が適切なヒートスプレッダとして機能していないことが示唆されました。

対策 1 でピーク温度は下がりましたが、熱経路は完全には解決していませんでした。  

![Modified-fever-symptoms](https://assets2.openterface.com/images/Modified-fever-symptoms.webp)

*レイアウト変更後の温度（対策 1）*

![Casing-temperature-test](https://assets2.openterface.com/images/Casing-temperature-test.webp)

*筐体熱伝達チェック（対策 1 後）*

---

## 記録 6: 対策 2——実効的な熱経路の構築（CNC アルミブロック + 熱界面材）
この段階から、筐体を単なるカバーではなく熱システムの一部として扱いました。

導入したもの：
- 上下の PCB スタック上の CNC アルミブロック
- 熱界面材（グリスまたはパッド）で、チップからアルミブロック、さらにアルミ筐体へ熱を伝達

目的は単純です。有効な放熱面積を増やし、筐体へ安全に熱が逃げる、安定した低抵抗の熱経路を確保することでした。

![cnc](https://assets2.openterface.com/images/cnc.webp)

*CNC 熱伝導ブロック（対策 2）*

![cnc2](https://assets2.openterface.com/images/cnc2.webp)

*CNC ブロック取り付け詳細*

### 対策 2 後の最終結果
熱伝導経路を追加した結果：
- 表面温度は約 65°C で安定
- 内部温度は約 55°C まで低下

熱画像が求める姿を示しました。熱分布が均一になり、筐体がようやく放熱に寄与し、内部への蓄熱を避けられるようになりました。 

![Temperature-measurement-after-adding-CNC](https://assets2.openterface.com/images/Temperature-measurement-after-adding-CNC.webp)

*CNC 熱伝導追加後の温度（対策 2）*

![CNC-machining](https://assets2.openterface.com/images/CNC-machining.webp)

*CNC 熱伝導後の筐体温度*

---

## 結び
この問題から得た教訓は、「DP と VGA がより熱くなる」だけではありません。多段変換で電力消費が増えるのは予想どおりですが、本当に学んだのは——このサイズの機器では、熱の発生量と同様に、「熱がどこへ行くか」が重要だということです。

対策 1（レイアウト）で内部ホットスポットの深刻度を下げました。  
対策 2（機械的な熱伝導経路）で、持続可能で製品にふさわしい解を得られました。

ファンもなく、ユーザー側の特別な扱いも不要。予測可能な設計になりました。
