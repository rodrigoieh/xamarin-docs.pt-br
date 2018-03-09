---
title: Depurar desgaste Android em um emulador
description: Esses artigos explicam como depurar um aplicativo xamarin desgaste em um emulador.
ms.topic: article
ms.prod: xamarin
ms.assetid: 225684B2-3122-4E3B-A028-A3A400976D31
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/16/2018
ms.openlocfilehash: 1ad3c193261bf22b7ee344aa1ccabb226533b907
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="debug-android-wear-on-an-emulator"></a>Depurar desgaste Android em um emulador

_Esses artigos explicam como depurar um aplicativo xamarin desgaste em um emulador._

## <a name="debug-wear-on-emulator-overview"></a>Depurar desgaste de visão geral do emulador

Desenvolvimento de aplicativos do Android desgaste requer executando o aplicativo no hardware físico ou usando um simulador ou emulador. O uso de hardware é a melhor abordagem, mas nem sempre a mais prática. Em muitos casos, pode ser mais simples e mais econômica para simular/emular hardware desgaste Android usando um emulador, conforme descrito abaixo. Se você não estiver familiarizado com o processo de implantação e execução de aplicativos Android desgaste, consulte [desgaste Hello,](~/android/wear/get-started/hello-wear.md).

## <a name="configure-the-android-sdk-emulator"></a>Configurar o emulador do SDK do Android

Para executar seu aplicativo desgaste em um emulador, você deve instalar o emulador do Android SDK do Android e configurá-lo para uso Android. Para informações de geral de emulador do Android SDK instalação e configuração, consulte [emulador do Android SDK](~/android/deploy-test/debugging/android-sdk-emulator/index.md).

Quando você cria um dispositivo virtual desgaste, selecione um perfil de dispositivo Android desgaste (como **Android desgaste quadrado**). Para melhorar o desempenho, use o desgaste **x86** CPU/ABI como mostrado neste exemplo:

[![Exemplo de configuração de dispositivo virtual desgaste](debug-on-emulator-images/01-wear-avd-example-sml.png)](debug-on-emulator-images/01-wear-avd-example.png)


## <a name="launch-the-wear-virtual-device"></a>Inicie o dispositivo Virtual desgaste 

Depois que você criou um dispositivo virtual Android desgaste, você pode escolhê-lo no menu suspenso de dispositivo no IDE antes de iniciar a depuração. Se seu dispositivo virtual não está disponível no dispositivo pendente, verifique se o projeto é um Android *desgaste* o projeto de aplicativo (não um projeto de aplicativo do Android) e que seu nível de API de destino é definido como a API do mesmo nível como o dispositivo virtual. Por exemplo:

[ ![Escolhendo um AVD desempenham no menu de dispositivo do Visual Studio](debug-on-emulator-images/vs/choose-wear-sim.png)](debug-on-emulator-images/vs/choose-wear-sim.png)

Após inicia o emulador Android, xamarin implantará o aplicativo de desgaste no emulador. O emulador executa o aplicativo com a imagem de dispositivo virtual configurada.

Não se surpreenda se vir isso (ou outra tela intersticial) primeiro. O emulador de inspeção pode levar algum tempo para ser inicializado: 

![Assista o emulador exibe apenas um minuto...](debug-on-emulator-images/please-wait.png)

O emulador pode ser deixado em execução, não é necessário desligá-lo e reiniciá-lo toda vez que o aplicativo for executado.

 
## <a name="summary"></a>Resumo
 
Este guia explicou como configurar o emulador do SDK do Android para o desenvolvimento de desgaste e iniciar um dispositivo virtual desgaste para depuração.