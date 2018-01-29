---
title: "Azure Portalı'nı kullanarak medya çözümleme | Microsoft Docs"
description: "Bu konuda, Azure Portalı'nı kullanarak medya analizi medya işlemcileri (Mp'leri) medyanızı işlemek nasıl ele alınmıştır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 18213fc1-74f5-4074-a32b-02846fe90601
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 22032aef0cc8b7b015503043028873e70c21ee85
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="analyze-your-media-using-the-azure-portal"></a>Azure portalını kullanarak medyanızı analiz etme
> [!NOTE]
> Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Genel Bakış
Azure Media Services analizi, kuruluş ve işletmelerin video dosyalarından eyleme dönüştürülebilir Öngörüler türetmesini kolaylaştıran konuşma ve görme bileşenler (Kurumsal ölçek, uyumluluk, güvenlik ve genel ulaşma) koleksiyonudur. Daha ayrıntılı Azure Media Services Analytics'e genel bakış için bkz: [bu](media-services-analytics-overview.md) konu. 

Bu konuda, Azure Portalı'nı kullanarak medya analizi medya işlemcileri (Mp'leri) medyanızı işlemek nasıl ele alınmıştır. Medya analizi Mp'leri MP4 veya JSON dosyaları üretir. Medya işlemcisi bir MP4 dosyası oluşturduysa dosyayı aşamalı olarak indirebilirsiniz. Medya işlemcisi bir JSON dosyası oluşturduysa dosyayı Azure blob depolamadan indirebilirsiniz. 

## <a name="choose-an-asset-that-you-want-to-analyze"></a>Analiz etmek istediğiniz bir varlığı seçin
1. [Azure portalında](https://portal.azure.com/) Azure Media Services hesabınızı seçin.
2. **Ayarlar** penceresinde **Varlıklar**’ı seçin.  
   .
    ![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. Çözümleme ve basın istediğiniz varlığı seçin **Çözümle** düğmesi.
   
    ![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. İçinde **medya analizi medya varlıkla işlem** penceresinde, işlemci seçin. 
   
    Makalenin kalanında nedenini açıklar ve her işlemci kullanma. 
5. Tuşuna **oluşturma** iş başlatma.

## <a name="azure-media-indexer"></a>Azure Media Indexer
**Azure Media Indexer** medya işlemcisi yanı sıra medya dosyaları ve içerik aranabilir yapmanıza kapalı açıklamalı alt yazı parçaları oluşturmak olanak sağlar. Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Dil
Multimedya dosyasında tanınması için doğal dil. Örneğin, İngilizce ve İspanyolca. 

### <a name="captions"></a>Resim yazıları
İçeriğinizi oluşturulan açıklamalı alt yazı biçimi seçebilirsiniz. Bir dizin oluşturma işi kapalı açıklamalı alt yazı dosyaları aşağıdaki biçimlerde oluşturabilirsiniz:  

* **SAMI**
* **TTML**
* **WebVTT**

Bu biçimler dosyalarında ses ve video dosyaları işitme engelli kişiler için erişilebilir hale getirmek için kullanılan açıklamalı alt yazı (CC) kapatıldı.

### <a name="aib-file"></a>AIB dosyası
Özel SQL Server IFilter ile kullanmak için ses dizin Blob dosyası oluşturmak istiyorsanız bu seçeneği belirleyin. Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogu.

### <a name="keywords"></a>Anahtar sözcükler
Anahtar sözcükler XML dosyası oluşturmak istiyorsanız bu seçeneği belirleyin. Bu dosya, sıklığı ve uzaklık bilgileri konuşma içerikten ayıklanan anahtar sözcükler içeriyor.

### <a name="job-name"></a>İş adı
İş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure medya Hyperlapse ilk kişi veya eylem kamera içerikten kesintisiz zaman onlara videolar oluşturan bir MP ' dir.  Daha fazla bilgi için [bu](media-services-hyperlapse-content.md) konu başlığına bakın. Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Hız
Giriş video hızlandırmak için hızıyla belirtin. Çıktı, sabit ve zaman onlara yorumlama video giriş şeklindedir.

### <a name="job-name"></a>İş adı
İş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
**Azure medya yüz algılayıcısı** medya işlemcisi (MP) sayısı, hareketleri izlemek ve İzleyici katılım ve tepki yüz ifadeleri aracılığıyla bile ölçer olanak sağlar. Bu hizmet, iki özellik içerir: 

* **Yüz algılama**
  
    Yüz algılama bulur ve video içinde İnsan yüzeyleri izler. Birden çok yüzeyleri algılanabilir ve bunların geçici bir JSON dosyası döndürülen zaman ve yer meta verilerle taşırken sonradan izlenmesi. İzleme sırasında bunu obstructed veya kısaca çerçeve bırakın olsa bile kişinin ekranında dolaşma sırada tutarlı kimliği aynı yüz vermek dener.
  
  > [!NOTE]
  > Bu hizmetler, yüz tanıma gerçekleştirmez. Çerçeve ayrıldığında ya da için obstructed hale bir kişi döndürmeleri zaman uzun yeni bir kimlik verilir.
  > 
  > 
* **Duygu algılama**
  
    Duygu algılama analiz mutluluk, sadness, Korku, öfke ve daha fazlası da dahil olmak üzere algılandı, yüzler birden çok kendini özniteliklerinde döndürür yüz algılama medya işlemcisi isteğe bağlı bir bileşenidir. 

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Algılama modu
Aşağıdaki modlarından birini işlemcisi tarafından kullanılabilir:

* Yüz algılama
* Yüz duygu algılama
* Birleşik duygu algılama

### <a name="job-name"></a>İş adı
İş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
**Azure medya hareket algılayıcısı** medya işlemcisi (MP), aksi takdirde uzun ve olaysız video içinde ilgi bölümleri verimli bir şekilde tanımlamak sağlar. Hareket algılama statik kamera görüntülerinin video hareket oluştuğu bölümlerini belirlemek için kullanılabilir. Zaman damgaları ve olayın gerçekleştiği sınırlayıcı bölge ile meta verileri içeren bir JSON dosyası oluşturur.

Doğru güvenlik video akışları hedeflenen, bu teknolojiyi ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi hareket kategorilere yapabiliyor. Bu, güvenlik uyarıları sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videoların ilgi dakika ayıklayın kullanabilmeye devam ederken adresinize olmadan kamera Akışları'oluşturmanıza olanak sağlar.

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Bu işlemci otomatik olarak kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir. Bu, uzun bir video beklenmesi gerekenler hızlı bir bakış sağlamak istediğinizde yararlıdır. Ayrıntılı bilgi ve örnekler için bkz: [bir Video özeti oluşturma kullanım Azure medya Video küçük](media-services-video-summarization.md)

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>İş adı
İş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl bir işin ilerleme durumunu izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="next-steps"></a>Sonraki adımlar
Görünüm Media Services'i öğrenme yolları.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

