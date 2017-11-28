---
title: "DNS bölgeleri ve kayıtları koruma | Microsoft Docs"
description: "DNS bölgeleri ve Microsoft Azure DNS kayıt kümelerini korumak nasıl."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: 190e69eb-e820-4fc8-8e9a-baaf0b3fb74a
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/20/2016
ms.author: jonatul
ms.openlocfilehash: 0b7040d6273b3a6b85cd55850d596807226b87fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-protect-dns-zones-and-records"></a><span data-ttu-id="0441d-103">DNS bölgeleri ve kayıtları korumak nasıl</span><span class="sxs-lookup"><span data-stu-id="0441d-103">How to protect DNS zones and records</span></span>

<span data-ttu-id="0441d-104">DNS bölgeleri ve kayıtları kritik kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="0441d-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="0441d-105">Bir DNS bölgesine veya bile yalnızca tek bir DNS kaydı silinirken bir toplam hizmet kesintisine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="0441d-106">Bu nedenle kritik DNS bölgeleri ve kayıtları yetkisiz veya yanlışlıkla değişikliklere karşı korumalı önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0441d-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="0441d-107">Bu makalede, Azure DNS'ye nasıl, DNS bölgeleri ve kayıtları bu değişikliklere karşı korumanıza olanak tanır açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0441d-107">This article explains how Azure DNS enables you to protect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="0441d-108">Biz Azure Resource Manager tarafından sağlanan iki güçlü güvenlik özelliklerini uygulayın: [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) ve [kaynak kilitleri](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="0441d-109">Rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="0441d-109">Role-based access control</span></span>

<span data-ttu-id="0441d-110">Azure rol tabanlı erişim denetimi (RBAC) Azure kullanıcıları, grupları ve kaynakları için ayrıntılı erişim yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0441d-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="0441d-111">RBAC kullanarak, kullanıcıların işlerini yapmak için gereksinim duyduğu tam olarak erişim miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0441d-111">Using RBAC, you can grant precisely the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="0441d-112">RBAC erişimi yönetmenize nasıl yardımcı olduğunu hakkında daha fazla bilgi için bkz: [rol tabanlı erişim denetimi nedir](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="the-dns-zone-contributor-role"></a><span data-ttu-id="0441d-113">'DNS bölge katılımcı' rolü</span><span class="sxs-lookup"><span data-stu-id="0441d-113">The 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="0441d-114">'DNS bölge katılımcı' rolü DNS kaynakları yönetmek için Azure tarafından sağlanan yerleşik bir roldür.</span><span class="sxs-lookup"><span data-stu-id="0441d-114">The 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="0441d-115">Bir kullanıcı veya grup için DNS bölge katkıda bulunan izinleri atama DNS kaynakları, ancak kaynakları diğer herhangi bir tür değil yönetmek bu grubu sağlar.</span><span class="sxs-lookup"><span data-stu-id="0441d-115">Assigning DNS Zone Contributor permissions to a user or group enables that group to manage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="0441d-116">Örneğin, Contoso Corporation için beş bölgeleri 'myzones' kaynak grubu içeren varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0441d-116">For example, suppose the resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="0441d-117">DNS Yöneticisi, kaynak grubuna 'DNS bölge katkıda bulunan' izin verme, bu DNS bölgeleri üzerinde tam denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="0441d-117">Granting the DNS administrator 'DNS Zone Contributor' permissions to that resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="0441d-118">Örneğin DNS Yöneticisi oluşturmak veya sanal makineleri durdurmayı gereksiz izinleri verme önler.</span><span class="sxs-lookup"><span data-stu-id="0441d-118">It also avoids granting unnecessary permissions, for example the DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="0441d-119">RBAC izinler atamak için en basit yolu [Azure Portalı aracılığıyla](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-119">The simplest way to assign RBAC permissions is [via the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="0441d-120">Kaynak grubu için 'Erişim denetimi (IAM)' dikey penceresini açın, ardından 'Add','i tıklatın ardından 'DNS bölge katılımcı' rolü seçin ve gerekli kullanıcıları veya grupları izinleri vermek için seçin.</span><span class="sxs-lookup"><span data-stu-id="0441d-120">Open the 'Access control (IAM)' blade for the resource group, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Azure Portalı aracılığıyla kaynak grubu düzeyinde RBAC](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="0441d-122">İzinleri de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="0441d-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="0441d-123">Eşdeğer ayrıca komuttur [Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="0441d-123">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to all zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="0441d-124">Bölge düzeyi RBAC</span><span class="sxs-lookup"><span data-stu-id="0441d-124">Zone level RBAC</span></span>

<span data-ttu-id="0441d-125">Azure RBAC kuralları, bir abonelik, bir kaynak grubu veya tek başına bir kaynak için uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-125">Azure RBAC rules can be applied to a subscription, a resource group or to an individual resource.</span></span> <span data-ttu-id="0441d-126">Azure DNS söz konusu olduğunda, o kaynak tek tek bir DNS bölgesine veya hatta tek tek bir kayıt kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-126">In the case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="0441d-127">Örneğin, "contoso.com" bölgesi ve CNAME kayıtları her müşteri hesabı için oluşturulan bir'subzone customers.contoso.com' kaynak grubu 'myzones' bulunduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="0441d-127">For example, suppose the resource group 'myzones' contains the zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="0441d-128">Bu CNAME kayıtları yönetmek için kullanılan hesabın yalnızca 'customers.contoso.com' bölgesinde kayıtları oluşturmak için izinlerin atanması, erişim için diğer bölgeler olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="0441d-128">The account used to manage these CNAME records should be assigned permissions to create records in the 'customers.contoso.com' zone only, it should not have access to the other zones.</span></span>

<span data-ttu-id="0441d-129">Bölge düzeyi RBAC izinleri Azure portalı üzerinden verilebilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-129">Zone-level RBAC permissions can be granted via the Azure portal.</span></span>  <span data-ttu-id="0441d-130">Bölge için 'Erişim denetimi (IAM)' dikey penceresini açın, ardından 'Add','ı tıklatın ardından 'DNS bölge katılımcı' rolü seçin ve gerekli kullanıcıları veya grupları izinleri vermek için seçin.</span><span class="sxs-lookup"><span data-stu-id="0441d-130">Open the 'Access control (IAM)' blade for the zone, then click 'Add', then select the 'DNS Zone Contributor' role and select the required users or groups to grant permissions.</span></span>

![Azure Portalı aracılığıyla düzeyi RBAC DNS bölgesi](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="0441d-132">İzinleri de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="0441d-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions to a specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="0441d-133">Eşdeğer ayrıca komuttur [Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="0441d-133">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions to a specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="0441d-134">Kayıt düzeyini RBAC ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0441d-134">Record set level RBAC</span></span>

<span data-ttu-id="0441d-135">Biz bir adım daha fazla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0441d-135">We can go one step further.</span></span> <span data-ttu-id="0441d-136">"Contoso.com" bölgenin tepesinde MX ve TXT kayıtları erişmesi gereken Contoso Corporation, posta Yöneticisi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="0441d-136">Consider the mail administrator for Contoso Corporation, who needs access to the MX and TXT records at the apex of the 'contoso.com' zone.</span></span>  <span data-ttu-id="0441d-137">Aynen diğer MX veya TXT kaydı veya diğer herhangi bir türdeki herhangi bir kayıt erişimi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="0441d-137">She doesn't need access to any other MX or TXT records, or to any records of any other type.</span></span>  <span data-ttu-id="0441d-138">Azure DNS, tam olarak posta yönetici erişmesi kayıtları kayıt kümesi düzeyinde izinler atamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="0441d-138">Azure DNS allows you to assign permissions at the record set level, to precisely the records that the mail administrator needs access to.</span></span>  <span data-ttu-id="0441d-139">Posta yönetici kendisinin gerekir ve başka değişiklikler yapmak alamıyor tam denetim verilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-139">The mail administrator is granted precisely the control she needs, and is unable to make any other changes.</span></span>

<span data-ttu-id="0441d-140">Kayıt kümesi düzeyinde RBAC izinler kayıt kümesi dikey penceresinde 'Kullanıcılar' düğmesini kullanarak Azure Portalı aracılığıyla yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="0441d-140">Record-set level RBAC permissions can be configured via the Azure portal, using the 'Users' button in the record set blade:</span></span>

![Düzey RBAC Azure portalı üzerinden kayıt kümesi](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="0441d-142">Kayıt kümesi düzeyinde RBAC izinler de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="0441d-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions to a specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="0441d-143">Eşdeğer ayrıca komuttur [Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="0441d-143">The equivalent command is also [available via the Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions to a specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="0441d-144">Özel roller</span><span class="sxs-lookup"><span data-stu-id="0441d-144">Custom roles</span></span>

<span data-ttu-id="0441d-145">Yerleşik 'DNS bölge katılımcı' rolü DNS kaynak üzerinde tam denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="0441d-145">The built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="0441d-146">Kendi müşteri bile geçirmiş denetimi sağlamak için Azure rolleri oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0441d-146">It is also possible to build your own customer Azure roles, to provide even finer-grained control.</span></span>

<span data-ttu-id="0441d-147">Yeniden her Contoso Corporation müşteri hesabı için bir CNAME kaydı 'customers.contoso.com' bölgesinde oluşturulduğu örneği göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="0441d-147">Consider again the example in which a CNAME record in the zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="0441d-148">Bu CNAME'ler yönetmek için kullanılan hesabın CNAME kayıtlarına yalnızca yönetme izni verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0441d-148">The account used to manage these CNAMEs should be granted permission to manage CNAME records only.</span></span>  <span data-ttu-id="0441d-149">Ardından, (MX kayıtları değiştirme gibi) diğer türleri kayıtlarını değiştirme veya bölge düzeyinde bölge silme gibi işlemleri gerçekleştirmek alamıyor.</span><span class="sxs-lookup"><span data-stu-id="0441d-149">It is then unable to modify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="0441d-150">Aşağıdaki örnek, CNAME kayıtlarına yalnızca yönetmek için özel rol tanımını gösterir:</span><span class="sxs-lookup"><span data-stu-id="0441d-150">The following example shows a custom role definition for managing CNAME records only:</span></span>

```json
{
    "Name": "DNS CNAME Contributor",
    "Id": "",
    "IsCustom": true,
    "Description": "Can manage DNS CNAME records only.",
    "Actions": [
        "Microsoft.Network/dnsZones/CNAME/*",
        "Microsoft.Network/dnsZones/read",
        "Microsoft.Authorization/*/read",
        "Microsoft.Insights/alertRules/*",
        "Microsoft.ResourceHealth/availabilityStatuses/read",
        "Microsoft.Resources/deployments/*",
        "Microsoft.Resources/subscriptions/resourceGroups/read",
        "Microsoft.Support/*"
    ],
    "NotActions": [
    ],
    "AssignableScopes": [
        "/subscriptions/ c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
}
```

<span data-ttu-id="0441d-151">Eylemler özelliği aşağıdaki DNS özgü izinleri tanımlar:</span><span class="sxs-lookup"><span data-stu-id="0441d-151">The Actions property defines the following DNS-specific permissions:</span></span>

* <span data-ttu-id="0441d-152">`Microsoft.Network/dnsZones/CNAME/*`CNAME kayıtları üzerinde tam denetim verir</span><span class="sxs-lookup"><span data-stu-id="0441d-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="0441d-153">`Microsoft.Network/dnsZones/read`DNS bölgelerini okumak için ancak bunları CNAME oluşturulmaktadır bölge görmenizi etkinleştirme değiştirmek için izin verir.</span><span class="sxs-lookup"><span data-stu-id="0441d-153">`Microsoft.Network/dnsZones/read` grants permission to read DNS zones, but not to modify them, enabling you to see the zone in which the CNAME is being created.</span></span>

<span data-ttu-id="0441d-154">Kalan Eylemler kopyalandığı [DNS bölge katkıda bulunan yerleşik rolü](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="0441d-154">The remaining Actions are copied from the [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="0441d-155">Kayıt kümeleri hala güncelleştirilmesi vermeden etkili bir denetim olmamasına karşın silme engellemek için özel bir RBAC rolü kullanma.</span><span class="sxs-lookup"><span data-stu-id="0441d-155">Using a custom RBAC role to prevent deleting record sets while still allowing them to be updated is not an effective control.</span></span> <span data-ttu-id="0441d-156">Kayıt kümeleri silinmesini engeller, ancak değiştirilen veren'in engel olmaz.</span><span class="sxs-lookup"><span data-stu-id="0441d-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="0441d-157">İzin verilen değişiklikleri ekleme ve kaldırma 'empty' kayıt kümesi bırakmak tüm kayıtları dahil olmak üzere kayıt kümesinden kayıt kaldırma içerir.</span><span class="sxs-lookup"><span data-stu-id="0441d-157">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="0441d-158">Bu kayıt DNS çözümlemesi görüş açısından kümesine silme aynı etkiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0441d-158">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="0441d-159">Özel rol tanımları şu anda Azure portalı üzerinden tanımlanamaz.</span><span class="sxs-lookup"><span data-stu-id="0441d-159">Custom role definitions cannot currently be defined via the Azure portal.</span></span> <span data-ttu-id="0441d-160">Bu rol tanımına dayalı özel bir rol, Azure PowerShell kullanarak oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="0441d-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="0441d-161">Ayrıca Azure CLI oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="0441d-161">It can also be created via the Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="0441d-162">Rol sonra yerleşik roller aynı şekilde bu makalenin önceki bölümlerinde açıklandığı gibi atanabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-162">The role can then be assigned in the same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="0441d-163">Oluşturma, yönetme ve özel roller atama hakkında daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-163">For more information on how to create, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="0441d-164">Kaynak kilitleri</span><span class="sxs-lookup"><span data-stu-id="0441d-164">Resource locks</span></span>

<span data-ttu-id="0441d-165">RBAC yanı sıra, Azure Resource Manager başka bir tür güvenlik denetimi, yani 'lock' Kaynakları özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="0441d-165">In addition to RBAC, Azure Resource Manager supports another type of security control, namely the ability to 'lock' resources.</span></span> <span data-ttu-id="0441d-166">Burada RBAC, denetimine izin verme kuralları belirli kullanıcılar ve gruplar eylemleri, kaynak kilitleri kaynağa uygulanır ve tüm kullanıcılar ve roller etkili olur.</span><span class="sxs-lookup"><span data-stu-id="0441d-166">Where RBAC rules allow you to control the actions of specific users and groups, resource locks are applied to the resource, and are effective across all users and roles.</span></span> <span data-ttu-id="0441d-167">Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="0441d-168">Kaynak kilidi iki tür vardır: **DoNotDelete** ve **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="0441d-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="0441d-169">Bu, bir DNS bölgesine veya tek bir kayıt kümesine uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-169">These can be applied either to a DNS zone, or to an individual record set.</span></span>  <span data-ttu-id="0441d-170">Aşağıdaki bölümlerde birçok yaygın senaryolar ve bunları destekleyen anlatan kaynak kilitleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="0441d-170">The following sections describe several common scenarios, and how to support them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="0441d-171">Tüm değişiklikleri karşı koruma</span><span class="sxs-lookup"><span data-stu-id="0441d-171">Protecting against all changes</span></span>

<span data-ttu-id="0441d-172">Yapılan değişiklikleri önlemek için salt okunur kilit bölgeye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="0441d-172">To prevent any changes being made, apply a ReadOnly lock to the zone.</span></span>  <span data-ttu-id="0441d-173">Bu yeni kayıt kümeleri değiştirilmiş veya silinmiş gelen oluşturulan ve varolan kaydı kümeleri engeller.</span><span class="sxs-lookup"><span data-stu-id="0441d-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="0441d-174">Bölge düzeyi kaynak kilitleri Azure portalı üzerinden oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-174">Zone level resource locks can be created via the Azure portal.</span></span>  <span data-ttu-id="0441d-175">DNS bölge dikey penceresinden 'Kilitleri','ı tıklatın ardından 'Ekle':</span><span class="sxs-lookup"><span data-stu-id="0441d-175">From the DNS zone blade, click 'Locks', then 'Add':</span></span>

![Bölge düzeyi kaynak kilitleri Azure Portalı aracılığıyla](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="0441d-177">Bölge düzeyi kaynak kilitleri Azure PowerShell ile de oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="0441d-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="0441d-178">Azure kaynak kilitleri yapılandırma, Azure CLI şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0441d-178">Configuring Azure resource locks is not currently supported via the Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="0441d-179">Kayıtları tek tek koruma</span><span class="sxs-lookup"><span data-stu-id="0441d-179">Protecting individual records</span></span>

<span data-ttu-id="0441d-180">Var olan bir DNS kayıt karşı değişiklik kümesi önlemek için kayıt kümesi salt okunur kilit uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0441d-180">To prevent an existing DNS record set against modification, apply a ReadOnly lock to the record set.</span></span>

> [!NOTE]
> <span data-ttu-id="0441d-181">Bir kayıt kümesine DoNotDelete kilit uygulama etkin bir denetimi değil.</span><span class="sxs-lookup"><span data-stu-id="0441d-181">Applying a DoNotDelete lock to a record set is not an effective control.</span></span> <span data-ttu-id="0441d-182">Kayıt kümesine silinmesini engeller, ancak bu, değiştirilmesini engellemez.</span><span class="sxs-lookup"><span data-stu-id="0441d-182">It prevents the record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="0441d-183">İzin verilen değişiklikleri ekleme ve kaldırma 'empty' kayıt kümesi bırakmak tüm kayıtları dahil olmak üzere kayıt kümesinden kayıt kaldırma içerir.</span><span class="sxs-lookup"><span data-stu-id="0441d-183">Permitted modifications include adding and removing records from the record set, including removing all records to leave an 'empty' record set.</span></span> <span data-ttu-id="0441d-184">Bu kayıt DNS çözümlemesi görüş açısından kümesine silme aynı etkiye sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0441d-184">This has the same effect as deleting the record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="0441d-185">Kayıt kümesi düzeyi kaynak kilitleri için şu anda yalnızca Azure PowerShell kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0441d-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="0441d-186">Azure portalında veya Azure CLI desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="0441d-186">They are not supported in the Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="0441d-187">Bölge silinmeye karşı koruma</span><span class="sxs-lookup"><span data-stu-id="0441d-187">Protecting against zone deletion</span></span>

<span data-ttu-id="0441d-188">Azure DNS'de bölge silindiğinde, bölgedeki tüm kayıt kümelerinin de silinir.</span><span class="sxs-lookup"><span data-stu-id="0441d-188">When a zone is deleted in Azure DNS, all record sets in the zone are also deleted.</span></span>  <span data-ttu-id="0441d-189">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="0441d-189">This operation cannot be undone.</span></span>  <span data-ttu-id="0441d-190">Kritik bir bölgenin yanlışlıkla silinmesi önemli iş etkisine sahip olma olasılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="0441d-190">Accidentally deleting a critical zone has the potential to have a significant business impact.</span></span>  <span data-ttu-id="0441d-191">Bu nedenle yanlışlıkla bölge silinmeye karşı korumak çok önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0441d-191">It is therefore very important to protect against accidental zone deletion.</span></span>

<span data-ttu-id="0441d-192">Bir bölgeye DoNotDelete kilit uygulama bölge silinmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="0441d-192">Applying a DoNotDelete lock to a zone prevents the zone from being deleted.</span></span>  <span data-ttu-id="0441d-193">Ancak, kilit alt kaynaklar tarafından devralınır olduğundan, ayrıca tüm kayıt kümelerini bölgesinde siliniyor, gelen istenmeyen olabilen engeller.</span><span class="sxs-lookup"><span data-stu-id="0441d-193">However, since locks are inherited by child resources, it also prevents any record sets in the zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="0441d-194">Kayıtları hala mevcut kayıt kümelerinden kaldırılabilir Ayrıca, yukarıdaki not açıklandığı gibi bu da etkisiz olduğu.</span><span class="sxs-lookup"><span data-stu-id="0441d-194">Furthermore, as described in the note above, it is also ineffective since records can still be removed from the existing record sets.</span></span>

<span data-ttu-id="0441d-195">Alternatif olarak, bölgenin SOA kayıt kümesi gibi kümesindeki bir kayda DoNotDelete kilit uygulamayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="0441d-195">As an alternative, consider applying a DoNotDelete lock to a record set in the zone, such as the SOA record set.</span></span>  <span data-ttu-id="0441d-196">Kayıt kümeleri de silmeden bölge silinemiyor olduğundan, bu hala serbestçe değiştirilecek bölge içinde kayıt kümeleri vererek bölge silme korur.</span><span class="sxs-lookup"><span data-stu-id="0441d-196">Since the zone cannot be deleted without also deleting the record sets, this protects against zone deletion, while still allowing record sets within the zone to be modified freely.</span></span> <span data-ttu-id="0441d-197">Bölgeyi silmek için bir girişimde, Azure Resource Manager bunu SOA kayıt kümesi de siler ve SOA kilitlendiğinden çağrı engeller algılar.</span><span class="sxs-lookup"><span data-stu-id="0441d-197">If an attempt is made to delete the zone, Azure Resource Manager detects this would also delete the SOA record set, and blocks the call because the SOA is locked.</span></span>  <span data-ttu-id="0441d-198">Hiçbir kayıt kümelerini silinir.</span><span class="sxs-lookup"><span data-stu-id="0441d-198">No record sets are deleted.</span></span>

<span data-ttu-id="0441d-199">Aşağıdaki PowerShell komutunu verilen bölgenin SOA kaydına karşı DoNotDelete Kilitle oluşturur:</span><span class="sxs-lookup"><span data-stu-id="0441d-199">The following PowerShell command creates a DoNotDelete lock against the SOA record of the given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on the record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="0441d-200">Yanlışlıkla bölge silinmesini önlemek için başka bir işleç emin olmak için özel bir güvenlik rolünü kullanarak yoludur ve bölgelerinizi yönetmek için kullanılan hizmet hesaplarını izinleri bölge yok.</span><span class="sxs-lookup"><span data-stu-id="0441d-200">Another way to prevent accidental zone deletion is by using a custom role to ensure the operator and service accounts used to manage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="0441d-201">Bir bölge silmek gerektiğinde bir iki adımlı silme, ilk izni veriliyor bölge Sil (kapsamındaki izinler yanlış bölgeyi silmeden önlemek için bölge,) ve ikinci bölgeyi silme uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="0441d-201">When you do need to delete a zone, you can enforce a two-step delete, first granting zone delete permissions (at the zone scope, to prevent deleting the wrong zone) and second to delete the zone.</span></span>

<span data-ttu-id="0441d-202">Bu ikinci yaklaşımı kilitleri oluşturmak anımsamak zorunda kalmadan hesaplar tarafından erişilen tüm bölgelerde çalıştığını avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0441d-202">This second approach has the advantage that it works for all zones accessed by those accounts, without having to remember to create any locks.</span></span> <span data-ttu-id="0441d-203">Abonelik sahibi gibi bölge silme izinlerine sahip herhangi bir hesabı kritik bir bölge hala yanlışlıkla silebilirsiniz dezavantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="0441d-203">It has the disadvantage that any accounts with zone delete permissions, such as the subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="0441d-204">Aynı zamanda, savunma yaklaşım DNS bölge koruma için her iki yaklaşımın - kaynak kilitler ve özel roller - kullanmak da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0441d-204">It is possible to use both approaches - resource locks and custom roles - at the same time, as a defense-in-depth approach to DNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0441d-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0441d-205">Next steps</span></span>

* <span data-ttu-id="0441d-206">RBAC ile çalışma hakkında daha fazla bilgi için bkz: [Azure portalında erişim yönetimini kullanmaya başlama](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-206">For more information about working with RBAC, see [Get started with access management in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="0441d-207">Kaynak kilitleri ile çalışma hakkında daha fazla bilgi için bkz: [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0441d-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

