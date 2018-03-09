---
title: "Configuração personalizada do vinculador"
ms.topic: article
ms.prod: xamarin
ms.assetid: F8A99E3F-2197-4399-AC81-F1DBAB5729C9
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 03/22/2017
ms.openlocfilehash: d5470dfc314677dbe558bca2f3ddfa107354c752
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="custom-linker-configuration"></a>Configuração personalizada do vinculador

Se o conjunto padrão de opções não for o suficiente, faça o processo de vinculação com um arquivo XML que descreve o que você deseja do vinculador.

Você pode fornecer definições extras para o vinculador para garantir que o tipo, os métodos e/ou os campos não sejam eliminados do seu aplicativo. Em seu próprio código, o modo preferido é usar o atributo personalizado `[Preserve]`, conforme discutido nos guias [Vinculação no iOS](~/ios/deploy-test/linker.md) e [Vinculação no Android](~/android/deploy-test/linker.md).
No entanto, se você precisar de algumas definições dos assemblies do SDK ou do produto, a melhor solução para você poderá ser usar um arquivo XML (em vez de adicionar código que garantirá que o vinculador não eliminará itens de que você precise).

Para fazer isso, você define um arquivo XML com o elemento de nível superior <linker>, que contém nós de *assembly* que, por sua vez, contêm nós de *tipo* que, por sua vez, contêm nós de *método* e de *campo*.

Quando você tiver esse arquivo de descrição de vinculador, adicione-o ao seu projeto e:

-  **Para o Android**: defina a **Ação de Build** para **LinkDescription**
-  **Para o iOS**: defina a **Ação de Build** para **LinkDescription**


O exemplo a seguir mostra a aparência do arquivo XML:

```xml
<linker>
        <assembly fullname="mscorlib">
                <type fullname="System.Environment">
                        <field name="mono_corlib_version" />
                        <method name="get_StackTrace" />
                </type>
        </assembly>
        <assembly fullname="My.Own.Assembly">
                <type fullname="Foo" preserve="fields">
                        <method name=".ctor" />
                </type>
                <type fullname="Bar">
                        <method signature="System.Void .ctor(System.String)" />
                        <field signature="System.String _blah" />
                </type>
                <namespace fullname="My.Own.Namespace" />
                <type fullname="My.Other*" />
        </assembly>
</linker>
```

No exemplo acima, o vinculador lerá e aplicará as instruções aos assemblies `mscorlib.dll` (fornecido com o Mono para Android) e `My.Own.Assembly` (código do usuário).

A primeira seção, para `mscorlib.dll`, garantirá que o tipo `System.Environment` preservará seu campo denominado `mono_corlib_version` e seu método `get_StackTrace`.
Observe que os nomes de método getter e/ou setter devem ser usados, pois o vinculador funciona em IL e não entende propriedades do C#.

A segunda seção, para `My.Own.Assembly.dll`, garantirá que o tipo `Foo` preservará todos os seus campos (ou seja, o atributo `preserve="fields"`) e todos os seus construtores (ou seja, todos os métodos chamados `.ctor` em IL). O tipo `Bar` preservará assinaturas específicas (não nomes) para um construtor (que aceita um único parâmetro de cadeia de caracteres) e para um campo de cadeia de caracteres específica `_blah`.
O namespace `My.Own.Namespace` preservará todos os tipos que ele contém.
Por fim, qualquer tipo cujo nome completo (incluindo o namespace) corresponda ao padrão de curinga "My.Other\*" preservará todos os seus campos e métodos. O caractere curinga `*` pode ser incluído várias vezes dentro de um padrão "tipo nomecompleto".



## <a name="related-links"></a>Links relacionados

- [Vinculação no iOS](~/ios/deploy-test/linker.md)
- [Vinculação no Android](~/android/deploy-test/linker.md)