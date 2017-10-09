---
title: "aaaDelegate, DNS etki alanı tooAzure | Microsoft Docs"
description: "Nasıl toochange etki alanı temsilcisi kullanımı Azure DNS etki alanı tooprovide barındıran sunucu adı ve anlayın."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 257da6ec-d6e2-4b6f-ad76-ee2dde4efbcc
ms.service: dns
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: gwallace
ms.openlocfilehash: f780bdaa416150e5e3afe6c6845dc75ba54b6203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-a-domain-tooazure-dns"></a><span data-ttu-id="84f61-103">Bir etki alanı tooAzure DNS temsilci seçme</span><span class="sxs-lookup"><span data-stu-id="84f61-103">Delegate a domain tooAzure DNS</span></span>

<span data-ttu-id="84f61-104">Azure DNS toohost bir DNS bölgesi sağlar ve azure'de bir etki alanı için DNS kayıtlarını hello yönetin.</span><span class="sxs-lookup"><span data-stu-id="84f61-104">Azure DNS allows you toohost a DNS zone and manage hello DNS records for a domain in Azure.</span></span> <span data-ttu-id="84f61-105">Bir etki alanı tooreach Azure DNS için DNS sorgularını sırayla hello etki alanı toobe sahip hello üst etki alanından tooAzure DNS temsilcisi.</span><span class="sxs-lookup"><span data-stu-id="84f61-105">In order for DNS queries for a domain tooreach Azure DNS, hello domain has toobe delegated tooAzure DNS from hello parent domain.</span></span> <span data-ttu-id="84f61-106">Azure DNS unutmayın hello etki alanı kayıt değil.</span><span class="sxs-lookup"><span data-stu-id="84f61-106">Keep in mind Azure DNS is not hello domain registrar.</span></span> <span data-ttu-id="84f61-107">Bu makalede açıklanır nasıl toodelegate, DNS etki alanı tooAzure.</span><span class="sxs-lookup"><span data-stu-id="84f61-107">This article explains how toodelegate your domain tooAzure DNS.</span></span>

<span data-ttu-id="84f61-108">Bir kayıt şirketinden satın alınan etki alanları için kayıt şirketiniz bu NS kayıtlarını ayarlama seçeneğini tooset hello sunar.</span><span class="sxs-lookup"><span data-stu-id="84f61-108">For domains purchased from a registrar, your registrar offers hello option tooset up these NS records.</span></span> <span data-ttu-id="84f61-109">Bir etki alanı toocreate bu etki alanı adı ile bir DNS bölgesi durum Azure DNS'de tooown gerekmez.</span><span class="sxs-lookup"><span data-stu-id="84f61-109">You do not have tooown a domain toocreate a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="84f61-110">Ancak, tooown hello etki alanı tooset hello temsilci tooAzure DNS yukarı hello kayıt şirketinizle gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f61-110">However, you do need tooown hello domain tooset up hello delegation tooAzure DNS with hello registrar.</span></span>

<span data-ttu-id="84f61-111">Örneğin, 'contoso.net' hello etki alanı satın alın ve Azure DNS'de hello adı 'contoso.net' ile bir bölge oluşturmanız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="84f61-111">For example, suppose you purchase hello domain 'contoso.net' and create a zone with hello name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="84f61-112">Merhaba etki alanının Hello sahibi olarak, etki alanınız için seçenek tooconfigure hello ad sunucusu adreslerini (yani, hello NS kayıtları) hello kayıt sunar.</span><span class="sxs-lookup"><span data-stu-id="84f61-112">As hello owner of hello domain, your registrar offers you hello option tooconfigure hello name server addresses (that is, hello NS records) for your domain.</span></span> <span data-ttu-id="84f61-113">Merhaba kayıt şirketi bu NS kayıtlarını bu durumda '.net' hello üst etki alanında depolar.</span><span class="sxs-lookup"><span data-stu-id="84f61-113">hello registrar stores these NS records in hello parent domain, in this case '.net'.</span></span> <span data-ttu-id="84f61-114">Merhaba Dünya istemciler, ardından 'contoso.net' tooresolve DNS kayıtlarını çalışırken Azure DNS bölgesindeki yönlendirilmiş tooyour etki alanı olabilir.</span><span class="sxs-lookup"><span data-stu-id="84f61-114">Clients around hello world can then be directed tooyour domain in Azure DNS zone when trying tooresolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="84f61-115">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f61-115">Create a DNS zone</span></span>

1. <span data-ttu-id="84f61-116">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="84f61-116">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="84f61-117">Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.</span><span class="sxs-lookup"><span data-stu-id="84f61-117">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS bölgesi](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="84f61-119">Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="84f61-119">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="84f61-120">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="84f61-120">**Setting**</span></span> | <span data-ttu-id="84f61-121">**Değer**</span><span class="sxs-lookup"><span data-stu-id="84f61-121">**Value**</span></span> | <span data-ttu-id="84f61-122">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="84f61-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="84f61-123">**Ad**</span><span class="sxs-lookup"><span data-stu-id="84f61-123">**Name**</span></span>|<span data-ttu-id="84f61-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="84f61-124">contoso.net</span></span>|<span data-ttu-id="84f61-125">Merhaba DNS bölgesinin Hello adı</span><span class="sxs-lookup"><span data-stu-id="84f61-125">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="84f61-126">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="84f61-126">**Subscription**</span></span>|<span data-ttu-id="84f61-127">[Aboneliğiniz]</span><span class="sxs-lookup"><span data-stu-id="84f61-127">[Your subscription]</span></span>|<span data-ttu-id="84f61-128">Bir abonelik toocreate hello uygulama ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="84f61-128">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="84f61-129">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="84f61-129">**Resource group**</span></span>|<span data-ttu-id="84f61-130">**Yeni oluştur:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="84f61-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="84f61-131">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84f61-131">Create a resource group.</span></span> <span data-ttu-id="84f61-132">Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="84f61-132">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="84f61-133">Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.</span><span class="sxs-lookup"><span data-stu-id="84f61-133">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="84f61-134">**Konum**</span><span class="sxs-lookup"><span data-stu-id="84f61-134">**Location**</span></span>|<span data-ttu-id="84f61-135">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="84f61-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="84f61-136">Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="84f61-136">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="84f61-137">Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="84f61-137">hello DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="84f61-138">Ad sunucularını alma</span><span class="sxs-lookup"><span data-stu-id="84f61-138">Retrieve name servers</span></span>

<span data-ttu-id="84f61-139">DNS bölge tooAzure DNS temsilci önce ilk tooknow hello ad sunucusu adlarını bölgenizin gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f61-139">Before you can delegate your DNS zone tooAzure DNS, you first need tooknow hello name server names for your zone.</span></span> <span data-ttu-id="84f61-140">Azure DNS, her bölge oluşturmada bir havuzdan ad sunucuları ayırır.</span><span class="sxs-lookup"><span data-stu-id="84f61-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="84f61-141">Oluşturulan, hello Azure portal hello DNS bölgesine **Sık Kullanılanlar** bölmesinde, tıklatın **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="84f61-141">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="84f61-142">Merhaba tıklatın **contoso.net** hello DNS bölgesinde **tüm kaynakları** dikey.</span><span class="sxs-lookup"><span data-stu-id="84f61-142">Click hello **contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="84f61-143">Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **contoso.net** adına göre filtre hello içinde...</span><span class="sxs-lookup"><span data-stu-id="84f61-143">If hello subscription you selected already has several resources in it, you can enter **contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="84f61-144">kutusunu tooeasily erişim hello uygulama ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="84f61-144">box tooeasily access hello application gateway.</span></span> 

1. <span data-ttu-id="84f61-145">Merhaba ad sunucuları hello DNS bölgesine dikey penceresinden alır.</span><span class="sxs-lookup"><span data-stu-id="84f61-145">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="84f61-146">Bu örnekte 'contoso.net' hello bölge ad sunucuları atanmıştır ' ns1-01.azure-dns.com', 'ns2-01.azure-DNS.NET', ' ns3-01.azure-dns.org', ve ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="84f61-146">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="84f61-148">Azure DNS, bölgenizi hello atanan ad sunucularını içeren yetkili NS kayıtları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84f61-148">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="84f61-149">Azure PowerShell veya Azure CLI toosee hello ad sunucusu adlarını, tooretrieve bu kayıtları yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="84f61-149">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

<span data-ttu-id="84f61-150">Merhaba aşağıdaki örneklerde ayrıca hello adımlar tooretrieve hello ad sunucuları, PowerShell ve Azure CLI Azure DNS'de bölge sağlar.</span><span class="sxs-lookup"><span data-stu-id="84f61-150">hello following examples also provide hello steps tooretrieve hello name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="84f61-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f61-151">PowerShell</span></span>

```powershell
# hello record name "@" is used toorefer toorecords at hello top of hello zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="84f61-152">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="84f61-152">hello following example is hello response.</span></span>

```
Name              : @
ZoneName          : contoso.net
ResourceGroupName : contosorg
Ttl               : 172800
Etag              : 03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5
RecordType        : NS
Records           : {ns1-07.azure-dns.com., ns2-07.azure-dns.net., ns3-07.azure-dns.org.,
                    ns4-07.azure-dns.info.}
Metadata          :
```

### <a name="azure-cli"></a><span data-ttu-id="84f61-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84f61-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="84f61-154">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="84f61-154">hello following example is hello response.</span></span>

```json
{
  "etag": "03bff8f1-9c60-4a9b-ad9d-ac97366ee4d5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosoRG/providers/Microsoft.Network/dnszones/contoso.net/NS/@",
  "metadata": null,
  "name": "@",
  "nsRecords": [
    {
      "nsdname": "ns1-07.azure-dns.com."
    },
    {
      "nsdname": "ns2-07.azure-dns.net."
    },
    {
      "nsdname": "ns3-07.azure-dns.org."
    },
    {
      "nsdname": "ns4-07.azure-dns.info."
    }
  ],
  "resourceGroup": "contosoRG",
  "ttl": 172800,
  "type": "Microsoft.Network/dnszones/NS"
}
```

## <a name="delegate-hello-domain"></a><span data-ttu-id="84f61-155">Temsilci hello etki alanı</span><span class="sxs-lookup"><span data-stu-id="84f61-155">Delegate hello domain</span></span>

<span data-ttu-id="84f61-156">Merhaba DNS bölgesi oluşturulur ve hello ad sunucuları sahip olduğunuza hello üst etki alanı hello Azure DNS ad sunucuları ile güncelleştirilmiş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f61-156">Now that hello DNS zone is created and you have hello name servers, hello parent domain needs toobe updated with hello Azure DNS name servers.</span></span> <span data-ttu-id="84f61-157">Her kayıt şirketi kendi DNS Yönetim Araçları toochange hello ad sunucusu kayıtları etki alanı var.</span><span class="sxs-lookup"><span data-stu-id="84f61-157">Each registrar has their own DNS management tools toochange hello name server records for a domain.</span></span> <span data-ttu-id="84f61-158">Merhaba kayıt şirketinizin DNS Yönetim sayfasında, hello NS kayıtlarını düzenleyin ve hello NS kayıtlarını Azure DNS oluşturulan hello olanları ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="84f61-158">In hello registrar's DNS management page, edit hello NS records and replace hello NS records with hello ones Azure DNS created.</span></span>

<span data-ttu-id="84f61-159">Bir etki alanı tooAzure DNS devrederken Azure DNS tarafından sağlanan hello ad sunucusu adlarını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f61-159">When delegating a domain tooAzure DNS, you must use hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="84f61-160">Tüm toouse önerilen dört sunucu adları, etki alanınızın adını hello bağımsız olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="84f61-160">It is recommended toouse all four name server names, regardless of hello name of your domain.</span></span> <span data-ttu-id="84f61-161">Etki alanı temsilcisi hello adını sunucu adı toouse gerektirmez hello etki alanınız aynı üst düzey etki alanı.</span><span class="sxs-lookup"><span data-stu-id="84f61-161">Domain delegation does not require hello name server name toouse hello same top-level domain as your domain.</span></span>

<span data-ttu-id="84f61-162">Bu IP adresleri gelecekte değişebileceği ederken "Birleştirici kayıtlar' toopoint toohello Azure DNS ad sunucusu IP adreslerini, kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f61-162">You should not use 'glue records' toopoint toohello Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="84f61-163">Kendi bölgenizdeki ad sunucusu adlarını kullanan ve bazen "gösterim ad sunucuları" olarak adlandırılan temsilci seçimleri, Azure DNS'de şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="84f61-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="84f61-164">Ad çözümlemesinin çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="84f61-164">Verify name resolution is working</span></span>

<span data-ttu-id="84f61-165">Merhaba temsilci seçmeyi tamamladıktan sonra ad çözümlemesi (Merhaba bölge oluşturulduğunda bu da otomatik olarak oluşturulur), bölgenin SOA kaydına 'nslookup' tooquery hello gibi bir araç kullanarak çalıştığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84f61-165">After completing hello delegation, you can verify that name resolution is working by using a tool such as 'nslookup' tooquery hello SOA record for your zone (which is also automatically created when hello zone is created).</span></span>

<span data-ttu-id="84f61-166">Merhaba temsilci doğru hello normal DNS çözümleme işlemi ayarlarsanız hello ad sunucuları otomatik olarak bulur, toospecify hello Azure DNS ad sunucuları sahip.</span><span class="sxs-lookup"><span data-stu-id="84f61-166">You do not have toospecify hello Azure DNS name servers, if hello delegation has been set up correctly, hello normal DNS resolution process finds hello name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="84f61-167">Merhaba, hello komutu önceki örnek yanıttan aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="84f61-167">hello following is an example response from hello preceding command:</span></span>

```
Server: ns1-04.azure-dns.com
Address: 208.76.47.4

contoso.com
primary name server = ns1-04.azure-dns.com
responsible mail addr = msnhst.microsoft.com
serial = 1
refresh = 900 (15 mins)
retry = 300 (5 mins)
expire = 604800 (7 days)
default TTL = 300 (5 mins)
```

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="84f61-168">Azure DNS'de alt etki alanlarını devretme</span><span class="sxs-lookup"><span data-stu-id="84f61-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="84f61-169">Tooset ayrı bir alt bölge kurmak istiyorsanız Azure DNS'de bir alt etki alanını devredebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84f61-169">If you want tooset up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="84f61-170">Örneğin, ayarladığınız ve Azure DNS'ye temsilci 'contoso.net' tooset ayrı alt bölge ayarlamak istediğinizi varsayalım 'partners.contoso.net'.</span><span class="sxs-lookup"><span data-stu-id="84f61-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like tooset up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="84f61-171">Merhaba alt bölge 'partners.contoso.net' Azure DNS'de oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84f61-171">Create hello child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="84f61-172">Merhaba alt bölge tooobtain hello ad sunucuları Azure DNS'deki hello alt bölgeyi barındıran hello yetkili NS kayıtlarını arayın.</span><span class="sxs-lookup"><span data-stu-id="84f61-172">Look up hello authoritative NS records in hello child zone tooobtain hello name servers hosting hello child zone in Azure DNS.</span></span>
3. <span data-ttu-id="84f61-173">Merhaba üst bölgede toohello alt bölgeyi işaret eden NS kayıtlarını yapılandırarak hello alt bölge temsilcisi.</span><span class="sxs-lookup"><span data-stu-id="84f61-173">Delegate hello child zone by configuring NS records in hello parent zone pointing toohello child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="84f61-174">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f61-174">Create a DNS zone</span></span>

1. <span data-ttu-id="84f61-175">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="84f61-175">Sign in toohello Azure portal</span></span>
1. <span data-ttu-id="84f61-176">Hello Hub menüsünde ve tıklayın **yeni > Ağ iletişimi >** ve ardından **DNS bölgesi** tooopen hello oluşturmak DNS bölge dikey.</span><span class="sxs-lookup"><span data-stu-id="84f61-176">On hello Hub menu, click and click **New > Networking >** and then click **DNS zone** tooopen hello Create DNS zone blade.</span></span>

    ![DNS bölgesi](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="84f61-178">Merhaba üzerinde **oluşturma DNS bölgesi** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **oluşturma**:</span><span class="sxs-lookup"><span data-stu-id="84f61-178">On hello **Create DNS zone** blade enter hello following values, then click **Create**:</span></span>

   | <span data-ttu-id="84f61-179">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="84f61-179">**Setting**</span></span> | <span data-ttu-id="84f61-180">**Değer**</span><span class="sxs-lookup"><span data-stu-id="84f61-180">**Value**</span></span> | <span data-ttu-id="84f61-181">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="84f61-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="84f61-182">**Ad**</span><span class="sxs-lookup"><span data-stu-id="84f61-182">**Name**</span></span>|<span data-ttu-id="84f61-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="84f61-183">partners.contoso.net</span></span>|<span data-ttu-id="84f61-184">Merhaba DNS bölgesinin Hello adı</span><span class="sxs-lookup"><span data-stu-id="84f61-184">hello name of hello DNS zone</span></span>|
   |<span data-ttu-id="84f61-185">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="84f61-185">**Subscription**</span></span>|<span data-ttu-id="84f61-186">[Aboneliğiniz]</span><span class="sxs-lookup"><span data-stu-id="84f61-186">[Your subscription]</span></span>|<span data-ttu-id="84f61-187">Bir abonelik toocreate hello uygulama ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="84f61-187">Select a subscription toocreate hello application gateway in.</span></span>|
   |<span data-ttu-id="84f61-188">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="84f61-188">**Resource group**</span></span>|<span data-ttu-id="84f61-189">**Varolanı kullan:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="84f61-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="84f61-190">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84f61-190">Create a resource group.</span></span> <span data-ttu-id="84f61-191">Merhaba kaynak grubu adı, seçtiğiniz hello abonelik içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="84f61-191">hello resource group name must be unique within hello subscription you selected.</span></span> <span data-ttu-id="84f61-192">Merhaba okuyun, kaynak grupları hakkında daha fazla toolearn [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) genel bakış makalesi.</span><span class="sxs-lookup"><span data-stu-id="84f61-192">toolearn more about resource groups, read hello [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="84f61-193">**Konum**</span><span class="sxs-lookup"><span data-stu-id="84f61-193">**Location**</span></span>|<span data-ttu-id="84f61-194">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="84f61-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="84f61-195">Merhaba kaynak grubu hello kaynak grubu toohello konumunu gösterir ve hello DNS bölgesi üzerinde hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="84f61-195">hello resource group refers toohello location of hello resource group, and has no impact on hello DNS zone.</span></span> <span data-ttu-id="84f61-196">Merhaba DNS bölgesi konumunu her zaman "Genel" ve gösterilmiyor.</span><span class="sxs-lookup"><span data-stu-id="84f61-196">hello DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="84f61-197">Ad sunucularını alma</span><span class="sxs-lookup"><span data-stu-id="84f61-197">Retrieve name servers</span></span>

1. <span data-ttu-id="84f61-198">Oluşturulan, hello Azure portal hello DNS bölgesine **Sık Kullanılanlar** bölmesinde, tıklatın **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="84f61-198">With hello DNS zone created, in hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="84f61-199">Merhaba tıklatın **partners.contoso.net** hello DNS bölgesinde **tüm kaynakları** dikey.</span><span class="sxs-lookup"><span data-stu-id="84f61-199">Click hello **partners.contoso.net** DNS zone in hello **All resources** blade.</span></span> <span data-ttu-id="84f61-200">Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **partners.contoso.net** adına göre filtre hello içinde...</span><span class="sxs-lookup"><span data-stu-id="84f61-200">If hello subscription you selected already has several resources in it, you can enter **partners.contoso.net** in hello Filter by name…</span></span> <span data-ttu-id="84f61-201">kutusunu tooeasily erişim hello DNS bölgesi.</span><span class="sxs-lookup"><span data-stu-id="84f61-201">box tooeasily access hello DNS zone.</span></span>

1. <span data-ttu-id="84f61-202">Merhaba ad sunucuları hello DNS bölgesine dikey penceresinden alır.</span><span class="sxs-lookup"><span data-stu-id="84f61-202">Retrieve hello name servers from hello DNS zone blade.</span></span> <span data-ttu-id="84f61-203">Bu örnekte 'contoso.net' hello bölge ad sunucuları atanmıştır ' ns1-01.azure-dns.com', 'ns2-01.azure-DNS.NET', ' ns3-01.azure-dns.org', ve ' ns4-01.azure-dns.info':</span><span class="sxs-lookup"><span data-stu-id="84f61-203">In this example, hello zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="84f61-205">Azure DNS, bölgenizi hello atanan ad sunucularını içeren yetkili NS kayıtları otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84f61-205">Azure DNS automatically creates authoritative NS records in your zone containing hello assigned name servers.</span></span>  <span data-ttu-id="84f61-206">Azure PowerShell veya Azure CLI toosee hello ad sunucusu adlarını, tooretrieve bu kayıtları yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="84f61-206">toosee hello name server names via Azure PowerShell or Azure CLI, you simply need tooretrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="84f61-207">Üst bölgede ad sunucusu kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="84f61-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="84f61-208">Toohello gidin **contoso.net** hello Azure portal DNS bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="84f61-208">Navigate toohello **contoso.net** DNS zone in hello Azure portal.</span></span>
1. <span data-ttu-id="84f61-209">**+ Kayıt kümesi**’ne tıklayın</span><span class="sxs-lookup"><span data-stu-id="84f61-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="84f61-210">Merhaba üzerinde **kayıt kümesi ekleme** dikey penceresinde hello aşağıdaki değerleri girin ve ardından **Tamam**:</span><span class="sxs-lookup"><span data-stu-id="84f61-210">On hello **Add record set** blade, enter hello following values, then click **OK**:</span></span>

   | <span data-ttu-id="84f61-211">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="84f61-211">**Setting**</span></span> | <span data-ttu-id="84f61-212">**Değer**</span><span class="sxs-lookup"><span data-stu-id="84f61-212">**Value**</span></span> | <span data-ttu-id="84f61-213">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="84f61-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="84f61-214">**Ad**</span><span class="sxs-lookup"><span data-stu-id="84f61-214">**Name**</span></span>|<span data-ttu-id="84f61-215">iş ortakları</span><span class="sxs-lookup"><span data-stu-id="84f61-215">partners</span></span>|<span data-ttu-id="84f61-216">Merhaba alt DNS bölgesinin Hello adı</span><span class="sxs-lookup"><span data-stu-id="84f61-216">hello name of hello child DNS zone</span></span>|
   |<span data-ttu-id="84f61-217">**Tür**</span><span class="sxs-lookup"><span data-stu-id="84f61-217">**Type**</span></span>|<span data-ttu-id="84f61-218">NS</span><span class="sxs-lookup"><span data-stu-id="84f61-218">NS</span></span>|<span data-ttu-id="84f61-219">Ad sunucusu kayıtları için NS kullanın.</span><span class="sxs-lookup"><span data-stu-id="84f61-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="84f61-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="84f61-220">**TTL**</span></span>|<span data-ttu-id="84f61-221">1</span><span class="sxs-lookup"><span data-stu-id="84f61-221">1</span></span>|<span data-ttu-id="84f61-222">Saat toolive.</span><span class="sxs-lookup"><span data-stu-id="84f61-222">Time toolive.</span></span>|
   |<span data-ttu-id="84f61-223">**TTL birimi**</span><span class="sxs-lookup"><span data-stu-id="84f61-223">**TTL unit**</span></span>|<span data-ttu-id="84f61-224">Saat</span><span class="sxs-lookup"><span data-stu-id="84f61-224">Hours</span></span>|<span data-ttu-id="84f61-225">zaman toolive birim toohours ayarlar</span><span class="sxs-lookup"><span data-stu-id="84f61-225">sets time toolive unit toohours</span></span>|
   |<span data-ttu-id="84f61-226">**AD SUNUCUSU**</span><span class="sxs-lookup"><span data-stu-id="84f61-226">**NAME SERVER**</span></span>|<span data-ttu-id="84f61-227">{partners.contoso.net bölgesinden ad sunucuları}</span><span class="sxs-lookup"><span data-stu-id="84f61-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="84f61-228">Merhaba ad sunucuları tüm 4 partners.contoso.net bölgeden girin.</span><span class="sxs-lookup"><span data-stu-id="84f61-228">Enter all 4 of hello name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="84f61-230">Diğer araçlarla Azure DNS'de alt etki alanlarını devretme</span><span class="sxs-lookup"><span data-stu-id="84f61-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="84f61-231">Merhaba aşağıdaki örneklerde hello adımlar toodelegate, PowerShell ve CLI Azure DNS'de alt etki alanlarını sağlar:</span><span class="sxs-lookup"><span data-stu-id="84f61-231">hello following examples provide hello steps toodelegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="84f61-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84f61-232">PowerShell</span></span>

<span data-ttu-id="84f61-233">Aşağıdaki PowerShell örneğine hello bunun nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="84f61-233">hello following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="84f61-234">aynı adımları hello Azure portal çalıştırılabilir veya platformlar arası Azure CLI aracılığıyla hello hello.</span><span class="sxs-lookup"><span data-stu-id="84f61-234">hello same steps can be executed via hello Azure portal, or via hello cross-platform Azure CLI.</span></span>

```powershell
# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve hello authoritative NS records from hello child zone as shown in hello next example. This contains hello name servers assigned toohello child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create hello corresponding NS record set in hello parent zone toocomplete hello delegation. hello record set name in hello parent zone matches hello child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="84f61-235">Kullanım `nslookup` her şeyin doğru şekilde hello alt bölgenin SOA kaydına hello bakarak ayarlanan tooverify.</span><span class="sxs-lookup"><span data-stu-id="84f61-235">Use `nslookup` tooverify that everything is set up correctly by looking up hello SOA record of hello child zone.</span></span>

```
nslookup -type=SOA partners.contoso.com
```

```
Server: ns1-08.azure-dns.com
Address: 208.76.47.8

partners.contoso.com
    primary name server = ns1-08.azure-dns.com
    responsible mail addr = msnhst.microsoft.com
    serial = 1
    refresh = 900 (15 mins)
    retry = 300 (5 mins)
    expire = 604800 (7 days)
    default TTL = 300 (5 mins)
```

#### <a name="azure-cli"></a><span data-ttu-id="84f61-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84f61-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create hello parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="84f61-237">Hello için Hello ad sunucularını almak `partners.contoso.net` hello çıkış bölgeden.</span><span class="sxs-lookup"><span data-stu-id="84f61-237">Retrieve hello name servers for hello `partners.contoso.net` zone from hello output.</span></span>

```
{
  "etag": "00000003-0000-0000-418f-250de2b2d201",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/contosorg/providers/Microsoft.Network/dnszones/partners.contoso.net",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "partners.contoso.net",
  "nameServers": [
    "ns1-09.azure-dns.com.",
    "ns2-09.azure-dns.net.",
    "ns3-09.azure-dns.org.",
    "ns4-09.azure-dns.info."
  ],
  "numberOfRecordSets": 2,
  "resourceGroup": "contosorg",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

<span data-ttu-id="84f61-238">Merhaba kayıt kümesi ve her bir ad sunucusu için NS kayıtları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84f61-238">Create hello record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create hello record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="84f61-239">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="84f61-239">Delete all resources</span></span>

<span data-ttu-id="84f61-240">Bu makalede, aşağıdaki adımları tam hello oluşturulan tüm kaynakları toodelete:</span><span class="sxs-lookup"><span data-stu-id="84f61-240">toodelete all resources created in this article, complete hello following steps:</span></span>

1. <span data-ttu-id="84f61-241">Hello Azure portal'ın **Sık Kullanılanlar** bölmesinde tıklatın **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="84f61-241">In hello Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="84f61-242">Merhaba tıklatın **contosorg** kaynak tüm kaynaklar dikey penceresinde hello grubu.</span><span class="sxs-lookup"><span data-stu-id="84f61-242">Click hello **contosorg** resource group in hello All resources blade.</span></span> <span data-ttu-id="84f61-243">Merhaba aboneliği zaten içinde birçok kaynak varsa, girebilirsiniz **contosorg** hello içinde **ada göre Filtrele...**</span><span class="sxs-lookup"><span data-stu-id="84f61-243">If hello subscription you selected already has several resources in it, you can enter **contosorg** in hello **Filter by name…**</span></span> <span data-ttu-id="84f61-244">kutusunu tooeasily erişim hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="84f61-244">box tooeasily access hello resource group.</span></span>
1. <span data-ttu-id="84f61-245">Merhaba, **contosorg** dikey penceresinde hello tıklatın **silmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="84f61-245">In hello **contosorg** blade, click hello **Delete** button.</span></span>
1. <span data-ttu-id="84f61-246">Merhaba portal tootype hello toodelete istediğiniz hello kaynak grubu tooconfirm adını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="84f61-246">hello portal requires you tootype hello name of hello resource group tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="84f61-247">Tür *contosorg* hello kaynak grubu adı için ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="84f61-247">Type *contosorg* for hello resource group name, then click **Delete**.</span></span> <span data-ttu-id="84f61-248">Bu nedenle her zaman emin tooconfirm silmeden önce bir kaynak grubu Merhaba içeriğine olması, bir kaynak grubunu silme hello kaynak grubundaki tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="84f61-248">Deleting a resource group deletes all resources within hello resource group, so always be sure tooconfirm hello contents of a resource group before deleting it.</span></span> <span data-ttu-id="84f61-249">Merhaba portal hello kaynak grubu içinde bulunan tüm kaynakları siler ve sonra hello kaynak grubu kendisini siler.</span><span class="sxs-lookup"><span data-stu-id="84f61-249">hello portal deletes all resources contained within hello resource group, then deletes hello resource group itself.</span></span> <span data-ttu-id="84f61-250">Bu işlem birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="84f61-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84f61-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84f61-251">Next steps</span></span>

[<span data-ttu-id="84f61-252">DNS bölgelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="84f61-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="84f61-253">DNS kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="84f61-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
