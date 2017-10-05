---
title: "Azure AD v2 Windows Masaüstü tıklatmalarını başlatıldı - Kurulumu | Microsoft Docs"
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
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="436ae-103">Projenizin kurulumunu</span><span class="sxs-lookup"><span data-stu-id="436ae-103">Set up your project</span></span>

<span data-ttu-id="436ae-104">Bu bölümde bir Windows Masaüstü .NET uygulaması (XAML) tümleştirme göstermek için yeni bir proje oluşturmak için adım adım yönergeler sağlar *Microsoft ile oturum açma* için bir belirteç gerekiyor Web API'leri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="436ae-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="436ae-105">Bu kılavuz tarafından oluşturulan uygulama grafiği ve sonuçları ekran ve oturum kapatma düğmesini göster düğmesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="436ae-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="436ae-106">Bunun yerine bu örneği ait Visual Studio projesi indirmeyi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="436ae-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="436ae-107">[Bir proje indirme](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) ve geçin [yapılandırma adımı](#create-an-application-express) kod örneği çalıştırmadan önce yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="436ae-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="436ae-108">Uygulamanızı oluşturun</span><span class="sxs-lookup"><span data-stu-id="436ae-108">Create your application</span></span>
1. <span data-ttu-id="436ae-109">Visual Studio'da:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="436ae-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="436ae-110">Altında *şablonları*seçin`Visual C#`</span><span class="sxs-lookup"><span data-stu-id="436ae-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="436ae-111">Seçin `WPF App` (veya *WPF uygulaması* , Visual Studio sürümüne bağlı olarak)</span><span class="sxs-lookup"><span data-stu-id="436ae-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="436ae-112">Microsoft kimlik doğrulama kitaplığı (MSAL) projenize ekleyin</span><span class="sxs-lookup"><span data-stu-id="436ae-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="436ae-113">Visual Studio'da:`Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="436ae-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="436ae-114">Paket Yöneticisi konsolu penceresinde aşağıdakileri kopyalayıp yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="436ae-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="436ae-115">Yukarıdaki paket Microsoft kimlik doğrulama kitaplığı (MSAL) yükler.</span><span class="sxs-lookup"><span data-stu-id="436ae-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="436ae-116">MSAL alınırken, önbelleğe alma ve Azure Active Directory v2 tarafından korunan API'leri erişmek için kullanılan kullanıcı toskens yenilemeyi işler.</span><span class="sxs-lookup"><span data-stu-id="436ae-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="436ae-117">MSAL başlatmak için kod ekleme</span><span class="sxs-lookup"><span data-stu-id="436ae-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="436ae-118">Bu adımı MSAL kitaplığı ile etkileşim belirteçleri işleme gibi işlemek için bir sınıf oluşturmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="436ae-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="436ae-119">Açık `App.xaml.cs` dosya ve MSAL Kitaplığı Başvurusu sınıfına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="436ae-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="436ae-120">Uygulama sınıfı şu güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="436ae-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="436ae-121">Uygulamanızın kullanıcı Arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="436ae-121">Create your application’s UI</span></span>
<span data-ttu-id="436ae-122">Aşağıdaki bölümü, bir uygulama gibi Microsoft Graph korumalı arka uç sunucusuna nasıl sorgulayabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="436ae-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="436ae-123">MainWindow.xaml dosya proje şablonu bir parçası olarak otomatik olarak oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="436ae-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="436ae-124">Bu dosya bu dosyayı açın ve aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="436ae-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="436ae-125">Uygulamanızın Değiştir `<Grid>` aşağıdaki olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="436ae-125">Replace your application’s `<Grid>` with be the following:</span></span>

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
