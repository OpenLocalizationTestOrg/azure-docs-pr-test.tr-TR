---
title: "Etki alanınızı Azure DNS'ye devretme | Microsoft Belgeleri"
description: "Etki alanı temsilcisi seçiminin nasıl değiştirileceğini ve etki alanı barındırma sağlamak üzere Azure DNS ad sunucularının nasıl kullanılacağını anlayın."
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
ms.openlocfilehash: 33b3ec24432ff1268860b9a2e9d5098600a8dedc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="delegate-a-domain-to-azure-dns"></a><span data-ttu-id="8ed44-103">Azure DNS'ye bir etki alanı devretme</span><span class="sxs-lookup"><span data-stu-id="8ed44-103">Delegate a domain to Azure DNS</span></span>

<span data-ttu-id="8ed44-104">Azure DNS, bir DNS bölgesi barındırmanızı ve Azure'de bir etki alanı için DNS kayıtlarını yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ed44-104">Azure DNS allows you to host a DNS zone and manage the DNS records for a domain in Azure.</span></span> <span data-ttu-id="8ed44-105">Bir etki alanının DNS sorgularının Azure DNS'ye erişmesi için, etki alanının Azure DNS'ye üst etki alanından devredilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-105">In order for DNS queries for a domain to reach Azure DNS, the domain has to be delegated to Azure DNS from the parent domain.</span></span> <span data-ttu-id="8ed44-106">Azure DNS'nin etki alanı kayıt şirketi olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-106">Keep in mind Azure DNS is not the domain registrar.</span></span> <span data-ttu-id="8ed44-107">Bu makalede etki alanınızı Azure DNS’ye devretme işlemi açıklanır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-107">This article explains how to delegate your domain to Azure DNS.</span></span>

<span data-ttu-id="8ed44-108">Bir kayıt şirketinden satın alınan etki alanları için, kayıt şirketiniz bu NS kayıtlarını ayarlama seçeneğini sunar.</span><span class="sxs-lookup"><span data-stu-id="8ed44-108">For domains purchased from a registrar, your registrar offers the option to set up these NS records.</span></span> <span data-ttu-id="8ed44-109">Azure DNS'de aynı etki alanı adıyla DNS bölgesi oluşturmak için bir etki alanına sahip olmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8ed44-109">You do not have to own a domain to create a DNS zone with that domain name in Azure DNS.</span></span> <span data-ttu-id="8ed44-110">Ancak Azure DNS'ye temsilci seçmeyi kayıt şirketi ile ayarlamak için etki alanına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-110">However, you do need to own the domain to set up the delegation to Azure DNS with the registrar.</span></span>

<span data-ttu-id="8ed44-111">Örneğin, "contoso.net" etki alanını satın aldığınızı ve Azure DNS'de "contoso.net" adlı bir bölge oluşturduğunuzu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8ed44-111">For example, suppose you purchase the domain 'contoso.net' and create a zone with the name 'contoso.net' in Azure DNS.</span></span> <span data-ttu-id="8ed44-112">Etki alanı sahibi olarak, kayıt şirketiniz size etki alanınız için ad sunucusu adreslerini (yani NS kayıtlarını) yapılandırma seçeneğini sunar.</span><span class="sxs-lookup"><span data-stu-id="8ed44-112">As the owner of the domain, your registrar offers you the option to configure the name server addresses (that is, the NS records) for your domain.</span></span> <span data-ttu-id="8ed44-113">Kayıt şirketi bu NS kayıtlarını üst etki alanında (bu durumda “.net”te) depolar.</span><span class="sxs-lookup"><span data-stu-id="8ed44-113">The registrar stores these NS records in the parent domain, in this case '.net'.</span></span> <span data-ttu-id="8ed44-114">Ardından, dünya genelindeki istemciler “contoso.net”teki DNS kayıtlarını çözümlemeye çalışırken Azure DNS bölgesindeki etki alanınıza yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-114">Clients around the world can then be directed to your domain in Azure DNS zone when trying to resolve DNS records in 'contoso.net'.</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="8ed44-115">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ed44-115">Create a DNS zone</span></span>

1. <span data-ttu-id="8ed44-116">Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="8ed44-116">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="8ed44-117">Hub menüsünde **Yeni > Ağ >** ve ardından **DNS bölgesi**’ne tıklayarak DNS bölgesi oluştur dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-117">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS bölgesi](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="8ed44-119">**DNS bölgesi oluştur** dikey penceresinde aşağıdaki değerleri girin ve **Oluştur**’a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="8ed44-119">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="8ed44-120">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="8ed44-120">**Setting**</span></span> | <span data-ttu-id="8ed44-121">**Değer**</span><span class="sxs-lookup"><span data-stu-id="8ed44-121">**Value**</span></span> | <span data-ttu-id="8ed44-122">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="8ed44-122">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="8ed44-123">**Ad**</span><span class="sxs-lookup"><span data-stu-id="8ed44-123">**Name**</span></span>|<span data-ttu-id="8ed44-124">contoso.net</span><span class="sxs-lookup"><span data-stu-id="8ed44-124">contoso.net</span></span>|<span data-ttu-id="8ed44-125">DNS bölgesinin adı</span><span class="sxs-lookup"><span data-stu-id="8ed44-125">The name of the DNS zone</span></span>|
   |<span data-ttu-id="8ed44-126">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="8ed44-126">**Subscription**</span></span>|<span data-ttu-id="8ed44-127">[Aboneliğiniz]</span><span class="sxs-lookup"><span data-stu-id="8ed44-127">[Your subscription]</span></span>|<span data-ttu-id="8ed44-128">Uygulama ağ geçidinin oluşturulacağı bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="8ed44-128">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="8ed44-129">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="8ed44-129">**Resource group**</span></span>|<span data-ttu-id="8ed44-130">**Yeni oluştur:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="8ed44-130">**Create new:** contosoRG</span></span>|<span data-ttu-id="8ed44-131">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ed44-131">Create a resource group.</span></span> <span data-ttu-id="8ed44-132">Kaynak grubu adı, seçili abonelik içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-132">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="8ed44-133">Kaynak grupları hakkında daha fazla bilgi için, [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)’a genel bakış makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="8ed44-133">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="8ed44-134">**Konum**</span><span class="sxs-lookup"><span data-stu-id="8ed44-134">**Location**</span></span>|<span data-ttu-id="8ed44-135">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="8ed44-135">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="8ed44-136">Kaynak grubu, kaynak grubunun konumunu ifade eder ve DNS bölgesini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="8ed44-136">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="8ed44-137">DNS bölgesinin konumu her zaman "genel" şeklindedir ve gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="8ed44-137">The DNS zone location is always "global", and is not shown.</span></span>

## <a name="retrieve-name-servers"></a><span data-ttu-id="8ed44-138">Ad sunucularını alma</span><span class="sxs-lookup"><span data-stu-id="8ed44-138">Retrieve name servers</span></span>

<span data-ttu-id="8ed44-139">DNS bölgenizi Azure DNS'ye devretmeden önce, bölgenizin ad sunucusu adlarını bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-139">Before you can delegate your DNS zone to Azure DNS, you first need to know the name server names for your zone.</span></span> <span data-ttu-id="8ed44-140">Azure DNS, her bölge oluşturmada bir havuzdan ad sunucuları ayırır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-140">Azure DNS allocates name servers from a pool each time a zone is created.</span></span>

1. <span data-ttu-id="8ed44-141">Oluşturulan DNS bölgesiyle, Azure Portal **Sık Kullanılanlar** bölmesinde, **Tüm kaynaklar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-141">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="8ed44-142">**Tüm kaynaklar** dikey penceresinde **contoso.net** DNS bölgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-142">Click the **contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="8ed44-143">Seçili abonelikte zaten çeşitli kaynaklar varsa, uygulama ağ geçidine kolaylıkla erişmek için Ada göre filtrele... kutusuna **contoso.net**</span><span class="sxs-lookup"><span data-stu-id="8ed44-143">If the subscription you selected already has several resources in it, you can enter **contoso.net** in the Filter by name…</span></span> <span data-ttu-id="8ed44-144">girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed44-144">box to easily access the application gateway.</span></span> 

1. <span data-ttu-id="8ed44-145">DNS bölgesi dikey penceresinden ad sunucularını alın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-145">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="8ed44-146">Bu örnekte, "contoso.net" bölgesine "ns1-01.azure-dns.com", "ns2-01.azure-dns.net", "ns3-01.azure-dns.org" ve "ns4-01.azure-dns.info" ad sunucuları atanmıştır:</span><span class="sxs-lookup"><span data-stu-id="8ed44-146">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="8ed44-148">Azure DNS, atanan ad sunucularını içeren yetkili NS kayıtlarını bölgenizde otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ed44-148">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="8ed44-149">Ad sunucusu adlarını Azure PowerShell veya Azure CLI aracılığıyla görmek için bu kayıtları almanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-149">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

<span data-ttu-id="8ed44-150">Aşağıdaki örneklerde, PowerShell ve Azure CLI ile Azure DNS içindeki bir bölgenin ad sunucularını alma adımları da sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-150">The following examples also provide the steps to retrieve the name servers for a zone in Azure DNS with PowerShell and Azure CLI.</span></span>

### <a name="powershell"></a><span data-ttu-id="8ed44-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed44-151">PowerShell</span></span>

```powershell
# The record name "@" is used to refer to records at the top of the zone.
$zone = Get-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
Get-AzureRmDnsRecordSet -Name "@" -RecordType NS -Zone $zone
```

<span data-ttu-id="8ed44-152">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-152">The following example is the response.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="8ed44-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8ed44-153">Azure CLI</span></span>

```azurecli
az network dns record-set show --resource-group contosoRG --zone-name contoso.net --type NS --name @
```

<span data-ttu-id="8ed44-154">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-154">The following example is the response.</span></span>

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

## <a name="delegate-the-domain"></a><span data-ttu-id="8ed44-155">Etki alanını devretme</span><span class="sxs-lookup"><span data-stu-id="8ed44-155">Delegate the domain</span></span>

<span data-ttu-id="8ed44-156">Artık DNS bölgesi oluşturulduğuna ve ad sunucularınız olduğuna göre, üst etki alanının Azure DNS ad sunucularıyla güncelleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-156">Now that the DNS zone is created and you have the name servers, the parent domain needs to be updated with the Azure DNS name servers.</span></span> <span data-ttu-id="8ed44-157">Her kayıt şirketi, bir etki alanının ad sunucusu kayıtlarını değiştirmek için kendi DNS yönetim araçlarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-157">Each registrar has their own DNS management tools to change the name server records for a domain.</span></span> <span data-ttu-id="8ed44-158">Kayıt şirketinin DNS yönetim sayfasında NS kayıtlarını düzenleyin ve NS kayıtlarını Azure DNS'nin oluşturduklarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8ed44-158">In the registrar's DNS management page, edit the NS records and replace the NS records with the ones Azure DNS created.</span></span>

<span data-ttu-id="8ed44-159">Bir etki alanını Azure DNS'ye devrederken Azure DNS tarafından sağlanan ad sunucusu adlarını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-159">When delegating a domain to Azure DNS, you must use the name server names provided by Azure DNS.</span></span> <span data-ttu-id="8ed44-160">Etki alanınızın adından bağımsız olarak her zaman dört sunucu adını da kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-160">It is recommended to use all four name server names, regardless of the name of your domain.</span></span> <span data-ttu-id="8ed44-161">Etki alanı temsilcisi, sunucu adının etki alanınızla aynı üst düzey etki alanını kullanmasını gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="8ed44-161">Domain delegation does not require the name server name to use the same top-level domain as your domain.</span></span>

<span data-ttu-id="8ed44-162">Azure DNS ad sunucusu IP adresleri gelecekte değişebileceği için, bu IP adreslerine işaret ederken "birleştirici kayıtlar"ı kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-162">You should not use 'glue records' to point to the Azure DNS name server IP addresses, since these IP addresses may change in future.</span></span> <span data-ttu-id="8ed44-163">Kendi bölgenizdeki ad sunucusu adlarını kullanan ve bazen "gösterim ad sunucuları" olarak adlandırılan temsilci seçimleri, Azure DNS'de şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-163">Delegations using name server names in your own zone, sometimes called 'vanity name servers', are not currently supported in Azure DNS.</span></span>

## <a name="verify-name-resolution-is-working"></a><span data-ttu-id="8ed44-164">Ad çözümlemesinin çalıştığını doğrulama</span><span class="sxs-lookup"><span data-stu-id="8ed44-164">Verify name resolution is working</span></span>

<span data-ttu-id="8ed44-165">Temsilci seçmeyi tamamladıktan sonra, bölgenizin SOA kaydını (bölge oluşturulduğunda bu da otomatik olarak oluşturulur) sorgulamak için "nslookup" gibi bir araç kullanarak ad çözümlemesinin çalışıp çalışmadığını doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed44-165">After completing the delegation, you can verify that name resolution is working by using a tool such as 'nslookup' to query the SOA record for your zone (which is also automatically created when the zone is created).</span></span>

<span data-ttu-id="8ed44-166">Azure DNS ad sunucularını belirtmeniz gerekmez; temsil doğru şekilde ayarlandıysa, normal DNS çözümleme işlemi ad sunucularını otomatik olarak bulur.</span><span class="sxs-lookup"><span data-stu-id="8ed44-166">You do not have to specify the Azure DNS name servers, if the delegation has been set up correctly, the normal DNS resolution process finds the name servers automatically.</span></span>

```
nslookup -type=SOA contoso.com
```

<span data-ttu-id="8ed44-167">Aşağıda, önceki komuttan bir yanıt örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="8ed44-167">The following is an example response from the preceding command:</span></span>

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

## <a name="delegate-sub-domains-in-azure-dns"></a><span data-ttu-id="8ed44-168">Azure DNS'de alt etki alanlarını devretme</span><span class="sxs-lookup"><span data-stu-id="8ed44-168">Delegate sub-domains in Azure DNS</span></span>

<span data-ttu-id="8ed44-169">Ayrı bir alt bölge kurmak istiyorsanız Azure DNS'de bir alt etki alanını devredebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed44-169">If you want to set up a separate child zone, you can delegate a sub-domain in Azure DNS.</span></span> <span data-ttu-id="8ed44-170">Örneğin, Azure DNS'de ayarladığınız ve devrettiğiniz "contoso.net" için "partners.contoso.net" olarak ayrı bir alt bölge ayarlamak istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8ed44-170">For example, having set up and delegated 'contoso.net' in Azure DNS, suppose you would like to set up a separate child zone, 'partners.contoso.net'.</span></span>

1. <span data-ttu-id="8ed44-171">Azure DNS'de "partners.contoso.net" alt bölgesini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ed44-171">Create the child zone 'partners.contoso.net' in Azure DNS.</span></span>
2. <span data-ttu-id="8ed44-172">Azure DNS'de alt bölgeyi barındıran ad sunucularını almak için, alt bölgedeki yetkili NS kayıtlarını arayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-172">Look up the authoritative NS records in the child zone to obtain the name servers hosting the child zone in Azure DNS.</span></span>
3. <span data-ttu-id="8ed44-173">Üst bölgeden alt bölgeye işaret eden NS kayıtlarını yapılandırarak alt bölgeyi devredin.</span><span class="sxs-lookup"><span data-stu-id="8ed44-173">Delegate the child zone by configuring NS records in the parent zone pointing to the child zone.</span></span>

### <a name="create-a-dns-zone"></a><span data-ttu-id="8ed44-174">DNS bölgesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ed44-174">Create a DNS zone</span></span>

1. <span data-ttu-id="8ed44-175">Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="8ed44-175">Sign in to the Azure portal</span></span>
1. <span data-ttu-id="8ed44-176">Hub menüsünde **Yeni > Ağ >** ve ardından **DNS bölgesi**’ne tıklayarak DNS bölgesi oluştur dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-176">On the Hub menu, click and click **New > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS bölgesi](./media/dns-domain-delegation/dns.png)

1. <span data-ttu-id="8ed44-178">**DNS bölgesi oluştur** dikey penceresinde aşağıdaki değerleri girin ve **Oluştur**’a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="8ed44-178">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>

   | <span data-ttu-id="8ed44-179">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="8ed44-179">**Setting**</span></span> | <span data-ttu-id="8ed44-180">**Değer**</span><span class="sxs-lookup"><span data-stu-id="8ed44-180">**Value**</span></span> | <span data-ttu-id="8ed44-181">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="8ed44-181">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="8ed44-182">**Ad**</span><span class="sxs-lookup"><span data-stu-id="8ed44-182">**Name**</span></span>|<span data-ttu-id="8ed44-183">partners.contoso.net</span><span class="sxs-lookup"><span data-stu-id="8ed44-183">partners.contoso.net</span></span>|<span data-ttu-id="8ed44-184">DNS bölgesinin adı</span><span class="sxs-lookup"><span data-stu-id="8ed44-184">The name of the DNS zone</span></span>|
   |<span data-ttu-id="8ed44-185">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="8ed44-185">**Subscription**</span></span>|<span data-ttu-id="8ed44-186">[Aboneliğiniz]</span><span class="sxs-lookup"><span data-stu-id="8ed44-186">[Your subscription]</span></span>|<span data-ttu-id="8ed44-187">Uygulama ağ geçidinin oluşturulacağı bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="8ed44-187">Select a subscription to create the application gateway in.</span></span>|
   |<span data-ttu-id="8ed44-188">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="8ed44-188">**Resource group**</span></span>|<span data-ttu-id="8ed44-189">**Varolanı kullan:** contosoRG</span><span class="sxs-lookup"><span data-stu-id="8ed44-189">**Use Existing:** contosoRG</span></span>|<span data-ttu-id="8ed44-190">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ed44-190">Create a resource group.</span></span> <span data-ttu-id="8ed44-191">Kaynak grubu adı, seçili abonelik içinde benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8ed44-191">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="8ed44-192">Kaynak grupları hakkında daha fazla bilgi için, [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups)’a genel bakış makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="8ed44-192">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="8ed44-193">**Konum**</span><span class="sxs-lookup"><span data-stu-id="8ed44-193">**Location**</span></span>|<span data-ttu-id="8ed44-194">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="8ed44-194">West US</span></span>||

> [!NOTE]
> <span data-ttu-id="8ed44-195">Kaynak grubu, kaynak grubunun konumunu ifade eder ve DNS bölgesini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="8ed44-195">The resource group refers to the location of the resource group, and has no impact on the DNS zone.</span></span> <span data-ttu-id="8ed44-196">DNS bölgesinin konumu her zaman "genel" şeklindedir ve gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="8ed44-196">The DNS zone location is always "global", and is not shown.</span></span>

### <a name="retrieve-name-servers"></a><span data-ttu-id="8ed44-197">Ad sunucularını alma</span><span class="sxs-lookup"><span data-stu-id="8ed44-197">Retrieve name servers</span></span>

1. <span data-ttu-id="8ed44-198">Oluşturulan DNS bölgesiyle, Azure Portal **Sık Kullanılanlar** bölmesinde, **Tüm kaynaklar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-198">With the DNS zone created, in the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="8ed44-199">**Tüm kaynaklar** dikey penceresinde **partners.contoso.net** DNS bölgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-199">Click the **partners.contoso.net** DNS zone in the **All resources** blade.</span></span> <span data-ttu-id="8ed44-200">Seçili abonelikte zaten çeşitli kaynaklar varsa, DNS bölgesine kolaylıkla erişmek için Ada göre filtrele... kutusuna **partners.contoso.net**</span><span class="sxs-lookup"><span data-stu-id="8ed44-200">If the subscription you selected already has several resources in it, you can enter **partners.contoso.net** in the Filter by name…</span></span> <span data-ttu-id="8ed44-201">girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed44-201">box to easily access the DNS zone.</span></span>

1. <span data-ttu-id="8ed44-202">DNS bölgesi dikey penceresinden ad sunucularını alın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-202">Retrieve the name servers from the DNS zone blade.</span></span> <span data-ttu-id="8ed44-203">Bu örnekte, "contoso.net" bölgesine "ns1-01.azure-dns.com", "ns2-01.azure-dns.net", "ns3-01.azure-dns.org" ve "ns4-01.azure-dns.info" ad sunucuları atanmıştır:</span><span class="sxs-lookup"><span data-stu-id="8ed44-203">In this example, the zone 'contoso.net' has been assigned name servers 'ns1-01.azure-dns.com', 'ns2-01.azure-dns.net', 'ns3-01.azure-dns.org', and 'ns4-01.azure-dns.info':</span></span>

 ![Dns-nameserver](./media/dns-domain-delegation/viewzonens500.png)

<span data-ttu-id="8ed44-205">Azure DNS, atanan ad sunucularını içeren yetkili NS kayıtlarını bölgenizde otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8ed44-205">Azure DNS automatically creates authoritative NS records in your zone containing the assigned name servers.</span></span>  <span data-ttu-id="8ed44-206">Ad sunucusu adlarını Azure PowerShell veya Azure CLI aracılığıyla görmek için bu kayıtları almanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-206">To see the name server names via Azure PowerShell or Azure CLI, you simply need to retrieve these records.</span></span>

### <a name="create-name-server-record-in-parent-zone"></a><span data-ttu-id="8ed44-207">Üst bölgede ad sunucusu kaydı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ed44-207">Create name server record in parent zone</span></span>

1. <span data-ttu-id="8ed44-208">Azure Portal’da **contoso.net** DNS bölgesine gidin.</span><span class="sxs-lookup"><span data-stu-id="8ed44-208">Navigate to the **contoso.net** DNS zone in the Azure portal.</span></span>
1. <span data-ttu-id="8ed44-209">**+ Kayıt kümesi**’ne tıklayın</span><span class="sxs-lookup"><span data-stu-id="8ed44-209">Click **+ Record set**</span></span>
1. <span data-ttu-id="8ed44-210">**Kaynak kümesi ekle** dikey penceresinde aşağıdaki değerleri girin, ardından **Tamam**’a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="8ed44-210">On the **Add record set** blade, enter the following values, then click **OK**:</span></span>

   | <span data-ttu-id="8ed44-211">**Ayar**</span><span class="sxs-lookup"><span data-stu-id="8ed44-211">**Setting**</span></span> | <span data-ttu-id="8ed44-212">**Değer**</span><span class="sxs-lookup"><span data-stu-id="8ed44-212">**Value**</span></span> | <span data-ttu-id="8ed44-213">**Ayrıntılar**</span><span class="sxs-lookup"><span data-stu-id="8ed44-213">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="8ed44-214">**Ad**</span><span class="sxs-lookup"><span data-stu-id="8ed44-214">**Name**</span></span>|<span data-ttu-id="8ed44-215">iş ortakları</span><span class="sxs-lookup"><span data-stu-id="8ed44-215">partners</span></span>|<span data-ttu-id="8ed44-216">Alt DNS bölgesinin adı</span><span class="sxs-lookup"><span data-stu-id="8ed44-216">The name of the child DNS zone</span></span>|
   |<span data-ttu-id="8ed44-217">**Tür**</span><span class="sxs-lookup"><span data-stu-id="8ed44-217">**Type**</span></span>|<span data-ttu-id="8ed44-218">NS</span><span class="sxs-lookup"><span data-stu-id="8ed44-218">NS</span></span>|<span data-ttu-id="8ed44-219">Ad sunucusu kayıtları için NS kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-219">Use NS for name server records.</span></span>|
   |<span data-ttu-id="8ed44-220">**TTL**</span><span class="sxs-lookup"><span data-stu-id="8ed44-220">**TTL**</span></span>|<span data-ttu-id="8ed44-221">1</span><span class="sxs-lookup"><span data-stu-id="8ed44-221">1</span></span>|<span data-ttu-id="8ed44-222">Yaşam süresi.</span><span class="sxs-lookup"><span data-stu-id="8ed44-222">Time to live.</span></span>|
   |<span data-ttu-id="8ed44-223">**TTL birimi**</span><span class="sxs-lookup"><span data-stu-id="8ed44-223">**TTL unit**</span></span>|<span data-ttu-id="8ed44-224">Saat</span><span class="sxs-lookup"><span data-stu-id="8ed44-224">Hours</span></span>|<span data-ttu-id="8ed44-225">yaşam süresi birimi olarak saati ayarlar</span><span class="sxs-lookup"><span data-stu-id="8ed44-225">sets time to live unit to hours</span></span>|
   |<span data-ttu-id="8ed44-226">**AD SUNUCUSU**</span><span class="sxs-lookup"><span data-stu-id="8ed44-226">**NAME SERVER**</span></span>|<span data-ttu-id="8ed44-227">{partners.contoso.net bölgesinden ad sunucuları}</span><span class="sxs-lookup"><span data-stu-id="8ed44-227">{name servers from partners.contoso.net zone}</span></span>|<span data-ttu-id="8ed44-228">Partners.contoso.net bölgesindeki 4 ad sunucusunun adını da girin.</span><span class="sxs-lookup"><span data-stu-id="8ed44-228">Enter all 4 of the name servers from partners.contoso.net zone.</span></span> |

   ![Dns-nameserver](./media/dns-domain-delegation/partnerzone.png)


### <a name="delegating-sub-domains-in-azure-dns-with-other-tools"></a><span data-ttu-id="8ed44-230">Diğer araçlarla Azure DNS'de alt etki alanlarını devretme</span><span class="sxs-lookup"><span data-stu-id="8ed44-230">Delegating sub-domains in Azure DNS with other tools</span></span>

<span data-ttu-id="8ed44-231">Aşağıdaki örneklerde, PowerShell ve CLI ile Azure DNS’de alt etki alanlarını devretme adımları sağlanır:</span><span class="sxs-lookup"><span data-stu-id="8ed44-231">The following examples provide the steps to delegate sub-domains in Azure DNS with PowerShell and CLI:</span></span>

#### <a name="powershell"></a><span data-ttu-id="8ed44-232">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ed44-232">PowerShell</span></span>

<span data-ttu-id="8ed44-233">Aşağıdaki PowerShell örneğinde bunun nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-233">The following PowerShell example demonstrates how this works.</span></span> <span data-ttu-id="8ed44-234">Aynı adımlar Azure portalı veya platformlar arası Azure CLI yoluyla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-234">The same steps can be executed via the Azure portal, or via the cross-platform Azure CLI.</span></span>

```powershell
# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
$parent = New-AzureRmDnsZone -Name contoso.net -ResourceGroupName contosoRG
$child = New-AzureRmDnsZone -Name partners.contoso.net -ResourceGroupName contosoRG

# Retrieve the authoritative NS records from the child zone as shown in the next example. This contains the name servers assigned to the child zone.
$child_ns_recordset = Get-AzureRmDnsRecordSet -Zone $child -Name "@" -RecordType NS

# Create the corresponding NS record set in the parent zone to complete the delegation. The record set name in the parent zone matches the child zone name, in this case "partners".
$parent_ns_recordset = New-AzureRmDnsRecordSet -Zone $parent -Name "partners" -RecordType NS -Ttl 3600
$parent_ns_recordset.Records = $child_ns_recordset.Records
Set-AzureRmDnsRecordSet -RecordSet $parent_ns_recordset
```

<span data-ttu-id="8ed44-235">Alt bölgenin SOA kaydına bakarak her şeyin doğru şekilde ayarlandığını doğrulamak için `nslookup` kullanın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-235">Use `nslookup` to verify that everything is set up correctly by looking up the SOA record of the child zone.</span></span>

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

#### <a name="azure-cli"></a><span data-ttu-id="8ed44-236">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8ed44-236">Azure CLI</span></span>

```azurecli
#!/bin/bash

# Create the parent and child zones. These can be in same resource group or different resource groups as Azure DNS is a global service.
az network dns zone create -g contosoRG -n contoso.net
az network dns zone create -g contosoRG -n partners.contoso.net
```

<span data-ttu-id="8ed44-237">Çıkıştan, `partners.contoso.net` bölgesinin ad sunucularını alın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-237">Retrieve the name servers for the `partners.contoso.net` zone from the output.</span></span>

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

<span data-ttu-id="8ed44-238">Her ad sunucusu için kayıt kümesini ve NS kayıtlarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8ed44-238">Create the record set and NS records for each name server.</span></span>

```azurecli
#!/bin/bash

# Create the record set
az network dns record-set ns create --resource-group contosorg --zone-name contoso.net --name partners

# Create a ns record for each name server.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns1-09.azure-dns.com.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns2-09.azure-dns.net.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns3-09.azure-dns.org.
az network dns record-set ns add-record --resource-group contosorg --zone-name contoso.net --record-set-name partners --nsdname ns4-09.azure-dns.info.
```

## <a name="delete-all-resources"></a><span data-ttu-id="8ed44-239">Tüm kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="8ed44-239">Delete all resources</span></span>

<span data-ttu-id="8ed44-240">Bu makalede oluşturulan tüm kaynakları silmek için, aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="8ed44-240">To delete all resources created in this article, complete the following steps:</span></span>

1. <span data-ttu-id="8ed44-241">Azure Portal **Sık Kullanılanlar** bölmesinde, **Tüm kaynaklar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-241">In the Azure portal **Favorites** pane, click **All resources**.</span></span> <span data-ttu-id="8ed44-242">Tüm kaynaklar dikey penceresinde **contosorg** kaynak grubuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-242">Click the **contosorg** resource group in the All resources blade.</span></span> <span data-ttu-id="8ed44-243">Seçili abonelikte zaten çeşitli kaynaklar varsa, kaynak grubuna kolaylıkla erişmek için **Ada göre filtrele...** kutusuna **contosorg**</span><span class="sxs-lookup"><span data-stu-id="8ed44-243">If the subscription you selected already has several resources in it, you can enter **contosorg** in the **Filter by name…**</span></span> <span data-ttu-id="8ed44-244">girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ed44-244">box to easily access the resource group.</span></span>
1. <span data-ttu-id="8ed44-245">**contosorg** dikey penceresinde **Sil** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-245">In the **contosorg** blade, click the **Delete** button.</span></span>
1. <span data-ttu-id="8ed44-246">Portal, silmek istediğinizi onaylamak için kaynak grubunun adını yazmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ed44-246">The portal requires you to type the name of the resource group to confirm that you want to delete it.</span></span> <span data-ttu-id="8ed44-247">Kaynak grubu adı için *contosorg* yazın ve **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-247">Type *contosorg* for the resource group name, then click **Delete**.</span></span> <span data-ttu-id="8ed44-248">Bir kaynak grubunun silinmesiyle, kaynak grubu içerisindeki tüm kaynaklar silinir, bu nedenle, silmeden önce kaynak grubunun içeriğini onaylamayı hiçbir zaman unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8ed44-248">Deleting a resource group deletes all resources within the resource group, so always be sure to confirm the contents of a resource group before deleting it.</span></span> <span data-ttu-id="8ed44-249">Portal, kaynak grubu içinde yer alan tüm kaynakları siler ve sonra kaynak grubunu siler.</span><span class="sxs-lookup"><span data-stu-id="8ed44-249">The portal deletes all resources contained within the resource group, then deletes the resource group itself.</span></span> <span data-ttu-id="8ed44-250">Bu işlem birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8ed44-250">This process takes several minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ed44-251">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ed44-251">Next steps</span></span>

[<span data-ttu-id="8ed44-252">DNS bölgelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="8ed44-252">Manage DNS zones</span></span>](dns-operations-dnszones.md)

[<span data-ttu-id="8ed44-253">DNS kayıtlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8ed44-253">Manage DNS records</span></span>](dns-operations-recordsets.md)
