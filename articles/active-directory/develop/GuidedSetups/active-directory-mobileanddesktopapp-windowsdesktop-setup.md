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
## <a name="set-up-your-project"></a><span data-ttu-id="25ea6-103">Projenizin kurulumunu</span><span class="sxs-lookup"><span data-stu-id="25ea6-103">Set up your project</span></span>

<span data-ttu-id="25ea6-104">Bu bölümde hakkında adım adım yönergeler sağlar toocreate yeni bir proje toodemonstrate nasıl toointegrate bir Windows Masaüstü .NET uygulama (XAML) ile *Microsoft ile oturum açma* için bir belirteç gerekiyor Web API'leri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25ea6-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="25ea6-105">Bu kılavuz tarafından oluşturulan hello uygulama düğmesi toograph ve Göster sonuçları ekran ve oturum kapatma düğmesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="25ea6-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="25ea6-106">Toodownload, bunun yerine bu örnekte 's Visual Studio projesi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="25ea6-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="25ea6-107">[Bir proje indirme](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) ve toohello atla [yapılandırma adımı](#create-an-application-express) yürütmeden önce tooconfigure hello kod örneği.</span><span class="sxs-lookup"><span data-stu-id="25ea6-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="25ea6-108">Uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="25ea6-108">Create your application</span></span>
1. <span data-ttu-id="25ea6-109">Visual Studio'da:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="25ea6-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="25ea6-110">Altında *şablonları*seçin`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="25ea6-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="25ea6-111">Seçin `WPF App` (veya *WPF uygulaması* , Visual Studio hello sürümüne bağlı olarak)</span><span class="sxs-lookup"><span data-stu-id="25ea6-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="25ea6-112">Merhaba Microsoft kimlik doğrulama kitaplığı (MSAL) tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="25ea6-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="25ea6-113">Visual Studio'da:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="25ea6-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="25ea6-114">Kopyalayıp hello aşağıdaki hello Paket Yöneticisi konsol penceresine yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="25ea6-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="25ea6-115">Yukarıdaki Hello paketi hello Microsoft kimlik doğrulama kitaplığı (MSAL) yükler.</span><span class="sxs-lookup"><span data-stu-id="25ea6-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="25ea6-116">MSAL alınırken, önbelleğe alma ve kullanıcı kullanılan toskens tooaccess tarafından Azure Active Directory v2 korumalı API'leri yenilemeyi işler.</span><span class="sxs-lookup"><span data-stu-id="25ea6-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="25ea6-117">Merhaba kod tooinitialize MSAL ekleme</span><span class="sxs-lookup"><span data-stu-id="25ea6-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="25ea6-118">Bu adım belirteçleri işleme gibi bir sınıf toohandle etkileşim MSAL kitaplığıyla oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="25ea6-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="25ea6-119">Açık hello `App.xaml.cs` dosya ve MSAL kitaplığı toohello sınıfı hello başvurusunu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="25ea6-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="25ea6-120">Merhaba uygulama sınıfı toohello aşağıdaki güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="25ea6-120">Update hello App class toohello following:</span></span>
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

## <a name="create-your-applications-ui"></a><span data-ttu-id="25ea6-121">Uygulamanızın kullanıcı Arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="25ea6-121">Create your application’s UI</span></span>
<span data-ttu-id="25ea6-122">bir uygulama gibi Microsoft Graph korumalı arka uç sunucusuna nasıl sorgulayabilir Hello bölümüne gösterir.</span><span class="sxs-lookup"><span data-stu-id="25ea6-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="25ea6-123">MainWindow.xaml dosya proje şablonu bir parçası olarak otomatik olarak oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="25ea6-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="25ea6-124">Bu dosya bu dosyayı açın ve aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="25ea6-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="25ea6-125">Uygulamanızın Değiştir `<Grid>` hello şu olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="25ea6-125">Replace your application’s `<Grid>` with be hello following:</span></span>

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
