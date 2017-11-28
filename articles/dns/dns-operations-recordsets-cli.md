---
title: "Azure DNS kullanarak aaaManage DNS kayıtları hello Azure CLI 2.0 | Microsoft Docs"
description: "DNS kayıt kümelerini ve Azure DNS kayıtlarını Azure DNS'nin etki alanınızda barındırdığında yönetme. Kayıt kümelerini ve kayıtları işlemleri için tüm CLI 2.0 komutları."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 5356a3a5-8dec-44ac-9709-0c2b707f6cb5
ms.service: dns
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: jonatul
ms.openlocfilehash: 9d6f8e74ebad55ccd2381fd84a830d2c7bbb1f30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-dns-records-and-recordsets-in-azure-dns-using-hello-azure-cli-20"></a><span data-ttu-id="3eac7-104">DNS kayıtlarını ve kayıt kümeleri hello Azure CLI 2.0 kullanarak Azure DNS'de yönetme</span><span class="sxs-lookup"><span data-stu-id="3eac7-104">Manage DNS records and recordsets in Azure DNS using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3eac7-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3eac7-105">Azure Portal</span></span>](dns-operations-recordsets-portal.md)
> * [<span data-ttu-id="3eac7-106">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3eac7-106">Azure CLI 1.0</span></span>](dns-operations-recordsets-cli-nodejs.md)
> * [<span data-ttu-id="3eac7-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3eac7-107">Azure CLI 2.0</span></span>](dns-operations-recordsets-cli.md)
> * [<span data-ttu-id="3eac7-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3eac7-108">PowerShell</span></span>](dns-operations-recordsets.md)

<span data-ttu-id="3eac7-109">Bu makalede nasıl toomanage DNS kayıtları kullanarak DNS bölgenizi için platformlar arası Azure komut satırı arabirimi (Windows, Mac ve Linux için kullanılabilir olan CLI) 2.0 hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-109">This article shows you how toomanage DNS records for your DNS zone by using hello cross-platform Azure command-line interface (CLI) 2.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="3eac7-110">DNS kayıtlarınızı kullanarak da yönetebilirsiniz [Azure PowerShell](dns-operations-recordsets.md) veya hello [Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3eac7-110">You can also manage your DNS records using [Azure PowerShell](dns-operations-recordsets.md) or hello [Azure portal](dns-operations-recordsets-portal.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="3eac7-111">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="3eac7-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="3eac7-112">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="3eac7-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="3eac7-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) -bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için.</span><span class="sxs-lookup"><span data-stu-id="3eac7-113">[Azure CLI 1.0](dns-operations-recordsets-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="3eac7-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için.</span><span class="sxs-lookup"><span data-stu-id="3eac7-114">[Azure CLI 2.0](dns-operations-recordsets-cli.md) - our next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="3eac7-115">Bu makaledeki Hello örnekler, zaten sahip olduğunuzu varsayar [Merhaba, oturum açan Azure CLI 2.0 yüklü ve bir DNS bölgesi oluşturulan](dns-operations-dnszones-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3eac7-115">hello examples in this article assume you have already [installed hello Azure CLI 2.0, signed in, and created a DNS zone](dns-operations-dnszones-cli.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="3eac7-116">Giriş</span><span class="sxs-lookup"><span data-stu-id="3eac7-116">Introduction</span></span>

<span data-ttu-id="3eac7-117">Azure DNS'de DNS kayıtlarını oluşturmadan önce ilk toounderstand ihtiyacınız nasıl Azure DNS DNS kayıtlarını DNS kayıt kümeleri halinde düzenler.</span><span class="sxs-lookup"><span data-stu-id="3eac7-117">Before creating DNS records in Azure DNS, you first need toounderstand how Azure DNS organizes DNS records into DNS record sets.</span></span>

[!INCLUDE [dns-about-records-include](../../includes/dns-about-records-include.md)]

<span data-ttu-id="3eac7-118">Azure DNS’deki DNS kayıtları hakkında daha fazla bilgi için bkz. [DNS bölgeleri ve kayıtları](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="3eac7-118">For more information about DNS records in Azure DNS, see [DNS zones and records](dns-zones-records.md).</span></span>

## <a name="create-a-dns-record"></a><span data-ttu-id="3eac7-119">DNS kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3eac7-119">Create a DNS record</span></span>

<span data-ttu-id="3eac7-120">toocreate bir DNS kaydı kullanmak hello `az network dns record-set <record-type> set-record` komutu (burada `<record-type>` kaydına hello türünde yani</span><span class="sxs-lookup"><span data-stu-id="3eac7-120">toocreate a DNS record, use hello `az network dns record-set <record-type> set-record` command (where `<record-type>` is hello type of record, i.e</span></span> <span data-ttu-id="3eac7-121">bir, srv, txt, vs.) Yardım için bkz. `az network dns record-set --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-121">a, srv, txt, etc.) For help, see `az network dns record-set --help`.</span></span>

<span data-ttu-id="3eac7-122">Bir kayıt oluştururken, toospecify hello kaynak grubu adı, bölge adı gerekiyor, kayıt adı, hello kayıt türünü ve hello oluşturulmakta hello kaydın ayrıntılarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3eac7-122">When creating a record, you need toospecify hello resource group name, zone name, record set name, hello record type, and hello details of hello record being created.</span></span> <span data-ttu-id="3eac7-123">Merhaba verilen kayıt kümesi adı olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-123">hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span>

<span data-ttu-id="3eac7-124">Merhaba kayıt kümesi zaten mevcut değilse, bu komutu, sizin için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3eac7-124">If hello record set does not already exist, this command creates it for you.</span></span> <span data-ttu-id="3eac7-125">Hello kayıt kümesi zaten varsa, bu komut toohello varolan bir kayıt kümesini belirttiğiniz hello kayıt ekler.</span><span class="sxs-lookup"><span data-stu-id="3eac7-125">If hello record set already exists, this command adds hello record you specify toohello existing record set.</span></span>

<span data-ttu-id="3eac7-126">Yeni bir kayıt kümesi oluşturuluyorsa yaşam süresi (TTL) olarak varsayılan 3600 değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3eac7-126">If a new record set is created, a default time-to-live (TTL) of 3600 is used.</span></span> <span data-ttu-id="3eac7-127">Yönergeler için nasıl toouse farklı TTLs bkz [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="3eac7-127">For instructions on how toouse different TTLs, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="3eac7-128">Merhaba aşağıdaki örnekte oluşturur adlı bir A kaydı *www* hello bölgesinde *contoso.com* hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="3eac7-128">hello following example creates an A record called *www* in hello zone *contoso.com* in hello resource group *MyResourceGroup*.</span></span> <span data-ttu-id="3eac7-129">Merhaba bir kayıttır hello IP adresini *1.2.3.4*.</span><span class="sxs-lookup"><span data-stu-id="3eac7-129">hello IP address of hello A record is *1.2.3.4*.</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="3eac7-130">toocreate bir kayıt kümesi hello hello bölge tepesinde içinde (Bu durumda, "contoso.com"), hello kayıt adını kullanın "@", hello tırnak işaretleri dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="3eac7-130">toocreate a record set in hello apex of hello zone (in this case, "contoso.com"), use hello record name "@", including hello quotation marks:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --ipv4-address 1.2.3.4
```

## <a name="create-a-dns-record-set"></a><span data-ttu-id="3eac7-131">DNS kayıt kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3eac7-131">Create a DNS record set</span></span>

<span data-ttu-id="3eac7-132">Örnekleri yukarıda Hello hello DNS kayıt kayıt kümesinde varolan ya da eklenen tooan olduğundan veya hello kayıt kümesi oluşturuldu *örtük olarak*.</span><span class="sxs-lookup"><span data-stu-id="3eac7-132">In hello above examples, hello DNS record was either added tooan existing record set, or hello record set was created *implicitly*.</span></span> <span data-ttu-id="3eac7-133">Merhaba kayıt kümesi de oluşturabilirsiniz *açıkça* önce ekleme tooit kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3eac7-133">You can also create hello record set *explicitly* before adding records tooit.</span></span> <span data-ttu-id="3eac7-134">Azure DNS, DNS kayıtlarını oluşturmadan önce bir DNS adı bir yer tutucu tooreserve çalışabilmek için 'empty' kayıt kümelerini destekler.</span><span class="sxs-lookup"><span data-stu-id="3eac7-134">Azure DNS supports 'empty' record sets, which can act as a placeholder tooreserve a DNS name before creating DNS records.</span></span> <span data-ttu-id="3eac7-135">Boş kaydı kümeleri Azure DNS düzlemi denetlemek, ancak hello Azure DNS ad sunucuları üzerinde görünmeyen hello görünür.</span><span class="sxs-lookup"><span data-stu-id="3eac7-135">Empty record sets are visible in hello Azure DNS control plane, but do not appear on hello Azure DNS name servers.</span></span>

<span data-ttu-id="3eac7-136">Kayıt kümeleri hello kullanarak oluşturulur `az network dns record-set <record-type> create` komutu.</span><span class="sxs-lookup"><span data-stu-id="3eac7-136">Record sets are created using hello `az network dns record-set <record-type> create` command.</span></span> <span data-ttu-id="3eac7-137">Yardım için bkz. `az network dns record-set <record-type> create --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-137">For help, see `az network dns record-set <record-type> create --help`.</span></span>

<span data-ttu-id="3eac7-138">Merhaba kayıt açıkça kümesi oluşturma verir hello gibi toospecify kayıt kümesi özellikleri [yaşam süresi (TTL)](dns-zones-records.md#time-to-live) ve meta verileri.</span><span class="sxs-lookup"><span data-stu-id="3eac7-138">Creating hello record set explicitly allows you toospecify record set properties such as hello [Time-To-Live (TTL)](dns-zones-records.md#time-to-live) and metadata.</span></span> <span data-ttu-id="3eac7-139">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-139">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span>

<span data-ttu-id="3eac7-140">Merhaba aşağıdaki örnekte bir 60 saniye TTL Değerine sahip ' A' türündeki boş bir kayıt kümesi hello kullanarak oluşturur `--ttl` parametre (kısa form `-l`):</span><span class="sxs-lookup"><span data-stu-id="3eac7-140">hello following example creates an empty record set of type 'A' with a 60-second TTL, by using hello `--ttl` parameter (short form `-l`):</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --ttl 60
```

<span data-ttu-id="3eac7-141">Merhaba aşağıdaki örnekte iki meta veri girişi ile ayarlanmış bir kayıt oluşturur "Bölüm Finans =" ve "ortam üretim =", hello kullanarak `--metadata` parametre:</span><span class="sxs-lookup"><span data-stu-id="3eac7-141">hello following example creates a record set with two metadata entries, "dept=finance" and "environment=production", by using hello `--metadata` parameter :</span></span>

```azurecli
az network dns record-set a create --resource-group myresourcegroup --zone-name contoso.com --name www --metadata "dept=finance" "environment=production"
```

<span data-ttu-id="3eac7-142">Boş bir kayıt kümesi oluşturulduktan sonra kayıtları kullanılarak eklenebilir `azure network dns record-set <record-type> set-record` açıklandığı gibi [bir DNS kaydı oluşturma](#create-a-dns-record).</span><span class="sxs-lookup"><span data-stu-id="3eac7-142">Having created an empty record set, records can be added using `azure network dns record-set <record-type> set-record` as described in [Create a DNS record](#create-a-dns-record).</span></span>

## <a name="create-records-of-other-types"></a><span data-ttu-id="3eac7-143">Diğer türleri kayıtları oluşturma</span><span class="sxs-lookup"><span data-stu-id="3eac7-143">Create records of other types</span></span>

<span data-ttu-id="3eac7-144">Ayrıntılı olarak nasıl toocreate 'A' kaydeder, Azure DNS tarafından nasıl toocreate kayıt diğer kayıt türlerinin desteklenen örneklerde aşağıdaki hello görülen.</span><span class="sxs-lookup"><span data-stu-id="3eac7-144">Having seen in detail how toocreate 'A' records, hello following examples show how toocreate record of other record types supported by Azure DNS.</span></span>

<span data-ttu-id="3eac7-145">Merhaba parametreleri veri hello kayıt hello türüne bağlı olarak farklılık toospecify hello kaydı için kullanılmış.</span><span class="sxs-lookup"><span data-stu-id="3eac7-145">hello parameters used toospecify hello record data vary depending on hello type of hello record.</span></span> <span data-ttu-id="3eac7-146">Örneğin, için bir kayıt türü "A" Merhaba IPv4 adresi hello parametresiyle belirttiğiniz `--ipv4-address <IPv4 address>`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-146">For example, for a record of type "A", you specify hello IPv4 address with hello parameter `--ipv4-address <IPv4 address>`.</span></span> <span data-ttu-id="3eac7-147">Her bir kayıt türü kullanılarak listelenebilir için parametreleri Hello `az network dns record-set <record-type> set-record --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-147">hello parameters for each record type can be listed using `az network dns record-set <record-type> set-record --help`.</span></span>

<span data-ttu-id="3eac7-148">Her durumda, gösteriyoruz nasıl toocreate tek bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="3eac7-148">In each case, we show how toocreate a single record.</span></span> <span data-ttu-id="3eac7-149">kayıt kümesi varolan eklenen toohello Hello kaydıdır veya bir kayıt kümesini örtük olarak oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="3eac7-149">hello record is added toohello existing record set, or a record set created implicitly.</span></span> <span data-ttu-id="3eac7-150">Kayıt kümeleri oluşturma ve kayıt tanımlama hakkında daha fazla bilgi için parametre açıkça, bakın [DNS kayıt kümesi oluşturma](#create-a-dns-record-set).</span><span class="sxs-lookup"><span data-stu-id="3eac7-150">For more information on creating record sets and defining record set parameter explicitly, see [Create a DNS record set](#create-a-dns-record-set).</span></span>

<span data-ttu-id="3eac7-151">SOAs oluşturulduğundan bir örnek toocreate bir SOA kayıt kümesi sunuyoruz değil ve her DNS bölge ile silinmiş ve oluşturulamaz veya ayrı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-151">We do not give an example toocreate an SOA record set, since SOAs are created and deleted with each DNS zone and cannot be created or deleted separately.</span></span> <span data-ttu-id="3eac7-152">Ancak, [SOA değiştirilebilir, bir sonraki örnekte gösterildiği gibi hello](#to-modify-an-SOA-record).</span><span class="sxs-lookup"><span data-stu-id="3eac7-152">However, [hello SOA can be modified, as shown in a later example](#to-modify-an-SOA-record).</span></span>

### <a name="create-an-aaaa-record"></a><span data-ttu-id="3eac7-153">Bir AAAA kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="3eac7-153">Create an AAAA record</span></span>

```azurecli
az network dns record-set aaaa set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-aaaa --ipv6-address 2607:f8b0:4009:1803::1005
```

### <a name="create-a-cname-record"></a><span data-ttu-id="3eac7-154">Bir CNAME kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="3eac7-154">Create a CNAME record</span></span>

> [!NOTE]
> <span data-ttu-id="3eac7-155">Merhaba DNS standartlarında izin vermiyor CNAME kayıtları hello bir bölgenin tepesinde (`--Name "@"`), ya da birden çok kayıt içeren kayıt kümeleri izin yapın.</span><span class="sxs-lookup"><span data-stu-id="3eac7-155">hello DNS standards do not permit CNAME records at hello apex of a zone (`--Name "@"`), nor do they permit record sets containing more than one record.</span></span>
> 
> <span data-ttu-id="3eac7-156">Daha fazla bilgi için bkz: [CNAME kayıtları](dns-zones-records.md#cname-records).</span><span class="sxs-lookup"><span data-stu-id="3eac7-156">For more information, see [CNAME records](dns-zones-records.md#cname-records).</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.contoso.com
```

### <a name="create-an-mx-record"></a><span data-ttu-id="3eac7-157">MX kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3eac7-157">Create an MX record</span></span>

<span data-ttu-id="3eac7-158">Bu örnekte, hello kayıt kümesi adını kullanıyoruz "@" toocreate hello MX kaydı hello bölge tepesinde (Bu durumda, "contoso.com").</span><span class="sxs-lookup"><span data-stu-id="3eac7-158">In this example, we use hello record set name "@" toocreate hello MX record at hello zone apex (in this case, "contoso.com").</span></span>

```azurecli
az network dns record-set mx set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --exchange mail.contoso.com --preference 5
```

### <a name="create-an-ns-record"></a><span data-ttu-id="3eac7-159">Bir NS kayıt oluşturma</span><span class="sxs-lookup"><span data-stu-id="3eac7-159">Create an NS record</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-ns --nsdname ns1.contoso.com
```

### <a name="create-a-ptr-record"></a><span data-ttu-id="3eac7-160">PTR kaydı oluştur</span><span class="sxs-lookup"><span data-stu-id="3eac7-160">Create a PTR record</span></span>

<span data-ttu-id="3eac7-161">Bu durumda, ' my-arpa-zone.com' hello IP aralığınızı temsil eden ARPA bölge temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3eac7-161">In this case, 'my-arpa-zone.com' represents hello ARPA zone representing your IP range.</span></span> <span data-ttu-id="3eac7-162">Bu bölgede ayarlamak her PTR kaydı tooan IP adresi bu IP aralığı içinde karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-162">Each PTR record set in this zone corresponds tooan IP address within this IP range.</span></span>  <span data-ttu-id="3eac7-163">Merhaba kaydı '10' hello IP adresinin bu kayıt tarafından temsil edilen bu IP aralığı içinde son sekizlisi hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="3eac7-163">hello record name '10' is hello last octet of hello IP address within this IP range represented by this record.</span></span>

```azurecli
az network dns record-set ptr set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name my-arpa.zone.com --ptrdname myservice.contoso.com
```

### <a name="create-an-srv-record"></a><span data-ttu-id="3eac7-164">Bir SRV kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="3eac7-164">Create an SRV record</span></span>

<span data-ttu-id="3eac7-165">Oluştururken bir [SRV kayıt kümesi](dns-zones-records.md#srv-records), hello belirtin  *\_hizmet* ve  *\_Protokolü* hello kayıt kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="3eac7-165">When creating an [SRV record set](dns-zones-records.md#srv-records), specify hello *\_service* and *\_protocol* in hello record set name.</span></span> <span data-ttu-id="3eac7-166">Hiçbir gerek tooinclude yok "@" hello kayıt kümesi adı bir SRV kaydı kümesi hello bölgenin tepesinde oluştururken.</span><span class="sxs-lookup"><span data-stu-id="3eac7-166">There is no need tooinclude "@" in hello record set name when creating an SRV record set at hello zone apex.</span></span>

```azurecli
az network dns record-set srv set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name _sip._tls --priority 10 --weight 5 --port 8080 --target sip.contoso.com
```

### <a name="create-a-txt-record"></a><span data-ttu-id="3eac7-167">TXT kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3eac7-167">Create a TXT record</span></span>

<span data-ttu-id="3eac7-168">Merhaba aşağıdaki örnekte nasıl toocreate bir TXT kaydı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-168">hello following example shows how toocreate a TXT record.</span></span> <span data-ttu-id="3eac7-169">TXT kayıtlarının desteklenen hello maksimum dize uzunluğu hakkında daha fazla bilgi için bkz: [TXT kayıtlarının](dns-zones-records.md#txt-records).</span><span class="sxs-lookup"><span data-stu-id="3eac7-169">For more information about hello maximum string length supported in TXT records, see [TXT records](dns-zones-records.md#txt-records).</span></span>

```azurecli
az network dns record-set txt set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-txt --value "This is a TXT record"
```

## <a name="get-a-record-set"></a><span data-ttu-id="3eac7-170">Bir kayıt kümesini Al</span><span class="sxs-lookup"><span data-stu-id="3eac7-170">Get a record set</span></span>

<span data-ttu-id="3eac7-171">tooretrieve varolan bir kayıt kümesini kullanma `az network dns record-set <record-type> show`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-171">tooretrieve an existing record set, use `az network dns record-set <record-type> show`.</span></span> <span data-ttu-id="3eac7-172">Yardım için bkz. `az network dns record-set <record-type> show --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-172">For help, see `az network dns record-set <record-type> show --help`.</span></span>

<span data-ttu-id="3eac7-173">Bir kayıt veya kayıt kümesi oluştururken, hello kayıt kümesinin adı verilen olarak olmalıdır bir *göreli* adı, hello bölge adı dışarıda gerekir anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-173">As when creating a record or record set, hello record set name given must be a *relative* name, meaning it must exclude hello zone name.</span></span> <span data-ttu-id="3eac7-174">Toospecify hello kayıt türü de gerekir, hello kayıt içeren hello bölge ayarlamak ve hello bölge içeren kaynak grubunu hello.</span><span class="sxs-lookup"><span data-stu-id="3eac7-174">You also need toospecify hello record type, hello zone containing hello record set, and hello resource group containing hello zone.</span></span>

<span data-ttu-id="3eac7-175">Merhaba aşağıdaki örnek hello kaydı alır *www* bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3eac7-175">hello following example retrieves hello record *www* of type A from zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a show --resource-group myresourcegroup --zone-name contoso.com --name www
```

## <a name="list-record-sets"></a><span data-ttu-id="3eac7-176">Liste kayıt kümeleri</span><span class="sxs-lookup"><span data-stu-id="3eac7-176">List record sets</span></span>

<span data-ttu-id="3eac7-177">Hello kullanarak bir DNS bölgedeki tüm kayıtları listeleyebilirsiniz `az network dns record-set list` komutu.</span><span class="sxs-lookup"><span data-stu-id="3eac7-177">You can list all records in a DNS zone by using hello `az network dns record-set list` command.</span></span> <span data-ttu-id="3eac7-178">Yardım için bkz. `az network dns record-set list --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-178">For help, see `az network dns record-set list --help`.</span></span>

<span data-ttu-id="3eac7-179">Bu örnekte tüm kayıt kümeleri hello bölgesinde döndürür *contoso.com*, kaynak grubundaki *MyResourceGroup*, adı veya kayıt türü ne olursa olsun:</span><span class="sxs-lookup"><span data-stu-id="3eac7-179">This example returns all record sets in hello zone *contoso.com*, in resource group *MyResourceGroup*, regardless of name or record type:</span></span>

```azurecli
az network dns record-set list --resource-group myresourcegroup --zone-name contoso.com
```

<span data-ttu-id="3eac7-180">Bu örnek kayıt türü (Bu durumda, 'Bir' kayıtları) verilen hello eşleşen tüm kayıt kümelerinin döndürür:</span><span class="sxs-lookup"><span data-stu-id="3eac7-180">This example returns all record sets that match hello given record type (in this case, 'A' records):</span></span>

```azurecli
az network dns record-set a list --resource-group myresourcegroup --zone-name contoso.com 
```

## <a name="add-a-record-tooan-existing-record-set"></a><span data-ttu-id="3eac7-181">Kayıt kümesi varolan bir kayıt tooan Ekle</span><span class="sxs-lookup"><span data-stu-id="3eac7-181">Add a record tooan existing record set</span></span>

<span data-ttu-id="3eac7-182">Kullanabileceğiniz `az network dns record-set <record-type> set-record` hem yeni bir kayıt kaydında toocreate ayarlayın veya kayıt tooan varolan bir kaydı tooadd ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3eac7-182">You can use `az network dns record-set <record-type> set-record` both toocreate a record in a new record set, or tooadd a record tooan existing record set.</span></span>

<span data-ttu-id="3eac7-183">Daha fazla bilgi için bkz: [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.</span><span class="sxs-lookup"><span data-stu-id="3eac7-183">For more information, see [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

## <a name="remove-a-record-from-an-existing-record-set"></a><span data-ttu-id="3eac7-184">Varolan bir kayıt kümesinden bir kaydı kaldırma.</span><span class="sxs-lookup"><span data-stu-id="3eac7-184">Remove a record from an existing record set.</span></span>

<span data-ttu-id="3eac7-185">tooremove bir DNS kaydı varolan kayıt kümesinden, kullanım `az network dns record-set <record-type> remove-record`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-185">tooremove a DNS record from an existing record set, use `az network dns record-set <record-type> remove-record`.</span></span> <span data-ttu-id="3eac7-186">Yardım için bkz. `az network dns record-set <record-type> remove-record -h`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-186">For help, see `az network dns record-set <record-type> remove-record -h`.</span></span>

<span data-ttu-id="3eac7-187">Bu komut, kayıt kümesindeki bir DNS kaydı siler.</span><span class="sxs-lookup"><span data-stu-id="3eac7-187">This command deletes a DNS record from a record set.</span></span> <span data-ttu-id="3eac7-188">Bir kayıt kümesindeki Hello son kaydı silinirse, hello kayıt kendisini kümesi de silinir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-188">If hello last record in a record set is deleted, hello record set itself is also deleted.</span></span> <span data-ttu-id="3eac7-189">Bunun yerine, kullanın hello tookeep hello boş kayıt kümesi `--keep-empty-record-set` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="3eac7-189">tookeep hello empty record set instead, use hello `--keep-empty-record-set` option.</span></span>

<span data-ttu-id="3eac7-190">Toospecify ihtiyacınız hello kayıt toobe silinmiş ve onu silinmesi, kullanarak hello bölge kayıt kullanarak oluştururken, aynı parametreleri hello `az network dns record-set <record-type> set-record`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-190">You need toospecify hello record toobe deleted and hello zone it should be deleted from, using hello same parameters as when creating a record using `az network dns record-set <record-type> set-record`.</span></span> <span data-ttu-id="3eac7-191">Bu parametreler açıklanmaktadır [bir DNS kaydı oluşturma](#create-a-dns-record) ve [kayıtlar diğer türleri oluşturma](#create-records-of-other-types) üstünde.</span><span class="sxs-lookup"><span data-stu-id="3eac7-191">These parameters are described in [Create a DNS record](#create-a-dns-record) and [Create records of other types](#create-records-of-other-types) above.</span></span>

<span data-ttu-id="3eac7-192">Aşağıdaki örnek siler hello hello hello kaydından ' 1.2.3.4 adlandırılmış kümesi' içeren bir kaydı *www* hello bölgesinde *contoso.com*, hello kaynak grubunda *MyResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="3eac7-192">hello following example deletes hello A record with value '1.2.3.4' from hello record set named *www* in hello zone *contoso.com*, in hello resource group *MyResourceGroup*.</span></span>

```azurecli
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "www" --ipv4-address 1.2.3.4
```

## <a name="modify-an-existing-record-set"></a><span data-ttu-id="3eac7-193">Varolan bir kayıt kümesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="3eac7-193">Modify an existing record set</span></span>

<span data-ttu-id="3eac7-194">Her bir kayıt kümesi içeren bir [yaşam süresi (TTL)](dns-zones-records.md#time-to-live), [meta veri](dns-zones-records.md#tags-and-metadata)ve DNS kayıtlarını.</span><span class="sxs-lookup"><span data-stu-id="3eac7-194">Each record set contains a [time-to-live (TTL)](dns-zones-records.md#time-to-live), [metadata](dns-zones-records.md#tags-and-metadata), and DNS records.</span></span> <span data-ttu-id="3eac7-195">Merhaba aşağıdaki bölümlerde açıklanmıştır nasıl toomodify her bu özelliklerin.</span><span class="sxs-lookup"><span data-stu-id="3eac7-195">hello following sections explain how toomodify each of these properties.</span></span>

### <a name="toomodify-an-a-aaaa-mx-ns-ptr-srv-or-txt-record"></a><span data-ttu-id="3eac7-196">toomodify bir A, AAAA, MX, NS, PTR, SRV ve TXT kaydı</span><span class="sxs-lookup"><span data-stu-id="3eac7-196">toomodify an A, AAAA, MX, NS, PTR, SRV, or TXT record</span></span>

<span data-ttu-id="3eac7-197">var olan bir tür A, AAAA, MX, NS, PTR, SRV ve TXT kaydını toomodify, yeni bir kayıt ve ardından silme hello varolan kaydı ilk eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-197">toomodify an existing record of type A, AAAA, MX, NS, PTR, SRV, or TXT, you should first add a new record and then delete hello existing record.</span></span> <span data-ttu-id="3eac7-198">Ayrıntılı yönergeler için toodelete ve kayıtları eklemek için bkz: Merhaba bu makalenin önceki bölümlerinde.</span><span class="sxs-lookup"><span data-stu-id="3eac7-198">For detailed instructions on how toodelete and add records, see hello earlier sections of this article.</span></span>

<span data-ttu-id="3eac7-199">Aşağıdaki örneğine hello nasıl toomodify bir 'A' kaydından IP adresi 1.2.3.4 tooIP adres 5.6.7.8 gösterir:</span><span class="sxs-lookup"><span data-stu-id="3eac7-199">hello following example shows how toomodify an 'A' record, from IP address 1.2.3.4 tooIP address 5.6.7.8:</span></span>

```azurecli
az network dns record-set a set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 5.6.7.8
az network dns record-set a remove-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name www --ipv4-address 1.2.3.4
```

<span data-ttu-id="3eac7-200">Ekle, Kaldır veya değiştiremezsiniz hello kayıtları otomatik olarak oluşturulan NS kayıt kümesi hello bölgenin tepesinde hello (`--Name "@"`, tırnak işaretleri dahil olmak üzere).</span><span class="sxs-lookup"><span data-stu-id="3eac7-200">You cannot add, remove, or modify hello records in hello automatically created NS record set at hello zone apex (`--Name "@"`, including quote marks).</span></span> <span data-ttu-id="3eac7-201">Bu kayıt kümesi için izin verilen hello yalnızca TTL ve meta veri toomodify hello kayıt kümesinin değişir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-201">For this record set, hello only changes permitted are toomodify hello record set TTL and metadata.</span></span>

### <a name="toomodify-a-cname-record"></a><span data-ttu-id="3eac7-202">toomodify bir CNAME kaydı</span><span class="sxs-lookup"><span data-stu-id="3eac7-202">toomodify a CNAME record</span></span>

<span data-ttu-id="3eac7-203">Çoğu diğer kayıt türlerinin aksine, bir CNAME kayıt kümesi yalnızca tek bir kaydını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-203">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="3eac7-204">Bu nedenle, yeni bir kayıt ekleme ve diğer kayıt türleri için olduğu gibi hello varolan kaydını kaldırarak hello geçerli değeri değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="3eac7-204">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="3eac7-205">Bunun yerine bir CNAME kaydı toomodify kullanın `az network dns record-set cname set-record`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-205">Instead, toomodify a CNAME record, use `az network dns record-set cname set-record`.</span></span> <span data-ttu-id="3eac7-206">Yardım için bkz.`az network dns record-set cname set-record --help`</span><span class="sxs-lookup"><span data-stu-id="3eac7-206">For help, see `az network dns record-set cname set-record --help`</span></span>

<span data-ttu-id="3eac7-207">Merhaba örnek değiştirir hello CNAME kayıt kümesi *www* hello bölgesinde *contoso.com*, kaynak grubundaki *MyResourceGroup*, toopoint çok yerine ' www.fabrikam.net' kendi Mevcut değer:</span><span class="sxs-lookup"><span data-stu-id="3eac7-207">hello example modifies hello CNAME record set *www* in hello zone *contoso.com*, in resource group *MyResourceGroup*, toopoint too'www.fabrikam.net' instead of its existing value:</span></span>

```azurecli
az network dns record-set cname set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name test-cname --cname www.fabrikam.net
``` 

### <a name="toomodify-an-soa-record"></a><span data-ttu-id="3eac7-208">toomodify bir SOA kaydı</span><span class="sxs-lookup"><span data-stu-id="3eac7-208">toomodify an SOA record</span></span>

<span data-ttu-id="3eac7-209">Çoğu diğer kayıt türlerinin aksine, bir CNAME kayıt kümesi yalnızca tek bir kaydını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-209">Unlike most other record types, a CNAME record set can only contain a single record.</span></span>  <span data-ttu-id="3eac7-210">Bu nedenle, yeni bir kayıt ekleme ve diğer kayıt türleri için olduğu gibi hello varolan kaydını kaldırarak hello geçerli değeri değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="3eac7-210">Therefore, you cannot replace hello current value by adding a new record and removing hello existing record, as for other record types.</span></span>

<span data-ttu-id="3eac7-211">Bunun yerine, toomodify hello SOA kaydı kullanın `az network dns record-set soa update`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-211">Instead, toomodify hello SOA record, use `az network dns record-set soa update`.</span></span> <span data-ttu-id="3eac7-212">Yardım için bkz. `az network dns record-set soa update --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-212">For help, see `az network dns record-set soa update --help`.</span></span>

<span data-ttu-id="3eac7-213">Merhaba aşağıdaki örnekte nasıl hello SOA tooset hello 'e-posta' özelliği kayıt hello bölgenin gösterir *contoso.com* hello kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3eac7-213">hello following example shows how tooset hello 'email' property of hello SOA record for hello zone *contoso.com* in hello resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set soa update --resource-group myresourcegroup --zone-name contoso.com --email admin.contoso.com
```

### <a name="toomodify-ns-records-at-hello-zone-apex"></a><span data-ttu-id="3eac7-214">Merhaba bölge tepesinde toomodify NS kayıtları</span><span class="sxs-lookup"><span data-stu-id="3eac7-214">toomodify NS records at hello zone apex</span></span>

<span data-ttu-id="3eac7-215">Merhaba NS kayıt Hello bölgenin tepesinde kümesi her DNS bölge ile otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3eac7-215">hello NS record set at hello zone apex is automatically created with each DNS zone.</span></span> <span data-ttu-id="3eac7-216">Hello Azure DNS ad sunucuları atanan toohello bölgesi hello adlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-216">It contains hello names of hello Azure DNS name servers assigned toohello zone.</span></span>

<span data-ttu-id="3eac7-217">Ek ad sunucuları toothis NS kayıt kümesi, etki alanları birden fazla DNS sağlayıcınız ile birlikte barındırma toosupport ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3eac7-217">You can add additional name servers toothis NS record set, toosupport co-hosting domains with more than one DNS provider.</span></span> <span data-ttu-id="3eac7-218">Merhaba TTL ve bu kayıt kümesi için meta verileri de değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3eac7-218">You can also modify hello TTL and metadata for this record set.</span></span> <span data-ttu-id="3eac7-219">Ancak, kaldırmak veya hello önceden doldurulmuş haldedir Azure DNS ad sunucuları değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3eac7-219">However, you cannot remove or modify hello pre-populated Azure DNS name servers.</span></span>

<span data-ttu-id="3eac7-220">Bu yalnızca toohello NS kayıt kümesi hello bölge tepesinde en geçerli olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3eac7-220">Note that this applies only toohello NS record set at hello zone apex.</span></span> <span data-ttu-id="3eac7-221">Diğer NS kayıt kümelerinde bölgenizi (olarak kullanılan toodelegate alt bölgeler) kısıtlama değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-221">Other NS record sets in your zone (as used toodelegate child zones) can be modified without constraint.</span></span>

<span data-ttu-id="3eac7-222">Aşağıdaki örneğine hello tooadd bir ek ad sunucusu toohello NS kaydı hello bölgenin tepesinde nasıl ayarlanacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="3eac7-222">hello following example shows how tooadd an additional name server toohello NS record set at hello zone apex:</span></span>

```azurecli
az network dns record-set ns set-record --resource-group myresourcegroup --zone-name contoso.com --record-set-name "@" --nsdname ns1.myotherdnsprovider.com 
```

### <a name="toomodify-hello-ttl-of-an-existing-record-set"></a><span data-ttu-id="3eac7-223">toomodify hello varolan bir kaydı TTL Ayarla</span><span class="sxs-lookup"><span data-stu-id="3eac7-223">toomodify hello TTL of an existing record set</span></span>

<span data-ttu-id="3eac7-224">Varolan bir kaydı TTL toomodify hello ayarlayabilir, kullanabilir `azure network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-224">toomodify hello TTL of an existing record set, use `azure network dns record-set <record-type> update`.</span></span> <span data-ttu-id="3eac7-225">Yardım için bkz. `azure network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-225">For help, see `azure network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="3eac7-226">Aşağıdaki örnek hello nasıl toomodify kayıt kümesi TTL, bu durumda too60 saniye gösterir:</span><span class="sxs-lookup"><span data-stu-id="3eac7-226">hello following example shows how toomodify a record set TTL, in this case too60 seconds:</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set ttl=60
```

### <a name="toomodify-hello-metadata-of-an-existing-record-set"></a><span data-ttu-id="3eac7-227">Varolan bir kayıt kümesini toomodify hello meta verileri</span><span class="sxs-lookup"><span data-stu-id="3eac7-227">toomodify hello metadata of an existing record set</span></span>

<span data-ttu-id="3eac7-228">[Kayıt kümesi meta verileri](dns-zones-records.md#tags-and-metadata) anahtar-değer çiftleri olarak her bir kayıt kümesi ile kullanılan tooassociate uygulamaya özgü verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="3eac7-228">[Record set metadata](dns-zones-records.md#tags-and-metadata) can be used tooassociate application-specific data with each record set, as key-value pairs.</span></span> <span data-ttu-id="3eac7-229">Varolan bir kaydı toomodify hello meta verileri ayarlama, kullanın `az network dns record-set <record-type> update`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-229">toomodify hello metadata of an existing record set, use `az network dns record-set <record-type> update`.</span></span> <span data-ttu-id="3eac7-230">Yardım için bkz. `az network dns record-set <record-type> update --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-230">For help, see `az network dns record-set <record-type> update --help`.</span></span>

<span data-ttu-id="3eac7-231">Merhaba aşağıdaki örnek toomodify kayıt iki meta veri girişi ile nasıl ayarlanacağını gösterir "Bölüm Finans =" ve "ortam üretim =".</span><span class="sxs-lookup"><span data-stu-id="3eac7-231">hello following example shows how toomodify a record set with two metadata entries, "dept=finance" and "environment=production".</span></span> <span data-ttu-id="3eac7-232">Var olan herhangi bir meta veri olduğuna dikkat edin *yerini* verilen hello değerlere göre.</span><span class="sxs-lookup"><span data-stu-id="3eac7-232">Note that any existing metadata is *replaced* by hello values given.</span></span>

```azurecli
az network dns record-set a update --resource-group myresourcegroup --zone-name contoso.com --name www --set metadata.dept=finance metadata.environment=production
```

## <a name="delete-a-record-set"></a><span data-ttu-id="3eac7-233">Bir kayıt kümesini Sil</span><span class="sxs-lookup"><span data-stu-id="3eac7-233">Delete a record set</span></span>

<span data-ttu-id="3eac7-234">Kayıt kümeleri hello kullanarak silinebilir `az network dns record-set <record-type> delete` komutu.</span><span class="sxs-lookup"><span data-stu-id="3eac7-234">Record sets can be deleted by using hello `az network dns record-set <record-type> delete` command.</span></span> <span data-ttu-id="3eac7-235">Yardım için bkz. `azure network dns record-set <record-type> delete --help`.</span><span class="sxs-lookup"><span data-stu-id="3eac7-235">For help, see `azure network dns record-set <record-type> delete --help`.</span></span> <span data-ttu-id="3eac7-236">Kayıt kümesi siliniyor hello kayıt kümesi içindeki tüm kayıtları siler.</span><span class="sxs-lookup"><span data-stu-id="3eac7-236">Deleting a record set also deletes all records within hello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="3eac7-237">Merhaba SOA ve NS kayıt kümelerini hello bölge tepesinde adresindeki silemezsiniz (`--name "@"`).</span><span class="sxs-lookup"><span data-stu-id="3eac7-237">You cannot delete hello SOA and NS record sets at hello zone apex (`--name "@"`).</span></span>  <span data-ttu-id="3eac7-238">Bu, ne zaman hello bölge oluşturuldu ve hello bölge silindiğinde otomatik olarak silinir otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3eac7-238">These are created automatically when hello zone was created, and are deleted automatically when hello zone is deleted.</span></span>

<span data-ttu-id="3eac7-239">Merhaba aşağıdaki örnek siler hello kayıt adlandırılmış kümesi *www* hello bölgeden türü a *contoso.com* kaynak grubunda *MyResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3eac7-239">hello following example deletes hello record set named *www* of type A from hello zone *contoso.com* in resource group *MyResourceGroup*:</span></span>

```azurecli
az network dns record-set a delete --resource-group myresourcegroup --zone-name contoso.com --name www
```

<span data-ttu-id="3eac7-240">İstendiğinde tooconfirm hello silme işlemi var.</span><span class="sxs-lookup"><span data-stu-id="3eac7-240">You are prompted tooconfirm hello delete operation.</span></span> <span data-ttu-id="3eac7-241">Bu komut istemi toosuppress hello kullanmak `--yes` geçin.</span><span class="sxs-lookup"><span data-stu-id="3eac7-241">toosuppress this prompt, use hello `--yes` switch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3eac7-242">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3eac7-242">Next steps</span></span>

<span data-ttu-id="3eac7-243">Daha fazla bilgi edinmek [bölgeleri ve Azure DNS kayıtlarında](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="3eac7-243">Learn more about [zones and records in Azure DNS](dns-zones-records.md).</span></span>
<br>
<span data-ttu-id="3eac7-244">Nasıl çok öğrenin[bölgeleri ve kayıtları korumak](dns-protect-zones-recordsets.md) Azure DNS kullanırken.</span><span class="sxs-lookup"><span data-stu-id="3eac7-244">Learn how too[protect your zones and records](dns-protect-zones-recordsets.md) when using Azure DNS.</span></span>
