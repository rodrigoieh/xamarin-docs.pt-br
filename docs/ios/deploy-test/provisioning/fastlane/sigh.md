---
title: "fastlane para iOS – sigh"
ms.topic: article
ms.prod: xamarin
ms.assetid: 92B35AB1-7AB7-3D3B-DB31-CC971E0B43AE
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: 3d80a0ab5583231f95241fb8d4f6e339e44a84ca
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="fastlane-for-ios--sigh"></a>fastlane para iOS – sigh

> [!IMPORTANT]
> O fastlane recomenda o uso de [`match`](~/ios/deploy-test/provisioning/fastlane/match.md) para gerar e manter perfis de provisionamento. Use o Sigh diretamente apenas se você deseja controle total e sabe o suficiente sobre a assinatura de código.

## <a name="overview"></a>Visão geral

Tradicionalmente, o provisionamento do dispositivo é executado por cada membro de uma equipe de desenvolvimento pelo Xcode ou no Portal do desenvolvedor da Apple. Ele consiste em várias etapas:

- Solicitando um certificado de desenvolvimento
- Adicionando um dispositivo ao portal
- Criando uma ID do aplicativo
- Criando um perfil de provisionamento
- Baixando Perfis e Certificados

Cada uma dessas etapas contém variáveis que precisam ser resolvidas e que dependem do tipo de aplicativo que você está desenvolvendo. Mais informações sobre as etapas necessárias para configurar um dispositivo para desenvolvimento manual ou usando Xcode podem ser encontradas no guia [Provisionamento de dispositivo](~/ios/get-started/installation/device-provisioning/index.md).

Este guia apresenta as ferramentas do Fastlane como uma alternativa ao uso do Xcode e explica o seguinte:

- [O que é o sigh?](#whatissigh)
- [Criando uma ID do aplicativo](#appid)
- [Adicionando novos dispositivos](#newdevices)
- [Uso do sigh](#using)
- [Opções adicionais](#options)

> [!NOTE]
> Se houver uma ID do aplicativo existente que corresponda à ID de pacote do seu aplicativo e se o dispositivo existir no portal do desenvolvedor, você poderá ignorar as etapas em [Criar uma ID do aplicativo](#appid) e [Adicionar um dispositivo](#newdevices). Nesse caso, vá direto para [Uso do sigh](#using) para começar.

## <a name="installation"></a>Instalação

Para saber mais sobre como instalar o fastlane, consulte o guia Introdução ao [fastlane](~/ios/deploy-test/provisioning/fastlane/index.md#Installation).

<a name="whatissigh" />

## <a name="what-is-sigh"></a>O que é o sigh

O sigh fornece uma interface de terminal que permite que você crie e renove perfis de provisionamento para todas as configurações: Desenvolvimento, Distribuição de loja de aplicativos, Distribuição Ad Hoc e Distribuição corporativa. Além disso, ele fornece uma maneira simples de baixar e reparar os perfis de provisionamento.

<a name="appid" />

## <a name="creating-an-app-id"></a>Criando uma ID do aplicativo

Uma ID do aplicativo pode ser criada com o seguinte comando:

    fastlane produce -u your@appleid.com -a com.company.appname --skip_itc

Em que `com.company.appname` é a ID do pacote do aplicativo, que está localizada no arquivo Info.plist do aplicativo do Xamarin.iOS, conforme ilustrado abaixo:

[ ![](sigh-images/fastlane-image5.png "O arquivo Info.plist do aplicativo Xamarin.iOS")](sigh-images/fastlane-image5.png)

A ID do aplicativo exclusiva deve ser uma cadeia de caracteres de estilo DNS reversa. Depois de ter criado a ID, crie um lembrete sobre ela, pois você precisará usá-la quando for usar o Sigh posteriormente neste guia.

Se o aplicativo precisar ser criado no [iTunes Connect](~/ios/deploy-test/app-distribution/app-store-distribution/itunesconnect.md), remova o sinalizador `--skip_itc` do comando acima.

<a name="newdevices" />

## <a name="adding-new-devices"></a>Adicionando novos dispositivos

Para adicionar um único dispositivo ao Portal do desenvolvedor da linha de comando, digite o seguinte comando:

```bash
fastlane run register_device name:"Adam iPhone" udid:"abcdeg1234567"
```

Para adicionar mais de um dispositivo, use o comando `register_devices`:

```bash
    register_devices(
        devices: {
            "iPhone 6" => "1234567890123456789012345678901234567890",
            "iPad Air 2" => "abcdefghijklmnopqrstvuwxyzabcdefghijklmn"
         }
    )
```

<a name="using" />

## <a name="using-sigh"></a>Uso do sigh

Para começar a usar o utilitário Sigh, digite o seguinte comando no seu terminal:

```bash
fastlane sigh
```

Por padrão, isso criará um perfil de provisionamento de [distribuição da loja de aplicativo](~/ios/deploy-test/app-distribution/app-store-distribution/index.md). Para configurar seu dispositivo para desenvolvimento, passe o sinalizador `--development`:

```bash
fastlane sigh --development
```

Insira seu nome de usuário da Apple ID quando solicitado pelo Fastlane. Também pode ser solicitada a senha se esta for a primeira vez que você estiver usando o Fastlane. Caso contrário, ele coletará a variável de ambiente de senha do conjunto de chaves.

Se sua Apple ID estiver conectada a várias equipes, elas serão exibidas aqui. Selecione o número que corresponde à equipe que você deseja usar:

[ ![](sigh-images/fastlane-image2.png "Selecione a equipe que você deseja usar")](sigh-images/fastlane-image2.png)

A ID da equipe também pode ser passada para a CLI do seguinte modo:

```bash
fastlane sigh -l 2TU993NY9J
```

Insira a [ID do aplicativo](#appid) do seu aplicativo. Lembre-se de que ela deve corresponder ao identificador de pacote no Info.plist do seu aplicativo.

Todos os dispositivos conectados à sua conta serão adicionados ao seu perfil de provisionamento.

O fastlane, então, criará, baixará e instalará o perfil de provisionamento para você.

Se procurar a Central de desenvolvedores, você poderá exibir o perfil de provisionamento recém-criado, conforme ilustrado abaixo:

[ ![](sigh-images/fastlane-image10.png "Exiba o perfil de provisionamento recém-criado")](sigh-images/fastlane-image10.png)

O sigh armazenará os perfis de provisionamento na pasta atual, por padrão. Para alterar o diretório de saída, edite o `output_path` ou faça o seguinte:

```bash
fastlane sigh -o "~/Library/MobileDevice/Provisioning Profiles"
```

<a name="options" />

## <a name="sigh-additional-options"></a>Opções adicionais do sigh

As opções a seguir podem ser usadas para dar suporte adicional ao usar o Sigh:

- Para baixar todos os perfis de provisionamento, use:

    ````bash
    fastlane sigh download_all
    ```

- To use a specific signing identity for your provisioning profile use:

    ```bash
    fastlane sigh -c "Amy cert"
    ```
    
    Where `Amy cert` is the Code Signing Identity name.


## Related Links

- [fastlane - sigh](https://github.com/fastlane/fastlane/tree/master/sigh#readme)