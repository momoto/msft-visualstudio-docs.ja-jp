---
title: IDebugObject::IsEqual |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf592fa83a18c47bf676b84073c0be0e4cb476e8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323582"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
このオブジェクトを持つオブジェクトを比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
[in][IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)と比較するオブジェクトを表すオブジェクト。

`pfIsEqual`\
[out]0 以外を返します (`TRUE`) のオブジェクトの値がそれ以外の場合は 0 を返します (`FALSE`)。

## <a name="return-value"></a>戻り値
 成功した場合、S_OK を返します。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>Remarks
 通常、このメソッドはによって表される値のアドレスを比較できる、`pObject`パラメーターとこの[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトは、アドレスが等しいかどうかは、オブジェクトを等しい。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)