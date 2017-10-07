---
title: "Aspera kullanarak Azure Media Services hesabı aaaUpload dosyalarıyla | Microsoft Docs"
description: "Bu öğretici, hello kullanarak Media Services hesabı ile ilişkili bir depolama hesabı içine dosyaları karşıya hello adım adım anlatılmaktadır ** Aspera sunucu üzerinde isteğe bağlı ** Azure hizmeti."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Azure'da hello Aspera sunucu isteğe bağlı hizmet kullanarak bir Media Services hesabı içine dosyaları karşıya yükleme

## <a name="overview"></a>Genel Bakış

**Aspera** çok yüksek hızlı bir dosya aktarım yazılımıdır. Azure için **Aspera Server On Demand**, büyük dosyaların doğrudan Azure Blob nesne depolama alanına yüksek hızda yüklenmesini ve indirilmesini sağlar. Hakkında bilgi için **isteğe bağlı Aspera**, hello bkz [Aspera bulut](http://cloud.asperasoft.com/) site. 
  
**İsteğe bağlı Aspera sunucu** hello satınalma için Azure kullanılabilir [Azure Market](https://azure.microsoft.com/en-us/marketplace/). İçinde bir satın toocomplete sipariş **Aspera sunucu isteğe bağlı** Azure için lütfen Azure Marketi Windows Live ID'niz ile oturum açın

Bu öğretici, hello kullanarak Media Services hesabı ile ilişkili bir depolama hesabı içine dosyaları karşıya hello adım adım anlatılmaktadır **Aspera sunucu isteğe bağlı** Azure üzerinde hizmet. 

Toouse Azure Aspera ve Media Services ile nasıl çalıştığını gösteren bir örnek bulabilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Azure Media Services ile medya işlemcileri (Mp'leri) işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur. Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.
>

## <a name="prerequisites"></a>Ön koşullar 

toocomplete Bu öğretici, gerekir:

* Windows Live ID
* Bir [Azure hesabı](https://azure.microsoft.com). Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/). 
* Bir [Azure Media Services hesabı](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Azure için İsteğe Bağlı Aspera yazılımını satın alın

Azure Market oturum açtıktan sonra bu temel adımları toocomplete Aspera istendiğinde Azure satın alma işleminiz izleyin.

1. Aspera ifadesini arayın ve 'Server On Demand' öğesini seçin.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Merhaba abonelik planları gözden geçirin ve ' oturum üzerinde ' düğmesini tıklatın

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. İsteğe bağlı abonelik sunucunuzda hello ayrıntıları doldurun.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Tıklatın hello üzerinde **fiyatlandırma katmanı** ve istenen aylık biriminiz hello alt panelinde seçin. Merhaba, **planlama ayrıntıları** paneli, select **Tamam**. Ardından hello **fiyatlandırma Katmanınızı seçin** öğesine tıklayın **seçin**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Tıklayın **yasal koşulları** tooview ve hello alt panelinde hello yasal koşulları kabul edin. Merhaba yasal koşulları gözden geçirdikten sonra tıklayın **satın alma**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Tamamlamak hello satın alma tıklayarak **oluşturma**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. Hello Azure Pano hello hizmet sağlama, Duyurusu.  Sağlamada tamamlandıktan sonra hello yeni abonelik kaynaklarınız hello hizmetin hello adı için arayarak bulabilirsiniz. Merhaba hizmeti, çift tıklayarak toolaunch hello Hizmet Yönetim Portalı bulduktan sonra.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Merhaba Aspera Yönetim Portalı'nı başlatın. Yeni Aspera hizmetinizi bulduktan sonra hello hizmette tıklayarak erişim toohello Yönetim Portalı, kaynaklara erişebilir.  Yeni bir panel başlatılır. Bu yeni paneli, hello üzerinde tooclick gereken **kaynak adı** yeni hizmetinizin.  Aşağıdaki ekran görüntüsü hello 'AsperaTransferDemo' hello kaynak adıdır. Merhaba kaynak adına tıkladığınızda, başka bir panel başlatılır. Yeni başlatılan bu panelde bir 'Yönet' bağlantısı görürsünüz. Merhaba üzerinde 'Yönet' bağlantı toolaunch hello Aspera Yönetim Portalı'ı tıklatın.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Merhaba üzerinde tıklatarak bağlantı yönetmek için gerekli toohello kayıt sayfası alırsınız tooaccess hello hizmet.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. Bu noktada, burada erişim tuşları oluşturma, Aspera istemcileri ve lisansları yükleyin, kullanım görüntüleyebilir ve API hello hakkında bilgi edinin erişim toohello Aspera Hizmet Yönetim Portalı, olması gerekir.

    Merhaba aşağıdaki ekran görüntüsü hello erişim oluşturmayı gösterir. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Merhaba aşağıdaki ekran görüntüsünde hello portal arabirimlerde raporlama hello kullanımını gösterir. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Aspera ile dosyaları karşıya yükleme

1. Karşıdan yükle ve hello Aspera istemci yazılımı yükleyin:
    
    * [Tarayıcı eklentisi](http://downloads.asperasoft.com/connect2/)
    * [Zengin istemci](http://downloads.asperasoft.com/en/downloads/2)

2. İlk aktarımınızı yapın. Merhaba Aspera Aktarım Hizmeti ile sipariş toouse hello Aspera istemci tootransfer içinde toocomplete hello aşağıdaki gerekir: 

    1. Merhaba Aspera portalı kullanarak bir erişim anahtarı oluşturun.  
    2. İndirme, yükleme ve lisans hello Aspera istemci (yazılım hello Aspera Portalı'nda bulunabilir).  

    >[!NOTE]
    >Merhaba Aspera istemci Kılavuzu yapılandırma bilgileri okuyun.
    
    3. Azure Media hello kullanarak hesabınızla ilişkilendirilen depolama hesabınızın bazı bilgiler almak [Azure portal](https://portal.azure.com/). Özellikle, adı ve anahtar ve hello depolama blob kapsayıcı adı toowhich içinde içeriğinizi tooplace istiyor. 

        * tooget hello depolama bilgisi hello portalından: depolama hesabınız, hello erişim tuşları ve hesabınızın kopyalama hello adı ve hello anahtar'ı tıklatın.
        * tooget hello kapsayıcı adı: seçin, depolama hesabını bulmak **BLOB'lar**seçin hello kapsayıcısının içine tooupload hello içerik istediğiniz hello adı. 

    Merhaba ekran görüntüsü hello Aspera istemci aşağıdadır **Bağlantı Yöneticisi** burada belirtmelisiniz hello blob kapsayıcısı yanı sıra hello 'Azure' depolama türünü ve kimlik bilgileri.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Kaynaklar

Merhaba kaynakları izleyerek, bu makalede bahsedilen. 

* [Connect Tarayıcı Eklentisi](http://downloads.asperasoft.com/connect2/)
* [Connect Kılavuzu](http://downloads.asperasoft.com/en/documentation/8)
* [Aspera İstemcisi](http://downloads.asperasoft.com/en/downloads/2)
* [İstemci Kılavuzu](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>Sonraki adımlar

Artık, [bir depolama hesabından AMS hesabına blob kopyalayabilirsiniz](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

