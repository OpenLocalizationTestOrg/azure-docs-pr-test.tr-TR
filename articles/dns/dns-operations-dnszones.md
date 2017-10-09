---
title: "aaaManage DNS bölgeleri Azure DNS - PowerShell | Microsoft Docs"
description: "DNS bölgelerini Azure Powershell kullanarak yönetebilirsiniz. Bu makalede nasıl tooupdate, silme ve Azure DNS üzerinde DNS bölgeleri oluşturma"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: a67992ab-8166-4052-9b28-554c5a39e60c
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 261b89f72213aa9784034d47ff9d1c55a4e80d65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-dns-zones-using-powershell"></a>Nasıl toomanage DNS bölgeleri PowerShell'i kullanma

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

Bu makalede, nasıl Azure PowerShell kullanarak toomanage DNS bölgeleri gösterir. DNS bölgelerini hello platformlar arası kullanarak da yönetebilirsiniz [Azure CLI](dns-operations-dnszones-cli.md) ya da Azure portal hello.

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

[!INCLUDE [dns-powershell-setup](../../includes/dns-powershell-setup-include.md)]


## <a name="create-a-dns-zone"></a>DNS bölgesi oluşturma

Bir DNS bölgesi hello kullanılarak oluşturulan `New-AzureRmDnsZone` cmdlet'i.

Merhaba aşağıdaki örnek adlı bir DNS bölgesi oluşturur *contoso.com* adlı hello kaynak grubunda *MyResourceGroup*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

Hello aşağıdaki örnekte nasıl toocreate bir DNS bölgesi iki gösterir [Azure Resource Manager etiketlerine](dns-zones-records.md#tags), *project = demo* ve *env = test*:

```powershell
New-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

## <a name="get-a-dns-zone"></a>Bir DNS bölgesini alın

tooretrieve bir DNS bölgesi kullanmak hello `Get-AzureRmDnsZone` cmdlet'i. Bu işlem, bir DNS bölgesi nesne karşılık gelen tooan varolan bir bölge Azure DNS'de döndürür. Merhaba nesne hello bölge (örneğin, kayıt kümesi sayısı hello) hakkında veri içerir, ancak kayıt kümelerini hello kendilerini içermiyor (bkz: `Get-AzureRmDnsRecordSet`).

```powershell
Get-AzureRmDnsZone -Name contoso.com –ResourceGroupName MyAzureResourceGroup

Name                  : contoso.com
ResourceGroupName     : myresourcegroup
Etag                  : 00000003-0000-0000-8ec2-f4879750d201
Tags                  : {project, env}
NameServers           : {ns1-01.azure-dns.com., ns2-01.azure-dns.net., ns3-01.azure-dns.org.,
                        ns4-01.azure-dns.info.}
NumberOfRecordSets    : 2
MaxNumberOfRecordSets : 5000
```

## <a name="list-dns-zones"></a>Liste DNS bölgeleri

Merhaba bölge adını atlama tarafından `Get-AzureRmDnsZone`, bir kaynak grubundaki tüm bölgeler sıralayabilirsiniz. Bu işlem, bölge nesneleri içeren bir dizi döndürür.

```powershell
$zoneList = Get-AzureRmDnsZone -ResourceGroupName MyAzureResourceGroup
```

Merhaba bölge adı ve hello kaynak grubu adı atlama tarafından `Get-AzureRmDnsZone`, tüm bölgelerde hello Azure aboneliği sıralayabilirsiniz.

```powershell
$zoneList = Get-AzureRmDnsZone
```

## <a name="update-a-dns-zone"></a>Bir DNS bölgesini güncelleştirme

Değişiklikleri kullanarak DNS bölgesi kaynak yapılabilir tooa `Set-AzureRmDnsZone`. Bu cmdlet herhangi bir hello DNS kayıt kümelerini hello bölge içinde güncelleştirmez (bkz [nasıl tooManage DNS kayıtlarını](dns-operations-recordsets.md)). Yalnızca hello bölge kaynağını kendisini tooupdate özelliklerini de kullandı. Merhaba yazılabilir bölge özellikleri olan şu anda sınırlı toohello [Azure Resource Manager 'etiketleri' hello bölge kaynak için](dns-zones-records.md#tags).

Bir DNS bölgesi iki yolu tooupdate aşağıdaki hello birini kullanın:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group"></a>Merhaba bölge adı ve kaynak grubu kullanarak hello bölgesi belirtin

Bu yaklaşım hello varolan bölge etiketleri belirtilen hello değerlerle değiştirir.

```powershell
Set-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup -Tag @{ project="demo"; env="test" }
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Bir $zone nesnesi kullanılarak hello dilimini belirtin

Bu yaklaşım hello varolan bölge nesnesi alır, hello etiketleri değiştirir ve hello değişiklikleri kaydeder. Bu şekilde, varolan etiketleri korunabilir.

```powershell
# Get hello zone object
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup

# Remove an existing tag
$zone.Tags.Remove("project")

# Add a new tag
$zone.Tags.Add("status","approved")

# Commit changes
Set-AzureRmDnsZone -Zone $zone
```

Kullanırken `Set-AzureRmDnsZone` $zone nesnesiyle [Etag denetler](dns-zones-records.md#etags) kullanılan tooensure eşzamanlı değişiklikleri yazılmaz. İsteğe bağlı hello kullanabilirsiniz `-Overwrite` bu denetimleri toosuppress geçin.

## <a name="delete-a-dns-zone"></a>Bir DNS bölgesi Sil

DNS bölgelerini hello kullanarak silinebilir `Remove-AzureRmDnsZone` cmdlet'i.

> [!NOTE]
> Bir DNS bölgesi silme hello bölgedeki tüm DNS kayıtlarını siler. Bu işlem geri alınamaz. Merhaba DNS bölgesi kullanımdaysa hello bölge silindiğinde hello bölge kullanarak Hizmetleri başarısız olur.
>
>yanlışlıkla bölge silinmesine karşı tooprotect bkz [nasıl tooprotect DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).


Bir DNS bölgesi iki yolu toodelete aşağıdaki hello birini kullanın:

### <a name="specify-hello-zone-using-hello-zone-name-and-resource-group-name"></a>Merhaba bölge adı ve kaynak grubu adı kullanarak hello bölgesi belirtin

```powershell
Remove-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
```

### <a name="specify-hello-zone-using-a-zone-object"></a>Bir $zone nesnesi kullanılarak hello dilimini belirtin

Merhaba bölge toobe kullanılarak silinen belirtebilirsiniz bir `$zone` tarafından döndürülen nesne `Get-AzureRmDnsZone`.

```powershell
$zone = Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup
Remove-AzureRmDnsZone -Zone $zone
```

Merhaba bölge nesnesini parametre olarak geçirilen yerine de yöneltilen:

```powershell
Get-AzureRmDnsZone -Name contoso.com -ResourceGroupName MyAzureResourceGroup | Remove-AzureRmDnsZone

```

İle `Set-AzureRmDnsZone`, belirtme hello bölge kullanarak bir `$zone` nesne Etag denetler tooensure eşzamanlı değişiklikleri silinmez etkinleştirir. Kullanım hello `-Overwrite` bu denetimleri toosuppress geçin.

## <a name="confirmation-prompts"></a>Onay istekleri

Merhaba `New-AzureRmDnsZone`, `Set-AzureRmDnsZone`, ve `Remove-AzureRmDnsZone` cmdlet'leri tüm destek onay ister.

Her ikisi de `New-AzureRmDnsZone` ve `Set-AzureRmDnsZone` hello varsa onay iste `$ConfirmPreference` PowerShell tercih değişkeni değerine sahip `Medium` veya daha düşük. Bir DNS bölgesi hello silme toohello olasılığı yüksek etkisi nedeniyle `Remove-AzureRmDnsZone` cmdlet hello varsa onay ister `$ConfirmPreference` PowerShell değişkeni sahip herhangi bir değer dışındaki `None`.

Merhaba varsayılan değeri itibaren `$ConfirmPreference` olan `High`, yalnızca `Remove-AzureRmDnsZone` varsayılan olarak onaylamanız istenir.

Merhaba geçerli kılabilirsiniz `$ConfirmPreference` hello kullanarak ayarını `-Confirm` parametresi. Belirtirseniz `-Confirm` veya `-Confirm:$True` , hello cmdlet sizden, önce onay çalıştırır. Belirtirseniz `-Confirm:$False` , hello cmdlet istenmez sizin için onay.

Hakkında daha fazla bilgi için `-Confirm` ve `$ConfirmPreference`, bkz: [tercih değişkenleri hakkında](https://msdn.microsoft.com/powershell/reference/5.1/Microsoft.PowerShell.Core/about/about_Preference_Variables).

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[kayıt kümelerini ve kayıtları yönetmek](dns-operations-recordsets.md) DNS bölgesinde.
<br>
Nasıl çok öğrenin[, etki alanı tooAzure DNS temsilci](dns-domain-delegation.md).
<br>
Gözden geçirme hello [Azure DNS PowerShell başvuru belgeleri](/powershell/module/azurerm.dns).

