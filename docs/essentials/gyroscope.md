---
title: Xamarin.Essentials giroscópio
description: A classe giroscópio permite monitorar o sensor de giroscópio do dispositivo que é a rotação em torno de três eixos de principal do dispositivo.
ms.assetid: DA4F968A-D988-41F5-8745-1BEE693660A1
ms.technology: xamarin-crossplatform
author: jamesmontemagno
ms.author: jamont
ms.date: 05/04/2018
ms.openlocfilehash: 586c8446df2f84070925faee2fc851657f32a2ab
ms.sourcegitcommit: 46d3c9daa45350bdd536d9e105517f3c1c753c5b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
---
# <a name="xamarinessentials-gyroscope"></a>Xamarin.Essentials giroscópio

![Pré-lançamento NuGet](~/media/shared/pre-release.png)

O **giroscópio** classe permite que você monitore o sensor de giroscópio do dispositivo que é a rotação em torno de três eixos de principal do dispositivo.

## <a name="using-gyroscope"></a>Usando giroscópio

Adicione uma referência a Xamarin.Essentials em sua classe:

```csharp
using Xamarin.Essentials;
```

A funcionalidade de giroscópio funciona chamando o `Start` e `Stop` métodos para escuta de alterações para o giroscópio. As alterações são enviadas através de `ReadingChanged` eventos. Aqui está o exemplo de uso:

```csharp

public class GyroscopeTest
{
    // Set speed delay for monitoring changes.
    SensorSpeed speed = SensorSpeed.Ui;

    public GyroscopeTest()
    {
        // Register for reading changes.
        Gyroscope.ReadingChanged += Gyroscope_ReadingChanged;
    }

    void Gyroscope_ReadingChanged(GyroscopeChangedEventArgs e)
    {
        var data = e.Reading;
        // Process Angular Velocity X, Y, and Z
        Console.WriteLine($"Reading: X: {data.AngularVelocity.X}, Y: {data.AngularVelocity.Y}, Z: {data.AngularVelocity.Z}");
    }

    public void ToggleGyroscope()
    {
        try
        {
            if (Gyroscope.IsMonitoring)
              Gyroscope.Stop();
            else
              Gyroscope.Start(speed);
        }
        catch (FeatureNotSupportedException fnsEx)
        {
            // Feature not supported on device
        }
        catch (Exception ex)
        {
            // Other error has occurred.
        }
    }
}
```

## <a name="sensor-speedxrefxamarinessentialssensorspeed"></a>[Sensor de velocidade](xref:Xamarin.Essentials.SensorSpeed)

- **Mais rápido** – obter os dados de sensor mais rápido possível (não é garantido para retornar no thread de interface do usuário).
- **Jogo** – taxa adequado para jogos (não é garantidos para retornar no thread de interface do usuário).
- **Normal** – taxa padrão adequada para alterações de orientação da tela.
- **Interface do usuário** – taxa adequado para a interface de usuário geral.

## <a name="api"></a>API

- [Código-fonte giroscópio](https://github.com/xamarin/Essentials/tree/master/Essentials/Gyroscope)
- [Documentação da API do giroscópio](xref:Xamarin.Essentials.Gyroscope)