---
title: Windows ストア アプリ (JavaScript) 用の Visual Studio デバッグ セッションでのストア アプリの実行の制御 |Microsoft Docs
ms.custom: ''
ms.date: 2018-06-30
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 60159535-61ec-466a-a4a6-115ec72a8af5
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e5725dc2be204ae3b657a857c5a358a29b8c3709
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2018
ms.locfileid: "47535623"
---
# <a name="control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript"></a>Windows ストア アプリ用の Visual Studio デバッグ セッションでの、ストア アプリの実行制御 (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックの最新バージョンをご覧[Windows ストア アプリ (JavaScript) 用の Visual Studio デバッグ セッションで、ストア アプリの実行を制御](https://docs.microsoft.com/visualstudio/debugger/control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript)します。  
  
このクイック スタートでは、Visual Studio デバッガー内を移動する方法と、セッションでのプログラムの状態を表示する方法を示します。  
  
 Visual Studio でのデバッグに慣れていない開発者や、Visual Studio でのデバッグ セッション間の移動について詳しく学習したい開発者向けです。 デバッグ自体の手法については説明しません。 サンプル コードの関数は、このトピックで説明しているデバッグ手順を示すためだけに設計されています。 これらの関数は、アプリまたは関数の設計に関するベスト プラクティスに従ったものではありません。 実際、すぐにわかるように、関数もアプリ自体もほとんど何もしません。  
  
 このクイック スタートの各セクションは、できるだけ独立した設計にしたので、既に精通している情報が含まれているセクションはスキップできます。 また、サンプル アプリを作成する必要はありません。 それでも、できる限り簡単にしてあるので、作成することをお勧めします。  
  
 **デバッガーのキーボード ショートカット。** Visual Studio デバッガーのナビゲーションは、マウスとキーボードの両方に最適化されています。 このトピックの手順の多くでは、キーボード アクセス キーまたはショートカット キーが、かっこで囲まれて示されています。 たとえば、(キーボード: F5) は、F5 キーを押すとデバッガーの実行が開始または継続されることを示しています。  
  
> [!NOTE]
>  **モジュール パターン**  
>   
>  Windows ストア アプリでは、JavaScript の *モジュール パターン* を使用してデータと関数をページ内にカプセル化することがよくあります。 モジュール パターンでは、自己実行形式の単一の匿名クロージャを使用して、ページの機能をグローバル名前空間から分離します。 このトピックでは、そのような関数を *モジュール*と呼びます。  
  
## <a name="in-this-topic"></a>このトピックの内容  
 以下の方法について説明します。  
  
 [サンプル アプリを作成する](#BKMK_Create_the_sample_app)  
  
 [ブレークポイントを設定してそこまで実行し、関数にステップ インして、プログラムのデータを調べる](#BKMK_Set_and_run_to_a_breakpoint__step_into_a_function__and_examine_program_data)  
  
 [関数をステップイン、ステップオーバー、ステップアウトする](#BKMK_Step_into__over__and_out_of_functions)  
  
 [条件付きブレークポイントを設定し、カーソル位置まで実行して、変数を視覚化する](#BKMK_Set_a_conditional_breakpoint__run_to_the_cursor__and_visualize_a_variable)  
  
 [[ローカル] ウィンドウで変数のデータを表示する](#BKMK_View_variable_data_in_the_Locals_window)  
  
-   [オブジェクトの変数データとプロトタイプ チェーンを表示する](#BKMK_View_variable_data_and_the_prototype_chain_of_an_object)  
  
-   [スコープ チェーンのデータを調べる](#BKMK_Examine_scope_chain_data)  
  
 [[呼び出し履歴] ウィンドウを使用してコードに移動する](#BKMK_Navigate_to_code_by_using_the_Call_Stack_window)  
  
##  <a name="BKMK_Create_the_sample_app"></a> サンプル アプリを作成する  
 デバッグの対象はコードなので、このサンプル アプリでは、デバッグ セッション内の移動方法とプログラムの状態を調べる方法がわかる程度のソース ファイルを作成するためだけに Windows ストア アプリのフレームワークを使用します。 呼び出すコードはすべて、default.js ファイルの `module` 関数から呼び出されます。 コントロールは追加されず、イベントは処理されません。  
  
1.  **空の JavaScript Windows ストア アプリを作成します。** Visual Studio を開きます。 ホーム ページで、 **[新しいプロジェクト]** リンクを選択します。 **[新しいプロジェクト]** ダイアログ ボックスで、 **[インストール済み]** ボックスの一覧の **[JavaScript]** を選択し、 **[Windows ストア]** を選択します。 プロジェクト テンプレートの一覧で、 **[新しいアプリケーション]** を選択します。 新しいソリューションとプロジェクトが作成され、default.htm ファイルがコード エディターに表示されます。  
  
     ページに読み込まれるスクリプト ファイルにご注意ください。  
  
    -   `base.js` および `ui.js` ファイルによって、 **JavaScript 用 Windows ライブラリ**が作成されます。 JavaScript 用 Windows ライブラリは一連の JavaScript および CSS ファイルであり、JavaScript を使用して Windows ストア アプリを簡単に作成できるようにします。 これを HTML、CSS、Windows ランタイムと共に使用して、アプリを作成します。  
  
    -   コードは `default.js`  ファイルで開始します。  
  
2.  **default.js ソース ファイルを開きます。** ソリューション エクスプローラーで、 **[js]** ノードを開いて `default.js`と呼びます。  
  
3.  **ページの内容をサンプル コードに置き換えます。** `default.js` ファイルの内容をすべて削除します。 「 [Debugger navigation sample code (JavaScript)](../debugger/debugger-navigation-sample-code-javascript.md)」を参照して、JavaScript セクションに記載されているコードをクリップボードにコピーします。 (選択**戻る**ブラウザーまたはヘルプ ビューアーは、このクイック スタート ページに戻る)。Visual Studio エディターで、空にした `default.js` にコードを貼り付けます。 **Ctrl+ S** を選んでファイルを保存します。  
  
 これで、このトピックの例を実際に行うことができるようになりました。  
  
##  <a name="BKMK_Set_and_run_to_a_breakpoint__step_into_a_function__and_examine_program_data"></a> ブレークポイントを設定してそこまで実行し、関数にステップ インして、プログラムのデータを調べる  
 デバッグ セッションを開始する最も一般的な方法は、 **[デバッグ]** メニューの **[デバッグ開始]** を選ぶことです (キーボード: F5)。 アプリが開始し、ブレークポイントに達するか、手動で実行が中断されるか、例外が発生するか、アプリが終了するまで実行が続きます。  
  
 デバッガーで実行が中断されているときは、変数の上にマウスを置けば、アクティブな変数の値をデータのヒントで確認できます。  
  
 アプリの実行を中断 (デバッガーで中断) した後、残りのプログラム コードの実行方法を制御します。 1 行ずつ実行したり、関数呼び出しから関数自体に移動したり、呼び出されている関数をシングル ステップで実行したりできます。 これらの手順は、アプリのステップ実行と呼ばれます。 また、アプリの普通の実行を再開したり、設定してある次のブレークポイントまで実行したり、カーソルを置いた行まで実行したりすることもできます。 デバッグ セッションはいつでも停止できます。 デバッガーは、必要なクリーンアップ操作を行って実行を終了するように設計されています。  
  
###  <a name="BKMK_Example_1"></a> 例 1  
 この例では、 `module` の `default.js` 関数の本体にブレークポイントを設定します。ここで、最初のユーザー ステートメントが呼び出されます。 次に、関数にステップ インし、デバッガーのデータのヒントで変数の値を表示して、デバッグを停止します。  
  
1.  **ブレークポイントを設定します。** `app.start()` の呼び出しの直後にあるステートメント `callTrack = "module function";` にブレークポイントを設定します。 ソース コード エディターの網掛けされた余白で行を選びます (キーボード: 行にカーソルを置き、 **F9** キーを押します)。  
  
     ![例 1 にブレークポイントを設定](../debugger/media/dbg-jsnav-example1-breakpoint.png "DBG_JSNAV_example1_breakpoint")  
  
     ブレークポイント アイコンが余白に表示されます。  
  
2.  **ブレークポイントまで実行します。** 選択して、デバッグ セッションを開始**デバッグの開始**上、**デバッグ**メニュー (キーボード: F5)。  
  
     アプリの実行が開始され、ブレークポイントを設定したステートメントの直前で実行が中断します。 余白の現在行アイコンによって場所が示され、現在のステートメントが強調表示されます。  
  
     ![ブレークポイントまで実行](../debugger/media/dbg-jsnav-example1-run-to-breakpoint.png "DBG_JSNAV_example1_run_to_breakpoint")  
  
     アプリの実行を制御できるようになり、プログラムのステートメントをステップ実行しながらプログラムの状態を確認できます。  
  
3.  **関数にステップ インします。** **デバッグ**] メニューの [選択**ステップ イン**(キーボード: **F11**)。  
  
     ![コード行にステップ イン](../debugger/media/dbg-jsnav-example1-step-into.png "DBG_JSNAV_example1_step_into")  
  
     デバッガーが次の行である `example1` 関数の呼び出しに移動します。 **[ステップ イン]** を再び選択します。 デバッガーが `example1` 関数の最初のコード行に移動します。 強調表示された行はまだ実行されていませんが、関数は呼び出し履歴に読み込まれ、ローカル変数のメモリが割り当てられています。  
  
4.  コード行にステップ インするとき、デバッガーは次の操作のいずれかを実行します。  
  
    -   次のステートメントがソリューション内の関数の呼び出しではない場合、デバッガーはステートメントを実行し、次のステートメントに移動して、実行を中断します。  
  
    -   ステートメントがソリューション内の関数の呼び出しの場合、デバッガーは呼び出された関数の最初の行に移動して、実行を中断します。  
  
     終了ポイントに到達するまで、 `example1` のステートメントのステップ インを続けます。 デバッガーにより、関数の終了の中かっこが強調表示されます。  
  
5.  **データのヒントで変数の値を表示します。** 終了ポイントに到達するまで、 `example1` のステートメントのステップ インを続けます。 デバッガーにより、関数の終了の中かっこが強調表示されます。 変数名の上にマウス ポインターを置くと、変数の名前と値がデータのヒントに表示されます。  
  
     ![データ ヒントで変数の値を表示](../debugger/media/dbg-jsnav-data-tip.png "DBG_JSNAV_data_tip")  
  
6.  **callTrack 変数のウォッチ式を追加します。** このクイック スタートでは、例の中で呼び出された関数の表示に `callTrack` 変数を使用しています。 変数の値を見やすくするため、ウォッチ ウィンドウに追加します。 エディターで変数名を選び、ショートカット メニューの **[ウォッチ式の追加]** を選びます。  
  
     ![変数のウォッチ](../debugger/media/dbg-jsnav-watch-window.png "DBG_JSNAV_watch_window")  
  
     [ウォッチ] ウィンドウでは複数の変数を確認できます。 データ ヒント ウィンドウの値など、ウォッチ対象の変数の値は、実行が中断されるたびに更新されます。 ウォッチ対象の変数は、デバッグ セッション間で保存されます。  
  
7.  **デバッグを停止します。** **デバッグ** メニューの 選択**デバッグの停止** (キーボード: **Shift + F5**)。 これによりデバッグ セッションが終了します。  
  
##  <a name="BKMK_Step_into__over__and_out_of_functions"></a> 関数をステップイン、ステップオーバー、ステップアウトする  
 親関数によって呼び出される関数へのステップ インとは異なり、関数のステップ オーバーでは、子関数が実行された後、親が再開すると、呼び出し側の関数で実行が中断されます。 関数の動作がよくわかっていて、その実行が調査中の問題に影響を与えないことが明らかな場合などは、関数をステップ オーバーします。  
  
 関数の呼び出しを含まないコード行をステップ オーバーすると、行へのステップ インと同じように行が実行されます。  
  
 子関数をステップ アウトすると、子関数の実行が続けられ、子関数から呼び出し側の関数に戻った後で、実行が中断されます。 長い関数で残りの部分は重要ではないと判断した場合など、ステップ アウトを使用できます。  
  
 関数のステップ オーバーでもステップ アウトでも、関数は実行されます。  
  
 ![手順に、オーバー、およびメソッドから](../debugger/media/dbg-basics-stepintooverout.png "DBG_Basics_StepIntoOverOut")  
  
###  <a name="BKMK_Example_2"></a> 例 2  
 この例では、関数のステップイン、ステップ オーバー、およびステップ アウトを実行します。  
  
1.  **モジュール関数内の example2 関数を呼び出します。** 編集、`module`関数し、後の行を置換`var callTrack = "module function"`で`example2();`します。  
  
     ![Example2 関数を呼び出す](../debugger/media/dbg-jsnav-example2.png "DBG_JSNAV_example2")  
  
2.  **ブレークポイントまで実行します。** 選択して、デバッグ セッションを開始**デバッグの開始**上、**デバッグ**メニュー (キーボード: F5)。 デバッガーの実行がブレークポイントで中断します。  
  
3.  **ステップ オーバーのコード行。** **デバッグ**] メニューの [選択**ステップ オーバー** (キーボード: F10)。 デバッガーは、ステートメントのステップ インと同じ方法で、 `var callTrack = "module function"` ステートメントを実行します。  
  
4.  **Example2 および example2_a にステップ インします。** 選択、 **F11**にステップ イン キー、`example2`関数。 `example2` 行に到達するまで `var x = example2_a();`のステートメントのステップ インを続けます。 再びこの行にステップ インして、 `example2_a`のエントリ ポイントに移動します。 `example2_a` に戻るまで `example2`の各ステートメントのステップ インを続けます。  
  
     ![ステップ オーバー関数](../debugger/media/dbg-jsnav-example2-a.png "DBG_JSNAV_example2_a")  
  
5.  **関数をステップ オーバーします。** `example2` の次の行 `var y = example2_a();` は基本的に前の行と同じであることに注意してください。 この行は安全にステップ オーバーできます。 **F10** キーを押して、 `example2` の再開から `example2_a`のこの 2 回目の呼び出しまで移動します。 `callTrack` 文字列で `example2_a` 関数が 2 回実行されたことが示されている点にご注意ください。  
  
6.  **関数をステップ アウトします。** 選択、 **F11**にステップ イン キー、`example2_b`関数。 `example2_b` が `example2_a`と大差ないことに注意してください。 関数をステップ アウトするには、 **[デバッグ]** メニューの **[ステップ アウト]** を選択します (キーボード: **Shift+F11**)。 `callTrack` 変数で、 `example2_b` が実行されたこと、またデバッガーが `example2` の再開ポイントに戻ったことが示されていることにご注意ください。  
  
7.  **デバッグを停止します。** **デバッグ** メニューの 選択**デバッグの停止** (キーボード: **Shift + F5**)。 これによりデバッグ セッションが終了します。  
  
##  <a name="BKMK_Set_a_conditional_breakpoint__run_to_the_cursor__and_visualize_a_variable"></a> 条件付きブレークポイントを設定し、カーソル位置まで実行して、変数を視覚化する  
 条件付きブレークポイントでは、デバッガーが実行を中断する条件を指定します。 条件は、true または false として評価できる任意のコード式によって指定します。 たとえば、条件付きブレークポイントを使用すると、変数が特定の値に到達した場合にのみ、頻繁に呼び出される関数でのプログラムの状態を確認できます。  
  
 カーソルまでの実行は、一度だけのブレークポイントを設定することと同じです。 実行が中断されたら、ソースで行を選択し、選択した行に到達するまで実行を再開できます。 たとえば、関数内のループをステップ実行していて、ループのコードが正しく実行していることがわかったものとします。 そのような場合、ループのすべての反復をステップ実行する代わりに、ループの実行が終了した後に配置したカーソルまで実行できます。  
  
 データのヒントや他のデータ ウィンドウの行で変数の値を表示することが困難な場合があります。 デバッガーでは、スクロール可能なウィンドウに書式設定された値が表示されるテキスト ビジュアライザーで、文字列、HTML、Xml を表示できます。  
  
###  <a name="BKMK_Example_3"></a> 例 3  
 この例では、ループの特定の繰り返しで中断するように条件付きブレークポイントを設定し、ループの後に配置したカーソルまで実行します。 また、テキスト ビジュアライザーで変数の値を表示します。  
  
1.  **モジュール関数内の example3 関数を呼び出します。** 編集、`module`関数し、後の行を置換`var callTrack = "module function";`行`example3();`します。  
  
     ![Example3 メソッドを呼び出す](../debugger/media/dbg-jsnav-example3.png "DBG_JSNAV_example3")  
  
2.  **ブレークポイントまで実行します。** 選択して、デバッグ セッションを開始**デバッグの開始**上、**デバッグ**メニュー (キーボード: **F5**)。 `module` 関数内のブレークポイントでデバッガーの実行が中断します。  
  
3.  **Example3 関数にステップ インします。** 選択**ステップ イン**上、**デバッグ**メニュー (キーボード: **F11**) のエントリ ポイントに移動する、`example3`関数。 関数のステップ インを続けて、 `for` ブロックのループを 1 または 2 回繰り返します。 1000 回の繰り返しすべてをステップ実行するには長い時間がかかります。  
  
4.  **条件付きブレークポイントを設定します。** コード ウィンドウの左側の余白で、 `s += i.toString() + "\n";` という行を右クリックし、ショートカット メニューの **[条件]** を選択します。  
  
     **[条件]** チェック ボックスをオンにして、テキスト ボックスに「 `i == 500;` 」と入力します。 **[true の場合]** オプションを選択し、 **[OK]** をクリックします。 ブレークポイントでは、 `for` ループの 500 回目の繰り返しでの値を確認できます。 条件付きブレークポイント アイコンは白い十字が目印です。  
  
     ![条件付きブレークポイント アイコン](../debugger/media/dbg-jsnav-breakpoint-condition-icon.png "DBG_JSNAV_Breakpoint_Condition_icon")  
  
5.  **ブレークポイントまで実行します。** **デバッグ**] メニューの [選択**続行**(キーボード: **F5**)。 `i` で一時停止し、 `i` の現在の値が 500 であることを確認します。 変数 `s` が 1 行に表示され、データ ヒント ウィンドウよりかなり長いことにもご注意ください。  
  
6.  **文字列変数を視覚化します。** データ ヒントで虫眼鏡アイコンをクリックして、`s`します。  
  
     テキスト ビジュアライザー ウィンドウが表示され、文字列の値が複数行の文字列として示されます。  
  
     ![テキスト ビジュアライザーのデバッグ](../debugger/media/dbg-jsnav-text-visualizer.png "DBG_JSNAV_Text_Visualizer")  
  
7.  **カーソルまでを実行します。** 行を選択します`callTrack += "->example3";`選び、**カーソルまで実行**ショートカット メニューの (キーボード: **Ctrl + F10**)。 デバッガーは、ループの繰り返しを完了して、カーソルの行で実行を中断します。  
  
8.  **デバッグを停止します。** **デバッグ** メニューの 選択**デバッグの停止** (キーボード: **Shift + F5**)。 これによりデバッグ セッションが終了します。  
  
###  <a name="BKMK_Use_Run_to_Cursor_to_return_to_your_code_and_delete_a_breakpoint"></a> [カーソル行の前まで実行] を使用してコードに戻り、ブレークポイントを削除する  
 Microsoft またはサードパーティから提供されているライブラリ コードにステップ インしている場合、カーソル行の前まで実行すると便利な場合があります。 ライブラリ コードのステップ実行は役に立ちますが、長い時間がかかることがあります。 また、自分のコードに対する興味の方がはるかに大きいのが普通です。 この演習では、その方法を説明します。  
  
1.  **App.start の呼び出しにブレークポイントを設定します。** `module`関数を行にブレークポイントを設定 `app.start()`  
  
2.  **ブレークポイントまで実行し、ライブラリ関数にステップ インします。**  
  
     `app.start()`にステップ インすると、エディターに `base.js`のコードが表示されます。 さらに数行ステップ インします。  
  
3.  **フェールオーバーと関数からの手順です。** ステップ オーバー (**F10**) およびステップ アウト (**SHIFT + F11**) でコードを`base.js`は start 関数の長さは行わないことに、複雑さを調べるという結論になる可能性があります。  
  
4.  **自分のコードにカーソルを設定して、そこまで実行します。** コード エディターで `default.js` ファイルに切り替えます。 `app.start()` の後の最初のコード行を選択します (コメント行または空白行まで実行することはできません)。 ショートカット メニューの **[カーソル行の前まで実行]** を選択します。 デバッガーは app.start の関数の実行を続け、ブレークポイントで実行を中断します。  
  
##  <a name="BKMK_View_variable_data_in_the_Locals_window"></a> [ローカル] ウィンドウで変数のデータを表示する  
 [ローカル] ウィンドウは、現在実行中の関数のスコープ チェーンに含まれるパラメーターと変数のツリー ビューです。  
  
###  <a name="BKMK_View_variable_data_and_the_prototype_chain_of_an_object"></a> オブジェクトの変数データとプロトタイプ チェーンを表示する  
  
1.  **配列オブジェクトをモジュール関数を追加します。** 編集、`module`関数し、後の行を置換`var callTrack = "module function"`で `var myArray = new Array(1, 2, 3);`  
  
     ![myArray 定義](../debugger/media/dbg-jsnav-myarray.png "DBG_JSNAV_myArray")  
  
2.  **ブレークポイントまで実行します。** 選択して、デバッグ セッションを開始**デバッグの開始**上、**デバッグ**メニュー (キーボード: **F5**)。 デバッガーの実行がブレークポイントで中断します。 この行までステップ インします。  
  
3.  **[ローカル] ウィンドウを開きます。** On the **[デバッグ開始]** メニューの **[ウィンドウ]** をポイントし、 **[ローカル]** と呼びます。 (キーボード: Alt + 4)。  
  
4.  **モジュール関数でローカル変数を調べます。** [ローカル] ウィンドウでは、現在実行中の関数 ( `module` 関数) の変数が、ツリーの最上位ノードとして表示されます。 関数に入ると、JavaScript はすべての変数を作成し、 `undefined`という値を設定します。 関数内で定義されている関数には、値としてそれぞれテキストが設定されています。  
  
     ![[ローカル] ウィンドウ](../debugger/media/dbg-jsnav-locals-window.png "DBG_JSNAV_Locals_window")  
  
5.  **callTrack および myArray の定義をステップ実行します。** [ローカル] ウィンドウで callTrack 変数および myArray 変数を探します。 2 つの定義をステップ オーバーし (**F10**)、 **Value** フィールドと **Type** フィールドが変更されていることを確認します。 [ローカル] ウィンドウでは、前回のブレーク以降に変更された変数の値が強調表示されます。  
  
6.  **MyArray オブジェクトを調べます**展開、`myArray`変数。 配列の各要素が、 **オブジェクトの継承階層を含む** [プロトタイプ] `Array` ノードに一覧表示されます。 このノードを展開します。  
  
     ![[ローカル] ウィンドウのプロトタイプ チェーン](../debugger/media/dbg-jsnav-locals-proto-chain.png "DBG_JSNAV_Locals_proto_chain")  
  
    -   **[メソッド]** ノードには、 `Array` オブジェクトのすべてのメソッドが一覧表示されます。  
  
    -   **[prototype]** ノードには、 `Object` の派生元である `Array` オブジェクトのプロトタイプが含まれます。 **[prototype]** ノードは再帰的である場合があります。 オブジェクト階層内の各親オブジェクトは、その子の **[prototype]** ノードで記述されています。  
  
7.  **デバッグを停止します。** **デバッグ** メニューの 選択**デバッグの停止** (キーボード: shift + f5)。 これによりデバッグ セッションが終了します。  
  
##  <a name="BKMK_Examine_scope_chain_data"></a> スコープ チェーンのデータを調べる  
 関数の *スコープ チェーン* には、アクティブであり、関数で到達可能なすべての変数が含まれます。 グローバル変数は、現在実行中の関数を定義している関数内で定義されているオブジェクト (関数を含みます) と同様に、スコープ チェーンの一部です。 たとえば、 `callTrack` の `module` 関数で定義されている `default.js` 変数は、 `module` 関数で定義されているすべての関数から到達可能です。 各スコープは [ローカル] ウィンドウで個別に一覧表示されます。  
  
-   現在実行中の関数の変数はウィンドウの最上部に表示されます。  
  
-   スコープ チェーン内の各関数スコープの変数は、その関数の **[Scope]** ノードに一覧表示されます。 スコープ関数は、現在の関数を定義している関数から、チェーンの最も外側の関数まで、チェーン内での順番で一覧表示されます。  
  
-   **[Globals]** ノードには、すべての関数の外側で定義されているグローバル オブジェクトが一覧表示されます。  
  
 スコープ チェーンはわかりにくいことがあり、例で示すとよくわかります。 次の例を見ると、 `module` 関数によってそれ自体のスコープが作成されている方法、およびクロージャを作成することで別のレベルのスコープを作成する方法がわかります。  
  
###  <a name="BKMK_Example_4"></a> 例 4  
  
1.  **モジュール関数内の example4 関数を呼び出します。** 編集、`module`関数し、後の行を置換`var callTrack = "module function"`で、 `example4()`:  
  
     ![Example4 メソッドを呼び出す](../debugger/media/dbg-jsnav-example4.png "DBG_JSNAV_example4")  
  
2.  **ブレークポイントまで実行します。** 選択して、デバッグ セッションを開始**デバッグの開始**上、**デバッグ**メニュー (キーボード: **F5**)。 デバッガーの実行がブレークポイントで中断します。  
  
3.  **[ローカル] ウィンドウを開きます。** 必要に応じて、 **[デバッグ開始]** メニューの **[ウィンドウ]** をポイントし、 **[ローカル]** と呼びます。 (キーボード: **Alt+4**)。 ウィンドウには `module` 関数内のすべての変数と関数が一覧表示されているほか、 **[Globals]** ノードが含まれています。  
  
4.  **グローバル変数を確認します。** [ローカル] ウィンドウで **[Globals]** ノードが含まれています。 [グローバル] 内のオブジェクトや変数は、JavaScript 用 Windows ライブラリによって設定されたものです。 グローバル スコープには独自の変数を追加できます。  
  
5.  **Example4 にステップ インし、ローカルの確認し、スコープ変数**にステップ イン (キーボード: **F11**)、`example4`関数。 `example4` は `module` 関数で定義されるため、 `module` 関数が親スコープになります。 `example4` は `module` 関数内の任意の関数を呼び出し、その変数にアクセスできます。 [ローカル] ウィンドウで **[Scope]** ノードを展開し、 `module` 関数と同じ変数が含まれることをご確認ください。  
  
     ![Example4 メソッドのスコープ](../debugger/media/dbg-jsnav-locals-example4-scope.png "DBG_JSNAV_Locals_example4_scope")  
  
6.  **example4_a にステップ インし、ローカル変数とスコープ変数を調べます。** 続けて `example4` にステップ インし、 `example4_a`の呼び出しにステップ インします。 ローカル変数が `example4_a`のものになり、 **[スコープ]** ノードには引き続き `module` 関数の変数が保持されていることに注意してください。 `example4` の変数はアクティブですが、 `example4_a` では到達できず、スコープ チェーンの一部ではなくなっています。  
  
7.  **multipyByA にステップ インし、ローカル変数とスコープ変数を調べます。** 残りの `example4_a` をステップ実行し、 `var x = multilpyByA(b);`の行にステップ インします。  
  
     関数の変数 `multipyByA` は、 `multiplyClosure` クロージャ *である*関数に設定されています。 `multipyClosure` は、内部関数 `mulitplyXby`を定義して返し、そのパラメーターと変数をキャプチャし (閉じ込め) ます。 クロージャでは、返される内部関数は外部関数のデータにアクセスでき、独自のスコープ レベルを作成します。  
  
     `var x = multilpyByA(b);`にステップ インすると、 `return a * b;` 内部関数の `mulitplyXby` 行に移動します。  
  
8.  [ローカル] ウィンドウでは、 `b` パラメーターだけが `multiplyXby`のローカル変数として表示されていますが、新しい **[Scope]** レベルが追加されています。 このノードを展開すると、 `multiplyClosure`のパラメーター、関数、変数が含まれ、さらに `a` の最初の行で呼び出されている `multiplyXby`変数も含まれることがわかります。 2 番目の **[Scope]** ノードを調べると、 `multiplyXby` が次の行でアクセスしているモジュール関数の変数が表示されます。  
  
     ![[ローカル] ウィンドウのクロージャのスコープ](../debugger/media/dbg-jsnav-scope-mulitplyxby.png "DBG_JSNAV_scope_mulitplyXby")  
  
9. **デバッグを停止します。** **デバッグ** メニューの 選択**デバッグの停止** (キーボード: **Shift + F5**)。 これによりデバッグ セッションが終了します。  
  
##  <a name="BKMK_Navigate_to_code_by_using_the_Call_Stack_window"></a> [呼び出し履歴] ウィンドウを使用してコードに移動する  
 呼び出し履歴は、アプリケーションの現在のスレッドで実行されている関数についての情報を格納するデータ構造です。 ブレークポイントにヒットすると、スタック上でアクティブなすべての関数が [呼び出し履歴] ウィンドウに一覧表示されます。 現在実行中の関数が、[呼び出し履歴] ウィンドウのリストの先頭に表示されます。 スレッドを開始した関数は、リストの最後にあります。 その間の関数は、開始関数から現在の関数までの呼び出しパスを示します。  
  
 現在実行中の関数までの呼び出しパスを表示するだけでなく、[呼び出し履歴] ウィンドウはコード エディター内のコードへの移動にも使用できます。 この機能は、複数のファイルの作業を実行していて、特定の関数にすばやく移動する場合に便利です。  
  
###  <a name="BKMK_Example_5"></a> 例 5  
 この例では、5 つのユーザー定義関数を含む呼び出しパスにステップ インします。  
  
1.  **モジュール関数内の example5 関数を呼び出します。** 編集、`module`関数し、後の行を置換`var callTrack = "module function";`行`example5();`します。  
  
     ![Example5 の呼び出し](../debugger/media/dbg-jsnav-example5.png "DBG_JSNAV_example5")  
  
2.  **ブレークポイントまで実行します。** 選択して、デバッグ セッションを開始**デバッグの開始**上、**デバッグ**メニュー (キーボード: **F5**)。 モジュール関数内のブレークポイントでデバッガーの実行が中断します。  
  
3.  **呼び出し履歴 ウィンドウを開きます。** **デバッグ**] メニューの [選択**Windows**を選び、**呼び出し履歴**(キーボード: alt + 7)。 [呼び出し履歴] ウィンドウに 2 つの関数が表示されます。  
  
    -   **[グローバル コード]** は、呼び出し履歴の下端にある `module` 関数のエントリ ポイントです。  
  
    -   **[匿名関数]** には、 `module` 関数内で実行が中断されている行が示されます。 これは、呼び出し履歴の先頭にあります。  
  
4.  **Example5_d 関数に到達する関数にステップ インします。** 選択**ステップ イン**上、**デバッグ**メニュー (キーボード: **F11**)、example5_d 関数のエントリ ポイントに到達するまで呼び出しパスの呼び出しを実行します。 ある関数で別の関数が呼び出されるたびに、呼び出す関数の行番号が保存され、呼び出される関数がスタックの先頭に表示されることに注意してください。 呼び出す関数の行番号は、呼び出す関数の実行が中断しているポイントです。 黄色の矢印は、現在実行中の関数を示します。  
  
     ![呼び出し履歴 ウィンドウ](../debugger/media/dbg-jsnav-callstack-windows.png "DBG_JSNAV_CallStack_windows")  
  
5.  **呼び出し履歴 ウィンドウを使用して example5_a のコードに移動し、ブレークポイントを設定します。** 呼び出し履歴] ウィンドウで、選択、`example5_a`リスト項目選び、**ソースに移動します**ショートカット メニューの [します。 コード エディターで、関数の return 行にカーソルが設定されます。 この行にブレークポイントを設定します。 現在実行中の行は変更されないことに注意してください。 エディターのカーソルだけが移動します。  
  
6.  **関数にステップ インし、ブレークポイントまで実行します。** `example5_d` のステップ インを続けます。 関数から戻ると、関数が呼び出し履歴から削除されることに注意してください。 **F5** キーを押してプログラムの実行を続行します。 前の手順で作成したブレークポイントで停止します。  
  
7.  **デバッグを停止します。** **デバッグ** メニューの 選択**デバッグの停止** (キーボード: **Shift + F5**)。 これによりデバッグ セッションが終了します。  
  
## <a name="see-also"></a>関連項目  
 [デバッグ セッション (JavaScript) を開始します。](../debugger/start-a-debugging-session-for-store-apps-in-visual-studio-javascript.md)   
 [クイック スタート: デバッガー ナビゲーション (JavaScript)](../debugger/control-execution-of-a-store-app-in-a-visual-studio-debug-session-for-windows-store-apps-javascript.md)   
 [クイック スタート: HTML と CSS をデバッグします。](../debugger/quickstart-debug-html-and-css.md)   
 [トリガーの中断、再開、およびバック グラウンド イベントを Windows ストア)](../debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)   
 [Visual Studio でのアプリのデバッグ](../debugger/debug-store-apps-in-visual-studio.md)


