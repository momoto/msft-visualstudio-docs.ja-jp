---
title: TASK_STATE_FAULTED フィールド |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_FAULTED field, Task class [.NET Framework debug engines]
ms.assetid: ced826ae-09a9-4acf-af00-a2343d396bb8
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d659d31de221d7a08ee85bee6350ade5c5a95808
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68176728"
---
# <a name="taskstatefaulted-field"></a>TASK_STATE_FAULTED フィールド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

タスクはハンドルされない例外が発生したために終了しました。  
  
 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>  
  
 **アセンブリ:** mscorlib (mscorlib.dll 内)  
  
 .NET Framework からこの内部メンバーにアクセスできないため、次の構文には共通中間言語 (CIL) が提供されます。  
  
## <a name="syntax"></a>構文  
  
```  
.field static assembly literal int32 TASK_STATE_FAULTED = int32(0x00400000)  
```  
  
## <a name="remarks"></a>Remarks  
 場合、 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md)フィールドには、この値が含まれています、<xref:System.Threading.Tasks.Task.Status%2A>プロパティが返す<xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName>します。  
  
## <a name="see-also"></a>関連項目  
 [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
