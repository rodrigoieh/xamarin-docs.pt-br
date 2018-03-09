---
title: Efeitos
description: "Interfaces de usuário do xamarin. Forms renderizadas usando controles nativos da plataforma de destino, permitindo que os aplicativos xamarin. Forms manter a aparência apropriada para cada plataforma. Efeitos permitem que os controles nativos em cada plataforma para serem personalizados sem precisar recorrer a uma implementação personalizada de processador."
ms.topic: article
ms.prod: xamarin
ms.assetid: 8AF168A7-4CD9-4603-B961-15B8B1543784
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 03/01/2017
ms.openlocfilehash: dd8b98982052e15744bf67ece6a25cd940a9875a
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="effects"></a>Efeitos

_Interfaces de usuário do xamarin. Forms renderizadas usando controles nativos da plataforma de destino, permitindo que os aplicativos xamarin. Forms manter a aparência apropriada para cada plataforma. Efeitos permitem que os controles nativos em cada plataforma para serem personalizados sem precisar recorrer a uma implementação personalizada de processador._

## <a name="introduction-to-effectsintroductionmd"></a>[Introdução aos efeitos](introduction.md)

Efeitos de permitir que os controles nativos em cada plataforma para personalização e são geralmente usados para o estilo de pequenas alterações. Este artigo fornece uma introdução aos efeitos, descreve o limite entre renderizadores personalizados e efeitos e descreve o `PlatformEffect` classe.

## <a name="creating-an-effectcreatingmd"></a>[Criando um efeito](creating.md)

Efeitos de simplificam a personalização de um controle. Este artigo demonstra como criar um efeito que altera a cor de fundo de [ `Entry` ](https://developer.xamarin.com/api/type/Xamarin.Forms.Entry/) controlar quando o controle obtém foco.

## <a name="passing-parameters-to-an-effectpassing-parametersindexmd"></a>[Passando parâmetros para um efeito](passing-parameters/index.md)

Criar um efeito que é configurado por meio de parâmetros permite que o efeito para ser reutilizado. Esses artigos demonstram o uso de propriedades para passar parâmetros para um efeito e alterar um parâmetro em tempo de execução.

## <a name="invoking-events-from-an-effecttouch-trackingmd"></a>[Eventos de invocação de um efeito](touch-tracking.md)

Efeitos podem invocar eventos. Este artigo mostra como criar um evento que implementa o dedo de baixo nível multitoque controle e sinaliza um aplicativo para versões de pressionamentos de toque e move.