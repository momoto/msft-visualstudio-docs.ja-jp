---
title: VSTextView オブジェクト |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSTextView
helpviewer_keywords:
- VSTextView object, reference
- views [Visual Studio SDK], reference
ms.assetid: 78272ddc-9718-4c65-a94e-a44a2e8d54f4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 927bbee8bde62ff24396ea7b50e55e901b8cff06
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189005"
---
# <a name="vstextview-object"></a>VSTextView オブジェクト

テキストビューは、テキストバッファーの Unicode テキストをユーザーが表示および編集できるウィンドウです。 基本的に、ビューは、ほとんどのユーザーがエディターとして参照します。 ビューは、さまざまなテキストレイヤー (右端での折り返し、アウトラインテキストなど) によってバッファーから分離されているため、ビューはバッファー内のテキストを正確に表現するとは限りません。 テキストビューの詳細については、「[従来の API を使用したテキストビューへのアクセス](/visualstudio/extensibility/accessing-thetext-view-by-using-the-legacy-api?view=vs-2015)」を参照してください。

次の表は、<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> オブジェクト内のインターフェイスを示しています。

|Interface|説明|
|---------------|-----------------|
|[IDropSource](/windows/desktop/api/oleidl/nn-oleidl-idropsource)|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IDropTarget>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|標準 OLE インターフェイス。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCompoundAction>|複合アクション (つまり、1つの元に戻す/やり直し単位でグループ化されたアクション) の作成を有効にします。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|ビューを管理およびアクセスするための基本的なメソッドを提供します。 `IVsTextView` がスレッドセーフではありません。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|ウィンドウペインを作成および管理します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|テキストレイヤーと対話します。|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsThreadSafeTextView>|別のスレッドからビューに対して操作を実行します。|

## <a name="see-also"></a>関連項目

- [図形の編集](https://www.microsoft.com/download/details.aspx?id=55984)
- [VSTextBuffer オブジェクト](../extensibility/vstextbuffer-object.md)