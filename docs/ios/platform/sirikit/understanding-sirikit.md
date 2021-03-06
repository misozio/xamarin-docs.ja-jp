---
title: SiriKit 概念を理解します。
description: この記事では、Xamarin.iOS アプリで SiriKit を操作するために必要となる重要な概念について説明します。
ms.prod: xamarin
ms.assetid: 99EC5C1E-484F-4371-8555-58C9F60DE37F
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/16/2017
ms.openlocfilehash: 7140747307c15b51fb330a41b496079dc680e5fa
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2018
---
# <a name="understanding-sirikit-concepts"></a>SiriKit 概念を理解します。

_この記事では、Xamarin.iOS アプリで SiriKit を操作するために必要となる重要な概念について説明します。_


新しい 10、iOS に SiriKit が iOS デバイスで Siri とマップのアプリを使用してユーザーがアクセスできるサービスを提供する Xamarin.iOS アプリを許可します。 この機能は、new を使用して 1 つまたは複数のアプリ拡張機能で提供**インテント**と**インテント UI**フレームワークです。

SiriKit により、アプリの拡張機能と、新しいを使用して iOS デバイスで Siri とマップのアプリを使用してユーザーがアクセスできるサービスを提供する iOS アプリ**インテント**と**インテント UI**フレームワークです。

Siri の動作の概念を**ドメイン**のグループが関連するタスクの操作を把握します。 Siri とされているアプリの各相互作用がとおりの既知のサービスのドメインのいずれかに分類する必要があります。

- オーディオまたはビデオ通話です。
- 素敵を予約します。
- ワークアウトを管理します。
- メッセージングです。
- 写真を検索しています。
- 送信または受信支払いを処理します。

ユーザーは、1 つのアプリ拡張機能のサービスに関連する Siri の要求を行う、SiriKit 送信、拡張機能、**インテント**サポート データと共に、ユーザーの要求を記述するオブジェクト。 アプリ拡張機能は、適切な生成**応答**オブジェクトを指定された**インテント**、拡張機能が、要求を処理する方法の詳細を示すです。

## <a name="the-intents-and-intents-ui-extensions"></a>意図的または意図的 UI 拡張機能

Siri とマップのアプリの両方は、2 つのさまざまな種類のアプリの拡張機能を使用して、アプリのサービスと対話します。

- **インテント拡張子**-Siri の提供しアプリのマップのコンテンツとは、サポートされている任意の目的を満たすために必要なタスクを実行します。
- **UI 拡張機能のインテント**-Siri またはマップのいずれかの中で、アプリのコンテンツの表示されるカスタム UI を提供します。

アプリが SiriKit をサポートするために意図的拡張機能を提供する必要があり、Siri およびマップは、ユーザーに提示できる情報を提供するため、およびを意図的に処理を行います。

Siri が通常すべてのユーザー操作を処理し、各サポートされているドメインで情報を表示するために、標準的な組み込み UI があるために、インテント UI 拡張機能の作成は省略できます。 インテント UI 拡張機能を提供する、アプリケーションで使用できる、**インテント UI**豊富なカスタム ユーザー インターフェイスを機能させると、アプリのブランド化を提供するフレームワークと追加情報。

## <a name="siri-and-the-maps-app-role"></a>Siri と、マップのアプリケーション ロール

ユーザーの音声の要求は、言語に処理され、目的とした拡張機能を処理できる実用的なインテントにそれらの要求を変換する Siri によって分析意味です。

マップでは、アプリの目的とした拡張機能を使用して、ユーザーの操作への応答内にあるマップ インターフェイスで情報を表示します。 最寄りのレストランを要求したり、取得など、アプリのレストランを確認します。

Siri とマップの両方のすべてのユーザーの操作を管理し、標準的なシステム インターフェイスを使用して結果を表示します。 アプリ拡張機能の役割は、表示されるデータを提供する、主にです。 必要に応じて、アプリはインテント UI 拡張機能を提供し、既定のシステム インターフェイスを強化するためにカスタム UI を表示できます。

## <a name="interacting-with-siri-via-sirikit"></a>SiriKit を介して Siri と対話します。

このセクションで Siri を使用するアプリと対話するユーザーを SiriKit ができるようにする方法の概要が表示されます。 この例で使用する、偽の MonkeyChat アプリ。

[![](understanding-sirikit-images/monkeychat01.png "MonkeyChat アイコン")](understanding-sirikit-images/monkeychat01.png#lightbox)

MonkeyChat がユーザーの友人の連絡先独自書籍を維持、それぞれ (Bobo など) のような画面名に関連付けられているユーザーの画面名が各友人にテキスト チャットを送信することができます。

方法は多数あります別のユーザーは、さまざまな形式で同じ要求を行うことがありますので、ユーザーに、アプリとのやり取りを開始可能性があります。

たとえば、ユーザーは、友人の Bobo にメッセージを送信する場合に、Siri と次のメッセージ交換がある可能性があります。

_ユーザー: Hey Siri、MonkeyChat メッセージを送信します。_<br />
_Siri: にだれか。_<br />
_ユーザー: Bobo です。_<br />
_Siri: 実行 Bobo にたいですか。_<br />
_ユーザーの場合は、複数バナナを送信してください。_<br />

別のユーザーには、別のメッセージ交換で同じ要求を行うことがあります。

_: ユーザーは、MonkeyChat で Bobo にメッセージを送信します。_<br />
_Siri: 実行 Bobo にたいですか。_<br />
_ユーザーの場合は、複数バナナを送信してください。_<br />

他のユーザーは、さらに短い要求を行う可能性があります。

_ユーザー: MonkeyChat Bobo に複数のバナナを送信してください。_<br />
_Siri: Ok、メッセージを送信する送信してください複数バナナ Monkeychat で Bobo。_<br />

または、別の言語でも同じ要求を行います。

_ユーザー: MonkeyChat Bobo s'il vous plaît envoyer plus de bananes です。_<br />
_Siri: Oui、envoi メッセージ s'il vous plaît envoyer plus de bananes à Bobo sur Monkeychat です。_<br />

まだ他のユーザーは、メッセージ交換でかなり詳細可能性があります。

_ユーザー: Hey Siri、できますくださいしないで me、優先と MonkeyChat のアプリケーションの送信を開始、メッセージ テキストが複数バナナを送信してください。_<br />
_Siri: にだれか。_<br />
_ユーザー: 最適な pal Bobo です。_<br />

さらに、方法は多数あります Siri がいくつかの要求が行われた方法に基づいて、要求に応答可能性があります。

- **ホーム ボタンを押し続けて**-Siri がさらに visual 応答の限られた口頭でフィードバックを提供します。
- **"Hey Siri"によって**-Siri 音声よりされ少ない visual 応答を実現します。

Siri はユーザーのユーザー補助機能のニーズを満たすとは対話し、それらのニーズに基づいた応答にも調整します。

要求が行われる方法または Siri が要求に応答する方法に関係なく Siri がユーザーにメッセージ交換を処理し、(その拡張機能) を使用してアプリ機能を提供します。

ユーザーが siri 口頭での要求を行ったとき、Siri が従うステップを次に示します。

[![](understanding-sirikit-images/monkeychat02.png "Siri が以下の手順")](understanding-sirikit-images/monkeychat02.png#lightbox)

1. Siri が最初に、ユーザーのオーディオを受け取る**音声**テキストに変換します。
2. 次に、テキストに変換、**インテント**ユーザーの要求の表現を構造化します。
3. 目的に基づき、Siri かかります**アクション**ユーザーの要求を実行します。
4. Siri が最後に、表示は**応答**(ビジュアルと音声の両方) を実行する操作に基づくユーザー。

次の 3 つメインする方法は、アプリを Siri でユーザーのメッセージ交換で行うことができます。

[![](understanding-sirikit-images/monkeychat03.png "Siri とユーザーのメッセージ交換で、アプリが参加する 3 つの主な方法")](understanding-sirikit-images/monkeychat03.png#lightbox)

1. **ボキャブラリ**-これは、どのアプリに通知 Siri という語とのやり取りを認識している必要があります。
2. **アプリケーション ロジック**- これらは、アクションと、アプリを実行する応答が特定の意図的に基づきます。
3. **ユーザー インターフェイス**-これは、アプリでの応答を与えることができる省略可能なカスタム ユーザー インターフェイス。

### <a name="example"></a>例

上記の情報を指定するには、次のメッセージ交換は MonkeyChat アプリと対話する方法を調べます。

_ユーザー: Hey Siri、MonkeyChat で Bobo にメッセージを送信します。_<br />
_Siri: 実行 Bobo にたいですか。_<br />
_ユーザーの場合は、複数バナナを送信してください。_<br />

アプリは、メッセージ交換の最初のロールは、Siri がユーザーの音声を理解するためです。

[![](understanding-sirikit-images/monkeychat04.png "ユーザーの音声を理解 Siri の支援")](understanding-sirikit-images/monkeychat04.png#lightbox)

Siri、そのデータベースに名前"Bobo"はありませんが、アプリしが語彙を介して Siri でこの情報を共有します。 アプリにも役立ちます Siri はあると認識 Bobo、受信者として Siri に指定したので、*連絡先*です。

Siri の詳細が、すばやくをチェックして、メッセージがコンテンツが必要かどうかを表示するアプリの拡張機能のために受信者だけよりもメッセージを送信する必要であると認識します。 Siri が質問を持つユーザーに応答する MonkeyChat のため、: *「実行 Bobo にたいですか?」*

上記の例では、ユーザーが応答した、 *「複数バナナを送信してください」*、構造化されたに組み込みます Siri が**インテント**:

[![](understanding-sirikit-images/monkeychat05.png "Siri を使用して、ユーザーの応答を構造化のインテントにバンドルされます。")](understanding-sirikit-images/monkeychat05.png#lightbox)

構造化のインテント、次の情報が含まれます。

- **[ドメイン]:**メッセージ
- **目的:** sendMessage
- **受信者:** Bobo
- **コンテンツ:**複数バナナを送信してください

セットとして各ドメインは、次のトピック*アクション*目的で一対多のパラメーターが含まれる可能性がゼロをその中で実行してドメインとアクションに基づいて、アプリに送信されます。

目的に送信されますのアプリの拡張機能の処理します。 その結果の意図を処理するには、アプリが生成されます、 **IntentResponse**でした目的でのアプリのアプリを記述するパラメーターを含めることを目的でまとめられます。

各 IntentResponse も含まれる、**応答コード**Siri に指示するかどうか、アプリにできましたか、要求を完了します。 一部のドメインには、非常に具体的なエラー応答コードも送信されることができますがあります。

最後に、IntentResponse にが含まれます、 `NSUserActivity` (手の形をサポートするために使用されるものなど)。 `NSUserActivity`応答 Siri 環境のままにし、完了するためにアプリを入力する必要な場合に、アプリを起動するために使用されます。 

Siri が自動的に適切なビルド`NSUserActivity`アプリを起動してピックアップ Siri 環境内のユーザーの中断場所にします。 ただし、アプリケーションを用意できます独自`NSUserActivity`カスタムについては、必要な場合です。

アプリは、目的が処理され、Siri への応答が返されますが後を提示結果をユーザーに (口頭でおよび視覚的に)。

[![](understanding-sirikit-images/monkeychat06.png "口頭と視覚的に、ユーザーに表示結果")](understanding-sirikit-images/monkeychat06.png#lightbox)

Siri のアプリに使用可能なドメインのそれぞれのいくつかの組み込み応答ユーザー インターフェイスがあります。 ただし、ため MonkeyChat が任意の目的とした UI 拡張機能を指定すると、上記の例では、ユーザーに、メッセージ交換の結果を表示する使用されます。

## <a name="the-intent-lifecycle"></a>インテントのライフ サイクル

アプリ拡張機能が意図的に処理するときに実行する必要がある 3 つの主なタスクがあります。

[![](understanding-sirikit-images/monkeychat07.png "インテントのライフ サイクル")](understanding-sirikit-images/monkeychat07.png#lightbox)

1. アプリにする必要があります**解決**イベント上のすべてのパラメーターです。 結果として、アプリでが呼び出す解決複数回 (1 回、各パラメーター) とも複数回、同じパラメーター アプリとユーザー要求されている内容に同意するまでです。
2. アプリにする必要があります**確認**ことは、要求の目的を処理し、Siri を予想される結果に知らせることできます。
3. 最後に、アプリが必要があります**処理**目的とした、要求された結果を実現するために、手順を実行します。

### <a name="the-resolve-stage"></a>解決ステージ

解決ステージでは、Siri の値をユーザーが指定により、ユーザーが実際に意図したものが、目的としたが、アプリによって処理されるときに発生する問題を理解することができます。 

この段階では、アプリケーションがユーザーにメッセージ交換中に Siri の動作に影響を与える機会も提供します。 アプリは、これを行う、**解決応答**です。 Siri を理解しているデータのさまざまな種類に定義済みの応答の数があります。

アプリからの応答を解像度がありますが、最も一般的な**成功**、特定のデータ (ユーザー表示名) などのパラメーターから一致するを知っている情報の一部をアプリを意味します。

アプリが特定の要求が適切なを知っている情報と一致していることを確認する必要がある場合があります。 このような場合は、送信、 **ConfirmationRequired**質問はいまたは no をユーザーになどへの応答*「送信メッセージ Bobo に優れた?」*

それ以外の場合に、アプリが必要である、オプションの短い一覧から選択するユーザーである可能性があります。 この場合、アプリは、**あいまいさを排除**などから選択するユーザーの 2 ~ 10 のオプションの一覧を含む応答。 

```csharp
Who do you want to message?

* Bobo the Great
* Bobo Jr.
* Little Bobo
```

Siri が口頭または Siri UI を使用した対話することで、選択を行うユーザーを処理して、結果をアプリに送信されます。

それ以外の場合、パラメーターを解決するのには、アプリのための十分な情報がなくてもまたはあいまいさを排除 (Bobo で 80 のユーザーの名前で) などを使用して解決するのには多数の一致結果である可能性があります。 この場合、アプリは、送信、 **NeedsMoreDetails**応答および Siri がもっと詳しく指定するユーザーを求められます。

送信できる場合は、ユーザーには、目的のプロセスに、ために必要となる値が提供されていなかったため、 **NeedsValue** Siri 値のユーザーに、要求に応答します。

送信できるアプリがユーザーが特定のパラメーターを指定する値をサポートしていない場合、 **UnsupportedWithReason**応答値はサポートされていない理由理由を指定します。 Siri は完全に新しい値のユーザーの入力を求めるとに指定した理由が必要です。

最後に使用して、**へ**Siri、アプリが特定のパラメーターに値を必要としないことを通知に応答します。 ユーザーは、1 つか場合、Siri で単に無視されます。

### <a name="the-confirm-stage"></a>確認ステージ

確認段階では、2 つの目的があります。

- Siri Siri をユーザーに伝えることが何が行われるように、目的の処理の予期される結果を指定します。
- 営業案件チェックに要求された支払いを行うことで十分な資金を持つなど、ユーザーによって提示される要求を完了する必要があります、アプリの必要な状態を提供します。

アプリの提供、**目的とした応答**確認ステップから Siri が通信できるように効果的にユーザーを使用して、多くの情報、アプリがある使用可能なにつれてを設定する必要があります。

ドメインとアクションの種類に基づき、Siri 要求があります、確認のため、ユーザーなど、支払いの送信、または素敵を予約する前に。

### <a name="the-handle-stage"></a>ハンドル ステージ

処理ステージを行うには要求されているタスクを実行することによって、アプリがユーザーの要求を満たす、ポイントになっているために、目的の操作の最も重要な部分です。

確認の段階と同じようにアプリを Siri はこれをユーザーに関連付けることができるように、可能な結果についてできるだけ多くの情報を提供する必要があります。 この情報を視覚的に表示される場合があります。 またはユーザーに送り返す話す Siri もは単純にします。 

ライブの人が (注文の出荷を完了し、またはユーザーの所在地を車を推進) などの要求を処理する必要がある場合、アプリがネットワークの呼び出しの遅延など、特定の要求の処理に余分な時間を必要とする場合または時間がかかることがあります。 Siri がアプリからの応答を待機している場合、アプリが要求を処理を指示するユーザーを待機している UI が表示されます。

理想的には、アプリは提供 Siri への応答は 2 ~ 3 秒以内多くてします。 送信する必要がある場合は、アプリは、指定された応答がプロセスに時間がかかるしようとしていることを知っていれば、 **InProgress** Siri への応答コード。 Siri は、ユーザーに通知し、アプリがバック グラウンドで要求を処理と、これを行うに Siri 環境を離れる場合でも続行されます。

## <a name="adding-sirikit-to-the-app"></a>SiriKit アプリに追加

Ios 10 SiriKit、Apple は 2 つの新しい拡張ポイントを作成しました。

- **インテント拡張子**- アプリのコンテンツを Siri を提供し、サポートされている任意の目的を満たすために必要なタスクを実行します。
- **UI 拡張機能のインテント**-Siri の内部でアプリのコンテンツの表示されるカスタム UI を提供します。 

単語や語句の形式で認識されるように支援するために Siri を提供する API です。

- **アプリのボキャブラリ**-単語や語句、アプリのすべてのユーザーに共通です。
- **ユーザーのボキャブラリ**-単語や語句は指定したアプリのユーザーに固有です。

## <a name="the-intents-extension"></a>目的の拡張機能

インテント拡張機能は、アプリと Siri 間の主な相互作用を次のように処理を担当します。

[![](understanding-sirikit-images/intents01.png "目的の拡張機能")](understanding-sirikit-images/intents01.png#lightbox)

目的とした拡張機能は、1 つまたは複数のインテントをサポートできますが、アプリで SiriKit を実装する方法を決定する開発者をします。 開発者は、処理する必要がある各目的の別個の目的とした拡張機能を追加する可能性がありますもできます。  ただし、Apple 要求 Siri が複数のプロセスを処理する複数のメモリと時間を必要とする、アプリで開く必要があるないように、開発者が目的とした拡張機能の数を制限します。

開発者も目的とした拡張機能が実行されるバック グラウンドで Siri がアクティブなときに対応する場合があります。 これにより、要求に関する情報を処理する拡張機能とまだ通信中にユーザーを使用してメッセージ交換でアクティブに実行するために Siri できます。

## <a name="privacy-and-security-considerations"></a>プライバシーとセキュリティの考慮事項

Apple では、ことを確認するユーザーについてセキュリティで保護された Siri を使用する場合は、ユーザーが iOS デバイス ログオンする必要があるいくつかの処理があるような場合は、プライベートなメジャーを取得しました。 たとえば、素敵を要求するときに、支払いを行うか。

さらに、特定の動作をアプリをデバイスにログインしているユーザーを制限する必要があります。 このような場合は、アプリが要求できる、**を制限するときにロックされている**動作します。 これは、設定を使用して、`Info.plist`ファイル。

ローカル認証フレームワークは目的とした拡張で使用できるように、アプリは、追加の認証については、ユーザーを要請することができます、デバイスは、既にロックされている場合でもです。

最後に、Apple Pay は目的とした拡張機能の使用可能なため、アプリは Apple Pay を使用してトランザクションを完了できるし、組み込みの Apple Pay シートが Siri インターフェイス上に表示されます。

Apple がサード パーティのアプリと情報など、ユーザーが送信されているときにユーザーが知っていることを確認するさらに、**必要があります**(アプリのバンドルの表示名で指定) と同じアプリの特定の名前を言うと、要求を行います。

Apple には、ユーザーを使用して、このため、自然、流体の会話の遂行に Siri が設計されていますに合わせて自然にユーザーの要求の場所に、多くの品詞で、アプリのバンドルの名前を使用できます。

ユーザーを実行する一般的な操作の 1 つを"verbify"アプリの名前、つまり、アプリ名を取得し、要求内の動詞として使用します。 たとえば、 *"MonkeyChat Bobo 優れたバナナこれらは、でした"。*

## <a name="the-intents-ui-extension"></a>インテント UI 拡張機能

インテント UI 拡張機能では、アプリの UI と Siri エクスペリエンスにブランド化する機会が表示され、アプリに接続されていると思われるユーザーにすること。 この拡張機能では、アプリは、ブランドだけでなく、トラン スクリプトにビジュアルと他の情報を表示できます。

[![](understanding-sirikit-images/intents02.png "UI 拡張機能の目的の出力の例")](understanding-sirikit-images/intents02.png#lightbox)

インテント UI 拡張機能は常に返します、`UIViewController`できますビュー コント ローラーが初回の応答を超える追加の情報を示すなどの内部で何も、アプリを追加したりできます。 インテント UI では、作業がどの程度場合がその場所まで自動車を共有素敵など、長時間実行されるイベントの状態でも、ユーザーを更新できます。

インテント UI 拡張機能が常にする、アプリのアイコンと、UI の上部にある名などの他の Siri 内容と共に表示または、目的に基づいて、(送信やキャンセル) などのボタンが下部に表示されます。

アプリが Siri メッセージングなどの既定では、ユーザーに表示するか、アプリがアプリに合わせて調整いずれかの既定のエクスペリエンスを置き換えることができます場所にマップされる情報を置き換えることができます、いくつかのインスタンスが生じます。

> [!IMPORTANT]
> などの対話型要素を追加することができますが`UIButtons`または`UITextFields`を目的とした UI 拡張機能の`UIViewController`非対話型の目的とした UI と禁じこれら、およびユーザーでは、対話機能を使用できません。

アプリが Siri にインテント種類ごとに UI の既定のセットが含まれているので、目的とした UI 拡張機能を提供するため完全に省略可能です。 さらに、インターフェイスの目的の UI は、のみ使用可能な特定のインテント Apple と判断したことがユーザーに役に立ちます。

## <a name="adding-sirikit-vocabulary"></a>SiriKit ボキャブラリを追加します。

SiriKit の実装の最後の部分は、必要なボキャブラリを提供することによって、アプリ内にあります。 多くのアプリには、情報をユーザーとアプリへの情報をユーザーが提供される独自の方法を説明するための一意な方法があります。

このため、Siri には、単語や語句をアプリに一意の理解にアプリのサポートが必要です。 アプリの一部は、すべてのユーザーが理解に理解できるようにこれらのフレーズの一部になります。 まだ他のユーザーが一意になるアプリケーションの特定のユーザーにします。

### <a name="app-specific-vocabulary"></a>アプリ固有の用語

アプリ固有のボキャブラリは、すべての車両のタイプまたはトレーニング名などのアプリのユーザーに、特定の単語と語句を認識するを定義します。 定義されているこれらは、アプリケーションの一部であるため、`AppIntentVocabulary.plist`メインのアプリ バンドルの一部としてファイル。 さらに、これらの単語や語句をローカライズする必要があります。

ボキャブラリをいくつかの部分もある`AppIntentVocabulary.plist`ファイル。

- **アプリのコード例**-これらは、一般的なユース ケースのセット要求に対して、ユーザーがアプリのすることができます。 例: *「で始める試してみて MonkeyFit」。*
- **パラメーター** -これらをアプリに特定の標準以外のパラメーター型のセットを提供します。 たとえば、トレーニング名前 MonkeyFit アプリ用です。 構成されます。
    - **語句**-アプリのアプリの一意の用語の定義を許可します。 例: MonkeyFit アプリの"Bananarific"トレーニング型です。 
    - **発音**-特定のフレーズの単純な発音スペルとして Siri へ発音のヒントを提供します。 たとえば、"ba nana ri fic"です。
    - **例**-アプリで特定のフレーズを使用する例を示します。 たとえば、 *"MonkeyFit で、Bananarific の開始"*です。

詳細については、Apple を参照してください[アプリ ボキャブラリ ファイル形式のリファレンス](https://developer.apple.com/library/prerelease/content/documentation/Intents/Conceptual/SiriIntegrationGuide/CustomVocabularyKeys.html#//apple_ref/doc/uid/TP40016875-CH10-SW1)です。

### <a name="user-specific-vocabulary"></a>ユーザー固有の用語

ボキャブラリを特定のユーザーがアプリの個々 のユーザーに固有の語句を提供しようとしています。 これらは、実行時にメインのアプリ (アプリ拡張機能) から、一覧の先頭に最も重要な条件を持つ、ユーザーの最も重要な使用の優先度に並べ替え用語の順序付きセットとして提供されます。

上に示した MonkeyChat アプリの使用例を見てください。 MonkeyChat は、すべてがユーザーの特定のボキャブラリを使用して Siri を送信するユーザーの連絡先のリストを保持します。 ユーザー メッセージの数が 10 の最新の連絡先の一覧も保持し、各ユーザーのお気に入りの連絡先のセットを持ちます。 この例では、お気に入りの連絡先する必要があります、ユーザー固有ボキャブラリ、最近使用した連絡先続けての開始時、ユーザーの連絡先の残りの部分です。

次の種類の情報は、ユーザーの特定ボキャブラリによってサポートされます。

- 連絡先の名前。
- トレーニングの名前です。
- フォト アルバムの名前です。
- 写真のキーワードです。

アプリは iOS アドレス帳に依存する場合、アプリはこの情報は既に Siri を使用できるよう、操作を行うありません。 のみ、アプリは、アプリ独自の連絡先の一意のデータベースがある場合は、連絡先の名前を提供する必要があります。

ボキャブラリを設計するときにのみ、ユーザーが把握し、気にするために必要な値を提供します。 電話番号や電子メール アドレスなどの情報を提供しないようにします。

アプリは、ユーザー固有のボキャブラリが変更されたときに Siri を迅速に更新する必要があります。 ユーザーが情報を要求するに慣れるため Siri、iOS デバイスに追加された時点からです。 たとえば、ユーザーは、アプリで新しい連絡先を追加する場合は、その情報を送信 Siri をユーザーがそれを保存するとすぐに。

アプリではさらに、_必要があります_Siri がまだ正しく認識時間または日後の情報を削除する場合、ユーザーが混乱になる可能性がありますのでに Siri のボキャブラリから情報をすぐに削除します。

> [!IMPORTANT]
> アプリ必要がありますからすべての削除、ユーザーの特定のボキャブラリ Siri、アプリのリセットをユーザーが選択した場合、または、ログアウトします。

## <a name="sirikit-permissions"></a>SiriKit アクセス許可

SiriKit の最後の部分を中心としたアクセス許可。 IOS (写真、カメラまたは連絡先) などの他の機能を使用すると同じようにユーザーは Siri と対話するアプリケーションの明示的な権限を付与する必要があります。

アプリは Siri に提供され、ユーザーがこのアクセス権を付与する理由に関するに伝えるためにどのような情報を定義する文字列を指定することです。 

Apple では、アプリは iOS 10 に、アップグレードした後、ユーザーがアプリを開いた Siri 最初の時刻を使用するユーザーからのアクセス許可を要求する必要がありますを提案します。 これは、ユーザーが Siri 統合は次のトピックし、最初の要求を加える前に、事前に許可された使用状況をできるようにします。

## <a name="sirikit-and-maps"></a>SiriKit とマップ

SiriKit が iOS の不可欠な部分と iOS 10 に追加される大規模なインテント フレームワークを利用します。 目的のフレームワークは、システムの他の部分と一般的なと共有アクションとインテントを共有するよう設計されました。

インテント フレームワークでは、Siri 統合だけを超えるし、連絡先の統合をアプリになる既定テレフォニーまたは特定の連絡先のメッセージング アプリケーションなどの機能を提供します。 意図的では、最高の VOIP エクスペリエンスをユーザーに提供 CallKit との緊密な統合も提供します。

IOS 10 にマップ アプリケーションには、飛行共有、ユーザーが Maps UI 内で直接素敵を予約できるなどの機能が追加されます。 飛行共有 (およびその他の) インテントは Siri とマップ間で共有できるように、SiriKit はマップに関する一般的な拡張ポイントを提供します。 

つまり場合は、アプリは SiriKit 拡張機能を採用してもを受け取ることが、マップの統合は無料です。 

## <a name="designing-a-great-siri-experience"></a>優れた Siri エクスペリエンスの設計

Siri にアプリを統合するときに、優れたユーザー エクスペリエンスの設計は、優れたアプリケーション ユーザー インターフェイスの設計とは異なるです。 直接アプリのユーザーが対話して、正常な状態とは異なりときのビジュアル インターフェイスが表示されていないすべての何度も、画面で、ある Siri を使用する場合は使用します。 たとえば、ユーザーが開始された時点でメッセージ交換*"Hey Siri"*です。

### <a name="how-siri-helps-the-developer"></a>Siri が、開発者がどう役立つか

アプリを構築することでアプリの対話 Siri を設計する際、*通信インターフェイス*コンテキストの意味は、アプリの代わりにユーザーに Siri のあるメッセージ交換から派生します。

視覚的な参照がない場合、ユーザー必要がありますの追跡の先頭に表示される情報。 このため、Siri 情報を提示してベア最小タスクを実現するために必要なユーザーを実行しようとします。

会話のインターフェイスが質問と回答して、メッセージ交換時に、ユーザーと Siri の両方から形です。 ようにすることが重要 Siri の質問し、このインターフェイスを設計するときの応答を考慮します。

Siri が、質問に応答メッセージを作成するユーザーの次の例を実行*「に送信する準備完了しますか?」*. ユーザーがなどのさまざまな方法で応答でした*「送信」*、 *「キャンセル」*ものも含め完全にこの質問に関連付けられていないか。 メッセージ交換の再生方法に関係なく Siri は、アプリの処理し、送信関連情報が利用可能になった。

ユーザーが Siri とのメッセージ交換を開始がいくつかの方法があります。

- デバイスを選択することによって、[ホーム] ボタンを押すとします。 このような状況より多くのビジュアル インターフェイスと小さい口頭での応答に Siri が紹介します。
- 述べて*"Hey Siri"*および自在メッセージ交換を開始します。 このような状況では、Siri は小さい visual およびより音声になります。
- Bluetooth などのユーザー補助機能を使用するには、特別なニーズを持つユーザーの UI をカスタマイズ、聴覚補助が有効になります。
- ユーザーが、注意を保持する必要がある自動車の再生を使用してによって、混乱を最小限に抑えるに保持することによって推進することに重点を置きます。

### <a name="how-the-developer-helps-siri"></a>開発者が Siri を利用する方法

Siri とアプリの統合に、開発者は多くの場合、この統合をテストし、それらが作業を進めている多くの異なる要求、できるだけ多くのさまざまな方法で情報やタスクの同じ部分を要求したことを確認する必要があります。

2 つには、待ち時間も人ありません、ため、開発者を取得する多くの異なるベータ テストを最適に調整のために、できるだけ Siri 統合が重要です。 ユーザーが情報を求められる場合がありますまたは作成要求の方法で、開発者ことはありませんがの微調整に役立ちます Siri で自社のアプリを使用して、優れたエクスペリエンスをユーザーの最も広範なグループがあることを確認してください。

状況によって異なる場合、環境でテストします。 すべてのこれらのメッセージ交換が流動性を維持することを確認することで自然な方法で Siri とメッセージ交換を開始します。 ここでユーザーより多くの場合を使用する場合、アプリのようにいっぱいになったジムでの場所でテストします。

アプリ、提供しているすべての情報を Siri が正しく、ユーザーに要求および結果を表す必要があることを確認します。 これは、手の空き状況で Siri を使用する場合に特に当てはまります。

### <a name="siri-design-guidelines"></a>Siri のデザイン ガイドライン

Siri がユーザーとのメッセージ交換をアプリの代理であることを忘れないでください。 開発者がこのメッセージ交換がまだよくわからないよう流動性およびできるだけ自然です。

任意の重要なメッセージ交換では、開発者は、次のことを確認する必要があります。

- アプリが、メッセージ交換用に準備します。
- アプリは、正確にどのようなユーザーをリッスンするは、実行しようとします。
- アプリは、適切なタイミングで適切な質問を確認します。
- アプリが応答すること、ユーザーが求めている情報を要求します。

#### <a name="preparing-for-the-conversation"></a>メッセージ交換の準備をしています

最初に保存することは、開発者とまったく同じであるアプリケーションのユーザーがいないことです。 別の背景からさまざまな言語またはアプリを操作するときに、特別なニーズを持つくる可能性があります。

さらに、開発者を設計して、アプリをビルド、ので、深さ、詳しい知識を持っての両方のアプリとその内部動作および関数の一般的なユーザーはありません。 したがって、開発者可能性がありますに問い合わせてください Siri の要求は通常のユーザーとは異なる。

Siri を使用するアプリとのやり取りをできるだけ多くの異なるユーザーが必要であるためにです。 ユーザーは、または開発者を考慮していない方法では、開発者が思い Siri を使用してアプリの要求を行うことがあります。

#### <a name="ensure-the-app-is-a-good-listener"></a>アプリが適切なリスナーであることを確認します。

開発者は、アプリが適切なリスナーは、ユーザーの期待を満たすメッセージ交換の具体的な情報を取得することを確認する必要があります。 ことが可能性がありますが指定されていないすべての情報が要求されたタスクを実現するために、アプリが必要であることもできます。

これには、アプリがこの状況を処理できなかったいくつかの方法があります。

- **欠損値の適切な既定の選択**共有アプリ素敵が既定値として、ユーザーの現在の場所から取得されるたいと考えているを指定している場合などです。
- **論理的な推測を行う**-アプリがユーザーに収集される具体的な情報を使用して、アプリがありますとユーザーの連絡先情報から不足している携帯電話番号の入力など、不足している情報を推測することです。 ただし、慎重を最も高価なオプションなどの選択など、不適切な予想外の問題を回避します。
- **詳細情報の入力を求める**-アプリは、欠損値のユーザー入力を求める Siri を持つことができます。 ただし、キーをここではしながら、メッセージ交換単純なをポイントします。 ユーザーは、その要求を実現するためにいくつかの質問に回答がある場合は、まごついたり簡単になります。
- **適切に誤った情報処理**-ユーザーは、アプリが予期されていないか、または指定されたコンテキストで処理できない値を指定可能性があります。 アプリが使用クリアとを修正するように簡単な方法でユーザーにこのような状況に関連していることを確認します。

問題が 1 つの値では、アプリが表示されたら、これに対処することをお勧めの確認を求め Siri があるを開始します。 たとえば、 *"'sizeof...' Bobo 優れた?"*、はいまたは no 答えを簡単に応答できるようにします。

いくつかの可能な選択肢を 1 つの値の正しいできた場合がある場合は、あいまいさを排除、推奨される処理方法です。 このような状況で Siri に 10 個までの使用可能なオプションから選択するとユーザーを要求できます。 例えば:

```csharp
Who do you want to send the message to?

* Bobo the Great!
* Bobo Jr.
* Little Bobo
```

質問の指定された値に固有のまったく新しい応答を提供するように求める Siri があります。

#### <a name="request-final-confirmation"></a>最終確認を要求します。

アプリ実際には、タスクを実行して、ユーザーの要求を満たすため、前に Siri をチェックして、アプリ拡張機能の準備が整ったことを確認します。 たとえば、ユーザーは十分な資金自身のアカウントに、要求されたか。

さらに、アプリは、ことを提供するすべての可能な情報 Siri をユーザーに表示および実行されるタスクが、期待を満たしていることを確認できるようにすることを確認する必要があります。

要求と、アプリにユーザーが確認されたらを実行して、アプリの必要性をもう一度確認を提供して、結果をすべて Siri に戻すため、ユーザーに関連付けることができます。

#### <a name="responding-to-the-request"></a>要求に応答

Siri は、それぞれのドメインと認識されるアクションのいくつかの組み込みのユーザー インターフェイスをいます。 ただし、必要に応じて、アプリは、アプリのブランド化し、UI または要求に存在していたより多くの情報を提示することにより、ユーザー エクスペリエンスを強化するには、カスタムの目的 UI 拡張機能を提供できます。

ただし、Siri のカスタム インターフェイスを設計するとき、用紙を使用する必要があります。 通常、ユーザーは、できるだけ迅速に行う特定のタスクを取得する必要が、不要な情報はオーバー ロードを許可したくないです。

慎重にカスタム UI を検索し、向きをユーザーにあるか、デバイスを使用する、さまざまな iOS デバイスのすべてのページで適切に動作します。

適切な場合は、既定の Siri UI 内に既に存在、冗長な情報を非表示にする SiriKit API を使用します。 まだアプリ、まだ提供している情報に Siri ができる、口頭で自在の状況で、ことを確認します。

Siri が、ユーザーが要求した写真を表示するなどのユーザーの要求を満たすためにアプリを起動する場所の状況である可能性があります。 これらの状況では、ユーザーに驚くしません。 中間段階またはそれ以上の介入を必要をしなくても、必要な情報を表示します。 決して情報の表示や、ユーザーが予期されていないタスクを実行します。

### <a name="polishing-the-design"></a>デザインの微調整

Apple での通信インターフェイスのデザインを整えるため推奨するいくつかの手順があります。 まず、明確で簡潔なボキャブラリと使用例に Siri を提供することによってです。

Siri という確認とメッセージ交換を開始することによって、ユーザーがアプリを検出する方法のいずれかが*「何を実行できるか」。* Siri は、開発者のアプリなど、実行できるし、例のヒーロー経由で提供しているケースを使用して異なる結果に表示されます、`plist`ファイル。

適切な使用例を記述する方法。

- 例が、アプリ名を含めることを確認します。
- 短期的およびポイントする例を保持します。
- アプリをサポートするインテントの複数の例を示します。
- インテントとアプリの最も一般的なユース ケースに基づいた内の例は、優先順位を設定します。
- アプリがローカライズされた例を提供することを確認します。
- アプリ内で期待どおりの動作を指定されたそれぞれの例を確認してください。
- Siri を例などのテキストを含めないようにアドレスを避けるため*「Hey Siri...」*
- など、不要な pleasantries を避けるため*「ください」*または*「ありがとう」*です。

探索し、実際にアプリが自身のためにユーザーに Siri のあるメッセージ交換を整形する方法を適切な時間がかかります。 やり取りと処理の間の一般的なユーザーでと対話することを確認し、アプリの期待が時間の経過と共に変更可能性があります。

さまざまな状況で、アプリおよびすべての Siri とのメッセージ交換を呼び出すためのさまざまな方法をテストしてください。 テスト現実世界の場所で、ユーザーの可能性がありますを使用しているアプリ、office および机から離れています。

会話 Siri (アプリケーション) の代わり流体、自然、「適切な感覚」に努めています。 

## <a name="summary"></a>まとめ

この記事では、SiriKit を使用するために必要し、iOS デバイスで Siri とマップのアプリを使用してユーザーがアクセスできるサービスを提供する Xamarin.iOS アプリと対話できますを示す主要な概念について説明しました。




## <a name="related-links"></a>関連リンク

- [ElizaChat サンプル](https://developer.xamarin.com/samples/monotouch/ios10/ElizaChat/)
- [SiriKit プログラミング ガイド](https://developer.apple.com/library/prerelease/content/documentation/Intents/Conceptual/SiriIntegrationGuide/index.html)
- [インテント Framework リファレンス](https://developer.apple.com/reference/intents)
- [目的の UI フレームワークのリファレンス](https://developer.apple.com/reference/intentsui)
