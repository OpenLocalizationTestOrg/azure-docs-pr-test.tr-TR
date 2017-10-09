---
title: "aaaProtecting DNS bölgeleri ve kayıtları | Microsoft Docs"
description: "Nasıl tooprotect DNS bölgeleri ve kaydı, Microsoft Azure DNS'de ayarlar."
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
ms.openlocfilehash: 7945f6240feeed3d79a11d340f9f845e083026ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-dns-zones-and-records"></a><span data-ttu-id="57fb1-103">Nasıl tooprotect DNS bölgeleri ve kaydeder</span><span class="sxs-lookup"><span data-stu-id="57fb1-103">How tooprotect DNS zones and records</span></span>

<span data-ttu-id="57fb1-104">DNS bölgeleri ve kayıtları kritik kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="57fb1-104">DNS zones and records are critical resources.</span></span> <span data-ttu-id="57fb1-105">Bir DNS bölgesine veya bile yalnızca tek bir DNS kaydı silinirken bir toplam hizmet kesintisine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-105">Deleting a DNS zone or even just a single DNS record can result in a total service outage.</span></span>  <span data-ttu-id="57fb1-106">Bu nedenle kritik DNS bölgeleri ve kayıtları yetkisiz veya yanlışlıkla değişikliklere karşı korumalı önemlidir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-106">It is therefore important that critical DNS zones and records are protected against unauthorized or accidental changes.</span></span>

<span data-ttu-id="57fb1-107">Bu makalede, DNS bölgeleri ve bu değişikliklere karşı kayıtları Azure DNS, tooprotect nasıl sağladığını açıklar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-107">This article explains how Azure DNS enables you tooprotect your DNS zones and records against such changes.</span></span>  <span data-ttu-id="57fb1-108">Biz Azure Resource Manager tarafından sağlanan iki güçlü güvenlik özelliklerini uygulayın: [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) ve [kaynak kilitleri](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-108">We apply two powerful security features provided by Azure Resource Manager: [role-based access control](../active-directory/role-based-access-control-what-is.md) and [resource locks](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="57fb1-109">Rol tabanlı erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="57fb1-109">Role-based access control</span></span>

<span data-ttu-id="57fb1-110">Azure rol tabanlı erişim denetimi (RBAC) Azure kullanıcıları, grupları ve kaynakları için ayrıntılı erişim yönetimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-110">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure users, groups, and resources.</span></span> <span data-ttu-id="57fb1-111">RBAC kullanarak, kullanıcıların işlerini tooperform gereken kesin olarak hello erişim miktarını verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57fb1-111">Using RBAC, you can grant precisely hello amount of access that users need tooperform their jobs.</span></span> <span data-ttu-id="57fb1-112">RBAC erişimi yönetmenize nasıl yardımcı olduğunu hakkında daha fazla bilgi için bkz: [rol tabanlı erişim denetimi nedir](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-112">For more information about how RBAC helps you manage access, see [What is Role-Based Access Control](../active-directory/role-based-access-control-what-is.md).</span></span>

### <a name="hello-dns-zone-contributor-role"></a><span data-ttu-id="57fb1-113">Merhaba 'DNS bölge katkıda bulunan' rolü</span><span class="sxs-lookup"><span data-stu-id="57fb1-113">hello 'DNS Zone Contributor' role</span></span>

<span data-ttu-id="57fb1-114">Merhaba 'DNS bölge katkıda bulunan' rol DNS kaynakları yönetmek için Azure tarafından sağlanan yerleşik bir roldür.</span><span class="sxs-lookup"><span data-stu-id="57fb1-114">hello 'DNS Zone Contributor' role is a built-in role provided by Azure for managing DNS resources.</span></span>  <span data-ttu-id="57fb1-115">DNS bölge katkıda bulunan izinleri tooa kullanıcı veya grup atama, bu Grup toomanage DNS kaynakları, ancak kaynakları diğer herhangi bir tür değil sağlar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-115">Assigning DNS Zone Contributor permissions tooa user or group enables that group toomanage DNS resources, but not resources of any other type.</span></span>

<span data-ttu-id="57fb1-116">Örneğin, Contoso Corporation için beş bölgeleri hello kaynak grubu 'myzones' içeren varsayalım.</span><span class="sxs-lookup"><span data-stu-id="57fb1-116">For example, suppose hello resource group 'myzones' contains five zones for Contoso Corporation.</span></span> <span data-ttu-id="57fb1-117">İzni veriliyor hello DNS Yöneticisi 'DNS bölge katkıda bulunan' izinleri toothat kaynak grubu, bu DNS bölgeleri üzerinde tam denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-117">Granting hello DNS administrator 'DNS Zone Contributor' permissions toothat resource group, enables full control over those DNS zones.</span></span> <span data-ttu-id="57fb1-118">Ayrıca, örneğin hello DNS Yöneticisi oluşturun veya sanal makineleri durdurmayı gereksiz izinleri verme önler.</span><span class="sxs-lookup"><span data-stu-id="57fb1-118">It also avoids granting unnecessary permissions, for example hello DNS administrator cannot create or stop Virtual Machines.</span></span>

<span data-ttu-id="57fb1-119">Merhaba en basit yolu tooassign RBAC izinleri [hello Azure portal aracılığıyla](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-119">hello simplest way tooassign RBAC permissions is [via hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>  <span data-ttu-id="57fb1-120">Merhaba 'erişim denetimi (IAM)' hello kaynak grubu dikey penceresini açmak 'Ekle'yi tıklatın, sonra hello 'DNS bölge katkıda bulunan' rolü ve select hello gerekli kullanıcı veya grup toogrant izinleri seçin.</span><span class="sxs-lookup"><span data-stu-id="57fb1-120">Open hello 'Access control (IAM)' blade for hello resource group, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![Kaynak grubu düzeyinde RBAC hello Azure portal aracılığıyla](./media/dns-protect-zones-recordsets/rbac1.png)

<span data-ttu-id="57fb1-122">İzinleri de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="57fb1-122">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="57fb1-123">Merhaba eşdeğer komutu [hello Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="57fb1-123">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a><span data-ttu-id="57fb1-124">Bölge düzeyi RBAC</span><span class="sxs-lookup"><span data-stu-id="57fb1-124">Zone level RBAC</span></span>

<span data-ttu-id="57fb1-125">Azure RBAC kuralları uygulanan tooa abonelik olabilir bir kaynak grubu veya tooan tek tek kaynak.</span><span class="sxs-lookup"><span data-stu-id="57fb1-125">Azure RBAC rules can be applied tooa subscription, a resource group or tooan individual resource.</span></span> <span data-ttu-id="57fb1-126">Azure DNS Hello durumda o kaynak tek tek bir DNS bölgesine veya hatta tek tek bir kayıt kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-126">In hello case of Azure DNS, that resource can be an individual DNS zone, or even an individual record set.</span></span>

<span data-ttu-id="57fb1-127">Örneğin, contoso.com' hello bölgesindeki' ve 'CNAME kayıtları her müşteri hesabı için oluşturulan subzone customers.contoso.com' hello kaynak grubu 'myzones' bulunduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="57fb1-127">For example, suppose hello resource group 'myzones' contains hello zone 'contoso.com' and a subzone 'customers.contoso.com' in which CNAME records are created for each customer account.</span></span>  <span data-ttu-id="57fb1-128">Merhaba kullanılan hesap toomanage izinleri toocreate bölgedeki kayıtları hello 'customers.contoso.com' yalnızca bu CNAME kayıtları atanmalıdır, erişim toohello diğer bölgelerdeki olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="57fb1-128">hello account used toomanage these CNAME records should be assigned permissions toocreate records in hello 'customers.contoso.com' zone only, it should not have access toohello other zones.</span></span>

<span data-ttu-id="57fb1-129">Bölge düzeyi RBAC izinleri hello Azure portal verilebilir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-129">Zone-level RBAC permissions can be granted via hello Azure portal.</span></span>  <span data-ttu-id="57fb1-130">Merhaba bölge Hello 'Erişim denetimi (IAM)' dikey penceresini açmak 'Ekle'yi tıklatın, sonra hello 'DNS bölge katkıda bulunan' rolü ve select hello gerekli kullanıcı veya grup toogrant izinleri seçin.</span><span class="sxs-lookup"><span data-stu-id="57fb1-130">Open hello 'Access control (IAM)' blade for hello zone, then click 'Add', then select hello 'DNS Zone Contributor' role and select hello required users or groups toogrant permissions.</span></span>

![DNS bölgesi düzeyi RBAC hello Azure portal aracılığıyla](./media/dns-protect-zones-recordsets/rbac2.png)

<span data-ttu-id="57fb1-132">İzinleri de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="57fb1-132">Permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

<span data-ttu-id="57fb1-133">Merhaba eşdeğer komutu [hello Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="57fb1-133">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a><span data-ttu-id="57fb1-134">Kayıt düzeyini RBAC ayarlayın</span><span class="sxs-lookup"><span data-stu-id="57fb1-134">Record set level RBAC</span></span>

<span data-ttu-id="57fb1-135">Biz bir adım daha fazla gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57fb1-135">We can go one step further.</span></span> <span data-ttu-id="57fb1-136">Erişim toohello MX ve TXT kayıtları hello "contoso.com" bölgesi hello tepesinde duyan Merhaba posta yönetici Contoso Corporation için göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="57fb1-136">Consider hello mail administrator for Contoso Corporation, who needs access toohello MX and TXT records at hello apex of hello 'contoso.com' zone.</span></span>  <span data-ttu-id="57fb1-137">Aynen tooany diğer MX veya TXT kaydı veya diğer herhangi bir tür tooany kayıtları erişim değil.</span><span class="sxs-lookup"><span data-stu-id="57fb1-137">She doesn't need access tooany other MX or TXT records, or tooany records of any other type.</span></span>  <span data-ttu-id="57fb1-138">Azure DNS, posta yönetici hello hello kayıt kümesi düzeyi, tooprecisely hello kayıtlarını tooassign izinleri erişmesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-138">Azure DNS allows you tooassign permissions at hello record set level, tooprecisely hello records that hello mail administrator needs access to.</span></span>  <span data-ttu-id="57fb1-139">Merhaba posta yönetici tam olarak hello denetim verilir kendisinin gerekir ve oluşturulamıyor toomake başka herhangi bir değişiklik değil.</span><span class="sxs-lookup"><span data-stu-id="57fb1-139">hello mail administrator is granted precisely hello control she needs, and is unable toomake any other changes.</span></span>

<span data-ttu-id="57fb1-140">Kayıt kümesi düzeyinde RBAC izinler hello hello kayıt kümesi dikey penceresinde hello 'kullanıcılar' düğmesini kullanarak Azure portal aracılığıyla yapılandırılabilir:</span><span class="sxs-lookup"><span data-stu-id="57fb1-140">Record-set level RBAC permissions can be configured via hello Azure portal, using hello 'Users' button in hello record set blade:</span></span>

![Kayıt hello Azure portal aracılığıyla RBAC düzeyini ayarlayın](./media/dns-protect-zones-recordsets/rbac3.png)

<span data-ttu-id="57fb1-142">Kayıt kümesi düzeyinde RBAC izinler de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="57fb1-142">Record-set level RBAC permissions can also be [granted using Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md):</span></span>

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

<span data-ttu-id="57fb1-143">Merhaba eşdeğer komutu [hello Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span><span class="sxs-lookup"><span data-stu-id="57fb1-143">hello equivalent command is also [available via hello Azure CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md):</span></span>

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a><span data-ttu-id="57fb1-144">Özel roller</span><span class="sxs-lookup"><span data-stu-id="57fb1-144">Custom roles</span></span>

<span data-ttu-id="57fb1-145">Merhaba yerleşik 'DNS bölge katkıda bulunan' rolü DNS kaynak üzerinde tam denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-145">hello built-in 'DNS Zone Contributor' role enables full control over a DNS resource.</span></span> <span data-ttu-id="57fb1-146">Bu da olası toobuild müşteri Azure olan roller, tooprovide bile geçirmiş denetim.</span><span class="sxs-lookup"><span data-stu-id="57fb1-146">It is also possible toobuild your own customer Azure roles, tooprovide even finer-grained control.</span></span>

<span data-ttu-id="57fb1-147">Yeniden her Contoso Corporation müşteri hesabı için bir CNAME kaydı hello bölge 'customers.contoso.com' ın oluşturulduğu hello örneği göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="57fb1-147">Consider again hello example in which a CNAME record in hello zone 'customers.contoso.com' is created for each Contoso Corporation customer account.</span></span>  <span data-ttu-id="57fb1-148">Hello kullanılan hesap toomanage izni toomanage CNAME kayıtlarına yalnızca bu CNAME'ler verilmelidir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-148">hello account used toomanage these CNAMEs should be granted permission toomanage CNAME records only.</span></span>  <span data-ttu-id="57fb1-149">Diğer oluşturulamıyor toomodify kayıtları (MX kayıtları değiştirme gibi) türleri veya bölge düzeyinde bölge silme gibi işlemleri sonra bu olur.</span><span class="sxs-lookup"><span data-stu-id="57fb1-149">It is then unable toomodify records of other types (such as changing MX records) or perform zone-level operations such as zone delete.</span></span>

<span data-ttu-id="57fb1-150">Aşağıdaki örneğine hello CNAME kayıtlarına yalnızca yönetmek için özel rol tanımını gösterir:</span><span class="sxs-lookup"><span data-stu-id="57fb1-150">hello following example shows a custom role definition for managing CNAME records only:</span></span>

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

<span data-ttu-id="57fb1-151">Merhaba Eylemler özelliği aşağıdaki DNS özel izinleri hello tanımlar:</span><span class="sxs-lookup"><span data-stu-id="57fb1-151">hello Actions property defines hello following DNS-specific permissions:</span></span>

* <span data-ttu-id="57fb1-152">`Microsoft.Network/dnsZones/CNAME/*`CNAME kayıtları üzerinde tam denetim verir</span><span class="sxs-lookup"><span data-stu-id="57fb1-152">`Microsoft.Network/dnsZones/CNAME/*` grants full control over CNAME records</span></span>
* <span data-ttu-id="57fb1-153">`Microsoft.Network/dnsZones/read`izni tooread DNS bölgeleri, ancak bunları, toosee etkinleştirme hangi hello CNAME oluşturulan bölge hello toomodify verir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-153">`Microsoft.Network/dnsZones/read` grants permission tooread DNS zones, but not toomodify them, enabling you toosee hello zone in which hello CNAME is being created.</span></span>

<span data-ttu-id="57fb1-154">Kalan Eylemler hello kopyalanan hello [DNS bölge katkıda bulunan yerleşik rolü](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span><span class="sxs-lookup"><span data-stu-id="57fb1-154">hello remaining Actions are copied from hello [DNS Zone Contributor built-in role](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).</span></span>

> [!NOTE]
> <span data-ttu-id="57fb1-155">Hala güncelleştirilmiş toobe izin vererek etkili bir denetim olmamasına karşın kaydı silinirken bir özel RBAC rolü tooprevent kullanarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-155">Using a custom RBAC role tooprevent deleting record sets while still allowing them toobe updated is not an effective control.</span></span> <span data-ttu-id="57fb1-156">Kayıt kümeleri silinmesini engeller, ancak değiştirilen veren'in engel olmaz.</span><span class="sxs-lookup"><span data-stu-id="57fb1-156">It prevents record sets from being deleted, but it does not prevent them from being modified.</span></span>  <span data-ttu-id="57fb1-157">İzin verilen değişiklikleri eklenmesi ve tüm kaldırma dahil olmak üzere hello kayıt kümesinden kayıt kaldırma tooleave 'empty' kayıt kümesi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="57fb1-157">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="57fb1-158">Bu DNS çözümlemesi görüş açısından hello kayıt silme aynı etkiye ayarlamak hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-158">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="57fb1-159">Özel rol tanımları şu anda hello Azure portal tanımlanamaz.</span><span class="sxs-lookup"><span data-stu-id="57fb1-159">Custom role definitions cannot currently be defined via hello Azure portal.</span></span> <span data-ttu-id="57fb1-160">Bu rol tanımına dayalı özel bir rol, Azure PowerShell kullanarak oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="57fb1-160">A custom role based on this role definition can be created using Azure PowerShell:</span></span>

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

<span data-ttu-id="57fb1-161">Ayrıca hello Azure CLI oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="57fb1-161">It can also be created via hello Azure CLI:</span></span>

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

<span data-ttu-id="57fb1-162">Merhaba rolü sonra hello aynı atanabilir şekilde yerleşik roller olarak bu makalenin önceki bölümlerinde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="57fb1-162">hello role can then be assigned in hello same way as built-in roles, as described earlier in this article.</span></span>

<span data-ttu-id="57fb1-163">Nasıl toocreate, yönetmek ve özel roller atama hakkında daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-163">For more information on how toocreate, manage, and assign custom roles, see [Custom Roles in Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).</span></span>

## <a name="resource-locks"></a><span data-ttu-id="57fb1-164">Kaynak kilitleri</span><span class="sxs-lookup"><span data-stu-id="57fb1-164">Resource locks</span></span>

<span data-ttu-id="57fb1-165">Toplama tooRBAC içinde başka bir tür güvenlik denetimi, hello özelliği too'lock Azure Resource Manager destekler ' kaynakları.</span><span class="sxs-lookup"><span data-stu-id="57fb1-165">In addition tooRBAC, Azure Resource Manager supports another type of security control, namely hello ability too'lock' resources.</span></span> <span data-ttu-id="57fb1-166">RBAC kuralları belirli kullanıcılar ve gruplar toocontrol hello eylemlerini izin burada kaynak kilitleri uygulanan toohello kaynaktır ve tüm kullanıcılar ve roller etkili olur.</span><span class="sxs-lookup"><span data-stu-id="57fb1-166">Where RBAC rules allow you toocontrol hello actions of specific users and groups, resource locks are applied toohello resource, and are effective across all users and roles.</span></span> <span data-ttu-id="57fb1-167">Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-167">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

<span data-ttu-id="57fb1-168">Kaynak kilidi iki tür vardır: **DoNotDelete** ve **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="57fb1-168">There are two types of resource lock: **DoNotDelete** and **ReadOnly**.</span></span> <span data-ttu-id="57fb1-169">Bunlar uygulanabilir tooa DNS bölgesine veya tooan tek tek kayıt kümesi.</span><span class="sxs-lookup"><span data-stu-id="57fb1-169">These can be applied either tooa DNS zone, or tooan individual record set.</span></span>  <span data-ttu-id="57fb1-170">Merhaba aşağıdaki bölümlerde açıklanmaktadır birçok yaygın senaryolar ve nasıl toosupport bunları kaynak kilitleri kullanma.</span><span class="sxs-lookup"><span data-stu-id="57fb1-170">hello following sections describe several common scenarios, and how toosupport them using resource locks.</span></span>

### <a name="protecting-against-all-changes"></a><span data-ttu-id="57fb1-171">Tüm değişiklikleri karşı koruma</span><span class="sxs-lookup"><span data-stu-id="57fb1-171">Protecting against all changes</span></span>

<span data-ttu-id="57fb1-172">tooprevent salt okunur kilit toohello bölge geçerli herhangi bir değişiklik yapılan.</span><span class="sxs-lookup"><span data-stu-id="57fb1-172">tooprevent any changes being made, apply a ReadOnly lock toohello zone.</span></span>  <span data-ttu-id="57fb1-173">Bu yeni kayıt kümeleri değiştirilmiş veya silinmiş gelen oluşturulan ve varolan kaydı kümeleri engeller.</span><span class="sxs-lookup"><span data-stu-id="57fb1-173">This prevents new record sets from being created, and existing record sets from being modified or deleted.</span></span>

<span data-ttu-id="57fb1-174">Bölge düzeyi kaynak kilitleri hello Azure portal oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-174">Zone level resource locks can be created via hello Azure portal.</span></span>  <span data-ttu-id="57fb1-175">'Kilitleri' Hello DNS bölge dikey penceresinden tıklayın ardından 'Ekle':</span><span class="sxs-lookup"><span data-stu-id="57fb1-175">From hello DNS zone blade, click 'Locks', then 'Add':</span></span>

![Bölge düzeyi kaynak kilitleri hello Azure portal aracılığıyla](./media/dns-protect-zones-recordsets/locks1.png)

<span data-ttu-id="57fb1-177">Bölge düzeyi kaynak kilitleri Azure PowerShell ile de oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="57fb1-177">Zone-level resource locks can also be created via Azure PowerShell:</span></span>

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

<span data-ttu-id="57fb1-178">Azure kaynak kilitleri yapılandırma hello Azure CLI şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="57fb1-178">Configuring Azure resource locks is not currently supported via hello Azure CLI.</span></span>

### <a name="protecting-individual-records"></a><span data-ttu-id="57fb1-179">Kayıtları tek tek koruma</span><span class="sxs-lookup"><span data-stu-id="57fb1-179">Protecting individual records</span></span>

<span data-ttu-id="57fb1-180">tooprevent değişikliği karşı ayarlamak varolan bir DNS kaydı ReadOnly kilit toohello kayıt kümesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="57fb1-180">tooprevent an existing DNS record set against modification, apply a ReadOnly lock toohello record set.</span></span>

> [!NOTE]
> <span data-ttu-id="57fb1-181">DoNotDelete kilit tooa uygulama kayıt kümesi etkili bir denetim değil.</span><span class="sxs-lookup"><span data-stu-id="57fb1-181">Applying a DoNotDelete lock tooa record set is not an effective control.</span></span> <span data-ttu-id="57fb1-182">Merhaba kayıt silinmesini kümesi engeller, ancak bu, değiştirilmesini engellemez.</span><span class="sxs-lookup"><span data-stu-id="57fb1-182">It prevents hello record set from being deleted, but it does not prevent it from being modified.</span></span>  <span data-ttu-id="57fb1-183">İzin verilen değişiklikleri eklenmesi ve tüm kaldırma dahil olmak üzere hello kayıt kümesinden kayıt kaldırma tooleave 'empty' kayıt kümesi kaydeder.</span><span class="sxs-lookup"><span data-stu-id="57fb1-183">Permitted modifications include adding and removing records from hello record set, including removing all records tooleave an 'empty' record set.</span></span> <span data-ttu-id="57fb1-184">Bu DNS çözümlemesi görüş açısından hello kayıt silme aynı etkiye ayarlamak hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-184">This has hello same effect as deleting hello record set from a DNS resolution viewpoint.</span></span>

<span data-ttu-id="57fb1-185">Kayıt kümesi düzeyi kaynak kilitleri için şu anda yalnızca Azure PowerShell kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="57fb1-185">Record set level resource locks can currently only be configured using Azure PowerShell.</span></span>  <span data-ttu-id="57fb1-186">Hello Azure portalında veya Azure CLI desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="57fb1-186">They are not supported in hello Azure portal or Azure CLI.</span></span>

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a><span data-ttu-id="57fb1-187">Bölge silinmeye karşı koruma</span><span class="sxs-lookup"><span data-stu-id="57fb1-187">Protecting against zone deletion</span></span>

<span data-ttu-id="57fb1-188">Azure DNS'de bölge silindiğinde, hello bölgedeki tüm kayıt kümelerinin de silinir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-188">When a zone is deleted in Azure DNS, all record sets in hello zone are also deleted.</span></span>  <span data-ttu-id="57fb1-189">Bu işlem geri alınamaz.</span><span class="sxs-lookup"><span data-stu-id="57fb1-189">This operation cannot be undone.</span></span>  <span data-ttu-id="57fb1-190">Kritik bir bölgenin yanlışlıkla silinmesi hello olası toohave önemli iş etkisine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-190">Accidentally deleting a critical zone has hello potential toohave a significant business impact.</span></span>  <span data-ttu-id="57fb1-191">Bu nedenle, yanlışlıkla bölge silinmesine karşı çok önemli tooprotect olur.</span><span class="sxs-lookup"><span data-stu-id="57fb1-191">It is therefore very important tooprotect against accidental zone deletion.</span></span>

<span data-ttu-id="57fb1-192">Bir DoNotDelete kilit tooa bölge uygulama hello bölge silinmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="57fb1-192">Applying a DoNotDelete lock tooa zone prevents hello zone from being deleted.</span></span>  <span data-ttu-id="57fb1-193">Ancak, kilit alt kaynaklar tarafından devralınır olduğundan, ayrıca tüm kayıt kümelerini istenmeyen olabilen siliniyor, gelen hello bölgesinde engeller.</span><span class="sxs-lookup"><span data-stu-id="57fb1-193">However, since locks are inherited by child resources, it also prevents any record sets in hello zone from being deleted, which may be undesirable.</span></span>  <span data-ttu-id="57fb1-194">Kayıtları hala hello mevcut kayıt kümelerinden kaldırılabilir beri Ayrıca, Not hello yukarıda açıklandığı gibi de etkisiz olabilir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-194">Furthermore, as described in hello note above, it is also ineffective since records can still be removed from hello existing record sets.</span></span>

<span data-ttu-id="57fb1-195">Alternatif olarak, bir DoNotDelete kilit tooa kaydı uygulama hello SOA kayıt kümesi gibi hello bölge kümesindeki. göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="57fb1-195">As an alternative, consider applying a DoNotDelete lock tooa record set in hello zone, such as hello SOA record set.</span></span>  <span data-ttu-id="57fb1-196">Ayrıca hello kayıt kümelerini silmeden Hello bölge silinemiyor olduğundan, bu kayıt kümelerini serbestçe değiştiren hello bölge toobe içinde hala verirken bölge silme korur.</span><span class="sxs-lookup"><span data-stu-id="57fb1-196">Since hello zone cannot be deleted without also deleting hello record sets, this protects against zone deletion, while still allowing record sets within hello zone toobe modified freely.</span></span> <span data-ttu-id="57fb1-197">Girişimde toodelete hello bölge, Azure Resource Manager bu aynı zamanda hello SOA kayıt kümesi siler ve hello SOA kilitlendiğinden blokları çağrısı hello algılar.</span><span class="sxs-lookup"><span data-stu-id="57fb1-197">If an attempt is made toodelete hello zone, Azure Resource Manager detects this would also delete hello SOA record set, and blocks hello call because hello SOA is locked.</span></span>  <span data-ttu-id="57fb1-198">Hiçbir kayıt kümelerini silinir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-198">No record sets are deleted.</span></span>

<span data-ttu-id="57fb1-199">PowerShell komutunu aşağıdaki hello hello SOA kaydına hello bölge verilen karşı DoNotDelete Kilitle oluşturur:</span><span class="sxs-lookup"><span data-stu-id="57fb1-199">hello following PowerShell command creates a DoNotDelete lock against hello SOA record of hello given zone:</span></span>

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

<span data-ttu-id="57fb1-200">Başka bir yolu bir özel rol tooensure hello işleci ve hizmet kullanılan hesaplar toomanage bölgelerinizi değil sahip bölge kullanmaktır tooprevent yanlışlıkla bölge silme izinleri silin.</span><span class="sxs-lookup"><span data-stu-id="57fb1-200">Another way tooprevent accidental zone deletion is by using a custom role tooensure hello operator and service accounts used toomanage your zones do not have zone delete permissions.</span></span> <span data-ttu-id="57fb1-201">Toodelete bir bölge gerektiğinde, iki aşamalı silme, ilk izni veriliyor bölge Sil (kapsamındaki izinler hello bölge, hello yanlış bölgeyi silmeden tooprevent) uygulayabilir ve ikinci toodelete hello bölgesi.</span><span class="sxs-lookup"><span data-stu-id="57fb1-201">When you do need toodelete a zone, you can enforce a two-step delete, first granting zone delete permissions (at hello zone scope, tooprevent deleting hello wrong zone) and second toodelete hello zone.</span></span>

<span data-ttu-id="57fb1-202">Bu ikinci yaklaşımı kilitleri tooremember toocreate gerek kalmadan bu hesapları tarafından erişilen tüm bölgelerde çalıştığını hello avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="57fb1-202">This second approach has hello advantage that it works for all zones accessed by those accounts, without having tooremember toocreate any locks.</span></span> <span data-ttu-id="57fb1-203">Hello abonelik sahibi gibi bölge silme izinlerine sahip herhangi bir hesabı kritik bir bölge hala yanlışlıkla silebilirsiniz hello dezavantajı vardır.</span><span class="sxs-lookup"><span data-stu-id="57fb1-203">It has hello disadvantage that any accounts with zone delete permissions, such as hello subscription owner, can still accidentally delete a critical zone.</span></span>

<span data-ttu-id="57fb1-204">Olası toouse olan her iki yaklaşımın - kaynak kilitler ve özel roller - hello adresindeki aynı zaman, bir savunma yaklaşım tooDNS bölge koruma.</span><span class="sxs-lookup"><span data-stu-id="57fb1-204">It is possible toouse both approaches - resource locks and custom roles - at hello same time, as a defense-in-depth approach tooDNS zone protection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57fb1-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57fb1-205">Next steps</span></span>

* <span data-ttu-id="57fb1-206">RBAC ile çalışma hakkında daha fazla bilgi için bkz: [hello Azure portalına erişim yönetimi kullanmaya başlama](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-206">For more information about working with RBAC, see [Get started with access management in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>
* <span data-ttu-id="57fb1-207">Kaynak kilitleri ile çalışma hakkında daha fazla bilgi için bkz: [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="57fb1-207">For more information about working with resource locks, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

