---
title: '方法: プログラムによって Visio 図面に図形を追加します。'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], adding Visio shapes
- shapes [Office development in Visual Studio], adding Visio shapes
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e172ff57fb784d6ae768dde1e705ef645b3f9a9c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967521"
---
# <a name="how-to-programmatically-add-shapes-to-a-visio-document"></a>方法: プログラムによって Visio 図面に図形を追加します。
  ステンシルからマスターを取得し、図形をアクティブ ページにドロップすると、Microsoft Office Visio 図面に図形を追加できます。

 詳しくは、 [Microsoft.Office.Interop.Visio.Documents.Add](/office/vba/api/Visio.Documents.Add) メソッド、 [Microsoft.Office.Interop.Visio.Application.ActivePage](/office/vba/api/Visio.Application.ActivePage) プロパティ、 [Microsoft.Office.Interop.Visio.Page.Drop](/office/vba/api/Visio.Page.Drop) メソッドの VBA リファレンス ドキュメントをご覧ください。

## <a name="add-shapes-to-a-visio-document"></a>Visio 図面に図形を追加します。

### <a name="to-add-shapes-to-a-visio-document"></a>Visio 図面に図形を追加するには

- ドキュメントをアクティブにして、Documents.Masters コレクションからマスターを取得し、アクティブなドキュメントに図形をドロップします。 インデックスまたはマスターの名前を使用して、マスターを取得できます。

     次のコード例は、空の Visio 図面を作成し、 **[基本図形]** ステンシルをドッキングした状態で図面を開きます。 次に、このコードはいくつかの図形を取得し、それらをアクティブ ページにドロップします。

     [!code-csharp[Trin_VstcoreVisioAutomationAddIn#13](../vsto/codesnippet/CSharp/trin_vstcorevisioautomationaddin/ThisAddIn.cs#13)]
     [!code-vb[Trin_VstcoreVisioAutomationAddIn#13](../vsto/codesnippet/VisualBasic/trin_vstcorevisioautomationaddin/ThisAddIn.vb#13)]

## <a name="see-also"></a>関連項目
- [Visio ソリューション](../vsto/visio-solutions.md)
- [Visio オブジェクト モデルの概要](../vsto/visio-object-model-overview.md)
- [Visio 図形を操作します。](../vsto/working-with-visio-shapes.md)
- [方法: プログラムによってコピーして、Visio 図面に図形を貼り付けます](../vsto/how-to-programmatically-copy-and-paste-shapes-in-a-visio-document.md)
