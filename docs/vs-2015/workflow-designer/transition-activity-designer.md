---
title: Transition アクティビティデザイナー |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- System.Activities.Statements.Transition.UI
ms.assetid: f6e8b5cc-7fb8-4699-9703-f3c9fc7cc316
caps.latest.revision: 7
author: steved0x
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 446a78e706e1ba3cfd650418a9d329b62b330de8
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72606926"
---
# <a name="transition-activity-designer"></a>Transition アクティビティ デザイナー
<xref:System.Activities.Statements.Transition> は、2 つの状態間の遷移を表します。

## <a name="using-the-transition-activity-designer"></a>Transition アクティビティ デザイナーの使用
 Transition アクティビティ デザイナーを使用すると、2 つの状態間の遷移を構成できます。

### <a name="transition-properties-in-the-workflow-designer"></a>ワークフロー デザイナーでの Transition のプロパティ
 次の表に、ワークフロー デザイナーを使用して設定できる <xref:System.Activities.Statements.Transition> のプロパティと、デザイナーでのその使用方法を示します。

|プロパティ名|必要|使用方法|
|-------------------|--------------|-----------|
|<xref:System.Activities.Statements.Transition.DisplayName%2A>|False|<xref:System.Activities.Statements.Transition> アクティビティ デザイナーの表示名を指定します。 既定値は**T1**です。 値は、プロパティ グリッド、展開された Transition デザイナーのヘッダー、および展開された Transition デザイナー内のアクション セクションのヘッダーで編集できます。 <xref:System.Activities.Activity.DisplayName%2A> は、ワークフロー デザイナーの上部に表示される階層リンク バーで使用されます。<br /><br /> <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。|
|<xref:System.Activities.Statements.Transition.Condition%2A>|False|存在する場合は、制御が送信先状態に渡される前に**True**に評価される必要がある式を指定します。 この条件は、プロパティ グリッドおよび展開された Transition デザイナーで編集できます。 共有遷移に含まれる複数の条件は、Transition デザイナーに表示される順に評価されます。 **注:** 移行の <xref:System.Activities.Statements.Transition.Condition%2A> が**false**と評価された場合 (または、共有トリガー遷移のすべての条件が**false**に評価された場合)、遷移は発生せず、状態からのすべての遷移のすべてのトリガーが再スケジュールされます。 このチュートリアルでは、条件の構成方法 (推定値が正しいか間違っているかを判断する特定のアクションが用意されています) により、この状況は発生しません。|
|**Source**|True|この遷移の発生元の状態を示します。 元の状態の名前をクリックすると、デザイナー ビューはその状態の展開ビューに切り替わります。 この値は、遷移が作成されていて、変更できない場合に設定されます。|
|<xref:System.Activities.Statements.Transition.Trigger%2A>|False|完了時に遷移を開始するアクティビティを指定します。 このアクティビティを設定するには、 **[ツールボックス]** からアクティビティをドラッグし、遷移の **[トリガー]** セクションにドロップします。|
|<xref:System.Activities.Statements.Transition.Action%2A>|False|トリガーアクティビティが完了し、<xref:System.Activities.Statements.Transition.Condition%2A> (存在する場合) が**true**と評価されたときに実行されるアクティビティを指定します。 このアクティビティは、元の状態の <xref:System.Activities.Statements.State.Exit%2A> アクティビティ (存在する場合) が実行された後、遷移先の状態に遷移するときに実行されます。 遷移デザイナーが展開されている場合、この値を設定するには、 **[ツールボックス]** からアクティビティをドラッグし、遷移の **[アクション]** セクションにドロップします。 1 つの遷移に対して複数のアクションが存在する場合があります。 遷移内に複数のアクションがある場合は、アクションに表示される上向き矢印または下向き矢印をクリックすることで、個々のアクションの展開と折りたたみ、および並べ替えを実行できます。|
|**インストール**|True|遷移の完了後にステート マシンが遷移した状態を示します。 これは、オブジェクト モデルにおける遷移の <xref:System.Activities.Statements.Transition.To%2A> プロパティに対応します。 遷移先の状態の名前をクリックすると、デザイナー ビューはその状態の展開ビューに切り替わります。 この値は、遷移が作成されたときに設定され、デザイナーで遷移を遷移先の状態に接続する矢印をドラッグすると変更できます。|

### <a name="creating-transitions"></a>遷移の作成
 遷移を作成するには、ある状態から別の状態へ線をドラッグするか、ある状態を別の状態の上にドラッグすると表示される三角形に状態をドロップします。 ドラッグによって遷移を作成するには、元の状態の端にマウス ポインターを置き、元の状態から遷移先の状態に線をドラッグします。 ドロップによって遷移を作成するには、遷移先の状態をドラッグして元の状態の上にマウス ポインターを置き、元の状態の周囲に表示される 4 つの三角形のうち 1 つにドロップします。 移動先の状態には、 **[ツールボックス]** からドラッグした新しい状態か、ワークフローデザイナーからドラッグした既存の状態を指定できます。

> [!NOTE]
> ステート マシンの 1 つの状態では、ワークフロー デザイナーを使用して作成された遷移を最大 76 個まで含めることができます。 デザイナー以外で作成されたワークフローの状態の遷移に関する制限は、システム リソースによってのみ制限されます。

 トリガーを共有する遷移とは、同じトリガー イベントを共有する遷移のセットです。 共有されるトリガーにより、共通のトリガー イベントを共有する複数の遷移用に構成された式の評価に基づいて、条件に従って遷移先の状態に移行することができます。 遷移に追加のアクションを追加して共有遷移を作成するには、目的の遷移の始点を表す円をクリックし、目的の状態にドラッグします。 新しい遷移では最初の遷移と同じトリガーが共有されますが、その条件とアクションは一意になります。 切り替え効果は、切り替え効果デザイナーの下部にある **[共有トリガー遷移の追加]** をクリックし、**接続に使用可能な**状態から目的の状態を選択することによっても作成できます。ドロップダウン。

## <a name="see-also"></a>参照
 [StateMachine](../workflow-designer/statemachine-activity-designer.md) [finalstate](../workflow-designer/finalstate-activity-designer.md) [状態](../workflow-designer/state-activity-designer.md)