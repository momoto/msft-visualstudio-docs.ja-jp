---
title: '方法: UML モデル内の変更に応答する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: f0300371-9cac-4def-a3f5-7d7b62dcd6f3
caps.latest.revision: 3
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9eaaa1406591bc950dbbf95aff8dcd732eef3448
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74293405"
---
# <a name="how-to-respond-to-changes-in-a-uml-model"></a>方法: UML モデル内で変更に応答する
Visual Studio の UML モデルで変更が生じたときに実行されるコードを作成できます。 このコードは、ユーザーが直接行った変更にも、他の Visual Studio 拡張機能による変更にも同様に応答します。 UML モデルをサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

> [!WARNING]
> これらの手法は、UML API ではサポートされていません。 将来のバージョンの Visual Studio では機能しなくなる可能性があります。

## <a name="see-also"></a>関連項目
 [UML モデルのイベントハンドラー内を移動](../modeling/navigate-the-uml-model.md)する[モデルの外部で変更を反映する](../modeling/event-handlers-propagate-changes-outside-the-model.md)[サンプル: ステレオタイプによる色](https://go.microsoft.com/fwlink/?LinkId=213841)