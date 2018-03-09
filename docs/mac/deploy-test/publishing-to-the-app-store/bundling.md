---
title: Agrupamento para Mac App Store
description: "Este guia ensina como agrupar um aplicativo Xamarin.Mac para publicação na Mac App Store."
ms.topic: article
ms.prod: xamarin
ms.assetid: 00a36d7c-937d-4657-bf6a-0de9684b8f94
ms.technology: xamarin-mac
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/14/2017
ms.openlocfilehash: e138fc1176c646a2e4e9caf94462028dd7c68e9f
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="bundle-for-mac-app-store"></a>Pacote para Mac App Store

Esta seção descreve as noções básicas da criação de um aplicativo para lançamento no Mac App Store usando o Visual Studio para Mac. Com base nos recursos adicionais (como acesso iCloud e notificações por push), outras instalações, que vão além do escopo deste artigo, podem ser necessárias.

> [!NOTE]
>  **Observação**: antes de iniciar esta seção, o desenvolvedor deve ter criado um Perfil de provisionamento de produção para compilar para a Mac App Store. Consulte as instruções anteriores neste documento sobre como criar os perfis de provisionamento necessários.

## <a name="code-signing-options"></a>Opções de assinatura de código

Altere **Configuração** para **Versão** antes de atualizar as opções de assinatura de código e empacotamento. O desenvolvedor precisa garantir que usem a **identidade** e o perfil de provisionamento criados acima quando assinarem o aplicativo para lançamento na App Store.

 [![Editar as opções de assinatura de código](bundling-images/config02.png "Editar as opções de assinatura de código")](bundling-images/config02-large.png)

Verifique se a opção de criar um pacote do instalador foi marcada nas configurações de **Build do Mac**:

[![Editar as opções de build](bundling-images/config03.png "Editar as opções de build")](bundling-images/config03-large.png)

## <a name="build"></a>Build

Antes de compilar, verifique se a configuração **Versão** foi selecionada. Quando o desenvolvedor compila o aplicativo, é solicitado a usar ambos os certificados:

 ![Permitir que o aplicativo use o certificado](bundling-images/image62.png "Permitir que o aplicativo use o certificado")

 ![Permitir que o aplicativo use o certificado](bundling-images/image63.png "Permitir que o aplicativo use o certificado")

Depois que o aplicativo é compilado, o desenvolvedor pode clicar com o botão direito no projeto e escolher **Abrir Pasta Recipiente** para localizar o arquivo do pacote (no diretório `bin/x86/AppStore` no exemplo mostrado abaixo).  Este arquivo de pacote inclui um instalador para o aplicativo que pode ser enviado para a Apple para inclusão na Mac App Store.

 ![Selecionar o pacote de build no Localizador](bundling-images/image64.png "Selecionar o pacote de build no Localizador")


## <a name="related-links"></a>Links relacionados

- [Instalação](/visualstudio/mac/installation/)
- [Amostra do Hello, Mac](~/mac/get-started/hello-mac.md)
- [Distribua aplicativos na Mac App Store](https://developer.apple.com/devcenter/mac/checklist/)
- [ID de Desenvolvedor e GateKeeper](https://developer.apple.com/resources/developer-id/)