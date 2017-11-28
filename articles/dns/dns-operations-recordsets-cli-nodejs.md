---
title: "Azure DNS kullanarak aaaManage DNS kayıtları hello Azure CLI 1.0 | Microsoft Docs"
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
ms.openlocfilehash: 1f01450b0839f712cb1d96be318766bac581fea1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-in-azure-dns-using-hello-azure-cli-10"></a><span data-ttu-id="9a49d-104">Hello Azure CLI 1.0 kullanarak Azure DNS'de DNS kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="9a49d-104">Manage DNS records in Azure DNS using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a49d-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9a49d-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="9a49d-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9a49d-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="9a49d-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9a49d-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="9a49d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a49d-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="9a49d-109">Bu makalede nasıl toomanage DNS kayıtları kullanarak DNS bölgenizi için platformlar arası Azure komut satırı Windows, Mac ve Linux için kullanılabilir olan arabirimi (CLI) hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI), which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="9a49d-110">DNS kayıtlarınızı kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-recordsets.md) veya hello [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9a49d-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9a49d-111">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="9a49d-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="9a49d-112">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="9a49d-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="9a49d-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.</span><span class="sxs-lookup"><span data-stu-id="9a49d-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="9a49d-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.</span><span class="sxs-lookup"><span data-stu-id="9a49d-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="9a49d-115">Bu makaledeki Hello örnekler, zaten sahip olduğunuzu varsayar [Merhaba, oturum açan Azure CLI 1.0 yüklü ve bir DNS bölgesi oluşturulan](dns-operations-dnszones-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9a49d-115">hello examples in this article assume you have already [installed hello Azure CLI 1.0, signed in, and created a DNS zone](dns-operations-dnszones-cli-nodejs.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="9a49d-116">Giriş</span><span class="sxs-lookup"><span data-stu-id="9a49d-116">Introduction</span></span>

<span data-ttu-id="9a49d-117">Azure DNS'de DNS kayıtlarını oluşturmadan önce ilk toounderstand ihtiyacınız nasıl Azure DNS DNS kayıtlarını DNS kayıt kümeleri halinde düzenler.</span><span class="sxs-lookup"><span data-stu-id="9a49d-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="9a49d-118">Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="9a49d-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="9a49d-119">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a49d-119">Create a DNS record</span></span>

<span data-ttu-id="9a49d-120">toocreate bir DNS kaydı kullanmak hello `azure network dns record-set add-record` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a49d-120">toocreate a DNS record, use hello `azure network dns record-set add-record` command.</span></span> <span data-ttu-id="9a49d-121">Yardım için bkz. `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-121">For help, see `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="9a49d-122">Bir kayıt oluştururken, toospecify hello kaynak grubu adı, bölge adı gerekiyor, kayıt adı, hello kayıt türünü ve hello oluşturulmakta hello kaydın ayrıntılarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a49d-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="9a49d-123">Merhaba verilen kayıt kümesi adı olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="9a49d-124">Merhaba kayıt kümesi zaten mevcut değilse, bu komutu, sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9a49d-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="9a49d-125">Merhaba kayıt kümesi zaten varsa, bu komutu olan hello kayıt toohello varolan bir kayıt kümesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="9a49d-125">If hello record set already exists, this command adda hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="9a49d-126">Yeni bir kayıt kümesi oluşturuluyorsa yaşam süresi (TTL) olarak varsayılan 3600 değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9a49d-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="9a49d-127">Yönergeler için nasıl toouse farklı TTLs bkz [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="9a49d-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="9a49d-128">Merhaba aşağıdaki örnekte oluşturur adlı bir A kaydı *www* hello bölgesinde *contoso.com* hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9a49d-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="9a49d-129">Merhaba bir kayıttır hello IP adresini *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="9a49d-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

<span data-ttu-id="9a49d-130">toocreate hello hello bölge tepesinde bir kayıt (Bu durumda, "contoso.com"), hello kayıt adını kullanın "@", hello tırnak işaretleri dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="9a49d-130">toocreate a record in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" A -a 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="9a49d-131">DNS kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a49d-131">Create a DNS record set</span></span>

<span data-ttu-id="9a49d-132">Örnekleri yukarıda Hello hello DNS kayıt kayıt kümesinde varolan ya da eklenen tooan olduğundan veya hello kayıt kümesi oluşturuldu *örtük olarak*.</span><span class="sxs-lookup"><span data-stu-id="9a49d-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="9a49d-133">Merhaba kayıt kümesi de oluşturabilirsiniz *açıkça* önce ekleme tooit kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9a49d-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="9a49d-134">Azure DNS, DNS kayıtlarını oluşturmadan önce bir DNS adı bir yer tutucu tooreserve çalışabilmek için 'empty' kayıt kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="9a49d-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="9a49d-135">Boş kaydı kümeleri Azure DNS düzlemi denetlemek, ancak hello Azure DNS ad sunucuları üzerinde görünmeyen hello görünür.</span><span class="sxs-lookup"><span data-stu-id="9a49d-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="9a49d-136">Kayıt kümeleri hello kullanarak oluşturulur `azure network dns record-set create` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a49d-136">Record sets are created using hello `azure network dns record-set create` command.</span></span> <span data-ttu-id="9a49d-137">Yardım için bkz. `azure network dns record-set create -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-137">For help, see `azure network dns record-set create -h`.</span></span>

<span data-ttu-id="9a49d-138">Merhaba kayıt açıkça kümesi oluşturma verir hello gibi toospecify kayıt kümesi özellikleri [yaşam süresi (TTL)](dns-zones-records.md#time-to-live) ve meta verileri.</span><span class="sxs-lookup"><span data-stu-id="9a49d-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="9a49d-139">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="9a49d-140">Merhaba aşağıdaki örnekte oluşturur boş bir kayıt hello kullanarak 60 saniye TTL ile kümesi `--ttl` parametre (kısa form `-l`):</span><span class="sxs-lookup"><span data-stu-id="9a49d-140">hello following example creates an empty record set with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --ttl 60
```

<span data-ttu-id="9a49d-141">Merhaba aşağıdaki örnekte iki meta veri girişi ile ayarlanmış bir kayıt oluşturur "Bölüm Finans =" ve "ortam üretim =", hello kullanarak `--metadata` parametre (kısa form `-m`):</span><span class="sxs-lookup"><span data-stu-id="9a49d-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`):</span></span>

```azurecli
azure network dns record-set create MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

<span data-ttu-id="9a49d-142">Boş bir kayıt kümesi oluşturulduktan sonra kayıtları kullanılarak eklenebilir `azure network dns record-set add-record` açıklandığı gibi [bir DNS kaydı oluşturma](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="9a49d-142">Having created an empty record set, records can be added using `azure network dns record-set add-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="9a49d-143">Diğer türleri kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a49d-143">Create records of other types</span></span>

<span data-ttu-id="9a49d-144">Ayrıntılı olarak nasıl toocreate 'A' kaydeder, Azure DNS tarafından nasıl toocreate kayıt diğer kayıt türlerinin desteklenen örneklerde aşağıdaki hello görülen.</span><span class="sxs-lookup"><span data-stu-id="9a49d-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="9a49d-145">Merhaba parametreleri veri hello kayıt hello türüne bağlı olarak farklılık toospecify hello kaydı için kullanılmış.</span><span class="sxs-lookup"><span data-stu-id="9a49d-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="9a49d-146">Örneğin, için bir kayıt türü "A" Merhaba IPv4 adresi hello parametresiyle belirttiğiniz `-a <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `-a <IPv4 address>`.</span></span> <span data-ttu-id="9a49d-147">Her bir kayıt türü kullanılarak listelenebilir için parametreleri Hello `azure network dns record-set add-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-147">hello parameters for each record type can be listed using `azure network dns record-set add-record -h`.</span></span>

<span data-ttu-id="9a49d-148">Her durumda, gösteriyoruz nasıl toocreate tek bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="9a49d-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="9a49d-149">kayıt kümesi varolan eklenen toohello Hello kaydıdır veya bir kayıt kümesini örtük olarak oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="9a49d-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="9a49d-150">Kayıt kümeleri oluşturma ve kayıt tanımlama hakkında daha fazla bilgi için parametre açıkça, bakın [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="9a49d-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="9a49d-151">SOAs oluşturulduğundan bir örnek toocreate bir SOA kayıt kümesi sunuyoruz değil ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="9a49d-152">Ancak, [SOA değiştirilebilir, bir sonraki örnekte gösterildiği gibi hello](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="9a49d-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="9a49d-153">Bir AAAA kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="9a49d-153">Create an AAAA record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-aaaa AAAA --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="9a49d-154">Bir CNAME kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="9a49d-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="9a49d-155">Merhaba DNS standartlarında izin vermiyor CNAME kayıtları hello bir bölgenin tepesinde (`-Name "@"`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.</span><span class="sxs-lookup"><span data-stu-id="9a49d-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`-Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="9a49d-156">Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="9a49d-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
azure network dns record-set add-record  MyResourceGroup contoso.com  test-cname CNAME --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="9a49d-157">MX kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a49d-157">Create an MX record</span></span>

<span data-ttu-id="9a49d-158">Bu örnekte, hello kayıt kümesi adını kullanıyoruz "@" toocreate hello MX kaydı hello bölge tepesinde (Bu durumda, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="9a49d-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "@" MX --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="9a49d-159">Bir NS kayıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a49d-159">Create an NS record</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup  contoso.com  test-ns NS --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="9a49d-160">PTR kaydı oluştur</span><span class="sxs-lookup"><span data-stu-id="9a49d-160">Create a PTR record</span></span>

<span data-ttu-id="9a49d-161">Bu durumda, ' my-arpa-zone.com' hello IP aralığınızı temsil eden ARPA bölge temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9a49d-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="9a49d-162">Bu bölgede ayarlamak her PTR kaydı tooan IP adresi bu IP aralığı içinde karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="9a49d-163">Merhaba kaydı '10' hello IP adresinin bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9a49d-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup my-arpa-zone.com "10" PTR --ptrdname "myservice.contoso.com"
```

### <a name="create-an-srv-record"></a><span data-ttu-id="9a49d-164">Bir SRV kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="9a49d-164">Create an SRV record</span></span>

<span data-ttu-id="9a49d-165">Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), hello belirtin  *\_hizmet* ve  *\_Protokolü* hello kayıt kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="9a49d-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="9a49d-166">Hiçbir gerek tooinclude yok "@" hello kayıt kümesi adı bir SRV kaydı kümesi hello bölgenin tepesinde oluştururken.</span><span class="sxs-lookup"><span data-stu-id="9a49d-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com  "_sip._tls" SRV --priority 10 --weight 5 --port 8080 --target "sip.contoso.com"
```

### <a name="create-a-txt-record"></a><span data-ttu-id="9a49d-167">TXT kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a49d-167">Create a TXT record</span></span>

<span data-ttu-id="9a49d-168">Merhaba aşağıdaki örnekte nasıl toocreate bir TXT kaydı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="9a49d-169">TXT kayıtlarının desteklenen hello maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="9a49d-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com test-txt TXT --text "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="9a49d-170">Bir kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="9a49d-170">Get a record set</span></span>

<span data-ttu-id="9a49d-171">tooretrieve varolan bir kayıt kümesini kullanma `azure network dns record-set show`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-171">tooretrieve an existing record set, use `azure network dns record-set show`.</span></span> <span data-ttu-id="9a49d-172">Yardım için bkz. `azure network dns record-set show -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-172">For help, see `azure network dns record-set show -h`.</span></span>

<span data-ttu-id="9a49d-173">Bir kayıt veya kayıt kümesi oluştururken, hello kayıt kümesinin adı verilen olarak olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="9a49d-174">Toospecify hello kayıt türü de gerekir, hello kayıt içeren hello bölge ayarlamak ve hello bölge içeren kaynak grubunu hello.</span><span class="sxs-lookup"><span data-stu-id="9a49d-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="9a49d-175">Merhaba aşağıdaki örnek hello kaydı alır *www* bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9a49d-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set show MyResourceGroup contoso.com www A
```

## <a name="list-record-sets"></a><span data-ttu-id="9a49d-176">Liste kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="9a49d-176">List record sets</span></span>

<span data-ttu-id="9a49d-177">Hello kullanarak bir DNS bölgedeki tüm kayıtları listeleyebilirsiniz `azure network dns record-set list` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a49d-177">You can list all records in a DNS zone by using hello `azure network dns record-set list` command.</span></span> <span data-ttu-id="9a49d-178">Yardım için bkz. `azure network dns record-set list -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-178">For help, see `azure network dns record-set list -h`.</span></span>

<span data-ttu-id="9a49d-179">Bu örnekte tüm kayıt kümeleri hello bölgesinde döndürür *contoso.com*, kaynak grubundaki *MyResourceGroup*, adı veya kayıt türü ne olursa olsun:</span><span class="sxs-lookup"><span data-stu-id="9a49d-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com
```

<span data-ttu-id="9a49d-180">Bu örnek kayıt türü (Bu durumda, 'Bir' kayıtları) verilen hello eşleşen tüm kayıt kümelerinin döndürür:</span><span class="sxs-lookup"><span data-stu-id="9a49d-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
azure network dns record-set list MyResourceGroup contoso.com --type A
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="9a49d-181">Kayıt kümesi varolan bir kayıt tooan Ekle</span><span class="sxs-lookup"><span data-stu-id="9a49d-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="9a49d-182">Kullanabileceğiniz `azure network dns record-set add-record` hem yeni bir kayıt kaydında toocreate ayarlayın veya kayıt tooan varolan bir kaydı tooadd ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9a49d-182">You can use `azure network dns record-set add-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="9a49d-183">Daha fazla bilgi için bkz: [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.</span><span class="sxs-lookup"><span data-stu-id="9a49d-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="9a49d-184">Varolan bir kayıt kümesinden bir kaydı kaldırma.</span><span class="sxs-lookup"><span data-stu-id="9a49d-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="9a49d-185">tooremove bir DNS kaydı varolan kayıt kümesinden, kullanım `azure network dns record-set delete-record`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-185">tooremove a DNS record from an existing record set, use `azure network dns record-set delete-record`.</span></span> <span data-ttu-id="9a49d-186">Yardım için bkz. `azure network dns record-set delete-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-186">For help, see `azure network dns record-set delete-record -h`.</span></span>

<span data-ttu-id="9a49d-187">Bu komut, kayıt kümesindeki bir DNS kaydı siler.</span><span class="sxs-lookup"><span data-stu-id="9a49d-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="9a49d-188">Bir kayıt kümesindeki Hello son kaydı silinirse, kendisini ayarlamak hello kaydıdır **değil** silindi.</span><span class="sxs-lookup"><span data-stu-id="9a49d-188">If hello last record in a record set is deleted, hello record set itself is **not** deleted.</span></span> <span data-ttu-id="9a49d-189">Bunun yerine, boş bir kayıt kümesi bırakılır.</span><span class="sxs-lookup"><span data-stu-id="9a49d-189">Instead, an empty record set is left.</span></span> <span data-ttu-id="9a49d-190">Bunun yerine, ayarlamak toodelete hello kaydını görmek [bir kayıt kümesini Sil](#delete-a-record-set).</span><span class="sxs-lookup"><span data-stu-id="9a49d-190">toodelete hello record set instead, see [Delete a record set](#delete-a-record-set).</span></span>

<span data-ttu-id="9a49d-191">Toospecify ihtiyacınız hello kayıt toobe silinmiş ve onu silinmesi, kullanarak hello bölge kayıt kullanarak oluştururken, aynı parametreleri hello `azure network dns record-set add-record`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-191">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `azure network dns record-set add-record`.</span></span> <span data-ttu-id="9a49d-192">Bu parametreler açıklanmaktadır [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.</span><span class="sxs-lookup"><span data-stu-id="9a49d-192">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="9a49d-193">Bu komut onaylamanızı ister.</span><span class="sxs-lookup"><span data-stu-id="9a49d-193">This command prompts for confirmation.</span></span> <span data-ttu-id="9a49d-194">Bu istemi hello kullanılarak gizlenebilir `--quiet` geçiş (kısa form `-q`).</span><span class="sxs-lookup"><span data-stu-id="9a49d-194">This prompt can be suppressed using hello `--quiet` switch (short form `-q`).</span></span>

<span data-ttu-id="9a49d-195">Aşağıdaki örnek siler hello hello hello kaydından ' 1.2.3.4 adlandırılmış kümesi' içeren bir kaydı *www* hello bölgesinde *contoso.com*, hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="9a49d-195">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="9a49d-196">Merhaba onay istemi engellenir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-196">hello confirmation prompt is suppressed.</span></span>

```azurecli
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4 --quiet
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="9a49d-197">Varolan bir kayıt kümesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="9a49d-197">Modify an existing record set</span></span>

<span data-ttu-id="9a49d-198">Her bir kayıt kümesi içeren bir [yaşam süresi (TTL)](dns-zones-records.md#time-to-live), [meta veri](dns-zones-records.md#tags-and-metadata)ve DNS kayıtlarını.</span><span class="sxs-lookup"><span data-stu-id="9a49d-198">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="9a49d-199">Merhaba aşağıdaki bölümlerde açıklanmıştır nasıl toomodify her bu özelliklerin.</span><span class="sxs-lookup"><span data-stu-id="9a49d-199">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="9a49d-200">toomodify bir A, AAAA, MX, NS, PTR, SRV ve TXT kaydı</span><span class="sxs-lookup"><span data-stu-id="9a49d-200">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="9a49d-201">var olan bir tür A, AAAA, MX, NS, PTR, SRV ve TXT kaydını toomodify, yeni bir kayıt ve ardından silme hello varolan kaydı ilk eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-201">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="9a49d-202">Ayrıntılı yönergeler için toodelete ve kayıtları eklemek için bkz: Merhaba bu makalenin önceki bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="9a49d-202">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="9a49d-203">Aşağıdaki örneğine hello nasıl toomodify bir 'A' kaydından IP adresi 1.2.3.4 tooIP adres 5.6.7.8 gösterir:</span><span class="sxs-lookup"><span data-stu-id="9a49d-203">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www A -a 5.6.7.8
azure network dns record-set delete-record MyResourceGroup contoso.com www A -a 1.2.3.4
```

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="9a49d-204">toomodify bir CNAME kaydı</span><span class="sxs-lookup"><span data-stu-id="9a49d-204">toomodify a CNAME record</span></span>

<span data-ttu-id="9a49d-205">toomodify bir CNAME kaydı kullanmak `azure network dns record-set add-record` tooadd hello yeni bir kayıt değeri.</span><span class="sxs-lookup"><span data-stu-id="9a49d-205">toomodify a CNAME record, use `azure network dns record-set add-record` tooadd hello new record value.</span></span> <span data-ttu-id="9a49d-206">Diğer kayıt türlerinin aksine, bir CNAME kayıt kümesi yalnızca tek bir kaydını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-206">Unlike other record types, a CNAME record set can only contain a single record.</span></span> <span data-ttu-id="9a49d-207">Bu nedenle, hello varolan kaydıdır *yerini* zaman hello yeni kayıt eklenir ve ayrı ayrı silinmiş toobe gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-207">Therefore, hello existing record is *replaced* when hello new record is added, and does not need toobe deleted separately.</span></span>  <span data-ttu-id="9a49d-208">Bu değişiklik istendiğinde tooaccept olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a49d-208">You will be prompted tooaccept this replacement.</span></span>

<span data-ttu-id="9a49d-209">Merhaba örnek değiştirir hello CNAME kayıt kümesi *www* hello bölgesinde *contoso.com*, kaynak grubundaki *MyResourceGroup*, toopoint çok yerine ' www.fabrikam.net' kendi Mevcut değer:</span><span class="sxs-lookup"><span data-stu-id="9a49d-209">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com www CNAME --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="9a49d-210">toomodify bir SOA kaydı</span><span class="sxs-lookup"><span data-stu-id="9a49d-210">toomodify an SOA record</span></span>

<span data-ttu-id="9a49d-211">Kullanım `azure network dns record-set set-soa-record` belirli bir DNS bölgesi için toomodify hello SOA.</span><span class="sxs-lookup"><span data-stu-id="9a49d-211">Use `azure network dns record-set set-soa-record` toomodify hello SOA for a given DNS zone.</span></span> <span data-ttu-id="9a49d-212">Yardım için bkz. `azure network dns record-set set-soa-record -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-212">For help, see `azure network dns record-set set-soa-record -h`.</span></span>

<span data-ttu-id="9a49d-213">Merhaba aşağıdaki örnekte nasıl hello SOA tooset hello 'e-posta' özelliği kayıt hello bölgenin gösterir *contoso.com* hello kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9a49d-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set set-soa-record rg1 contoso.com --email admin.contoso.com
```


### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="9a49d-214">Merhaba bölge tepesinde toomodify NS kayıtları</span><span class="sxs-lookup"><span data-stu-id="9a49d-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="9a49d-215">Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9a49d-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="9a49d-216">Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="9a49d-217">Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a49d-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="9a49d-218">Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a49d-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="9a49d-219">Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9a49d-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="9a49d-220">Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9a49d-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="9a49d-221">Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="9a49d-222">Aşağıdaki örneğine hello tooadd bir ek ad sunucusu toohello NS kaydı hello bölgenin tepesinde nasıl ayarlanacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="9a49d-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup contoso.com "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="9a49d-223">toomodify hello varolan bir kaydı TTL Ayarla</span><span class="sxs-lookup"><span data-stu-id="9a49d-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="9a49d-224">Varolan bir kaydı TTL toomodify hello ayarlayabilir, kullanabilir `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-224">toomodify hello TTL of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="9a49d-225">Yardım için bkz. `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-225">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="9a49d-226">Aşağıdaki örnek hello nasıl toomodify kayıt kümesi TTL, bu durumda too60 saniye gösterir:</span><span class="sxs-lookup"><span data-stu-id="9a49d-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --ttl 60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="9a49d-227">Varolan bir kayıt kümesini toomodify hello meta verileri</span><span class="sxs-lookup"><span data-stu-id="9a49d-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="9a49d-228">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="9a49d-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="9a49d-229">Varolan bir kaydı toomodify hello meta verileri ayarlama, kullanın `azure network dns record-set set`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-229">toomodify hello metadata of an existing record set, use `azure network dns record-set set`.</span></span> <span data-ttu-id="9a49d-230">Yardım için bkz. `azure network dns record-set set -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-230">For help, see `azure network dns record-set set -h`.</span></span>

<span data-ttu-id="9a49d-231">Merhaba aşağıdaki örnek toomodify kayıt iki meta veri girişi ile nasıl ayarlanacağını gösterir "Bölüm Finans =" ve "ortam üretim =", hello kullanarak `--metadata` parametre (kısa form `-m`).</span><span class="sxs-lookup"><span data-stu-id="9a49d-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter (short form `-m`).</span></span> <span data-ttu-id="9a49d-232">Var olan herhangi bir meta veri olduğuna dikkat edin *yerini* verilen hello değerlere göre.</span><span class="sxs-lookup"><span data-stu-id="9a49d-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
azure network dns record-set set MyResourceGroup contoso.com www A --metadata "dept=finance;environment=production"
```

## <a name="delete-a-record-set"></a><span data-ttu-id="9a49d-233">Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="9a49d-233">Delete a record set</span></span>

<span data-ttu-id="9a49d-234">Kayıt kümeleri hello kullanarak silinebilir `azure network dns record-set delete` komutu.</span><span class="sxs-lookup"><span data-stu-id="9a49d-234">Record sets can be deleted by using hello `azure network dns record-set delete` command.</span></span> <span data-ttu-id="9a49d-235">Yardım için bkz. `azure network dns record-set delete -h`.</span><span class="sxs-lookup"><span data-stu-id="9a49d-235">For help, see `azure network dns record-set delete -h`.</span></span> <span data-ttu-id="9a49d-236">Kayıt kümesi siliniyor hello kayıt kümesi içindeki tüm kayıtları siler.</span><span class="sxs-lookup"><span data-stu-id="9a49d-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="9a49d-237">Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (`-Name "@"`).</span><span class="sxs-lookup"><span data-stu-id="9a49d-237">You cannot delete hello SOA and NS record sets at hello zone apex (`-Name "@"`).</span></span>  <span data-ttu-id="9a49d-238">Bu, ne zaman hello bölge oluşturuldu ve hello bölge silindiğinde otomatik olarak silinir otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9a49d-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="9a49d-239">Merhaba aşağıdaki örnek siler hello kayıt adlandırılmış kümesi *www* hello bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="9a49d-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
azure network dns record-set delete MyResourceGroup contoso.com www A
```

<span data-ttu-id="9a49d-240">İstendiğinde tooconfirm hello silme işlemi var.</span><span class="sxs-lookup"><span data-stu-id="9a49d-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="9a49d-241">Bu komut istemi toosuppress hello kullanmak `--quiet` geçiş (kısa form `-q`).</span><span class="sxs-lookup"><span data-stu-id="9a49d-241">toosuppress this prompt, use hello `--quiet` switch (short form `-q`).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a49d-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a49d-242">Next steps</span></span>

<span data-ttu-id="9a49d-243">Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="9a49d-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="9a49d-244">Nasıl çok öğrenin[bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.</span><span class="sxs-lookup"><span data-stu-id="9a49d-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
