---
title: "Azure CLI 1.0 kullanarak Azure DNS'de DNS kayıtlarını yönetme | Microsoft Docs"
description: "DNS kayıt kümelerini ve Azure DNS kayıtlarını Azure DNS'nin etki alanınızda barındırdığında yönetme. Kayıt kümelerini ve kayıtları işlemleri için tüm CLI 1.0 komutları."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/20/2016
ms.author: jonatul
ms.openlocfilehash: 307b327e4c04a0461e39930114eb193791cbda9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-dns-records-in-azure-dns-using-the-azure-cli-10"></a><span data-ttu-id="e3414-104">Azure CLI 1.0 kullanarak Azure DNS'de DNS kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="e3414-104">Manage DNS records in Azure DNS using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3414-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e3414-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="e3414-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e3414-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="e3414-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e3414-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="e3414-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3414-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="e3414-109">Bu makalede, platformlar arası Azure komut satırı Windows, Mac ve Linux için kullanılabilir olan arabirimi (CLI) kullanarak DNS bölgenizi için DNS kayıtlarını yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e3414-109">This article shows you how to manage DNS records for your DNS zone by using the cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="e3414-110">DNS kayıtlarınızı kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-recordsets.md) veya [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e3414-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or the [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="e3414-111">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="e3414-111">CLI versions to complete the task</span></span>

<span data-ttu-id="e3414-112">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e3414-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="e3414-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md): Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI'mız.</span><span class="sxs-lookup"><span data-stu-id="e3414-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="e3414-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız.</span><span class="sxs-lookup"><span data-stu-id="e3414-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="e3414-115">Bu makaledeki örneklerde, zaten sahip varsayılmaktadır [, oturum açan Azure CLI 1.0 yüklü ve bir DNS bölgesi oluşturulan](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e3414-115">The examples in this article assume you have already [installed the Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="e3414-116">Giriş</span><span class="sxs-lookup"><span data-stu-id="e3414-116">Introduction</span></span>

<span data-ttu-id="e3414-117">Azure DNS’de DNS kayıtlarını oluşturmadan önce Azure DNS’nin DNS kayıtlarını DNS kayıt kümeleri şeklinde nasıl düzenlediğini kavramanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3414-117">Before creating DNS records in Azure DNS, you first need to understand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="e3414-118">Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="e3414-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="e3414-119">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3414-119">Create a DNS record</span></span>

<span data-ttu-id="e3414-120">DNS kaydı oluşturmak için `azure network dns record-set add-record` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="e3414-120">To create a DNS record, use the `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="e3414-121">Yardım için bkz. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="e3414-122">Bir kayıt oluştururken kaynak grubu adını, bölge adını, kaynak kümesi adını, kaynak türünü ve oluşturulan kaynağın ayrıntılarını belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3414-122">When creating a record, you need to specify the resource group name, zone name, record set name, the record type, and the details of the record being created.</span></span> <span data-ttu-id="e3414-123">Verilen kayıt kümesi adı olmalıdır bir *göreli* ad, bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e3414-123">The record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span>

<span data-ttu-id="e3414-124">Kayıt kümesi mevcut değilse bu komutla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e3414-124">If the record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="e3414-125">Kayıt kümesi zaten varsa, bu komutu olan varolan bir kayda belirttiğiniz kayıt ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e3414-125">If the record set already exists, this command adda the record you specify to the existing record set.</span></span>

<span data-ttu-id="e3414-126">Yeni bir kayıt kümesi oluşturuluyorsa yaşam süresi (TTL) olarak varsayılan 3600 değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e3414-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="e3414-127">Farklı TTLs kullanma hakkında daha fazla yönerge için bkz: [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="e3414-127">For instructions on how to use different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="e3414-128">Aşağıdaki örnek *www* adlı A kaydını *contoso.com* bölgesinde ve *MyResourceGroup* kaynak grubu içinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e3414-128">The following example creates an A record called *www* in the zone *contoso.com* in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="e3414-129">A kaydının IP adresi *1.2.3.4* olarak belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e3414-129">The IP address of the A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="e3414-130">Bölgenin tepesinde bir kayıt oluşturmak için (Bu durumda, "contoso.com"), kayıt adını kullanın "@", tırnak işaretleri dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="e3414-130">To create a record in the apex of the zone (in this case, "contoso.com"), use the record name "@", including the quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="e3414-131">DNS kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3414-131">Create a DNS record set</span></span>

<span data-ttu-id="e3414-132">Yukarıdaki örneklerde, DNS kaydı ya da var olan bir kayıt kümesine eklendi veya kayıt kümesi oluşturuldu *örtük olarak*.</span><span class="sxs-lookup"><span data-stu-id="e3414-132">In the above examples, the DNS record was either added to an existing record set, or the record set was created *implicitly*.</span></span> <span data-ttu-id="e3414-133">Kayıt kümesi de oluşturabilirsiniz *açıkça* kayıtlarını eklemeden önce.</span><span class="sxs-lookup"><span data-stu-id="e3414-133">You can also create the record set *explicitly* before adding records to it.</span></span> <span data-ttu-id="e3414-134">Azure DNS, DNS kayıtlarını oluşturmadan önce bir DNS adı ayırmak için bir yer tutucu olarak davranıp 'empty' kayıt kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="e3414-134">Azure DNS supports 'empty' record sets, which can act as a placeholder to reserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="e3414-135">Boş kaydı kümeleri Azure DNS denetim düzeyi görünür, ancak Azure DNS ad sunucuları üzerinde görünmez.</span><span class="sxs-lookup"><span data-stu-id="e3414-135">Empty record sets are visible in the Azure DNS control plane, but do not appear on the Azure DNS name servers.</span></span>

<span data-ttu-id="e3414-136">Kayıt kümeleri kullanarak oluşturulur `azure network dns record-set create` komutu.</span><span class="sxs-lookup"><span data-stu-id="e3414-136">Record sets are created using the `azure network dns record-set create` command.</span></span> <span data-ttu-id="e3414-137">Yardım için bkz. `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="e3414-138">Kayıt açıkça kümesi oluşturma kayıt kümesinin özellikler gibi belirtmenize olanak verir [yaşam süresi (TTL)](dns-zones-records.md#time-to-live) ve meta verileri.</span><span class="sxs-lookup"><span data-stu-id="e3414-138">Creating the record set explicitly allows you to specify record set properties such as the [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="e3414-139">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) uygulamaya özgü verileri anahtar-değer çiftleri olarak her bir kayıt kümesi ile ilişkilendirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3414-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="e3414-140">Aşağıdaki örnek, boş bir kayıt 60 saniye TTL ile kullanarak kümesi oluşturur `--ttl` parametre (kısa form `-l`):</span><span class="sxs-lookup"><span data-stu-id="e3414-140">The following example creates an empty record set with a 60-second TTL, by using the `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="e3414-141">Aşağıdaki örnek, bir kayıt iki meta veri girişlerle kümesi oluşturur "Bölüm Finans =" ve "ortam üretim =", kullanarak `--metadata` parametre (kısa form `-m`):</span><span class="sxs-lookup"><span data-stu-id="e3414-141">The following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="e3414-142">Boş bir kayıt kümesi oluşturulduktan sonra kayıtları kullanılarak eklenebilir `azure network dns record-set add-record` açıklandığı gibi [bir DNS kaydı oluşturma](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="e3414-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="e3414-143">Diğer türleri kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3414-143">Create records of other types</span></span>

<span data-ttu-id="e3414-144">Aşağıdaki örnekler, ayrıntılı olarak 'Bir' kayıtları oluşturmak nasıl görülen, Azure DNS sunucuları tarafından desteklenen diğer kayıt türlerinin kaydının nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3414-144">Having seen in detail how to create 'A' records, the following examples show how to create record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="e3414-145">Kayıt verilerini belirtmek için kullanılan parametreler, kayıt türüne bağlı olarak değişiklik gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3414-145">The parameters used to specify the record data vary depending on the type of the record.</span></span> <span data-ttu-id="e3414-146">Örneğin "A" türünde bir kayıt için IPv4 adresini `-a <IPv4 address>` parametresiyle belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3414-146">For example, for a record of type "A", you specify the IPv4 address with the parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="e3414-147">Her bir kayıt türü için parametreler kullanılarak listelenebilir `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-147">The parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="e3414-148">Her durumda, tek bir kaydını nasıl oluşturacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e3414-148">In each case, we show how to create a single record.</span></span> <span data-ttu-id="e3414-149">Kayıt, varolan bir kayıt kümesini veya örtük olarak oluşturulmuş bir kayıt kümesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="e3414-149">The record is added to the existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="e3414-150">Kayıt kümeleri oluşturma ve kayıt tanımlama hakkında daha fazla bilgi için parametre açıkça, bakın [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="e3414-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="e3414-151">SOAs oluşturulduğundan bir SOA kayıt kümesi oluşturmak için örnek vermeyin ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="e3414-151">We do not give an example to create an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="e3414-152">Ancak, [SOA, bir sonraki örnekte gösterildiği gibi değiştirilebilir](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="e3414-152">However, [the SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="e3414-153">Bir AAAA kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="e3414-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="e3414-154">Bir CNAME kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="e3414-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="e3414-155">DNS standartlarında bir bölge tepesinde CNAME kayıtlarına izin vermediği (`-Name "@"`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.</span><span class="sxs-lookup"><span data-stu-id="e3414-155">The DNS standards do not permit CNAME records at the apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="e3414-156">Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="e3414-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="e3414-157">MX kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3414-157">Create an MX record</span></span>

<span data-ttu-id="e3414-158">Bu örnekte, bölgenin tepesinde (bu durumda "contoso.com") MX kaydı oluşturmak için "@" kayıt kümesi adını kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="e3414-158">In this example, we use the record set name "@" to create the MX record at the zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="e3414-159">Bir NS kayıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3414-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="e3414-160">PTR kaydı oluştur</span><span class="sxs-lookup"><span data-stu-id="e3414-160">Create a PTR record</span></span>

<span data-ttu-id="e3414-161">Bu durumda, ' my-arpa-zone.com' IP aralığınızı temsil eden ARPA bölgeleri temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e3414-161">In this case, 'my-arpa-zone.com' represents the ARPA zone representing your IP range.</span></span> <span data-ttu-id="e3414-162">Bu bölgedeki her PTR kaydı bu IP aralığındaki bir IP adresine karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="e3414-162">Each PTR record set in this zone corresponds to an IP address within this IP range.</span></span>  <span data-ttu-id="e3414-163">Kayıt '10' IP adresi bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi addır.</span><span class="sxs-lookup"><span data-stu-id="e3414-163">The record name '10' is the last octet of the IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="e3414-164">Bir SRV kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="e3414-164">Create an SRV record</span></span>

<span data-ttu-id="e3414-165">Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), belirtin  *\_hizmet* ve  *\_Protokolü* kayıt kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="e3414-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify the *\_service* and *\_protocol* in the record set name.</span></span> <span data-ttu-id="e3414-166">Eklenecek gerek yoktur "@" kayıt kümesi adında SRV kayıt kümesi bölgenin tepesinde oluştururken.</span><span class="sxs-lookup"><span data-stu-id="e3414-166">There is no need to include "@" in the record set name when creating an SRV record set at the zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="e3414-167">TXT kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e3414-167">Create a TXT record</span></span>

<span data-ttu-id="e3414-168">Aşağıdaki örnek, bir TXT kaydını oluşturmak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e3414-168">The following example shows how to create a TXT record.</span></span> <span data-ttu-id="e3414-169">TXT kayıtlarının desteklenen maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="e3414-169">For more information about the maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="e3414-170">Bir kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="e3414-170">Get a record set</span></span>

<span data-ttu-id="e3414-171">Varolan bir kayıt kümesini almak kullanın `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="e3414-171">To retrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="e3414-172">Yardım için bkz. `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="e3414-173">Bir kayıt veya kayıt kümesi oluşturulurken verilen kayıt kümesi adı olmalıdır gibi bir *göreli* ad, bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="e3414-173">As when creating a record or record set, the record set name given must be a *relative* name, meaning it must exclude the zone name.</span></span> <span data-ttu-id="e3414-174">Kayıt kümesi ve bölge içeren kaynak grubunu içeren bölgesi kayıt türünü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e3414-174">You also need to specify the record type, the zone containing the record set, and the resource group containing the zone.</span></span>

<span data-ttu-id="e3414-175">Aşağıdaki örnek kaydı alır *www* bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e3414-175">The following example retrieves the record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="e3414-176">Liste kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="e3414-176">List record sets</span></span>

<span data-ttu-id="e3414-177">Kullanarak bir DNS bölgedeki tüm kayıtları listeleyebilirsiniz `azure network dns record-set list` komutu.</span><span class="sxs-lookup"><span data-stu-id="e3414-177">You can list all records in a DNS zone by using the `azure network dns record-set list` command.</span></span> <span data-ttu-id="e3414-178">Yardım için bkz. `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="e3414-179">Bu örnekte tüm kayıt kümeleri bölgesinde döndürür *contoso.com*, kaynak grubundaki *MyResourceGroup*, adı veya kayıt türü ne olursa olsun:</span><span class="sxs-lookup"><span data-stu-id="e3414-179">This example returns all record sets in the zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="e3414-180">Bu örnek, belirli kayıt türü (Bu durumda, 'Bir' kayıtları) eşleşen tüm kayıt kümelerinin döndürür:</span><span class="sxs-lookup"><span data-stu-id="e3414-180">This example returns all record sets that match the given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-to-an-existing-record-set"></a><span data-ttu-id="e3414-181">Bir kaydı var olan bir kayıt kümesine ekleme</span><span class="sxs-lookup"><span data-stu-id="e3414-181">Add a record to an existing record set</span></span>

<span data-ttu-id="e3414-182">Kullanabileceğiniz `azure network dns record-set add-record` hem yeni bir kayıt kümesinde bir kayıt oluşturmak veya var olan bir kayıt eklemek için kayıt kümesi.</span><span class="sxs-lookup"><span data-stu-id="e3414-182">You can use `azure network dns record-set add-record` both to create a record in a new record set, or to add a record to an existing record set.</span></span>

<span data-ttu-id="e3414-183">Daha fazla bilgi için bkz: [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.</span><span class="sxs-lookup"><span data-stu-id="e3414-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="e3414-184">Varolan bir kayıt kümesinden bir kaydı kaldırma.</span><span class="sxs-lookup"><span data-stu-id="e3414-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="e3414-185">Bir DNS kaydı varolan bir kayıt kümesinden kaldırmak için kullanın `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="e3414-185">To remove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="e3414-186">Yardım için bkz. `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="e3414-187">Bu komut, kayıt kümesindeki bir DNS kaydı siler.</span><span class="sxs-lookup"><span data-stu-id="e3414-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="e3414-188">Bir kayıt kümesindeki son kaydı silinirse, kendisini ayarlamak kaydıdır **değil** silindi.</span><span class="sxs-lookup"><span data-stu-id="e3414-188">If the last record in a record set is deleted, the record set itself is **not** deleted.</span></span> <span data-ttu-id="e3414-189">Bunun yerine, boş bir kayıt kümesi bırakılır.</span><span class="sxs-lookup"><span data-stu-id="e3414-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="e3414-190">Bunun yerine ayarlayın kaydını silmek için bkz: [bir kayıt kümesini Sil](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="e3414-190">To delete the record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="e3414-191">Silinecek kaydı belirtmeniz gerekir ve bölge, kullanarak bir kayıt oluştururken, aynı parametreleri kullanarak silinmesi `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="e3414-191">You need to specify the record to be deleted and the zone it should be deleted from, using the same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="e3414-192">Bu parametreler açıklanmaktadır [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.</span><span class="sxs-lookup"><span data-stu-id="e3414-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="e3414-193">Bu komut onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="e3414-193">This command prompts for confirmation.</span></span> <span data-ttu-id="e3414-194">Bu istemi kullanılarak gizlenebilir `--quiet` geçiş (kısa form `-q`).</span><span class="sxs-lookup"><span data-stu-id="e3414-194">This prompt can be suppressed using the `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="e3414-195">Aşağıdaki örnek kaydındaki ' 1.2.3.4 adlandırılmış kümesi' değeriyle A kaydını siler *www* bölgesinde *contoso.com*, kaynak grubundaki *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="e3414-195">The following example deletes the A record with value '1.2.3.4' from the record set named *www* in the zone *contoso.com*, in the resource group *MyResourceGroup*.</span></span> <span data-ttu-id="e3414-196">Onay istemi engellenir.</span><span class="sxs-lookup"><span data-stu-id="e3414-196">The confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="e3414-197">Varolan bir kayıt kümesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="e3414-197">Modify an existing record set</span></span>

<span data-ttu-id="e3414-198">Her bir kayıt kümesi içeren bir [yaşam süresi (TTL)](dns-zones-records.md#time-to-live), [meta veri](dns-zones-records.md#tags-and-metadata)ve DNS kayıtlarını.</span><span class="sxs-lookup"><span data-stu-id="e3414-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="e3414-199">Aşağıdaki bölümlerde, bu özelliklerin her biri değiştirmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e3414-199">The following sections explain how to modify each of these properties.</span></span>

### <a name="to-modify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="e3414-200">Bir A, AAAA, MX, NS, PTR, SRV ve TXT kaydı değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="e3414-200">To modify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="e3414-201">Var olan bir tür A, AAAA, MX, NS, PTR, SRV ve TXT kaydını değiştirmek için önce yeni bir kayıt ekleyin ve varolan kaydını silin.</span><span class="sxs-lookup"><span data-stu-id="e3414-201">To modify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete the existing record.</span></span> <span data-ttu-id="e3414-202">Bu makalenin önceki bölümlerinde silin ve kayıt ekleme konusunda ayrıntılı yönergeler için bkz.</span><span class="sxs-lookup"><span data-stu-id="e3414-202">For detailed instructions on how to delete and add records, see the earlier sections of this article.</span></span>

<span data-ttu-id="e3414-203">Aşağıdaki örnek IP adresine 5.6.7.8 1.2.3.4 IP adresinden bir 'Bir' kaydını değiştirerek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e3414-203">The following example shows how to modify an 'A' record, from IP address 1.2.3.4 to IP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="to-modify-a-cname-record"></a><span data-ttu-id="e3414-204">Bir CNAME kaydı değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="e3414-204">To modify a CNAME record</span></span>

<span data-ttu-id="e3414-205">Bir CNAME kaydı değiştirmek için `azure network dns record-set add-record` yeni kayıt değeri eklemek için.</span><span class="sxs-lookup"><span data-stu-id="e3414-205">To modify a CNAME record, use `azure network dns record-set add-record` to add the new record value.</span></span> <span data-ttu-id="e3414-206">Diğer kayıt türlerinin aksine, bir CNAME kayıt kümesi yalnızca tek bir kaydını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e3414-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="e3414-207">Bu nedenle, varolan bir bölüm kayıttır *yerini* zaman yeni kayıttaki eklenir ve ayrı olarak silinmesi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e3414-207">Therefore, the existing record is *replaced* when the new record is added, and does not need to be deleted separately.</span></span>  <span data-ttu-id="e3414-208">Bu değişikliği kabul istenir.</span><span class="sxs-lookup"><span data-stu-id="e3414-208">You will be prompted to accept this replacement.</span></span>

<span data-ttu-id="e3414-209">CNAME kayıt kümesi örnek değiştirir *www* bölgesinde *contoso.com*, kaynak grubundaki *MyResourceGroup*, kendi varolan yerine 'www.fabrikam.net' işaret etmek için değer:</span><span class="sxs-lookup"><span data-stu-id="e3414-209">The example modifies the CNAME record set *www* in the zone *contoso.com*, in resource group *MyResourceGroup*, to point to 'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="to-modify-an-soa-record"></a><span data-ttu-id="e3414-210">Bir SOA kaydına değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="e3414-210">To modify an SOA record</span></span>

<span data-ttu-id="e3414-211">Kullanım `azure network dns record-set set-soa-record` belirli bir DNS bölgesi için SOA değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="e3414-211">Use `azure network dns record-set set-soa-record` to modify the SOA for a given DNS zone.</span></span> <span data-ttu-id="e3414-212">Yardım için bkz. `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="e3414-213">Aşağıdaki örnekte, bölgenin SOA kaydına 'e-posta' özelliğini ayarlamak gösterilmiştir *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e3414-213">The following example shows how to set the 'email' property of the SOA record for the zone *contoso.com* in the resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="to-modify-ns-records-at-the-zone-apex"></a><span data-ttu-id="e3414-214">Bölge tepesinde NS kayıtları değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="e3414-214">To modify NS records at the zone apex</span></span>

<span data-ttu-id="e3414-215">NS kayıt bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e3414-215">The NS record set at the zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="e3414-216">Bölgeye atanan Azure DNS ad sunucularının adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="e3414-216">It contains the names of the Azure DNS name servers assigned to the zone.</span></span>

<span data-ttu-id="e3414-217">Birden fazla DNS sağlayıcınız ile birlikte barındırma etki alanlarını destekleyecek şekilde bu NS kaydının sunucularına ayarlayın ek ad ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3414-217">You can add additional name servers to this NS record set, to support co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="e3414-218">Bu kayıt kümesi için meta verileri ve TTL de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e3414-218">You can also modify the TTL and metadata for this record set.</span></span> <span data-ttu-id="e3414-219">Ancak, kaldırmak veya önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e3414-219">However, you cannot remove or modify the pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="e3414-220">Bu bölge tepesinde yalnızca NS kayıt kümesi için geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e3414-220">Note that this applies only to the NS record set at the zone apex.</span></span> <span data-ttu-id="e3414-221">(Alt bölgelere temsilci seçmek için kullanıldığı şekilde), bu bölgedeki diğer NS kayıt kümelerini kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e3414-221">Other NS record sets in your zone (as used to delegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="e3414-222">Aşağıdaki örnekte, bölgenin tepesinde ayarlamak NS kaydı bir ek ad sunucusu eklemek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e3414-222">The following example shows how to add an additional name server to the NS record set at the zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="to-modify-the-ttl-of-an-existing-record-set"></a><span data-ttu-id="e3414-223">Varolan bir kayıt kümesi TTL değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="e3414-223">To modify the TTL of an existing record set</span></span>

<span data-ttu-id="e3414-224">Varolan bir kayıt kümesi TTL değiştirmek için `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="e3414-224">To modify the TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="e3414-225">Yardım için bkz. `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="e3414-226">Aşağıdaki örnek, bir kayıt kümesi TTL, bu durumda 60 saniye olarak değiştirmek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="e3414-226">The following example shows how to modify a record set TTL, in this case to 60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="to-modify-the-metadata-of-an-existing-record-set"></a><span data-ttu-id="e3414-227">Varolan bir kayıt kümesini meta verilerini değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="e3414-227">To modify the metadata of an existing record set</span></span>

<span data-ttu-id="e3414-228">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) uygulamaya özgü verileri anahtar-değer çiftleri olarak her bir kayıt kümesi ile ilişkilendirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e3414-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used to associate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="e3414-229">Varolan bir kayıt kümesini meta verilerini değiştirmek için `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="e3414-229">To modify the metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="e3414-230">Yardım için bkz. `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="e3414-231">Aşağıdaki örnek, bir kayıt kümesi iki meta veri girişi ile değiştirmek gösterilmiştir "Bölüm Finans =" ve "ortam üretim =", kullanarak `--metadata` parametre (kısa form `-m`).</span><span class="sxs-lookup"><span data-stu-id="e3414-231">The following example shows how to modify a record set with two metadata entries, "dept=finance" and "environment=production", by using the `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="e3414-232">Var olan herhangi bir meta veri olduğuna dikkat edin *yerini* verilen değerlere göre.</span><span class="sxs-lookup"><span data-stu-id="e3414-232">Note that any existing metadata is *replaced* by the values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="e3414-233">Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="e3414-233">Delete a record set</span></span>

<span data-ttu-id="e3414-234">Kayıt kümeleri kullanarak silinebilir `azure network dns record-set delete` komutu.</span><span class="sxs-lookup"><span data-stu-id="e3414-234">Record sets can be deleted by using the `azure network dns record-set delete` command.</span></span> <span data-ttu-id="e3414-235">Yardım için bkz. `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="e3414-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="e3414-236">Kayıt kümesi siliniyor, kayıt kümesindeki tüm kayıtları siler.</span><span class="sxs-lookup"><span data-stu-id="e3414-236">Deleting a record set also deletes all records within the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="e3414-237">SOA silemezsiniz ve NS kayıt kümeleri bölgenin tepesinde (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="e3414-237">You cannot delete the SOA and NS record sets at the zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="e3414-238">Bu, zaman dilimi oluşturulduğunu ve bölge silindiğinde otomatik olarak silinir otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e3414-238">These are created automatically when the zone was created, and are deleted automatically when the zone is deleted.</span></span>

<span data-ttu-id="e3414-239">Aşağıdaki örnek kayıt adlandırılmış kümesi siler *www* bölgesinden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="e3414-239">The following example deletes the record set named *www* of type A from the zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="e3414-240">Silme işlemi onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="e3414-240">You are prompted to confirm the delete operation.</span></span> <span data-ttu-id="e3414-241">Bu uyarıyı gizlemek için kullanın `--quiet` geçiş (kısa form `-q`).</span><span class="sxs-lookup"><span data-stu-id="e3414-241">To suppress this prompt, use the `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3414-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e3414-242">Next steps</span></span>

<span data-ttu-id="e3414-243">Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="e3414-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="e3414-244">Bilgi nasıl [bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.</span><span class="sxs-lookup"><span data-stu-id="e3414-244">Learn how to [protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
