---
title: '方法: アプリケーション マニフェストおよび配置マニフェストに再署名 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Office applications, signing manifests
- deploying applications [ClickOnce], signing manifests
- deploying applications, signing manifests
- ClickOnce deployment, signing manifests
- Office development in Visual Studio, signing manifests
ms.assetid: d53bceb9-4d3b-4c22-b909-8f370e7231fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e934832f20ea7ab11484cdeb345f989aa842e06d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62928354"
---
# <a name="how-to-re-sign-application-and-deployment-manifests"></a>方法: アプリケーション マニフェストと配置マニフェストの再署名
Windows フォーム アプリケーション、Windows Presentation Foundation アプリケーション (xbap)、Office ソリューション用アプリケーション マニフェストの配置プロパティを変更したら、両方のアプリケーションを再署名する必要があり、配置マニフェストに、証明書。 このプロセスによって、改ざんされたファイルがエンド ユーザーのコンピューターにインストールされないようにすることができます。

 マニフェストを再署名が別のシナリオは、お客様が、アプリケーションに署名して、配置マニフェストに、独自の証明書です。

## <a name="re-sign-the-application-and-deployment-manifests"></a>アプリケーション マニフェストと配置マニフェストへの再署名
 この手順は、アプリケーション マニフェスト ファイルへの変更が既に行われたことを想定しています (*.manifest*)。 詳細については、「[方法 :展開のプロパティを変更する](https://msdn.microsoft.com/library/66052a3a-8127-4964-8147-2477ef5d1472)します。

#### <a name="to-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してマニフェストに、アプリケーションおよび配置を再署名するには

1. 開く、 **Visual Studio コマンド プロンプト**ウィンドウ。

2. マニフェスト ファイルに署名するが含まれるフォルダーにディレクトリを変更します。

3. アプリケーション マニフェスト ファイルの署名には、次のコマンドを入力します。 置換*ManifestFileName*マニフェスト ファイルと、拡張の名前に置き換えます。 置換*証明書*置換、証明書ファイルの相対パスまたは完全修飾パスで*パスワード*証明書のパスワードに置き換えます。

    ```cmd
    mage -sign ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドインによって、Windows フォーム アプリケーションでは、または Windows Presentation Foundation ブラウザー アプリケーションのアプリケーション マニフェストに署名するには、次のコマンドを実行できます。 Visual Studio によって作成された一時的な証明書は実稼働環境に展開するため推奨されません。

    ```cmd
    mage -sign WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -sign ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -sign WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

4. 更新し、前の手順のようにプレース ホルダー名を置き換えて、配置マニフェスト ファイルを署名するには、次のコマンドを入力します。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、更新、および Excel のアドインで、Windows フォーム アプリケーション、または Windows Presentation Foundation ブラウザー アプリケーションの配置マニフェストに署名するには、次のコマンドを実行できます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 必要に応じて、マスター展開マニフェストをコピー (*発行\\\<appname > .application*) バージョンの展開ディレクトリに (*publish\Application ファイル\\\<appname > _\<バージョン >*)。

## <a name="update-and-re-sign-the-application-and-deployment-manifests"></a>更新し、アプリケーション マニフェストと配置マニフェストに再署名
 この手順は、アプリケーション マニフェスト ファイルへの変更が既に行われたことを想定しています (*.manifest*) が、その他の更新されたファイルがあります。 ファイルが更新されると、ファイルを表すハッシュも更新する必要があります。

#### <a name="to-update-and-re-sign-the-application-and-deployment-manifests-with-mageexe"></a>Mage.exe を使用してマニフェストを更新し、アプリケーションおよび配置に再署名するには

1. 開く、 **Visual Studio コマンド プロンプト**ウィンドウ。

2. マニフェスト ファイルに署名するが含まれるフォルダーにディレクトリを変更します。

3. 削除、 *.deploy*ファイル拡張子のファイルからの出力フォルダー。

4. 更新されたファイル用の新しいハッシュで、アプリケーション マニフェストを更新して、アプリケーション マニフェスト ファイルに署名するには、次のコマンドを入力します。 置換*ManifestFileName*マニフェスト ファイルと、拡張の名前に置き換えます。 置換*証明書*置換、証明書ファイルの相対パスまたは完全修飾パスで*パスワード*証明書のパスワードに置き換えます。

    ```cmd
    mage -update ManifestFileName.manifest -CertFile Certificate -Password Password
    ```

     たとえば、アドインによって、Windows フォーム アプリケーションでは、または Windows Presentation Foundation ブラウザー アプリケーションのアプリケーション マニフェストに署名するには、次のコマンドを実行できます。 Visual Studio によって作成された一時的な証明書は実稼働環境に展開するため推奨されません。

    ```cmd
    mage -update WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

5. 更新し、前の手順のようにプレース ホルダー名を置き換えて、配置マニフェスト ファイルを署名するには、次のコマンドを入力します。

    ```cmd
    mage -update DeploymentManifest -appmanifest ApplicationManifest -CertFile Certificate -Password Password
    ```

     たとえば、更新、および Excel のアドインで、Windows フォーム アプリケーション、または Windows Presentation Foundation ブラウザー アプリケーションの配置マニフェストに署名するには、次のコマンドを実行できます。

    ```cmd
    mage -update WindowsFormsApplication1.application -appmanifest WindowsFormsApplication1.exe.manifest -CertFile ..\WindowsFormsApplication1_TemporaryKey.pfx
    mage -update ExcelAddin1.vsto -appmanifest ExcelAddin1.dll.manifest -CertFile ..\ExcelAddIn1_TemporaryKey.pfx
    mage -update WpfBrowserApplication1.xbap -appmanifest WpfBrowserApplication1.exe.manifest -CertFile ..\WpfBrowserApplication1_TemporaryKey.pfx
    ```

6. 追加、 *.deploy*点を除いて、アプリケーションおよび配置マニフェスト ファイルに、ファイルにファイル拡張子。

7. 必要に応じて、マスター展開マニフェストをコピー (*発行\\\<appname > .application*) バージョンの展開ディレクトリに (*publish\Application ファイル\\\<appname > _\<バージョン >*)。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
- [ClickOnce アプリケーションのコード アクセス セキュリティ](../deployment/code-access-security-for-clickonce-applications.md)
- [ClickOnce と Authenticode](../deployment/clickonce-and-authenticode.md)
- [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)
- [方法: ClickOnce のセキュリティ設定を有効にします。](../deployment/how-to-enable-clickonce-security-settings.md)
- [方法: ClickOnce アプリケーションのセキュリティ ゾーンを設定します。](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)
- [方法: ClickOnce アプリケーションのカスタム アクセス許可の設定](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)
- [方法: 制限されたアクセス許可を使用して ClickOnce アプリケーションをデバッグします。](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)
- [方法: ClickOnce アプリケーションのクライアント コンピューターに信頼された発行元を追加します。](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)
- [方法: ClickOnce 信頼プロンプトの動作を構成する](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)