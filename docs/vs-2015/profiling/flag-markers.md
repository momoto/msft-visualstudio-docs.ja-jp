---
title: フラグ マーカー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.flag
ms.assetid: f3ec919e-63e5-484b-adbf-8f0e79342e75
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e531d2d2a41cc9ceaa3b6ba39c6d77a166cfae83
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193690"
---
# <a name="flag-markers"></a>フラグ マーカー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

フラグ マーカーは、ある時点にアプリで何かが発生したことを表します。 フラグは、多様なアプリケーション イベントを表現することができます。 たとえば、特定の作業項目がスケジュールされていた時間や、例外がスローされた時間をフラグで示すことができます。 タスク並列ライブラリなどのランタイムでフラグを生成することもできます。  
  
## <a name="flag-importance"></a>フラグの重要度  
 フラグは重要度に応じて異なるサイズで表示されます。 他のマーカーと同様に、低、標準、高、致命的という重要度があります。  次の図は、重要度レベルごとのマーカーの外観です。  
  
 ![重要度マーカー (低、標準、高、致命的)](../profiling/media/cvmarkerimportance.png "CVMarkerImportance")  
フラグの重要度を示すマーカー  
  
## <a name="flag-category"></a>フラグのカテゴリ  
 フラグは、カテゴリに応じて 5 種類の色のいずれかで表示されます。 色が 6 種類以上ある場合、色は再利用されます。 色を選択することはできません。 他のマーカーと同様に、カテゴリには任意の整数を指定できます。 次の図は、最初の 5 つのカテゴリの色を示しています。  
  
 ![5 色のカテゴリ マーカー](../profiling/media/cvmarkercategory.png "CVMarkerCategory")  
カテゴリを示すマーカー  
  
## <a name="alerts"></a>アラート  
 アラートは、例外などの致命的なアプリケーション イベントを表す赤色のフラグです。  アラートは次のように表示されます。  
  
 ![コンカレンシー ビジュアライザーの警告マーカー](../profiling/media/cvmarkeralert.png "CVMarkerAlert")  
アラート マーカー  
  
## <a name="aggregation-flags"></a>集約フラグ  
 コンカレンシー ビジュアライザーで、複数のフラグが相互に近接しすぎて、個別に描画できないことがあります。 このような場合、基になるフラグを示す灰色の*集約フラグ*が表示されます。 それらのアイコンのいずれかにポインターを置くと、表現されている、基になるフラグの数がツールヒントに表示されます。 フラグを表示するには、ズームインします。 限界までズームインしてもなお集約フラグが表示される場合には、基になるフラグを[マーカー レポート](../profiling/markers-report.md)で確認できます。  
  
 集約フラグはさまざまなサイズで描画されます。 サイズは、集約の最も高い重要度フラグの重要度レベルによって変わります。 次の図は、集約フラグを重要度の昇順で示します。  
  
 ![4 レベルの重要度を示す集約フラグ](../profiling/media/cvmarkeraggregate.png "CVMarkerAggregate")  
重要度レベル別の集約フラグ  
  
## <a name="see-also"></a>関連項目  
 [コンカレンシー ビジュアライザー マーカー](../profiling/concurrency-visualizer-markers.md)   
 [コンカレンシー ビジュアライザー SDK](../profiling/concurrency-visualizer-sdk.md)
