---
title: '方法: 発行バージョンを設定、ClickOnce |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, setting publish version
- publishing, ClickOnce
- Publish Version property
ms.assetid: 06f15504-6385-40a6-b01d-cd90ca36dc73
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e2bd526203b777bafd77c79a4934d1f3e8754dee
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63406852"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>方法: ClickOnce の発行バージョンを設定する
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version`プロパティが公開するアプリケーションは更新プログラムとして扱うかどうかを決定します。 各時点のバージョンがインクリメントされます、アプリケーションは、更新プログラムとして発行されます。

 `Publish Version`でプロパティを設定することができます、**発行**のページ、**プロジェクト デザイナー**します。

> [!NOTE]
> 自動的にインクリメントするプロジェクトのオプションがある、`Publish Version`プロパティごとにアプリケーションを発行する。 このオプションは既定で有効にします。 詳細については、「[方法 :ClickOnce の発行バージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)」を参照してください。

### <a name="to-change-the-publish-version"></a>発行バージョンを変更するには

1. **ソリューション エクスプ ローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。

2. **発行**タブをクリックします。

3. **発行バージョン**フィールドに、インクリメント、**メジャー**、**マイナー**、**ビルド**、または**リビジョン**バージョン数値。

    > [!NOTE]
    > バージョン番号がデクリメントしないでください。そうする予期しない更新プログラムの動作と原因でした。

## <a name="see-also"></a>関連項目
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [方法: ClickOnce の発行バージョンを自動的にインクリメントする](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)
- [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行する](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)