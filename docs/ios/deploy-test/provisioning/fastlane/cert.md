---
title: "fastlane para iOS – cert"
ms.topic: article
ms.prod: xamarin
ms.assetid: 92B35AB1-7AB7-3D3B-DB31-CC971E0B43AE
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: b98375f8a526cd08f7d11f4ea6bb3498db87009c
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="fastlane-for-ios--cert"></a>fastlane para iOS – cert

> [!IMPORTANT]
> O fastlane recomenda o uso da ferramenta [`match`](~/ios/deploy-test/provisioning/fastlane/match.md) para gerar e manter certificados. Use `cert` diretamente apenas se você deseja controle total e sabe o suficiente sobre a assinatura de código. Use esta ação para baixar a identidade de assinatura de código mais recente.

## <a name="overview"></a>Visão geral

Tradicionalmente, o provisionamento do dispositivo é executado por cada membro de uma equipe de desenvolvimento pelo Xcode ou no Portal do desenvolvedor da Apple. Ele consiste em várias etapas:

- Solicitando um certificado de desenvolvimento
- Adicionando um dispositivo ao portal
- Criando uma ID do aplicativo
- Criando um perfil de provisionamento
- Baixando perfis e certificados

Cada uma dessas etapas contém variáveis que precisam ser resolvidas e que dependem do tipo de aplicativo que você está desenvolvendo. Mais informações sobre as etapas necessárias para configurar um dispositivo para desenvolvimento manual ou usando Xcode podem ser encontradas no guia [Provisionamento de dispositivo](~/ios/get-started/installation/device-provisioning/index.md).

Este guia apresenta as ferramentas do Fastlane como uma alternativa ao uso do Xcode e explica o seguinte:

- [O que é certificado?](#whatiscert)
- [Usando certificados](#using)
- [Opções adicionais](#options)

## <a name="installation"></a>Instalação

Para saber mais sobre como instalar e atualizar o fastlane, veja o guia Introdução ao [fastlane](~/ios/deploy-test/provisioning/fastlane/index.md#Installation).

<a name="whatiscert" />

## <a name="what-is-cert"></a>O que é certificado?

O cert fornece uma interface de terminal que cria novas identidades de assinatura de código (geralmente conhecidas como um _certificado_ de desenvolvedor) para ambientes de desenvolvimento e distribuição.

<a name="using" />

## <a name="using-cert"></a>Usando certificados

Para usar o utilitário de certificado, digite o seguinte comando no terminal CLI:

    fastlane cert

Por padrão, isso criará um certificado de distribuição. Para criar um certificado de desenvolvimento, passe o sinalizador `--development`:

    fastlane cert --development

O cert solicitará sua Apple ID e senha, então insira:

[ ![](cert-images/fastlane-image1.png "O cert solicitará sua Apple ID e senha")](cert-images/fastlane-image1.png)

> [!IMPORTANT]
> Na primeira vez em que a senha for inserida, ela será salva no conjunto de chaves do macOS local. Como alternativa, variáveis de ambiente podem ser usadas para armazenar o nome de usuário e a senha ou você poderá usar `export fastlane_DONT_STORE_PASSWORD=1` se não quiser que sua senha seja armazenada no conjunto de chaves. Para saber mais sobre como gerenciar credenciais com fastlane, veja o guia do [gerenciador de credenciais](https://github.com/fastlane/fastlane/blob/master/credentials_manager/README.md) do fastlane.

A Apple ID também pode ser passada como um argumento usando o seguinte comando:

    fastlane cert -u myemailadress@domain.com

Se sua Apple ID estiver conectada a várias equipes, elas serão exibidas aqui. Selecione o número que corresponde à equipe que você deseja usar:

[ ![](cert-images/fastlane-image2.png "Selecione a equipe que você deseja usar")](cert-images/fastlane-image2.png)

A ID da equipe também pode ser passada usando o seguinte sinalizador:

    fastlane cert -l 2TU993NY9J

O fastlane verificará se um dos certificados de autenticação disponíveis está instalado no computador local e, se estiver, ele o usará.

Se não houver nenhum certificado de autenticação, o certificado irá:

- Criar uma nova chave privada e solicitação de assinatura
- Gerar, baixar e instalar o certificado
- Importar o certificado e a chave privada para o conjunto de chaves

Quando o número máximo de identidades de assinatura permitido para a sua conta for atingido, uma exceção será gerada. Se desejar criar uma nova identidade de assinatura, você deverá revogar manualmente um dos certificados existentes por meio da Central de desenvolvedores e tentar novamente.

> [!NOTE]
> O fastlane não conseguirá baixar as identidades de assinatura existentes na Central de Desenvolvedores se elas ainda não estiverem no seu conjunto de chaves. Isso ocorre porque a chave privada só existe no seu computador ou na versão exportada (*.p12) do certificado e nunca na Central de desenvolvedores.

<a name="options" />

## <a name="additional-options"></a>Opções Adicionais

As opções a seguir podem ser usadas para dar suporte adicional ao usar o certificado:

- Use o sinalizador `-–help` para obter uma lista de todos os comandos disponíveis:

        fastlane cert --help

- Use o sinalizador `-–verbose` para aumentar os detalhes da saída

        fastlane cert --development --verbose


## <a name="related-links"></a>Links relacionados

- [fastlane – cert](https://github.com/fastlane/fastlane/blob/master/cert/README.md)