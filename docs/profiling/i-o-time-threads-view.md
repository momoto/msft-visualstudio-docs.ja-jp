---
title: I/O 時間 (スレッド ビュー) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.io
helpviewer_keywords:
- Concurrency Visualizer, I/O time (Threads View)
ms.assetid: 0c4ec14d-d8dd-49c1-999c-dcbf4e8e1dc8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9d7ba29383ddddc02160967a90b56046128d2f19
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62995440"
---
# <a name="io-time-threads-view"></a>I/O 時間 (スレッド ビュー)
タイムライン内のこれらのセグメントは、I/O として分類されたブロック時間に関連付けられます。 つまり、スレッドは I/O 操作の完了を待ちます。 スレッドは API でブロックされている可能性があります。あるいは、コンカレンシー ビジュアライザーが I/O としてカウントしている I/O 関連のカーネル待機によりブロックされている可能性があります。 `CreateFile()`、`ReadFile()`、`WSARecv()` のような API がこのグループに属します。

## <a name="see-also"></a>関連項目
- [スレッド ビュー](../profiling/threads-view-parallel-performance.md)