---
title: Propriedades, métodos e eventos de controle comum do Xamarin. Forms
description: Este artigo descreve Propriedades, métodos e eventos comuns definidos na classe Visualelement, que são comumente usados na derivação de classes.
ms.prod: xamarin
ms.assetId: 85A0CCF5-C1D8-40BB-927F-A4D944E5534D
ms.technology: xamarin-forms
author: profexorgeek
ms.author: jusjohns
ms.date: 08/21/2019
ms.openlocfilehash: 6d10e665c6461655440ddfb2c524cb56a14337f6
ms.sourcegitcommit: 1dd7d09b60fcb1bf15ba54831ed3dd46aa5240cb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/28/2019
ms.locfileid: "70121355"
---
# <a name="xamarinforms-common-control-properties-methods-and-events"></a>Propriedades, métodos e eventos de controle comum do Xamarin. Forms

A classe Xamarin. `VisualElement` Forms é a classe base para a maioria dos controles usados em um aplicativo Xamarin. Forms. A `VisualElement` classe define muitas [Propriedades](#properties), [métodos](#methods)e [eventos](#events) que são usados na derivação de classes.

## <a name="properties"></a>Propriedades

As propriedades a seguir estão disponíveis `VisualElement` em instâncias. Para obter uma lista completa, consulte as [Propriedades da API](xref:Xamarin.Forms.VisualElement#properties)do visualelement.

### [`AnchorX`](xref:Xamarin.Forms.VisualElement.AnchorX)

A `AnchorX` propriedade é um `double` valor que define o ponto central no eixo X para transformações, como escala e rotação. O valor padrão é 0,5.

### [`AnchorY`](xref:Xamarin.Forms.VisualElement.AnchorY)

A `AnchorY` propriedade é um `double` valor que define o ponto central no eixo X para transformações, como escala e rotação. O valor padrão é 0,5.

### [`BackgroundColor`](xref:Xamarin.Forms.VisualElement.BackgroundColor)

A `BackgroundColor` propriedade é um `Color` que determina a cor do plano de fundo do controle. Se a definição for desdefinida, o plano `Color` de fundo será o objeto padrão, que é renderizado como transparente.

### [`Behaviors`](xref:Xamarin.Forms.VisualElement.Behaviors)

A `Behaviors` propriedade é um `List` de `Behavior` objetos. Os `Behaviors` comportamentos permitem que você anexe funcionalidade reutilizável a elementos adicionando-os à lista. Para obter mais informações sobre `Behavior` a classe, consulte [comportamentos do Xamarin. Forms](~/xamarin-forms/app-fundamentals/behaviors/index.md).

### [`Bounds`](xref:Xamarin.Forms.VisualElement.Bounds)

A `Bounds` propriedade é um objeto somente `Rectangle` leitura que representa o espaço ocupado pelo controle. O `Bounds` valor da propriedade é atribuído durante o ciclo de layout. `Rectangle` O`struct` contém propriedades e métodos úteis para testar a interseção e o confinamento de retângulos. Para obter mais informações, consulte a [API do retângulo do Xamarin. Forms](xref:Xamarin.Forms.Rectangle).

### [`Effects`](xref:Xamarin.Forms.Element.Effects)

A `Effects` propriedade é um `List` dos `Effect` objetos herdados da `Element`classe (xref: Xamarin. Forms. Element). Os efeitos permitem que os controles nativos sejam personalizados e normalmente são usados para alterações de estilo pequeno. Para obter mais informações sobre `Effect` a classe, consulte [efeitos do Xamarin. Forms](~/xamarin-forms/app-fundamentals/effects/index.md).

### [`FlowDirection`](xref:Xamarin.Forms.VisualElement.FlowDirection)

A `FlowDirection` propriedade é um `FlowDirection` valor de enumeração. A direção do fluxo pode ser `MatchParent`definida `LeftToRight`como, `RightToLeft` , ou e determina a ordem e a direção do layout. A `FlowDirection` propriedade é normalmente usada para dar suporte a idiomas que são lidos da direita para a esquerda.

### [`Height`](xref:Xamarin.Forms.VisualElement.Height)

A `Height` propriedade é um valor somente `double` leitura que descreve a altura renderizada do controle. A `Height` propriedade é calculada durante o ciclo de layout e não pode ser definida diretamente. A altura de um controle pode ser solicitada usando a [Propriedade HeightRequest](#heightrequest).

### [`HeightRequest`](xref:Xamarin.Forms.VisualElement.HeightRequest)

A `HeightRequest` propriedade é um `double` valor que determina a altura desejada do controle. A altura absoluta do controle pode não corresponder ao valor solicitado. Para obter mais informações, consulte [Propriedades da solicitação](#request-properties).

### [`InputTransparent`](xref:Xamarin.Forms.VisualElement.InputTransparent)

A `InputTransparent` propriedade é um `bool` que determina se o controle recebe entrada do usuário. O valor padrão é `false`, garantindo que o elemento receba a entrada. Essa propriedade é transferida para elementos filho quando ele é definido. Definir a `InputTransparent` Propriedade como `true` em uma classe de layout fará com que todos os elementos dentro do layout não recebam entrada.

### [`IsEnabled`](xref:Xamarin.Forms.VisualElement.IsEnabled)

A `IsEnabled` propriedade é um `bool` valor que determina se o controle reage à entrada do usuário. O valor padrão é `true`. Definir essa propriedade como false impedirá que o controle aceite a entrada do usuário.

### [`IsFocused`](xref:Xamarin.Forms.VisualElement.IsFocused)

A `IsFocused` propriedade é um `bool` valor que descreve se o controle é atualmente o objeto focalizado. Chamar o [`Focus`](#focus) método no controle resultará `IsFocused` no valor definido como true. Chamar o [`Unfocus`](#unfocus) método definirá essa propriedade como false.

### [`IsTabStop`](xref:Xamarin.Forms.VisualElement.IsTabStop)

A `IsTabStop` propriedade é um `bool` valor que define se o controle recebe o foco quando o usuário está avançando pelos controles com a tecla Tab. Se essa propriedade for false, a `TabIndex` propriedade não terá nenhum efeito.

### [`IsVisible`](xref:Xamarin.Forms.VisualElement.IsVisible)

A `IsVisible` propriedade é um `bool` valor que determina se o controle é renderizado. Os controles com `IsVisible` a propriedade definida como false não serão exibidos, não serão considerados cálculos de espaço durante o ciclo de layout e não poderão aceitar a entrada do usuário.

### [`MinimumHeightRequest`](xref:Xamarin.Forms.VisualElement.MinimumHeightRequest)

A `MinimumHeightRequest` propriedade é um `double` valor que determina como o estouro é tratado quando dois elementos estão competindo por um espaço limitado. A definição `MinimumHeightRequest` da propriedade permite que o processo de layout dimensione o elemento para baixo até a dimensão mínima solicitada. Se não `MinimumHeightRequest` for especificado, o valor padrão será-1 e o processo de layout `HeightRequest` considerará que será o valor mínimo. Isso significa que elementos `MinimumHeightRequest` sem valor não terão altura escalonável.

Para obter mais informações, consulte [mínimo de propriedades de solicitação](#minimum-request-properties).

### [`MinimumWidthRequest`](xref:Xamarin.Forms.VisualElement.MinimumWidthRequest)

A `MinimumWidthRequest` propriedade é um `double` valor que determina como o estouro é tratado quando dois elementos estão competindo por um espaço limitado. A definição `MinimumWidthRequest` da propriedade permite que o processo de layout dimensione o elemento para baixo até a dimensão mínima solicitada. Se não `MinimumWidthRequest` for especificado, o valor padrão será-1 e o processo de layout `WidthRequest` considerará que será o valor mínimo. Isso significa que elementos `MinimumWidthRequest` sem valor não terão largura escalonável.

Para obter mais informações, consulte [mínimo de propriedades de solicitação](#minimum-request-properties).

### [`Opacity`](xref:Xamarin.Forms.VisualElement.Opacity)

A `Opacity` propriedade é um `double` valor de zero a um que determina a opacidade do controle durante a renderização. O valor padrão dessa propriedade é 1,0. Os valores fora do intervalo de 0 a 1 serão clamped. A `Opacity` propriedade só será aplicada se a [`IsVisible`](#isvisible) propriedade for `true`. A opacidade é aplicada iterativamente. Portanto, se um controle pai tiver 0,5 de opacidade e seu filho tiver uma opacidade de 0,5, o filho será renderizado com um valor de opacidade de 0,25 efetivo. A definição `Opacity` da propriedade de um controle de entrada como 0 tem um comportamento indefinido.

### [`Parent`](xref:Xamarin.Forms.Element.Parent)

A `Parent` propriedade é herdada `Element` da classe. Essa propriedade é um `Element` objeto que é o pai do controle. A `Parent` propriedade normalmente é definida automaticamente em um elemento quando é adicionada como um filho de outro elemento.

### [`Resources`](xref:Xamarin.Forms.VisualElement.Resources)

A `Resources` propriedade é uma `ResourceDictionary` instância que é populada com pares de chave/valor que normalmente são populados em tempo de execução do XAML. Esse dicionário permite que os desenvolvedores de aplicativos reutilizem objetos definidos em XAML no tempo de compilação e no tempo de execução. As chaves no dicionário são populadas a `x:Key` partir do atributo da marca XAML. O objeto criado a partir de XAML é inserido `ResourceDictionary` no para a chave especificada. Depois de inicializado.

Para obter mais informações, consulte dicionários de [recursos](~/xamarin-forms/xaml/resource-dictionaries.md).

### [`Rotation`](xref:Xamarin.Forms.VisualElement.Rotation)

A `Rotation` propriedade é um `double` valor entre zero e 360 que define a rotação sobre o eixo Z em graus. O valor padrão dessa propriedade é 0. A [`AnchorX`](#anchorx) rotação é aplicada em relação aos [`AnchorY`](#anchory) valores e.

### [`RotationX`](xref:Xamarin.Forms.VisualElement.RotationX)

A `RotationX` propriedade é um `double` valor entre zero e 360 que define a rotação sobre o eixo X em graus. O valor padrão dessa propriedade é 0. A [`AnchorX`](#anchorx) rotação é aplicada em relação aos [`AnchorY`](#anchory) valores e.

### [`RotationY`](xref:Xamarin.Forms.VisualElement.RotationY)

A `RotationY` propriedade é um `double` valor entre zero e 360 que define a rotação sobre o eixo Y em graus. O valor padrão dessa propriedade é 0. A [`AnchorX`](#anchorx) rotação é aplicada em relação aos [`AnchorY`](#anchory) valores e.

### [`Scale`](xref:Xamarin.Forms.VisualElement.Scale)

A `Scale` propriedade é um `double` valor que define a escala do controle. O valor padrão dessa propriedade é 1,0. A [`AnchorX`](#anchorx) escala é aplicada em relação aos [`AnchorY`](#anchory) valores e.

### [`ScaleX`](xref:Xamarin.Forms.VisualElement.ScaleX)

A `ScaleX` propriedade é um `double` valor que define a escala do controle ao longo do eixo X. O valor padrão dessa propriedade é 1,0. A `ScaleX` propriedade é aplicada [`AnchorX`](#anchorx) com relação ao valor.

### [`ScaleY`](xref:Xamarin.Forms.VisualElement.ScaleY)

A `ScaleY` propriedade é um `double` valor que define a escala do controle ao longo do eixo Y. O valor padrão dessa propriedade é 1,0. A `ScaleY` propriedade é aplicada [`AnchorY`](#anchory) com relação ao valor.

### [`Style`](xref:Xamarin.Forms.NavigableElement.Style)

A `Style` propriedade é herdada `NavigableElement` da classe. Essa propriedade é uma instância da `Style` classe. A `Style` classe contém disparadores, setters e comportamentos que definem a aparência e o comportamento de elementos visuais. Para obter mais informações, consulte [estilos XAML do Xamarin. Forms](~/xamarin-forms/user-interface/styles/xaml/index.md).

### [`StyleClass`](xref:Xamarin.Forms.NavigableElement.StyleClass)

A `StyleClass` propriedade é uma lista de `string` objetos que representam os nomes das `Style` classes. Essa propriedade é herdada da `NavigableElement` classe. A `StyleClass` propriedade permite que vários atributos de estilo sejam aplicados a `VisualElement` uma instância. Para obter mais informações, consulte [classes de estilo Xamarin. Forms](~/xamarin-forms/user-interface/styles/xaml/style-class.md).

### [`TabIndex`](xref:Xamarin.Forms.VisualElement.TabIndex)

A `TabIndex` propriedade é um `int` valor que define a ordem de controle ao avançar pelos controles com a tecla Tab. A `TabIndex` propriedade é a implementação para a propriedade definida `ITabStopElement` na interface, que a `VisualElement` classe implementa.

### [`TranslationX`](xref:Xamarin.Forms.VisualElement.TranslationX)

A `TranslationX` propriedade é um `double` valor que define a conversão Delta a ser aplicada no eixo X. A conversão é aplicada após o layout e é normalmente usada para aplicar animações. Convertendo um elemento fora dos limites de seu contêiner pai meus impedem que as entradas funcionem.

Para obter mais informações, consulte [animação no Xamarin. Forms](~/xamarin-forms/user-interface/animation/index.md).

### [`TranslationY`](xref:Xamarin.Forms.VisualElement.TranslationY)

A `TranslationY` propriedade é um `double` valor que define a conversão Delta a ser aplicada no eixo Y. A conversão é aplicada após o layout e é normalmente usada para aplicar animações. Convertendo um elemento fora dos limites de seu contêiner pai meus impedem que as entradas funcionem.

Para obter mais informações, consulte [animação no Xamarin. Forms](~/xamarin-forms/user-interface/animation/index.md).

### [`Triggers`](xref:Xamarin.Forms.VisualElement.Triggers)

A `Triggers` propriedade é somente `List` leitura de `TriggerBase` objetos. Os gatilhos permitem que os desenvolvedores de aplicativos expressem ações em XAML que alteram a aparência visual de controles em resposta a alterações de evento ou propriedade. Para obter mais informações, consulte gatilhos do [Xamarin. Forms](~/xamarin-forms/app-fundamentals/triggers.md).

### [`Visual`](xref:Xamarin.Forms.VisualElement.Visual)

A `Visual` propriedade é uma `IVisual` instância que permite que os renderizadores sejam criados e aplicados seletivamente `VisualElement` a instâncias. A `Visual` propriedade é definida para corresponder ao seu pai, de modo que definir um processador em um componente também se aplicará a qualquer filho desse componente. Se nenhum renderizador personalizado for definido em um controle ou seus ancestrais, o renderizador padrão do Xamarin. Forms será usado. Para obter mais informações, consulte [Visual do Xamarin. Forms](~/xamarin-forms/user-interface/visual/index.md).

### [`Width`](xref:Xamarin.Forms.VisualElement.Width)

A `Width` propriedade é um valor somente `double` leitura que descreve a largura renderizada do controle. A `Width` propriedade é calculada durante o ciclo de layout e não pode ser definida diretamente. A largura de um controle pode ser solicitada usando a [Propriedade WidthRequest](#widthrequest).

### [`WidthRequest`](xref:Xamarin.Forms.VisualElement.WidthRequest)

A `WidthRequest` propriedade é um `double` valor que determina a largura desejada do controle. A largura absoluta do controle pode não corresponder ao valor solicitado. Para obter mais informações, consulte [Propriedades da solicitação](#request-properties).

### [`X`](xref:Xamarin.Forms.VisualElement.X)

A `X` propriedade é um valor somente `double` leitura que descreve a posição X atual do controle.

### [`Y`](xref:Xamarin.Forms.VisualElement.Y)

A `Y` propriedade é um valor somente `double` leitura que descreve a posição Y atual do controle.

## <a name="methods"></a>Métodos

Os métodos a seguir estão disponíveis na `VisualElement` classe. Para obter uma lista completa, consulte [métodos de API](xref:Xamarin.Forms.VisualElement#methods)do visualelement.

### [`FindByName`](xref:Xamarin.Forms.Element.FindByName*)

O `FindByName` método é herdado `Element` da classe e tem a seguinte assinatura:

```csharp
public object FindByName (string name)
```

Esse método pesquisa todos os elementos filho para o `name` argumento fornecido e retorna o elemento que tem o nome especificado. Se nenhuma correspondência for encontrada, `null` será retornado.

### [`Focus`](xref:Xamarin.Forms.VisualElement.Focus)

O `Focus` método tenta definir o foco no elemento. Esse método tem a seguinte assinatura:

```csharp
public bool Focus ()
```

O `Focus` método retorna `true` se o foco do teclado foi definido com `false` êxito e se a chamada do método não resultou em uma alteração de foco. O elemento deve ser capaz de receber o foco para que esse método funcione. Chamar o `Focus` método em elementos que estão fora da tela ou não é realizado tem comportamento indefinido.

### [`Unfocus`](xref:Xamarin.Forms.VisualElement.Unfocus)

O `Unfocus` método tenta remover o foco no elemento. Esse método tem a seguinte assinatura:

```csharp
public void Unfocus ()
```

O elemento já deve ter foco para que esse método funcione.

## <a name="events"></a>Events

Os eventos a seguir estão disponíveis na `VisualElement` classe. Para obter uma lista completa, consulte eventos de Visualelement do [Xamarin. Forms](xref:Xamarin.Forms.VisualElement#events).

### [`Focused`](xref:Xamarin.Forms.VisualElement.Focused)

O `Focused` evento é gerado sempre que `VisualElement` a instância recebe o foco. Esse evento não é bolha por meio da pilha Xamarin. Forms, ele é recebido diretamente do controle nativo. Esse evento é emitido pelo setter de [`IsFocused`](#isfocused) propriedade.

### [`SizeChanged`](xref:Xamarin.Forms.VisualElement.SizeChanged)

O `SizeChanged` evento é gerado sempre que `VisualElement` a `Height` instância `Width` ou as propriedades são alteradas. Se os desenvolvedores quiserem responder diretamente à alteração de tamanho, em vez de responder ao evento de pós-alteração, eles deverão [`OnSizeAllocated`](xref:Xamarin.Forms.VisualElement.OnSizeAllocated*) implementar o método virtual em vez disso.

### [`Unfocused`](xref:Xamarin.Forms.VisualElement.Unfocused)

O `Unfocused` evento é gerado sempre que `VisualElement` a instância perde o foco. Esse evento não é bolha por meio da pilha Xamarin. Forms, ele é recebido diretamente do controle nativo. Esse evento é emitido pelo setter de [`IsFocused`](#isfocused) propriedade.

## <a name="units-of-measurement"></a>Unidades de medida

As plataformas Android, iOS e UWP têm unidades de medida diferentes que podem variar entre os dispositivos. O Xamarin. Forms usa uma unidade de medida independente de plataforma que normaliza as unidades entre dispositivos e plataformas. Há 160 unidades por polegada ou 64 unidades por centímetro, no Xamarin. Forms.

## <a name="request-properties"></a>Propriedades de solicitação

Propriedades cujos nomes contêm "solicitação" definem um valor desejado, que pode não corresponder ao valor real renderizado. Por exemplo, `HeightRequest` pode ser definido como 150, mas se o layout permitir apenas espaço para 100 unidades, o `Height` processamento do controle será apenas 100. O tamanho renderizado é afetado pelo espaço disponível e pelos componentes contidos.

## <a name="minimum-request-properties"></a>Propriedades de solicitação mínimas

As propriedades de solicitação `MinimumHeightRequest` mínimas incluem e `MinimumWidthRequest`e destinam-se a permitir um controle mais preciso sobre como os elementos manipulam o estouro em relação uns aos outros. No entanto, o comportamento de layout relacionado a essas propriedades tem algumas considerações importantes.

### <a name="unspecified-minimum-property-values"></a>Valores mínimos de propriedade não especificados

Se um valor mínimo não for definido, a propriedade Minimum definirá como padrão-1. O processo de layout ignora esse valor e considera o valor absoluto como o mínimo. A consequência prática desse comportamento é que um elemento sem nenhum valor mínimo especificado **não será** reduzido. Um elemento com um valor mínimo especificado **será** reduzido.

O XAML a seguir mostra `BoxView` dois elementos em uma `StackLayout`horizontal:

```xaml
<StackLayout Orientation="Horizontal">
    <BoxView HeightRequest="100" BackgroundColor="Purple" WidthRequest="500"></BoxView>
    <BoxView HeightRequest="100" BackgroundColor="Green" WidthRequest="500" MinimumWidthRequest="250"></BoxView>
</StackLayout>
```

A primeira `BoxView` instância solicita uma largura de 500 e não especifica uma largura mínima. A segunda `BoxView` instância solicita uma largura de 500 e uma largura mínima de 250. Se o elemento `StackLayout` pai não for grande o suficiente para conter os dois componentes na largura solicitada, `BoxView` a primeira instância será considerada pelo processo de layout para ter uma largura mínima de 500, pois nenhum outro mínimo válido será especificado. A segunda `BoxView` instância tem permissão para reduzir para 250 e será reduzida para se ajustar até que sua largura atinja 250 unidades.

Se o comportamento desejado for para a primeira `BoxView` instância reduzir verticalmente sem largura mínima, o `MinimumWidthRequest` deverá ser definido como um valor válido, como 0.

### <a name="minimum-and-absolute-property-values"></a>Valores de propriedade mínimo e absoluto

O comportamento é indefinido quando o valor mínimo é maior que o valor absoluto. Por exemplo, se `MinimumWidthRequest` for definido como 100, a `WidthRequest` Propriedade nunca deverá exceder 100. Ao especificar um valor mínimo de propriedade, você sempre deve especificar um valor absoluto para garantir que o valor absoluto seja maior que o valor mínimo.

### <a name="minimum-properties-within-a-grid"></a>Propriedades mínimas em uma grade

`Grid`os layouts têm seu próprio sistema para o dimensionamento relativo de linhas e colunas. Usar `MinimumWidthRequest` `Grid` ou `MinimumHeightRequest` dentro de um layout não terá efeito. Para obter mais informações, consulte a [grade Xamarin. Forms](~/xamarin-forms/user-interface/layouts/grid.md).

## <a name="related-links"></a>Links relacionados

* [Documentação da API do visualelement](xref:Xamarin.Forms.VisualElement)