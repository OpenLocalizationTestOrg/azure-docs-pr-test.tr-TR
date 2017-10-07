---
title: "aaaManage DNS kayıtları Azure PowerShell kullanarak Azure DNS'de | Microsoft Docs"
description: "DNS kayıt kümelerini ve Azure DNS kayıtlarını Azure DNS'nin etki alanınızda barındırdığında yönetme. Kayıt kümelerini ve kayıtları işlemleri için tüm PowerShell komutları."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 7136a373-0682-471c-9c28-9e00d2add9c2
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 12/21/2016
ms.author: gwallace
ms.openlocfilehash: bfdf116e174d06db0514abdc0ec3f4fc4ee0a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="c144b-104">DNS kayıtlarını ve kayıt kümeleri Azure PowerShell kullanarak Azure DNS'de yönetme</span><span class="sxs-lookup"><span data-stu-id="c144b-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c144b-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c144b-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="c144b-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c144b-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="c144b-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c144b-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="c144b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c144b-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="c144b-109">Bu makalede, Azure PowerShell kullanarak DNS bölgesi için kayıt toomanage DNS kayıtları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c144b-109">This article shows you how toomanage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="c144b-110">DNS kayıtlarını da yönetilebilir hello platformlar arası kullanarak [Azure CLI](dns-operations-recordsets-cli.md) veya hello [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-110">DNS records can also be managed by using hello cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="c144b-111">Bu makaledeki Hello örnekler, zaten sahip olduğunuzu varsayar [, oturum açan Azure PowerShell yüklenmiş ve bir DNS bölgesi oluşturulan](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-111">hello examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="c144b-112">Giriş</span><span class="sxs-lookup"><span data-stu-id="c144b-112">Introduction</span></span>

<span data-ttu-id="c144b-113">Azure DNS'de DNS kayıtlarını oluşturmadan önce ilk toounderstand ihtiyacınız nasıl Azure DNS DNS kayıtlarını DNS kayıt kümeleri halinde düzenler.</span><span class="sxs-lookup"><span data-stu-id="c144b-113">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="c144b-114">Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="c144b-115">Yeni bir DNS kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="c144b-115">Create a new DNS record</span></span>

<span data-ttu-id="c144b-116">Aynı ad ve tür var olan bir kaydı hello yeni kaydınız varsa, çok ihtiyacınız[toohello varolan bir kayıt kümesini eklemek](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="c144b-116">If your new record has hello same name and type as an existing record, you need too[add it toohello existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="c144b-117">Yeni kaydınız kayıtları varolan farklı bir ad ve tür tooall varsa toocreate yeni bir kayıt kümesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c144b-117">If your new record has a different name and type tooall existing records, you need toocreate a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="c144b-118">Yeni bir kayıt kümesinde 'Bir' kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="c144b-119">Hello kullanarak kayıt kümeleri oluşturma `New-AzureRmDnsRecordSet` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c144b-119">You create record sets by using hello `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c144b-120">Kayıt kümesi oluştururken, gereksinim duyduğunuz toospecify hello kayıt kümesi adı, hello bölge, toolive (TTL), hello kayıt türünü ve hello kayıtları toobe oluşturulan hello zamanı.</span><span class="sxs-lookup"><span data-stu-id="c144b-120">When creating a record set, you need toospecify hello record set name, hello zone, hello time toolive (TTL), hello record type, and hello records toobe created.</span></span>

<span data-ttu-id="c144b-121">kayıtları tooa kayıt kümesi eklemek için hello parametreler hello kayıt kümesi hello türüne bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="c144b-121">hello parameters for adding records tooa record set vary depending on hello type of hello record set.</span></span> <span data-ttu-id="c144b-122">Örneğin, 'A' türündeki kayıt kümesini kullanırken hello parametresini kullanarak toospecify başlangıç IP adresi ihtiyacınız `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="c144b-122">For example, when using a record set of type 'A', you need toospecify hello IP address using hello parameter `-IPv4Address`.</span></span> <span data-ttu-id="c144b-123">Diğer parametreler diğer kayıt türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c144b-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="c144b-124">Bkz: [ek kayıt türü örnekleri](#additional-record-type-examples) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="c144b-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="c144b-125">Merhaba aşağıdaki örnek bir kayıt hello göreli adlı hello "contoso.com" DNS bölgesi içinde ' www' kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c144b-125">hello following example creates a record set with hello relative name 'www' in hello DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="c144b-126">Merhaba tam hello kayıt kümesinin 'www.contoso.com' adıdır.</span><span class="sxs-lookup"><span data-stu-id="c144b-126">hello fully-qualified name of hello record set is 'www.contoso.com'.</span></span> <span data-ttu-id="c144b-127">'A' Hello kayıt türü olan ve hello TTL 3600 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="c144b-127">hello record type is 'A', and hello TTL is 3600 seconds.</span></span> <span data-ttu-id="c144b-128">Merhaba kayıt kümesi '1.2.3.4' IP adresiyle tek bir kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="c144b-128">hello record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="c144b-129">toocreate bir kayıt kümesinin bir bölge ' tepesinde' hello (Bu durumda, "contoso.com"), hello kayıt kümesi adını kullan ' @' (tırnak işaretleri hariç):</span><span class="sxs-lookup"><span data-stu-id="c144b-129">toocreate a record set at hello 'apex' of a zone (in this case, 'contoso.com'), use hello record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="c144b-130">Bir kayıt kümesinin birden çok kayıt içeren toocreate gerekiyorsa, önce yerel bir dizi oluşturup hello kayıtları ekleyin, ardından hello dizi çok geçirmek`New-AzureRmDnsRecordSet` gibi:</span><span class="sxs-lookup"><span data-stu-id="c144b-130">If you need toocreate a record set containing more than one record, first create a local array and add hello records, then pass hello array too`New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="c144b-131">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="c144b-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="c144b-132">Merhaba aşağıdaki örnek toocreate kayıt iki meta veri girişi ile nasıl ayarlanacağını gösterir ' bölüm Finans =' ve ' ortam Üretim ='.</span><span class="sxs-lookup"><span data-stu-id="c144b-132">hello following example shows how toocreate a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="c144b-133">Azure DNS, ayrıca DNS kayıtlarını oluşturmadan önce bir DNS adı bir yer tutucu tooreserve çalışabilmek için 'empty' kayıt kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="c144b-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="c144b-134">Boş kaydı kümeleri hello Azure DNS denetim düzlemi görünür, ancak hello Azure DNS ad sunucuları üzerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c144b-134">Empty record sets are visible in hello Azure DNS control plane, but do appear on hello Azure DNS name servers.</span></span> <span data-ttu-id="c144b-135">Aşağıdaki örnek hello boş bir kayıt kümesi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="c144b-135">hello following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="c144b-136">Diğer türleri kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-136">Create records of other types</span></span>

<span data-ttu-id="c144b-137">Ayrıntılı olarak nasıl toocreate 'A' kayıtları, aşağıdaki örneklerde gösterildiği nasıl toocreate kayıtları, diğer kayıt türleri Azure DNS sunucuları tarafından desteklenen hello görülen.</span><span class="sxs-lookup"><span data-stu-id="c144b-137">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="c144b-138">Her durumda, tek bir kayıt içeren bir kayıt toocreate nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c144b-138">In each case, we show how toocreate a record set containing a single record.</span></span> <span data-ttu-id="c144b-139">Merhaba önceki örnekler 'Bir' kayıtları için meta veriler ile birden çok kayıt içeren diğer türleri kayıt kümelerini uyarlanmış toocreate olabilir veya toocreate boş kaydı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="c144b-139">hello earlier examples for 'A' records can be adapted toocreate record sets of other types containing multiple records, with metadata, or toocreate empty record sets.</span></span>

<span data-ttu-id="c144b-140">SOAs oluşturulduğundan bir örnek toocreate bir SOA kayıt kümesi sunuyoruz değil ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="c144b-140">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="c144b-141">Ancak, [SOA değiştirilebilir, bir sonraki örnekte gösterildiği gibi hello](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="c144b-141">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="c144b-142">Tek kayıtlı bir AAAA kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="c144b-143">Tek kayıtlı bir CNAME kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="c144b-144">Merhaba DNS standartlarında izin vermiyor CNAME kayıtları hello bir bölgenin tepesinde (`-Name '@'`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.</span><span class="sxs-lookup"><span data-stu-id="c144b-144">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="c144b-145">Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="c144b-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="c144b-146">Tek kayıtlı bir MX kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="c144b-147">Bu örnekte, hello kayıt kümesi adını kullanıyoruz ' @' toocreate bir MX kaydı hello bölge tepesinde (Bu durumda, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="c144b-147">In this example, we use hello record set name '@' toocreate an MX record at hello zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="c144b-148">Tek kayıtlı bir NS kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="c144b-149">Tek kayıtlı bir PTR kaydı kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="c144b-150">Bu durumda, ' my-arpa-zone.com' hello IP aralığınızı temsil eden ARPA geriye doğru arama bölgesi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c144b-150">In this case, 'my-arpa-zone.com' represents hello ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="c144b-151">Bu bölgede ayarlamak her PTR kaydı tooan IP adresi bu IP aralığı içinde karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="c144b-151">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span> <span data-ttu-id="c144b-152">Merhaba kaydı '10' hello IP adresinin bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="c144b-152">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="c144b-153">Tek kayıtlı bir SRV kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="c144b-154">Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), hello belirtin  *\_hizmet* ve  *\_Protokolü* hello kayıt kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="c144b-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="c144b-155">Hiçbir gerek tooinclude yok ' @' hello kayıt kümesi adı bir SRV kaydı kümesi hello bölgenin tepesinde oluştururken.</span><span class="sxs-lookup"><span data-stu-id="c144b-155">There is no need tooinclude '@' in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="c144b-156">Bir tek kayıtlı bir TXT kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c144b-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="c144b-157">Merhaba aşağıdaki örnekte nasıl toocreate bir TXT kaydı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c144b-157">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="c144b-158">TXT kayıtlarının desteklenen hello maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="c144b-158">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="c144b-159">Bir kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="c144b-159">Get a record set</span></span>

<span data-ttu-id="c144b-160">tooretrieve varolan bir kayıt kümesini kullanma `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="c144b-160">tooretrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="c144b-161">Bu cmdlet hello kayıt Azure DNS'de kümesi temsil eden yerel bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="c144b-161">This cmdlet returns a local object that represents hello record set in Azure DNS.</span></span>

<span data-ttu-id="c144b-162">İle `New-AzureRmDnsRecordSet`, verilen hello kayıt kümesi adı olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c144b-162">As with `New-AzureRmDnsRecordSet`, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="c144b-163">Ayrıca toospecify hello kayıt türünü ve hello kayıt kümesi içeren hello bölge gerekir.</span><span class="sxs-lookup"><span data-stu-id="c144b-163">You also need toospecify hello record type, and hello zone containing hello record set.</span></span>

<span data-ttu-id="c144b-164">Merhaba aşağıdaki örnek bir kayıt tooretrieve nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c144b-164">hello following example shows how tooretrieve a record set.</span></span> <span data-ttu-id="c144b-165">Bu örnekte, hello bölge hello kullanarak belirtilen `-ZoneName` ve `-ResourceGroupName` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="c144b-165">In this example, hello zone is specified using hello `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c144b-166">Alternatif olarak, aynı zamanda hello kullanılarak geçirilen bir bölge nesnesi kullanarak hello bölgesi belirtebilirsiniz `-Zone` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c144b-166">Alternatively, you can also specify hello zone using a zone object, passed using hello `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="c144b-167">Liste kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="c144b-167">List record sets</span></span>

<span data-ttu-id="c144b-168">Aynı zamanda `Get-AzureRmDnsZone` toolist kaydı hello kaldırarak bir bölgede ayarlar `-Name` ve/veya `-RecordType` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="c144b-168">You can also use `Get-AzureRmDnsZone` toolist record sets in a zone, by omitting hello `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="c144b-169">Merhaba aşağıdaki örnek hello bölgesinde tüm kayıt kümeleri döndürür:</span><span class="sxs-lookup"><span data-stu-id="c144b-169">hello following example returns all record sets in hello zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c144b-170">Merhaba aşağıdaki örnekte nasıl tüm kayıt kümeleri belirli bir türde gösterir hello kaydı atlama kümesi adı sırada hello kayıt türü belirterek alınabilir:</span><span class="sxs-lookup"><span data-stu-id="c144b-170">hello following example shows how all record sets of a given type can be retrieved by specifying hello record type while omitting hello record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c144b-171">verilen ada sahip tüm kayıt kümeleri tooretrieve kayıt türleri arasında tooretrieve tüm kayıt kümelerini ve ardından filtre hello sonuçları gerekir:</span><span class="sxs-lookup"><span data-stu-id="c144b-171">tooretrieve all record sets with a given name, across record types, you need tooretrieve all record sets and then filter hello results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="c144b-172">Örnekler yukarıdaki tüm hello, hello bölge olabilir hello kullanarak ya da belirtilen `-ZoneName` ve `-ResourceGroupName`parametreleri (gösterildiği gibi) veya bir bölge nesnesi belirterek:</span><span class="sxs-lookup"><span data-stu-id="c144b-172">In all hello above examples, hello zone can be specified either by using hello `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="c144b-173">Kayıt kümesi varolan bir kayıt tooan Ekle</span><span class="sxs-lookup"><span data-stu-id="c144b-173">Add a record tooan existing record set</span></span>

<span data-ttu-id="c144b-174">tooadd kayıt tooan varolan bir kaydı ayarlayın, hello aşağıdaki üç adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c144b-174">tooadd a record tooan existing record set, follow hello following three steps:</span></span>

1. <span data-ttu-id="c144b-175">Merhaba mevcut kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="c144b-175">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="c144b-176">Merhaba yeni kayıt toohello yerel kayıt kümesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c144b-176">Add hello new record toohello local record set.</span></span> <span data-ttu-id="c144b-177">Bu çevrimdışı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="c144b-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="c144b-178">Merhaba değişikliği geri toohello Azure DNS hizmeti uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c144b-178">Commit hello change back toohello Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="c144b-179">Kullanarak `Set-AzureRmDnsRecordSet` *değiştirir* mevcut kayıt Azure DNS (ve içerdiği tüm kayıtları) belirtilen hello kayıt kümesiyle kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="c144b-179">Using `Set-AzureRmDnsRecordSet` *replaces* hello existing record set in Azure DNS (and all records it contains) with hello record set specified.</span></span> <span data-ttu-id="c144b-180">[ETag denetimleri](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="c144b-180">[Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="c144b-181">İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.</span><span class="sxs-lookup"><span data-stu-id="c144b-181">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="c144b-182">Bu işlem dizisi de olabilir *yöneltilen*, parametre olarak geçirme yerine hello kanal kullanarak hello kayıt kümesi nesnesi geçirdiğiniz anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="c144b-182">This sequence of operations can also be *piped*, meaning you pass hello record set object by using hello pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="c144b-183">Yukarıdaki Hello örnekler nasıl tooadd 'Bir' kayıt tooan varolan bir kayıt kümesinin türü 'A' gösterir.</span><span class="sxs-lookup"><span data-stu-id="c144b-183">hello examples above show how tooadd an 'A' record tooan existing record set of type 'A'.</span></span> <span data-ttu-id="c144b-184">Benzer işlemleri kullanılan tooadd kayıtları toorecord hello değiştirerek diğer türleri kümesi dizisidir `-Ipv4Address` parametresinin `Add-AzureRmDnsRecordConfig` diğer parametreleri belirli tooeach kayıt türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="c144b-184">A similar sequence of operations is used tooadd records toorecord sets of other types, substituting hello `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific tooeach record type.</span></span> <span data-ttu-id="c144b-185">Merhaba her kayıt türü için parametreler olan hello aynı olduğu gibi hello `New-AzureRmDnsRecordConfig` gösterildiği gibi cmdlet [ek kayıt türü örnekleri](#additional-record-type-examples) üstünde.</span><span class="sxs-lookup"><span data-stu-id="c144b-185">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="c144b-186">Kayıt kümeleri 'CNAME' veya 'SOA' türünde birden fazla kayıt içeremez.</span><span class="sxs-lookup"><span data-stu-id="c144b-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="c144b-187">Bu sınırlama hello DNS standartları ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="c144b-187">This constraint arises from hello DNS standards.</span></span> <span data-ttu-id="c144b-188">Azure DNS sınırlandırılmasıdır değil.</span><span class="sxs-lookup"><span data-stu-id="c144b-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="c144b-189">Varolan bir kayıt kümesinden bir kaydı kaldırma</span><span class="sxs-lookup"><span data-stu-id="c144b-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="c144b-190">Merhaba işlem tooremove kayıt kümesinden bir kaydı olan mevcut kayıt tooan benzer toohello işlem tooadd kayıt kümesi:</span><span class="sxs-lookup"><span data-stu-id="c144b-190">hello process tooremove a record from a record set is similar toohello process tooadd a record tooan existing record set:</span></span>

1. <span data-ttu-id="c144b-191">Merhaba mevcut kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="c144b-191">Get hello existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="c144b-192">Merhaba kaydını hello yerel kayıt kümesi nesnesinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c144b-192">Remove hello record from hello local record set object.</span></span> <span data-ttu-id="c144b-193">Bu çevrimdışı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="c144b-193">This is an off-line operation.</span></span> <span data-ttu-id="c144b-194">kaldırılmakta hello kaydı varolan bir kayıtla tam bir eşleşme tüm parametreleri arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c144b-194">hello record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="c144b-195">Merhaba değişikliği geri toohello Azure DNS hizmeti uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c144b-195">Commit hello change back toohello Azure DNS service.</span></span> <span data-ttu-id="c144b-196">İsteğe bağlı kullanım hello `-Overwrite` geçiş toosuppress [Etag denetler](dns-zones-records.md#etags) eşzamanlı değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="c144b-196">Use hello optional `-Overwrite` switch toosuppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="c144b-197">Merhaba dizisi tooremove hello son kaydından bir kayıt kümesini yukarıdaki kullanarak hello kayıt kümesi silinmez, bunun yerine boş bir kayıt kümesi bırakır.</span><span class="sxs-lookup"><span data-stu-id="c144b-197">Using hello above sequence tooremove hello last record from a record set does not delete hello record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="c144b-198">bir kayıt kümesinin tamamen tooremove bkz [bir kayıt kümesini Sil](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="c144b-198">tooremove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="c144b-199">Benzer şekilde tooadding kayıtları tooa kayıt kümesi, bir kayıt kümesini de yöneltilen işlemleri tooremove hello dizisi:</span><span class="sxs-lookup"><span data-stu-id="c144b-199">Similarly tooadding records tooa record set, hello sequence of operations tooremove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="c144b-200">Farklı kayıt türleri hello uygun türe özgü parametreler çok geçirerek desteklenir`Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="c144b-200">Different record types are supported by passing hello appropriate type-specific parameters too`Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="c144b-201">Merhaba her kayıt türü için parametreler olan hello aynı olduğu gibi hello `New-AzureRmDnsRecordConfig` gösterildiği gibi cmdlet [ek kayıt türü örnekleri](#additional-record-type-examples) üstünde.</span><span class="sxs-lookup"><span data-stu-id="c144b-201">hello parameters for each record type are hello same as for hello `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="c144b-202">Varolan bir kayıt kümesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="c144b-202">Modify an existing record set</span></span>

<span data-ttu-id="c144b-203">Varolan bir kayıt kümesini değiştirme hello adımlar, ekleme veya kayıt kümesindeki kayıt kaldırırken benzer toohello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c144b-203">hello steps for modifying an existing record set are similar toohello steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="c144b-204">Merhaba mevcut kayıt kullanarak kümesi almak `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="c144b-204">Retrieve hello existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="c144b-205">Merhaba yerel kayıt kümesi nesnesi tarafından değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c144b-205">Modify hello local record set object by:</span></span>
    * <span data-ttu-id="c144b-206">Ekleme veya kayıt kaldırma</span><span class="sxs-lookup"><span data-stu-id="c144b-206">Adding or removing records</span></span>
    * <span data-ttu-id="c144b-207">Merhaba parametrelerinin varolan kayıtları değiştirme</span><span class="sxs-lookup"><span data-stu-id="c144b-207">Changing hello parameters of existing records</span></span>
    * <span data-ttu-id="c144b-208">Merhaba kaydı değiştirme meta verileri ve toolive süresi (TTL) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c144b-208">Changing hello record set metadata and time toolive (TTL)</span></span>
3. <span data-ttu-id="c144b-209">Hello kullanarak, değişiklikleri `Set-AzureRmDnsRecordSet` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c144b-209">Commit your changes by using hello `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c144b-210">Bu *değiştirir* mevcut kayıt hello kayıt kümesi belirtilen ile Azure DNS'de kümesi hello.</span><span class="sxs-lookup"><span data-stu-id="c144b-210">This *replaces* hello existing record set in Azure DNS with hello record set specified.</span></span>

<span data-ttu-id="c144b-211">Kullanırken `Set-AzureRmDnsRecordSet`, [Etag denetler](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri yazılmaz.</span><span class="sxs-lookup"><span data-stu-id="c144b-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="c144b-212">İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.</span><span class="sxs-lookup"><span data-stu-id="c144b-212">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

### <a name="tooupdate-a-record-in-an-existing-record-set"></a><span data-ttu-id="c144b-213">Varolan bir kaydı bir kayıtta tooupdate ayarlayın</span><span class="sxs-lookup"><span data-stu-id="c144b-213">tooupdate a record in an existing record set</span></span>

<span data-ttu-id="c144b-214">Bu örnekte, varolan 'Bir' kayıt başlangıç IP adresi değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c144b-214">In this example, we change hello IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="c144b-215">toomodify bir SOA kaydı</span><span class="sxs-lookup"><span data-stu-id="c144b-215">toomodify an SOA record</span></span>

<span data-ttu-id="c144b-216">Ekleme veya SOA kaydına hello bölgenin tepesinde Ayarla otomatik olarak oluşturulan hello kayıtları kaldırın (`-Name "@"`, tırnak işaretleri dahil olmak üzere).</span><span class="sxs-lookup"><span data-stu-id="c144b-216">You cannot add or remove records from hello automatically created SOA record set at hello zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="c144b-217">Ancak, hello SOA kaydı (dışında "ana bilgisayar") içinde hello parametrelerinden herhangi birini değiştirmek ve TTL hello kayıt ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c144b-217">However, you can modify any of hello parameters within hello SOA record (except "Host") and hello record set TTL.</span></span>

<span data-ttu-id="c144b-218">örnekte gösterildiği nasıl aşağıdaki hello toochange hello *e-posta* SOA kaydına hello özelliği:</span><span class="sxs-lookup"><span data-stu-id="c144b-218">hello following example shows how toochange hello *Email* property of hello SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="c144b-219">Merhaba bölge tepesinde toomodify NS kayıtları</span><span class="sxs-lookup"><span data-stu-id="c144b-219">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="c144b-220">Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c144b-220">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="c144b-221">Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="c144b-221">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="c144b-222">Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c144b-222">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="c144b-223">Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c144b-223">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="c144b-224">Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="c144b-224">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="c144b-225">Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c144b-225">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="c144b-226">Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="c144b-226">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="c144b-227">Aşağıdaki örneğine hello tooadd bir ek ad sunucusu toohello NS kaydı hello bölgenin tepesinde nasıl ayarlanacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c144b-227">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="toomodify-record-set-metadata"></a><span data-ttu-id="c144b-228">meta veri toomodify kayıt kümesi</span><span class="sxs-lookup"><span data-stu-id="c144b-228">toomodify record set metadata</span></span>

<span data-ttu-id="c144b-229">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="c144b-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="c144b-230">Merhaba aşağıdaki örnek varolan bir kaydı toomodify hello meta verileri nasıl ayarlanacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c144b-230">hello following example shows how toomodify hello metadata of an existing record set:</span></span>

```powershell
# Get hello record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="c144b-231">Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="c144b-231">Delete a record set</span></span>

<span data-ttu-id="c144b-232">Kayıt kümeleri hello kullanarak silinebilir `Remove-AzureRmDnsRecordSet` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="c144b-232">Record sets can be deleted by using hello `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="c144b-233">Kayıt kümesi siliniyor hello kayıt kümesi içindeki tüm kayıtları siler.</span><span class="sxs-lookup"><span data-stu-id="c144b-233">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="c144b-234">Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="c144b-234">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="c144b-235">Azure DNS Hello bölge oluşturuldu ve hello bölge silindiğinde bunları otomatik olarak siler. Bunlar otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c144b-235">Azure DNS created these automatically when hello zone was created, and deletes them automatically when hello zone is deleted.</span></span>

<span data-ttu-id="c144b-236">Merhaba aşağıdaki örnek bir kayıt toodelete nasıl ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c144b-236">hello following example shows how toodelete a record set.</span></span> <span data-ttu-id="c144b-237">Bu örnekte, hello kayıt kümesi adını, kayıt kümesi türü, bölge adını ve kaynak grubu her açıkça belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="c144b-237">In this example, hello record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="c144b-238">Alternatif olarak, hello kayıt kümesi adı ve türü ile belirtilebilir ve hello bölge belirtilen nesneyi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="c144b-238">Alternatively, hello record set can be specified by name and type, and hello zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="c144b-239">Üçüncü seçenek olarak, bir kayıt kümesi nesnesi kullanılarak hello kayıt kendisini kümesi belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="c144b-239">As a third option, hello record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="c144b-240">Merhaba kayıt kümesinin bir kayıt kümesi nesnesi kullanarak silinmiş toobe belirttiğinizde [Etag denetler](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri silinmez.</span><span class="sxs-lookup"><span data-stu-id="c144b-240">When you specify hello record set toobe deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used tooensure concurrent changes are not deleted.</span></span> <span data-ttu-id="c144b-241">İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.</span><span class="sxs-lookup"><span data-stu-id="c144b-241">You can use hello optional `-Overwrite` switch toosuppress these checks.</span></span>

<span data-ttu-id="c144b-242">Merhaba kayıt kümesi nesnesi bir parametre olarak geçirilen yerine de yöneltilen:</span><span class="sxs-lookup"><span data-stu-id="c144b-242">hello record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="c144b-243">Onay istekleri</span><span class="sxs-lookup"><span data-stu-id="c144b-243">Confirmation prompts</span></span>

<span data-ttu-id="c144b-244">Merhaba `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, ve `Remove-AzureRmDnsRecordSet` cmdlet'leri tüm destek onay ister.</span><span class="sxs-lookup"><span data-stu-id="c144b-244">hello `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="c144b-245">Merhaba, her cmdlet için onay ister `$ConfirmPreference` PowerShell tercih değişkeni değerine sahip `Medium` veya daha düşük.</span><span class="sxs-lookup"><span data-stu-id="c144b-245">Each cmdlet prompts for confirmation if hello `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="c144b-246">Merhaba varsayılan değeri itibaren `$ConfirmPreference` olan `High`, bu komut istemlerini hello varsayılan PowerShell ayarlarını kullanırken verilmez.</span><span class="sxs-lookup"><span data-stu-id="c144b-246">Since hello default value for `$ConfirmPreference` is `High`, these prompts are not given when using hello default PowerShell settings.</span></span>

<span data-ttu-id="c144b-247">Merhaba geçerli kılabilirsiniz `$ConfirmPreference` hello kullanarak ayarını `-Confirm` parametresi.</span><span class="sxs-lookup"><span data-stu-id="c144b-247">You can override hello current `$ConfirmPreference` setting using hello `-Confirm` parameter.</span></span> <span data-ttu-id="c144b-248">Belirtirseniz `-Confirm` veya `-Confirm:$True` , hello cmdlet sizden, önce onay çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="c144b-248">If you specify `-Confirm` or `-Confirm:$True` , hello cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="c144b-249">Belirtirseniz `-Confirm:$False` , hello cmdlet istenmez sizin için onay.</span><span class="sxs-lookup"><span data-stu-id="c144b-249">If you specify `-Confirm:$False` , hello cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="c144b-250">Hakkında daha fazla bilgi için `-Confirm` ve `$ConfirmPreference`, bkz: [tercih değişkenleri hakkında](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="c144b-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c144b-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c144b-251">Next steps</span></span>

<span data-ttu-id="c144b-252">Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="c144b-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="c144b-253">Nasıl çok öğrenin[bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.</span><span class="sxs-lookup"><span data-stu-id="c144b-253">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="c144b-254">Gözden geçirme hello [Azure DNS PowerShell başvuru belgeleri](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="c144b-254">Review hello [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
