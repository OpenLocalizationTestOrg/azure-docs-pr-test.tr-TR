---
title: "aaaCreate hello Azure portal ile bir Azure Media Services hesabı | Microsoft Docs"
description: "Bu öğretici, hello Azure portal ile Azure Media Services hesabı oluşturma hello adım adım anlatılmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir Azure Media Services hesabı oluşturma
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

Hello Azure portal tooquickly bir Azure Media Services (AMS) hesap oluşturma bir yol sağlar. Hesap tooaccess, toostore etkinleştirmek, şifrelemek, kodlama, yönetmek ve azure'da medya içeriği akış medya Hizmetleri kullanabilirsiniz. Merhaba zaman, Media Services hesabı oluşturma, ayrıca ilişkili bir depolama hesabı oluşturun (veya mevcut bir kullanabilirsiniz) hello içinde aynı coğrafi bölgede hello Media Services hesabı.

Bu makalede, bazı ortak kavramları açıklar ve nasıl toocreate Media Services hesap hello Azure portal ile gösterir.

## <a name="concepts"></a>Kavramlar
Media Services’e erişim iki ilişkili hesap gerektirir:

* Bir Media Services hesabı. Mevcut olan bulut tabanlı Media Services tooa kümesi erişim, hesap sağlar. Bir Media Services hesabı gerçek medya verilerini depolamaz. Bunun yerine, hesabınızdaki hello medya içeriği ve medya işleme işleri hakkındaki meta verileri depolar. Merhaba hesabı oluşturma hello aynı anda kullanılabilir bir Media Services bölge seçin. Seçtiğiniz hello hello hesabınız için meta veri kayıtlarını saklayan bir veri merkezi bölgedir.
  
* Bir Azure depolama hesabı. Hello depolama hesapları bulunan aynı coğrafi bölgede hello Media Services hesabı. Bir Media Services hesabı oluşturduğunuzda ya da mevcut bir depolama hesabını seçebileceğiniz hello hello içinde yeni bir depolama hesabı aynı bölgede veya oluşturabilirsiniz aynı bölgede. Bir Media Services hesabını silerseniz ilişkili depolama hesabınızdaki hello BLOB'lar silinmez.

> [!NOTE]
> Azure Media Services özelliklerinin farklı bölgelerde kullanılabilirliği hakkında bilgi için bkz. [Veri merkezleri arasında AMS özelliklerinin kullanılabilirliği](scenarios-and-availability.md#availability).

## <a name="create-an-ams-account"></a>AMS hesabı oluşturma
Merhaba adımları bu bölümünde Göster nasıl toocreate bir AMS hesabının.

1. Merhaba oturum açma [Azure portal](https://portal.azure.com/).
2. **+Yeni** > **Web + Mobil** > **Media Services**’e tıklayın.
   
    ![Media Services Oluşturma](./media/media-services-create-account/media-services-new1.png)
3. **MEDYA HİZMETLERİ HESABI OLUŞTUR**’a gerekli değerleri girin.
   
    ![Media Services Oluşturma](./media/media-services-create-account/media-services-new3.png)
   
   1. İçinde **hesap adı**, hello hello yeni AMS hesabının adını girin. Bir Media Services hesabı adı tüm küçük harf ya da boşluk numaralarıyla ve 3 too24 karakter uzunluğunda olmalıdır.
   2. Abonelikte erişiminiz hello farklı Azure abonelikleri arasından seçim.
   3. İçinde **kaynak grubu**, hello yeni veya mevcut bir kaynağı seçin.  Kaynak grubu; yaşam döngüsünü, izinleri ve ilkeleri paylaşan kaynakların bir koleksiyonudur. [Burada](../azure-resource-manager/resource-group-overview.md#resource-groups) daha fazla bilgi edinin.
   4. İçinde **konumu**, hello Media Services hesabınız için kullanılan toostore hello medya ve meta veri kayıtlarını olacaktır coğrafi bölgeyi seçin. Bu bölge medyanızı akışını sağlamak ve kullanılan tooprocess olması. Yalnızca hello Media Services kullanılabilen bölgeler hello aşağı açılan liste kutusunda görüntülenir. 
   5. İçinde **depolama hesabı**, Media Services hesabınızdan bir depolama hesabı tooprovide blob depolama hello medya içeriği seçin. Mevcut bir depolama hesabını hello seçebilirsiniz Media Services hesabınızla veya aynı coğrafi bölgede bir depolama hesabı oluşturabilirsiniz. Yeni bir depolama hesabı aynı hello oluşturulan bölge. Depolama hesabı için adları hello kurallar aynı Media Services hesapları için olduğu gibi hello.
      
       Depolama hakkında daha fazla bilgi [burada](../storage/common/storage-introduction.md).
   6. Seçin **PIN toodashboard** toosee hello hello hesap dağıtımının ilerlemesini.
4. Tıklatın **oluşturma** hello form hello sonundaki.
   
    Merhaba hesap başarıyla oluşturulduktan sonra genel bakış sayfasına yükler. Hello uç nokta tablo hello hesabı Akış akış uç noktası hello içinde varsayılan olacaktır **durduruldu** durumu. 

    >[!NOTE]
    >AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 
   
## <a name="toomanage-your-ams-account"></a>toomanage AMS hesabınızı

toomanage AMS hesabınızı (örneğin, toohello AMS API program aracılığıyla bağlanmak, videoları karşıya yüklemek, varlıkları kodlamak, içerik koruma yapılandırma, işin ilerleme durumunu izlemek) seçin **ayarları** yan hello portalının sol hello üzerinde. Merhaba gelen **ayarları**, hello kullanılabilir Kanatlar tooone gidin (örneğin: **API erişimini**, **varlıklar**, **işleri**, **İçerik koruma**).


## <a name="next-steps"></a>Sonraki adımlar

Bundan böyle dosyaları AMS hesabınıza yükleyebilirsiniz. Daha fazla bilgi için bkz. [Dosya yükleme](media-services-portal-upload-files.md).

Tooaccess AMS API program aracılığıyla planlıyorsanız bkz [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

