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
# <a name="get-started-with-azure-cdn-development"></a>Azure CDN ile geliştirmeye başlama
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Merhaba kullanabilirsiniz [.NET için Azure CDN Kitaplığı](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate oluşturulması ve CDN profili ve uç noktaları yönetimi.  Bu öğreticide, birkaç hello kullanılabilir işlemleri gösteren basit bir .NET konsol uygulaması hello oluşturulmasını açıklanmaktadır.  Bu öğretici tasarlanmamış toodescribe tüm yönlerini hello Azure CDN kitaplığı için .NET ayrıntılı olarak değil.

Bu öğreticide Visual Studio 2015 toocomplete gerekir.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) ücretsiz olarak karşıdan yüklenebilir.

> [!TIP]
> Merhaba [Bu öğreticinin tamamlanan projeden](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) MSDN'de indirilebilir.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Projenizi oluşturmak ve Nuget paketleri ekleme
Bizim CDN profili için bir kaynak grubu oluşturduk artık ve verilen bizim Azure AD uygulama izni toomanage CDN profili ve uç noktaları grubu içindeki göre biz uygulamamızı oluşturmaya başlayabilirsiniz.

Visual Studio 2015'içinde ' ı tıklatın **dosya**, **yeni**, **proje...**  tooopen hello yeni proje iletişim kutusu.  Genişletme **Visual C#**seçeneğini belirleyip **Windows** hello soldaki hello bölmesinde.  Tıklatın **konsol uygulaması** hello orta bölmesinde.  Projenizi adlandırın ve ardından **Tamam**.  

![Yeni Proje](./media/cdn-app-dev-net/cdn-new-project.png)

Projemizin bazı Azure kitaplıkları Nuget paketlerini içinde yer alan toouse geçiyor.  Bu toohello proje ekleyelim.

1. Merhaba tıklatın **Araçları** menüsünde **Nuget Paket Yöneticisi**, ardından **Paket Yöneticisi Konsolu**.
   
    ![Nuget paketlerini yönetme](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. Komut tooinstall hello aşağıdaki hello Hello Paket Yöneticisi konsolu, yürütme **Active Directory Authentication Library (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Tooinstall hello aşağıdaki hello yürütme **Azure CDN Yönetimi Kitaplığı**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Yönergeleri, sabitleri, ana yöntemi ve yardımcı yöntemler
Şimdi yazılmış programımız temel yapısını hello alın.

1. Geri hello Program.cs, hello Değiştir sekmesi `using` yönergeleri hello aşağıdaki ile Merhaba üstünde:
   
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
2. Bizim yöntemler kullanacağı bazı sabitleri toodefine ihtiyacımız var.  Merhaba, `Program` sınıfı, ancak önce hello `Main` yöntemi, hello aşağıdakileri ekleyin.  Merhaba yer tutucular hello dahil olmak üzere, emin tooreplace olması  **&lt;köşeli&gt;**, gerektiği gibi kendi değerlere sahip.
   
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
3. Ayrıca hello sınıf düzeyinde iki bu değişkenleri tanımlayın.  Profil ve uç nokta zaten mevcutsa bu sonraki toodetermine kullanacağız.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Hello yerine `Main` yöntemini aşağıdaki şekilde:
   
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
5. Bizim diğer yöntemlerden bazıları tooprompt hello kullanıcı "Evet/Hayır" sorularını adımıdır.  Yöntem toomake aşağıdaki hello eklemek, biraz daha kolay:
   
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

Merhaba temel programımız yapısını yazılır, hello tarafından adlı hello yöntemler oluşturmanız gerekir `Main` yöntemi.

## <a name="authentication"></a>Kimlik Doğrulaması
Hello Azure CDN Yönetimi Kitaplığı kullanabilmeniz için önce kimliğinizi tooauthenticate hizmetimizi asıl gerekir ve kimlik doğrulama belirtecini elde edin.  Bu yöntem ADAL tooretrieve hello belirtecini kullanır.

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

Tek tek kullanıcı kimlik doğrulaması kullanıyorsanız, hello `GetAccessToken` yöntemi biraz farklı görünür.

> [!IMPORTANT]
> Yalnızca bir hizmet sorumlusu yerine toohave tek tek kullanıcı kimlik doğrulaması seçerek, bu kod örneği kullanın.
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

Emin tooreplace olması `<redirect URI>` hello ile Azure AD içinde Merhaba uygulaması kaydolurken girdiğiniz URI'sini yeniden yönlendir.

## <a name="list-cdn-profiles-and-endpoints"></a>Liste CDN profili ve uç noktaları
Şimdi hazır tooperform CDN işlemler demektir.  Merhaba bizim yöntemi ilk şey tüm hello profilleri ve uç noktaları, kaynak grubundaki listesidir ve bizim sabitler belirtilen hello profil ve uç nokta adları için bir eşleşme bulursa, biz toocreate çoğaltmaları denemeyin şekilde, Not için daha sonra sağlar.

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

## <a name="create-cdn-profiles-and-endpoints"></a>CDN profili ve uç noktaları oluşturma
Ardından, bir profil oluşturacağız.

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

Hello profil oluşturulduktan sonra bir uç nokta oluşturacağız.

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
> Yukarıdaki örnekte Hello atar hello endpoint adlı bir kaynak *Contoso* bir ana bilgisayar adı ile `www.contoso.com`.  Bu toopoint tooyour kendi kaynağın ana bilgisayar adını değiştirmeniz gerekir.
> 
> 

## <a name="purge-an-endpoint"></a>Bir uç noktası
Tooperform bizim programında isteyebilirsiniz, hello uç noktası oluşturuldu varsayıldığında, bizim endpoint hello içeriğinde bir ortak görev temizleme.

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
> Merhaba yukarıdaki örnekte, dize hello `/*` toopurge her şeyi hello bitiş noktası yolu hello kökündeki istiyorum olduğunu gösterir.  Eşdeğer toochecking budur **temizleme tüm** hello Azure portal'ın "iletişim temizleme". Merhaba, `CreateCdnProfile` yöntemi, oluşturduğum bizim profil olarak bir **verizon'dan Azure CDN** hello kodu kullanarak profili `Sku = new Sku(SkuName.StandardVerizon)`, böylece bu başarılı olur.  Ancak, **akamai'den Azure CDN** profilleri desteklemez **temizleme tüm**, Bu öğretici için bir Akamai profili kullanıyordu, tooinclude belirli yollar toopurge gerekir.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>CDN profili ve uç noktaları Sil
Merhaba son yöntemleri bizim uç noktası ve profil silinmesine neden olur.

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

## <a name="running-hello-program"></a>Merhaba programı çalıştırma
Biz artık derleyebilir ve hello tıklayarak hello program Çalıştır **Başlat** Visual Studio'da düğmesi.

![Program çalışıyor](./media/cdn-app-dev-net/cdn-program-running-1.png)

Merhaba program istemi yukarıda hello ulaştığında, hello Azure portal mümkün tooreturn tooyour kaynak grubunda olması ve hello profili oluşturuldu bakın.

![Başarılı!](./media/cdn-app-dev-net/cdn-success.png)

Biz, ardından hello istemleri toorun hello rest hello programının onaylayabilirsiniz.

![Program Tamamlanıyor](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Sonraki Adımlar
Bu kılavuzda toosee tamamlandı hello projeden [hello örnek indirme](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

.NET, görünüm hello hello Azure CDN Yönetimi Kitaplığı hakkındaki belgeleri ek toofind [MSDN'de başvuru](https://msdn.microsoft.com/library/mt657769.aspx).

CDN kaynaklarınızı yönetmek [PowerShell](cdn-manage-powershell.md).

