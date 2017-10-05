---
title: "PowerShell ile Azure Media Services hesaplarını yönetme"
description: "Azure Media Services hesapları PowerShell cmdlet'leri ile yönetmeyi öğrenin."
author: Juliako
manager: erikre
editor: 
services: media-services
documentationcenter: 
ms.assetid: 17a10c25-d94f-421c-b6bc-ae0958e2ac96
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: juliako
ms.openlocfilehash: 3d999d9e27844bc0164cc3572522b9ec022118a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>PowerShell ile Azure Media Services hesaplarını yönetme
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> Azure Media Services hesabı oluşturmak için bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.
> 
> 

## <a name="overview"></a>Genel Bakış
Bu makale Azure PowerShell cmdlet'lerini Azure Resource Manager framework Azure Media Services (AMS) listeler. Cmdlet'leri mevcut **Microsoft.Azure.Commands.Media** ad alanı.

## <a name="versions"></a>Sürümler
**ApiVersion**: "2015-10-01"

## <a name="new-azurermmediaservice"></a>New-AzureRmMediaService
Medya hizmeti oluşturur.

### <a name="syntax"></a>Sözdizimi
Parametre kümesi: StorageAccountIdParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccountId] <string> [-Tags <hashtable>]  [<CommonParameters>]

Parametre kümesi: StorageAccountsParamSet

    New-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Location] <string> [-StorageAccounts] <PSStorageAccount[]> [-Tags <hashtable>]  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Ad |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

**-Location &lt;dize&gt;**

Medya hizmeti kaynak konumunu belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |2 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccountId &lt;dize&gt;**

Medya hizmeti ile ilişkili bir birincil depolama hesabını belirtir.

* Yalnızca desteklenen (Resource Manager API ile) yeni depolama hesabı oluşturuldu.
* Depolama hesabı bulunmalı ve medya hizmeti ile aynı konumda yok.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |3 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |StorageAccountIdParamSet |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.

* Yalnızca desteklenen (Resource Manager API ile) yeni depolama hesabı oluşturuldu.
* Depolama hesabı bulunmalı ve medya hizmeti ile aynı konumda yok.
* Yalnızca bir depolama hesabı birincil olarak belirtilebilir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |3 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |StorageAccountsParamSet |
| Joker karakterler kabul edilsin mi? |False |

**-Etiketler &lt;Hashtable&gt;**

Bir karma tablosu medya hizmeti ile ilişkilendirilmiş etiketleri belirtir.

* Örnek: @{"tag1"="value1";" tag2 "=: value2"}

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |False |
| Konum? |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Bir medya hizmeti güncelleştirir.

### <a name="syntax"></a>Sözdizimi
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Ad |
| --- | --- |
| Gerekli? |True |
| Konum? |1 |
| Varsayılan değer |None |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.

* Yalnızca desteklenen (Resource Manager API ile) yeni depolama hesabı oluşturuldu.
* Depolama hesabı bulunmalı ve medya hizmeti ile aynı konumda yok.
* Yalnızca bir depolama hesabı birincil olarak belirtilebilir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |False |
| Konum? |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |StorageAccountsParamSet |
| Joker karakterler kabul edilsin mi? |False |

**-Etiketler &lt;Hashtable&gt;**

Bu medya hizmeti ile ilişkilendirilmiş etiketleri karma tablosu belirtir.

* Medya hizmeti ile ilişkilendirilmiş etiketleri, müşteri tarafından belirtilen değeri ile değiştirilir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |False |
| Konum? |Adlı |
| Varsayılan değer |None |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Medya hizmeti kaldırır.

### <a name="syntax"></a>Sözdizimi
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |2 |
| Varsayılan değer |None |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Bir kaynak grubunda tüm medya Hizmetleri veya belirli bir ada sahip bir medya hizmeti alır.

### <a name="syntax"></a>Sözdizimi
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |ResourceGroupParameterSet, AccountNameParameterSet |

Joker karakterler kabul edilsin mi?   False

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |AccountNameParameterSet |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Medya hizmeti anahtarları alır.

### <a name="syntax"></a>Sözdizimi
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Medya hizmeti birincil veya ikincil anahtarı yeniden oluşturur.

### <a name="syntax"></a>Sözdizimi
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-KeyType &lt;KeyType&gt;**

Medya hizmeti anahtar türünü belirtir.

* Birincil veya ikincil

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |2 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Medya hizmeti ile ilişkilendirilmiş bir depolama hesabı için depolama hesabı anahtarları eşitler.

### <a name="syntax"></a>Sözdizimi
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait olduğu kaynak grubu adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Medya hizmeti adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccountId &lt;dize&gt;**

Medya hizmeti ile ilişkilendirilmiş depolama hesabını belirtir.

| Diğer adlar | Kimlik |
| --- | --- |
| Gerekli? |TRUE |
| Konum? |2 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet şu genel parametreleri destekler: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction ve -WarningVariable.

### <a name="inputs"></a>Girişleri
Girdi türü cmdlet'e iletebildiğiniz nesnelerin türüdür.

### <a name="outputs"></a>Çıkışları
Çıkış türü cmdlet'in çıkardığı nesnelerin türüdür.

## <a name="next-step"></a>Sonraki adım
Media Services'i öğrenme yolları denetleyin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

