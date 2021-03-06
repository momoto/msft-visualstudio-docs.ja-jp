---
title: マネージド コードの "マネージ最小規則" 規則セット
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 44a50c54-8dd3-42b2-8387-532a150e5a6c
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: efb282d8876d48d4f8e7eb81963719e2d14e5900
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72649256"
---
# <a name="managed-minimum-rules-rule-set-for-managed-code"></a>マネージド コードの "マネージ最小規則" 規則セット

マネージ最小規則は、潜在的なセキュリティホール、アプリケーションのクラッシュ、その他の重要な論理エラーやデザインエラーなど、コードの最も重大な問題に焦点を当てています。 この規則セットは、プロジェクト用に作成するカスタム規則セットに含めます。

|規則|説明|
|----------|-----------------|
|[CA1001](../code-quality/ca1001.md)|破棄可能なフィールドを所有する型は、破棄可能でなければなりません|
|[CA1821](../code-quality/ca1821.md)|空のファイナライザーを削除します|
|[CA2213](../code-quality/ca2213.md)|破棄可能なフィールドは破棄されなければなりません|
|[CA2231](../code-quality/ca2231.md)|オーバーライド `ValueType.Equals` で、演算子 equals をオーバーロードします|
