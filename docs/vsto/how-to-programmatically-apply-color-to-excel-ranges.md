---
title: '方法: プログラムによって Excel の範囲に色を適用します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- formatting [Office development in Visual Studio]
- color, Excel ranges
- ranges, applying color
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 56ecbfcdaf22132f63df1ecf5eadba97dee426af
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62817274"
---
# <a name="how-to-programmatically-apply-color-to-excel-ranges"></a>方法: プログラムによって Excel の範囲に色を適用します。
  セルの範囲内のテキストの色を適用するには、使用、<xref:Microsoft.Office.Tools.Excel.NamedRange>コントロールまたはネイティブな Excel 範囲オブジェクト。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>NamedRange コントロールを使用します。
 この例では、ドキュメント レベルのカスタマイズです。

### <a name="to-apply-color-to-a-namedrange-control"></a>NamedRange コントロールに色を適用するには

1. 作成、<xref:Microsoft.Office.Tools.Excel.NamedRange>セル A1 にあるコントロール。

     [!code-csharp[Trin_VstcoreExcelAutomation#65](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#65)]
     [!code-vb[Trin_VstcoreExcelAutomation#65](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#65)]

2. 内のテキストの色を設定、<xref:Microsoft.Office.Tools.Excel.NamedRange>コントロール。

     [!code-csharp[Trin_VstcoreExcelAutomation#66](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#66)]
     [!code-vb[Trin_VstcoreExcelAutomation#66](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#66)]

## <a name="use-native-excel-ranges"></a>ネイティブの Excel の範囲を使用して、

### <a name="to-apply-color-to-a-native-excel-range-object"></a>ネイティブな Excel 範囲オブジェクトに色を適用するには

1. セル A1 に範囲を作成し、テキストの色を設定します。

     [!code-csharp[Trin_VstcoreExcelAutomation#67](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#67)]
     [!code-vb[Trin_VstcoreExcelAutomation#67](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#67)]

## <a name="see-also"></a>関連項目
- [範囲を操作します。](../vsto/working-with-ranges.md)
- [NamedRange コントロール](../vsto/namedrange-control.md)
- [方法: プログラムによってブック内の範囲にスタイルを適用します。](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [方法: コード内でワークシートの範囲をプログラムで参照してください。](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [拡張オブジェクトを使用した Excel の自動化](../vsto/automating-excel-by-using-extended-objects.md)
- [Office ソリューションの省略可能なパラメーター](../vsto/optional-parameters-in-office-solutions.md)
