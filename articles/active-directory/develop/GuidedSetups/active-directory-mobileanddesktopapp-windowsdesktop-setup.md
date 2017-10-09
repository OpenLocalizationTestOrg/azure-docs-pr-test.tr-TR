---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - Kurulumu | Microsoft Docs"
description: "Windows Masaüstü .NET (XAML) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a>Projenizin kurulumunu

Bu bölümde hakkında adım adım yönergeler sağlar toocreate yeni bir proje toodemonstrate nasıl toointegrate bir Windows Masaüstü .NET uygulama (XAML) ile *Microsoft ile oturum açma* için bir belirteç gerekiyor Web API'leri sorgulayabilirsiniz.

Bu kılavuz tarafından oluşturulan hello uygulama düğmesi toograph ve Göster sonuçları ekran ve oturum kapatma düğmesini gösterir.

> Toodownload, bunun yerine bu örnekte 's Visual Studio projesi tercih ediyorsunuz? [Bir proje indirme](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) ve toohello atla [yapılandırma adımı](#create-an-application-express) yürütmeden önce tooconfigure hello kod örneği.


### <a name="create-your-application"></a>Uygulamanızı oluşturun
1. Visual Studio'da:`File` > `New` > `Project`<br/>
2. Altında *şablonları*seçin`Visual C#`
3. Seçin `WPF App` (veya *WPF uygulaması* , Visual Studio hello sürümüne bağlı olarak)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Merhaba Microsoft kimlik doğrulama kitaplığı (MSAL) tooyour proje ekleyin
1. Visual Studio'da:`Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Kopyalayıp hello aşağıdaki hello Paket Yöneticisi konsol penceresine yapıştırın:

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> Yukarıdaki Hello paketi hello Microsoft kimlik doğrulama kitaplığı (MSAL) yükler. MSAL alınırken, önbelleğe alma ve kullanıcı kullanılan toskens tooaccess tarafından Azure Active Directory v2 korumalı API'leri yenilemeyi işler.

## <a name="add-hello-code-tooinitialize-msal"></a>Merhaba kod tooinitialize MSAL ekleme
Bu adım belirteçleri işleme gibi bir sınıf toohandle etkileşim MSAL kitaplığıyla oluşturmanıza yardımcı olur.

1. Açık hello `App.xaml.cs` dosya ve MSAL kitaplığı toohello sınıfı hello başvurusunu ekleyin:

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Merhaba uygulama sınıfı toohello aşağıdaki güncelleştirin:
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a>Uygulamanızın kullanıcı Arabirimi oluşturma
bir uygulama gibi Microsoft Graph korumalı arka uç sunucusuna nasıl sorgulayabilir Hello bölümüne gösterir. MainWindow.xaml dosya proje şablonu bir parçası olarak otomatik olarak oluşturulması gerekir. Bu dosya bu dosyayı açın ve aşağıdaki hello yönergeleri izleyin:

Uygulamanızın Değiştir `<Grid>` hello şu olmalıdır:

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
