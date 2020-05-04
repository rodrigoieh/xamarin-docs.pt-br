---
title: Expansor do Xamarin. Forms
description: O controle expansor do Xamarin. Forms fornece um contêiner expansível para hospedar qualquer conteúdo. O conteúdo é exibido ou oculto tocando no cabeçalho do expansor.
ms.prod: xamarin
ms.assetid: 381DCB55-522D-4414-B45B-E8DD70AA9985
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/15/2020
ms.openlocfilehash: f47dc08d11a97598966ba7af620cfc81e5fe284f
ms.sourcegitcommit: 8d13d2262d02468c99c4e18207d50cd82275d233
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82532621"
---
# <a name="xamarinforms-expander"></a>Expansor do Xamarin. Forms

[![Baixar exemplo](~/media/shared/download.png) baixar o exemplo](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-expanderdemos/)

O controle Xamarin. `Expander` Forms fornece um contêiner expansível para hospedar qualquer conteúdo. O controle tem um cabeçalho e conteúdo, e o conteúdo é mostrado ou oculto tocando no `Expander` cabeçalho. Quando apenas o `Expander` cabeçalho é mostrado, o `Expander` é *recolhido*. Quando o `Expander` conteúdo estiver visível, `Expander` o será *expandido*.

As capturas de tela a `Expander` seguir mostram um em seus Estados recolhidos e expandidos, com caixas vermelhas indicando o cabeçalho e o conteúdo:

![Captura de tela de um expansor em Estados recolhidos e expandidos, no iOS e no Android](expander-images/expander.png "Expansor no iOS e Android")

> [!IMPORTANT]
> `Expander`o é experimental e só pode ser usado com a definição `Expander_Experimental` do sinalizador. Para obter mais informações, consulte [sinalizadores experimentais](~/xamarin-forms/internals/experimental-flags.md).

O `Expander` controle define as seguintes propriedades:

- `CollapseAnimationEasing`, do tipo [`Easing`](xref:Xamarin.Forms.Easing), que representa a função de atenuação a ser aplicada `Expander` ao conteúdo quando ele está sendo recolhido.
- `CollapseAnimationLength`, do tipo `uint`, que define a duração da animação quando o `Expander` está sendo recolhido. O valor padrão dessa propriedade é 250 MS.
- `Command`, do tipo `ICommand`, que é executado quando o `Expander` cabeçalho é tocado.
- `CommandParameter`, do tipo `object`, que é o parâmetro passado para `Command`.
- `Content`, do tipo [`View`](xref:Xamarin.Forms.View), que define o conteúdo a ser exibido quando o `Expander` expande.
- `ContentTemplate`, do tipo [`DataTemplate`](xref:Xamarin.Forms.DataTemplate), que é o modelo usado para aumentar dinamicamente o conteúdo do `Expander`.
- `ExpandAnimationEasing`, do tipo [`Easing`](xref:Xamarin.Forms.Easing), que representa a função de atenuação a ser aplicada `Expander` ao conteúdo durante a expansão.
- `ExpandAnimationLength`, do tipo `uint`, que define a duração da animação quando o `Expander` expande. O valor padrão dessa propriedade é 250 MS.
- `ForceUpdateSizeCommand`, do tipo `ICommand`, que define o comando que é executado quando o tamanho da força `Expander` é atualizado. Essa propriedade usa o `OneWayToSource` modo de associação.
- `Header`, do tipo [`View`](xref:Xamarin.Forms.View), que define o conteúdo do cabeçalho.
- `IsExpanded`, do tipo `bool`, que determina se o `Expander` é expandido. Essa propriedade usa o `TwoWay` modo de associação e tem um valor padrão de `false`.
- `Spacing`, do tipo `double`, que representa o espaço entre o cabeçalho e seu conteúdo. O valor padrão dessa propriedade é 0.
- `State`, do tipo `ExpanderState`, que representa o estado do `Expander`. Essa propriedade usa o `OneWayToSource` modo de associação.

Essas propriedades são apoiadas por [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) objetos, o que significa que eles podem ser destinos de associações de dados e com estilo.

> [!NOTE]
> A `Content` propriedade é a propriedade content da `Expander` classe e, portanto, não precisa ser definida explicitamente a partir de XAML.

A enumeração `ExpanderState` define os seguintes membros:

- `Expanding`indica que o `Expander` está sendo expandido.
- `Expanded`indica que o `Expander` está expandido.
- `Collapsing`indica que o `Expander` está sendo recolhido.
- `Collapsed`indica que o `Expander` está recolhido.

O `Expander` controle também define um `Tapped` evento que é acionado quando `Expander` o cabeçalho é tocado. Além disso, `Expander` o inclui `ForceUpdateSize` um método que pode ser chamado para redimensionar `Expander` de forma programática o em tempo de execução.

## <a name="create-an-expander"></a>Criar um expansor

O exemplo a seguir mostra como criar uma `Expander` instância de em XAML:

```xaml
<Expander>
    <Expander.Header>
        <Label Text="Baboon"
               FontAttributes="Bold"
               FontSize="Medium" />
    </Expander.Header>
    <Grid Padding="10">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <Image Source="http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg"
               Aspect="AspectFill"
               HeightRequest="120"
               WidthRequest="120" />
        <Label Grid.Column="1"
               Text="Baboons are African and Arabian Old World monkeys belonging to the genus Papio, part of the subfamily Cercopithecinae."
               FontAttributes="Italic" />
    </Grid>
</Expander>
```

Neste exemplo, o `Expander` é recolhido por padrão e exibe um [`Label`](xref:Xamarin.Forms.Label) como seu cabeçalho. Tocar no cabeçalho resulta na `Expander` expansão para revelar seu conteúdo, que é um [`Grid`](xref:Xamarin.Forms.Grid) que contém controles filho. Quando o `Expander` é expandido, tocar em seu cabeçalho recolhe `Expander`o.

> [!IMPORTANT]
> Ao definir a `Expander.Content` Propriedade, implícita ou explicitamente, o `Expander` conteúdo é criado quando a página que o contém é navegada, mesmo que o `Expander` seja recolhido. No entanto `Expander.ContentTemplate` , a propriedade pode ser definida como conteúdo que só fica inplana quando `Expander` o é expandido pela primeira vez. Para obter mais informações, consulte [criar conteúdo do expansor sob demanda](#create-expander-content-on-demand).

Como alternativa, um `Expander` pode ser criado no código:

```csharp
Expander expander = new Expander
{
    Header = new Label
    {
        Text = "Baboon",
        FontAttributes = FontAttributes.Bold,
        FontSize = Device.GetNamedSize(NamedSize.Medium, typeof(Label))
    }
};

Grid grid = new Grid
{
    Padding = new Thickness(10),
    ColumnDefinitions =
    {
        new ColumnDefinition { Width = GridLength.Auto },
        new ColumnDefinition { Width = GridLength.Auto }
    }
};

grid.Children.Add(new Image
{
    Source = "http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg",
    Aspect = Aspect.AspectFill,
    HeightRequest = 120,
    WidthRequest = 120
});

grid.Children.Add(new Label
{
    Text = "Baboons are African and Arabian Old World monkeys belonging to the genus Papio, part of the subfamily Cercopithecinae.",
    FontAttributes = FontAttributes.Italic
}, 1, 0);

expander.Content = grid;
```

## <a name="create-expander-content-on-demand"></a>Criar conteúdo do expansor sob demanda

`Expander`o `Expander` conteúdo pode ser criado sob demanda, em resposta à expansão. Isso pode ser feito definindo a `Expander.ContentTemplate` Propriedade como um [`DataTemplate`](xref:Xamarin.Forms.DataTemplate) que contém o conteúdo:

```xaml
<Expander>
    <Expander.Header>
        <Label Text="{Binding Name}"
               FontAttributes="Bold"
               FontSize="Medium" />
    </Expander.Header>
    <Expander.ContentTemplate>
        <DataTemplate>
            <Grid Padding="10">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="Auto" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <Image Source="{Binding ImageUrl}"
                       Aspect="AspectFill"
                       HeightRequest="120"
                       WidthRequest="120" />
                <Label Grid.Column="1"
                       Text="{Binding Details}"
                       FontAttributes="Italic" />
            </Grid>
        </DataTemplate>
    </Expander.ContentTemplate>
</Expander>
```

Neste exemplo, o `Expander` conteúdo é apenas inalterado quando o `Expander` expande pela primeira vez.

A vantagem dessa abordagem é que, quando uma página contém vários `Expander` objetos, o conteúdo de um `Expander` é criado apenas quando expandido pela primeira vez pelo usuário.

## <a name="add-an-expansion-indicator"></a>Adicionar um indicador de expansão

Um [`Image`](xref:Xamarin.Forms.Image) pode ser adicionado a um `Expander` cabeçalho para fornecer uma indicação visual do estado de expansão. Um [`DataTrigger`](xref:Xamarin.Forms.DataTrigger) pode ser anexado ao `Image`, que altera a `Source` Propriedade com base no valor da `Expander.IsExpanded` Propriedade:

```xaml
<Expander>
    <Expander.Header>
        <Grid>
            <Label Text="{Binding Name}"
                   FontAttributes="Bold"
                   FontSize="Medium" />
            <Image Source="expand.png"
                   HorizontalOptions="End"
                   VerticalOptions="Start">
                <Image.Triggers>
                    <DataTrigger TargetType="Image"
                                 Binding="{Binding Source={RelativeSource AncestorType={x:Type Expander}}, Path=IsExpanded}"
                                 Value="True">
                        <Setter Property="Source"
                                Value="collapse.png" />
                    </DataTrigger>
                </Image.Triggers>
            </Image>
        </Grid>
    </Expander.Header>
    <Expander.ContentTemplate>
        <DataTemplate>
            <Grid Padding="10">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="Auto" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <Image Source="{Binding ImageUrl}"
                       Aspect="AspectFill"
                       HeightRequest="120"
                       WidthRequest="120" />
                <Label Grid.Column="1"
                       Text="{Binding Details}"
                       FontAttributes="Italic" />
            </Grid>
        </DataTemplate>
    </Expander.ContentTemplate>
</Expander>
```

Neste exemplo, o [`Image`](xref:Xamarin.Forms.Image) exibe o `expand` ícone por padrão:

![Captura de tela de um ícone de expansor no estado recolhido, no iOS e no Android](expander-images/icon-expand.png "Ícone expandido no iOS e no Android")

A `IsExpanded` Propriedade se `true` torna quando `Expander` o cabeçalho é tocado, o que resulta `collapse` no ícone que está sendo exibido:

![Captura de tela de um ícone de expansor no estado de expansão, no iOS e no Android](expander-images/icon-collapse.png "Ícone expandido no iOS e no Android")

Para obter mais informações sobre gatilhos, consulte [gatilhos do Xamarin. Forms](~/xamarin-forms/app-fundamentals/triggers.md).

## <a name="define-the-space-between-header-and-content"></a>Definir o espaço entre o cabeçalho e o conteúdo

Por padrão, o conteúdo em um `Expander` aparece diretamente abaixo de seu cabeçalho. No entanto, esse comportamento pode ser alterado definindo `Spacing` a propriedade como `double` um valor que representa o espaço vazio entre o conteúdo e seu cabeçalho:

```xaml
<Expander Spacing="50"
          IsExpanded="true">
    <Expander.Header>
        <Label Text="Baboon"
               FontAttributes="Bold"
               FontSize="Medium" />
    </Expander.Header>
    <Grid Padding="10">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" />
            <ColumnDefinition Width="Auto" />
        </Grid.ColumnDefinitions>
        <Image Source="http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg"
               Aspect="AspectFill"
               HeightRequest="120"
               WidthRequest="120" />
        <Label Grid.Column="1"
               Text="Baboons are African and Arabian Old World monkeys belonging to the genus Papio, part of the subfamily Cercopithecinae."
               FontAttributes="Italic" />
    </Grid>
</Expander>
```

Neste exemplo, o `Expander` conteúdo aparece 50 unidades independentes de dispositivo abaixo de seu cabeçalho:

![Captura de tela de um expansor com conjunto de espaçamento, no iOS e no Android](expander-images/expander-spacing.png "Expansor com espaçamento definido no iOS e no Android")

## <a name="embed-an-expander-in-an-expander"></a>Inserir um expansor em um expansor

O conteúdo de um `Expander` pode ser definido para outro `Expander` controle, para habilitar vários níveis de expansão. O XAML a seguir mostra `Expander` um cujo conteúdo é `Expander` outro objeto:

```xaml
<Expander Spacing="10">
    <Expander.Header>
        <Label Text="{Binding Name}"
               FontAttributes="Bold"
               FontSize="Medium" />
    </Expander.Header>
    <Expander Padding="10"
              Spacing="10">
        <Expander.Header>
            <Label Text="{Binding Location}"
                   FontSize="Medium" />
        </Expander.Header>
            <Expander.ContentTemplate>
                <DataTemplate>
                    <Grid>
                        <Grid.ColumnDefinitions>
                            <ColumnDefinition Width="Auto" />
                            <ColumnDefinition Width="Auto" />
                        </Grid.ColumnDefinitions>
                        <Image Source="{Binding ImageUrl}"
                               Aspect="AspectFill"
                               HeightRequest="120"
                               WidthRequest="120" />
                        <Label Grid.Column="1"
                               Text="{Binding Details}"
                               FontAttributes="Italic" />
                    </Grid>
                </DataTemplate>
            </Expander.ContentTemplate>
    </Expander>
</Expander>
```

Neste exemplo, tocar no cabeçalho raiz `Expander` revela o cabeçalho para o filho `Expander`:

![Captura de tela de um expansor inserido, no iOS e no Android](expander-images/embedded-expander1.png "Expansor inserido no iOS e no Android")

Tocar no cabeçalho `Expander` filho faz com que seu conteúdo seja inalterado e exibido:

![Captura de tela de um expansor inserido, no iOS e no Android](expander-images/embedded-expander2.png "Expansor inserido no iOS e no Android")

## <a name="define-the-expand-and-collapse-animation"></a>Definir a animação de expandir e recolher

A animação que ocorre quando um `Expander` expande ou recolhe pode ser definida definindo as `ExpandAnimationEasing` Propriedades e `CollapseAnimationEasing` como qualquer uma das funções de atenuação incluídas no Xamarin. Forms ou nas funções de atenuação personalizadas. Por padrão, as animações expandir e recolher ocorrem em 250 MS. No entanto, essas durações podem ser alteradas definindo `ExpandAnimationLength` as `CollapseAnimationLength` Propriedades e `uint` como valores.

O XAML a seguir mostra um exemplo de como definir a animação que ocorre `Expander` quando o é expandido ou recolhido pelo usuário:

```xaml
<Expander ExpandAnimationEasing="{x:Static Easing.CubicIn}"
          ExpandAnimationLength="500"
          CollapseAnimationEasing="{x:Static Easing.CubicOut}"
          CollapseAnimationLength="500">
    <Expander.Header>
        <Label Text="{Binding Name}"
               FontAttributes="Bold"
               FontSize="Medium" />
    </Expander.Header>
    <Expander.ContentTemplate>
        <DataTemplate>
            <Grid Padding="10">
                <Grid.ColumnDefinitions>
                    <ColumnDefinition Width="Auto" />
                    <ColumnDefinition Width="Auto" />
                </Grid.ColumnDefinitions>
                <Image Source="{Binding ImageUrl}"
                       Aspect="AspectFill"
                       HeightRequest="120"
                       WidthRequest="120" />
                <Label Grid.Column="1"
                       Text="{Binding Details}"
                       FontAttributes="Italic" />
            </Grid>
        </DataTemplate>
    </Expander.ContentTemplate>
</Expander>
```

Neste exemplo, a função `CubicIn` de atenuação acelera lentamente a animação de expansão em 500 MS e a `CubicOut` função de atenuação reduz rapidamente a animação de recolhimento em 500 ms.

Para saber mais sobre as funções de atenuação, confira [funções de atenuação do Xamarin. Forms](~/xamarin-forms/user-interface/animation/easing.md).

## <a name="resize-an-expander-at-runtime"></a>Redimensionar um expansor em tempo de execução

Um `Expander` pode ser redimensionado programaticamente em tempo `ForceUpdateSize` de execução com o método.

Dado um `Expander` nome `expander`, cujo conteúdo inclui um [`Label`](xref:Xamarin.Forms.Label) que tem um `TapGestureRecognizer` anexado a ele, o exemplo de código a seguir mostra `ForceUpdateSize` a chamada do método:

```csharp
void OnLabelTapped(object sender, EventArgs e)
{
    Label label = sender as Label;
    Expander expander = label.Parent.Parent.Parent as Expander;

    if (label.FontSize == Device.GetNamedSize(NamedSize.Default, label))
    {
        label.FontSize = Device.GetNamedSize(NamedSize.Large, label);
    }
    else
    {
        label.FontSize = Device.GetNamedSize(NamedSize.Default, label);
    }
    expander.ForceUpdateSize();
}
```

Neste exemplo, o `FontSize` de uma [`Label`](xref:Xamarin.Forms.Label) alteração quando o `Label` é tocado. Devido ao tamanho da fonte em alteração, é necessário atualizar o tamanho do `Expander` chamando seu `ForceUpdateSize` método.

## <a name="disable-an-expander"></a>Desabilitar um expansor

Um aplicativo pode inserir um estado em que a `Expander` expansão de uma não é uma operação válida. Nesses casos, o `Expander` pode ser desabilitado definindo sua `IsEnabled` Propriedade como false. Isso impedirá que os usuários expandam ou `Expander`recolham o.

## <a name="related-links"></a>Links relacionados

- [Demonstrações do expansor (exemplo)](https://docs.microsoft.com/samples/xamarin/xamarin-forms-samples/userinterface-expanderdemos/)
- [Funções de atenuação do Xamarin. Forms](~/xamarin-forms/user-interface/animation/easing.md)
- [Gatilhos do Xamarin.Forms](~/xamarin-forms/app-fundamentals/triggers.md)
- [Layouts vinculáveis do Xamarin. Forms](~/xamarin-forms/user-interface/layouts/bindable-layouts.md)