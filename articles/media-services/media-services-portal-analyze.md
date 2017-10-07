---
title: aaaAnalyze hello Azure portal kullanarak medya | Microsoft Docs
description: "Bu konuda ele alınmıştır nasıl medyanızı kullanarak medya analizi medya işlemcileri (Mp'leri) ile Azure portal hello tooprocess."
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
ms.openlocfilehash: d549c0315cd58c3771420379316b4f2ad3c2cea6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-media-using-hello-azure-portal"></a>Hello Azure portal kullanarak medya Çözümle
> [!NOTE]
> toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
> 
> 

## <a name="overview"></a>Genel Bakış
Azure Media Services analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler için kendi video dosyalarından kolaylaştıran konuşma ve görme bileşenler (Kurumsal ölçek, uyumluluk, güvenlik ve genel ulaşma) koleksiyonudur. Daha ayrıntılı Azure Media Services Analytics'e genel bakış için bkz: [bu](media-services-analytics-overview.md) konu. 

Bu konuda ele alınmıştır nasıl medyanızı kullanarak medya analizi medya işlemcileri (Mp'leri) ile Azure portal hello tooprocess. Medya analizi Mp'leri MP4 veya JSON dosyaları üretir. Medya işlemcisi bir MP4 dosyası oluşturduysa hello dosyayı aşamalı olarak indirebilirsiniz. Medya işlemcisi bir JSON dosyası oluşturduysa hello Azure blob depolama hello dosyayı indirebilirsiniz. 

## <a name="choose-an-asset-that-you-want-tooanalyze"></a>Bir varlığı seçin tooanalyze istiyor
1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. Merhaba, **ayarları** penceresinde, seçin **varlıklar**.  
   .
    ![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze001.png)
3. İstediğiniz select hello varlık tooanalyze ve tuşuna hello **Çözümle** düğmesi.
   
    ![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze002.png)
4. Merhaba, **medya analizi medya varlıkla işlem** penceresinde, select hello işlemci. 
   
    Merhaba makalenin devamında, hello açıklar neden ve nasıl toouse her işlemci. 
5. Tuşuna **oluşturma** toohello bir proje başlatın.

## <a name="azure-media-indexer"></a>Azure Media Indexer
Merhaba **Azure Media Indexer** medya işlemcisi sağlar toomake medya dosyaları ve içerik aranabilir, yanı sıra kapalı açıklamalı alt yazı parçaları oluşturur. Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze003.png)

### <a name="language"></a>Dil
Merhaba doğal dil toobe Hello multimedya dosyasında tanınmıyor. Örneğin, İngilizce ve İspanyolca. 

### <a name="captions"></a>Resim yazıları
İçeriğinizi oluşturulan açıklamalı alt yazı biçimi seçebilirsiniz. Bir dizin oluşturma işi kapalı açıklamalı alt yazı dosyaları biçimleri aşağıdaki hello oluşturabilirsiniz:  

* **SAMI**
* **TTML**
* **WebVTT**

Bu biçimler kapalı açıklamalı alt yazı (CC) dosyalarında kullanılan toomake ses olabilir ve erişilebilir toopeople işitme engelli ile video dosyaları.

### <a name="aib-file"></a>AIB dosyası
Özel SQL Server IFilter ile kullanılmak üzere toogenerate hello ses dizin Blob dosya gibi hello, bu seçeneği belirleyin. Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/using-aib-files-with-azure-media-indexer-and-sql-server/) blogu.

### <a name="keywords"></a>Anahtar sözcükler
Anahtar sözcükler XML dosyası toogenerate istiyorsanız bu seçeneği belirleyin. Bu dosya, sıklığı ve uzaklık bilgileri hello konuşma içerikten ayıklanan anahtar sözcükler içeriyor.

### <a name="job-name"></a>İş adı
Hello iş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="azure-media-hyperlapse"></a>Azure Media Hyperlapse
Azure medya Hyperlapse ilk kişi veya eylem kamera içerikten kesintisiz zaman onlara videolar oluşturan bir MP ' dir.  Daha fazla bilgi için [bu](media-services-hyperlapse-content.md) konu başlığına bakın. Bu bölüm bu MP için belirlediğiniz seçenekleri ile ilgili bazı ayrıntılar sağlar.

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze004.png)

### <a name="speed"></a>Hız
Hangi toospeed hello giriş video yukarı ile Merhaba hızını belirtin. Merhaba çıkışı sabit ve zaman onlara yorumlama hello giriş videonun yapılır.

### <a name="job-name"></a>İş adı
Hello iş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="azure-media-face-detector"></a>Azure Media Face Detector
Merhaba **Azure medya yüz algılayıcısı** medya işlemcisi (MP) etkinleştirir, size, toocount, izleme hareketleri ve hatta ölçer İzleyici katılım ve tepki yüz ifadeleri aracılığıyla. Bu hizmet, iki özellik içerir: 

* **Yüz algılama**
  
    Yüz algılama bulur ve video içinde İnsan yüzeyleri izler. Birden çok yüzeyleri algılanabilir ve bunların geçici bir JSON dosyası döndürülen hello zaman ve yer meta verilerle taşırken sonradan izlenmesi. İzleme sırasında toogive obstructed veya kısaca hello çerçeve bırakın olsa bile hello kişi ekranında dolaşma sırada aynı yönde tutarlı bir kimliği toohello dener.
  
  > [!NOTE]
  > Bu hizmetler, yüz tanıma gerçekleştirmez. Merhaba çerçeve ayrıldığında ya da için obstructed hale bir kişi döndürmeleri zaman uzun yeni bir kimlik verilir.
  > 
  > 
* **Duygu algılama**
  
    Duygu algılama hello analiz mutluluk, sadness, Korku, öfke ve daha fazlası da dahil olmak üzere algılandı, hello yüzeyleri birden çok kendini özniteliklerinde döndürür yüz algılama medya işlemcisi isteğe bağlı bir bileşenidir. 

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze005.png)

### <a name="detection-mode"></a>Algılama modu
Modları aşağıdaki hello birini hello işlemcisi tarafından kullanılabilir:

* Yüz algılama
* Yüz duygu algılama
* Birleşik duygu algılama

### <a name="job-name"></a>İş adı
Hello iş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="azure-media-motion-detector"></a>Azure Media Motion Detector
Merhaba **Azure medya hareket algılayıcısı** , tooefficiently aksi uzun ve olaysız video içinde ilgi bölümleri tanımlamak medya işlemci (MP) etkinleştirir. Hareket algılama hareket oluştuğu statik kamera görüntülerinin tooidentify bölümlerini hello video üzerinde kullanılabilir. Zaman damgaları ve bölge hello olayın gerçekleştiği sınırlayıcı hello meta verileri içeren bir JSON dosyası oluşturur.

Doğru güvenlik video akışları hedeflenen, bu mümkün toocategorize hareket ilgili olayları ve hatalı pozitif sonuç gölgeleri ve aydınlatma değişiklikleri gibi teknolojisidir. Bu işlem, sonsuz ilgisiz olaylarıyla aşırı uzun gözetleme videolar gelen ilgi mümkün tooextract dakika devam ederken adresinize olmadan kamera akışları toogenerate güvenlik uyarıları sağlar.

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze006.png)

## <a name="azure-media-video-thumbnails"></a>Azure Media Video Thumbnails
Bu işlemci otomatik olarak hello kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir. Tooprovide hangi tooexpect uzun videoda hızlı bir genel bakış istediğinizde kullanışlıdır. Ayrıntılı bilgi ve örnekler için bkz: [kullanım Azure medya Video küçük resimleri tooCreate bir Video özeti](media-services-video-summarization.md)

![Videolar Çözümle](./media/media-services-portal-analyze/media-services-portal-analyze008.png)

### <a name="job-name"></a>İş adı
Hello iş belirlemenize olanak sağlayan bir kolay ad. [Bu](media-services-portal-check-job-progress.md) makalede nasıl hello işinin ilerlemesini izleyebilirsiniz. 

### <a name="output-file"></a>Çıkış dosyası
Merhaba çıkış içeriği belirlemenize olanak sağlayan bir kolay ad. 

## <a name="next-steps"></a>Sonraki adımlar
Görünüm Media Services'i öğrenme yolları.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

