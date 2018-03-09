---
title: "Implantação e Teste"
description: "Estabilização e guias de implantação"
ms.topic: article
ms.prod: xamarin
ms.assetid: 92B35AB1-7AB7-3D3B-DB31-CC971E0B43AE
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/19/2017
ms.openlocfilehash: 0c152c389a6aa62512882863cd2830b436587475
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="deployment-and-testing"></a>Implantação e Teste

Esta seção aborda tópicos usados para testar um aplicativo, bem como para distribuí-lo. Os tópicos aqui incluem coisas como ferramentas usadas para depuração, implantação em testadores e como publicar um aplicativo na App Store.


##  <a name="app-distributioniosdeploy-testapp-distributionindexmd"></a>[Distribuição de aplicativo](~/ios/deploy-test/app-distribution/index.md)

Este artigo mostra como configurar, compilar e publicar um aplicativo Xamarin.iOS para distribuição através de várias maneiras diferentes, incluindo:

- [Distribuição da App Store](~/ios/deploy-test/app-distribution/app-store-distribution/index.md)
- [Distribuição interna (Empresa)](~/ios/deploy-test/app-distribution/in-house-distribution.md)
- [Distribuição Ad Hoc](~/ios/deploy-test/app-distribution/ad-hoc-distribution.md)

##  <a name="ipa-deploymentiosdeploy-testapp-distributionipa-supportmd"></a>[Implantação de IPA](~/ios/deploy-test/app-distribution/ipa-support.md)

As Implantações da Empresa e Ad Hoc permitem aos desenvolvedores criar pacotes que podem ser distribuídos para teste ou para usuários internos da empresa. Este documento explica como criar um IPA que pode ser sincronizado com um dispositivo iOS usando o iTunes.

## <a name="provisioningprovisioningindexmd"></a>[Provisionamento](provisioning/index.md)

Este conjunto de guias abrange a assinatura de código e princípios básicos de provisionamento, por exemplo, como trabalhar com listas de propriedades e como configurar um aplicativo para serviços de aplicativo. 

## <a name="wireless-deploymentwireless-deploymentmd"></a>[Implantação sem fio](wireless-deployment.md)

 O Xcode 9 introduziu a opção de implantação em um dispositivo iOS ou Apple TV por meio de uma rede, em vez de exigir instalações físicas sempre que você quiser implantar e depurar o aplicativo. Este recurso está atualmente em versão prévia.

##  <a name="testflightiosdeploy-testtestflightmd"></a>[TestFlight](~/ios/deploy-test/testflight.md)

O TestFlight agora é de propriedade da Apple e é a principal maneira de fazer o teste beta de seus aplicativos Xamarin.iOS. Este artigo o orientará por todas as etapas do Processo de TestFlight – do upload do aplicativo até o trabalho com o iTunes Connect.

##  <a name="debugging-in-xamariniosiosdeploy-testdebugging-in-xamarin-iosmd"></a>[Depuração no Xamarin.iOS](~/ios/deploy-test/debugging-in-xamarin-ios.md)

Os IDEs (ambientes de desenvolvimento integrado) do Visual Studio e do Visual Studio para Mac incluem suporte para a depuração de aplicativos Xamarin.iOS no simulador de iOS e em dispositivos iOS. Este artigo mostra como usar o depurador e também como configurar várias opções às quais ele oferece suporte.


##  <a name="touchunitiosdeploy-testtouchunitmd"></a>[Touch.Unit](~/ios/deploy-test/touch.unit.md)

Este documento descreve como criar testes de unidade para seus projetos do Xamarin.iOS.
Os testes de unidade com o Xamarin.iOS são feitos usando a estrutura Touch.Unit que inclui um executor de teste iOS, bem como uma versão modificada da estrutura [NUnitLite](http://www.nunitlite.com/) que fornece um conjunto familiar de APIs para gravar testes de unidade.



##  <a name="using-instruments-to-detect-native-leaks-using-markheapiosdeploy-testusing-instruments-to-detect-native-leaks-using-markheapmd"></a>[Uso do Instrumentos para detectar perdas nativas usando o MarkHeap](~/ios/deploy-test/using-instruments-to-detect-native-leaks-using-markheap.md)

Este artigo descreve como usar o Instrumentos em qualquer dispositivo iOS e qualquer aplicativo Xamarin.iOS. Ele também mostra como analisar aplicativos no simulador.



##  <a name="walkthrough---using-apples-instrument-tooliosdeploy-testwalkthrough-apples-instrumentmd"></a>[Passo a passo – usando a ferramenta Instruments da Apple](~/ios/deploy-test/walkthrough-apples-instrument.md)

Este artigo explica como usar a ferramenta Instrumentos da Apple para diagnosticar problemas de memória em um aplicativo iOS compilado com o Xamarin. Demonstra como inicializar o Instrumentos, tirar instantâneos do heap e analisar o aumento da memória. Ele também mostra como usar o Instrumentos para exibir e identificar as linhas exatas do código que causam o problema de memória.

##  <a name="linking-on-ioslinkermd"></a>[Vinculação no iOS](linker.md)

Explica como funciona o vinculador para garantir o menor pacote de aplicativos possível e como modificar as configurações e o uso.

##  <a name="xamarinios-performanceperformancemd"></a>[Desempenho do Xamarin.iOS](performance.md)

Há várias técnicas para aumentar o desempenho dos aplicativos criados com o Xamarin.iOS. Coletivamente, essas técnicas podem reduzir de forma considerável a quantidade de trabalho que está sendo executado por uma CPU e a quantidade de memória consumida por um aplicativo.

##  <a name="mtouchmtouchmd"></a>[mtouch](mtouch.md)

Notas e informações sobre o mtouch.exe, a ferramenta de linha de comando que compila seu projeto em um aplicativo que pode ser usado em iOS.

## <a name="ios-build-mechanicsios-build-mechanicsmd"></a>[Mecânica de compilação do iOS](ios-build-mechanics.md)

Este guia explora como determinar o ritmo dos seus aplicativos e como usar métodos que podem ser empregados para compilações mais rápidas para todas as configurações de compilação.