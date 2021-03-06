---
title: Xamarin.iOS のパフォーマンス
description: Xamarin.iOS でビルドされたアプリケーションのパフォーマンスを高めるための方法は多数あります。 これらの手法をすべて使用することで、CPU で実行される作業量や、アプリケーションで消費されるメモリ量を大幅に減らすことができます。 この記事では、これらの手法について説明します。
ms.prod: xamarin
ms.assetid: 02b1f628-52d9-49de-8479-f2696546ca3f
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 01/29/2016
ms.openlocfilehash: 3fc6263aa99edb94ae69f1ce8f87835043477392
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2018
---
# <a name="xamarinios-performance"></a>Xamarin.iOS のパフォーマンス

_Xamarin.iOS でビルドされたアプリケーションのパフォーマンスを高めるための方法は多数あります。これらの手法をすべて使用することで、CPU で実行される作業量や、アプリケーションで消費されるメモリ量を大幅に減らすことができます。この記事では、これらの方法について説明します。_

低いアプリケーション パフォーマンスは、さまざまな方法で示されます。 たとえば、アプリケーションが応答しない、スクロールが遅くなった、電池の寿命が減っている可能性がある、などです。 ただし、パフォーマンスを最適化するには、単に効率的なコードを実装するだけでは済みません。 アプリケーション パフォーマンスのユーザー エクスペリエンスも考慮する必要があります。 たとえば、操作の実行によって、ユーザーが他の操作を実行できない状況にならないようにすることで、ユーザー エクスペリエンスを改善できます。

Xamarin.iOS でビルドされたアプリケーションのパフォーマンスとユーザーの体感パフォーマンスを高めるための方法は多数あります。 Windows コモン コントロールには以下が含まれます。

- [強い参照循環を避ける](#avoidcircularreferences)
- [テーブル ビューを最適化する](#optimizetableviews)
- [非透過的なビューを使用する](#opaqueviews)
- [FAT XIB を避ける](#avoidfatxibs)
- [イメージ リソースを最適化する](#optimizeimages)
- [デバイスでテストする](#testondevices)
- [アニメーションと表示の更新を同期する](#synchronizeanimations)
- [コア アニメーションの透過を避ける](#avoidtransparency)
- [コード生成を避ける](#avoidcodegeneration)

> [!NOTE]
> この記事を読む前に、まず、「[Cross-Platform Performance](~/cross-platform/deploy-test/memory-perf-best-practices.md)」(クロスプラットフォーム パフォーマンス) をお読みください。Xamarin プラットフォームを使用してビルドされたアプリケーションのメモリ使用量とパフォーマンスを改善するための、プラットフォーム固有ではない手法について説明されています。

<a name="avoidcircularreferences" />

## <a name="avoid-strong-circular-references"></a>強い循環参照を避ける

場合によっては、ガベージ コレクターからオブジェクトのメモリが再要求されないように、強い参照循環を作成することがあります。 たとえば、[`NSObject`](https://developer.xamarin.com/api/type/Foundation.NSObject/) から派生するサブクラス ([`UIView`](https://developer.xamarin.com/api/type/UIKit.UIView/) から継承されたクラスなど) は、次のコード例のように、`NSObject` から派生したコンテナーに追加され、Objective-C から強く参照されます。

```csharp
class Container : UIView
{
    public void Poke ()
    {
    // Call this method to poke this object
    }
}

class MyView : UIView
{
    Container parent;
    public MyView (Container parent)
    {
        this.parent = parent;
    }

    void PokeParent ()
    {
        parent.Poke ();
    }
}

var container = new Container ();
container.AddSubview (new MyView (container));
```

このコードで `Container` インスタンスを作成すると、C# オブジェクトは Objective-C オブジェクトに対して強い参照を持つことになります。 同様に、`MyView` インスタンスも、Objective-C オブジェクトへの強い参照を持つことになります。

さらに、`container.AddSubview` を呼び出すと、アンマネージ インスタンス `MyView` の参照カウントが増えます。 このとき、Xamarin.iOS ランタイムは `GCHandle` インスタンスを作成することで、マネージ コードの `MyView` オブジェクトを維持し続けます。これは、マネージ オブジェクトが参照を維持し続ける保証がないためです。 マネージ コードの観点からは、`GCHandle` に対する [`AddSubview`](https://developer.xamarin.com/api/member/UIKit.UIView.AddSubview/p/UIKit.UIView/) の呼び出しではなくなった後に `MyView` オブジェクトは再要求されます。

アンマネージ `MyView` オブジェクトは、マネージ オブジェクトを示す `GCHandle` を持つことになります。これは*強いリンク*と呼ばれます。 マネージ オブジェクトには、`Container` インスタンスへの参照が含まれます。 そして `Container` インスタンスには `MyView` オブジェクトへのマネージ参照が含まれます。

含まれるオブジェクトがコンテナーに対するリンクを維持する場合、循環参照の処理に使用できる選択肢がいくつかあります。

-  コンテナーへのリンクを `null` に設定することで、手動で循環を中断する。
-  コンテナーに含まれているオブジェクトを手動で削除する。
-  オブジェクトに対して `Dispose` を呼び出す。
-  コンテナーに対して弱い参照を維持することで、循環参照を避ける。 詳細については、弱い参照のセクションを参照してください。

### <a name="using-weakreferences"></a>弱い参照の使用

循環を避ける方法の 1 つとして、子から親に対して弱い参照を使用する方法などがあります。たとえば、上記のコードは次のように記述することができます。

```csharp
class Container : UIView
{
    public void Poke ()
    {
    // Call this method to poke this object
    }
}

class MyView : UIView
{
    WeakReference<Container> weakParent;
    public MyView (Container parent)
    {
        this.weakParent = new WeakReference<Container> (parent);
    }

    void PokeParent ()
    {
        if (weakParent.TryGetTarget (out var parent))
            parent.Poke ();
    }
}

var container = new Container ();
container.AddSubview (new MyView (container));
```

つまり、含まれるオブジェクトによって親は維持されず、親は `container.AddSubView` に対する呼び出しによって子のみを維持します。

デリゲートまたはデータ ソース パターンを使用する iOS API でも、この用法が利用されます。この場合、たとえば [`Delegate`](https://developer.xamarin.com/api/property/MonoTouch.UIKit.UITableView.Delegate/) プロパティまたは [`DataSource`](https://developer.xamarin.com/api/property/MonoTouch.UIKit.UITableView.DataSource/) を [`UITableView`](https://developer.xamarin.com/api/type/UIKit.UITableView/) クラスで設定するときなどに、ピア クラスに実装が含まれます。

プロトコルを実装するためだけに作成されたクラスの場合 ([`IUITableViewDataSource`](https://developer.xamarin.com/api/type/MonoTouch.UIKit.IUITableViewDataSource/) など) にできることは、サブクラスの作成ではなく、クラスにインターフェイスを実装し、メソッドをオーバーライドし、`DataSource` プロパティを `this` に割り当てることです。

### <a name="disposing-of-objects-with-strong-references"></a>強い参照を使用したオブジェクトの破棄

強い参照が存在し、依存関係を削除するのが困難な場合は、`Dispose` メソッドで親ポインターをクリアします。

コンテナーの場合は、`Dispose` メソッドをオーバーライドして含まれるオブジェクトを削除します。次にコード例を示します。

```csharp
class MyContainer : UIView
{
    public override void Dispose ()
    {
        // Brute force, remove everything
        foreach (var view in Subviews)
        {
              view.RemoveFromSuperview ();
        }
        base.Dispose ();
    }
}
```

親に対する強い参照を維持する子オブジェクトの場合は、`Dispose` 実装で親に対する参照をクリアします。

```csharp
    class MyChild : UIView {
    MyContainer container;
    public MyChild (MyContainer container)
    {
        this.container = container;
    }
    public override void Dispose ()
    {
        container = null;
    }
}
```

強い参照の解放の詳細については、「[Release IDisposable Resources](~/cross-platform/deploy-test/memory-perf-best-practices.md#idisposable)」(IDisposable リソースの解放) を参照してください。
また、ブログの投稿「[Xamarin.iOS, the garbage collector and me](http://krumelur.me/2015/04/27/xamarin-ios-the-garbage-collector-and-me/)」(Xamarin.iOS とガベージ コレクターと私) の説明もお勧めします。

### <a name="more-information"></a>説明

詳細については、Cocoa With Love の「[Rules to Avoid Retain Cycles](http://www.cocoawithlove.com/2009/07/rules-to-avoid-retain-cycles.html)」(循環の保持を回避する規則)、StackOverflow の「[Is this a bug in MonoTouch GC](http://stackoverflow.com/questions/13058521/is-this-a-bug-in-monotouch-gc)」(これは MonoTouch GC のバグですか)、StackOverflow の「[Why can't MonoTouch GC kill managed objects with refcount > 1?](http://stackoverflow.com/questions/13064669/why-cant-monotouch-gc-kill-managed-objects-with-refcount-1)」(参照カウントが 1 を超えるマネージ オブジェクトを MonoTouch GC でキルできないのはなぜですか?) を参照してください。


<a name="optimizetableviews" />

## <a name="optimize-table-views"></a>テーブル ビューを最適化する

ユーザーは[`UITableView`](https://developer.xamarin.com/api/type/UIKit.UITableView/) インスタンスに対してスムーズなスクロールと高速な読み込み時間を期待します。 ただし、セルに深い入れ子のビュー階層が含まれる場合、またはセルに複雑なレイアウトが含まれる場合、スクロールのパフォーマンスは低下する可能性があります。 ただし、`UITableView` のパフォーマンス低下を回避するために使用できる手法があります。

- セルを再利用する。 詳細については、「[Reuse Cells](#reusecells)」(セルの再利用) を参照してください。
- サブビューの数を減らす。
- Web サービスから取得されるセルのコンテンツをキャッシュする。
- 行の高さが同じでない場合はキャッシュする。
- セルと他のビューを非透過的にする。
- イメージのスケーリングとグラデーションを避ける。

これらの手法をすべて使うことで、[`UITableView`](https://developer.xamarin.com/api/type/UIKit.UITableView/) インスタンスのスクロールをスムーズに保つことができます。

<a name="reusecells" />

### <a name="reuse-cells"></a>セルを再利用する

[`UITableView`](https://developer.xamarin.com/api/type/UIKit.UITableView/) で数百行を表示する場合、少数のみが 1 画面に表示されるなら、数百単位の [`UITableViewCell`](https://developer.xamarin.com/api/type/UIKit.UITableViewCell/) オブジェクトを作成するのはメモリの無駄です。 代わりに、画面に表示されるセルのみをメモリに読み込み、その再利用されるセルに**コンテンツ**を読み込むことができます。 こうすることで、数百単位の追加オブジェクトのインスタンス化を防ぎ、時間とメモリを節約することができます。

そのため、次のコード例のように、セルが画面から消えるときに、そのビューを再利用のためのキューに格納できます。

```csharp
class MyTableSource : UITableViewSource
{
    public override UITableViewCell GetCell (UITableView tableView, NSIndexPath indexPath)
    {
        // iOS will create a cell automatically if one isn't available in the reuse pool
        var cell = (MyCell) tableView.DequeueReusableCell (MyCellId, indexPath);

        // Perform required cell actions
        return cell;
    }
}
```

ユーザーがスクロールすると、[`UITableView`](https://developer.xamarin.com/api/type/UIKit.UITableView/) は `GetCell` のオーバーライドを呼び出し、新しいビューの表示を要求します。 このオーバーライドは [`DequeueReusableCell`](https://developer.xamarin.com/api/member/UIKit.UITableView.DequeueReusableCell/p/Foundation.NSString/) メソッドを呼び出し、再利用できるセルがある場合はそのセルが返されます。

詳細については、「[Populating a Table with Data](~/ios/user-interface/controls/tables/populating-a-table-with-data.md)」(データを使用したテーブルの設定) の「[Cell Reuse](~/ios/user-interface/controls/tables/populating-a-table-with-data.md)」(セルの再利用) を参照してください。

<a name="opaqueviews" />

## <a name="use-opaque-views"></a>非透過的なビューを使用する

透過性が定義されていないビューには、[`Opaque`](https://developer.xamarin.com/api/property/UIKit.UIView.Opaque/) プロパティを設定するようにします。 こうすることで、描画システムはビューを最適にレンダリングします。 この方法は、ビューが [`UIScrollView`](https://developer.xamarin.com/api/type/UIKit.UIScrollView/) に埋め込まれている場合、または複雑なアニメーションの一部の場合に特に重要です。 そうしないと、描画システムは他のコンテンツを含むビューを作成し、結果的にパフォーマンスが大きく低下する可能性があります。

<a name="avoidfatxibs" />

## <a name="avoid-fat-xibs"></a>FAT XIB を避ける

大部分の XIB はストーリーボードに置き換えられましたが、まだ XIB が使用されている環境も一部にあります。 XIB がメモリに読み込まれると、すべての画像を含め、すべてのコンテンツがメモリに読み込まれます。 XIB にすぐに使用されないビューが含まれると、メモリは無駄になります。 そのため、XIB を使用する場合は、1 つのビュー コントローラーにつき XIB を 1 つのみにします。また、可能であれば、ビュー コントローラーのビュー階層を別の XIB に分けます。

<a name="optimizeimages" />

## <a name="optimize-image-resources"></a>イメージ リソースを最適化する

アプリケーションが使用するリソースのうち最もコストが高いものとして画像があります。多くの場合、画像は高解像度でキャプチャされます。 そのため、[`UIImageView`](https://developer.xamarin.com/api/type/UIKit.UIImageView/) でアプリのバンドルから画像を表示する場合は、画像と `UIImageView` のサイズが同じになるようにします。 実行時に画像の拡大縮小を行うと、コストの高い操作になる可能性があります。`UIImageView` が [`UIScrollView`](https://developer.xamarin.com/api/type/UIKit.UIScrollView/) に埋め込まれている場合は特にそうです。

詳細については、「[Cross-Platform Performance](~/cross-platform/deploy-test/memory-perf-best-practices.md)」(クロスプラットフォーム パフォーマンス) ガイドの「[Optimize Image Resources](~/cross-platform/deploy-test/memory-perf-best-practices.md#optimizeimages)」(イメージ リソースの最適化) を参照してください。

<a name="testondevices" />

## <a name="test-on-devices"></a>デバイスでテストする

物理デバイスでのアプリケーションの展開とテストは、できるだけ早く始めます。 シミュレーターは、デバイスの動作と制限とまったく同じではありません。そのため、できるだけはやく実際のデバイスのシナリオでテストすることが重要です。

特に、シミュレーターでは、物理デバイスのメモリまたは CPU の制限をシミュレートすることはできません。

<a name="synchronizeanimations" />

## <a name="synchronize-animations-with-the-display-refresh"></a>アニメーションと表示の更新を同期する

ゲームには、ゲーム ロジックを実行し、画面を更新するループが詰まっている傾向があります。 一般的なフレーム レート範囲は 1 秒あたり 30 から 60 フレームです。 開発者によっては、1 秒あたりの画面の更新回数を可能な限り多くした方がよいと考え、ゲームのシミュレーションを画面の更新を組み合わせて、1 秒あたりのフレーム数を 60 超にしようとするかもしれません。

一方、ディスプレイ サーバーは 1 秒あたり 60 下位の上限で画面の更新を実行します。 そのため、この上限よりも高速に画面を更新しようとすると、画面の停止や途切れが発生する可能性があります。 画面の更新がディスプレイの更新と同期するようにコードを作成することをお勧めします。 この同期には、[`CoreAnimation.CADisplayLink`](https://developer.xamarin.com/api/type/CoreAnimation.CADisplayLink/) クラスを使用できます。このクラスは、1 秒あたり 60 フレームで実行される視覚化やゲームに適したタイマーです。

<a name="avoidtransparency" />

## <a name="avoid-core-animation-transparency"></a>コア アニメーションの透過を避ける

コア アニメーションの透過を避けることで、ビットマップ作成のパフォーマンスが改善されます。 一般的に、可能な限り透過レイヤーと罫線のぼかしを避けることをお勧めします。

<a name="avoidcodegeneration" />

## <a name="avoid-code-generation"></a>コード生成を避ける

`System.Reflection.Emit` または*動的言語ランタイム*による動的なコード生成は避ける必要があります。これは、iOS カーネルが動的なコード実行を回避するからです。

## <a name="summary"></a>まとめ

この記事では、Xamarin.iOS でビルドされたアプリケーションのパフォーマンスを高めるための手法について説明しました。 これらの手法をすべて使用することで、CPU で実行される作業量や、アプリケーションで消費されるメモリ量を大幅に減らすことができます。

## <a name="related-links"></a>関連リンク

- [クロスプラットフォームのパフォーマンス](~/cross-platform/deploy-test/memory-perf-best-practices.md)
