---
title: ListView
description: "ListView é um componente importante da interface do usuário dos aplicativos do Android; ele é usado em qualquer lugar da lista curta de opções de menu para listas longas de contatos ou Favoritos do internet. Ele fornece uma maneira simples para apresentar uma lista de rolagem de linhas que pode ser formatado com um estilo interno ou personalizado extensivamente."
ms.topic: article
ms.prod: xamarin
ms.assetid: C2BA2705-9B20-01C2-468D-860BDFEDC157
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/06/2018
ms.openlocfilehash: 70a7abb186c102fb803c0ab6fa38c7b2d8222292
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="listview"></a>ListView

_ListView é um componente importante da interface do usuário dos aplicativos do Android; ele é usado em qualquer lugar da lista curta de opções de menu para listas longas de contatos ou Favoritos do internet. Ele fornece uma maneira simples para apresentar uma lista de rolagem de linhas que pode ser formatado com um estilo interno ou personalizado extensivamente._

<a name="overview" />

## <a name="overview"></a>Visão geral

Adaptadores e modos de exibição de lista são incluídas em blocos de construção mais importantes de aplicativos do Android. O `ListView` classe fornece um modo flexível para apresentar dados, seja um menu curto ou uma lista de rolagem longa. Ele fornece recursos de usabilidade como índices de rolagem, rápidos e seleção de uma ou vários para ajudá-lo a criar interfaces do usuário de dispositivos móveis para seus aplicativos. A instância `ListView` requer um *Adaptador* para fornecer a ela dados contidos nas exibições de linha.

Este guia explica como implementar `ListView` e os diversos `Adapter` classes no xamarin. Ele também demonstra como personalizar a aparência de um `ListView`, e ele discute a importância da linha reutilização para reduzir o consumo de memória. Também há algumas discussão de como o ciclo de vida da atividade afeta `ListView` e `Adapter` usar. Se você estiver trabalhando em aplicativos de plataforma cruzada com xamarin, o `ListView` controle é estruturalmente similar do iOS `UITableView` (e o Android `Adapter` é semelhante de `UITableViewSource`).

Primeiro, um breve tutorial apresenta o `ListView` com um exemplo de código básico. Em seguida, os links para tópicos mais avançados são fornecidos para ajudá-lo a usar `ListView` em aplicativos do mundo real.


> [!NOTE]
> **Observação**: O `RecyclerView` widget é uma versão mais avançada e flexível de `ListView`. Porque `RecyclerView` foi projetado para ser o sucessor `ListView` (e `GridView`), é recomendável que você use `RecyclerView` em vez de `ListView` para novo desenvolvimento de aplicativos. Para obter mais informações, consulte [RecyclerView](~/android/user-interface/layouts/recycler-view/index.md).


<a name="tutorial" />

## <a name="listview-tutorial"></a>Tutorial de ListView

[`ListView`](https://developer.xamarin.com/api/type/Android.Widget.ListView/) é um [ `ViewGroup` ](https://developer.xamarin.com/api/type/Android.Views.ViewGroup/) que cria uma lista de itens roláveis. Os itens da lista são inseridos automaticamente à lista usando um [ `IListAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.IListAdapter/).

Neste tutorial, você criará uma lista de rolagem de nomes de país que são lidos a partir de uma matriz de cadeia de caracteres. Quando um item de lista é selecionado, será exibida uma mensagem de notificação do sistema a posição do item na lista.


Iniciar um novo projeto denominado **HelloListView**.

Criar um arquivo XML denominado **list_item.xml** e salvá-lo dentro de **recursos/Layout/** pasta. Insira o seguinte:

```xml
<?xml version="1.0" encoding="utf-8"?>
<TextView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:padding="10dp"
    android:textSize="16sp">
</TextView>
```

Esse arquivo define o layout para cada item que será colocada no [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/).

Abra o `HelloListView.cs` e fazer com que a classe estender [ `ListActivity` ](https://developer.xamarin.com/api/type/Android.App.ListActivity/) (em vez de [ `Activity` ](https://developer.xamarin.com/api/type/Android.App.Activity/)):

```csharp
public class HelloListView : ListActivity
{
```

Insira o seguinte código para o [ `OnCreate()` ](https://developer.xamarin.com/api/member/Android.App.Activity.OnCreate/(Android.OS.Bundle)) método:

```csharp
protected override void OnCreate (Bundle bundle)
{
    base.OnCreate (bundle);

    ListAdapter = new ArrayAdapter<string> (this, Resource.Layout.list_item, countries);

    ListView.TextFilterEnabled = true;

    ListView.ItemClick += delegate (object sender, ItemEventArgs args) {
        // When clicked, show a toast with the TextView text
        Toast.MakeText (Application, ((TextView)args.View).Text, ToastLength.Short).Show ();
    };
}
```

Observe que isso não carregar um arquivo de layout para a atividade (que geralmente faz com [ `SetContentView(int)` ](https://developer.xamarin.com/api/member/Android.App.Activity.SetContentView/(System.Int32))).
Em vez disso, definindo o [ `ListAdapter` ](https://developer.xamarin.com/api/property/Android.App.ListActivity.ListAdapter/) propriedade adiciona automaticamente um [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/) para preencher a tela inteira do [ `ListActivity` ](https://developer.xamarin.com/api/type/Android.App.ListActivity/).
Esse método usa um [ `ArrayAdapter<T>` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter%601/), que gerencia a matriz de itens de lista que serão colocados no [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/).
O [ `ArrayAdapter<T>` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter%601/) construtor usa o aplicativo [ `Context` ](https://developer.xamarin.com/api/type/Android.Content.Context/), a descrição de layout para cada item de lista (criado na etapa anterior) e um `T[]` ou [ `Java.Util.IList<T>` ](https://developer.xamarin.com/api/type/Java.Util.IList/) matriz de objetos para inserir no [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/) (definido em seguida).

O [ `TextFilterEnabled` ](https://developer.xamarin.com/api/property/Android.Widget.AbsListView.TextFilterEnabled/) ativa de propriedade de texto de filtragem para o [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/), de modo que quando o usuário começa a digitar, a lista será filtrada.

O [ `ItemClick` ](https://developer.xamarin.com/api/event/Android.Widget.AdapterView.ItemClick/) evento pode ser usado para assinar manipuladores de cliques. Quando um item de [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/) é clicado, o manipulador é chamado e uma [ `Toast` ](https://developer.xamarin.com/api/type/Android.Widget.Toast/) mensagem é exibida, usando o texto do item clicado.

Você pode usar os designs de item de lista fornecidos pela plataforma em vez de definir seu próprio arquivo de layout para o [ `ListAdapter` ](https://developer.xamarin.com/api/property/Android.App.ListActivity.ListAdapter/).
Por exemplo, tente usar `Android.Resource.Layout.SimpleListItem1` em vez de `Resource.Layout.list_item`.

Após o [ `OnCreate()` ](https://developer.xamarin.com/api/member/Android.App.Activity.OnCreate/(Android.OS.Bundle)) método, adicione a matriz de cadeia de caracteres:

```csharp
static readonly string[] countries = new String[] {
    "Afghanistan","Albania","Algeria","American Samoa","Andorra",
    "Angola","Anguilla","Antarctica","Antigua and Barbuda","Argentina",
    "Armenia","Aruba","Australia","Austria","Azerbaijan",
    "Bahrain","Bangladesh","Barbados","Belarus","Belgium",
    "Belize","Benin","Bermuda","Bhutan","Bolivia",
    "Bosnia and Herzegovina","Botswana","Bouvet Island","Brazil","British Indian Ocean Territory",
    "British Virgin Islands","Brunei","Bulgaria","Burkina Faso","Burundi",
    "Cote d'Ivoire","Cambodia","Cameroon","Canada","Cape Verde",
    "Cayman Islands","Central African Republic","Chad","Chile","China",
    "Christmas Island","Cocos (Keeling) Islands","Colombia","Comoros","Congo",
    "Cook Islands","Costa Rica","Croatia","Cuba","Cyprus","Czech Republic",
    "Democratic Republic of the Congo","Denmark","Djibouti","Dominica","Dominican Republic",
    "East Timor","Ecuador","Egypt","El Salvador","Equatorial Guinea","Eritrea",
    "Estonia","Ethiopia","Faeroe Islands","Falkland Islands","Fiji","Finland",
    "Former Yugoslav Republic of Macedonia","France","French Guiana","French Polynesia",
    "French Southern Territories","Gabon","Georgia","Germany","Ghana","Gibraltar",
    "Greece","Greenland","Grenada","Guadeloupe","Guam","Guatemala","Guinea","Guinea-Bissau",
    "Guyana","Haiti","Heard Island and McDonald Islands","Honduras","Hong Kong","Hungary",
    "Iceland","India","Indonesia","Iran","Iraq","Ireland","Israel","Italy","Jamaica",
    "Japan","Jordan","Kazakhstan","Kenya","Kiribati","Kuwait","Kyrgyzstan","Laos",
    "Latvia","Lebanon","Lesotho","Liberia","Libya","Liechtenstein","Lithuania","Luxembourg",
    "Macau","Madagascar","Malawi","Malaysia","Maldives","Mali","Malta","Marshall Islands",
    "Martinique","Mauritania","Mauritius","Mayotte","Mexico","Micronesia","Moldova",
    "Monaco","Mongolia","Montserrat","Morocco","Mozambique","Myanmar","Namibia",
    "Nauru","Nepal","Netherlands","Netherlands Antilles","New Caledonia","New Zealand",
    "Nicaragua","Niger","Nigeria","Niue","Norfolk Island","North Korea","Northern Marianas",
    "Norway","Oman","Pakistan","Palau","Panama","Papua New Guinea","Paraguay","Peru",
    "Philippines","Pitcairn Islands","Poland","Portugal","Puerto Rico","Qatar",
    "Reunion","Romania","Russia","Rwanda","Sqo Tome and Principe","Saint Helena",
    "Saint Kitts and Nevis","Saint Lucia","Saint Pierre and Miquelon",
    "Saint Vincent and the Grenadines","Samoa","San Marino","Saudi Arabia","Senegal",
    "Seychelles","Sierra Leone","Singapore","Slovakia","Slovenia","Solomon Islands",
    "Somalia","South Africa","South Georgia and the South Sandwich Islands","South Korea",
    "Spain","Sri Lanka","Sudan","Suriname","Svalbard and Jan Mayen","Swaziland","Sweden",
    "Switzerland","Syria","Taiwan","Tajikistan","Tanzania","Thailand","The Bahamas",
    "The Gambia","Togo","Tokelau","Tonga","Trinidad and Tobago","Tunisia","Turkey",
    "Turkmenistan","Turks and Caicos Islands","Tuvalu","Virgin Islands","Uganda",
    "Ukraine","United Arab Emirates","United Kingdom",
    "United States","United States Minor Outlying Islands","Uruguay","Uzbekistan",
    "Vanuatu","Vatican City","Venezuela","Vietnam","Wallis and Futuna","Western Sahara",
    "Yemen","Yugoslavia","Zambia","Zimbabwe"
  };
```

Isso é a matriz de cadeias de caracteres que serão colocados no [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/).

Execute o aplicativo. Role a lista ou digite para filtrar a ele e clique em um item para ver uma mensagem. Você deve ver algo parecido com isso:

[ ![Captura de tela de exemplo de ListView com nomes de país](images/helloviews6.png)](images/helloviews6.png)

Observe que o uso de uma matriz de cadeia de caracteres codificada não é a prática recomendada de design. Um é usado neste tutorial para simplificar, para demonstrar o [ `ListView` ](https://developer.xamarin.com/api/type/Android.Widget.ListView/) widget. A melhor prática é fazer referência a uma matriz de cadeia de caracteres definida por um recurso externo, como com um `string-array` recursos em seu projeto **Resources/Values/Strings.xml** arquivo. Por exemplo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string-array name="countries_array">
        <item>Bahrain</item>
        <item>Bangladesh</item>
        <item>Barbados</item>
        <item>Belarus</item>
        <item>Belgium</item>
        <item>Belize</item>
        <item>Benin</item>
    </string-array>
</resources>
```

Para usar essas cadeias de caracteres de recurso para o [ `ArrayAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter%601/), substitua o original [ `ListAdapter` ](https://developer.xamarin.com/api/property/Android.App.ListActivity.ListAdapter/) linha com o seguinte:

```csharp
string[] countries = Resources.GetStringArray (Resource.Array.countries_array);
ListAdapter = new ArrayAdapter<string> (this, Resource.Layout.list_item, countries);
```

<a name="going_further" />

## <a name="going-further-with-listview"></a>Continuar com ListView

Os tópicos restantes (vinculados abaixo) dar uma olhada abrangente trabalhando com o `ListView` classe e os diferentes tipos de tipos de adaptadores que você pode usar com ele. A estrutura é a seguinte:

-   **Aparência** &ndash; partes do `ListView` controle e como elas funcionam.

-   **Classes de** &ndash; visão geral das classes usadas para exibir um `ListView`.

-   **Exibindo dados em uma ListView** &ndash; como exibir uma lista simple de dados; como implementar `ListView's` recursos de usabilidade; como usar linha internas diferentes layouts; e como adaptadores economizar memória reutilizando os modos de exibição de linha.

-   **Aparência personalizada** &ndash; alterando o estilo da `ListView` com layouts personalizados, fontes e cores.

-   **Usando SQLite** &ndash; como exibir dados de um banco de dados SQLite com um `CursorAdapter`.

-   **Ciclo de vida da atividade** &ndash; considerações de Design ao implementar `ListView` atividades, incluindo onde, no ciclo de vida, você deve preencher seus dados e quando liberar recursos.

A discussão (dividida em seis partes) começa com uma visão geral do `ListView` própria classe antes de introduzir progressivamente mais complexos exemplos de como usá-lo.

-   [Funcionalidade e partes de ListView](~/android/user-interface/layouts/list-view/parts-and-functionality.md)
-   [Preenchendo uma ListView com dados](~/android/user-interface/layouts/list-view/populating.md)
-   [Personalizando a aparência de um ListView](~/android/user-interface/layouts/list-view/customizing-appearance.md)
-   [Usando CursorAdapters](~/android/user-interface/layouts/list-view/cursor-adapters.md)
-   [Usando um ContentProvider](~/android/user-interface/layouts/list-view/content-provider.md)
-   [ListView e o ciclo de vida da atividade](~/android/user-interface/layouts/list-view/activity-lifecycle.md)

<a name="summary" />

## <a name="summary"></a>Resumo

Este conjunto de tópicos introduzido `ListView` e fornecidos alguns exemplos de como usar os recursos internos do `ListActivity`. Ele discutido implementações personalizadas de `ListView` permitido para layouts coloridos e usando um banco de dados SQLite e tocadas brevemente na relevância do ciclo de vida da atividade seu `ListView` implementação.


## <a name="related-links"></a>Links relacionados

- [AccessoryViews (exemplo)](https://developer.xamarin.com/samples/AccessoryViews/)
- [BasicTableAndroid (sample)](https://developer.xamarin.com/samples/BasicTableAndroid/)
- [BasicTableAdapter (exemplo)](https://developer.xamarin.com/samples/BasicTableAdapter/)
- [BuiltInViews (sample)](https://developer.xamarin.com/samples/BuiltInViews/)
- [CustomRowView (exemplo)](https://developer.xamarin.com/samples/CustomRowView/)
- [FastScroll (exemplo)](https://developer.xamarin.com/samples/FastScroll/)
- [SectionIndex (exemplo)](https://developer.xamarin.com/samples/SectionIndex/)
- [SimpleCursorTableAdapter (exemplo)](https://developer.xamarin.com/samples/SimpleCursorTableAdapter/)
- [CursorTableAdapter (exemplo)](https://developer.xamarin.com/samples/CursorTableAdapter/)
- [Tutorial de ciclo de vida da atividade](~/android/app-fundamentals/activity-lifecycle/index.md)
- [Trabalhar com tabelas e células (xamarin)](~/ios/user-interface/controls/tables/index.md)
- [Referência de classe de ListView](https://developer.xamarin.com/api/type/Android.Widget.ListView/)
- [Referência de classe ListActivity](https://developer.xamarin.com/api/type/Android.App.ListActivity/)
- [Referência de classe BaseAdapter](https://developer.xamarin.com/api/type/Android.Widget.BaseAdapter/)
- [Referência de classe ArrayAdapter](https://developer.xamarin.com/api/type/Android.Widget.ArrayAdapter/)
- [Referência de classe CursorAdapter](https://developer.xamarin.com/api/type/Android.Widget.CursorAdapter/)