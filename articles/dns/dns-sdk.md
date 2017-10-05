---
title: "DNS bölgeleri oluşturma ve kayıt kümeleri .NET SDK kullanarak Azure DNS'de | Microsoft Docs"
description: "DNS bölgeleri ve kaydı nasıl oluşturulacağını, .NET SDK kullanarak Azure DNS'de ayarlar."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: c0fb0be8da1c0ca48a4d43ea027d30a0bc17fe30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-zones-and-record-sets-using-the-net-sdk"></a><span data-ttu-id="d1c83-103">DNS bölgeleri ve .NET SDK kullanarak kayıt kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1c83-103">Create DNS zones and record sets using the .NET SDK</span></span>

<span data-ttu-id="d1c83-104">Oluşturamaz, silemez veya DNS bölgeleri, kayıt kümelerini ve kayıtları .NET DNS Yönetim kitaplığıyla DNS SDK kullanılarak güncelleştirmek için işlemleri otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1c83-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="d1c83-105">Tam bir Visual Studio projesi kullanılabilir [burada.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="d1c83-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="d1c83-106">Bir hizmet sorumlusu hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d1c83-106">Create a service principal account</span></span>

<span data-ttu-id="d1c83-107">Genellikle, kendi kullanıcı kimlik bilgilerini yerine adanmış bir hesap Azure kaynaklarına programlı erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="d1c83-108">Bu ayrılmış hesapları 'hizmet sorumlusu' hesapları adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="d1c83-109">Azure DNS SDK örnek proje kullanmak için önce bir hizmet sorumlusu hesabı oluşturmak ve doğru izinleri atamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span></span>

1. <span data-ttu-id="d1c83-110">İzleyin [bu yönergeleri](../azure-resource-manager/resource-group-authenticate-service-principal.md) (Azure DNS SDK örnek proje parola tabanlı kimlik doğrulama varsayar.) bir hizmet sorumlusu hesabı oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="d1c83-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="d1c83-111">Bir kaynak grubu oluşturun ([burada nasıl](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="d1c83-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="d1c83-112">Hizmet sorumlusu hesabı kaynak grubunda 'DNS bölge katkıda bulunan' izinleri vermek için Azure RBAC kullanın ([burada nasıl](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="d1c83-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="d1c83-113">Azure DNS SDK örnek proje kullanıyorsanız, aşağıdaki gibi 'program.cs' dosyasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="d1c83-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="d1c83-114">Tenantıd, istemci kimliği (hesap kimliği olarak da bilinir), gizliliği (hizmet sorumlusu hesabı parola) ve 1. adımda kullanılan Subscriptionıd için doğru değerleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d1c83-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="d1c83-115">2. adımda seçilen kaynak grubu adı girin.</span><span class="sxs-lookup"><span data-stu-id="d1c83-115">Enter the resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="d1c83-116">Tercih ettiğiniz bir DNS bölgesi ad girin.</span><span class="sxs-lookup"><span data-stu-id="d1c83-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="d1c83-117">NuGet paketleri ve ad alanı bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d1c83-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="d1c83-118">Azure DNS .NET SDK'yı kullanmak için yüklemeniz gerekir **Azure DNS Yönetimi Kitaplığı** NuGet paketi ve diğer gerekli Azure paketler.</span><span class="sxs-lookup"><span data-stu-id="d1c83-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="d1c83-119">İçinde **Visual Studio**, bir proje veya yeni bir proje açın.</span><span class="sxs-lookup"><span data-stu-id="d1c83-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="d1c83-120">Git **Araçları**  **>**  **NuGet Paket Yöneticisi**  **>**  **çözüm için NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="d1c83-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="d1c83-121">Tıklatın **Gözat**, etkinleştirme **INCLUDE yayın öncesi** onay kutusunu ve türü **Microsoft.Azure.Management.Dns** arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="d1c83-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span></span>
4. <span data-ttu-id="d1c83-122">Paketi seçin ve **yükleme** Visual Studio projenize eklemek için.</span><span class="sxs-lookup"><span data-stu-id="d1c83-122">Select the package and click **Install** to add it to your Visual Studio project.</span></span>
5. <span data-ttu-id="d1c83-123">Ayrıca aşağıdaki paketleri yüklemek için yukarıdaki işlemi tekrarlayın: **Microsoft.Rest.ClientRuntime.Azure.Authentication** ve **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="d1c83-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="d1c83-124">Ad alanı bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d1c83-124">Add namespace declarations</span></span>

<span data-ttu-id="d1c83-125">Aşağıdaki ad alanı bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="d1c83-125">Add the following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-the-dns-management-client"></a><span data-ttu-id="d1c83-126">DNS yönetim istemcisi başlatılamadı</span><span class="sxs-lookup"><span data-stu-id="d1c83-126">Initialize the DNS management client</span></span>

<span data-ttu-id="d1c83-127">*DnsManagementClient* DNS bölgeleri ve kayıt kümeleri yönetmek için gerekli özellikler ve yöntemler içerir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="d1c83-128">Aşağıdaki kod, hizmet sorumlusu hesabı oturum açtığında ve bir DnsManagementClient nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d1c83-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build the service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="d1c83-129">Bir DNS bölgesi güncelle</span><span class="sxs-lookup"><span data-stu-id="d1c83-129">Create or update a DNS zone</span></span>

<span data-ttu-id="d1c83-130">Bir DNS bölgesi oluşturmak için öncelikle bir "Bölgesine" nesne DNS bölge parametrelerini içerecek şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d1c83-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span></span> <span data-ttu-id="d1c83-131">DNS bölgelerini belirli bir bölgede bağlı değildir çünkü konumu 'genel' olarak ayarlıdır.</span><span class="sxs-lookup"><span data-stu-id="d1c83-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span></span> <span data-ttu-id="d1c83-132">Bu örnekte, bir [Azure Resource Manager 'etiketinin'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) de bölgesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span></span>

<span data-ttu-id="d1c83-133">Gerçekte oluşturmak veya Azure DNS bölgesinde güncelleştirmek için bölge parametrelerini içeren bölge nesnesi geçirilir *DnsManagementClient.Zones.CreateOrUpdateAsyc* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d1c83-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="d1c83-134">DnsManagementClient işlemi üç modlarını destekler: eşzamanlı ('CreateOrUpdate'), zaman uyumsuz ('CreateOrUpdateAsync'), ya da erişim HTTP yanıtına ('CreateOrUpdateWithHttpMessagesAsync') ile uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="d1c83-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="d1c83-135">Uygulamanızın gereksinimlerine bağlı olarak bu modlarından birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1c83-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="d1c83-136">Azure DNS destekler adlı iyimser eşzamanlılık [Etag'ler](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="d1c83-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="d1c83-137">Bu örnekte belirtme "*" 'If-None-Match için' Azure bir zaten yoksa, bir DNS bölgesi oluşturmak için DNS üstbilgi söyler.</span><span class="sxs-lookup"><span data-stu-id="d1c83-137">In this example, specifying "*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="d1c83-138">Verilen ada sahip bir bölge verilen kaynak grubunda zaten varsa, çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d1c83-138">The call fails if a zone with the given name already exists in the given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create the actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if the zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting the http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="d1c83-139">DNS kayıt kümelerini ve kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1c83-139">Create DNS record sets and records</span></span>

<span data-ttu-id="d1c83-140">DNS kayıtlarını kayıt kümesi yönetilir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="d1c83-141">Kayıt kümesi, aynı ada ve bir bölge içindeki kayıt türü kayıtlarıyla kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-141">A record set is a set of records with the same name and record type within a zone.</span></span>  <span data-ttu-id="d1c83-142">Kayıt kümesi, bölge adı göreli değil tam DNS adı adıdır.</span><span class="sxs-lookup"><span data-stu-id="d1c83-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span></span>

<span data-ttu-id="d1c83-143">Bir kayıt kümesini oluştur veya güncelleştir için bir "Kayıt kümesi" parametreleri nesnesi oluşturulur ve geçirilen *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="d1c83-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="d1c83-144">DNS bölgeleri ile olmadığından işlem üç modu: eşzamanlı ('CreateOrUpdate'), zaman uyumsuz ('CreateOrUpdateAsync'), veya zaman uyumsuz HTTP yanıtı ('CreateOrUpdateWithHttpMessagesAsync') erişim.</span><span class="sxs-lookup"><span data-stu-id="d1c83-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="d1c83-145">DNS bölgeleri gibi ile kayıt kümeleri üzerinde işlem iyimser eşzamanlılık desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="d1c83-146">'If-Match' ne 'If-None-Match' belirtilmiş olduğundan, bu örnekte, her zaman kayıt kümesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d1c83-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span></span>  <span data-ttu-id="d1c83-147">Bu çağrı, bu DNS bölgesinde aynı ada ve kayıt türü ile ayarlamak varolan bir kaydı üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="d1c83-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records to the record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata to the record set.  Similar to Azure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create the actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="d1c83-148">Get bölgeleri ve kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="d1c83-148">Get zones and record sets</span></span>

<span data-ttu-id="d1c83-149">*DnsManagementClient.Zones.Get* ve *DnsManagementClient.RecordSets.Get* yöntemleri tek başına bölgeleri ve kayıt kümelerini sırasıyla alma.</span><span class="sxs-lookup"><span data-stu-id="d1c83-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="d1c83-150">Kayıt kümeleri kendi türü, adı ve bunlar mevcut bölgesi ve kaynak grubu tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d1c83-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span></span> <span data-ttu-id="d1c83-151">Bölgeler, kendi ad ve bunlar mevcut kaynak grubu tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d1c83-151">Zones are identified by their name and the resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="d1c83-152">Varolan bir kayıt kümesini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="d1c83-152">Update an existing record set</span></span>

<span data-ttu-id="d1c83-153">Varolan bir DNS kaydı kümesini güncelleştirmek, ilk kayıt kümesi almak kayıt kümesi içeriği güncelleştirmek için ardından değişiklik gönderin.</span><span class="sxs-lookup"><span data-stu-id="d1c83-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span></span>  <span data-ttu-id="d1c83-154">Bu örnekte, alınan kayıt kümesinde 'If-Match' parametresinde 'Etag' belirtin.</span><span class="sxs-lookup"><span data-stu-id="d1c83-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span></span> <span data-ttu-id="d1c83-155">Eşzamanlı bir işlem kayıt zarfında kümesine değiştirdi çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d1c83-155">The call fails if a concurrent operation has modified the record set in the meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record to the local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update the record set in Azure DNS
// Note: ETAG check specified, update will be rejected if the record set has changed in the meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="d1c83-156">Liste bölgeleri ve kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="d1c83-156">List zones and record sets</span></span>

<span data-ttu-id="d1c83-157">Bölgeler listesinden, kullanmak için *DnsManagementClient.Zones.List...*  belirtilen kaynak grubunun tüm bölgelerde ya da belirli bir Azure aboneliği tüm bölgelerde (kaynak grupları arasında.) listeleme destek yöntemleri Kayıt kümeleri listesinde, kullanmak için *DnsManagementClient.RecordSets.List...*  belirli bir bölgedeki tüm kayıt kümelerinin ya da bu kaydı kümeleri yalnızca belirli bir türdeki listeleme destek yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d1c83-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="d1c83-158">Bölgeleri listelerken not alın ve sonuçları kayıt kümelerini anlatır.</span><span class="sxs-lookup"><span data-stu-id="d1c83-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="d1c83-159">Aşağıdaki örnek, sonuçları sayfalarıyla yinelemek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-159">The following example shows how to iterate through the pages of results.</span></span> <span data-ttu-id="d1c83-160">('2' yapay küçük sayfa boyutunu, disk belleği zorlamak için kullanılır; uygulamada bu parametre atlanırsa ve varsayılan sayfa boyutu kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="d1c83-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) to demonstrate paging
// In practice, to improve performance you would use a large page size or just use the system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="d1c83-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1c83-161">Next steps</span></span>

<span data-ttu-id="d1c83-162">Karşıdan [Azure DNS .NET SDK örnek proje](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), başka Azure DNS .NET diğer DNS kayıt türleri için örnekler dahil SDK kullanma örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1c83-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
