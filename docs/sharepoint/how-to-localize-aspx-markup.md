---
title: '方法: ASPX マークアップのローカライズ |Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- localizing XML [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, localizing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4cd3c17a9e771ad9a1aee7526f24e3a8282f208d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443102"
---
# <a name="how-to-localize-aspx-markup"></a>方法: ASPX マークアップをローカライズします。
  [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] (.aspx) ページは、通常のハード コーディングされた文字列値を使用します。 これらの文字列をローカライズするには、それらをローカライズされたリソースを参照する式に置き換えます。

## <a name="localize-aspx-markup"></a>ASPX マークアップをローカライズします。

#### <a name="to-localize-aspx-markup"></a>ASPX マークアップをローカライズするには

1. 別のリソース ファイルを追加します。 既定の言語と各ローカライズ言語。

     マークアップとコードではなくのみをローカライズする場合は、グローバル リソース ファイル プロジェクト項目を追加します。 コードとマークアップをローカライズする場合は、リソース ファイル プロジェクト項目を追加します。

    1. グローバル リソース ファイルを追加する**ソリューション エクスプ ローラー**、SharePoint プロジェクト項目のショートカット メニューを開き、選択し、**追加** > **新しい項目の**します。 SharePoint で**2010**ノードを選択して、**グローバル リソース ファイル**テンプレート。

    2. リソース ファイルを追加する**ソリューション エクスプ ローラー**、SharePoint プロジェクト項目のショートカット メニューを開き、選択し、**追加** > **新しい項目の**します。 いずれかで、 **Visual Basic**または**Visual c#** ノードを選択して、**リソース ファイル**テンプレート。

    > [!NOTE]
    > 展開の種類プロパティを有効にする SharePoint プロジェクト アイテムにリソース ファイルを追加してください。 このプロパティは、後で必要になります。 場合は、ソリューションには、SharePoint プロジェクト アイテムがあるない、空の SharePoint プロジェクトの追加し、その既定値を削除*Elements.xml*ファイル。

2. 既定の言語リソース ファイルの名前が付いた任意の *.resx* (MyAppResources.resx など) の拡張機能。 ローカライズされたリソース ファイルごとに、同じ基本名を使用して、カルチャ[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]します。 たとえば、リソースのローカライズ、ドイツ語の名前*MyAppResources.de」という*します。

3. 値を変更、**展開の種類**プロパティには、各リソース ファイルの**AppGlobalResource**にサーバーの App_GlobalResources フォルダーに展開することがあります。

4. ASPX マークアップに加えてコードをローカライズするリソースを使用する場合の値を受け入れ、**ビルド アクション**プロパティとして各ファイルの**埋め込まれたリソース**します。 マークアップのローカライズにのみ、リソース ファイルを使用する場合は、ファイルのプロパティの値を必要に応じて変更できます**コンテンツ**します。 詳細については、次を参照してください。[ローカライズ SharePoint ソリューション](../sharepoint/localizing-sharepoint-solutions.md)します。

5. 各リソース ファイルを開き、各ファイルに同じ文字列 Id を使用して、ローカライズされた文字列を追加します。

6. [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ASPX ページまたはコントロールのマークアップは、次の形式を使用する値でハードコーディングされた文字列を置き換えます。

    ```aspx-csharp
    <%$Resources:Resource File Name, String ID%>
    ```

     などのアプリケーション ページ上のラベル コントロールのテキストをローカライズする次のように変更します。

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="Label text"></asp:Label>
    </asp:Content>
    ```

     から

    ```aspx-csharp
    <asp:Content ID="Main" ContentPlaceHolderID="PlaceHolderMain" runat="server">
    <asp:Label ID="lbl" runat="server" Text="<%$Resources:MyAppResources,String1%>"></asp:Label>
    </asp:Content>
    ```

7. 選択、 **F5**キー、アプリケーションをビルドして実行します。

8. SharePoint で、表示言語を既定の言語から変更します。

     ローカライズされた文字列がアプリケーションに表示されます。 ローカライズされたリソースを表示するには、リソース ファイルのカルチャに対応する Language Pack が SharePoint サーバーにインストールされている必要があります。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションをローカライズします。](../sharepoint/localizing-sharepoint-solutions.md)
- [方法: フィーチャーをローカライズします。](../sharepoint/how-to-localize-a-feature.md)
- [方法: リソース ファイルを追加します。](../sharepoint/how-to-add-a-resource-file.md)
- [方法: コードをローカライズします。](../sharepoint/how-to-localize-code.md)
