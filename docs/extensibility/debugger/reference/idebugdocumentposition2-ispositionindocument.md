---
title: IDebugDocumentPosition2::IsPositionInDocument |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
helpviewer_keywords:
- IDebugDocumentPosition2::IsPositionInDocument
ms.assetid: d5cf57cb-b93b-4e1d-bec9-185f4fe8668d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab4792427a98f97fcd50d4b39c2bb332527a0942
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66333406"
---
# <a name="idebugdocumentposition2ispositionindocument"></a>IDebugDocumentPosition2::IsPositionInDocument
ドキュメントの位置が特定のドキュメントに含まれているかどうかを決定します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsPositionInDocument( 
   IDebugDocument2* pDoc
);
```

```csharp
int IsPositionInDocument( 
   IDebugDocument2 pDoc
);
```

## <a name="parameters"></a>パラメーター
`pDoc`\
[in][IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)を含んでいるドキュメントの候補を表すオブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは主にブレークポイントを設定に使用[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイス。 ドキュメントが読み込まれると、ブレークポイントの位置はこの位置がドキュメントに含まれているかどうかに呼び出されます。

## <a name="see-also"></a>関連項目
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)