---
title: "Azure DNS'de DNS arama bölgeleri ters barındırma | Microsoft Docs"
description: "Azure DNS geriye doğru DNS arama bölgeleri IP aralıkları için barındırmak için kullanmayı öğrenin"
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
ms.openlocfilehash: 3e10b25d2f9b91c96af2958fef6dc6a4fdbff301
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="hosting-reverse-dns-lookup-zones-in-azure-dns"></a><span data-ttu-id="be424-103">Azure DNS geriye doğru DNS araması bölgelerinde barındırma</span><span class="sxs-lookup"><span data-stu-id="be424-103">Hosting reverse DNS lookup zones in Azure DNS</span></span>

<span data-ttu-id="be424-104">Bu makalede, Azure DNS'de, atanan IP aralıkları için geriye doğru DNS arama bölgeleri barındıran açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="be424-104">This article explains how to host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS.</span></span> <span data-ttu-id="be424-105">Geriye doğru arama bölgesi tarafından temsil edilen IP aralıkları, kuruluşunuz için genellikle ISS'niz tarafından atanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be424-105">The IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="be424-106">Azure Hizmetinize atanmış Azure ait IP adresi için ters DNS yapılandırmak için bkz: [Azure hizmetiniz için ayrılan IP adresleri için geriye doğru arama yapılandırma](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="be424-106">To configure reverse DNS for Azure-owned IP address assigned to your Azure service, see [configure the reverse lookup for the IP addresses allocated to your Azure service](dns-reverse-dns-for-azure-services.md).</span></span>

<span data-ttu-id="be424-107">Bu makalede okumadan önce bu bilgi sahibi olmanız [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be424-107">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="be424-108">Bu makalede, ilk geriye doğru arama DNS bölgesi oluşturma ve Azure portalı, Azure PowerShell, Azure CLI 1.0 veya Azure CLI 2.0 kullanarak kaydetmek için adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="be424-108">This article walks you through the steps to create your first reverse lookup DNS zone and record using the Azure portal, Azure PowerShell, Azure CLI 1.0 or Azure CLI 2.0.</span></span>

## <a name="create-a-reverse-lookup-dns-zone"></a><span data-ttu-id="be424-109">Geriye doğru arama DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="be424-109">Create a reverse lookup DNS zone</span></span>

1. <span data-ttu-id="be424-110">Oturum [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="be424-110">Sign in to the [Azure portal](https://portal.azure.com)</span></span>
1. <span data-ttu-id="be424-111">Hub menüsünde, tıklayıp **yeni** > **ağ** > ve ardından **DNS bölgesi** açmak için **oluşturma DNS bölgesi** Dikey.</span><span class="sxs-lookup"><span data-stu-id="be424-111">On the Hub menu, click and click **New** > **Networking** > and then click **DNS zone** to open the **Create DNS zone** blade.</span></span>

   ![DNS bölgesi](./media/dns-reverse-dns-hosting/figure1.png)

1. <span data-ttu-id="be424-113">Üzerinde **oluşturma DNS bölgesi** dikey penceresinde, DNS bölgenizi adı.</span><span class="sxs-lookup"><span data-stu-id="be424-113">On the **Create DNS zone** blade, name your DNS zone.</span></span> <span data-ttu-id="be424-114">Bölge adı farklı IPv4 ve IPv6 önekleri için hazırlanmış.</span><span class="sxs-lookup"><span data-stu-id="be424-114">The name of the zone is crafted differently for IPv4 and IPv6 prefixes.</span></span> <span data-ttu-id="be424-115">Her iki yönergelerini kullanın [IPv4](#ipv4) veya [IPv6](#ipv6) bölgenizi adlandırın.</span><span class="sxs-lookup"><span data-stu-id="be424-115">Use either the instructions for [IPV4](#ipv4) or [IPv6](#ipv6) to name your zone.</span></span> <span data-ttu-id="be424-116">Tıklatın tamamlandığında **oluşturma** bölgesi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="be424-116">When complete click **Create** to create the zone.</span></span>

### <a name="ipv4"></a><span data-ttu-id="be424-117">IPv4</span><span class="sxs-lookup"><span data-stu-id="be424-117">IPv4</span></span>

<span data-ttu-id="be424-118">Bir IPv4 geriye doğru arama bölgesi adı temsil ettiği IP aralığına dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="be424-118">The name of an IPv4 reverse lookup zone is based on the IP range it represents.</span></span> <span data-ttu-id="be424-119">Şu biçimde olmalıdır: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="be424-119">It should be in the following format: `<IPv4 network prefix in reverse order>.in-addr.arpa`.</span></span> <span data-ttu-id="be424-120">Örnekler için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md#ipv4).</span><span class="sxs-lookup"><span data-stu-id="be424-120">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv4).</span></span>

> [!NOTE]
> <span data-ttu-id="be424-121">Azure DNS'de Sınıfsız geriye doğru DNS arama bölgeleri oluştururken, kısa çizgi kullanmanız gerekir (`-`) yerine eğik çizgi ('/ ') bölge adı.</span><span class="sxs-lookup"><span data-stu-id="be424-121">When creating classless reverse DNS lookup zones in Azure DNS, you must use a hyphen (`-`) rather than a forward slash ('/') in the zone name.</span></span>
>
> <span data-ttu-id="be424-122">Örneğin, IP aralığı 192.0.2.128/26 için kullanmanız gerekir `128-26.2.0.192.in-addr.arpa` yerine bölge adı olarak `128/26.2.0.192.in-addr.arpa`.</span><span class="sxs-lookup"><span data-stu-id="be424-122">For example, for the IP range 192.0.2.128/26, you must use `128-26.2.0.192.in-addr.arpa` as the zone name instead of `128/26.2.0.192.in-addr.arpa`.</span></span>
>
> <span data-ttu-id="be424-123">Her ikisi de DNS standartları tarafından desteklenir, ancak eğik içeren adlara DNS bölgesi, bunun nedeni (`/`) karakter Azure DNS'de desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="be424-123">This is because, while both are supported by the DNS standards, DNS zone names containing the forward slash (`/`) character are not supported in Azure DNS.</span></span>

<span data-ttu-id="be424-124">Aşağıdaki örnek adlı bir 'C sınıfı' geriye doğru DNS bölgesi oluşturmak nasıl gösterir `2.0.192.in-addr.arpa` Azure Portalı aracılığıyla Azure DNS'de:</span><span class="sxs-lookup"><span data-stu-id="be424-124">The following example shows how to create a 'Class C' reverse DNS zone named `2.0.192.in-addr.arpa` in Azure DNS via the Azure portal:</span></span>

 ![DNS bölgesi oluşturma](./media/dns-reverse-dns-hosting/figure2.png)

<span data-ttu-id="be424-126">'Kaynak grubu konumu' kaynak grubu için konum tanımlar ve DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="be424-126">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="be424-127">DNS bölge konumu her zaman 'global' dır ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="be424-127">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="be424-128">Aşağıdaki örnekler, Azure PowerShell ve Azure CLI bu görevi tamamlamak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="be424-128">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="be424-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be424-129">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="be424-130">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be424-130">Azure CLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="be424-131">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be424-131">Azure CLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="be424-132">IPv6</span><span class="sxs-lookup"><span data-stu-id="be424-132">IPv6</span></span>

<span data-ttu-id="be424-133">Bir IPv6 geriye doğru arama bölgesi adı şu biçimde olmalıdır: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span><span class="sxs-lookup"><span data-stu-id="be424-133">The name of an IPv6 reverse lookup zone should be in the following form: `<IPv6 network prefix in reverse order>.ip6.arpa`.</span></span>  <span data-ttu-id="be424-134">Örnekler için bkz: [geriye doğru DNS ve Azure desteği'na genel bakış](dns-reverse-dns-overview.md#ipv6).</span><span class="sxs-lookup"><span data-stu-id="be424-134">For examples, see [overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md#ipv6).</span></span>


<span data-ttu-id="be424-135">Aşağıdaki örnek adlı bir IPv6 geriye doğru DNS arama bölgesi oluşturmak nasıl gösterir `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` Azure Portalı aracılığıyla Azure DNS'de:</span><span class="sxs-lookup"><span data-stu-id="be424-135">The following example shows how to create an IPv6 reverse DNS lookup zone named `0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa` in Azure DNS via the Azure portal:</span></span>

 ![DNS bölgesi oluşturma](./media/dns-reverse-dns-hosting/figure3.png)

<span data-ttu-id="be424-137">'Kaynak grubu konumu' kaynak grubu için konum tanımlar ve DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="be424-137">The 'Resource group location' defines the location for the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="be424-138">DNS bölge konumu her zaman 'global' dır ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="be424-138">The DNS zone location is always 'global', and is not shown.</span></span>

<span data-ttu-id="be424-139">Aşağıdaki örnekler, Azure PowerShell ve Azure CLI bu görevi tamamlamak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="be424-139">The following examples show how to complete this task with Azure PowerShell and the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="be424-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be424-140">PowerShell</span></span>

```powershell
New-AzureRmDnsZone -Name 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azurecli-10"></a><span data-ttu-id="be424-141">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be424-141">AzureCLI 1.0</span></span>

```azurecli
azure network dns zone create MyResourceGroup 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azurecli-20"></a><span data-ttu-id="be424-142">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be424-142">AzureCLI 2.0</span></span>

```azurecli
az network dns zone create -g MyResourceGroup -n 0.0.0.0.d.c.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="delegate-a-reverse-dns-lookup-zone"></a><span data-ttu-id="be424-143">DNS geriye doğru arama bölgesini temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="be424-143">Delegate a reverse DNS lookup zone</span></span>

<span data-ttu-id="be424-144">Geriye doğru DNS araması bölgenizi oluşturduktan, bölge üst bölgeden bir temsilci emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="be424-144">Having created your reverse DNS lookup zone, you must ensure that the zone is delegated from the parent zone.</span></span> <span data-ttu-id="be424-145">DNS temsilcisi, geriye doğru DNS arama bölgesini barındıran ad sunucularını bulmak DNS ad çözümleme işlemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="be424-145">DNS delegation enables the DNS name resolution process to find the name servers hosting your reverse DNS lookup zone.</span></span> <span data-ttu-id="be424-146">Bu, adres aralığındaki IP adresleri için geriye doğru DNS sorgularını yanıtlamak bu ad sunucuları sağlar.</span><span class="sxs-lookup"><span data-stu-id="be424-146">This enables those name servers to answer DNS reverse queries for the IP addresses in your address range.</span></span>

<span data-ttu-id="be424-147">Bir DNS bölgesi için temsilci seçme işleminin açıklanan ileriye doğru arama bölgeleri için [etki alanınızı Azure DNS'ye temsilci](dns-delegate-domain-azure-dns.md).</span><span class="sxs-lookup"><span data-stu-id="be424-147">For forward lookup zones, the process of delegating a DNS zone is described in [Delegate your domain to Azure DNS](dns-delegate-domain-azure-dns.md).</span></span> <span data-ttu-id="be424-148">Geriye doğru arama bölgeleri için temsilci seçme aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="be424-148">Delegation for reverse lookup zones works the same way.</span></span> <span data-ttu-id="be424-149">Tek fark, ad sunucuları, etki alanı adı kayıt yerine IP aralığınızı sağlanan ISS ile yapılandırmanız gerekiyor ' dir.</span><span class="sxs-lookup"><span data-stu-id="be424-149">The only difference is that you need to configure the name servers with the ISP who provided your IP range, rather than your domain name registrar.</span></span>

## <a name="create-a-dns-ptr-record"></a><span data-ttu-id="be424-150">Bir DNS PTR kaydı oluştur</span><span class="sxs-lookup"><span data-stu-id="be424-150">Create a DNS PTR record</span></span>

### <a name="ipv4"></a><span data-ttu-id="be424-151">IPv4</span><span class="sxs-lookup"><span data-stu-id="be424-151">IPv4</span></span>

<span data-ttu-id="be424-152">Aşağıdaki örnek, bir geriye doğru DNS bölgesinde Azure DNS PTR kaydı oluşturma işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="be424-152">The following example walks you through the process of creating a PTR record in a reverse DNS zone in Azure DNS.</span></span> <span data-ttu-id="be424-153">Diğer kayıt türleri ve var olan kayıtların değiştirilmesi hakkında bilgi için bkz. [Azure portalı kullanarak DNS kayıtlarını ve kayıt kümelerini yönetme](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be424-153">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1.  <span data-ttu-id="be424-154">**DNS bölgesi** dikey penceresinin üzerindeki **+ Kayıt kümesi**’ni seçerek **Kayıt kümesi ekle** dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="be424-154">At the top of the **DNS zone** blade, select **+ Record set** to open the **Add record set** blade.</span></span>

 ![DNS bölgesi](./media/dns-reverse-dns-hosting/figure4.png)

1. <span data-ttu-id="be424-156">Üzerinde **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="be424-156">On the **Add record set** blade.</span></span> 
1. <span data-ttu-id="be424-157">Seçin **PTR** kayıttan "**türü**" menüsü.</span><span class="sxs-lookup"><span data-stu-id="be424-157">Select **PTR** from the record "**Type**" menu.</span></span>  
1. <span data-ttu-id="be424-158">Kayıt için bir PTR kayıt kümesi adını IPv4 adresi kalan ters sırada olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be424-158">The name of the record set for a PTR record needs to be the rest of the IPv4 address in reverse order.</span></span> <span data-ttu-id="be424-159">Bu örnekte, ilk üç sekizlisinin bölge adı (.2.0.192) bir parçası olarak önceden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="be424-159">In this example, the first three octets are already populated as part of the zone name (.2.0.192).</span></span> <span data-ttu-id="be424-160">Bu nedenle, yalnızca son sekizli ad alanında sağlanır.</span><span class="sxs-lookup"><span data-stu-id="be424-160">Therefore, only the last octet is supplied in the name field.</span></span> <span data-ttu-id="be424-161">Örneğin, kayıt kümenizi adlandırabilirsiniz "**15**", IP adresi 192.0.2.15 olan bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="be424-161">For example, you could name your record set "**15**" for a resource whose IP address is 192.0.2.15.</span></span>  
1. <span data-ttu-id="be424-162">İçindeki "**etki alanı adı**" alanı, IP kullanarak kaynak tam etki alanı adı (FQDN) girin.</span><span class="sxs-lookup"><span data-stu-id="be424-162">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
1. <span data-ttu-id="be424-163">DNS kaydını oluşturmak için dikey pencerenin altındaki **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="be424-163">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

 ![kayıt kümesi Ekle](./media/dns-reverse-dns-hosting/figure5.png)

<span data-ttu-id="be424-165">Bu görev, PowerShell ve AzureCLI tamamlamak hakkında örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="be424-165">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="be424-166">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be424-166">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name 15 -RecordType PTR -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc1.contoso.com")
```
#### <a name="azurecli-10"></a><span data-ttu-id="be424-167">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be424-167">AzureCLI 1.0</span></span>

```azurecli
azure network dns record-set add-record MyResourceGroup 2.0.192.in-addr.arpa 15 PTR --ptrdname dc1.contoso.com  
```

#### <a name="azurecli-20"></a><span data-ttu-id="be424-168">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be424-168">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 2.0.192.in-addr.arpa -n 15 --ptrdname dc1.contoso.com
```

### <a name="ipv6"></a><span data-ttu-id="be424-169">IPv6</span><span class="sxs-lookup"><span data-stu-id="be424-169">IPv6</span></span>

<span data-ttu-id="be424-170">Aşağıdaki örnek yeni bir 'PTR' kayıt oluşturma sürecinde yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="be424-170">The following example walks you through the process of creating new 'PTR' record.</span></span> <span data-ttu-id="be424-171">Diğer kayıt türleri ve var olan kayıtların değiştirilmesi hakkında bilgi için bkz. [Azure portalı kullanarak DNS kayıtlarını ve kayıt kümelerini yönetme](dns-operations-recordsets-portal.md).</span><span class="sxs-lookup"><span data-stu-id="be424-171">For other record types and to modify existing records, see [Manage DNS records and record sets by using the Azure portal](dns-operations-recordsets-portal.md).</span></span>

1. <span data-ttu-id="be424-172">Üstündeki **DNS bölge dikey**seçin **+ kayıt kümesine** açmak için **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="be424-172">At the top of the **DNS zone blade**, select **+ Record set** to open the **Add record set** blade.</span></span>

  ![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure6.png)

2. <span data-ttu-id="be424-174">Üzerinde **kayıt kümesi ekleme** dikey.</span><span class="sxs-lookup"><span data-stu-id="be424-174">On the **Add record set** blade.</span></span> 
3. <span data-ttu-id="be424-175">Seçin **PTR** kayıttan "**türü**" menüsü.</span><span class="sxs-lookup"><span data-stu-id="be424-175">Select **PTR** from the record "**Type**" menu.</span></span>  
4. <span data-ttu-id="be424-176">Kayıt için bir PTR kayıt kümesi adını rest IPv6 adresinin ters sırada olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="be424-176">The name of the record set for a PTR record needs to be the rest of the IPv6 address in reverse order.</span></span> <span data-ttu-id="be424-177">Sıfır sıkıştırma eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="be424-177">It must not include any zero compression.</span></span> <span data-ttu-id="be424-178">Bu örnekte, ilk 64 bit IPv6 bölge adı (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa) bir parçası olarak önceden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="be424-178">In this example, the first 64 bits of the IPv6 are already populated as part of the zone name (0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa).</span></span> <span data-ttu-id="be424-179">Bu nedenle, yalnızca son 64 bitlik ad alanında verilir.</span><span class="sxs-lookup"><span data-stu-id="be424-179">Therefore, only the last 64 bits are supplied in the name field.</span></span> <span data-ttu-id="be424-180">Son 64 bit IP adresinin ters sırada bir süre her onaltılık sayı bölücüyü kullanarak girilir.</span><span class="sxs-lookup"><span data-stu-id="be424-180">The last 64 bits of the IP address are entered in reverse order, using a period as the delimiter between each hexadecimal number.</span></span> <span data-ttu-id="be424-181">Örneğin, kayıt kümenizi adlandırabilirsiniz "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**", IP adresi 2001:0db8:abdc:0000:f524:10bc:1af9:405e olan bir kaynak için.</span><span class="sxs-lookup"><span data-stu-id="be424-181">For example, you could name your record set "**e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f**" for a resource whose IP address is 2001:0db8:abdc:0000:f524:10bc:1af9:405e.</span></span>  
5. <span data-ttu-id="be424-182">İçindeki "**etki alanı adı**" alanı, IP kullanarak kaynak tam etki alanı adı (FQDN) girin.</span><span class="sxs-lookup"><span data-stu-id="be424-182">In the "**Domain Name**" field, enter the fully qualified domain name (FQDN) of the resource using the IP.</span></span>
6. <span data-ttu-id="be424-183">DNS kaydını oluşturmak için dikey pencerenin altındaki **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="be424-183">Select **OK** at the bottom of the blade to create the DNS record.</span></span>

![kayıt kümesi dikey ekleme](./media/dns-reverse-dns-hosting/figure7.png)

<span data-ttu-id="be424-185">Bu görev, PowerShell ve AzureCLI tamamlamak hakkında örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="be424-185">The following are examples on how to complete this task with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="be424-186">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be424-186">PowerShell</span></span>

```powershell
New-AzureRmDnsRecordSet -Name "e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f" -RecordType PTR -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup -Ttl 3600 -DnsRecords (New-AzureRmDnsRecordConfig -Ptrdname "dc2.contoso.com")
```

#### <a name="azurecli-10"></a><span data-ttu-id="be424-187">AzureCLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be424-187">AzureCLI 1.0</span></span>

```
azure network dns record-set add-record MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f PTR --ptrdname dc2.contoso.com 
```
 
#### <a name="azurecli-20"></a><span data-ttu-id="be424-188">AzureCLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be424-188">AzureCLI 2.0</span></span>

```azurecli
    az network dns record-set ptr add-record -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -n e.5.0.4.9.f.a.1.c.b.0.1.4.2.5.f --ptrdname dc2.contoso.com
```

## <a name="view-records"></a><span data-ttu-id="be424-189">Kayıtları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="be424-189">View Records</span></span>

<span data-ttu-id="be424-190">Oluşturduğunuz kayıtları görüntülemek için DNS bölgenizi Azure portalında gidin.</span><span class="sxs-lookup"><span data-stu-id="be424-190">To view the records you created, navigate to your DNS zone in the Azure portal.</span></span> <span data-ttu-id="be424-191">Alt kısmında **DNS bölgesi** dikey penceresinde, DNS bölgesi için kayıt görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be424-191">In the lower part of the **DNS zone** blade, you can see the records for the DNS zone.</span></span> <span data-ttu-id="be424-192">Her bölgede oluşturulan varsayılan NS ve SOA kayıtlarının yanı sıra, oluşturduğunuz tüm kayıtları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="be424-192">You should see the default NS and SOA records, which are created in every zone, plus any new records you have created.</span></span>

### <a name="ipv4"></a><span data-ttu-id="be424-193">IPv4</span><span class="sxs-lookup"><span data-stu-id="be424-193">IPv4</span></span>

<span data-ttu-id="be424-194">IPv4 PTR kayıtları gösteren DNS bölge dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="be424-194">DNS zone blade, showing IPv4 PTR records:</span></span>

![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure8.png)

<span data-ttu-id="be424-196">Aşağıdaki örnekler, PowerShell veya Azure CLI kullanarak PTR kayıtları görüntülemek nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="be424-196">The following examples show how to view the PTR records using PowerShell or the Azure CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="be424-197">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be424-197">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 2.0.192.in-addr.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="be424-198">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be424-198">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 2.0.192.in-addr.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="be424-199">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be424-199">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 2.0.192.in-addr.arpa
```

### <a name="ipv6"></a><span data-ttu-id="be424-200">IPv6</span><span class="sxs-lookup"><span data-stu-id="be424-200">IPv6</span></span>

<span data-ttu-id="be424-201">IPv6 PTR kayıtları gösteren DNS bölge dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="be424-201">DNS zone blade, showing IPv6 PTR records:</span></span>

![DNS bölge dikey penceresi](./media/dns-reverse-dns-hosting/figure9.png)

<span data-ttu-id="be424-203">PowerShell ve AzureCLI kayıtları görüntülemek nasıl örnekleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="be424-203">The following are examples on how to view the records with PowerShell and the AzureCLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="be424-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be424-204">PowerShell</span></span>

```powershell
Get-AzureRmDnsRecordSet -ZoneName 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa -ResourceGroupName MyResourceGroup
```

#### <a name="azure-cli-10"></a><span data-ttu-id="be424-205">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="be424-205">Azure CLI 1.0</span></span>

```azurecli
    azure network dns record-set list MyResourceGroup 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

#### <a name="azure-cli-20"></a><span data-ttu-id="be424-206">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be424-206">Azure CLI 2.0</span></span>

```azurecli
    azure network dns record-set list -g MyResourceGroup -z 0.0.0.0.c.d.b.a.8.b.d.0.1.0.0.2.ip6.arpa
```

## <a name="faq"></a><span data-ttu-id="be424-207">SSS</span><span class="sxs-lookup"><span data-stu-id="be424-207">FAQ</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-my-isp-assigned-ip-blocks-on-azure-dns"></a><span data-ttu-id="be424-208">Geriye doğru DNS arama bölgeleri my ISS atanan IP blokları Azure DNS üzerinde barındırabilir?</span><span class="sxs-lookup"><span data-stu-id="be424-208">Can I host reverse DNS lookup zones for my ISP-assigned IP blocks on Azure DNS?</span></span>

<span data-ttu-id="be424-209">Evet.</span><span class="sxs-lookup"><span data-stu-id="be424-209">Yes.</span></span> <span data-ttu-id="be424-210">Azure DNS'de kendi IP aralıkları için (ARPA) geriye doğru arama bölgeleri barındıran tam olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="be424-210">Hosting the reverse lookup (ARPA) zones for your own IP ranges in Azure DNS is fully supported.</span></span>

<span data-ttu-id="be424-211">Bu makalede anlatıldığı gibi Azure DNS geriye doğru arama bölgesi oluşturun, sonra Internet servis Sağlayıcınıza ile çalışırsınız [bölgeye temsilci](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="be424-211">Create the reverse lookup zone in Azure DNS as explained in this article, then work with your ISP to [delegate the zone](dns-domain-delegation.md).</span></span>  <span data-ttu-id="be424-212">Daha sonra PTR kayıtları her geriye doğru arama için diğer kayıt türleri aynı şekilde yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be424-212">You can then manage the PTR records for each reverse lookup in the same way as other record types.</span></span>

### <a name="how-much-does-hosting-my-reverse-dns-lookup-zone-cost"></a><span data-ttu-id="be424-213">Ne kadar my ters DNS araması bölge maliyeti barındırma mu?</span><span class="sxs-lookup"><span data-stu-id="be424-213">How much does hosting my reverse DNS lookup zone cost?</span></span>

<span data-ttu-id="be424-214">Azure DNS, ISS atanan IP Blok adresindeki doludur için geriye doğru DNS arama bölgesini barındıran [standart Azure DNS ücretler](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="be424-214">Hosting the reverse DNS lookup zone for your ISP-assigned IP block in Azure DNS is charged at [standard Azure DNS rates](https://azure.microsoft.com/pricing/details/dns/).</span></span>

### <a name="can-i-host-reverse-dns-lookup-zones-for-both-ipv4-and-ipv6-addresses-in-azure-dns"></a><span data-ttu-id="be424-215">Azure DNS'de IPv4 ve IPv6 adresleri için geriye doğru DNS arama bölgeleri barındıran?</span><span class="sxs-lookup"><span data-stu-id="be424-215">Can I host reverse DNS lookup zones for both IPv4 and IPv6 addresses in Azure DNS?</span></span>

<span data-ttu-id="be424-216">Evet.</span><span class="sxs-lookup"><span data-stu-id="be424-216">Yes.</span></span> <span data-ttu-id="be424-217">Bu makalede, Azure DNS'de hem IPv4 hem de IPv6 geriye doğru DNS arama bölgeleri oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="be424-217">This article explains how to create both IPv4 and IPv6 reverse DNS lookup zones in Azure DNS.</span></span>

### <a name="can-i-import-an-existing-reverse-dns-lookup-zone"></a><span data-ttu-id="be424-218">Varolan bir geriye doğru DNS araması bölge alabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="be424-218">Can I import an existing reverse DNS lookup zone?</span></span>

<span data-ttu-id="be424-219">Evet.</span><span class="sxs-lookup"><span data-stu-id="be424-219">Yes.</span></span> <span data-ttu-id="be424-220">Azure CLI, var olan DNS bölgeleri Azure DNS aktarmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be424-220">You can use the Azure CLI to import existing DNS zones into Azure DNS.</span></span> <span data-ttu-id="be424-221">Bu, ileriye doğru arama bölgeleri ve geriye doğru arama bölgeleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="be424-221">This works for both forward lookup zones and reverse lookup zones.</span></span>

<span data-ttu-id="be424-222">Daha fazla bilgi için bkz: [içeri ve dışarı aktarma Azure CLI kullanarak bir DNS bölge dosyasına](dns-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="be424-222">For more information, see [Import and export a DNS zone file using the Azure CLI](dns-import-export.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="be424-223">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be424-223">Next steps</span></span>

<span data-ttu-id="be424-224">Geriye doğru DNS hakkında daha fazla bilgi için bkz: [wikipedia'da ters DNS araması](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="be424-224">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="be424-225">Bilgi edinmek için nasıl [, Azure Hizmetleri için ters DNS kayıtlarını yönetme](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="be424-225">Learn how to [manage reverse DNS records for your Azure services](dns-reverse-dns-for-azure-services.md).</span></span>
