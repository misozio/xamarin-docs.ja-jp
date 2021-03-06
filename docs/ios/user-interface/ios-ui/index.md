---
title: IOS のユーザー インターフェイス
description: Xamarin.iOS アプリでは、iOS ユーザー インターフェイスの操作について説明します。
ms.prod: xamarin
ms.assetid: 1BB46561-F503-491E-A27C-7878E7EBE00B
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 06/14/2017
ms.openlocfilehash: dd07ba6853901c93ad26b371ea88b7d39c37d3f7
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2018
---
# <a name="user-interface-in-ios"></a>IOS のユーザー インターフェイス

## <a name="appearance-apiintroduction-to-the-appearance-apimd"></a>[外観 API](introduction-to-the-appearance-api.md)

iOS では、UIAppearance Api を使用してテーマを指定するユーザー インターフェイス コントロールの多くの視覚属性を使用できます。

## <a name="creating-user-interface-objectsiosuser-interfaceios-uicreating-ui-objectsmd"></a>[ユーザー インターフェイス オブジェクトの作成](~/ios/user-interface/ios-ui/creating-ui-objects.md)

機能と同じで Xamarin.iOS 名前空間の「フレームワーク」を使用する Apple のグループの関連部分です。 `UIKit` iOS 用のすべてのユーザー インターフェイス コントロールを含む名前空間がします。

## <a name="layout-optionsiosuser-interfaceios-uilayout-optionsmd"></a>[レイアウト オプション](~/ios/user-interface/ios-ui/layout-options.md)

ビューがサイズ変更、または回転したときに、レイアウトを制御するための 2 つの異なるメカニズムがある: サイズの自動変更し、自動レイアウトです。

## <a name="providing-haptic-feedbackiosuser-interfaceios-uihaptic-feedbackmd"></a>[Haptic フィードバックの提供](~/ios/user-interface/ios-ui/haptic-feedback.md)

この記事では、Xamarin.iOS でそれらを実装する方法と iOS 10 で使用できる haptic フィードバックの新しい型について説明します。

## <a name="working-with-the-ui-threadiosuser-interfaceios-uiui-threadmd"></a>[UI スレッドの操作](~/ios/user-interface/ios-ui/ui-thread.md)

コードを変更するユーザーのメイン インターフェイス コントロール (または UI) スレッドのみ行います。 (コールバックまたはバック グラウンドのスレッド) などの別のスレッドで発生する UI の更新は、画面にレンダリング取得されない可能性があります。 またはクラッシュが生じる場合もします。




