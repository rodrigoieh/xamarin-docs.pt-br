---
title: Inicie o aplicativo de mapa nativo do Xamarin. Forms
description: O aplicativo de mapas nativo em cada plataforma pode ser iniciado por meio de um aplicativo Xamarin. Forms pela classe iniciador Xamarin. Essentials.
ms.prod: xamarin
ms.assetid: 5CF7CD67-3F20-4D80-B99E-D35A5FD1019A
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 10/30/2019
ms.openlocfilehash: 54776d28bb75b152a6402e4d531d1baa4f724cba
ms.sourcegitcommit: 3ea19e3a51515b30349d03c70a5b3acd7eca7fe7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73426198"
---
# <a name="launch-the-native-map-app-from-xamarinforms"></a>Inicie o aplicativo de mapa nativo do Xamarin. Forms

[![Baixar Exemplo](~/media/shared/download.png) Baixar o exemplo](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithmaps)

O aplicativo de mapa nativo em cada plataforma pode ser iniciado por meio de um aplicativo Xamarin. Forms pela classe Xamarin. Essentials `Launcher`. Essa classe permite que um aplicativo abra outro aplicativo por meio de seu esquema de URI personalizado. A funcionalidade do inicializador pode ser invocada com o método `OpenAsync`, passando um `string` ou `Uri` argumento que representa o esquema de URL personalizado a ser aberto. Para obter mais informações sobre o Xamarin. Essentials, consulte [xamarin. Essentials](~/essentials/index.md?context=xamarin/xamarin-forms).

> [!NOTE]
> Uma alternativa ao uso da classe `Launcher` Xamarin. Essentials é usar sua classe `Map`. Para obter mais informações, consulte [Xamarin. Essentials: map](~/essentials/maps.md?context=xamarin/xamarin-forms).

O aplicativo Maps em cada plataforma usa um esquema de URI personalizado exclusivo. Para obter informações sobre o esquema de URI de mapas no iOS, consulte [mapear links](https://developer.apple.com/library/archive/featuredarticles/iPhoneURLScheme_Reference/MapLinks/MapLinks.html) em developer.Apple.com. Para obter informações sobre o esquema de URI de mapas no Android, consulte o [Guia do desenvolvedor de mapas](https://developer.android.com/guide/components/intents-common.html#Maps) e [tentativas do Google Maps para Android](https://developers.google.com/maps/documentation/urls/android-intents) no Developers.Android.com. Para obter informações sobre o esquema URI de mapas no Plataforma Universal do Windows (UWP), consulte [iniciar o aplicativo Windows Maps](/windows/uwp/launch-resume/launch-maps-app).

## <a name="launch-the-map-app-at-a-specific-location"></a>Iniciar o aplicativo de mapa em um local específico

Um local no aplicativo nativo Maps pode ser aberto adicionando parâmetros de consulta apropriados ao esquema de URI personalizado para cada aplicativo de mapa:

```csharp
if (Device.RuntimePlatform == Device.iOS)
{
    // https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/MapLinks/MapLinks.html
    await Launcher.OpenAsync("http://maps.apple.com/?q=394+Pacific+Ave+San+Francisco+CA");
}
else if (Device.RuntimePlatform == Device.Android)
{
    // open the maps app directly
    await Launcher.OpenAsync("geo:0,0?q=394+Pacific+Ave+San+Francisco+CA");
}
else if (Device.RuntimePlatform == Device.UWP)
{
    await Launcher.OpenAsync("bingmaps:?where=394 Pacific Ave San Francisco CA");
}
```

Este código de exemplo resulta na inicialização do aplicativo de mapa nativo em cada plataforma, com o mapa centralizado em um PIN que representa o local especificado:

[![Captura de tela do aplicativo de mapa nativo, no iOS e no Android](native-map-app-images/location.png "Aplicativo de mapa nativo")](native-map-app-images/location-large.png#lightbox "Aplicativo de mapa nativo")

## <a name="launch-the-map-app-with-directions"></a>Iniciar o aplicativo de mapa com direções

O aplicativo de mapas nativo pode ser iniciado exibindo direções, adicionando parâmetros de consulta apropriados ao esquema de URI personalizado para cada aplicativo de mapa:

```csharp
if (Device.RuntimePlatform == Device.iOS)
{
    // https://developer.apple.com/library/ios/featuredarticles/iPhoneURLScheme_Reference/MapLinks/MapLinks.html
    await Launcher.OpenAsync("http://maps.apple.com/?daddr=San+Francisco,+CA&saddr=cupertino");
}
else if (Device.RuntimePlatform == Device.Android)
{
    // opens the 'task chooser' so the user can pick Maps, Chrome or other mapping app
    await Launcher.OpenAsync("http://maps.google.com/?daddr=San+Francisco,+CA&saddr=Mountain+View");
}
else if (Device.RuntimePlatform == Device.UWP)
{
    await Launcher.OpenAsync("bingmaps:?rtp=adr.394 Pacific Ave San Francisco CA~adr.One Microsoft Way Redmond WA 98052");
}
```

Este código de exemplo resulta na inicialização do aplicativo de mapa nativo em cada plataforma, com o mapa centralizado em uma rota entre os locais especificados:

[![Captura de tela da rota do aplicativo de mapa nativo no iOS e no Android](native-map-app-images/directions.png "Direções do aplicativo de mapa nativo")](native-map-app-images/directions-large.png#lightbox "Direções do aplicativo de mapa nativo")

## <a name="related-links"></a>Links relacionados

- [Exemplo de mapas](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/workingwithmaps)
- [Xamarin.Essentials](~/essentials/index.md?context=xamarin/xamarin-forms)
- [Links de mapa](https://developer.apple.com/library/archive/featuredarticles/iPhoneURLScheme_Reference/MapLinks/MapLinks.html)
- [Guia do desenvolvedor de mapas](https://developer.android.com/guide/components/intents-common.html#Maps)
- [Tentativas do Google Maps para Android](https://developers.google.com/maps/documentation/)
- [Iniciar o aplicativo do Windows Maps](/windows/uwp/launch-resume/launch-maps-app)