---
title: "Solução de problemas"
description: "Condições de erro comuns e como resolvê-los"
ms.topic: article
ms.prod: xamarin
ms.assetid: 63291951-7375-4CBF-BCC3-2E4AD157A2C8
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 04/25/2017
ms.openlocfilehash: 23ebefcbd6114b06c39740b3b56f87aeac0b9a00
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/27/2018
---
# <a name="troubleshooting"></a>Solução de problemas

_Condições de erro comuns e como resolvê-los_

## <a name="error-unable-to-find-a-version-of-xamarinforms-compatible-with"></a>Erro: "não é possível localizar uma versão do xamarin. Forms compatível com..."

Os erros a seguir podem aparecer no **pacote Console** janela ao atualizar todos os pacotes do Nuget em uma solução xamarin. Forms ou em um projeto de aplicativo xamarin. Forms Android:

```csharp
Attempting to resolve dependency 'Xamarin.Android.Support.v7.AppCompat (= 23.3.0.0)'.
Attempting to resolve dependency 'Xamarin.Android.Support.v4 (= 23.3.0.0)'.
Looking for updates for 'Xamarin.Android.Support.v7.MediaRouter'...
Updating 'Xamarin.Android.Support.v7.MediaRouter' from version '23.3.0.0' to '23.3.1.0' in project 'Todo.Droid'.
Updating 'Xamarin.Android.Support.v7.MediaRouter 23.3.0.0' to 'Xamarin.Android.Support.v7.MediaRouter 23.3.1.0' failed.
Unable to find a version of 'Xamarin.Forms' that is compatible with 'Xamarin.Android.Support.v7.MediaRouter 23.3.0.0'.
```

### <a name="what-causes-this-error"></a>O que causa esse erro?

O Visual Studio para Mac (ou o Visual Studio) pode indicar que atualizações estejam disponíveis para o xamarin. Forms Nuget packge *e todas as suas dependências*. Do Xamarin Studio, a solução **pacotes** nó pode ter esta aparência (os números de versão podem ser diferentes):

![](images/updates-available.png "Pasta de pacotes do projeto Android")

Esse erro pode ocorrer se você tentar atualizar _todos os_ os pacotes.

Isso é porque com Android projetos definidos para uma versão de compilação/destino do Android 6.0 (API 23) ou abaixo, xamarin. Forms tem uma dependência de disco rígida em *específico* versões do Android que suportam a pacotes. Embora as versões atualizadas desses pacotes podem estar disponíveis, xamarin. Forms não é necessariamente compatível com eles.

Nesse caso, você deve atualizar _somente_ o **xamarin. Forms** pois isso assegurará que as dependências permanecem em versões compatíveis do pacote. Outros pacotes que você adicionou ao seu projeto também podem ser atualizados individualmente, contanto que eles não fazem com que os pacotes de suporte do Android atualizar.


> [!NOTE]
> Se você estiver usando o xamarin. Forms 2.3.4 ou posterior **e** versão de destino/compilação do seu projeto Android é definido para o Android 7.0 (API 24) ou superior, em seguida, as dependências de disco rígidas mencionadas acima não se aplicam e você pode atualizar o suporte pacotes independentemente do pacote xamarin. Forms.


### <a name="fix-remove-all-packages-and-re-add-xamarinforms"></a>Correção: Remover todos os pacotes e adicionar novamente o xamarin. Forms

Se o **Xamarin.Android.Support** pacotes foram atualizados para versões incompatíveis, a correção mais simples é:

1. Exclua manualmente todos os pacotes do Nuget no projeto do Android, em seguida
2. Adicionar novamente o **xamarin. Forms** pacote.

Isso fará o download automaticamente o *correto* versões dos outros pacotes.

Para ver um vídeo desse processo, consulte a [post fóruns](https://forums.xamarin.com/discussion/comment/170012/#Comment_170012).