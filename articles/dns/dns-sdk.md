---
title: "aaaCreate DNS bölgeleri ve kullanarak Azure DNS kayıt kümelerini hello .NET SDK'sı | Microsoft Docs"
description: "Nasıl toocreate DNS bölgeleri ve kayıt kümelerini Azure DNS'de hello .NET SDK kullanarak."
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
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="274d7-103">DNS bölgeleri ve hello .NET SDK kullanarak kayıt kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="274d7-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="274d7-104">.NET DNS Yönetim kitaplığıyla DNS SDK kullanılarak işlemleri toocreate, delete veya update DNS bölgeleri, kayıt kümelerini ve kayıtları otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274d7-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="274d7-105">Tam bir Visual Studio projesi kullanılabilir [burada.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="274d7-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="274d7-106">Bir hizmet sorumlusu hesabı oluşturun</span><span class="sxs-lookup"><span data-stu-id="274d7-106">Create a service principal account</span></span>

<span data-ttu-id="274d7-107">Genellikle, tooAzure kaynaklarına programlı erişim verilir, kendi kullanıcı kimlik bilgilerini yerine adanmış bir hesap.</span><span class="sxs-lookup"><span data-stu-id="274d7-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="274d7-108">Bu ayrılmış hesapları 'hizmet sorumlusu' hesapları adı verilir.</span><span class="sxs-lookup"><span data-stu-id="274d7-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="274d7-109">toouse hello Azure DNS SDK örnek proje, ilk toocreate bir hizmet sorumlusu hesabı gerekir ve hello doğru izinleri atayın.</span><span class="sxs-lookup"><span data-stu-id="274d7-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="274d7-110">İzleyin [bu yönergeleri](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate bir hizmet sorumlusu hesabı (hello Azure DNS SDK örnek proje parola tabanlı kimlik doğrulama varsayar.)</span><span class="sxs-lookup"><span data-stu-id="274d7-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="274d7-111">Bir kaynak grubu oluşturun ([burada nasıl](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="274d7-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="274d7-112">Kullanım Azure RBAC toogrant hello hizmet asıl hesabı 'DNS bölge katkıda bulunan' izinleri toohello kaynak grubu ([burada nasıl](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="274d7-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="274d7-113">Hello Azure DNS SDK örnek proje kullanıyorsanız, aşağıdaki gibi hello 'program.cs' dosyasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="274d7-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="274d7-114">Merhaba Tenantıd, istemci kimliği (hesap kimliği olarak da bilinir), gizliliği (hizmet sorumlusu hesabı parola) ve 1. adımda kullanılan Subscriptionıd için doğru değerleri Hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="274d7-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="274d7-115">2. adımda seçilen hello kaynak grubu adı girin.</span><span class="sxs-lookup"><span data-stu-id="274d7-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="274d7-116">Tercih ettiğiniz bir DNS bölgesi ad girin.</span><span class="sxs-lookup"><span data-stu-id="274d7-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="274d7-117">NuGet paketleri ve ad alanı bildirimleri</span><span class="sxs-lookup"><span data-stu-id="274d7-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="274d7-118">toouse hello Azure DNS .NET SDK'sı, gereksinim duyduğunuz tooinstall hello **Azure DNS Yönetimi Kitaplığı** NuGet paketi ve diğer gerekli Azure paketler.</span><span class="sxs-lookup"><span data-stu-id="274d7-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="274d7-119">İçinde **Visual Studio**, bir proje veya yeni bir proje açın.</span><span class="sxs-lookup"><span data-stu-id="274d7-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="274d7-120">Çok Git**Araçları** ** > ** **NuGet Paket Yöneticisi** ** > ** **için NuGet paketlerini Yönet Çözüm... **.</span><span class="sxs-lookup"><span data-stu-id="274d7-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="274d7-121">Tıklatın **Gözat**, hello etkinleştirmek **INCLUDE yayın öncesi** onay kutusunu ve türü **Microsoft.Azure.Management.Dns** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="274d7-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="274d7-122">Merhaba paketi seçin ve **yükleme** tooadd, tooyour Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="274d7-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="274d7-123">Paketleri aşağıdaki tooalso yükleme hello yukarıda Hello işlemi tekrarlayın: **Microsoft.Rest.ClientRuntime.Azure.Authentication** ve **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="274d7-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="274d7-124">Ad alanı bildirimleri ekleme</span><span class="sxs-lookup"><span data-stu-id="274d7-124">Add namespace declarations</span></span>

<span data-ttu-id="274d7-125">Ad alanı bildirimleri aşağıdaki hello ekleme</span><span class="sxs-lookup"><span data-stu-id="274d7-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="274d7-126">Merhaba DNS yönetim istemcisi başlatılamadı</span><span class="sxs-lookup"><span data-stu-id="274d7-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="274d7-127">Merhaba *DnsManagementClient* hello yöntemleri ve DNS bölgeleri ve kayıt kümeleri yönetmek için gerekli özellikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="274d7-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="274d7-128">Merhaba aşağıdaki kodu toohello hizmet asıl hesabı'nda günlüğe kaydeder ve bir DnsManagementClient nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="274d7-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="274d7-129">Bir DNS bölgesi güncelle</span><span class="sxs-lookup"><span data-stu-id="274d7-129">Create or update a DNS zone</span></span>

<span data-ttu-id="274d7-130">toocreate bir DNS bölgesi, ilk toocontain hello DNS bölge parametrelerini "Bölgesine" nesnesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="274d7-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="274d7-131">DNS bölgelerini değil bağlantılı tooa belirli bir bölge olduğundan, hello konum too'global ayarlanır '.</span><span class="sxs-lookup"><span data-stu-id="274d7-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="274d7-132">Bu örnekte, bir [Azure Resource Manager 'etiketinin'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) toohello bölge de eklenir.</span><span class="sxs-lookup"><span data-stu-id="274d7-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="274d7-133">tooactually oluşturma veya güncelleştirme hello bölge Azure DNS'de hello bölge parametrelerini içeren hello bölge nesnesi toohello geçirilen *DnsManagementClient.Zones.CreateOrUpdateAsyc* yöntemi.</span><span class="sxs-lookup"><span data-stu-id="274d7-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="274d7-134">DnsManagementClient işlemi üç modlarını destekler: eşzamanlı ('CreateOrUpdate'), zaman uyumsuz ('CreateOrUpdateAsync'), ya da erişim toohello HTTP yanıtı ('CreateOrUpdateWithHttpMessagesAsync') ile uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="274d7-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="274d7-135">Uygulamanızın gereksinimlerine bağlı olarak bu modlarından birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274d7-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="274d7-136">Azure DNS destekler adlı iyimser eşzamanlılık [Etag'ler](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="274d7-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="274d7-137">Bu örnekte belirtme "*" bir zaten mevcut değilse hello 'If-None-Match' üstbilgi Azure DNS toocreate bir DNS bölgesi söyler. için.</span><span class="sxs-lookup"><span data-stu-id="274d7-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="274d7-138">kaynak grubu verilen hello hello verilen ada sahip bir bölge zaten varsa hello çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="274d7-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="274d7-139">DNS kayıt kümelerini ve kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="274d7-139">Create DNS record sets and records</span></span>

<span data-ttu-id="274d7-140">DNS kayıtlarını kayıt kümesi yönetilir.</span><span class="sxs-lookup"><span data-stu-id="274d7-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="274d7-141">Kayıt kümesi aynı ad ve kayıt hello kayıtlarıyla kümesidir bir bölgedeki türü.</span><span class="sxs-lookup"><span data-stu-id="274d7-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="274d7-142">Merhaba kayıt kümesi adı göreli toohello bölge adı, tam DNS adı hello değil.</span><span class="sxs-lookup"><span data-stu-id="274d7-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="274d7-143">toocreate veya güncelleştirme bir kayıt kümesi, "Kayıt kümesi" parametreleri nesnesi oluşturulur ve çok geçirilen*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="274d7-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="274d7-144">DNS bölgeleri ile olmadığından işlem üç modu: eşzamanlı ('CreateOrUpdate'), zaman uyumsuz ('CreateOrUpdateAsync'), ya da erişim toohello HTTP yanıtı ('CreateOrUpdateWithHttpMessagesAsync') ile uyumsuz.</span><span class="sxs-lookup"><span data-stu-id="274d7-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="274d7-145">DNS bölgeleri gibi ile kayıt kümeleri üzerinde işlem iyimser eşzamanlılık desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="274d7-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="274d7-146">'If-Match' ne 'If-None-Match' belirtilmiş olduğundan, bu örnekte, her zaman hello kayıt kümesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="274d7-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="274d7-147">Bu çağrı ile aynı ad ve kayıt hello ayarlamak varolan bir kaydı üzerine yazar bu DNS bölgesinde türü.</span><span class="sxs-lookup"><span data-stu-id="274d7-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="274d7-148">Get bölgeleri ve kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="274d7-148">Get zones and record sets</span></span>

<span data-ttu-id="274d7-149">Merhaba *DnsManagementClient.Zones.Get* ve *DnsManagementClient.RecordSets.Get* yöntemleri tek başına bölgeleri ve kayıt kümelerini sırasıyla alma.</span><span class="sxs-lookup"><span data-stu-id="274d7-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="274d7-150">Kayıt kümeleri kendi türü, adı ve bunlar mevcut hello bölgesi ve kaynak grubu tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="274d7-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="274d7-151">Bölgeler, bunlar mevcut kendi adı ve hello kaynak grubu tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="274d7-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="274d7-152">Varolan bir kayıt kümesini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="274d7-152">Update an existing record set</span></span>

<span data-ttu-id="274d7-153">tooupdate varolan bir DNS kaydı kümesi, güncelleştirme hello kayıt içeriği sonra hello değişiklik Gönder sonra hello kayıt kümesi, ilk alma.</span><span class="sxs-lookup"><span data-stu-id="274d7-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="274d7-154">Bu örnekte, hello ' Etag'den' kayıt kümesi hello 'If-Match' parametresinde alınan hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="274d7-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="274d7-155">eşzamanlı işlem hello kayıt hello sırada kümesi değiştirilirse hello çağrı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="274d7-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="274d7-156">Liste bölgeleri ve kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="274d7-156">List zones and record sets</span></span>

<span data-ttu-id="274d7-157">toolist bölgeleri kullanmak hello *DnsManagementClient.Zones.List... * belirtilen kaynak grubunun tüm bölgelerde ya da belirli Azure abonelik (üzerinden kaynak gruplarını.) toolist kayıt kümesindeki tüm bölgeler listeleme desteği yöntemleri kullanın *DnsManagementClient.RecordSets.List... * belirli bir bölgedeki tüm kayıt kümelerinin ya da bu kaydı kümeleri yalnızca belirli bir türdeki listeleme destek yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="274d7-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="274d7-158">Bölgeleri listelerken not alın ve sonuçları kayıt kümelerini anlatır.</span><span class="sxs-lookup"><span data-stu-id="274d7-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="274d7-159">örnekte gösterildiği nasıl aşağıdaki hello sonuçlarının hello sayfaları aracılığıyla tooiterate.</span><span class="sxs-lookup"><span data-stu-id="274d7-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="274d7-160">(Bir yapay küçük sayfa boyutu '2' kullanılan tooforce disk belleği; yöntem bu parametre, alınmamalıdır ve varsayılan sayfa boyutu kullanılan hello.)</span><span class="sxs-lookup"><span data-stu-id="274d7-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="274d7-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="274d7-161">Next steps</span></span>

<span data-ttu-id="274d7-162">Merhaba karşıdan [Azure DNS .NET SDK örnek proje](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), nasıl toouse hello diğer DNS kayıt türleri için örnekler dahil olmak üzere Azure DNS .NET SDK hakkında daha fazla örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="274d7-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
