---
title: "Azure PowerShell kullanarak Azure DNS'de DNS kayıtlarını yönetme | Microsoft Docs"
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
ms.openlocfilehash: 2962e30e5d9c60b8e786e2ba79647cabfc5925cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-azure-powershell"></a><span data-ttu-id="238ba-104">DNS kayıtlarını ve kayıt kümeleri Azure PowerShell kullanarak Azure DNS'de yönetme</span><span class="sxs-lookup"><span data-stu-id="238ba-104">Manage DNS records and recordsets in Azure DNS using Azure PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="238ba-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="238ba-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="238ba-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="238ba-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="238ba-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="238ba-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="238ba-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="238ba-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="238ba-109">Bu makalede, Azure PowerShell kullanarak DNS bölgenizi için DNS kayıtlarını yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="238ba-109">This article shows you how to manage DNS records for your DNS zone by using Azure PowerShell.</span></span> <span data-ttu-id="238ba-110">DNS kayıtlarını da yönetilebilir platformlar arası kullanarak [Azure CLI](dns-operations-recordsets-cli.md) veya [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="238ba-110">DNS records can also be managed by using the cross-platform [Azure CLI](dns-operations-recordsets-cli.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

<span data-ttu-id="238ba-111">Bu makaledeki örneklerde, zaten sahip varsayılmaktadır [, oturum açan Azure PowerShell yüklenmiş ve bir DNS bölgesi oluşturulan](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="238ba-111">The examples in this article assume you have already [installed Azure PowerShell, signed in, and created a DNS zone](dns-operations-dnszones.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="238ba-112">Giriş</span><span class="sxs-lookup"><span data-stu-id="238ba-112">Introduction</span></span>

<span data-ttu-id="238ba-113">Azure DNS’de DNS kayıtlarını oluşturmadan önce Azure DNS’nin DNS kayıtlarını DNS kayıt kümeleri şeklinde nasıl düzenlediğini kavramanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="238ba-113">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="238ba-114">Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="238ba-114">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>


## <a name="create-a-new-dns-record"></a><span data-ttu-id="238ba-115">Yeni bir DNS kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="238ba-115">Create a new DNS record</span></span>

<span data-ttu-id="238ba-116">Yeni kaydınız aynı ad ve varolan bir kayıt türü varsa, gerek [var kayıt kümesine ekleme](#add-a-record-to-an-existing-record-set).</span><span class="sxs-lookup"><span data-stu-id="238ba-116">If your new record has the same name and type as an existing record, you need to [add it to the existing record set](#add-a-record-to-an-existing-record-set).</span></span> <span data-ttu-id="238ba-117">Farklı bir ad ve tüm mevcut kayıtları tür yeni kaydınız varsa, yeni bir kayıt kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="238ba-117">If your new record has a different name and type to all existing records, you need to create a new record set.</span></span> 

### <a name="create-a-records-in-a-new-record-set"></a><span data-ttu-id="238ba-118">Yeni bir kayıt kümesinde 'Bir' kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-118">Create 'A' records in a new record set</span></span>

<span data-ttu-id="238ba-119">`New-AzureRmDnsRecordSet` cmdlet’ini kullanarak kayıt kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="238ba-119">You create record sets by using the `New-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="238ba-120">Kayıt kümesi oluştururken, kaydı Canlı (TTL), ad, bölge, saati ayarlamak belirtmek zorunda oluşturulacak kayıt türünü ve kaydeder.</span><span class="sxs-lookup"><span data-stu-id="238ba-120">When creating a record set, you need to specify the record set name, the zone, the time to live (TTL), the record type, and the records to be created.</span></span>

<span data-ttu-id="238ba-121">Bir kayıt kümesine kayıt eklemeye yönelik parametreler, kayıt kümesinin türüne bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="238ba-121">The parameters for adding records to a record set vary depending on the type of the record set.</span></span> <span data-ttu-id="238ba-122">Örneğin, 'A' türündeki kayıt kümesi kullanırken, parametre kullanarak IP adresini belirtmek ihtiyacınız `-IPv4Address`.</span><span class="sxs-lookup"><span data-stu-id="238ba-122">For example, when using a record set of type 'A', you need to specify the IP address using the parameter `-IPv4Address`.</span></span> <span data-ttu-id="238ba-123">Diğer parametreler diğer kayıt türleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238ba-123">Other parameters are used for other record types.</span></span> <span data-ttu-id="238ba-124">Bkz: [ek kayıt türü örnekleri](#additional-record-type-examples) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="238ba-124">See [Additional record type examples](#additional-record-type-examples) for details.</span></span>

<span data-ttu-id="238ba-125">Aşağıdaki örnek, bir kayıt DNS bölgesinde "contoso.com" göreli adına sahip 'www' kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="238ba-125">The following example creates a record set with the relative name 'www' in the DNS Zone 'contoso.com'.</span></span> <span data-ttu-id="238ba-126">Tam kayıt kümesinin 'www.contoso.com' adıdır.</span><span class="sxs-lookup"><span data-stu-id="238ba-126">The fully-qualified name of the record set is 'www.contoso.com'.</span></span> <span data-ttu-id="238ba-127">'A' kayıt türüdür ve TTL 3600 saniye.</span><span class="sxs-lookup"><span data-stu-id="238ba-127">The record type is 'A', and the TTL is 3600 seconds.</span></span> <span data-ttu-id="238ba-128">Kayıt kümesi '1.2.3.4' IP adresiyle tek bir kayıt içerir.</span><span class="sxs-lookup"><span data-stu-id="238ba-128">The record set contains a single record, with IP address '1.2.3.4'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="238ba-129">Bir kayıt 'tepesinde' bir bölgenin kümesi oluşturmak için (Bu durumda, "contoso.com"), kayıt kümesi adını kullanın ' @' (tırnak işaretleri hariç):</span><span class="sxs-lookup"><span data-stu-id="238ba-129">To create a record set at the 'apex' of a zone (in this case, 'contoso.com'), use the record set name '@' (excluding quotation marks):</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") 
```

<span data-ttu-id="238ba-130">Bir kayıt birden çok kayıt içeren kümesi oluşturmanız gerekiyorsa, ilk yerel bir dizi oluşturmak ve kayıtları ekleyin ve sonra diziye geçirmek `New-AzureRmDnsRecordSet` gibi:</span><span class="sxs-lookup"><span data-stu-id="238ba-130">If you need to create a record set containing more than one record, first create a local array and add the records, then pass the array to `New-AzureRmDnsRecordSet` as follows:</span></span>

```powershell
$aRecords = @()
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4"
$aRecords += New-AzureRmDnsRecordConfig -IPv4Address "2.3.4.5"
New-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName MyResourceGroup -Ttl 3600 -RecordType A -DnsRecords $aRecords
```

<span data-ttu-id="238ba-131">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) uygulamaya özgü verileri anahtar-değer çiftleri olarak her bir kayıt kümesi ile ilişkilendirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="238ba-131">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="238ba-132">Aşağıdaki örnekte bir kayıt iki meta veri girişlerle kümesi oluşturma gösterilmektedir ' bölüm Finans =' ve ' ortam Üretim ='.</span><span class="sxs-lookup"><span data-stu-id="238ba-132">The following example shows how to create a record set with two metadata entries, 'dept=finance' and 'environment=production'.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -IPv4Address "1.2.3.4") -Metadata @{ dept="finance"; environment="production" } 
```

<span data-ttu-id="238ba-133">Azure DNS, ayrıca DNS kayıtlarını oluşturmadan önce bir DNS adı ayırmak için bir yer tutucu olarak davranıp 'empty' kayıt kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="238ba-133">Azure DNS also supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="238ba-134">Boş kayıt kümeleri içinde Azure DNS denetim düzlemi görünür, ancak Azure DNS ad sunucuları üzerinde görünür.</span><span class="sxs-lookup"><span data-stu-id="238ba-134">Empty record sets are visible in the Azure DNS control plane, but do appear on the Azure DNS name servers.</span></span> <span data-ttu-id="238ba-135">Aşağıdaki örnek, boş bir kayıt kümesi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="238ba-135">The following example creates an empty record set:</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords @()
```

## <a name="create-records-of-other-types"></a><span data-ttu-id="238ba-136">Diğer türleri kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-136">Create records of other types</span></span>

<span data-ttu-id="238ba-137">Aşağıdaki örnekler, ayrıntılı olarak 'Bir' kayıtları oluşturmak nasıl görülen, Azure DNS sunucuları tarafından desteklenen diğer kayıt türlerinin kayıtları oluşturmak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="238ba-137">Having seen in detail how to create 'A' records, the following examples show how to create records of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="238ba-138">Her durumda, tek bir kayıt içeren ayarlamak kaydının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="238ba-138">In each case, we show how to create a record set containing a single record.</span></span> <span data-ttu-id="238ba-139">'Bir' kayıtları önceki örneklerde, meta veriler ile birden çok kayıt içeren diğer türleri kayıt kümesini oluşturun veya boş kaydı kümeleri oluşturmak için uyarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="238ba-139">The earlier examples for 'A' records can be adapted to create record sets of other types containing multiple records, with metadata, or to create empty record sets.</span></span>

<span data-ttu-id="238ba-140">SOAs oluşturulduğundan bir SOA kayıt kümesi oluşturmak için örnek vermeyin ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="238ba-140">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="238ba-141">Ancak, [SOA, bir sonraki örnekte gösterildiği gibi değiştirilebilir](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="238ba-141">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record-set-with-a-single-record"></a><span data-ttu-id="238ba-142">Tek kayıtlı bir AAAA kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-142">Create an AAAA record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-aaaa" -RecordType AAAA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ipv6Address "2607:f8b0:4009:1803::1005") 
```

### <a name="create-a-cname-record-set-with-a-single-record"></a><span data-ttu-id="238ba-143">Tek kayıtlı bir CNAME kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-143">Create a CNAME record set with a single record</span></span>

> [!NOTE]
> <span data-ttu-id="238ba-144">DNS standartlarında bir bölge tepesinde CNAME kayıtlarına izin vermediği (`-Name '@'`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.</span><span class="sxs-lookup"><span data-stu-id="238ba-144">The DNS standards do not permit CNAME records at the apex of a zone (`-Name '@'`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="238ba-145">Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="238ba-145">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "test-cname" -RecordType CNAME -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Cname "www.contoso.com") 
```

### <a name="create-an-mx-record-set-with-a-single-record"></a><span data-ttu-id="238ba-146">Tek kayıtlı bir MX kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-146">Create an MX record set with a single record</span></span>

<span data-ttu-id="238ba-147">Bu örnekte, kayıt kümesi adını kullanıyoruz ' @' bölgenin tepesinde bir MX kaydı oluşturmak için (Bu durumda, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="238ba-147">In this example, we use the record set name '@' to create an MX record at the zone apex (in this case, 'contoso.com').</span></span>


```powershell
New-AzureRmDnsRecordSet -Name "@" -RecordType MX -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Exchange "mail.contoso.com" -Preference 5) 
```

### <a name="create-an-ns-record-set-with-a-single-record"></a><span data-ttu-id="238ba-148">Tek kayıtlı bir NS kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-148">Create an NS record set with a single record</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-ns" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Nsdname "ns1.contoso.com") 
```

### <a name="create-a-ptr-record-set-with-a-single-record"></a><span data-ttu-id="238ba-149">Tek kayıtlı bir PTR kaydı kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-149">Create a PTR record set with a single record</span></span>

<span data-ttu-id="238ba-150">Bu durumda, ' my-arpa-zone.com' IP aralığınızı temsil eden ARPA geriye doğru arama bölgesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="238ba-150">In this case, 'my-arpa-zone.com' represents the ARPA reverse lookup zone representing your IP range.</span></span> <span data-ttu-id="238ba-151">Bu bölgedeki her PTR kaydı bu IP aralığındaki bir IP adresine karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="238ba-151">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span> <span data-ttu-id="238ba-152">Kayıt '10' IP adresi bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi addır.</span><span class="sxs-lookup"><span data-stu-id="238ba-152">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 10 -RecordType PTR -ZoneName "my-arpa-zone.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "myservice.contoso.com") 
```

### <a name="create-an-srv-record-set-with-a-single-record"></a><span data-ttu-id="238ba-153">Tek kayıtlı bir SRV kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-153">Create an SRV record set with a single record</span></span>

<span data-ttu-id="238ba-154">Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), belirtin  *\_hizmet* ve  *\_Protokolü* kayıt kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="238ba-154">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="238ba-155">Dahil etmek için gerekli ' @' kayıt kümesi adında SRV kayıt kümesi bölgenin tepesinde oluştururken.</span><span class="sxs-lookup"><span data-stu-id="238ba-155">There is no need to include '@' in the record set name when creating an SRV record set at the zone apex.</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "_sip._tls" -RecordType SRV -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Priority 0 -Weight 5 -Port 8080 -Target "sip.contoso.com") 
```


### <a name="create-a-txt-record-set-with-a-single-record"></a><span data-ttu-id="238ba-156">Bir tek kayıtlı bir TXT kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="238ba-156">Create a TXT record set with a single record</span></span>

<span data-ttu-id="238ba-157">Aşağıdaki örnek, bir TXT kaydını oluşturmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="238ba-157">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="238ba-158">TXT kayıtlarının desteklenen maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="238ba-158">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "test-txt" -RecordType TXT -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Value "This is a TXT record") 
```


## <a name="get-a-record-set"></a><span data-ttu-id="238ba-159">Bir kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="238ba-159">Get a record set</span></span>

<span data-ttu-id="238ba-160">Varolan bir kayıt kümesini almak kullanın `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="238ba-160">To retrieve an existing record set, use `Get-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="238ba-161">Bu cmdlet kayıt Azure DNS'de kümesine temsil eden yerel bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="238ba-161">This cmdlet returns a local object that represents the record set in Azure DNS.</span></span>

<span data-ttu-id="238ba-162">İle `New-AzureRmDnsRecordSet`, verilen kayıt kümesi adı olmalıdır bir *göreli* ad, bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="238ba-162">As with `New-AzureRmDnsRecordSet`, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="238ba-163">Ayrıca kayıt türünü belirtmeniz gerekir ve kayıt içeren dilimini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="238ba-163">You also need to specify the record type, and the zone containing the record set.</span></span>

<span data-ttu-id="238ba-164">Aşağıdaki örnek, bir kayıt kümesini Al gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="238ba-164">The following example shows how to retrieve a record set.</span></span> <span data-ttu-id="238ba-165">Bu örnekte, bölgenin kullanarak belirtilen `-ZoneName` ve `-ResourceGroupName` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="238ba-165">In this example, the zone is specified using the `-ZoneName` and `-ResourceGroupName` parameters.</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="238ba-166">Alternatif olarak, aynı zamanda kullanılarak geçirilen bir bölge nesnesi kullanarak bölgesi belirtebilirsiniz `-Zone` parametresi.</span><span class="sxs-lookup"><span data-stu-id="238ba-166">Alternatively, you can also specify the zone using a zone object, passed using the `-Zone` parameter.</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs = Get-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

## <a name="list-record-sets"></a><span data-ttu-id="238ba-167">Liste kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="238ba-167">List record sets</span></span>

<span data-ttu-id="238ba-168">Aynı zamanda `Get-AzureRmDnsZone` listesini atlanması tarafından bir bölgedeki kayıt kümelerine `-Name` ve/veya `-RecordType` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="238ba-168">You can also use `Get-AzureRmDnsZone` to list record sets in a zone, by omitting the `-Name` and/or `-RecordType` parameters.</span></span>

<span data-ttu-id="238ba-169">Aşağıdaki örnekte, tüm kayıt bölgede ayarlar döndürür:</span><span class="sxs-lookup"><span data-stu-id="238ba-169">The following example returns all record sets in the zone:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="238ba-170">Aşağıdaki örnek, tüm kayıt kümeleri belirli bir türde nasıl gösterir kaydı atlama kümesi adı kayıt türü belirterek alınabilir:</span><span class="sxs-lookup"><span data-stu-id="238ba-170">The following example shows how all record sets of a given type can be retrieved by specifying the record type while omitting the record set name:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="238ba-171">Kayıt türleri arasında belirli bir ada sahip tüm kayıt kümelerini almak için tüm kayıt kümelerinin almak ve sonuçlara filtre uygulamak gerekir:</span><span class="sxs-lookup"><span data-stu-id="238ba-171">To retrieve all record sets with a given name, across record types, you need to retrieve all record sets and then filter the results:</span></span>

```powershell
$recordsets = Get-AzureRmDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | where {$_.Name.Equals("www")}
```

<span data-ttu-id="238ba-172">Tüm Yukarıdaki örneklerde, bölge ya da kullanılarak belirtilebilir `-ZoneName` ve `-ResourceGroupName`parametreleri (gösterildiği gibi) veya bir bölge nesnesi belirterek:</span><span class="sxs-lookup"><span data-stu-id="238ba-172">In all the above examples, the zone can be specified either by using the `-ZoneName` and `-ResourceGroupName`parameters (as shown), or by specifying a zone object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
$recordsets = Get-AzureRmDnsRecordSet -Zone $zone
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="238ba-173">Bir kaydı var olan bir kayıt kümesine ekleme</span><span class="sxs-lookup"><span data-stu-id="238ba-173">Add a record to an existing record set</span></span>

<span data-ttu-id="238ba-174">Bir kaydı var olan bir kayıt kümesine eklemek için aşağıdaki üç adımı izleyin:</span><span class="sxs-lookup"><span data-stu-id="238ba-174">To add a record to an existing record set, follow the following three steps:</span></span>

1. <span data-ttu-id="238ba-175">Mevcut kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="238ba-175">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="238ba-176">Yeni kayıttaki yerel kayıt kümesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="238ba-176">Add the new record to the local record set.</span></span> <span data-ttu-id="238ba-177">Bu çevrimdışı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="238ba-177">This is an off-line operation.</span></span>

    ```powershell
    Add-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="238ba-178">Değişikliği geri Azure DNS hizmeti uygulayın.</span><span class="sxs-lookup"><span data-stu-id="238ba-178">Commit the change back to the Azure DNS service.</span></span> 

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $rs
    ```

<span data-ttu-id="238ba-179">Kullanarak `Set-AzureRmDnsRecordSet` *değiştirir* mevcut kayıt Azure DNS (ve içerdiği tüm kayıtları) belirtilen kayıt kümesi ile kümesi.</span><span class="sxs-lookup"><span data-stu-id="238ba-179">Using `Set-AzureRmDnsRecordSet` *replaces* the existing record set in Azure DNS (and all records it contains) with the record set specified.</span></span> <span data-ttu-id="238ba-180">[ETag denetimleri](dns-zones-records.md#etags) eşzamanlı değişiklikleri yazılmaz sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238ba-180">[Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="238ba-181">Kullanabileceğiniz isteğe bağlı `-Overwrite` bu denetimleri gizlemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="238ba-181">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="238ba-182">Bu işlem dizisi de olabilir *yöneltilen*, parametre olarak geçirme yerine kanal kullanarak kayıt kümesi nesnesi geçirdiğiniz anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="238ba-182">This sequence of operations can also be *piped*, meaning you pass the record set object by using the pipe rather than passing it as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name "www" –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Add-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="238ba-183">Yukarıdaki örnekler bir '' kayıt türü 'A' Varolan kayıt kümesine eklemek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="238ba-183">The examples above show how to add an 'A' record to an existing record set of type 'A'.</span></span> <span data-ttu-id="238ba-184">Benzer bir işlem dizisi değiştirerek diğer türleri kayıt kümelerine kayıtları eklemek için kullanılan `-Ipv4Address` parametresinin `Add-AzureRmDnsRecordConfig` her bir kayıt türü belirli diğer parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="238ba-184">A similar sequence of operations is used to add records to record sets of other types, substituting the `-Ipv4Address` parameter of `Add-AzureRmDnsRecordConfig` with other parameters specific to each record type.</span></span> <span data-ttu-id="238ba-185">Her bir kayıt türü için parametreler aynıdır `New-AzureRmDnsRecordConfig` gösterildiği gibi cmdlet [ek kayıt türü örnekleri](#additional-record-type-examples) üstünde.</span><span class="sxs-lookup"><span data-stu-id="238ba-185">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>

<span data-ttu-id="238ba-186">Kayıt kümeleri 'CNAME' veya 'SOA' türünde birden fazla kayıt içeremez.</span><span class="sxs-lookup"><span data-stu-id="238ba-186">Record sets of type 'CNAME' or 'SOA' cannot contain more than one record.</span></span> <span data-ttu-id="238ba-187">Bu sınırlama DNS standartları ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="238ba-187">This constraint arises from the DNS standards.</span></span> <span data-ttu-id="238ba-188">Azure DNS sınırlandırılmasıdır değil.</span><span class="sxs-lookup"><span data-stu-id="238ba-188">It is not a limitation of Azure DNS.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="238ba-189">Varolan bir kayıt kümesinden bir kaydı kaldırma</span><span class="sxs-lookup"><span data-stu-id="238ba-189">Remove a record from an existing record set</span></span>

<span data-ttu-id="238ba-190">Bir kayıt kümesinden bir kaydı kaldırma işlemini, var olan bir kayıt kümesine kayıt ekleme işlemi benzerdir:</span><span class="sxs-lookup"><span data-stu-id="238ba-190">The process to remove a record from a record set is similar to the process to add a record to an existing record set:</span></span>

1. <span data-ttu-id="238ba-191">Mevcut kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="238ba-191">Get the existing record set</span></span>

    ```powershell
    $rs = Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A
    ```

2. <span data-ttu-id="238ba-192">Kayıt yerel kayıt kümesi nesnesinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="238ba-192">Remove the record from the local record set object.</span></span> <span data-ttu-id="238ba-193">Bu çevrimdışı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="238ba-193">This is an off-line operation.</span></span> <span data-ttu-id="238ba-194">Kaldırılmakta kaydı varolan bir kayıtla tam bir eşleşme tüm parametreleri arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="238ba-194">The record that's being removed must be an exact match with an existing record across all parameters.</span></span>

    ```powershell
    Remove-AzureRmDnsRecordConfig -RecordSet $rs -Ipv4Address "5.6.7.8"
    ```

3. <span data-ttu-id="238ba-195">Değişikliği geri Azure DNS hizmeti uygulayın.</span><span class="sxs-lookup"><span data-stu-id="238ba-195">Commit the change back to the Azure DNS service.</span></span> <span data-ttu-id="238ba-196">İsteğe bağlı kullanmak `-Overwrite` gizlemek için anahtar [Etag denetler](dns-zones-records.md#etags) eşzamanlı değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="238ba-196">Use the optional `-Overwrite` switch to suppress [Etag checks](dns-zones-records.md#etags) for concurrent changes.</span></span>

    ```powershell
    Set-AzureRmDnsRecordSet -RecordSet $Rs
    ```

<span data-ttu-id="238ba-197">Son kaydı kayıt kümesinden kaldırmak için yukarıdaki dizisi kullanılarak kayıt kümesi silinmez, bunun yerine boş bir kayıt kümesi bırakır.</span><span class="sxs-lookup"><span data-stu-id="238ba-197">Using the above sequence to remove the last record from a record set does not delete the record set, rather it leaves an empty record set.</span></span> <span data-ttu-id="238ba-198">Bir kayıt kümesi tamamen kaldırmak için bkz: [bir kayıt kümesini Sil](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="238ba-198">To remove a record set entirely, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="238ba-199">Benzer şekilde bir kayıt kümesine kayıt eklemeye bir kayıt kümesini kaldırmak için işlem dizisi de yöneltilen:</span><span class="sxs-lookup"><span data-stu-id="238ba-199">Similarly to adding records to a record set, the sequence of operations to remove a record set can also be piped:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www –ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" -RecordType A | Remove-AzureRmDnsRecordConfig -Ipv4Address "5.6.7.8" | Set-AzureRmDnsRecordSet
```

<span data-ttu-id="238ba-200">Farklı kayıt türleri için uygun türe özgü parametreleri geçirerek desteklenir `Remove-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="238ba-200">Different record types are supported by passing the appropriate type-specific parameters to `Remove-AzureRmDnsRecordSet`.</span></span> <span data-ttu-id="238ba-201">Her bir kayıt türü için parametreler aynıdır `New-AzureRmDnsRecordConfig` gösterildiği gibi cmdlet [ek kayıt türü örnekleri](#additional-record-type-examples) üstünde.</span><span class="sxs-lookup"><span data-stu-id="238ba-201">The parameters for each record type are the same as for the `New-AzureRmDnsRecordConfig` cmdlet, as shown in [Additional record type examples](#additional-record-type-examples) above.</span></span>


## <a name="modify-an-existing-record-set"></a><span data-ttu-id="238ba-202">Varolan bir kayıt kümesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="238ba-202">Modify an existing record set</span></span>

<span data-ttu-id="238ba-203">Varolan bir kayıt kümesini değiştirme adımları ekleme veya kayıt kümesindeki kayıt kaldırırken adımlar benzerdir:</span><span class="sxs-lookup"><span data-stu-id="238ba-203">The steps for modifying an existing record set are similar to the steps you take when adding or removing records from a record set:</span></span>

1. <span data-ttu-id="238ba-204">Varolan kayıt kullanarak kümesi almak `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="238ba-204">Retrieve the existing record set by using `Get-AzureRmDnsRecordSet`.</span></span>
2. <span data-ttu-id="238ba-205">Yerel kayıt kümesi nesnesi tarafından değiştirin:</span><span class="sxs-lookup"><span data-stu-id="238ba-205">Modify the local record set object by:</span></span>
    * <span data-ttu-id="238ba-206">Ekleme veya kayıt kaldırma</span><span class="sxs-lookup"><span data-stu-id="238ba-206">Adding or removing records</span></span>
    * <span data-ttu-id="238ba-207">Varolan kayıtları parametrelerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="238ba-207">Changing the parameters of existing records</span></span>
    * <span data-ttu-id="238ba-208">Kayıt değiştirme, meta verileri ve zamanı dinamik (TTL) ayarlayın</span><span class="sxs-lookup"><span data-stu-id="238ba-208">Changing the record set metadata and time to live (TTL)</span></span>
3. <span data-ttu-id="238ba-209">Kullanarak, değişiklikleri `Set-AzureRmDnsRecordSet` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="238ba-209">Commit your changes by using the `Set-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="238ba-210">Bu *değiştirir* mevcut kayıt belirtilen kayıt kümesi ile Azure DNS'de kümesi.</span><span class="sxs-lookup"><span data-stu-id="238ba-210">This *replaces* the existing record set in Azure DNS with the record set specified.</span></span>

<span data-ttu-id="238ba-211">Kullanırken `Set-AzureRmDnsRecordSet`, [Etag denetler](dns-zones-records.md#etags) eşzamanlı değişiklikleri yazılmaz sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238ba-211">When using `Set-AzureRmDnsRecordSet`, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not overwritten.</span></span> <span data-ttu-id="238ba-212">Kullanabileceğiniz isteğe bağlı `-Overwrite` bu denetimleri gizlemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="238ba-212">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

### <a name="to-update-a-record-in-an-existing-record-set"></a><span data-ttu-id="238ba-213">Varolan bir kayıt kümesindeki bir kaydı güncelleştirmeye</span><span class="sxs-lookup"><span data-stu-id="238ba-213">To update a record in an existing record set</span></span>

<span data-ttu-id="238ba-214">Bu örnekte, varolan 'Bir' kaydı IP adresini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="238ba-214">In this example, we change the IP address of an existing 'A' record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Ipv4Address = "9.8.7.6"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="238ba-215">Bir SOA kaydına değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="238ba-215">To modify an SOA record</span></span>

<span data-ttu-id="238ba-216">Ekleme veya kayıtları otomatik olarak oluşturulan SOA kayıt bölgenin tepesinde kümesi kaldırın (`-Name "@"`, tırnak işaretleri dahil olmak üzere).</span><span class="sxs-lookup"><span data-stu-id="238ba-216">You cannot add or remove records from the automatically created SOA record set at the zone apex (`-Name "@"`, including quote marks).</span></span> <span data-ttu-id="238ba-217">Ancak, SOA kaydı (dışında "ana bilgisayar") içinde parametrelerinden herhangi birini değiştirmek ve TTL kaydı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="238ba-217">However, you can modify any of the parameters within the SOA record (except "Host") and the record set TTL.</span></span>

<span data-ttu-id="238ba-218">Aşağıdaki örnekte nasıl değiştirileceğini gösterir *e-posta* SOA kaydı özelliği:</span><span class="sxs-lookup"><span data-stu-id="238ba-218">The following example shows how to change the *Email* property of the SOA record:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType SOA -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
$rs.Records[0].Email = "admin.contoso.com"
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="238ba-219">Bölge tepesinde NS kayıtları değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="238ba-219">To modify NS records at the zone apex</span></span>

<span data-ttu-id="238ba-220">NS kayıt bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="238ba-220">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="238ba-221">Bölgeye atanan Azure DNS ad sunucularının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="238ba-221">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="238ba-222">Birden fazla DNS sağlayıcınız ile birlikte barındırma etki alanlarını destekleyecek şekilde bu NS kaydının sunucularına ayarlayın ek ad ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="238ba-222">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="238ba-223">Bu kayıt kümesi için meta verileri ve TTL de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="238ba-223">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="238ba-224">Ancak, kaldırmak veya önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="238ba-224">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="238ba-225">Bu bölge tepesinde yalnızca NS kayıt kümesi için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="238ba-225">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="238ba-226">(Alt bölgelere temsilci seçmek için kullanıldığı şekilde), bu bölgedeki diğer NS kayıt kümelerini kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="238ba-226">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="238ba-227">Aşağıdaki örnekte, bölgenin tepesinde ayarlamak NS kaydı bir ek ad sunucusu eklemek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="238ba-227">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Add-AzureRmDnsRecordConfig -RecordSet $rs -Nsdname ns1.myotherdnsprovider.com
Set-AzureRmDnsRecordSet -RecordSet $rs
```

### <a name="to-modify-record-set-metadata"></a><span data-ttu-id="238ba-228">Kayıt kümesi meta verilerini değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="238ba-228">To modify record set metadata</span></span>

<span data-ttu-id="238ba-229">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) uygulamaya özgü verileri anahtar-değer çiftleri olarak her bir kayıt kümesi ile ilişkilendirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="238ba-229">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="238ba-230">Aşağıdaki örnek, varolan bir kayıt kümesini meta verileri değiştirmeye gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="238ba-230">The following example shows how to modify the metadata of an existing record set:</span></span>

```powershell
# Get the record set
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"

# Add 'dept=finance' name-value pair
$rs.Metadata.Add('dept', 'finance') 

# Remove metadata item named 'environment'
$rs.Metadata.Remove('environment')  

# Commit changes
Set-AzureRmDnsRecordSet -RecordSet $rs
```


## <a name="delete-a-record-set"></a><span data-ttu-id="238ba-231">Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="238ba-231">Delete a record set</span></span>

<span data-ttu-id="238ba-232">Kayıt kümeleri kullanarak silinebilir `Remove-AzureRmDnsRecordSet` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="238ba-232">Record sets can be deleted by using the `Remove-AzureRmDnsRecordSet` cmdlet.</span></span> <span data-ttu-id="238ba-233">Kayıt kümesi siliniyor, kayıt kümesindeki tüm kayıtları siler.</span><span class="sxs-lookup"><span data-stu-id="238ba-233">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="238ba-234">SOA silemezsiniz ve NS kayıt kümeleri bölgenin tepesinde (`-Name '@'`).</span><span class="sxs-lookup"><span data-stu-id="238ba-234">You cannot delete the SOA and NS record sets at the zone apex (`-Name '@'`).</span></span>  <span data-ttu-id="238ba-235">Azure DNS bölgesi oluşturuldu ve bölge silindiğinde bunları otomatik olarak siler. Bunlar otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="238ba-235">Azure DNS created these automatically when the zone was created, and deletes them automatically when the zone is deleted.</span></span>

<span data-ttu-id="238ba-236">Aşağıdaki örnek, bir kayıt kümesini Sil gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="238ba-236">The following example shows how to delete a record set.</span></span> <span data-ttu-id="238ba-237">Bu örnekte, kayıt kümesi adını, kayıt kümesi türü, bölge adını ve kaynak grubu her açıkça belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="238ba-237">In this example, the record set name, record set type, zone name, and resource group are each specified explicitly.</span></span>

```powershell
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
```

<span data-ttu-id="238ba-238">Alternatif olarak, kayıt kümesi adını ve türünü ve nesneyi kullanarak belirtilen bölge tarafından belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="238ba-238">Alternatively, the record set can be specified by name and type, and the zone specified using an object:</span></span>

```powershell
$zone = Get-AzureRmDnsZone -Name "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -Name "www" -RecordType A -Zone $zone
```

<span data-ttu-id="238ba-239">Üçüncü seçenek olarak, kayıt kendisini kümesine bir kayıt kümesi nesnesi kullanılarak belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="238ba-239">As a third option, the record set itself can be specified using a record set object:</span></span>

```powershell
$rs = Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup"
Remove-AzureRmDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="238ba-240">Kayıt bir kayıt kümesi nesnesi kullanarak silinecek kümesi belirttiğinizde [Etag denetler](dns-zones-records.md#etags) eşzamanlı değişiklikleri silinmez sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="238ba-240">When you specify the record set to be deleted by using a record set object, [Etag checks](dns-zones-records.md#etags) are used to ensure concurrent changes are not deleted.</span></span> <span data-ttu-id="238ba-241">Kullanabileceğiniz isteğe bağlı `-Overwrite` bu denetimleri gizlemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="238ba-241">You can use the optional `-Overwrite` switch to suppress these checks.</span></span>

<span data-ttu-id="238ba-242">Kayıt kümesi nesnesi bir parametre olarak geçirilen yerine de yöneltilen:</span><span class="sxs-lookup"><span data-stu-id="238ba-242">The record set object can also be piped instead of being passed as a parameter:</span></span>

```powershell
Get-AzureRmDnsRecordSet -Name www -RecordType A -ZoneName "contoso.com" -ResourceGroupName "MyResourceGroup" | Remove-AzureRmDnsRecordSet
```

## <a name="confirmation-prompts"></a><span data-ttu-id="238ba-243">Onay istekleri</span><span class="sxs-lookup"><span data-stu-id="238ba-243">Confirmation prompts</span></span>

<span data-ttu-id="238ba-244">`New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, Ve `Remove-AzureRmDnsRecordSet` cmdlet'leri tüm destek onay ister.</span><span class="sxs-lookup"><span data-stu-id="238ba-244">The `New-AzureRmDnsRecordSet`, `Set-AzureRmDnsRecordSet`, and `Remove-AzureRmDnsRecordSet` cmdlets all support confirmation prompts.</span></span>

<span data-ttu-id="238ba-245">Her bir cmdlet için onay ister `$ConfirmPreference` PowerShell tercih değişkeni değerine sahip `Medium` veya daha düşük.</span><span class="sxs-lookup"><span data-stu-id="238ba-245">Each cmdlet prompts for confirmation if the `$ConfirmPreference` PowerShell preference variable has a value of `Medium` or lower.</span></span> <span data-ttu-id="238ba-246">İçin varsayılan değer itibaren `$ConfirmPreference` olan `High`, bu komut istemlerini varsayılan PowerShell ayarlarını kullanırken verilmez.</span><span class="sxs-lookup"><span data-stu-id="238ba-246">Since the default value for `$ConfirmPreference` is `High`, these prompts are not given when using the default PowerShell settings.</span></span>

<span data-ttu-id="238ba-247">Geçerli kılabilirsiniz `$ConfirmPreference` kullanarak ayarlama `-Confirm` parametresi.</span><span class="sxs-lookup"><span data-stu-id="238ba-247">You can override the current `$ConfirmPreference` setting using the `-Confirm` parameter.</span></span> <span data-ttu-id="238ba-248">Belirtirseniz `-Confirm` veya `-Confirm:$True` , cmdlet sizden onay kendisinden önce çalışır ister.</span><span class="sxs-lookup"><span data-stu-id="238ba-248">If you specify `-Confirm` or `-Confirm:$True` , the cmdlet prompts you for confirmation before it runs.</span></span> <span data-ttu-id="238ba-249">Belirtirseniz `-Confirm:$False` , cmdlet onaylamanız istenmez.</span><span class="sxs-lookup"><span data-stu-id="238ba-249">If you specify `-Confirm:$False` , the cmdlet does not prompt you for confirmation.</span></span> 

<span data-ttu-id="238ba-250">Hakkında daha fazla bilgi için `-Confirm` ve `$ConfirmPreference`, bkz: [tercih değişkenleri hakkında](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span><span class="sxs-lookup"><span data-stu-id="238ba-250">For more information about `-Confirm` and `$ConfirmPreference`, see [About Preference Variables](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).</span></span>

## <a name="next-steps"></a><span data-ttu-id="238ba-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="238ba-251">Next steps</span></span>

<span data-ttu-id="238ba-252">Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="238ba-252">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="238ba-253">Bilgi nasıl [bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.</span><span class="sxs-lookup"><span data-stu-id="238ba-253">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
<br>
<span data-ttu-id="238ba-254">Gözden geçirme [Azure DNS PowerShell başvuru belgeleri](/powershell/module/azurerm.dns).</span><span class="sxs-lookup"><span data-stu-id="238ba-254">Review the [Azure DNS PowerShell reference documentation](/powershell/module/azurerm.dns).</span></span>
