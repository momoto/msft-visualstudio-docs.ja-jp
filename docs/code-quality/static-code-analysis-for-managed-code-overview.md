---
title: マネージド コードのコード分析
ms.date: 06/12/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 4eac88d56399b7f8552962afa50b52c8431232b9
ms.sourcegitcommit: 39a04f42d23597b70053686d7e927ba78f38a9a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2019
ms.locfileid: "71974933"
---
# <a name="overview-of-code-analysis-for-managed-code-in-visual-studio"></a>Visual Studio でのマネージコードのコード分析の概要

Visual Studio では、マネージコードのコード分析を2とおりの方法で実行できます。[従来の分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)では、マネージアセンブリの FxCop 静的分析とも呼ばれ、最新の .NET Compiler Platform ベースの[コードアナライザー](../code-quality/roslyn-analyzers-overview.md)を使用します。 このトピックでは、従来の分析について説明します。 .NET Compiler Platform ベースのコード分析の詳細については、「 [.NET Compiler Platform ベースのアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)」を参照してください。

マネージコードのコード分析では、マネージアセンブリを分析し、 [.Net デザインガイドライン](/dotnet/standard/design-guidelines/)に規定されているプログラミングやデザインの規則違反など、アセンブリに関する情報をレポートします。

分析ツールは、分析中に実行するチェック項目を警告メッセージとして表示します。 警告メッセージは、プログラミングやデザイン上の問題を識別し、可能であれば問題の解決方法を提供します。

> [!NOTE]
> レガシ分析 (静的コード分析) は、Visual Studio の .NET Core および .NET Standard プロジェクトではサポートされていません。 Msbuild の一部として .NET Core または .NET Standard プロジェクトに対してコード分析を実行すると、次のようなエラーが表示されます。 **CA0055: \<.dll > のプラットフォームを識別できませんでし**た。 .NET Core または .NET Standard プロジェクトのコードを分析するには、代わりに[コードアナライザー](../code-quality/roslyn-analyzers-overview.md)を使用します。

## <a name="ide-integrated-development-environment-integration"></a>IDE (統合開発環境) の統合

コード分析は、プロジェクトに対して手動または自動で実行できます。

プロジェクトをビルドするたびにコード分析を実行するには、プロジェクトの **[コード分析]** プロパティページでオプションを選択します。 詳細については、「[方法: 自動コード分析を有効または無効](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)にする」を参照してください。

プロジェクトでコード分析を手動で実行するには、メニューバーから **分析** を選択し、**コード分析の実行** >  **\<プロジェクト > でコード分析を実行** > ます。

## <a name="rule-sets"></a>規則セット

マネージド コード用のコード分析規則は、[規則セット](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)にグループ化されています。 Microsoft の標準の規則セットのいずれかを使用することも、特定のニーズを満たす[カスタム規則セットを作成](../code-quality/how-to-create-a-custom-rule-set.md)することもできます。

## <a name="suppress-warnings"></a>警告を表示しない

警告が適用されないことを示すと役に立つことがよくあります。 これによって、開発者や、そのコードを後でレビューする担当者は、その警告が既に調査済みであり、抑制されるのかまたは無視されるのかがわかります。

警告のソース内の抑制は、カスタム属性によって実装されます。 警告を抑制するには、次の例のように、属性 `SuppressMessage` をソース コードに追加します。

```csharp
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
Public class MyClass
{
   // code
}
```

詳細については、「[警告の非](../code-quality/in-source-suppression-overview.md)表示」を参照してください。

::: moniker range="vs-2017"

> [!NOTE]
> プロジェクトを Visual Studio 2017 に移行すると、コード分析の警告が多数発生する可能性があります。 警告を修正する準備ができていない場合は、[ > **分析**] を選択**してコード分析を実行し、アクティブな問題を抑制**することによって、すべての警告を非表示にすることができます。
>
> ![Visual Studio でコード分析を実行し、問題を抑制する](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019"

> [!NOTE]
> プロジェクトを Visual Studio 2019 に移行すると、コード分析の警告が多数発生する可能性があります。 警告を修正する準備ができていない場合は、 **[分析]** を選択して、**アクティブな問題を > ビルドし、非**表示にすることにより、すべてを抑制できます。

::: moniker-end

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>チェックイン ポリシーの一部としてのコード分析の実行

組織的な取り決めとして、チェックインされるすべてのコードが、特定のポリシーを満たしていることが必要な場合があります。 たとえば、次のようなポリシーが考えられます。

- チェックインされているコードにビルドエラーはありません。

- コード分析は、最新のビルドの一部として実行されます。

これは、チェックイン ポリシーを指定することにより実現できます。 詳細については、「[プロジェクトのチェックインポリシーによるコード品質の向上](../code-quality/how-to-create-or-update-standard-code-analysis-check-in-policies.md)」を参照してください。

## <a name="team-build-integration"></a>チームビルドの統合

ビルド システムの統合機能を使用すると、分析ツールをビルド プロセスの一環として実行できます。 詳細については、「[Azure Pipelines](/azure/devops/pipelines/index?view=vsts)」を参照してください。

## <a name="see-also"></a>参照

- [.NET Compiler Platform ベースのアナライザーの概要](../code-quality/roslyn-analyzers-overview.md)
- [規則セットを使用したコード分析規則のグループ化](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [方法: 自動コード分析を有効/無効にする](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
