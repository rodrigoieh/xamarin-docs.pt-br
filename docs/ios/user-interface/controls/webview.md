---
title: Exibições da Web no Xamarin. iOS
description: Este documento descreve as várias maneiras como um aplicativo Xamarin. iOS pode exibir conteúdo da Web. Ele aborda WKWebView, SFSafariViewController, Safari e segurança de transporte de aplicativo.
ms.prod: xamarin
ms.assetid: 84886CF4-2B2B-4540-AD92-7F0B791952D1
ms.technology: xamarin-ios
author: davidortinau
ms.author: daortin
ms.date: 03/22/2017
ms.openlocfilehash: 933edb1c0681f3fc9cbb8d81aa3091a65c4346e3
ms.sourcegitcommit: 3e94c6d2b6d6a70c94601e7bf922d62c4a6c7308
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/15/2020
ms.locfileid: "76031361"
---
# <a name="web-views-in-xamarinios"></a>Exibições da Web no Xamarin. iOS

Ao longo do tempo de vida do iOS, a Apple lançou várias maneiras para os desenvolvedores de aplicativos incorporarem a funcionalidade de exibição da Web em seus aplicativos. A maioria dos usuários utiliza o navegador da Web interno do Safari em seu dispositivo iOS e, portanto, espera que a funcionalidade de exibição da Web de outros aplicativos seja consistente com essa experiência. Eles esperam que os mesmos gestos funcionem, o desempenho deve estar em par e a funcionalidade do mesmo.

o iOS 11 introduziu novas alterações em `WKWebView` e `SFSafariViewController`. Para obter mais informações sobre eles, consulte as [alterações na Web no guia do guia do IOS 11](~/ios/platform/introduction-to-ios11/web.md) .

## <a name="wkwebview"></a>WKWebView

o `WKWebView` foi introduzido no iOS 8, permitindo que os desenvolvedores de aplicativos implementem uma interface de navegação na Web semelhante à do Mobile Safari. Isso é devido, em parte, ao fato de que `WKWebView` usa o mecanismo de JavaScript nitro, o mesmo mecanismo usado pelo Mobile Safari. `WKWebView` sempre deve ser usado em UIWebView, quando possível devido ao [aumento do desempenho](http://blog.initlabs.com/post/100113463211/wkwebview-vs-uiwebview), aos gestos internos amigáveis e à facilidade de interação entre a página da Web e seu aplicativo.
  
`WKWebView` pode ser adicionado ao seu aplicativo de uma maneira quase idêntica ao UIWebView, no entanto, como desenvolvedor, você tem muito mais controle sobre a interface do usuário/UX e a funcionalidade. Criar e exibir o objeto de exibição da Web exibirá a página solicitada, no entanto, você pode controlar como a exibição é apresentada, como o usuário pode navegar e como o usuário sai da exibição.  

O código a seguir pode ser usado para iniciar um `WKWebView` em seu aplicativo Xamarin. iOS:

```csharp
WKWebView webView = new WKWebView(View.Frame, new WKWebViewConfiguration());
View.AddSubview(webView);

var url = new NSUrl("https://docs.microsoft.com");
var request = new NSUrlRequest(url);
webView.LoadRequest(request);
```

É importante observar que `WKWebView` está no namespace `WebKit`, portanto, você precisará adicioná-lo usando a diretiva na parte superior da sua classe.

`WKWebView` também pode ser usado em aplicativos Xamarin. Mac e você deve usá-lo se estiver criando um aplicativo Mac/iOS de plataforma cruzada.

A receita [lidar com alertas JavaScript](https://github.com/xamarin/recipes/tree/master/Recipes/ios/content_controls/web_view/handle_javascript_alerts) também fornece informações sobre como usar o WKWebView com JavaScript.

## <a name="sfsafariviewcontroller"></a>SFSafariViewController

 `SFSafariViewController` é a maneira mais recente de fornecer conteúdo da Web do seu aplicativo e está disponível no iOS 9 e posterior. Ao contrário de `UIWebView` ou `WKWebView`, `SFSafariViewController` é um controlador de exibição e, portanto, não pode ser usado com outras exibições. Você deve apresentar `SFSafariViewController` como um novo controlador de exibição, da mesma maneira que apresentaria qualquer controlador de exibição.

 `SFSafariViewController` é essencialmente um "mini safari" que pode ser inserido em seu aplicativo. Como o WKWebView, ele usa o mesmo mecanismo de JavaScript nitro, mas também fornece uma variedade de recursos adicionais do Safari, como preenchimento automático, leitor e a capacidade de compartilhar cookies e dados com o Mobile Safari. A interação entre o usuário e o `SFSafariViewController` não é acessível para seu aplicativo. Seu aplicativo não terá acesso a nenhum dos recursos padrão do Safari.

Ele também, por padrão, implementa um botão **Done** , permitindo que o usuário retorne facilmente ao seu aplicativo e botões de navegação para frente e para trás, permitindo que o usuário navegue por uma pilha de páginas da Web. Além disso, ele também fornece ao usuário uma barra de endereços, oferecendo a tranqüilidade de que eles estejam na página da Web esperada. A barra de endereços não permite que o usuário altere a URL. 

Essas implementações não podem ser alteradas, portanto `SFSafariViewController` é ideal para ser usado como navegador padrão se seu aplicativo quiser apresentar uma página da Web sem nenhuma personalização.

O código a seguir pode ser usado para iniciar um `SFSafariViewController` em seu aplicativo Xamarin. iOS:

```csharp
var sfViewController = new SFSafariViewController(url);

PresentViewController(sfViewController, true, null);
```

Isso produz a seguinte exibição da Web:

[![um modo de exibição da Web de exemplo com SFSafariViewController](webview-images/sfsafariviewcontroller.png)](webview-images/sfsafariviewcontroller.png#lightbox)

## <a name="safari"></a>Safari

Também é possível abrir o aplicativo Mobile Safari de dentro de seu aplicativo, usando o código abaixo:

```csharp
var url = new NSUrl("https://docs.microsoft.com");

UIApplication.SharedApplication.OpenUrl(url);
```

Isso produz a seguinte exibição da Web:

[![uma página da Web apresentada no Safari](webview-images/safari.png)](webview-images/safari.png#lightbox)

A navegação de usuários fora do seu aplicativo para o Safari geralmente deve ser evitada sempre. A maioria dos usuários não esperará a navegação fora do seu aplicativo, portanto, se você sair do seu aplicativo, os usuários nunca poderão retorná-lo, essencialmente eliminando o envolvimento.

os aprimoramentos do iOS 9 permitem que o usuário retorne facilmente ao seu aplicativo por meio de um botão voltar que é fornecido no canto superior esquerdo da página do Safari.

## <a name="app-transport-security"></a>Segurança do transporte de aplicativo

A segurança de transporte de aplicativo ou a *ATS* foi introduzida pela Apple no Ios 9 para garantir que todas as comunicações da Internet estejam em conformidade com as práticas recomendadas de conexão seguras.

Para obter mais informações sobre o ATS, incluindo como implementá-lo em seu aplicativo, consulte o guia de [segurança do transporte de aplicativo](~/ios/app-fundamentals/ats.md) .

## <a name="uiwebview-deprecated"></a>UIWebView (preterido)

> [!IMPORTANT]
> O `UIWebView` foi preterido. Os aplicativos que usam esse controle [não serão aceitos na loja de aplicativos a partir de abril de 2020, e os aplicativos existentes precisarão removê-lo até 2020 de dezembro](https://developer.apple.com/news/?id=12232019b).
> 
> A [documentação de `UIWebView` da Apple](https://developer.apple.com/documentation/uikit/uiwebview) sugere que os aplicativos usem [`WKWebView`](#wkwebview) em vez disso.

> [!IMPORTANT]
> Se você estiver procurando recursos em relação ao `UIWebView` aviso de reprovação (ITMS-90809) ao usar o Xamarin. Forms, consulte a documentação do [WebView xamarin. Forms](~/xamarin-forms/user-interface/webview.md#uiwebview-deprecation-and-app-store-rejection-itms-90809) .

`UIWebView` é a maneira herdada da Apple de fornecer conteúdo da Web em seu aplicativo. Ele foi lançado no iOS 2,0 e foi preterido a partir de 8,0.

Para adicionar um UIWebView ao seu aplicativo Xamarin. iOS, use o seguinte código:

```csharp
webView = new UIWebView (View.Bounds);
View.AddSubview(webView);

var url = "https://docs.microsoft.com"; // NOTE: https secure request
webView.LoadRequest(new NSUrlRequest(new NSUrl(url)));
```

Isso produz a seguinte exibição da Web:

[![o efeito de ScalesPagesToFit](webview-images/webview.png)](webview-images/webview.png#lightbox)

## <a name="related-links"></a>Links Relacionados

- [Webviews (exemplo)](https://docs.microsoft.com/samples/xamarin/ios-samples/webview)