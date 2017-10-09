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
# <a name="how-tooprotect-dns-zones-and-records"></a>Nasıl tooprotect DNS bölgeleri ve kaydeder

DNS bölgeleri ve kayıtları kritik kaynaklardır. Bir DNS bölgesine veya bile yalnızca tek bir DNS kaydı silinirken bir toplam hizmet kesintisine neden olabilir.  Bu nedenle kritik DNS bölgeleri ve kayıtları yetkisiz veya yanlışlıkla değişikliklere karşı korumalı önemlidir.

Bu makalede, DNS bölgeleri ve bu değişikliklere karşı kayıtları Azure DNS, tooprotect nasıl sağladığını açıklar.  Biz Azure Resource Manager tarafından sağlanan iki güçlü güvenlik özelliklerini uygulayın: [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) ve [kaynak kilitleri](../azure-resource-manager/resource-group-lock-resources.md).

## <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi

Azure rol tabanlı erişim denetimi (RBAC) Azure kullanıcıları, grupları ve kaynakları için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, kullanıcıların işlerini tooperform gereken kesin olarak hello erişim miktarını verebilirsiniz. RBAC erişimi yönetmenize nasıl yardımcı olduğunu hakkında daha fazla bilgi için bkz: [rol tabanlı erişim denetimi nedir](../active-directory/role-based-access-control-what-is.md).

### <a name="hello-dns-zone-contributor-role"></a>Merhaba 'DNS bölge katkıda bulunan' rolü

Merhaba 'DNS bölge katkıda bulunan' rol DNS kaynakları yönetmek için Azure tarafından sağlanan yerleşik bir roldür.  DNS bölge katkıda bulunan izinleri tooa kullanıcı veya grup atama, bu Grup toomanage DNS kaynakları, ancak kaynakları diğer herhangi bir tür değil sağlar.

Örneğin, Contoso Corporation için beş bölgeleri hello kaynak grubu 'myzones' içeren varsayalım. İzni veriliyor hello DNS Yöneticisi 'DNS bölge katkıda bulunan' izinleri toothat kaynak grubu, bu DNS bölgeleri üzerinde tam denetim sağlar. Ayrıca, örneğin hello DNS Yöneticisi oluşturun veya sanal makineleri durdurmayı gereksiz izinleri verme önler.

Merhaba en basit yolu tooassign RBAC izinleri [hello Azure portal aracılığıyla](../active-directory/role-based-access-control-configure.md).  Merhaba 'erişim denetimi (IAM)' hello kaynak grubu dikey penceresini açmak 'Ekle'yi tıklatın, sonra hello 'DNS bölge katkıda bulunan' rolü ve select hello gerekli kullanıcı veya grup toogrant izinleri seçin.

![Kaynak grubu düzeyinde RBAC hello Azure portal aracılığıyla](./media/dns-protect-zones-recordsets/rbac1.png)

İzinleri de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>"
```

Merhaba eşdeğer komutu [hello Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooall zones in a resource group
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --resourceGroup "<resource group name>"
```

### <a name="zone-level-rbac"></a>Bölge düzeyi RBAC

Azure RBAC kuralları uygulanan tooa abonelik olabilir bir kaynak grubu veya tooan tek tek kaynak. Azure DNS Hello durumda o kaynak tek tek bir DNS bölgesine veya hatta tek tek bir kayıt kümesi olabilir.

Örneğin, contoso.com' hello bölgesindeki' ve 'CNAME kayıtları her müşteri hesabı için oluşturulan subzone customers.contoso.com' hello kaynak grubu 'myzones' bulunduğunu varsayın.  Merhaba kullanılan hesap toomanage izinleri toocreate bölgedeki kayıtları hello 'customers.contoso.com' yalnızca bu CNAME kayıtları atanmalıdır, erişim toohello diğer bölgelerdeki olmamalıdır.

Bölge düzeyi RBAC izinleri hello Azure portal verilebilir.  Merhaba bölge Hello 'Erişim denetimi (IAM)' dikey penceresini açmak 'Ekle'yi tıklatın, sonra hello 'DNS bölge katkıda bulunan' rolü ve select hello gerekli kullanıcı veya grup toogrant izinleri seçin.

![DNS bölgesi düzeyi RBAC hello Azure portal aracılığıyla](./media/dns-protect-zones-recordsets/rbac2.png)

İzinleri de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant 'DNS Zone Contributor' permissions tooa specific zone
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -ResourceGroupName "<resource group name>" -ResourceName "<zone name>" -ResourceType Microsoft.Network/DNSZones
```

Merhaba eşdeğer komutu [hello Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant 'DNS Zone Contributor' permissions tooa specific zone
azure role assignment create --signInName <user email address> --roleName "DNS Zone Contributor" --resource-name <zone name> --resource-type Microsoft.Network/DNSZones --resource-group <resource group name>
```

### <a name="record-set-level-rbac"></a>Kayıt düzeyini RBAC ayarlayın

Biz bir adım daha fazla gidebilirsiniz. Erişim toohello MX ve TXT kayıtları hello "contoso.com" bölgesi hello tepesinde duyan Merhaba posta yönetici Contoso Corporation için göz önünde bulundurun.  Aynen tooany diğer MX veya TXT kaydı veya diğer herhangi bir tür tooany kayıtları erişim değil.  Azure DNS, posta yönetici hello hello kayıt kümesi düzeyi, tooprecisely hello kayıtlarını tooassign izinleri erişmesi sağlar.  Merhaba posta yönetici tam olarak hello denetim verilir kendisinin gerekir ve oluşturulamıyor toomake başka herhangi bir değişiklik değil.

Kayıt kümesi düzeyinde RBAC izinler hello hello kayıt kümesi dikey penceresinde hello 'kullanıcılar' düğmesini kullanarak Azure portal aracılığıyla yapılandırılabilir:

![Kayıt hello Azure portal aracılığıyla RBAC düzeyini ayarlayın](./media/dns-protect-zones-recordsets/rbac3.png)

Kayıt kümesi düzeyinde RBAC izinler de olabilir [Azure PowerShell kullanarak verilen](../active-directory/role-based-access-control-manage-access-powershell.md):

```powershell
# Grant permissions tooa specific record set
New-AzureRmRoleAssignment -SignInName "<user email address>" -RoleDefinitionName "DNS Zone Contributor" -Scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

Merhaba eşdeğer komutu [hello Azure CLI aracılığıyla kullanılabilen](../active-directory/role-based-access-control-manage-access-azure-cli.md):

```azurecli
# Grant permissions tooa specific record set
azure role assignment create --signInName "<user email address>" --roleName "DNS Zone Contributor" --scope "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/dnszones/<zone name>/<record type>/<record name>"
```

### <a name="custom-roles"></a>Özel roller

Merhaba yerleşik 'DNS bölge katkıda bulunan' rolü DNS kaynak üzerinde tam denetim sağlar. Bu da olası toobuild müşteri Azure olan roller, tooprovide bile geçirmiş denetim.

Yeniden her Contoso Corporation müşteri hesabı için bir CNAME kaydı hello bölge 'customers.contoso.com' ın oluşturulduğu hello örneği göz önünde bulundurun.  Hello kullanılan hesap toomanage izni toomanage CNAME kayıtlarına yalnızca bu CNAME'ler verilmelidir.  Diğer oluşturulamıyor toomodify kayıtları (MX kayıtları değiştirme gibi) türleri veya bölge düzeyinde bölge silme gibi işlemleri sonra bu olur.

Aşağıdaki örneğine hello CNAME kayıtlarına yalnızca yönetmek için özel rol tanımını gösterir:

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

Merhaba Eylemler özelliği aşağıdaki DNS özel izinleri hello tanımlar:

* `Microsoft.Network/dnsZones/CNAME/*`CNAME kayıtları üzerinde tam denetim verir
* `Microsoft.Network/dnsZones/read`izni tooread DNS bölgeleri, ancak bunları, toosee etkinleştirme hangi hello CNAME oluşturulan bölge hello toomodify verir.

Kalan Eylemler hello kopyalanan hello [DNS bölge katkıda bulunan yerleşik rolü](../active-directory/role-based-access-built-in-roles.md#dns-zone-contributor).

> [!NOTE]
> Hala güncelleştirilmiş toobe izin vererek etkili bir denetim olmamasına karşın kaydı silinirken bir özel RBAC rolü tooprevent kullanarak ayarlar. Kayıt kümeleri silinmesini engeller, ancak değiştirilen veren'in engel olmaz.  İzin verilen değişiklikleri eklenmesi ve tüm kaldırma dahil olmak üzere hello kayıt kümesinden kayıt kaldırma tooleave 'empty' kayıt kümesi kaydeder. Bu DNS çözümlemesi görüş açısından hello kayıt silme aynı etkiye ayarlamak hello sahiptir.

Özel rol tanımları şu anda hello Azure portal tanımlanamaz. Bu rol tanımına dayalı özel bir rol, Azure PowerShell kullanarak oluşturulabilir:

```powershell
# Create new role definition based on input file
New-AzureRmRoleDefinition -InputFile <file path>
```

Ayrıca hello Azure CLI oluşturulabilir:

```azurecli
# Create new role definition based on input file
azure role create -inputfile <file path>
```

Merhaba rolü sonra hello aynı atanabilir şekilde yerleşik roller olarak bu makalenin önceki bölümlerinde açıklandığı gibi.

Nasıl toocreate, yönetmek ve özel roller atama hakkında daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md).

## <a name="resource-locks"></a>Kaynak kilitleri

Toplama tooRBAC içinde başka bir tür güvenlik denetimi, hello özelliği too'lock Azure Resource Manager destekler ' kaynakları. RBAC kuralları belirli kullanıcılar ve gruplar toocontrol hello eylemlerini izin burada kaynak kilitleri uygulanan toohello kaynaktır ve tüm kullanıcılar ve roller etkili olur. Daha fazla bilgi için bkz. [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).

Kaynak kilidi iki tür vardır: **DoNotDelete** ve **salt okunur**. Bunlar uygulanabilir tooa DNS bölgesine veya tooan tek tek kayıt kümesi.  Merhaba aşağıdaki bölümlerde açıklanmaktadır birçok yaygın senaryolar ve nasıl toosupport bunları kaynak kilitleri kullanma.

### <a name="protecting-against-all-changes"></a>Tüm değişiklikleri karşı koruma

tooprevent salt okunur kilit toohello bölge geçerli herhangi bir değişiklik yapılan.  Bu yeni kayıt kümeleri değiştirilmiş veya silinmiş gelen oluşturulan ve varolan kaydı kümeleri engeller.

Bölge düzeyi kaynak kilitleri hello Azure portal oluşturulabilir.  'Kilitleri' Hello DNS bölge dikey penceresinden tıklayın ardından 'Ekle':

![Bölge düzeyi kaynak kilitleri hello Azure portal aracılığıyla](./media/dns-protect-zones-recordsets/locks1.png)

Bölge düzeyi kaynak kilitleri Azure PowerShell ile de oluşturulabilir:

```powershell
# Lock a DNS zone
New-AzureRmResourceLock -LockLevel <lock level> -LockName <lock name> -ResourceName <zone name> -ResourceType Microsoft.Network/DNSZones -ResourceGroupName <resource group name>
```

Azure kaynak kilitleri yapılandırma hello Azure CLI şu anda desteklenmiyor.

### <a name="protecting-individual-records"></a>Kayıtları tek tek koruma

tooprevent değişikliği karşı ayarlamak varolan bir DNS kaydı ReadOnly kilit toohello kayıt kümesi uygulayın.

> [!NOTE]
> DoNotDelete kilit tooa uygulama kayıt kümesi etkili bir denetim değil. Merhaba kayıt silinmesini kümesi engeller, ancak bu, değiştirilmesini engellemez.  İzin verilen değişiklikleri eklenmesi ve tüm kaldırma dahil olmak üzere hello kayıt kümesinden kayıt kaldırma tooleave 'empty' kayıt kümesi kaydeder. Bu DNS çözümlemesi görüş açısından hello kayıt silme aynı etkiye ayarlamak hello sahiptir.

Kayıt kümesi düzeyi kaynak kilitleri için şu anda yalnızca Azure PowerShell kullanılarak yapılandırılır.  Hello Azure portalında veya Azure CLI desteklenmez.

```powershell
# Lock a DNS record set
New-AzureRmResourceLock -LockLevel <lock level> -LockName "<lock name>" -ResourceName "<zone name>/<record set name>" -ResourceType "Microsoft.Network/DNSZones/<record type>" -ResourceGroupName "<resource group name>"
```

### <a name="protecting-against-zone-deletion"></a>Bölge silinmeye karşı koruma

Azure DNS'de bölge silindiğinde, hello bölgedeki tüm kayıt kümelerinin de silinir.  Bu işlem geri alınamaz.  Kritik bir bölgenin yanlışlıkla silinmesi hello olası toohave önemli iş etkisine sahiptir.  Bu nedenle, yanlışlıkla bölge silinmesine karşı çok önemli tooprotect olur.

Bir DoNotDelete kilit tooa bölge uygulama hello bölge silinmesini engeller.  Ancak, kilit alt kaynaklar tarafından devralınır olduğundan, ayrıca tüm kayıt kümelerini istenmeyen olabilen siliniyor, gelen hello bölgesinde engeller.  Kayıtları hala hello mevcut kayıt kümelerinden kaldırılabilir beri Ayrıca, Not hello yukarıda açıklandığı gibi de etkisiz olabilir.

Alternatif olarak, bir DoNotDelete kilit tooa kaydı uygulama hello SOA kayıt kümesi gibi hello bölge kümesindeki. göz önünde bulundurun.  Ayrıca hello kayıt kümelerini silmeden Hello bölge silinemiyor olduğundan, bu kayıt kümelerini serbestçe değiştiren hello bölge toobe içinde hala verirken bölge silme korur. Girişimde toodelete hello bölge, Azure Resource Manager bu aynı zamanda hello SOA kayıt kümesi siler ve hello SOA kilitlendiğinden blokları çağrısı hello algılar.  Hiçbir kayıt kümelerini silinir.

PowerShell komutunu aşağıdaki hello hello SOA kaydına hello bölge verilen karşı DoNotDelete Kilitle oluşturur:

```powershell
# Protect against zone delete with DoNotDelete lock on hello record set
New-AzureRmResourceLock -LockLevel DoNotDelete -LockName "<lock name>" -ResourceName "<zone name>/@" -ResourceType" Microsoft.Network/DNSZones/SOA" -ResourceGroupName "<resource group name>"
```

Başka bir yolu bir özel rol tooensure hello işleci ve hizmet kullanılan hesaplar toomanage bölgelerinizi değil sahip bölge kullanmaktır tooprevent yanlışlıkla bölge silme izinleri silin. Toodelete bir bölge gerektiğinde, iki aşamalı silme, ilk izni veriliyor bölge Sil (kapsamındaki izinler hello bölge, hello yanlış bölgeyi silmeden tooprevent) uygulayabilir ve ikinci toodelete hello bölgesi.

Bu ikinci yaklaşımı kilitleri tooremember toocreate gerek kalmadan bu hesapları tarafından erişilen tüm bölgelerde çalıştığını hello avantajına sahiptir. Hello abonelik sahibi gibi bölge silme izinlerine sahip herhangi bir hesabı kritik bir bölge hala yanlışlıkla silebilirsiniz hello dezavantajı vardır.

Olası toouse olan her iki yaklaşımın - kaynak kilitler ve özel roller - hello adresindeki aynı zaman, bir savunma yaklaşım tooDNS bölge koruma.

## <a name="next-steps"></a>Sonraki adımlar

* RBAC ile çalışma hakkında daha fazla bilgi için bkz: [hello Azure portalına erişim yönetimi kullanmaya başlama](../active-directory/role-based-access-control-what-is.md).
* Kaynak kilitleri ile çalışma hakkında daha fazla bilgi için bkz: [Azure Resource Manager ile kaynakları kilitleme](../azure-resource-manager/resource-group-lock-resources.md).

