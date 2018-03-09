---
title: Analisar aplicativos Xamarin.iOS com o Instrumentos
description: Como usar o Instrumentos em um aplicativo Xamarin.iOS em um dispositivo ou no simulador.
ms.topic: article
ms.prod: xamarin
ms.assetid: 70A8CAC8-20C2-655B-37C3-ACF9EA7874D8
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: 9fec6fca0bf7930a59a6927557786a3ed7a412da
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="profiling-xamarinios-applications-with-instruments"></a>Analisar aplicativos Xamarin.iOS com o Instrumentos

_Como usar o Instrumentos em um aplicativo Xamarin.iOS em um dispositivo ou no simulador._

O **Instrumentos** do Xcode é uma ferramenta que pode ser usada para analisar aplicativos Xamarin.iOS em um dispositivo ou no simulador. O Mono usa seu modelo Just-in-Time para compilar o código e o Instrumentos não interpreta bem esses tipos de dados, portanto, pode ser difícil trabalhar com saídas de aplicativos com base em simulador que usam o Instrumentos.
Por causa desse problema, este guia se concentrará em como usar o aplicativo do desenvolvedor para interpretar a saída do Instrumentos neste documento.

## <a name="requirements"></a>Requisitos

O Instrumentos do Xcode só é executado em um Mac.

## <a name="opening-the-instruments-app"></a>Abrir o Aplicativo Instrumentos

Selecione o dispositivo e execute o aplicativo Instrumentos:

1.  Abra o projeto Xamarin.iOS no Visual Studio para Mac.
2.  Selecione a configuração **Depurar|iPhone**.
3.  Conecte um dispositivo iOS ao computador.
4.  No menu **Executar**, selecione **Carregar no Dispositivo**. Agora o aplicativo será compilado e carregado no dispositivo.
5.  No menu **Ferramentas**, selecione **Inicializar Instrumentos**.


O Instrumentos será aberto e exibirá a caixa de diálogo a seguir:

 [ ![](using-instruments-to-detect-native-leaks-using-markheap-images/instruments1.png "Escolher um modelo de criação de perfil")](using-instruments-to-detect-native-leaks-using-markheap-images/instruments1.png)

Clique para selecionar o modelo **Alocações**. Os outros modelos são válidos, mas este artigo apenas aborda o modelo de perfil **Alocações**.

Em seguida, selecione o dispositivo e o aplicativo usando o menu na parte superior da janela:

[ ![](using-instruments-to-detect-native-leaks-using-markheap-images/instruments2.png "Selecionar o dispositivo e o aplicativo")](using-instruments-to-detect-native-leaks-using-markheap-images/instruments2.png)

O dispositivo iOS deve ser selecionado no menu na parte superior da janela e o aplicativo a ser analisado deve ser selecionado próximo dele (**MemoryDemo** na captura de tela acima).

Se o dispositivo não estiver listado no menu, verifique as mensagens de erro no **Console** no Visual Studio para Mac que podem ser exibidas quando o aplicativo é implantado no dispositivo. Além disso, verifique se o dispositivo foi provisionado para desenvolvimento por meio do Xcode Organizer.

Clique no botão **Escolher** e a próxima tela deverá aparecer:

[ ![](using-instruments-to-detect-native-leaks-using-markheap-images/instruments3.png "A interface de criação de perfil")](using-instruments-to-detect-native-leaks-using-markheap-images/instruments3.png)

Clique no botão gravar (círculo vermelho no canto superior esquerdo) para iniciar a análise.

A captura de tela a seguir mostra um exemplo de análise usando o **Instrumentos**:

[ ![](using-instruments-to-detect-native-leaks-using-markheap-images/instruments4.png "Um exemplo de criação de perfil usando o Instrumentos")](using-instruments-to-detect-native-leaks-using-markheap-images/instruments4.png)

## <a name="summary"></a>Resumo

Este guia mostrou como iniciar os Instrumentos do Xcode para monitorar um aplicativo iOS de dentro do Visual Studio para Mac. Vá para o [Passo a passo do Instrumentos](~/ios/deploy-test/walkthrough-apples-instrument.md) para obter um exemplo de como diagnosticar um problema de memória usando o Instrumentos.

## <a name="related-links"></a>Links relacionados

- [Passo a passo do Instrumentos](~/ios/deploy-test/walkthrough-apples-instrument.md)
- [Coleta de lixo do Xamarin.iOS](https://krumelur.me/2015/04/27/xamarin-ios-the-garbage-collector-and-me/)