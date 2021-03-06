---
title: Android プラットフォーム機能
description: Xamarin.Forms アプリを Android 固有の機能を追加します。
ms.prod: xamarin
ms.assetid: E24168F3-0138-4814-86EA-B467F6B8A545
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 01/13/2016
ms.openlocfilehash: 3648f6f5f576a77bf7887668352c4f3d11f3906d
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2018
---
# <a name="android-platform-features"></a>Android プラットフォーム機能

## <a name="platform-support"></a>プラットフォームのサポート

Xamarin.Forms Android プロジェクトの既定値は、Android 5.0 の前に共通したコントロール renderering の以前のスタイルを使用します。 テンプレートを使用して構築されたアプリケーションが`FormsApplicationActivity`メインのアクティビティの基本クラスとして。

## <a name="material-design-via-appcompat"></a>AppCompat 経由での素材のデザイン

Xamarin.Forms も省略可能な`FormsAppCompatActivity`を使用して**AppCompat**マテリアル デザインのテーマを実装する Android によって提供される機能です。

次の資料デザインのテーマを Xamarin.Forms Android プロジェクトを追加する、 [AppCompat のインストール手順のサポート](appcompat.md)

ここでは、 **Todo** 、既定値はサンプル`FormsApplicationActivity`:

[![](images/before-appcompat-sml.png "AppCompat なしの Todo サンプル アプリケーション")](images/before-appcompat.png#lightbox "AppCompat なしの Todo サンプル アプリケーション")

これとは、同じコードを使用するプロジェクトをアップグレードした後`FormsAppCompatActivity`(およびその他のテーマ情報を追加する)。

[![](images/post-appcompat-sml.png "AppCompat とテーマでの Todo サンプル アプリケーション")](images/post-appcompat.png#lightbox "AppCompat とテーマでの Todo サンプル アプリケーション")

> [!NOTE]
> 使用する場合`FormsAppCompatActivity`、[一部 Android のカスタム レンダラーの基本クラス](~/xamarin-forms/app-fundamentals/custom-renderer/renderers.md)異なるになります。


## <a name="related-links"></a>関連リンク

- [素材のデザインのサポートを追加します。](appcompat.md)
