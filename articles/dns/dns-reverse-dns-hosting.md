---
title: "aaaHosting Azure DNS'de DNS arama bölgeleri ters | Microsoft Docs"
description: "Nasıl toouse Azure DNS toohost hello ters DNS arama bölgeleri IP aralıkları için bilgi edinin"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 24feb8ef1c75a7d91938867f348fed1190046e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="a698c-103">Azure DNS geriye doğru DNS araması bölgelerinde barındırma</span><span class="sxs-lookup"><span data-stu-id="a698c-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="a698c-104">Bu makalede, nasıl Azure DNS'de, atanan IP aralıkları için DNS arama bölgeleri ters toohost hello açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a698c-104">This article explains how toohost hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="a698c-105">Merhaba geriye doğru arama bölgesi tarafından temsil edilen hello IP aralıkları tooyour kuruluş, genellikle ISS'niz tarafından atanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a698c-105">hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="a698c-106">tooconfigure DNS geriye doğru Azure ait IP adresi atanmış tooyour Azure hizmeti için bkz: [hello geriye doğru arama ayrılan hello IP adreslerini tooyour Azure hizmeti için yapılandırma](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-106">tooconfigure reverse DNS for Azure-owned IP address assigned tooyour Azure service, see [configure hello reverse lookup for hello IP addresses allocated tooyour Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="a698c-107">Bu makalede okumadan önce bu bilgi sahibi olmanız [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="a698c-108">Bu makalede, ilk geriye doğru arama DNS bölgesi ve hello Azure portal, Azure PowerShell, Azure CLI 1.0 veya Azure CLI 2.0 kullanarak kayıt hello adımları toocreate anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a698c-108">This article walks you through hello steps toocreate your first reverse lookup DNS zone and record using hello Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="a698c-109">Geriye doğru arama DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a698c-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="a698c-110">İçinde toohello oturum [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a698c-110">Sign in toohello [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="a698c-111">Hello Hub menüsünde, tıklayıp **yeni** > **ağ** > ve ardından **DNS bölgesi** tooopen hello **oluşturma DNS bölgesi**dikey.</span><span class="sxs-lookup"><span data-stu-id="a698c-111">On hello Hub menu, click and click **New** > **Networking** > and then click **DNS zone** tooopen hello **Create DNS zone** blade.</span></span>

   ![DNS bölgesi](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="a698c-113">Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde, DNS bölgenizi adı.</span><span class="sxs-lookup"><span data-stu-id="a698c-113">On hello **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="a698c-114">Merhaba bölgenin Hello adı farklı IPv4 ve IPv6 önekleri için hazırlanmış.</span><span class="sxs-lookup"><span data-stu-id="a698c-114">hello name of hello zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="a698c-115">Her iki hello talimatlar için kullanması [IPv4](#ipv4) veya [IPv6](#ipv6) tooname bölgenizi.</span><span class="sxs-lookup"><span data-stu-id="a698c-115">Use either hello instructions for [IPV4](#ipv4) or [IPv6](#ipv6) tooname your zone.</span></span> <span data-ttu-id="a698c-116">Tıklatın tamamlandığında **oluşturma** toocreate hello bölgesi.</span><span class="sxs-lookup"><span data-stu-id="a698c-116">When complete click **Create** toocreate hello zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="a698c-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="a698c-117">IPv4</span></span>

<span data-ttu-id="a698c-118">bir IPv4 geriye doğru arama bölgesi Hello adını temsil ettiği hello IP aralığına dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="a698c-118">hello name of an IPv4 reverse lookup zone is based on hello IP range it represents.</span></span> <span data-ttu-id="a698c-119">Biçim aşağıdaki hello olmalıdır: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="a698c-119">It should be in hello following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="a698c-120">Örnekler için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="a698c-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="a698c-121">Azure DNS'de Sınıfsız geriye doğru DNS arama bölgeleri oluştururken, kısa çizgi kullanmanız gerekir (`-`) yerine eğik çizgi ('/ ') hello bölge adı.</span><span class="sxs-lookup"><span data-stu-id="a698c-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in hello zone name.</span></span>
>
> <span data-ttu-id="a698c-122">Örneğin, hello IP aralığı 192.0.2.128/26 için kullanmanız gerekir `128-26.2.0.192.in-addr.arpa` hello bölge adı yerine olarak `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="a698c-122">For example, for hello IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as hello zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="a698c-123">Her ikisi de hello DNS standartları tarafından desteklenir, ancak hello eğik içeren adlara DNS bölgesi, bunun nedeni (`/`) karakter Azure DNS'de desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a698c-123">This is because, while both are supported by hello DNS standards, DNS zone names containing hello forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="a698c-124">Merhaba aşağıdaki örnekte nasıl toocreate 'Sınıfı C' adlı DNS bölgesi ters gösterir `2.0.192.in-addr.arpa` hello Azure Portalı aracılığıyla Azure DNS'de:</span><span class="sxs-lookup"><span data-stu-id="a698c-124">hello following example shows how toocreate a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![DNS bölgesi oluşturma](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="a698c-126">Merhaba 'Kaynak grubu konumu' hello kaynak grubu için hello konum tanımlar ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="a698c-126">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="a698c-127">Merhaba DNS bölgesi konumunu her zaman 'global' dır ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a698c-127">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="a698c-128">Merhaba aşağıdaki toocomplete bu nasıl görev ile örnekler Azure PowerShell ve Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="a698c-128">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a698c-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a698c-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a698c-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a698c-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a698c-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a698c-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="a698c-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="a698c-132">IPv6</span></span>

<span data-ttu-id="a698c-133">bir IPv6 geriye doğru arama bölgesi Hello adını form aşağıdaki hello olmalıdır: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="a698c-133">hello name of an IPv6 reverse lookup zone should be in hello following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="a698c-134">Örnekler için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="a698c-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="a698c-135">Merhaba aşağıdaki örnekte nasıl toocreate bir IPv6 geriye doğru DNS arama bölgesini adlı gösterir `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` hello Azure Portalı aracılığıyla Azure DNS'de:</span><span class="sxs-lookup"><span data-stu-id="a698c-135">hello following example shows how toocreate an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via hello Azure portal:</span></span>

 ![DNS bölgesi oluşturma](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="a698c-137">Merhaba 'Kaynak grubu konumu' hello kaynak grubu için hello konum tanımlar ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="a698c-137">hello 'Resource group location' defines hello location for hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="a698c-138">Merhaba DNS bölgesi konumunu her zaman 'global' dır ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a698c-138">hello DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="a698c-139">Merhaba aşağıdaki toocomplete bu nasıl görev ile örnekler Azure PowerShell ve Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="a698c-139">hello following examples show how toocomplete this task with Azure PowerShell and hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a698c-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a698c-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="a698c-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a698c-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="a698c-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a698c-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="a698c-143">DNS geriye doğru arama bölgesini temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="a698c-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="a698c-144">Geriye doğru DNS araması bölgenizi oluşturduktan, hello üst bölgeden hello bölge temsilcisi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a698c-144">Having created your reverse DNS lookup zone, you must ensure that hello zone is delegated from hello parent zone.</span></span> <span data-ttu-id="a698c-145">DNS temsilcisi geriye doğru DNS araması bölgenizi barındırma hello DNS ad çözümleme işlemi toofind hello ad sunucuları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a698c-145">DNS delegation enables hello DNS name resolution process toofind hello name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="a698c-146">Bu ad sunucuları tooanswer DNS geriye doğru sorgularını hello IP adreslerinin adres aralığınızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a698c-146">This enables those name servers tooanswer DNS reverse queries for hello IP addresses in your address range.</span></span>

<span data-ttu-id="a698c-147">Bir DNS bölgesi için temsilci seçme işleminin hello açıklanan ileriye doğru arama bölgeleri için [, etki alanı tooAzure DNS temsilci](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-147">For forward lookup zones, hello process of delegating a DNS zone is described in [Delegate your domain tooAzure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="a698c-148">Geriye doğru arama bölgeleri için temsilci seçme çalışır hello aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="a698c-148">Delegation for reverse lookup zones works hello same way.</span></span> <span data-ttu-id="a698c-149">Merhaba yalnızca tooconfigure hello ad sunucuları hello etki alanı adı kayıt şirketiniz yerine IP aralığınızı sağlanan ISS ile gerektiğini farktır.</span><span class="sxs-lookup"><span data-stu-id="a698c-149">hello only difference is that you need tooconfigure hello name servers with hello ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="a698c-150">Bir DNS PTR kaydı oluştur</span><span class="sxs-lookup"><span data-stu-id="a698c-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="a698c-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="a698c-151">IPv4</span></span>

<span data-ttu-id="a698c-152">Merhaba aşağıdaki örnek, Azure DNS geriye doğru DNS bölgesinde bir PTR kaydı oluşturma hello işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a698c-152">hello following example walks you through hello process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="a698c-153">Diğer kayıt türleri ve toomodify mevcut kayıtları için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-153">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="a698c-154">Merhaba hello üstündeki **DNS bölgesi** dikey penceresinde, select **+ kayıt kümesine** tooopen hello **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="a698c-154">At hello top of hello **DNS zone** blade, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

 ![DNS bölgesi](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="a698c-156">Merhaba üzerinde **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="a698c-156">On hello **Add record set** blade.</span></span> 
1. <span data-ttu-id="a698c-157">Seçin **PTR** hello kaydından "**türü**" menüsü.</span><span class="sxs-lookup"><span data-stu-id="a698c-157">Select **PTR** from hello record "**Type**" menu.</span></span>  
1. <span data-ttu-id="a698c-158">Merhaba bir PTR kaydı hello kayıt kümesi adını toobe hello hello IPv4 adresi geri kalanı ters sırada gerekir.</span><span class="sxs-lookup"><span data-stu-id="a698c-158">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv4 address in reverse order.</span></span> <span data-ttu-id="a698c-159">Bu örnekte, hello ilk üç sekizlisinin zaten hello bölge adı (.2.0.192) bir parçası olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="a698c-159">In this example, hello first three octets are already populated as part of hello zone name (.2.0.192).</span></span> <span data-ttu-id="a698c-160">Bu nedenle, yalnızca hello son sekizli hello ad alanına sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a698c-160">Therefore, only hello last octet is supplied in hello name field.</span></span> <span data-ttu-id="a698c-161">Örneğin, kayıt kümenizi adlandırabilirsiniz "**15**", IP adresi 192.0.2.15 olan bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="a698c-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="a698c-162">Merhaba, "**etki alanı adı**" alanında, hello IP kullanan hello kaynağın hello tam etki alanı adı (FQDN) girin.</span><span class="sxs-lookup"><span data-stu-id="a698c-162">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
1. <span data-ttu-id="a698c-163">Seçin **Tamam** hello altındaki hello dikey toocreate hello DNS kaydı.</span><span class="sxs-lookup"><span data-stu-id="a698c-163">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

 ![kayıt kümesi Ekle](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="a698c-165">Merhaba nasıl örnekler aşağıdadır toocomplete bu görevi, PowerShell ve hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="a698c-165">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a698c-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a698c-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="a698c-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a698c-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="a698c-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a698c-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="a698c-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="a698c-169">IPv6</span></span>

<span data-ttu-id="a698c-170">Aşağıdaki örnek hello yeni 'PTR' kayıt oluşturma hello işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="a698c-170">hello following example walks you through hello process of creating new 'PTR' record.</span></span> <span data-ttu-id="a698c-171">Diğer kayıt türleri ve toomodify mevcut kayıtları için bkz: [yönetmek DNS kayıtlarını ve kayıt kümelerini kullanarak hello Azure portal](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-171">For other record types and toomodify existing records, see [Manage DNS records and record sets by using hello Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="a698c-172">Merhaba hello üstündeki **DNS bölge dikey**seçin **+ kayıt kümesine** tooopen hello **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="a698c-172">At hello top of hello **DNS zone blade**, select **+ Record set** tooopen hello **Add record set** blade.</span></span>

  ![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="a698c-174">Merhaba üzerinde **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="a698c-174">On hello **Add record set** blade.</span></span> 
3. <span data-ttu-id="a698c-175">Seçin **PTR** hello kaydından "**türü**" menüsü.</span><span class="sxs-lookup"><span data-stu-id="a698c-175">Select **PTR** from hello record "**Type**" menu.</span></span>  
4. <span data-ttu-id="a698c-176">Merhaba bir PTR kaydı hello kayıt kümesi adını toobe hello hello IPv6 adresi geri kalanı ters sırada gerekir.</span><span class="sxs-lookup"><span data-stu-id="a698c-176">hello name of hello record set for a PTR record needs toobe hello rest of hello IPv6 address in reverse order.</span></span> <span data-ttu-id="a698c-177">Sıfır sıkıştırma eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a698c-177">It must not include any zero compression.</span></span> <span data-ttu-id="a698c-178">Bu örnekte, IPv6 zaten hello bölge adı (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa) bir parçası olarak doldurulmuş hello ilk 64 bit hello.</span><span class="sxs-lookup"><span data-stu-id="a698c-178">In this example, hello first 64 bits of hello IPv6 are already populated as part of hello zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="a698c-179">Bu nedenle, yalnızca son 64 bit hello hello ad alanına sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a698c-179">Therefore, only hello last 64 bits are supplied in hello name field.</span></span> <span data-ttu-id="a698c-180">Merhaba hello IP adresinin son 64 bit girilir ters sırada bir süre her onaltılık sayı hello bölücüyü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a698c-180">hello last 64 bits of hello IP address are entered in reverse order, using a period as hello delimiter between each hexadecimal number.</span></span> <span data-ttu-id="a698c-181">Örneğin, kayıt kümenizi adlandırabilirsiniz "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**", IP adresi 2001:0db8:abdc:0000:f524:10bc:1af9:405e olan bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="a698c-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="a698c-182">Merhaba, "**etki alanı adı**" alanında, hello IP kullanan hello kaynağın hello tam etki alanı adı (FQDN) girin.</span><span class="sxs-lookup"><span data-stu-id="a698c-182">In hello "**Domain Name**" field, enter hello fully qualified domain name (FQDN) of hello resource using hello IP.</span></span>
6. <span data-ttu-id="a698c-183">Seçin **Tamam** hello altındaki hello dikey toocreate hello DNS kaydı.</span><span class="sxs-lookup"><span data-stu-id="a698c-183">Select **OK** at hello bottom of hello blade toocreate hello DNS record.</span></span>

![kayıt kümesi dikey ekleme](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="a698c-185">Merhaba nasıl örnekler aşağıdadır toocomplete bu görevi, PowerShell ve hello AzureCLI:</span><span class="sxs-lookup"><span data-stu-id="a698c-185">hello following are examples on how toocomplete this task with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a698c-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a698c-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="a698c-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a698c-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="a698c-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a698c-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="a698c-189">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a698c-189">View Records</span></span>

<span data-ttu-id="a698c-190">oluşturduğunuz tooview hello kayıtları tooyour DNS bölgesinde hello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="a698c-190">tooview hello records you created, navigate tooyour DNS zone in hello Azure portal.</span></span> <span data-ttu-id="a698c-191">Merhaba parçası Hello alt **DNS bölgesi** dikey penceresinde hello DNS bölgesi için hello kayıtlarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a698c-191">In hello lower part of hello **DNS zone** blade, you can see hello records for hello DNS zone.</span></span> <span data-ttu-id="a698c-192">Her bölgede oluşturulan, hello varsayılan NS ve SOA kayıtları, artı, oluşturduğunuz tüm yeni kayıtlar görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a698c-192">You should see hello default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="a698c-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="a698c-193">IPv4</span></span>

<span data-ttu-id="a698c-194">IPv4 PTR kayıtları gösteren DNS bölge dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="a698c-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="a698c-196">Merhaba aşağıdaki örneklerde PowerShell kullanarak nasıl tooview hello PTR kayıtlarını göster veya Azure CLI hello:</span><span class="sxs-lookup"><span data-stu-id="a698c-196">hello following examples show how tooview hello PTR records using PowerShell or hello Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a698c-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a698c-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a698c-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a698c-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a698c-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a698c-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="a698c-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="a698c-200">IPv6</span></span>

<span data-ttu-id="a698c-201">IPv6 PTR kayıtları gösteren DNS bölge dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="a698c-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="a698c-203">Merhaba, tooview hello PowerShell ve hello AzureCLI kayıtları nasıl örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a698c-203">hello following are examples on how tooview hello records with PowerShell and hello AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="a698c-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a698c-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="a698c-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a698c-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="a698c-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a698c-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="a698c-207">SSS</span><span class="sxs-lookup"><span data-stu-id="a698c-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="a698c-208">Geriye doğru DNS arama bölgeleri my ISS atanan IP blokları Azure DNS üzerinde barındırabilir?</span><span class="sxs-lookup"><span data-stu-id="a698c-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="a698c-209">Evet.</span><span class="sxs-lookup"><span data-stu-id="a698c-209">Yes.</span></span> <span data-ttu-id="a698c-210">Azure DNS'de kendi IP aralıkları için Hello (ARPA) geriye doğru arama bölgeleri barındıran tam olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a698c-210">Hosting hello reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="a698c-211">Bu makalede anlatıldığı gibi Azure DNS'de Hello geriye doğru arama bölgesi oluşturun, sonra ISS'niz ile çok çalışma[temsilci hello bölge](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-211">Create hello reverse lookup zone in Azure DNS as explained in this article, then work with your ISP too[delegate hello zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="a698c-212">Ardından hello PTR kayıtlarını yönetme aynı yolla diğer kayıt türleri hello her geriye doğru arama için.</span><span class="sxs-lookup"><span data-stu-id="a698c-212">You can then manage hello PTR records for each reverse lookup in hello same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="a698c-213">Ne kadar my ters DNS araması bölge maliyeti barındırma mu?</span><span class="sxs-lookup"><span data-stu-id="a698c-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="a698c-214">Azure DNS, ISS atanan IP Blok adresindeki doludur için hello geriye doğru DNS arama bölgesini barındıran [standart Azure DNS ücretler](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="a698c-214">Hosting hello reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="a698c-215">Azure DNS'de IPv4 ve IPv6 adresleri için geriye doğru DNS arama bölgeleri barındıran?</span><span class="sxs-lookup"><span data-stu-id="a698c-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="a698c-216">Evet.</span><span class="sxs-lookup"><span data-stu-id="a698c-216">Yes.</span></span> <span data-ttu-id="a698c-217">Bu makalede açıklanır nasıl toocreate IPv4 ve IPv6 geriye doğru DNS arama bölgeleri Azure DNS'de.</span><span class="sxs-lookup"><span data-stu-id="a698c-217">This article explains how toocreate both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="a698c-218">Varolan bir geriye doğru DNS araması bölge alabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="a698c-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="a698c-219">Evet.</span><span class="sxs-lookup"><span data-stu-id="a698c-219">Yes.</span></span> <span data-ttu-id="a698c-220">Azure DNS'yi hello Azure CLI tooimport var olan DNS bölgeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a698c-220">You can use hello Azure CLI tooimport existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="a698c-221">Bu, ileriye doğru arama bölgeleri ve geriye doğru arama bölgeleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="a698c-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="a698c-222">Daha fazla bilgi için bkz: [içeri ve dışarı aktarma bir DNS bölge dosyasını kullanarak hello Azure CLI](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-222">For more information, see [Import and export a DNS zone file using hello Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a698c-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a698c-223">Next steps</span></span>

<span data-ttu-id="a698c-224">Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="a698c-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="a698c-225">Nasıl çok öğrenin[, Azure Hizmetleri için ters DNS kayıtlarını yönetme](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="a698c-225">Learn how too[manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
