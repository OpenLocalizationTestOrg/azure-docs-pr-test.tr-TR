---
title: "Depolama çalışırken sonra aaaUpdate Media Services erişim anahtarları | Microsoft Docs"
description: "Bu makaleler nasıl tooupdate Media Services'ı depolama çalışırken sonra erişim anahtarları hakkında rehberlik sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a892ebb0-0ea0-4fc8-b715-60347cc5c95b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: milanga;cenkdin;juliako
ms.openlocfilehash: 26fa7a75a73397842aaebda59516a00f68ab97f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-media-services-after-rolling-storage-access-keys"></a>Depolama erişim tuşlarını çalışırken sonra güncelleştirme medya Hizmetleri

Yeni bir Azure Media Services (AMS) hesabı oluşturduğunuzda, bir Azure depolama hesabı başka bir deyişle tooselect toostore medya içeriğinizi kullanılan de istenir. Birden fazla depolama hesapları tooyour Media Services hesabı ekleyebilirsiniz. Bu konuda gösterilmektedir nasıl toorotate depolama anahtarları. Aynı zamanda, nasıl tooa medya hesabı tooadd depolama hesaplarını gösterir. 

Bu konuda açıklanan tooperform hello Eylemler, kullanıyor [ARM API'leri](https://docs.microsoft.com/rest/api/media/mediaservice) ve [Powershell](https://docs.microsoft.com/powershell/resourcemanager/azurerm.media/v0.3.2/azurerm.media).  Daha fazla bilgi için bkz: [nasıl toomanage Azure PowerShell ve Resource Manager kaynaklarıyla](../azure-resource-manager/powershell-azure-resource-manager.md).

## <a name="overview"></a>Genel Bakış

Yeni bir depolama hesabı oluşturduğunuzda Azure kullanılan tooauthenticate olan iki 512 bit depolama erişim tuşu oluşturur erişim tooyour depolama hesabı. Depolama bağlantılarınızı tooperiodically önerilen daha güvenli yeniden oluşturun ve depolama erişim anahtarınızı döndürme tookeep. Sipariş tooenable kullanarak, toomaintain bağlantıları toohello depolama hesabına erişim anahtarı hello yeniden oluşturmak diğer erişim tuşu iki erişim tuşu (birincil ve ikincil) sağlanır. Bu yordamı, "çalışırken erişim tuşları" olarak da adlandırılır.

Media Services tooit sağlanan bir depolama anahtarı bağlıdır. Özellikle, kullanılan toostream veya varlıklarınızı karşıdan hello bulucular hello belirtilen depolama erişim tuşu üzerinde bağlıdır. AMS hesabı oluşturduğunuzda, bir bağımlılık hello birincil depolama erişim tuşu üzerinde varsayılan olarak alır ancak bir kullanıcı olarak AMS sahip hello depolama anahtarı güncelleştirebilirsiniz. Bu konuda açıklanan adımları izleyerek hangi anahtar toouse toolet Media Services bilmeniz emin olmanız gerekir.  

>[!NOTE]
> Birden çok depolama hesabınız yoksa, bu yordamı her bir depolama hesabıyla gerçekleştirmelisiniz. Depolama anahtarları döndürme hello sipariş sabit değildir. Hello ikincil anahtar ilk döndürün ve birincil anahtar veya bunun tersini de hello.
>
> Adımları yürütmeden önce bu konuda yapma emin tootest bir üretim hesabı bunları bir üretim öncesi hesabında açıklanmaktadır.
>

## <a name="steps-toorotate-storage-keys"></a>Adımları toorotate depolama anahtarları 
 
 1. Değişiklik hello depolama hesabının birincil anahtarını hello powershell cmdlet'i aracılığıyla veya [Azure](https://portal.azure.com/) portal.
 2. Uygun parametreleri tooforce medya hesap toopick depolama hesabı anahtarlarını yukarı eşitleme AzureRmMediaServiceStorageKeys cmdlet'ini çağırın
 
    Aşağıdaki örnek hello nasıl toosync toostorage hesapları anahtarları gösterir.
  
         Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId
  
 3. Bir saat ya da bunu bekleyin. Merhaba akış senaryoları çalıştığınız doğrulayın.
 4. Depolama hesabının ikincil anahtarını hello powershell cmdlet veya Azure portal aracılığıyla değiştirin.
 5. Eşitleme AzureRmMediaServiceStorageKeys powershell uygun parametreleri tooforce medya hesap toopick yeni depolama hesabı anahtarları ayarlama ile çağırın. 
 6. Bir saat ya da bunu bekleyin. Merhaba akış senaryoları çalıştığınız doğrulayın.
 
### <a name="a-powershell-cmdlet-example"></a>Powershell cmdlet örneği 

Merhaba aşağıdaki örnekte nasıl tooget depolama hesabı hello ve hello AMS hesabıyla eşitleme gösterir.

    $regionName = "West US"
    $resourceGroupName = "SkyMedia-USWest-App"
    $mediaAccountName = "sky"
    $storageAccountName = "skystorage"
    $storageAccountId = "/subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.Storage/storageAccounts/$storageAccountName"

    Sync-AzureRmMediaServiceStorageKeys -ResourceGroupName $resourceGroupName -AccountName $mediaAccountName -StorageAccountId $storageAccountId

 
## <a name="steps-tooadd-storage-accounts-tooyour-ams-account"></a>Tooyour AMS hesabının adımları tooadd depolama hesapları

Merhaba aşağıdaki konu tooyour AMS hesabının nasıl tooadd depolama hesaplarını gösterir: [birden çok depolama hesapları tooa Media Services hesabı ekleme](meda-services-managing-multiple-storage-accounts.md).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>İlgili kaynaklar
Bu belge oluşturma doğrultusunda katkıda bulunan kişiler aşağıdaki tooacknowledge hello isteriz: Cenk Dingiloglu, Milan Gada Seva Titov.
