---
title: "aaaGet .NET için Azure CDN kitaplığı hello ile başlatılan | Microsoft Docs"
description: "Bilgi nasıl toowrite .NET uygulamaları toomanage Visual Studio kullanarak Azure CDN."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="69ada-103">Azure CDN ile geliştirmeye başlama</span><span class="sxs-lookup"><span data-stu-id="69ada-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69ada-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="69ada-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="69ada-105">.NET</span><span class="sxs-lookup"><span data-stu-id="69ada-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="69ada-106">Merhaba kullanabilirsiniz [.NET için Azure CDN Kitaplığı](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate oluşturulması ve CDN profili ve uç noktaları yönetimi.</span><span class="sxs-lookup"><span data-stu-id="69ada-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="69ada-107">Bu öğreticide, birkaç hello kullanılabilir işlemleri gösteren basit bir .NET konsol uygulaması hello oluşturulmasını açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="69ada-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="69ada-108">Bu öğretici tasarlanmamış toodescribe tüm yönlerini hello Azure CDN kitaplığı için .NET ayrıntılı olarak değil.</span><span class="sxs-lookup"><span data-stu-id="69ada-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="69ada-109">Bu öğreticide Visual Studio 2015 toocomplete gerekir.</span><span class="sxs-lookup"><span data-stu-id="69ada-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="69ada-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ücretsiz olarak karşıdan yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="69ada-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="69ada-111">Merhaba [Bu öğreticinin tamamlanan projeden](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) MSDN'de indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="69ada-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="69ada-112">Projenizi oluşturmak ve Nuget paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="69ada-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="69ada-113">Bizim CDN profili için bir kaynak grubu oluşturduk artık ve verilen bizim Azure AD uygulama izni toomanage CDN profili ve uç noktaları grubu içindeki göre biz uygulamamızı oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69ada-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="69ada-114">Visual Studio 2015'içinde ' ı tıklatın **dosya**, **yeni**, **proje...**  tooopen hello yeni proje iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="69ada-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="69ada-115">Genişletme **Visual C#**seçeneğini belirleyip **Windows** hello soldaki hello bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="69ada-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="69ada-116">Tıklatın **konsol uygulaması** hello orta bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="69ada-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="69ada-117">Projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="69ada-117">Name your project, then click **OK**.</span></span>  

![Yeni Proje](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="69ada-119">Projemizin bazı Azure kitaplıkları Nuget paketlerini içinde yer alan toouse geçiyor.</span><span class="sxs-lookup"><span data-stu-id="69ada-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="69ada-120">Bu toohello proje ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="69ada-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="69ada-121">Merhaba tıklatın **Araçları** menüsünde **Nuget Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="69ada-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Nuget paketlerini yönetme](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="69ada-123">Komut tooinstall hello aşağıdaki hello Hello Paket Yöneticisi konsolu, yürütme **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="69ada-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="69ada-124">Tooinstall hello aşağıdaki hello yürütme **Azure CDN Yönetimi Kitaplığı**:</span><span class="sxs-lookup"><span data-stu-id="69ada-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="69ada-125">Yönergeleri, sabitleri, ana yöntemi ve yardımcı yöntemler</span><span class="sxs-lookup"><span data-stu-id="69ada-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="69ada-126">Şimdi yazılmış programımız temel yapısını hello alın.</span><span class="sxs-lookup"><span data-stu-id="69ada-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="69ada-127">Geri hello Program.cs, hello Değiştir sekmesi `using` yönergeleri hello aşağıdaki ile Merhaba üstünde:</span><span class="sxs-lookup"><span data-stu-id="69ada-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. <span data-ttu-id="69ada-128">Bizim yöntemler kullanacağı bazı sabitleri toodefine ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="69ada-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="69ada-129">Merhaba, `Program` sınıfı, ancak önce hello `Main` yöntemi, hello aşağıdakileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="69ada-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="69ada-130">Merhaba yer tutucular hello dahil olmak üzere, emin tooreplace olması  **&lt;köşeli&gt;**, gerektiği gibi kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="69ada-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="69ada-131">Ayrıca hello sınıf düzeyinde iki bu değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="69ada-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="69ada-132">Profil ve uç nokta zaten mevcutsa bu sonraki toodetermine kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="69ada-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="69ada-133">Hello yerine `Main` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="69ada-133">Replace hello `Main` method as follows:</span></span>
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="69ada-134">Bizim diğer yöntemlerden bazıları tooprompt hello kullanıcı "Evet/Hayır" sorularını adımıdır.</span><span class="sxs-lookup"><span data-stu-id="69ada-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="69ada-135">Yöntem toomake aşağıdaki hello eklemek, biraz daha kolay:</span><span class="sxs-lookup"><span data-stu-id="69ada-135">Add hello following method toomake that a little easier:</span></span>
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

<span data-ttu-id="69ada-136">Merhaba temel programımız yapısını yazılır, hello tarafından adlı hello yöntemler oluşturmanız gerekir `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="69ada-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="69ada-137">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="69ada-137">Authentication</span></span>
<span data-ttu-id="69ada-138">Hello Azure CDN Yönetimi Kitaplığı kullanabilmeniz için önce kimliğinizi tooauthenticate hizmetimizi asıl gerekir ve kimlik doğrulama belirtecini elde edin.</span><span class="sxs-lookup"><span data-stu-id="69ada-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="69ada-139">Bu yöntem ADAL tooretrieve hello belirtecini kullanır.</span><span class="sxs-lookup"><span data-stu-id="69ada-139">This method uses ADAL tooretrieve hello token.</span></span>

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

<span data-ttu-id="69ada-140">Tek tek kullanıcı kimlik doğrulaması kullanıyorsanız, hello `GetAccessToken` yöntemi biraz farklı görünür.</span><span class="sxs-lookup"><span data-stu-id="69ada-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69ada-141">Yalnızca bir hizmet sorumlusu yerine toohave tek tek kullanıcı kimlik doğrulaması seçerek, bu kod örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="69ada-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

<span data-ttu-id="69ada-142">Emin tooreplace olması `<redirect URI>` hello ile Azure AD içinde Merhaba uygulaması kaydolurken girdiğiniz URI'sini yeniden yönlendir.</span><span class="sxs-lookup"><span data-stu-id="69ada-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="69ada-143">Liste CDN profili ve uç noktaları</span><span class="sxs-lookup"><span data-stu-id="69ada-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="69ada-144">Şimdi hazır tooperform CDN işlemler demektir.</span><span class="sxs-lookup"><span data-stu-id="69ada-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="69ada-145">Merhaba bizim yöntemi ilk şey tüm hello profilleri ve uç noktaları, kaynak grubundaki listesidir ve bizim sabitler belirtilen hello profil ve uç nokta adları için bir eşleşme bulursa, biz toocreate çoğaltmaları denemeyin şekilde, Not için daha sonra sağlar.</span><span class="sxs-lookup"><span data-stu-id="69ada-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="69ada-146">CDN profili ve uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="69ada-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="69ada-147">Ardından, bir profil oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="69ada-147">Next, we'll create a profile.</span></span>

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

<span data-ttu-id="69ada-148">Hello profil oluşturulduktan sonra bir uç nokta oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="69ada-148">Once hello profile is created, we'll create an endpoint.</span></span>

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> <span data-ttu-id="69ada-149">Yukarıdaki örnekte Hello atar hello endpoint adlı bir kaynak *Contoso* bir ana bilgisayar adı ile `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="69ada-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="69ada-150">Bu toopoint tooyour kendi kaynağın ana bilgisayar adını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="69ada-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="69ada-151">Bir uç noktası</span><span class="sxs-lookup"><span data-stu-id="69ada-151">Purge an endpoint</span></span>
<span data-ttu-id="69ada-152">Tooperform bizim programında isteyebilirsiniz, hello uç noktası oluşturuldu varsayıldığında, bizim endpoint hello içeriğinde bir ortak görev temizleme.</span><span class="sxs-lookup"><span data-stu-id="69ada-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> <span data-ttu-id="69ada-153">Merhaba yukarıdaki örnekte, dize hello `/*` toopurge her şeyi hello bitiş noktası yolu hello kökündeki istiyorum olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="69ada-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="69ada-154">Eşdeğer toochecking budur **temizleme tüm** hello Azure portal'ın "iletişim temizleme".</span><span class="sxs-lookup"><span data-stu-id="69ada-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="69ada-155">Merhaba, `CreateCdnProfile` yöntemi, oluşturduğum bizim profil olarak bir **verizon'dan Azure CDN** hello kodu kullanarak profili `Sku = new Sku(SkuName.StandardVerizon)`, böylece bu başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="69ada-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="69ada-156">Ancak, **akamai'den Azure CDN** profilleri desteklemez **temizleme tüm**, Bu öğretici için bir Akamai profili kullanıyordu, tooinclude belirli yollar toopurge gerekir.</span><span class="sxs-lookup"><span data-stu-id="69ada-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="69ada-157">CDN profili ve uç noktaları Sil</span><span class="sxs-lookup"><span data-stu-id="69ada-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="69ada-158">Merhaba son yöntemleri bizim uç noktası ve profil silinmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="69ada-158">hello last methods will delete our endpoint and profile.</span></span>

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a><span data-ttu-id="69ada-159">Merhaba programı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="69ada-159">Running hello program</span></span>
<span data-ttu-id="69ada-160">Biz artık derleyebilir ve hello tıklayarak hello program Çalıştır **Başlat** Visual Studio'da düğmesi.</span><span class="sxs-lookup"><span data-stu-id="69ada-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Program çalışıyor](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="69ada-162">Merhaba program istemi yukarıda hello ulaştığında, hello Azure portal mümkün tooreturn tooyour kaynak grubunda olması ve hello profili oluşturuldu bakın.</span><span class="sxs-lookup"><span data-stu-id="69ada-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![Başarılı!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="69ada-164">Biz, ardından hello istemleri toorun hello rest hello programının onaylayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69ada-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Program Tamamlanıyor](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="69ada-166">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="69ada-166">Next Steps</span></span>
<span data-ttu-id="69ada-167">Bu kılavuzda toosee tamamlandı hello projeden [hello örnek indirme](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="69ada-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="69ada-168">.NET, görünüm hello hello Azure CDN Yönetimi Kitaplığı hakkındaki belgeleri ek toofind [MSDN'de başvuru](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="69ada-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="69ada-169">CDN kaynaklarınızı yönetmek [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="69ada-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

