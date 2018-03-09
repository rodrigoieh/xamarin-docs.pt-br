---
title: "Trabalhando com os controladores de navegação"
description: "Este artigo aborda criando e trabalhando com barras de navegação dentro de um aplicativo Xamarin.tvOS."
ms.topic: article
ms.prod: xamarin
ms.assetid: 74E396B7-87F0-46F7-BC6C-827DB8884C97
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/16/2017
ms.openlocfilehash: 3d5b4b0d3e6e9388906efa3bff2db0ea38fa8605
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="working-with-navigation-controllers"></a>Trabalhando com os controladores de navegação

_Este artigo aborda criando e trabalhando com barras de navegação dentro de um aplicativo Xamarin.tvOS._

Barras de navegação pode ser adicionadas à parte superior das exibições para exibir um título e os botões da barra de navegação opcional. Normalmente, eles são usados quando o usuário navegar de uma página principal, como um modo de exibição de tabela, coleção ou Menu para um modo de exibição secundário mostrando os detalhes do item selecionado.

[ ![](navigation-bars-images/navbar01.png "Exemplo de barra de navegação")](navigation-bars-images/navbar01.png)

Além disso, com o título (que é exibido no centro), barras de navegação pode conter um ou mais botões da barra de navegação (`UIBarButtonItem`) à esquerda e direita da barra.

> [!IMPORTANT]
> **Observação:** barras de navegação são totalmente transparentes por padrão. Tome cuidado para garantir que o conteúdo da barra de navegação esteja legível o conteúdo abaixo dele. Por exemplo, quando o conteúdo em um modo de exibição de tabela ou uma coleção rola sob ele.




<a name="Navigation-Bars-and-Storyboards" />

## <a name="navigation-bars-and-storyboards"></a>Barras de navegação e Storyboards

É a maneira mais fácil trabalhar com barras de navegação em um aplicativo de Xamarin.tvOS para adicioná-los à interface de usuário do aplicativo usando o Designer do iOS.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio para Mac](#tab/vsmac)


1. No **solução preenchimento**, clique duas vezes em `Main.storyboard` de arquivo e abri-lo para edição.
1. Arraste um **barra de navegação** do **caixa de ferramentas** e solte-o no modo de exibição na parte superior da tela: 

    [ ![](navigation-bars-images/navbar02.png "Uma barra de navegação")](navigation-bars-images/navbar02.png)
1. Clique duas vezes no **barra de navegação** para selecionar a **Item de navegação**. No **Widget** guia do **propriedades de preenchimento**, você pode definir o **título**: 

    [ ![](navigation-bars-images/navbar03.png "Definir o título")](navigation-bars-images/navbar03.png)
1. Em seguida, você pode adicionar um ou mais **itens da barra de botão** para ambas as extremidades da barra de: 

    [ ![](navigation-bars-images/navbar04.png "Um Item de botão")](navigation-bars-images/navbar04.png)
1. Durante a transmissão por fim, o o **itens da barra de botão** ações no **eventos** guia do **propriedades Explorer**: 

    [ ![](navigation-bars-images/navbar05.png "A ação do Item de botão de barra")](navigation-bars-images/navbar05.png)
1. Salve as alterações.


# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)


1. No **Solution Explorer**, clique duas vezes em `Main.storyboard` de arquivo e abri-lo para edição.
1. Arraste um **barra de navegação** do **caixa de ferramentas** e solte-o no modo de exibição na parte superior da tela: 

    [ ![](navigation-bars-images/navbar02-vs.png "Uma barra de navegação")](navigation-bars-images/navbar02-vs.png)
1. Clique duas vezes no **barra de navegação** para selecionar a **Item de navegação**. No **Widget** guia do **propriedades Explorer**, você pode definir o **título**: 

    [ ![](navigation-bars-images/navbar03-vs.png "Definir o título")](navigation-bars-images/navbar03-vs.png)
1. Em seguida, você pode adicionar um ou mais **itens da barra de botão** para ambas as extremidades da barra de: 

    [ ![](navigation-bars-images/navbar04-vs.png "Um botão de itens")](navigation-bars-images/navbar04-vs.png)
1. Durante a transmissão por fim, o o **itens da barra de botão** ações no **eventos** guia do **propriedades Explorer**: 

    [ ![](navigation-bars-images/navbar05-vs.png "A barra de ações do Item de botão")](navigation-bars-images/navbar05-vs.png)
1. Salve as alterações.


-----

> [!IMPORTANT]
> **Observação:** enquanto é possível atribuir eventos como `TouchUpInside` para um elemento de interface do usuário (como um UIButton) no Designer do iOS, ele nunca será chamado porque Apple TV não tem um toque de tela ou oferecer suporte a eventos de toque. Você sempre deve usar o `Primary Action` eventos durante a criação de manipuladores de eventos para tvOS elementos da interface do usuário.




O código a seguir fornece um exemplo de manipuladores de eventos em três BarButtonItems diferentes: `ShowFirstHotel`, `ShowSecondHotel`, e `ShowThirdHotel`. Quando cada item é clicado, a imagem de plano de fundo `HotelImage` é alterado. Isso é editado no controlador de exibição (exemplo `ViewController.cs`) arquivo:

```csharp
using System;
using Foundation;
using UIKit;

namespace MySingleView
{
    public partial class ViewController : UIViewController
    {
        #region Constructors
        public ViewController (IntPtr handle) : base (handle)
        {
        }
        #endregion

        #region Override Methods
        public override void ViewDidLoad ()
        {
            base.ViewDidLoad ();
            // Perform any additional setup after loading the view, typically from a nib.
        }

        public override void DidReceiveMemoryWarning ()
        {
            base.DidReceiveMemoryWarning ();
            // Release any cached data, images, etc that aren't in use.
        }
        #endregion

        #region Custom Actions
        partial void ShowFirstHotel (UIBarButtonItem sender) {
            // Change background image
            HotelImage.Image = UIImage.FromFile("Motel01.jpg");
        }

        partial void ShowSecondHotel (UIBarButtonItem sender) {
            // Change background image
            HotelImage.Image = UIImage.FromFile("Motel02.jpg");
        }

        partial void ShowThirdHotel (UIBarButtonItem sender) {
            // Change background image
            HotelImage.Image = UIImage.FromFile("Motel03.jpg");
        }
        #endregion
    }
}
```

Desde que um botão `Enabled` é de propriedade `true` e ele não é coberto por outro controle ou exibição, pode ser feita o item de em foco usando Siri remoto.

Para obter mais informações sobre como trabalhar com Storyboards, consulte nosso [Hello, tvOS Quick Start Guide](~/ios/tvos/get-started/hello-tvos.md). 

<a name="Summary" />

## <a name="summary"></a>Resumo

Este artigo abordou criando e trabalhando com barras de navegação dentro de um aplicativo Xamarin.tvOS.



## <a name="related-links"></a>Links relacionados

- [Exemplos de tvOS](https://developer.xamarin.com/samples/tvos/all/)
- [tvOS](https://developer.apple.com/tvos/)
- [tvOS guias de Interface Humana](https://developer.apple.com/tvos/human-interface-guidelines/)
- [Guia de programação de aplicativo para tvOS](https://developer.apple.com/library/prerelease/tvos/documentation/General/Conceptual/AppleTV_PG/)