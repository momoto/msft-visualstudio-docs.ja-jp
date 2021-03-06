---
title: 'CA1801: 使用されていないパラメーターを確認します。Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedParameters
- CA1801
- ReviewUnusedParameters
helpviewer_keywords:
- CA1801
- ReviewUnusedParameters
ms.assetid: 5d73545c-e153-4b7c-a7b2-be6bf5aca5be
caps.latest.revision: 31
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: caf1ec865d604545940b0a5442947ef61bd60f9a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671526"
---
# <a name="ca1801-review-unused-parameters"></a>CA1801: 使用されていないパラメーターを再確認します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の最新のドキュメントについては、「 [CA1801: 使用](https://docs.microsoft.com/visualstudio/code-quality/ca1801-review-unused-parameters)されていないパラメーターの確認」を参照してください。

|||
|-|-|
|TypeName|ReviewUnusedParameters|
|CheckId|CA1801|
|カテゴリ|Microsoft. 使用方法|
|互換性に影響する変更点|非重大-変更に関係なく、メンバーがアセンブリの外部で参照できない場合。<br /><br /> 非ブレーク-本文内でパラメーターを使用するようにメンバーを変更した場合。<br /><br /> 中断-パラメーターを削除すると、アセンブリの外部から参照できるようになります。|

## <a name="cause"></a>原因
 メソッドのシグネチャに、メソッドの本体で使用されていないパラメーターがあります。 この規則では、次の方法は検証されません。

- デリゲートによって参照されるメソッド。

- イベントハンドラーとして使用されるメソッド。

- @No__t_0 `MustOverride` (Visual Basic) 修飾子で宣言されたメソッド。

- @No__t_0 `Overridable` (Visual Basic) 修飾子で宣言されたメソッド。

- @No__t_0 `Overrides` (Visual Basic) 修飾子で宣言されたメソッド。

- @No__t_0 (`Declare` ステートメント Visual Basic) 修飾子で宣言されたメソッド。

## <a name="rule-description"></a>規則の説明
 メソッド本体で使用されていない非仮想メソッドのパラメーターを確認して、アクセスできなかった部分に対して正しくないことを確認します。 未使用のパラメーターを使用すると、メンテナンスとパフォーマンスのコストが発生します。

 この規則に違反すると、メソッドの実装のバグを指す場合があります。 たとえば、パラメーターは、メソッドの本体で使用されている必要があります。 旧バージョンとの互換性のためにパラメーターが存在する必要がある場合は、この規則の警告を非表示にします。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則違反を修正するには、使用されていないパラメーター (重大な変更) を削除するか、メソッド本体でパラメーターを使用します (非互換性の変更)。

## <a name="when-to-suppress-warnings"></a>警告を抑制する状況
 以前に出荷されたコードについては、この修正プログラムが互換性に影響する変更になるという警告を抑制するのは安全です。

## <a name="example"></a>例
 次の例は、2つのメソッドを示しています。 1つのメソッドが規則に違反し、もう一方のメソッドが規則を満たしています。

 [!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ReviewUnusedParameters/cs/FxCop.Usage.ReviewUnusedPerameters.cs#1)]

## <a name="related-rules"></a>関連規則
 [CA1811: 呼び出されていないプライベート コードを使用しません](../code-quality/ca1811-avoid-uncalled-private-code.md)

 [CA1812: インスタンス化されていない内部クラスを使用しないでください](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1804: 使用されていないローカルを削除します](../code-quality/ca1804-remove-unused-locals.md)
