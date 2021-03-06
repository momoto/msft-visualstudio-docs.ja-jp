---
title: n 層アプリケーションのデータセットにコードを追加する
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending DataSets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 0002339b0a1aa2200894d701f04f343193376c4b
ms.sourcegitcommit: 8589d85cc10710ef87e6363a2effa5ee5610d46a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807033"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>n 層アプリケーションのデータセットにコードを追加する

データセットの機能を拡張するには、データセットの部分クラスファイルを作成し、そのデータセットにコードを追加します ( *DatasetName*にコードを追加するのではありません)。データセットデザイナーファイル)。 部分クラスを使用すると、特定のクラスのコードを複数の物理ファイルに分割できます。 詳細については、「[部分](/dotnet/visual-basic/language-reference/modifiers/partial)クラスまたは[部分クラスとメソッド](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)」を参照してください。

データセットを定義するコードは、(型指定されたデータセット内の) データセット定義に変更が加えられるたびに生成されます。 このコードは、データセットの構成を変更するウィザードの実行中に変更を加えた場合にも生成されます。 データセットの再生成時にコードが削除されないようにするには、データセットの部分クラスファイルにコードを追加します。

既定では、データセットと TableAdapter コードを分離した後、結果は各プロジェクトの不連続クラスファイルになります。 元のプロジェクトには、TableAdapter コードを含む*DatasetName* (または*DatasetName.Designer.cs*) という名前のファイルがあります。 " **Dataset プロジェクト**" プロパティで指定されているプロジェクトには、 *DatasetName* (または*DatasetName.DataSet.Designer.cs*) という名前のファイルがあります。このファイルには、データセットコードが含まれています。

> [!NOTE]
> データセットと Tableadapter を分離すると ( **DataSet プロジェクト**プロパティを設定することによって)、プロジェクト内の既存の部分データセットクラスは自動的には移動されません。 既存のデータセット部分クラスは、手動でデータセット プロジェクトに移動する必要があります。

> [!NOTE]
> 検証コードを追加する必要がある場合、型指定されたデータセットは、<xref:System.Data.DataTable.ColumnChanging> および <xref:System.Data.DataTable.RowChanging> のイベントハンドラーを生成するための機能を提供します。 詳細については、「 [n 層データセットへの検証の追加](../data-tools/add-validation-to-an-n-tier-dataset.md)」を参照してください。

## <a name="to-add-code-to-datasets-in-n-tier-applications"></a>N 層アプリケーションのデータセットにコードを追加するには

1. *.Xsd*ファイルが含まれているプロジェクトを見つけます。

2. **.Xsd**ファイルを選択して、データセットを開きます。

3. コード (タイトルバーのテーブル名) を追加するデータテーブルを右クリックし、 **[コードの表示]** を選択します。

     部分クラスが作成され、コードエディターで開きます。

4. 部分クラス宣言内にコードを追加します。

     次の例は、NorthwindDataSet 内の顧客 Sdatatable にコードを追加する場所を示しています。

    ```vb
    Partial Public Class CustomersDataTable
        ' Add code here to add functionality
        ' to the CustomersDataTable.
    End Class
    ```

    ```csharp
    partial class CustomersDataTable
    {
        // Add code here to add functionality
        // to the CustomersDataTable.
    }
    ```

## <a name="see-also"></a>関連項目

- [n 層データ アプリケーションの概要](../data-tools/n-tier-data-applications-overview.md)
- [n 層アプリケーションの TableAdapters にコードを追加する](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [Tableadapter の作成および構成](create-and-configure-tableadapters.md)
- [階層更新の概要](hierarchical-update.md)
- [Visual Studio のデータセットツール](../data-tools/dataset-tools-in-visual-studio.md)
