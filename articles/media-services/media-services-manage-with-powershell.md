---
title: "aaaManage PowerShell ile Azure Media Services hesapları"
description: "PowerShell cmdlet'leri ile nasıl toomanage Azure Media Services hesapları öğrenin."
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
ms.openlocfilehash: e8f97bb2393343e45fabf9c437b4fc09f2525dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-media-services-accounts-with-powershell"></a>PowerShell ile Azure Media Services hesaplarını yönetme
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toobe mümkün toocreate Azure Media Services hesabı, bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A8A8397B5" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.
> 
> 

## <a name="overview"></a>Genel Bakış
Bu makalede, Azure Media Services (AMS) hello Azure Resource Manager framework hello Azure PowerShell cmdlet'leri listelenmektedir. Merhaba cmdlet'leri mevcut hello **Microsoft.Azure.Commands.Media** ad alanı.

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

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Ad |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

**-Location &lt;dize&gt;**

Merhaba medya hizmeti Hello kaynak konumunu belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |2 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccountId &lt;dize&gt;**

Merhaba medya hizmeti ile ilişkili bir birincil depolama hesabını belirtir.

* Yalnızca desteklenen (Merhaba Resource Manager API ile) yeni depolama hesabı oluşturuldu.
* Merhaba depolama hesabının var olmalıdır ve hello hello medya hizmeti ile aynı konum.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |3 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |StorageAccountIdParamSet |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Merhaba medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.

* Yalnızca desteklenen (Merhaba Resource Manager API ile) yeni depolama hesabı oluşturuldu.
* Merhaba depolama hesabının var olmalıdır ve hello hello medya hizmeti ile aynı konum.
* Yalnızca bir depolama hesabı birincil olarak belirtilebilir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |3 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |StorageAccountsParamSet |
| Joker karakterler kabul edilsin mi? |False |

**-Etiketler &lt;Hashtable&gt;**

Bir karma tablosu hello medya hizmeti ile ilişkilendirilmiş hello etiketlerin belirtir.

* Örnek: @{"tag1"="value1";" tag2 "=: value2"}

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konum? |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="set-azurermmediaservice"></a>Set-AzureRmMediaService
Bir medya hizmeti güncelleştirir.

### <a name="syntax"></a>Sözdizimi
    Set-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string> [-Tags <hashtable>] [-StorageAccounts <PSStorageAccount[]>]  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Ad |
| --- | --- |
| Gerekli mi? |True |
| Konum? |1 |
| Varsayılan değer |None |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccounts &lt;PSStorageAccount\[\]&gt;**

Merhaba medya hizmeti ile ilişkilendirilmiş depolama hesaplarını belirtir.

* Yalnızca desteklenen (Merhaba Resource Manager API ile) yeni depolama hesabı oluşturuldu.
* Merhaba depolama hesabının var olmalıdır ve hello hello medya hizmeti ile aynı konum.
* Yalnızca bir depolama hesabı birincil olarak belirtilebilir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konum? |Adlı |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |StorageAccountsParamSet |
| Joker karakterler kabul edilsin mi? |False |

**-Etiketler &lt;Hashtable&gt;**

Bu medya hizmeti ile ilişkilendirilmiş hello etiketleri karma tablosu belirtir.

* Merhaba medya hizmeti ile ilişkilendirilmiş hello etiketleri hello müşteri tarafından belirtilen değeri ile değiştirilir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |False |
| Konum? |Adlı |
| Varsayılan değer |None |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="remove-azurermmediaservice"></a>Remove-AzureRmMediaService
Medya hizmeti kaldırır.

### <a name="syntax"></a>Sözdizimi
    Remove-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |2 |
| Varsayılan değer |None |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="get-azurermmediaservice"></a>Get-AzureRmMediaService
Bir kaynak grubunda tüm medya Hizmetleri veya belirli bir ada sahip bir medya hizmeti alır.

### <a name="syntax"></a>Sözdizimi
ParameterSet: ResourceGroupParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string>  [<CommonParameters>]    

ParameterSet: AccountNameParameterSet

    Get-AzureRmMediaService [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |ResourceGroupParameterSet, AccountNameParameterSet |

Joker karakterler kabul edilsin mi?   False

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Parametre kümesi adı |AccountNameParameterSet |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="get-azurermmediaservicekeys"></a>Get-AzureRmMediaServiceKeys
Medya hizmeti anahtarları alır.

### <a name="syntax"></a>Sözdizimi
    Get-AzureRmMediaServiceKeys [-ResourceGroupName] <string> [-AccountName] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="set-azurermmediaservicekey"></a>Set-AzureRmMediaServiceKey
Medya hizmeti birincil veya ikincil anahtarı yeniden oluşturur.

### <a name="syntax"></a>Sözdizimi
    Set-AzureRmMediaServiceKey [-ResourceGroupName] <string> [-AccountName] <string> [-KeyType] <KeyType> {Primary | Secondary}  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-KeyType &lt;KeyType&gt;**

Merhaba anahtar hello medya hizmeti türünü belirtir.

* Birincil veya ikincil

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |2 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |False |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toothe cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="sync-azurermmediaservicestoragekeys"></a>Sync-AzureRmMediaServiceStorageKeys
Merhaba medya hizmeti ile ilişkilendirilmiş bir depolama hesabı için depolama hesabı anahtarları eşitler.

### <a name="syntax"></a>Sözdizimi
    Sync-AzureRmMediaServiceStorageKeys [-ResourceGroupName] <string> [-MediaServiceAccountName] <string>    [-StorageAccountId] <string>  [<CommonParameters>]

### <a name="parameters"></a>Parametreler
**-ResourceGroupName &lt;dize&gt;**

Bu medya hizmeti ait hello kaynak grubu toowhich Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |0 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-AccountName &lt;dize&gt;**

Merhaba medya hizmeti Hello adını belirtir.

| Diğer adlar | Yok |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |1 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**-StorageAccountId &lt;dize&gt;**

Merhaba medya hizmeti ile ilişkili hello depolama hesabını belirtir.

| Diğer adlar | Kimlik |
| --- | --- |
| Gerekli mi? |TRUE |
| Konum? |2 |
| Varsayılan değer |Yok |
| Ardışık Düzen giriş kabul edilsin mi? |TRUE(ByPropertyName) |
| Joker karakterler kabul edilsin mi? |False |

**&lt;CommandParameters&gt;**

Bu cmdlet hello ortak parametreleri destekler:-Debug, - ErrorAction, - ErrorVariable, - Informationaction, - Informationvariable, - OutVariable,-OutBuffer, - PipelineVariable, - Verbose, - WarningAction ve - WarningVariable.

### <a name="inputs"></a>Girişleri
Merhaba giriş toohello cmdlet iletebildiğiniz hello hello türü nesneleri türüdür.

### <a name="outputs"></a>Çıkışları
Merhaba çıkış cmdlet hello hello nesnelerin hello türü yayar türüdür.

## <a name="next-step"></a>Sonraki adım
Media Services'i öğrenme yolları denetleyin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

