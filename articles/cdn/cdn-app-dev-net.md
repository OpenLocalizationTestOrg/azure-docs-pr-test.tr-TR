---
title: ".NET için Azure CDN kitaplığını kullanmaya başlama | Microsoft Docs"
description: "Visual Studio kullanarak Azure CDN yönetmek için .NET uygulamaları yazma öğrenin."
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="c178a-103">Azure CDN ile geliştirmeye başlama</span><span class="sxs-lookup"><span data-stu-id="c178a-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c178a-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="c178a-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="c178a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c178a-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="c178a-106">Kullanabileceğiniz [.NET için Azure CDN Kitaplığı](https://msdn.microsoft.com/library/mt657769.aspx) oluşturulması ve CDN profili ve uç noktaları Yönetimi otomatik hale getirmek için.</span><span class="sxs-lookup"><span data-stu-id="c178a-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="c178a-107">Bu öğreticide, kullanılabilir işlemleri çeşitli gösteren basit bir .NET konsol uygulaması oluşturma aşamasından açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c178a-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="c178a-108">Bu öğretici, ayrıntılı olarak .NET için Azure CDN kitaplığı tüm yönlerini açıklamak için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="c178a-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="c178a-109">Bu öğreticiyi tamamlamak için Visual Studio 2015 gerekir.</span><span class="sxs-lookup"><span data-stu-id="c178a-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="c178a-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ücretsiz olarak karşıdan yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="c178a-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="c178a-111">[Bu öğreticinin tamamlanan projeden](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) MSDN'de indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c178a-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="c178a-112">Projenizi oluşturmak ve Nuget paketleri ekleme</span><span class="sxs-lookup"><span data-stu-id="c178a-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="c178a-113">Bizim CDN profili için bir kaynak grubu oluşturduk artık ve CDN profili ve uç noktaları grubu içindeki yönetmek için Azure AD uygulama izni verilen göre biz uygulamamızı oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c178a-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="c178a-114">Visual Studio 2015'içinde ' ı tıklatın **dosya**, **yeni**, **proje...**  yeni proje iletişim kutusunu açın.</span><span class="sxs-lookup"><span data-stu-id="c178a-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="c178a-115">Genişletme **Visual C#**seçeneğini belirleyip **Windows** sol taraftaki bölmede.</span><span class="sxs-lookup"><span data-stu-id="c178a-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="c178a-116">Tıklatın **konsol uygulaması** Orta bölmede.</span><span class="sxs-lookup"><span data-stu-id="c178a-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="c178a-117">Projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c178a-117">Name your project, then click **OK**.</span></span>  

![Yeni Proje](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="c178a-119">Projemizin Nuget paketlerini içinde yer alan bazı Azure kitaplıkları kullanmak zordur.</span><span class="sxs-lookup"><span data-stu-id="c178a-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="c178a-120">Bu projeye ekleyelim.</span><span class="sxs-lookup"><span data-stu-id="c178a-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="c178a-121">Tıklatın **Araçları** menüsünde **Nuget Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="c178a-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Nuget paketlerini yönetme](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="c178a-123">Paket Yöneticisi konsolunda yüklemek için aşağıdaki komutu yürütün **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="c178a-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="c178a-124">Yüklemek için aşağıdakileri yürütün **Azure CDN Yönetimi Kitaplığı**:</span><span class="sxs-lookup"><span data-stu-id="c178a-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="c178a-125">Yönergeleri, sabitleri, ana yöntemi ve yardımcı yöntemler</span><span class="sxs-lookup"><span data-stu-id="c178a-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="c178a-126">Şimdi yazılmış programımız temel yapısını alın.</span><span class="sxs-lookup"><span data-stu-id="c178a-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="c178a-127">Program.cs sekmesinde geri, yerini `using` üst aşağıdaki yönergeleri:</span><span class="sxs-lookup"><span data-stu-id="c178a-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="c178a-128">Bizim yöntemler kullanacağı bazı sabitleri tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="c178a-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="c178a-129">İçinde `Program` sınıfı, ancak önce `Main` yöntemi, aşağıdaki ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c178a-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="c178a-130">Dahil olmak üzere, yer tutucular değiştirdiğinizden emin olun  **&lt;köşeli&gt;**, gerektiği gibi kendi değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="c178a-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="c178a-131">Ayrıca sınıf düzeyinde iki bu değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c178a-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="c178a-132">Bunlar daha sonra profil ve uç nokta zaten var olup olmadığını belirlemek için kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c178a-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="c178a-133">Değiştir `Main` yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="c178a-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="c178a-134">Bizim diğer yöntemlerden bazıları "Evet/Hayır" sorularını kullanıcıdan adımıdır.</span><span class="sxs-lookup"><span data-stu-id="c178a-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="c178a-135">Biraz daha kolay yapmak için aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c178a-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="c178a-136">Programımız temel yapısını yazılır, çağıran yöntemleri oluşturmanız gerekir `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c178a-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="c178a-137">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c178a-137">Authentication</span></span>
<span data-ttu-id="c178a-138">Azure CDN Yönetimi Kitaplığı kullanabilmeniz için önce kimliğinizi bizim hizmet sorumlusunun kimliğini doğrulamak ve kimlik doğrulama belirtecini almak gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c178a-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="c178a-139">Bu yöntem, belirtecini almak için ADAL kullanır.</span><span class="sxs-lookup"><span data-stu-id="c178a-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="c178a-140">Tek tek kullanıcı kimlik doğrulaması kullanıyorsanız, `GetAccessToken` yöntemi biraz farklı görünür.</span><span class="sxs-lookup"><span data-stu-id="c178a-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c178a-141">Yalnızca bireysel kullanıcı kimlik doğrulaması, bir hizmet sorumlusu yerine seçmek, bu kod örneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="c178a-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="c178a-142">Değiştirdiğinizden emin olun `<redirect URI>` yeniden yönlendirme URI'si Azure AD'de uygulama kaydolurken girdiğiniz ile.</span><span class="sxs-lookup"><span data-stu-id="c178a-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="c178a-143">Liste CDN profili ve uç noktaları</span><span class="sxs-lookup"><span data-stu-id="c178a-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="c178a-144">Şimdi biz CDN işlemlerini gerçekleştirmek için hazır.</span><span class="sxs-lookup"><span data-stu-id="c178a-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="c178a-145">Bizim yöntemi yapacağı ilk şey tüm profil ve uç noktaları bizim kaynak grubunda listesidir ve bizim sabitler belirtilen profil ve uç nokta adları için bir eşleşme bulursa, çoğaltmaları oluşturmak denemeyin şekilde, Not için daha sonra sağlar.</span><span class="sxs-lookup"><span data-stu-id="c178a-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="c178a-146">CDN profili ve uç noktaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c178a-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="c178a-147">Ardından, bir profil oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c178a-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="c178a-148">Profil oluşturulduktan sonra bir uç nokta oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c178a-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="c178a-149">Yukarıdaki örnekte uç nokta adlı bir kaynak atar *Contoso* bir ana bilgisayar adı ile `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="c178a-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="c178a-150">Bu, kendi kaynağın konak adına işaret edecek şekilde değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c178a-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="c178a-151">Bir uç noktası</span><span class="sxs-lookup"><span data-stu-id="c178a-151">Purge an endpoint</span></span>
<span data-ttu-id="c178a-152">Uç noktası oluşturuldu varsayıldığında, biz bizim programında gerçekleştirmek isteyebileceğiniz ortak bir görev bizim endpoint içeriği temizleme.</span><span class="sxs-lookup"><span data-stu-id="c178a-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="c178a-153">Dize yukarıdaki örnekte `/*` bitiş noktası yolu kök her şeyi temizlemek istediğiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="c178a-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="c178a-154">Bu denetimi için eşdeğerdir **temizleme tüm** Azure portal'ın "Temizle" iletişim.</span><span class="sxs-lookup"><span data-stu-id="c178a-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="c178a-155">İçinde `CreateCdnProfile` yöntemi, oluşturduğum bizim profili için farklı bir **verizon'dan Azure CDN** kod kullanarak profil `Sku = new Sku(SkuName.StandardVerizon)`, böylece bu başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="c178a-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="c178a-156">Ancak, **akamai'den Azure CDN** profilleri desteklemez **temizleme tüm**, Bu öğretici için bir Akamai profili kullanıyordu, t belirli yolları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c178a-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="c178a-157">CDN profili ve uç noktaları Sil</span><span class="sxs-lookup"><span data-stu-id="c178a-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="c178a-158">Son yöntemleri bizim uç noktası ve profil silinmesine neden olur.</span><span class="sxs-lookup"><span data-stu-id="c178a-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="c178a-159">Programın çalıştırılması</span><span class="sxs-lookup"><span data-stu-id="c178a-159">Running the program</span></span>
<span data-ttu-id="c178a-160">Biz artık derleyebilir ve tıklayarak program Çalıştır **Başlat** Visual Studio'da düğmesi.</span><span class="sxs-lookup"><span data-stu-id="c178a-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Program çalışıyor](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="c178a-162">Program yukarıdaki istemi ulaştığında, kaynak grubunuzdaki Azure portalına dönün ve profilin oluşturulduğunu görmek mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c178a-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Başarılı!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="c178a-164">Biz, ardından program kalan çalıştırmak ister onaylayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c178a-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Program Tamamlanıyor](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="c178a-166">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c178a-166">Next Steps</span></span>
<span data-ttu-id="c178a-167">Bu kılavuzda tamamlanmış projeden görmek için [örneği indirmek](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="c178a-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="c178a-168">.NET için Azure CDN Yönetimi Kitaplığı hakkındaki ek belgeleri bulmak için görüntülemek [MSDN'de başvuru](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="c178a-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="c178a-169">CDN kaynaklarınızı yönetmek [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c178a-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

