---
title: Xamarin.Forms の詳細
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: d97aa580-1eb9-48b3-b15b-0d7421ea7ae
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/06/2018
ms.openlocfilehash: e254aa14f5889cee6b5bee452f5275fd579eb8fc
ms.sourcegitcommit: 1561c8022c3585655229a869d9ef3510bf83f00a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2018
---
# <a name="xamarinforms-deep-dive"></a>Xamarin.Forms の詳細

「[Xamarin.Forms Quickstart](~/xamarin-forms/get-started/hello-xamarin-forms/quickstart.md)」(Xamarin.Forms クイックスタート) では、設定アプリケーションを構築しました。 この記事では、Xamarin.Forms アプリケーションのしくみの基礎を理解するために、構築された内容を確認します。

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

## <a name="introduction-to-visual-studio"></a>Visual Studio の概要

Visual Studio は Microsoft 製の強力な IDE です。 ビジュアル デザイナー、リファクタリング ツール付きのテキスト エディター、アセンブリ ブラウザー、ソース コード統合などの機能が完全に統合されています。 この記事では、主に Visual Studio の基本的な機能の一部と Xamarin プラグインを使用します。

Visual Studio は、コードを*ソリューション*と*プロジェクト*に分けて整理しています。 ソリューションとは、1 つまたは複数のプロジェクトを保持できるコンテナーです。 プロジェクトは、アプリケーション、サポートするライブラリ、テスト アプリケーションなどの場合があります。 Phoneword アプリケーションは、次のスクリーンショットのように、4 つのプロジェクトを含む 1 つのソリューションで構成されています。

![](deepdive-images/vs/solution.png "Visual Studio ソリューション エクスプローラー")

プロジェクトの内容:

- Phoneword - このプロジェクトは、すべての共有コードと共有 UI を保持する .NET Standard ライブラリ プロジェクトです。
- Phoneword.Android - このプロジェクトは、Android 固有のコードを保持します。Android アプリケーションのエントリ ポイントです。
- Phoneword.iOS: このプロジェクトは、iOS 固有のコードを保持します。iOS アプリケーションのエントリ ポイントです。
- Phoneword.UWP: このプロジェクトは、ユニバーサル Windows プラットフォーム (UWP) 固有のコードを保持します。UWP アプリケーションのエントリ ポイントです。

## <a name="anatomy-of-a-xamarinforms-application"></a>Xamarin.Forms アプリケーションの構造

次のスクリーンショットは、Visual Studio の Phoneword .NET Standard プロジェクトの内容です。

![](deepdive-images/vs/net-standard-project.png "Phoneword .NET Standard プロジェクトの内容")

このプロジェクトには、**NuGet** ノードと **SDK** ノードを含む **Dependencies** ノードがあります。 **NuGet** ノードには、プロジェクトに追加された Xamarin.Forms NuGet パッケージが含まれています。**SDK** ノードには .NET Standard を定義する NuGet パッケージの完全なセットを参照する `NETStandard.Library` メタパッケージが含まれています。

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

## <a name="introduction-to-visual-studio-for-mac"></a>Visual Studio for Mac の概要

Visual Studio for Mac は、Visual Studio と類似した無料のオープン ソース IDE です。 ビジュアル デザイナー、リファクタリング ツール付きのテキスト エディター、アセンブリ ブラウザー、ソース コード統合などの機能が完全に統合されています。 Visual Studio for Mac の詳細については、[Visual Studio for Mac の概要](/visualstudio/mac/)のページをご覧ください。

Visual Studio for Mac は、コードを*ソリューション*と*プロジェクト*に分けて整理するという Visual Studio の方法に従っています。 ソリューションとは、1 つまたは複数のプロジェクトを保持できるコンテナーです。 プロジェクトは、アプリケーション、サポートするライブラリ、テスト アプリケーションなどの場合があります。 Phoneword アプリケーションは、次のスクリーンショットのように、3 つのプロジェクトを含む 1 つのソリューションで構成されています。

![](deepdive-images/xs/solution.png "Visual Studio for Mac ソリューション ウィンドウ")

プロジェクトの内容:

- Phoneword: このプロジェクトは、すべての共有コードと共有 UI を保持するポータブル クラス ライブラリ (PCL) プロジェクトです。
- Phoneword.Droid: このプロジェクトは、Android 固有のコードを保持します。Android アプリケーションのエントリ ポイントです。
- Phoneword.iOS: このプロジェクトは、iOS 固有のコードを保持します。iOS アプリケーションのエントリ ポイントです。

## <a name="anatomy-of-a-xamarinforms-application"></a>Xamarin.Forms アプリケーションの構造

次のスクリーンショットは、Visual Studio for Mac の Phoneword PCL プロジェクトの内容です。

![](deepdive-images/xs/pcl-project.png "Phoneword PCL プロジェクトの内容")

このプロジェクトは 3 つのフォルダーで構成されています。

- **参照**: アプリケーションのビルドと実行に必要なアセンブリが含まれています。 [.NET ポータブル サブセット] フォルダーを展開すると、[System](http://msdn.microsoft.com/library/system%28v=vs.110%29.aspx)、System.Core、[System.Xml](http://msdn.microsoft.com/library/system.xml%28v=vs.110%29.aspx) などの .NET アセンブリの参照が表示されます。 **[パッケージから]** フォルダーを展開すると、Xamarin.Forms アセンブリの参照が表示されます。
- **パッケージ**: [パッケージ] ディレクトリには [NuGet](https://www.nuget.org) パッケージが含まれています。NuGet パッケージは、アプリケーションでサードパーティ ライブラリを使用するプロセスを簡略化するパッケージです。 これらのパッケージを最新リリースに更新するには、フォルダーを右クリックし、ポップアップ メニューの更新オプションを選択します。
- **プロパティ**: .NET アセンブリ メタデータ ファイルである **AssemblyInfo.cs** が含まれています。 このファイルには、アプリケーションに関する基本的な情報を入力しておくことをお勧めします。 このファイルの詳細については、MSDN の「[AssemblyInfo Class](http://msdn.microsoft.com/library/microsoft.visualbasic.applicationservices.assemblyinfo(v=vs.110).aspx)」(AssemblyInfo クラス) を参照してください。

-----

このプロジェクトには、以下の複数のファイルも含まれています。

- **App.xaml**: `App` クラスの XAML マークアップ。アプリケーションのリソース ディクショナリを定義します。
- **App.xaml.cs**: `App` クラスの分離コード。各プラットフォーム上のアプリケーションで表示される最初のページのインスタンス化と、アプリケーションのライフサイクル イベント処理を担当します。
- **IDialer.cs**: `IDialer` インターフェイス。いずれかの実装クラスで `Dial` メソッドを提供する必要があることを指定します。
- **MainPage.xaml**: `MainPage` クラスの XAML マークアップ。アプリケーションの起動時に表示されるページの UI を定義します。
- **MainPage.xaml.cs**: `MainPage` クラスの分離コード。ユーザーがページを操作したときに実行されるビジネス ロジックが含まれています。
- **packages.config** - (Visual Studio for Mac のみ) プロジェクトが使用している NuGet パッケージに関する情報が含まれている XML ファイル。必要なパッケージとそれぞれのバージョンを追跡するために使用されます。 Visual Studio for Mac と Visual Studio のいずれも、ソース コードを他のユーザーと共有するときに不足している NuGet パッケージを自動的に復元するように構成することができます。 このファイルの内容は、NuGet パッケージ マネージャーが制御するため、手動では編集しないでください。
- **PhoneTranslator.cs**: フォン ワード (電話のボタンに印字されている英数字を使った単語) を電話番号に変換する処理を担当するビジネス ロジックです。**MainPage.xaml.cs** から呼び出します。

Xamarin.iOS アプリケーションの構造については、「[Anatomy of a Xamarin.iOS Application](~/ios/get-started/hello-ios/hello-ios-deepdive.md#anatomy)」(Xamarin.iOS アプリケーションの構造) を参照してください。 Xamarin.Android アプリケーションの構造については、「[Anatomy of a Xamarin.Android Application](~/android/get-started/hello-android/hello-android-deepdive.md#anatomy)」(Xamarin.Android アプリケーションの構造) を参照してください。

## <a name="architecture-and-application-fundamentals"></a>アーキテクチャとアプリケーションの基礎

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Xamarin.Forms アプリケーションは、従来のクロスプラットフォーム アプリケーションと同じ方法で設計されています。 通常、共有コードは .NET Standard ライブラリに配置され、プラットフォーム固有のアプリケーションは共有コードを使用します。 次の図は、Phoneword アプリケーションのこの関係の概要を示しています。

![](deepdive-images/vs/architecture.png "Phoneword アーキテクチャ")

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

Xamarin.Forms アプリケーションは、従来のクロスプラットフォーム アプリケーションと同じ方法で設計されています。 通常、共有コードはポータブル クラス ライブラリ (PCL) に配置され、プラットフォーム固有のアプリケーションは共有コードを使用します。 次の図は、Phoneword アプリケーションのこの関係の概要を示しています。

![](deepdive-images/xs/architecture.png "Phoneword アーキテクチャ")

PCL の詳細については、「[Introduction to Portable Class Libraries](~/cross-platform/app-fundamentals/pcl.md)」(ポータブル クラス ライブラリの概要) を参照してください。

-----

スタートアップ コードを最大限に再利用するために、Xamarin.Forms アプリケーションは `App` という 1 つのクラスがあります。このクラスは、各プラットフォーム上のアプリケーションが表示する最初のページのインスタンス化を担当しています。次にコード例を示します。

```csharp
using Xamarin.Forms;
using Xamarin.Forms.Xaml;

[assembly: XamlCompilation(XamlCompilationOptions.Compile)]
namespace Phoneword
{
    public partial class App : Application
    {
        public App()
        {
            InitializeComponent();
            MainPage = new MainPage();
        }
        ...
    }
}
```

このコードは、`App` クラスの `MainPage` プロパティを、[`MainPage`](https://developer.xamarin.com/api/property/Xamarin.Forms.Application.MainPage/) クラスの新しいインスタンスに設定します。 また、XAML コンパイラで [`XamlCompilation`](https://developer.xamarin.com/api/type/Xamarin.Forms.Xaml.XamlCompilationAttribute/) 属性が有効なので、XAML は中間言語に直接コンパイルされます。 詳細については、「[XAML Compilation](~/xamarin-forms/xaml/xamlc.md)」(XAML のコンパイル) を参照してください。

## <a name="launching-the-application-on-each-platform"></a>各プラットフォームでのアプリケーションの起動

### <a name="ios"></a>iOS

iOS で最初の Xamarin.Forms ページを起動するために、Phoneword.iOS プロジェクトには、`FormsApplicationDelegate` から継承した `AppDelegate` クラスが含まれています。次にコード例を示します。

```csharp
namespace Phoneword.iOS
{
    [Register ("AppDelegate")]
    public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate
    {
        public override bool FinishedLaunching (UIApplication app, NSDictionary options)
        {
            global::Xamarin.Forms.Forms.Init ();
            LoadApplication (new App ());
            return base.FinishedLaunching (app, options);
        }
    }
}
```

`FinishedLaunching` オーバーライドは、`Init` メソッドを呼び出して Xamarin.Forms のフレームワークを初期化します。 その結果、Xamarin.Forms の iOS 固有の実装がアプリケーションに読み込まれ、次に `LoadApplication` メソッドの呼び出しによってルート ビュー コントローラーが設定されます。

### <a name="android"></a>Android

Android で最初の Xamarin.Forms ページを起動するために、Phoneword.Droid プロジェクトには、`MainLauncher` 属性を指定した `Activity` を作成し、`FormsApplicationActivity` クラスから継承したアクティビティが使用するコードが含まれています。次にコード例を示します。

```csharp
namespace Phoneword.Droid
{
    [Activity(Label = "Phoneword",
              Icon = "@drawable/icon",
              MainLauncher = true,
              ConfigurationChanges = ConfigChanges.ScreenSize | ConfigChanges.Orientation)]
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity
    {
        internal static MainActivity Instance { get; private set; }

        protected override void OnCreate(Bundle bundle)
        {
            base.OnCreate(bundle);

            Instance = this;
            global::Xamarin.Forms.Forms.Init(this, bundle);
            LoadApplication(new App());
        }
    }
}
```

`OnCreate` オーバーライドは、`Init` メソッドを呼び出して Xamarin.Forms のフレームワークを初期化します。 その結果、Xamarin.Forms の Android 固有の実装がアプリケーションに読み込まれ、次に Xamarin.Forms アプリケーションが読み込まれます。 さらに、`MainActivity` クラスは自身への参照を `Instance` プロパティに格納します。 `Instance` プロパティはローカル コンテキストと呼ばれ、`PhoneDialer` クラスから参照されます。

## <a name="universal-windows-platform"></a>ユニバーサル Windows プラットフォーム

ユニバーサル Windows プラットフォーム (UWP) アプリケーションでは、Xamarin.Forms フレームワークを初期化する `Init` メソッドが `App` から呼び出されます。

```csharp
Xamarin.Forms.Forms.Init (e);

if (e.PreviousExecutionState == ApplicationExecutionState.Terminated)
{
  ...
}
```

その結果、Xamarin.Forms の UWP 固有の実装がアプリケーションに読み込まれます。 最初の Xamarin.Forms ページは、次のコード例のように `MainPage` クラスによって起動されます。

```csharp
namespace Phoneword.UWP
{
    public sealed partial class MainPage
    {
        public MainPage()
        {
            this.InitializeComponent();
            this.LoadApplication(new Phoneword.App());
        }
    }
}
```

Xamarin.Forms アプリケーションは `LoadApplication` メソッドを使用して読み込まれます。

> [!NOTE]
> ユニバーサル Windows プラットフォーム (UWP) アプリは Xamarin.Forms を使用して構築できますが、Windows で Visual Studio を使用している必要があります。

## <a name="user-interface"></a>ユーザー インターフェイス

Xamarin.Forms アプリケーションのユーザー インターフェイスを作成するために、主に 4 つのコントロール グループが使用されます。

1. **ページ**: Xamarin.Forms のページは、クロスプラットフォーム モバイル アプリケーション画面を表しています。 Phoneword アプリケーションは、1 つの画面を表示するために [`ContentPage`](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentPage/) クラスを使用します。 ページの詳細については、「[Xamarin.Forms Pages](~/xamarin-forms/user-interface/controls/pages.md)」(Xamarin.Forms のページ) を参照してください。
1. **レイアウト**: Xamarin.Forms のレイアウトは、ビューを論理構造にまとめるために使用されるコンテナーです。 Phoneword アプリケーションは、[`StackLayout`](https://developer.xamarin.com/api/type/Xamarin.Forms.StackLayout/) クラスを使用して水平方向のスタックにコントロールを整列します。 レイアウトの詳細については、「[Xamarin.Forms Layouts](~/xamarin-forms/user-interface/controls/layouts.md)」(Xamarin.Forms のレイアウト) を参照してください。
1. **ビュー**: Xamarin.Forms のビューは、ユーザー インターフェイスに表示されるコントロールです。たとえば、ラベル、ボタン、テキスト入力ボックスなどです。 Phoneword アプリケーションは、[`Label`](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/)、[`Entry`](https://developer.xamarin.com/api/type/Xamarin.Forms.Entry/)、[`Button`](https://developer.xamarin.com/api/type/Xamarin.Forms.Button/) コントロールを使用します。 ビューの詳細については、「[Xamarin.Forms Views](~/xamarin-forms/user-interface/controls/views.md)」(Xamarin.Forms のビュー) を参照してください。
1. **セル**: Xamarin.Forms セルは、一覧内の項目に使用される特殊な要素です。一覧内の各項目を描画する方法を示しています。 Phoneword アプリケーションはセルを利用していません。 セルの詳細については、「[Xamarin.Forms Cells](~/xamarin-forms/user-interface/controls/cells.md)」(Xamarin.Forms のセル) を参照してください。

実行時に、各コントロールはネイティブの同等のものにマップされます。そしてそれがレンダリングされます。

どのプラットフォームでも、Phoneword アプリケーションを実行すると、Xamarin.Forms の [`Page`](https://developer.xamarin.com/api/type/Xamarin.Forms.Page/) に対応する 1 つの画面が表示されます。 `Page` は、Android では *ViewGroup*、iOS では *View Controller*、ユニバーサル Windows プラットフォームでは *Page* を表します。 また、Phoneword アプリケーションは、`MainPage` クラスを表す [`ContentPage`](https://developer.xamarin.com/api/type/Xamarin.Forms.ContentPage/) オブジェクトをインスタンス化します。その XAML マークアップを次のコード例に示します。

```xaml
<?xml version="1.0" encoding="UTF-8"?>
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
                         xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
                         x:Class="Phoneword.MainPage">
        ...
        <StackLayout>
            <Label Text="Enter a Phoneword:" />
            <Entry x:Name="phoneNumberText" Text="1-855-XAMARIN" />
            <Button x:Name="translateButon" Text="Translate" Clicked="OnTranslate" />
            <Button x:Name="callButton" Text="Call" IsEnabled="false" Clicked="OnCall" />
        </StackLayout>
</ContentPage>
```

画面サイズに関係なく、`MainPage` クラスは [`StackLayout`](https://developer.xamarin.com/api/type/Xamarin.Forms.StackLayout/) コントロールを使用して画面上のコントロールを自動的に整列します。 各子要素は、追加した順に、垂直方向に 1 つずつ配置されます。 `StackLayout` コントロールには、ページにテキストを表示する 1 つの [`Label`](https://developer.xamarin.com/api/type/Xamarin.Forms.Label/) コントロール、テキスト ユーザー入力を受け入れる 1 つの [`Entry`](https://developer.xamarin.com/api/type/Xamarin.Forms.Entry/) コントロール、タッチ イベントに応答してコードを実行するために使用される 2 つの [`Button`](https://developer.xamarin.com/api/type/Xamarin.Forms.Button/) コントロールが含まれています。

Xamarin.Forms の XAML の詳細については、「[Xamarin.Forms XAML Basics](~/xamarin-forms/xaml/xaml-basics/index.md)」(Xamarin.Forms XAML の基礎) を参照してください。

### <a name="responding-to-user-interaction"></a>ユーザー操作に対する応答

XAML に定義されているオブジェクトによって、分離コード ファイルで処理されるイベントが発生する可能性があります。 次のコード例は、`MainPage` クラスの分離コードの `OnTranslate` メソッドを示しています。*[Translate]\(変換\)* ボタンによって発生する [`Clicked`](https://developer.xamarin.com/api/event/Xamarin.Forms.Button.Clicked/) イベントに応答して実行されます。

```csharp
void OnTranslate(object sender, EventArgs e)
{
    translatedNumber = Core.PhonewordTranslator.ToNumber (phoneNumberText.Text);
    if (!string.IsNullOrWhiteSpace (translatedNumber)) {
        callButton.IsEnabled = true;
        callButton.Text = "Call " + translatedNumber;
    } else {
        callButton.IsEnabled = false;
        callButton.Text = "Call";
    }
}
```

`OnTranslate` メソッドによってフォンワードが対応する電話番号に変換され、応答で、呼び出しボタンのプロパティが設定されます。 XAML クラスの分離コード ファイルは、`x:Name` 属性を指定して割り当てられた名前を使用して、XAML に定義されているオブジェクトにアクセスできます。 この属性に割り当てられている値は、C# 変数と同じルールを持っています。つまり、英字またはアンダースコアから始まり、埋め込みスペースが含まれる必要があります。

変換ボタンから `OnTranslate` メソッドに接続する処理は、`MainPage` クラスの XAML マークアップで発生します。

```xaml
<Button x:Name="translateButon" Text="Translate" Clicked="OnTranslate" />
```

## <a name="additional-concepts-introduced-in-phoneword"></a>Phoneword で導入されているその他の概念

Xamarin.Forms 用 Phoneword アプリケーションは、このガイドでは説明していない概念をいくつか導入しました。 たとえば、次のような概念です。

- ボタンの有効化と無効化。 [`Button`](https://developer.xamarin.com/api/type/Xamarin.Forms.Button/) は、[`IsEnabled`](https://developer.xamarin.com/api/property/Xamarin.Forms.VisualElement.IsEnabled/) プロパティを変更することでオン/オフを切り替えることができます。 たとえば、次のコード例は `callButton` を無効にしています。

    ```csharp
    callButton.IsEnabled = false;
    ```

- アラート ダイアログを表示します。 ユーザーが呼び出し**ボタン**を押すと、Phoneword アプリケーションは、発信または通話のキャンセルを行うオプションを含む*アラート ダイアログ*を表示します。 [`DisplayAlert`](https://developer.xamarin.com/api/member/Xamarin.Forms.Page.DisplayAlert/p/System.String/System.String/System.String/System.String/) メソッドは、次のコード例のようにダイアログを作成するために使用されます。

    ```csharp
    await this.DisplayAlert (
            "Dial a Number",
            "Would you like to call " + translatedNumber + "?",
            "Yes",
            "No");
    ```

- [`DependencyService`](https://developer.xamarin.com/api/type/Xamarin.Forms.DependencyService/) クラス経由でネイティブ機能にアクセスします。 Phoneword アプリケーションは `DependencyService` クラスを使用して `IDialer` インターフェイスをプラットフォーム固有の電話ダイヤル処理の実装に解決します。次に Phoneword プロジェクトのコード例を示します。

    ```csharp
    async void OnCall (object sender, EventArgs e)
    {
        ...
        var dialer = DependencyService.Get<IDialer> ();
        ...
    }
    ```

  [`DependencyService`](https://developer.xamarin.com/api/type/Xamarin.Forms.DependencyService/) クラスの詳細については、「[Accessing Native Features via the DependencyService](~/xamarin-forms/app-fundamentals/dependency-service/index.md)」(DependencyService 経由でネイティブ機能にアクセスする) を参照してください。

- URL を使用して電話をかけます。 Phoneword アプリケーションは `OpenURL` を使用してシステム電話アプリを起動します。 URL は、`tel:` プレフィックスと、それに続く発信先電話番号から構成されます。次に iOS プロジェクトのコード例を示します。

    ```csharp
    return UIApplication.SharedApplication.OpenUrl (new NSUrl ("tel:" + number));
    ```

- プラットフォーム レイアウトの調整 開発者は [`Device`](https://developer.xamarin.com/api/type/Xamarin.Forms.Device/) クラスを使用して、プラットフォームごとのアプリケーションのレイアウトと機能をカスタマイズすることができます。次のコード例では、さまざまなプラットフォーム上のさまざまな [`Padding`](https://developer.xamarin.com/api/property/Xamarin.Forms.Layout.Padding/) 値を使用して、各ページを正しく表示しています。

    ```xaml
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms" ... >
        <ContentPage.Padding>
            <OnPlatform x:TypeArguments="Thickness">
                <On Platform="iOS" Value="20, 40, 20, 20" />
                <On Platform="Android, UWP" Value="20" />
            </OnPlatform>
        </ContentPage.Padding>
        ...
    </ContentPage>
    ```

  プラットフォームの調整については、「[Device Class](~/xamarin-forms/platform/device.md)」(デバイス クラス) を参照してください。

## <a name="testing-and-deployment"></a>テストと展開

Visual Studio for Mac と Visual Studio のいずれも、アプリケーションをテストおよび展開するためのオプションを多数用意しています。 アプリケーションのデバッグは、アプリケーション開発ライフサイクルの一般的な部分であり、コードの問題を診断するときに役立ちます。 詳細については、「[Set a Breakpoint](https://developer.xamarin.com/recipes/cross-platform/ide/debugging/set_a_breakpoint/)」(ブレークポイントの設定)、「[Step Through Code](https://developer.xamarin.com/recipes/cross-platform/ide/debugging/step_through_code/)」(コードのステップ スルー)、「[Output Information to the Log Window](https://developer.xamarin.com/recipes/cross-platform/ide/debugging/output_information_to_log_window/)」(ログ ウィンドウへの出力情報) を参照してください。

シミュレーターは、アプリケーションの展開とテストを始めるにはおすすめの場所です。また、テスト アプリケーションに役立つ機能があります。 ただし、ユーザーは完成したアプリケーションをシミュレーター上では使用しないので、早期に、そして何度も実際のデバイス上でアプリケーションをテストすることをお勧めします。 iOS デバイスのプロビジョニングの詳細については、「[Device Provisioning](~/ios/get-started/installation/device-provisioning/index.md)」(デバイスのプロビジョニング) を参照してください。 Android デバイスのプロビジョニングの詳細については、「[Set Up Device for Development](~/android/get-started/installation/set-up-device-for-development.md)」(開発用のデバイスの設定) を参照してください。

## <a name="summary"></a>まとめ

この記事では、Xamarin.Forms を使用したアプリケーション開発の基礎について説明しました。 たとえば、Xamarin.Forms アプリケーションの構造、アプリケーションのアーキテクチャ、と基礎、ユーザー インターフェイスについて説明しました。

このガイドの次のセクションでは、より高度な Xamarin.Forms アーキテクチャと概念を探るために、複数の画面を含むようにアプリケーションを拡張します。
