---
title: Agrupamento de CollectionView do Xamarin. Forms
description: CollectionView pode exibir dados agrupados corretamente definindo sua propriedade isgroupd como true.
ms.prod: xamarin
ms.assetid: 7E494245-FDBD-49D6-B7FA-CEF976EB59BB
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 07/24/2019
ms.openlocfilehash: 8fd37999428c2813bbf96de3bcbd6ebd1fe0879d
ms.sourcegitcommit: 5f972a757030a1f17f99177127b4b853816a1173
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2019
ms.locfileid: "69894023"
---
# <a name="xamarinforms-collectionview-grouping"></a>Agrupamento de CollectionView do Xamarin. Forms

![](~/media/shared/preview.png "Esta API está atualmente em pré-lançamento")

[![Baixar Exemplo](~/media/shared/download.png) Baixar o exemplo](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/CollectionViewDemos)

Conjuntos de dados grandes geralmente podem se tornar difíceis quando apresentados em uma lista de rolagem contínua. Nesse cenário, organizar os dados em grupos pode melhorar a experiência do usuário, facilitando a navegação dos dados.

[`CollectionView`](xref:Xamarin.Forms.CollectionView)dá suporte à exibição de dados agrupados e define as seguintes propriedades que controlam como ele será apresentado:

- `IsGrouped`, do tipo `bool`, indica se os dados subjacentes devem ser exibidos em grupos. O valor padrão dessa propriedade é `false`.
- `GroupHeaderTemplate`, do tipo [`DataTemplate`](xref:Xamarin.Forms.DataTemplate), o modelo a ser usado para o cabeçalho de cada grupo.
- `GroupFooterTemplate`, do tipo [`DataTemplate`](xref:Xamarin.Forms.DataTemplate), o modelo a ser usado para o rodapé de cada grupo.

Essas propriedades são apoiadas por [`BindableProperty`](xref:Xamarin.Forms.BindableProperty) objetos, o que significa que as propriedades podem ser destinos de associações de dados.

Para obter mais informações sobre modelos de dados, confira [Modelos de dados do Xamarin.Forms](~/xamarin-forms/app-fundamentals/templates/data-templates/index.md).

> [!IMPORTANT]
> O agrupamento de [`CollectionView`](xref:Xamarin.Forms.CollectionView) dados com o atualmente só tem suporte no Ios.

## <a name="group-data"></a>Agrupar dados

Os dados devem ser agrupados para que possam ser exibidos. Isso pode ser feito criando uma lista de grupos, onde cada grupo é uma lista de itens. A lista de grupos deve ser uma `IEnumerable<T>` coleção, em `T` que define dois tipos de dados:

- Um nome de grupo.
- Uma `IEnumerable` coleção que define os itens que pertencem ao grupo.

O processo de agrupamento de dados, portanto, é:

- Crie um tipo que modela um único item.
- Crie um tipo que modela um único grupo de itens.
- Crie uma `IEnumerable<T>` coleção, em `T` que é o tipo que modela um único grupo de itens. Essa coleção é, portanto, uma coleção de grupos, que armazena os dados agrupados.
- Adicione dados à `IEnumerable<T>` coleção.

### <a name="example"></a>Exemplo

Ao agrupar dados, a primeira etapa é criar um tipo que modela um único item. O exemplo a seguir mostra `Animal` a classe do aplicativo de exemplo:

```csharp
public class Animal
{
    public string Name { get; set; }
    public string Location { get; set; }
    public string Details { get; set; }
    public string ImageUrl { get; set; }
}
```

A `Animal` classe modela um único item. Um tipo que modela um grupo de itens pode ser criado. O exemplo a seguir mostra `AnimalGroup` a classe do aplicativo de exemplo:

```csharp
public class AnimalGroup : List<Animal>
{
    public string Name { get; private set; }

    public AnimalGroup(string name, List<Animal> animals) : base(animals)
    {
        Name = name;
    }
}
```

A `AnimalGroup` classe herda `List<T>` da classe e adiciona uma `Name` propriedade que representa o nome do grupo.

Uma `IEnumerable<T>` coleção de grupos pode ser criada:

```csharp
public List<AnimalGroup> Animals { get; private set; } = new List<AnimalGroup>();
```

Esse código define uma coleção chamada `Animals`, onde cada item na coleção é um `AnimalGroup` objeto. Cada `AnimalGroup` objeto consiste em um nome e uma `List<Animal>` coleção que define os `Animal` objetos no grupo.

Os dados agrupados podem ser adicionados à `Animals` coleção:

```csharp
Animals.Add(new AnimalGroup("Bears", new List<Animal>
{
    new Animal
    {
        Name = "American Black Bear",
        Location = "North America",
        Details = "Details about the bear go here.",
        ImageUrl = "https://upload.wikimedia.org/wikipedia/commons/0/08/01_Schwarzbär.jpg"
    },
    new Animal
    {
        Name = "Asian Black Bear",
        Location = "Asia",
        Details = "Details about the bear go here.",
        ImageUrl = "https://upload.wikimedia.org/wikipedia/commons/thumb/b/b7/Ursus_thibetanus_3_%28Wroclaw_zoo%29.JPG/180px-Ursus_thibetanus_3_%28Wroclaw_zoo%29.JPG"
    },
    // ...
}));

Animals.Add(new AnimalGroup("Monkeys", new List<Animal>
{
    new Animal
    {
        Name = "Baboon",
        Location = "Africa & Asia",
        Details = "Details about the monkey go here.",
        ImageUrl = "http://upload.wikimedia.org/wikipedia/commons/thumb/f/fc/Papio_anubis_%28Serengeti%2C_2009%29.jpg/200px-Papio_anubis_%28Serengeti%2C_2009%29.jpg"
    },
    new Animal
    {
        Name = "Capuchin Monkey",
        Location = "Central & South America",
        Details = "Details about the monkey go here.",
        ImageUrl = "http://upload.wikimedia.org/wikipedia/commons/thumb/4/40/Capuchin_Costa_Rica.jpg/200px-Capuchin_Costa_Rica.jpg"
    },
    new Animal
    {
        Name = "Blue Monkey",
        Location = "Central and East Africa",
        Details = "Details about the monkey go here.",
        ImageUrl = "http://upload.wikimedia.org/wikipedia/commons/thumb/8/83/BlueMonkey.jpg/220px-BlueMonkey.jpg"
    },
    // ...
}));
```

Esse código cria dois grupos na `Animals` coleção. O primeiro `AnimalGroup` é chamado `Bears`e contém uma `List<Animal>` coleção de detalhes de Bear. O segundo `AnimalGroup` é chamado `Monkeys`e contém uma `List<Animal>` coleção de detalhes de macaco.

## <a name="display-grouped-data"></a>Exibir dados agrupados

[`CollectionView`](xref:Xamarin.Forms.CollectionView)exibirá os dados agrupados, desde que os dados tenham sido agrupados corretamente, definindo a `IsGrouped` Propriedade como `true`:

```xaml
<CollectionView ItemsSource="{Binding Animals}"
                IsGrouped="true">
    <CollectionView.ItemTemplate>
        <DataTemplate>
            <Grid Padding="10">
                ...
                <Image Grid.RowSpan="2"
                       Source="{Binding ImageUrl}"
                       Aspect="AspectFill"
                       HeightRequest="60"
                       WidthRequest="60" />
                <Label Grid.Column="1"
                       Text="{Binding Name}"
                       FontAttributes="Bold" />
                <Label Grid.Row="1"
                       Grid.Column="1"
                       Text="{Binding Location}"
                       FontAttributes="Italic"
                       VerticalOptions="End" />
            </Grid>
        </DataTemplate>
    </CollectionView.ItemTemplate>
</CollectionView>
```

O código C# equivalente é:

```csharp
CollectionView collectionView = new CollectionView
{
    IsGrouped = true
};
collectionView.SetBinding(ItemsView.ItemsSourceProperty, "Animals");
// ...
```

A aparência de cada item no [`CollectionView`](xref:Xamarin.Forms.CollectionView) é definida pela definição da [`CollectionView.ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate) Propriedade como [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)a. Para obter mais informações, consulte [definir a aparência do item](~/xamarin-forms/user-interface/collectionview/populate-data.md#define-item-appearance).

> [!NOTE]
> Por padrão, [`CollectionView`](xref:Xamarin.Forms.CollectionView) o exibirá o nome do grupo no cabeçalho e no rodapé do grupo. Esse comportamento pode ser alterado Personalizando o cabeçalho do grupo e o rodapé do grupo.

## <a name="customize-the-group-header"></a>Personalizar o cabeçalho do grupo

A aparência de cada cabeçalho de grupo pode ser personalizada definindo a `CollectionView.GroupHeaderTemplate` propriedade [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)como a:

```xaml
<CollectionView ItemsSource="{Binding Animals}"
                IsGrouped="true">
    ...
    <CollectionView.GroupHeaderTemplate>
        <DataTemplate>
            <Label Text="{Binding Name}"
                   BackgroundColor="LightGray"
                   FontSize="Large"
                   FontAttributes="Bold" />
        </DataTemplate>
    </CollectionView.GroupHeaderTemplate>
</CollectionView>
```

Neste exemplo, cada cabeçalho de grupo é definido como um [`Label`](xref:Xamarin.Forms.Label) que exibe o nome do grupo e que tem outras propriedades de aparência definidas.

## <a name="customize-the-group-footer"></a>Personalizar o rodapé do grupo

A aparência de cada rodapé de grupo pode ser personalizada definindo a `CollectionView.GroupFooterTemplate` propriedade [`DataTemplate`](xref:Xamarin.Forms.DataTemplate)como a:

```xaml
<CollectionView ItemsSource="{Binding Animals}"
                IsGrouped="true">
    ...
    <CollectionView.GroupFooterTemplate>
        <DataTemplate>
            <Label Text="{Binding Count, StringFormat='Total animals: {0:D}'}"
                   Margin="0,0,0,10" />
        </DataTemplate>
    </CollectionView.GroupFooterTemplate>
</CollectionView>
```

Neste exemplo, cada rodapé de grupo é definido como um [`Label`](xref:Xamarin.Forms.Label) que exibe o número de itens no grupo.

## <a name="empty-groups"></a>Grupos vazios

Quando um [`CollectionView`](xref:Xamarin.Forms.CollectionView) exibe dados agrupados, ele exibirá todos os grupos vazios. Esses grupos serão exibidos com um cabeçalho e um rodapé de grupo, indicando que o grupo está vazio.

> [!NOTE]
> No iOS 10 e inferior, os cabeçalhos e rodapés de grupo de grupos vazios podem ser exibidos na parte superior do `CollectionView`.

## <a name="group-without-templates"></a>Grupo sem modelos

[`CollectionView`](xref:Xamarin.Forms.CollectionView)pode exibir dados agrupados corretamente sem definir a [`CollectionView.ItemTemplate`](xref:Xamarin.Forms.ItemsView.ItemTemplate) Propriedade como um [`DataTemplate`](xref:Xamarin.Forms.DataTemplate):

```xaml
<CollectionView ItemsSource="{Binding Animals}"
                IsGrouped="true" />
```

Nesse cenário, dados significativos podem ser exibidos substituindo o `ToString` método no tipo que modela um único item e o tipo que modela um único grupo de itens.

## <a name="related-links"></a>Links relacionados

- [CollectionView (exemplo)](https://github.com/xamarin/xamarin-forms-samples/tree/master/UserInterface/CollectionViewDemos/)
- [Modelos de dados do Xamarin. Forms](~/xamarin-forms/app-fundamentals/templates/data-templates/index.md)