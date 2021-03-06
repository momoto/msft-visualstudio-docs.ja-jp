---
title: 従来の言語サービスでのメンバー補完 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2c969b0f857e45279488d9ba667b431064375da6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349308"
---
# <a name="member-completion-in-a-legacy-language-service"></a>従来の言語サービスでのメンバー補完

IntelliSense メンバー入力候補は、クラス、構造体、列挙型、または名前空間などの特定のスコープの可能なメンバーの一覧を表示するツールヒント。 たとえば、c# の場合は、ユーザーが"this"に続けて、ピリオドを入力クラスまたは現在のスコープでの構造体のすべてのメンバーの一覧が含まれる場合ユーザーが選択できる一覧。

Managed package framework (MPF) ツール ヒントおよび; ツール ヒントの一覧を管理するためのサポートを提供しますために必要なすべてが、一覧に表示されるデータを提供するためにパーサーからの協力します。

従来の言語サービスは、VSPackage の一部として実装されますが、言語サービスの機能を実装する新しい方法は MEF 拡張機能を使用します。 詳細については、次を参照してください。[エディターと言語サービス拡張](../../extensibility/extending-the-editor-and-language-services.md)します。

> [!NOTE]
> 新しいエディターの API をできるだけ早く使用を開始することをお勧めします。 言語サービスのパフォーマンスを向上させる、エディターの新機能を活用することができます。

## <a name="how-it-works"></a>しくみ

MPF クラスを使用してメンバーの一覧が表示される 2 つの方法は、次のように。

- 識別子の上またはメンバー入力候補の文字の後にキャレットを配置し、選択**メンバーの一覧**から、 **IntelliSense**メニュー。

- <xref:Microsoft.VisualStudio.Package.IScanner>スキャナーは、メンバー入力候補の文字を検出し、トークンのトリガーを設定[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)その文字。

メンバー入力候補の文字は、クラス、構造体、列挙体のメンバーが次のことを示します。 たとえば、c# または Visual Basic でメンバー入力候補の文字は、 `.`、C++ では、文字ではいずれかを`.`または`->`します。 メンバー選択文字がスキャンされたときに、トリガーの値が設定されます。

### <a name="the-intellisense-member-list-command"></a>IntelliSense のメンバーの一覧表示コマンド

<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>コマンドへの呼び出しを開始する、<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッドを<xref:Microsoft.VisualStudio.Package.Source>クラスおよび<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッドを呼び出す、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド パーサーの解析の理由で[ParseReason.DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>).

パーサーは、下、または現在の位置の直前に、トークンと同様に、現在の位置のコンテキストを指定します。 このトークンに基づき、宣言の一覧が表示されます。 たとえば、c# でクラスのメンバーと選択にキャレットを配置する場合**メンバーの一覧**クラスのすべてのメンバーの一覧を取得します。 オブジェクト変数に続くピリオドの後にキャレットを配置する場合は、オブジェクトが表すクラスのすべてのメンバーの一覧を取得します。 メンバーの一覧が表示されるときにメンバーのキャレットが置かれている場合は、キャレットの一覧でいずれかであるメンバーで置き換えるリストからメンバーを選択するに注意してください。

### <a name="the-token-trigger"></a>トークンのトリガー

[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)トリガーへの呼び出しを開始する、<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッドを<xref:Microsoft.VisualStudio.Package.Source>クラスおよび<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>メソッド、さらに、パーサーの解析の理由を呼び出す[ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)します。 トークンのトリガーにも含まれている場合、 [TokenTriggers.MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>)フラグは、解析理由は、 [ParseReason.MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)、結合するメンバーの選択と中かっこが強調表示.

パーサーは、現在のコンテキストを指定します。 どのようなメンバーの文字を選択する前に入力したと配置します。 この情報からは、パーサーは、要求されたスコープのすべてのメンバーの一覧を作成します。 この宣言の一覧が格納されている、<xref:Microsoft.VisualStudio.Package.AuthoringScope>オブジェクトから返される、<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>メソッド。 すべての宣言が返された場合は、メンバー入力候補のツール ヒントが表示されます。 ツール ヒントがのインスタンスによって管理されている、<xref:Microsoft.VisualStudio.Package.CompletionSet>クラス。

## <a name="enable-support-for-member-completion"></a>メンバー入力候補のサポートを有効にします。

必要があります、 `CodeSense` IntelliSense の操作をサポートするために、レジストリ エントリが 1 に設定します。 渡される名前付きパラメーターを使用してこのレジストリ エントリを設定することができます、<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>言語パッケージに関連付けられているユーザーの属性。 言語サービスのクラスからは、このレジストリ エントリの値の読み取り、<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>プロパティを<xref:Microsoft.VisualStudio.Package.LanguagePreferences>クラス。

スキャナーがトークンのトリガーを返す場合[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)、メンバー入力候補の一覧を表示し、パーサーは、宣言の一覧を返します。

## <a name="support-member-completion-in-the-scanner"></a>スキャナーのサポート メンバー入力候補

スキャナーは、メンバー入力候補の文字を検出し、トークンのトリガーを設定することである必要があります[TokenTriggers.MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)その文字が解析されます。

### <a name="scanner-example"></a>スキャナーの例

メンバー入力候補の文字を検出し、適切な設定の簡略化された例を次に示します<xref:Microsoft.VisualStudio.Package.TokenTriggers>フラグ。 この例では、例示を目的としてのみです。 スキャナーにメソッドが含まれていると想定して`GetNextToken`を識別し、行のテキストからトークンを返します。 適切な種類の文字が認識されるたびに、コード例は単純に、トリガーを設定します。

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char memberSelectChar = '.';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (c == memberSelectChar)
                {
                        tokenInfo.Trigger |= TokenTriggers.MemberSelect;
                }
            }
            return foundToken;
        }
    }
}
```

## <a name="support-member-completion-in-the-parser"></a>パーサーのサポート メンバー入力候補

メンバー入力候補、<xref:Microsoft.VisualStudio.Package.Source>クラスが呼び出す、<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>メソッド。 派生したクラスの一覧を実装する必要があります、<xref:Microsoft.VisualStudio.Package.Declarations>クラス。 参照してください、<xref:Microsoft.VisualStudio.Package.Declarations>クラスの詳細については、メソッドを実装する必要があります。

パーサーが呼び出された[ParseReason.MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>)または[ParseReason.MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>)メンバー選択文字は型指定されています。 指定された場所、<xref:Microsoft.VisualStudio.Package.ParseRequest>メンバーは、文字を選択した後すぐにオブジェクトをします。 パーサーは、特定の時点で、ソース コード、メンバー リストに含まれるすべてのメンバーの名前を収集する必要があります。 パーサーは、ユーザーがメンバー選択文字に関連付けられたスコープを決定するのには、現在の行を解析する必要があります。

メンバーの文字を選択する前に、このスコープは、識別子の型に基づきます。 たとえば、c# の場合は、メンバー変数を指定`languageService`の型を持つ`LanguageService`入力、 **languageService します。** すべてのメンバーの一覧を作成、`LanguageService`クラス。 C# でも入力**これです。** 現在のスコープ内のクラスのすべてのメンバーの一覧を生成します。

### <a name="parser-example"></a>パーサーの使用例

次の例では、設定する方法の 1 つ、<xref:Microsoft.VisualStudio.Package.Declarations>一覧。 このコードには、パーサーは宣言を構築し、呼び出すことによって、一覧に追加しますが前提としています、`AddDeclaration`メソッドを`TestAuthoringScope`クラス。

```csharp
using System.Collections;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclaration
    {
        public string Name;            // Name of declaration
        public int     TypeImageIndex; // Glyph index
        public string Description;     // Description of declaration

        public TestDeclaration(string name, int typeImageIndex, string description)
        {
            this.Name = name;
            this.TypeImageIndex = typeImageIndex;
            this.Description = description;
        }
    }

    //===================================================
    internal class TestDeclarations : Declarations
    {
        private ArrayList declarations;

        public TestDeclarations()
            : base()
        {
            declarations = new ArrayList();
        }

        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        //////////////////////////////////////////////////////////////////////
        // Declarations of class methods that must be implemented.
        public override int GetCount()
        {
            // Return the number of declarations to show.
            return declarations.Count;
        }

        public override string GetDescription(int index)
        {
            // Return the description of the specified item.
            string description = "";
            if (index >= 0 && index < declarations.Count)
            {
                description = ((TestDeclaration)declarations[index]).Description;
            }
            return description;
        }

        public override string GetDisplayText(int index)
        {
            // Determine what is displayed in the tool tip list.
            string text = null;
            if (index >= 0 && index < declarations.Count)
            {
                text = ((TestDeclaration)declarations[index]).Name;
            }
            return text;
        }

        public override int GetGlyph(int index)
        {
            // Return index of image to display next to the display text.
            int imageIndex = -1;
            if (index >= 0 && index < declarations.Count)
            {
                imageIndex = ((TestDeclaration)declarations[index]).TypeImageIndex;
            }
            return imageIndex;
        }

        public override string GetName(int index)
        {
            string name = null;
            if (index >= 0 && index < declarations.Count)
            {
                name = ((TestDeclaration)declarations[index]).Name;
            }
            return name;
        }
    }

    //===================================================
    public class TestAuthoringScope : AuthoringScope
    {
        private TestDeclarations declarationsList;

        public void AddDeclaration(TestDeclaration declaration)
        {
            if (declaration != null)
            {
                if (declarationsList == null)
                {
                    declarationsList = new TestDeclarations();
                }
                declarationsList.AddDeclaration(declaration);
            }
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return declarationsList;
        }

        /////////////////////////////////////////////////
        // Remainder of AuthoringScope methods not shown.
        /////////////////////////////////////////////////
    }

    //===================================================
    class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            TestAuthoringScope scope = new TestAuthoringScope();
            if (req.Reason == ParseReason.MemberSelect ||
                req.Reason == ParseReason.MemberSelectAndHighlightBraces)
            {
                // Gather list of declarations based on what the user
                // has typed so far. In this example, this list is an array of
                // MemberDeclaration objects (a helper class you might implement
                // to hold member declarations).
                // How this list is gathered is dependent on the parser
                // and is not shown here.
                MemberDeclarations memberDeclarations;
                memberDeclarations = GetDeclarationsForScope();

                // Now populate the Declarations list in the authoring scope.
                // GetImageIndexBasedOnType() is a helper method you
                // might implement to convert a member type to an index into
                // the image list returned from the language service.
                foreach (MemberDeclaration dec in memberDeclarations)
                {
                    scope.AddDeclaration(new TestDeclaration(
                                             dec.Name,
                                             GetImageIndexBasedOnType(dec.Type),
                                             dec.Description));
                }
            }
            return scope;
        }
    }
}
```