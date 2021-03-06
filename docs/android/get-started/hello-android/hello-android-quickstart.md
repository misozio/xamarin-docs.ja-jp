---
title: 'Hello, Android: クイック スタート'
description: このガイドは 2 つに分かれています。最初に (Visual Studio または Visual Studio for Mac を使用して) Xamarin.Android アプリケーションを作成し、Xamarin での Android アプリケーション開発の基礎について理解を深めます。 その過程で、Xamarin.Android アプリケーションの作成と展開に必要なツール、概念、および手順を紹介します。
ms.topic: quickstart
ms.prod: xamarin
ms.assetid: 44007FA1-3ABC-4935-BF52-4613AF0553A6
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 04/25/2018
ms.openlocfilehash: 44c3e4b0f05526560ff4b32808ba476110ce5e8f
ms.sourcegitcommit: 1561c8022c3585655229a869d9ef3510bf83f00a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2018
---
# <a name="hello-android-quickstart"></a>Hello, Android: クイック スタート

_このガイドは 2 つに分かれています。最初に (Visual Studio または Visual Studio for Mac を使用して) Xamarin.Android アプリケーションを作成し、Xamarin での Android アプリケーション開発の基礎について理解を深めます。その過程で、Xamarin.Android アプリケーションの作成と展開に必要なツール、概念、および手順を紹介します。_

## <a name="hello-android-quickstart"></a>Hello, Android クイック スタート

このチュートリアルでは、英数字の電話番号 (ユーザーが入力) を数字の電話番号に変換し、その番号をユーザーに表示するアプリケーションを作成します。 最終的にアプリケーションは次のようになります。

[![完成時のアプリのスクリーンショット](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)


## <a name="requirements"></a>必要条件

このチュートリアルに従うには、以下が必要になります。

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

-   Windows 7 以降。

-   Visual Studio 2015 Professional 以降。

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

-   Visual Studio for Mac の最新バージョン。

-   OS X Yosemite 以降。

-----

このチュートリアルでは、最新バージョンの Xamarin.Android が任意のプラットフォームでインストールされ、実行されていることを前提とします。 Xamarin.Android のインストール ガイドについては、[Xamarin.Android のインストール](~/android/get-started/installation/index.md)に関するガイドを参照してください。
作業を開始する前に、[Xamarin App Icons & Launch Screens](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true) セットをダウンロードして解凍してください。

## <a name="configuring-emulators"></a>エミュレーターの構成

Google の Android SDK エミュレーターを使用している場合は、ハードウェア アクセラレータを使用するようにエミュレーターを構成することをお勧めします。 ハードウェア アクセラレータを構成するための手順は、[ハードウェアの高速化](~/android/get-started/installation/android-emulator/hardware-acceleration.md)に関するページで確認できます。

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Visual Studio の Android エミュレーターを使用している場合は、コンピューターで Hyper-V を有効にする必要があります。 Visual Studio の Android エミュレーターの構成の詳細については、「[Visual Studio Emulator for Android のシステム要件](https://msdn.microsoft.com/en-us/library/mt228280.aspx)」を参照してください。

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

-----

## <a name="walkthrough"></a>チュートリアル

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Visual Studio を起動します。  **[ファイル]、[新規]、[プロジェクト]** の順にクリックして、新しいプロジェクトを作成します。

**[新しいプロジェクト]** ダイアログで、**[空のアプリ (Android)]** テンプレートをクリックします。
新しいプロジェクトに `Phoneword` という名前を付けます。 **[OK]** をクリックして、新しいプロジェクトを作成します。

[![新しいプロジェクトが Phoneword であることを示すスクリーンショット](hello-android-quickstart-images/vs/02-new-project-name-sml.png)](hello-android-quickstart-images/vs/02-new-project-name.png#lightbox)

### <a name="creating-the-layout"></a>レイアウトの作成

新しいプロジェクトが作成されたら、**ソリューション エクスプローラー**で **Resources** フォルダーを展開してから **layout** フォルダーを展開します。
**Main.axml** をダブルクリックして、Android Designer で開きます。 アプリの画面の layout ファイルを以下に示します。

[![Main.axml を開く](hello-android-quickstart-images/vs/04-open-layout-sml.png)](hello-android-quickstart-images/vs/04-open-layout.png#lightbox)

**[ツールボックス]** (左側の領域) の検索フィールドに「`text`」と入力し、デザイン サーフェイス (中央の領域) に **Text (Large)** ウィジェットをドラッグします。

[![ラージ テキスト ウィジェットを追加する](hello-android-quickstart-images/vs/04-large-text-sml.png)](hello-android-quickstart-images/vs/04-large-text.png#lightbox)

デザイン サーフェイスで **Text (Large)** コントロールを選択した状態で、次のように、**[プロパティ]** ウィンドウを使用して **Text (Large)** ウィジェットの `text` プロパティを `Enter a Phoneword:` に変更します。

[![ラージ テキスト プロパティを設定する](hello-android-quickstart-images/vs/05-enter-a-phoneword-sml.png)](hello-android-quickstart-images/vs/05-enter-a-phoneword.png#lightbox)

**Plain Text** ウィジェットを **[ツールボックス]** からデザイン サーフェイスにドラッグし、**Text (Large)** ウィジェットの下に配置します。

[![プレーン テキスト ウィジェットを追加する](hello-android-quickstart-images/vs/06-plain-text-sml.png)](hello-android-quickstart-images/vs/06-plain-text.png#lightbox)

デザイン サーフェイスで **Plain Text** ウィジェットを選択した状態で、次のように、**[プロパティ]** ウィンドウを使用して **Plain Text** ウィジェットの `id` プロパティを `@+id/PhoneNumberText` に変更し、`text` プロパティを `1-855-XAMARIN` に変更します。

[![プレーン テキスト プロパティを設定する](hello-android-quickstart-images/vs/07-add-properties-sml.png)](hello-android-quickstart-images/vs/07-add-properties.png#lightbox)

**Button** を **[ツールボックス]** からデザイン サーフェイスにドラッグし、**Plain Text** ウィジェットの下に配置します。

[![デザインに変換ボタンをドラッグする](hello-android-quickstart-images/vs/08-drag-button-sml.png)](hello-android-quickstart-images/vs/08-drag-button.png#lightbox)

デザイン サーフェイスで **[Button]** を選択した状態で、次のように、**[プロパティ]** ウィンドウを使用して **[Button]** の `id` プロパティを `@+id/TranslateButton` に変更し、`text` プロパティを `Translate` に変更します。

[![変換ボタン プロパティを設定する](hello-android-quickstart-images/vs/09-translate-button-sml.png)](hello-android-quickstart-images/vs/09-translate-button.png#lightbox)

**[TextView]** を **[ツールボックス]** からデザイン サーフェスにドラッグし、**[Button]** ウィジェットの下に配置します。 次のように、**[TextView]** の `id` プロパティを `@+id/TranslatedPhoneWord` に設定し、`text` を空の文字列に変更します。

[![テキスト ビューでプロパティを設定する](hello-android-quickstart-images/vs/10-textview-properties-sml.png)](hello-android-quickstart-images/vs/10-textview-properties.png#lightbox)    

**CTRL + S** キーを押して、作業内容を保存します。

### <a name="writing-translation-code"></a>変換コードの作成

次の手順では、電話番号を英数字から数字に変換するコードをいくつか追加します。 以下のように、**ソリューション エクスプローラー** ウィンドウの **Phoneword** プロジェクトを右クリックし、**[追加]、[新しい項目...]** の順に選択して、新しいファイルをプロジェクトに追加します。

[![新しい項目を追加する](hello-android-quickstart-images/vs/12-add-new-item-sml.png)](hello-android-quickstart-images/vs/12-add-new-item.png#lightbox)

**[新しい項目の追加]** ダイアログで、**[Visual C#]、[コード]** の順に選択し、新しいコード ファイルに **PhoneTranslator.cs** という名前を付けます。

[![PhoneTranslator.cs を追加する](hello-android-quickstart-images/vs/14-add-class-sml.png)](hello-android-quickstart-images/vs/14-add-class.png#lightbox)

これで、新しい空の C# クラスが作成されます。 このファイルに次のコードを挿入します。

```csharp
using System.Text;
using System;
namespace Core
{
    public static class PhonewordTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
                return "";
            else
                raw = raw.ToUpperInvariant();

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                        newNumber.Append(result);
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }
        static bool Contains (this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }
        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
                return 2;
            else if ("DEF".Contains(c))
                return 3;
            else if ("GHI".Contains(c))
                return 4;
            else if ("JKL".Contains(c))
                return 5;
            else if ("MNO".Contains(c))
                return 6;
            else if ("PQRS".Contains(c))
                return 7;
            else if ("TUV".Contains(c))
                return 8;
            else if ("WXYZ".Contains(c))
                return 9;
            return null;
        }
    }
}
```

**[ファイル]、[保存]** の順にクリックし (または **CTRL + S** キーを押し)、**PhoneTranslator.cs** ファイルへの変更内容を保存してから、ファイルを閉じます。

### <a name="wiring-up-the-interface"></a>インターフェイスの接続

次の手順では、`MainActivity` クラスにバッキング コードを挿入し、ユーザー インターフェイスを接続するためのコードを追加します。 まず、**Translate** ボタンを接続します。 `MainActivity` クラスで、`OnCreate` メソッドを見つけます。 次の手順では、`OnCreate` 内 (`base.OnCreate(bundle)` および `SetContentView
(Resource.Layout.Main)` 呼び出しの下) にボタン コードを追加します。 最初に、`OnCreate` メソッドが次のようになるようにテンプレート コードを変更します。

```csharp
using Android.App;
using Android.OS;
using Android.Widget;
using Core;

namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        protected override void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // New code will go here
        }
    }
}
```

Android Designer を使用してレイアウト ファイルで作成されたコントロールへの参照を取得します。 `OnCreate` メソッド内 (`SetContentView` 呼び出しの後) に次のコードを追加します。

```csharp
// Get our UI controls from the loaded layout
EditText phoneNumberText = FindViewById<EditText>(Resource.Id.PhoneNumberText);
TextView translatedPhoneWord = FindViewById<TextView>(Resource.Id.TranslatedPhoneWord);
Button translateButton = FindViewById<Button>(Resource.Id.TranslateButton);
```

ユーザーが **Translate** ボタンを押したときに応答するコードを追加します。
`OnCreate` メソッド (前の手順で追加した行の後) に次のコードを追加します。

```csharp
// Add code to translate number
translateButton.Click += (sender, e) =>
{
    // Translate user's alphanumeric phone number to numeric
    string translatedNumber = Core.PhonewordTranslator.ToNumber(phoneNumberText.Text);
    if (string.IsNullOrWhiteSpace(translatedNumber))
    {
        translatedPhoneWord.Text = string.Empty;
    }
    else
    {
        translatedPhoneWord.Text = translatedNumber;
    }
};
```

**[ファイル]、[すべて保存]** の順に選択して (または **CTRL + SHIFT + S** キーを押して) 作業内容を保存し、**[ビルド]、[ソリューションのリビルド]** の順に選択して (または **CTRL + SHIFT + B** キーを押して) アプリケーションをビルドします。 

エラーがある場合は、アプリケーションが正常にビルドされるまで、前の手順を実行し、誤りを修正します。 "_現在のコンテキストにリソースが存在しません_" などのビルド エラーが表示された場合は、**MainActivity.cs** の名前空間名とプロジェクト名 (`Phoneword`) が一致していることを確認してから、ソリューションを完全にリビルドします。 それでもビルド エラーが表示される場合は、最新の Xamarin.Android 更新プログラムをインストールしていることを確認します。

### <a name="setting-the-label-and-app-icon"></a>ラベルとアプリ アイコンの設定

これでアプリケーションは動作します。次は最後の仕上げを加えます。 **MainActivity.cs** で、`MainActivity` の `Label` を編集します。 `Label` は、Android の画面の上部に表示され、アプリケーションでの位置をユーザーに知らせます。
以下のように、`MainActivity` クラスの上部にある `Label` を `Phone Word` に変更します。

```csharp
namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        ...
    }
}
```

次は、アプリケーションのアイコンを設定します。 既定では、Visual Studio はプロジェクトの既定のアイコンを提供します。 ソリューションからこれらのファイルを削除して、別のアイコンに置き換えましょう。 **Solution Pad** の **[リソース]** フォルダーを展開します。 次のように、**mipmap-** のプレフィックスがついたフォルダーが 5 つあり、これらのフォルダーのそれぞれに **Icon.png** ファイルが 1 つ含まれています。

[![mipmap- フォルダーと Icon.png ファイル](hello-android-quickstart-images/vs/21-mipmap-folders-sml.png)](hello-android-quickstart-images/vs/21-mipmap-folders.png#lightbox)

これらの各アイコン ファイルをプロジェクトから削除する必要があります。 各 **Icon.png** ファイルを右クリックし、コンテキスト メニューから **[削除]** を選択します。
   
[![既定の Icon.png を削除する](hello-android-quickstart-images/vs/21-delete-icon-sml.png)](hello-android-quickstart-images/vs/21-delete-icon.png#lightbox)
   
ダイアログで **[削除]** ボタンをクリックします。

次に、[Xamarin App Icons セット](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)をダウンロードして解凍します。 この ZIP ファイルは、アプリケーションのアイコンを含んでいます。 各アイコンは見た目は同じですが、さまざまな解像度で、画面密度が異なるさまざまなデバイスに正しくレンダリングできます。  Xamarin.Android プロジェクトに、このファイルのセットをコピーする必要があります。 Visual Studio の**ソリューション エクスプローラー**で、**mipmap-hdpi** フォルダーを右クリックし、**[追加]、[既存の項目]** の順に選択します。

[![ファイルを追加する](hello-android-quickstart-images/vs/22-add-files-sml.png)](hello-android-quickstart-images/vs/22-add-files.png#lightbox)

選択ダイアログから、解凍した Xamarin AdApp Icons のディレクトリに移動し、**mipmap-hdpi** フォルダーを開きます。 **Icon.png** を選択して **[追加]** をクリックします。

**mipmap-** Xamarin App Icons フォルダーの内容が **Phoneword** プロジェクトの対応する **mipmap-** フォルダーにコピーされるまで、**mipmap-** フォルダーごとにこれらの手順を繰り返します。

すべてのアイコンを Xamarin.Android プロジェクトにコピーしたら、**Solution Pad** でプロジェクトを右クリックして、**[プロジェクト オプション]** ダイアログを開きます。 **[ビルド]、[Android アプリケーション]** の順に選択し、**[アプリケーション アイコン]** コンボ ボックスから **@mipmap/icon** を選択します。

[![プロジェクト アイコンを設定する](hello-android-quickstart-images/vs/25-set-project-icon-sml.png)](hello-android-quickstart-images/vs/25-set-project-icon.png#lightbox)

### <a name="running-the-app"></a>アプリの実行

最後に、Android デバイスまたはエミュレーターでこのアプリケーションを実行し、Phoneword を変換してアプリケーションをテストします。

[![完成時のアプリのスクリーンショット](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio for Mac](#tab/vsmac)

**Applications** フォルダーまたは**スポットライト**から Visual Studio for Mac を起動します。 

**[新しいソリューション...]** をクリックして新しいプロジェクトを作成します。

**[新しいプロジェクト用のテンプレートを選びます]** ダイアログで、**[Android]、[アプリ]** の順にクリックして、**[Android アプリ]** テンプレートを選択します。 **[次へ]** をクリックします。

[![Android アプリ テンプレートを選択する](hello-android-quickstart-images/xs/03-choose-template-sml.png)](hello-android-quickstart-images/xs/03-choose-template.png#lightbox)

**[Android アプリの構成]** ダイアログで、新しいアプリに `Phoneword` という名前を付けて **[次へ]** をクリックします。

[![Android アプリを構成する](hello-android-quickstart-images/xs/04-configure-android-app-sml.png)](hello-android-quickstart-images/xs/04-configure-android-app.png#lightbox)

**[Configure your new Android App]\(新しい Android アプリを構成します\)** ダイアログでは、ソリューションとプロジェクトの名前は `Phoneword` に設定したままにし、**[作成]** をクリックしてプロジェクトを作成します。

### <a name="creating-the-layout"></a>レイアウトの作成

新しいプロジェクトが作成されたら、**[ソリューション]** パッドで **Resources** フォルダーを展開してから **layout** フォルダーを展開します。
**Main.axml** をダブルクリックして、Android Designer で開きます。 Android Designer で表示されるときの画面のレイアウト ファイルを以下に示します。

[![Main.axml を開く](hello-android-quickstart-images/xs/05-open-layout-sml.png)](hello-android-quickstart-images/xs/05-open-layout.png#lightbox)

**[Hello World, Click Me!]**  **ボタン** (デザイン サーフェイスにあります) を選択し、**Delete** キーを押して削除します。 

**[ツールボックス]** (右側の領域) の検索フィールドに「`text`」と入力し、デザイン サーフェイス (中央の領域) に **Text (Large)** ウィジェットをドラッグします。

[![ラージ テキスト ウィジェットを追加する](hello-android-quickstart-images/xs/06-large-text-sml.png)](hello-android-quickstart-images/xs/06-large-text.png#lightbox)

デザイン サーフェイスで **Text (Large)** ウィジェットを選択した状態で、次のように、**[プロパティ]** パッドを使用して **Text (Large)** ウィジェットの `Text` プロパティを `Enter a Phoneword:` に変更することができます。

[![ラージ テキスト ウィジェットのプロパティを設定する](hello-android-quickstart-images/xs/07-enter-a-phoneword-sml.png)](hello-android-quickstart-images/xs/07-enter-a-phoneword.png#lightbox)

次に、**Plain Text** ウィジェットを **[ツールボックス]** からデザイン サーフェイスにドラッグし、**Text (Large)** ウィジェットの下に配置します。 次のように、検索フィールドを使用して、名前でウィジェットを見つけることができます。

[![プレーン テキスト ウィジェットを追加する](hello-android-quickstart-images/xs/08-plain-text-sml.png)](hello-android-quickstart-images/xs/08-plain-text.png#lightbox)

デザイン サーフェイスで **Plain Text** ウィジェットを選択した状態で、次のように、**[プロパティ]** パッドを使用して **Plain Text** ウィジェットの `Id` プロパティを `@+id/PhoneNumberText` に変更し、`Text` プロパティを `1-855-XAMARIN` に変更することができます。

[![プレーン テキスト ウィジェットのプロパティを設定する](hello-android-quickstart-images/xs/09-add-properties-sml.png)](hello-android-quickstart-images/xs/09-add-properties.png#lightbox)

**Button** を **[ツールボックス]** からデザイン サーフェイスにドラッグし、**Plain Text** ウィジェットの下に配置します。

[![ボタンを追加する](hello-android-quickstart-images/xs/10-drag-button-sml.png)](hello-android-quickstart-images/xs/10-drag-button.png#lightbox)

デザイン サーフェイスで **Button** を選択した状態で、次のように、**[プロパティ]** パッドを使用して **Button** の `Id` プロパティを `@+id/TranslateButton` に変更し、`Text` プロパティを `Translate` に変更できます。

[![変換ボタンとして構成する](hello-android-quickstart-images/xs/11-translate-button-sml.png)](hello-android-quickstart-images/xs/11-translate-button.png#lightbox)

**[TextView]** を **[ツールボックス]** からデザイン サーフェスにドラッグし、**[Button]** ウィジェットの下に配置します。 次のように、選択した **[TextView]** で、**[TextView]** の `id` プロパティを `@+id/TranslatedPhoneWord` に設定し、`text` を空の文字列に変更します。

[![テキスト ビューでプロパティを設定する](hello-android-quickstart-images/xs/12-textview-properties-sml.png)](hello-android-quickstart-images/xs/12-textview-properties.png#lightbox)    

**&#8984; + S** キーを押して、作業内容を保存します。

### <a name="writing-translation-code"></a>変換コードの作成

ここでは、電話番号を英数字から数字に変換するコードをいくつか追加します。 以下のように、**[ソリューション]** パッドの **Phoneword** プロジェクトの横にある歯車アイコンをクリックし、**[追加]、[新しいファイル...]** の順に選択して、新しいファイルをプロジェクトに追加します。

[![新しいファイルをプロジェクトに追加する](hello-android-quickstart-images/xs/14-add-new-file-sml.png)](hello-android-quickstart-images/xs/14-add-new-file.png#lightbox)

**[新しいファイル]** ダイアログで、**[全般]、[空のクラス]** の順に選択し、新しいファイルに **PhoneTranslator** という名前を付けて **[新規]** をクリックします。 これで、新しい空の C# クラスが作成されます。

新しいクラスのテンプレート コードをすべて削除し、次のコードに置き換えます。

```csharp
using System.Text;
using System;
namespace Core
{
    public static class PhonewordTranslator
    {
        public static string ToNumber(string raw)
        {
            if (string.IsNullOrWhiteSpace(raw))
                return "";
            else
                raw = raw.ToUpperInvariant();

            var newNumber = new StringBuilder();
            foreach (var c in raw)
            {
                if (" -0123456789".Contains(c))
                {
                    newNumber.Append(c);
                }
                else
                {
                    var result = TranslateToNumber(c);
                    if (result != null)
                        newNumber.Append(result);
                }
                // otherwise we've skipped a non-numeric char
            }
            return newNumber.ToString();
        }
        static bool Contains (this string keyString, char c)
        {
            return keyString.IndexOf(c) >= 0;
        }
        static int? TranslateToNumber(char c)
        {
            if ("ABC".Contains(c))
                return 2;
            else if ("DEF".Contains(c))
                return 3;
            else if ("GHI".Contains(c))
                return 4;
            else if ("JKL".Contains(c))
                return 5;
            else if ("MNO".Contains(c))
                return 6;
            else if ("PQRS".Contains(c))
                return 7;
            else if ("TUV".Contains(c))
                return 8;
            else if ("WXYZ".Contains(c))
                return 9;
            return null;
        }
    }
}
```

**[ファイル]、[保存]** の順に選択し (または **&#8984; + S** キーを押し)、**PhoneTranslator.cs** ファイルへの変更内容を保存してから、ファイルを閉じます。 ソリューションをリビルドして、コンパイル時エラーがないことを確認してください。

### <a name="wiring-up-the-interface"></a>インターフェイスの接続

次の手順では、`MainActivity` クラスにバッキング コードを追加し、ユーザー インターフェイスを接続するためのコードを追加します。
**Solution Pad** で **MainActivity.cs** をダブルクリックして開きます。

まず、**[変換]** ボタンにイベント ハンドラーを追加します。 `MainActivity` クラスで、`OnCreate` メソッドを見つけます。 `OnCreate` 内 (`base.OnCreate(bundle)` および `SetContentView (Resource.Layout.Main)` 呼び出しの下) にボタン コードを追加します。 `OnCreate` メソッドが次のようになるように、テンプレート ボタン処理コードを削除します。

```csharp
using Android.App;
using Android.OS;
using Android.Widget;
using Core;

namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        protected override void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Our code will go here
        }
    }
}
```

次は、Android Designer を使用してレイアウト ファイルで作成されたコントロールへの参照が必要になります。 `OnCreate` メソッド内 (`SetContentView` 呼び出しの後) に次のコードを追加します。

```csharp
// Get our UI controls from the loaded layout
EditText phoneNumberText = FindViewById<EditText>(Resource.Id.PhoneNumberText);
TextView translatedPhoneWord = FindViewById<TextView>(Resource.Id.TranslatedPhoneWord);
Button translateButton = FindViewById<Button>(Resource.Id.TranslateButton);
```

ユーザーが **Translate** ボタンを押したときに応答するコードを追加します。その場合、`OnCreate` メソッド (最後の手順で追加する行の後) に次のコードを追加します。

```csharp
// Add code to translate number
string translatedNumber = string.Empty;

translateButton.Click += (sender, e) =>
{
    // Translate user's alphanumeric phone number to numeric
    translatedNumber = PhonewordTranslator.ToNumber(phoneNumberText.Text);
    if (string.IsNullOrWhiteSpace(translatedNumber))
    {
        translatedPhoneWord.Text = string.Empty;
    }
    else
    {
        translatedPhoneWord.Text = translatedNumber;
    }
};
```

作業内容を保存し、**[ビルド]、[すべてビルド]** の順に選択して (または **&#8984; + B** キーを押して)、アプリケーションをビルドします。 アプリケーションがコンパイルされると、Visual Studio for Mac の上部に成功メッセージが表示されます。

エラーがある場合は、アプリケーションが正常にビルドされるまで、前の手順を実行し、誤りを修正します。 "_現在のコンテキストにリソースが存在しません_" などのビルド エラーが表示された場合は、**MainActivity.cs** の名前空間名とプロジェクト名 (`Phoneword`) が一致していることを確認してから、ソリューションを完全にリビルドします。 それでもビルド エラーが表示される場合は、最新の Xamarin.Android および Visual Studio for Mac の更新プログラムをインストールしていることを確認します。

### <a name="setting-the-label-and-app-icon"></a>ラベルとアプリ アイコンの設定

これでアプリケーションは動作します。次は最後の仕上げを加えます。 まず、`MainActivity` の `Label` を編集します。
`Label` は、Android の画面の上部に表示され、アプリケーションでの位置をユーザーに知らせます。 以下のように、`MainActivity` クラスの上部にある `Label` を `Phone Word` に変更します。

```csharp
namespace Phoneword
{
    [Activity (Label = "Phone Word", MainLauncher = true)]
    public class MainActivity : Activity
    {
        ...
    }
}
```

次は、アプリケーションのアイコンを設定します。 既定では、Visual Studio for Mac は、プロジェクトの既定のアイコンを提供します。 ソリューションからこれらのファイルを削除して、別のアイコンに置き換えましょう。 **Solution Pad** の **[リソース]** フォルダーを展開します。 次のように、**mipmap-** のプレフィックスがついたフォルダーが 5 つあり、これらのフォルダーのそれぞれに **Icon.png** ファイルが 1 つ含まれています。

[![mipmap- フォルダーと Icon.png ファイル](hello-android-quickstart-images/xs/23-mipmap-folders-sml.png)](hello-android-quickstart-images/xs/23-mipmap-folders.png#lightbox)

これらの各アイコン ファイルをプロジェクトから削除する必要があります。 各 **Icon.png** ファイルを右クリックし、コンテキスト メニューから **[削除]** を選択します。

[![既定の Icon.png を削除する](hello-android-quickstart-images/xs/23-delete-icon-sml.png)](hello-android-quickstart-images/xs/23-delete-icon.png#lightbox)

ダイアログで **[削除]** ボタンをクリックします。

次に、[Xamarin App Icons セット](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)をダウンロードして解凍します。 この ZIP ファイルは、アプリケーションのアイコンを含んでいます。 各アイコンは見た目は同じですが、さまざまな解像度で、画面密度が異なるさまざまなデバイスに正しくレンダリングできます。  Xamarin.Android プロジェクトに、このファイルのセットをコピーする必要があります。 Visual Studio for Mac の **Solution Pad** で、**mipmap-hdpi** フォルダーを右クリックし、**[追加]、[ファイルの追加]** の順に選択します。

[![ファイルを追加する](hello-android-quickstart-images/xs/24-add-files-sml.png)](hello-android-quickstart-images/xs/24-add-files.png#lightbox)

選択ダイアログから、解凍した Xamarin AdApp Icons のディレクトリに移動し、**mipmap-hdpi** フォルダーを開きます。 **Icon.png** を選択して **[開く]** をクリックします。

**[ファイルをフォルダーに追加する]** ダイアログ ボックスで、**[Copy the file into the directory]\(ファイルをディレクトリにコピーする\)** を選択して **[OK]** をクリックします。

[![[ファイルをディレクトリにコピーする] ダイアログ](hello-android-quickstart-images/xs/26-copy-to-directory-sml.png)](hello-android-quickstart-images/xs/26-copy-to-directory.png#lightbox)

**mipmap-** Xamarin App Icons フォルダーの内容が **Phoneword** プロジェクトの対応する **mipmap-** フォルダーにコピーされるまで、**mipmap-** フォルダーごとにこれらの手順を繰り返します。

すべてのアイコンを Xamarin.Android プロジェクトにコピーしたら、**Solution Pad** でプロジェクトを右クリックして、**[プロジェクト オプション]** ダイアログを開きます。 **[ビルド]、[Android アプリケーション]** の順に選択し、**[アプリケーション アイコン]** コンボ ボックスから **@mipmap/icon** を選択します。

[![プロジェクト アイコンを設定する](hello-android-quickstart-images/xs/28-set-project-icon-sml.png)](hello-android-quickstart-images/xs/28-set-project-icon.png#lightbox)

### <a name="running-the-app"></a>アプリの実行

最後に、Android デバイスまたはエミュレーターでこのアプリケーションを実行し、Phoneword を変換してアプリケーションをテストします。

[![完成時のアプリのスクリーンショット](hello-android-quickstart-images/intro-app-examples-sml.png)](hello-android-quickstart-images/intro-app-examples.png#lightbox)

-----

おつかれさまでした。これで最初の Xamarin.Android アプリケーションが完成しました。
次は、ここで習得したツールとスキルを細かく分析します。 「[Hello, Android Deep Dive」](~/android/get-started/hello-android/hello-android-deepdive.md) (Hello, Android の詳細) に進んでください。


## <a name="related-links"></a>関連リンク

- [Xamarin Android アプリ アイコン (ZIP)](https://github.com/xamarin/monodroid-samples/blob/master/Phoneword/Resources/XamarinAndroidIcons.zip?raw=true)
- [Phoneword (サンプル)](https://developer.xamarin.com/samples/monodroid/Phoneword)
