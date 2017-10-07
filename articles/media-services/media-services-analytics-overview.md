---
title: aaaMedia Analytics hello Media Services platformunda | Microsoft Docs
description: "Medya analizi, Kurumsal ölçek, uyumluluk, güvenlik ve genel ulaşma konuşma ve bilgisayar görme hizmetler koleksiyonu genel önizlemesi genel bakış"
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: c56e3781-8510-4f7f-b5ff-a218c1bb6f4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2017
ms.author: milanga;juliako;johndeu
ms.openlocfilehash: 7545f0532d7618164ebe65e2f4232c5f63453cfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-analytics-on-hello-media-services-platform"></a>Medya analizi hello Media Services platformda
## <a name="overview"></a>Genel Bakış
Daha fazla kuruluşlar video tercih edilen Orta tootrain hello gibi çalışanların kullanıyorsanız, müşterileri ve belge iş işlevleri gerçekleştirmesine. Sağlayan bir şekilde toostore bulut akış ve bu büyük medya dosyalarını erişebilirsiniz. Ancak bir şirketin kitaplığı video içeriğinin büyüdükçe Öngörüler Merhaba içeriğine ayıklanması, eşit etkili bir yol gerekiyor. 

tooaddress Azure Media Services bu büyüyen gereksiniminin Azure medya analizi sunar. Medya analizi, kuruluş ve işletmelerin tooderive eyleme dönüştürülebilir Öngörüler kendi video dosyalarından kolaylaştırır konuşma ve görme bileşenidir koleksiyonudur. Merhaba çekirdek Media Services platform bileşenleri kullanılarak oluşturulmuş, medya analizi medya gün bir ölçekte işleme işleyebilir.

Medya Analizi ile geliştiricilerin hızla Gelişmiş video işlevselliği uygulamalara kullanıma sunabilirsiniz. Kurumsal ortamlarda hello tam ölçekli, uyumluluk, güvenlik ve büyük kuruluşlar tarafından gerekli genel erişim sağlar.

Merhaba Aşağıdaki diyagramda medya analizi ve hello Media Services platformunun diğer başlıca parçaları gösterilmektedir. 

![VoD iş akışı](./media/media-services-analytics-overview/media-services-analytics-overview01.png)

Medya Analizi medya işlemcileri MP4 veya JSON dosyaları üretir. Medya işlemcisi bir MP4 dosyası oluşturursa hello dosyayı aşamalı olarak indirebilirsiniz. Medya işlemcisi bir JSON dosyası oluşturursa, Azure Blob depolama alanından hello dosyayı indirebilirsiniz. 

## <a name="media-analytics-services"></a>Medya analizi hizmetlerinden

### <a name="indexer"></a>Dizinleyici
Azure Media Indexer ile aranabilir içerik ve kapalı açıklamalı parçaları oluşturmak yapabilirsiniz. Karşılaştırılan toohello önceki sürümü, Azure Media Indexer 2 Önizleme hızlı dizin oluşturma ve daha geniş dil desteği içerir. Desteklenen diller, İngilizce, İspanyolca, Fransızca, Almanca, İtalyanca, Çince, Portekizce ve Arapça içerir. Ayrıntılı bilgi ve örnekler için bkz: [Azure Media Indexer 2 ile video işleme](media-services-process-content-with-indexer2.md).
### <a name="hyperlapse"></a>Hyperlapse
Microsoft Hyperlapse video sabitlemeyi ve zaman atlama yetenek toocreate hızlı, kaynaklarda videoların uzun formlu içeriğinizi birleştirir. Zaman atlama video oluşturmanın yanı sıra Hyperlapse toocreate kararlı videoların cep telefonları ve kameralar aracılığıyla yakalanan shaky videolar kullanabilirsiniz. Ayrıntılı bilgi ve örnekler için bkz: [Hyperlapse Azure medya Hyperlapse ile medya dosyalarını](media-services-hyperlapse-content.md).
### <a name="motion-detector"></a>Hareket Algılayıcısı
Hareket algılayıcısı toodetect hareket video sabit arka plan ile kullanabilirsiniz. Bu, hatalı pozitif sonuç için olası toocheck hareket olayları izleme kameralarını tarafından algılanan kolaylaştırır. Ayrıntılı bilgi ve örnekler için bkz: [hareket algılama Azure medya analizi için](media-services-motion-detection.md).
### <a name="face-detector"></a>Yüz Algılayıcısı
Yüz algılayıcısı kullanarak, kişilerin yüzeyleri ve mutluluk, sadness ve beklenmedik biçimde dahil olmak üzere kendi duygular algılayabilir. Bu, toplama ve analiz etme tepki olaya katılan kişilerin de dahil olmak üzere daha sonra açıklanan çeşitli yararlı endüstri uygulamalar, sahiptir. Ayrıntılı bilgi ve örnekler için bkz: [Azure medya analizi için yüz ve duygu algılama](media-services-face-and-emotion-detection.md).
### <a name="video-summarization"></a>Video özetleme
Video özetleme otomatik olarak hello kaynak video ilginç parçacıkları'i seçerek uzun videoları özetlerini oluşturmanıza yardımcı olabilir. Bu özellik, tooprovide hangi tooexpect uzun videoda hızlı bir genel bakış istediğinizde yararlıdır. Ayrıntılı bilgi ve örnekler için bkz: [kullanım Azure medya Video küçük resimleri toocreate video özetleme](media-services-video-summarization.md).
### <a name="optical-character-recognition"></a>Optik karakter tanıma
Azure Media ORC (optik karakter tanıma) ile video dosyaları metin içeriği düzenlenebilir, aranabilir dijital metne dönüştürebilirsiniz. Ardından hello video sinyali medyanızın anlamlı meta verilerin hello ayıklama otomatik hale getirebilirsiniz.
### <a name="scalable-face-redaction"></a>Ölçeklenebilir yüz Redaksiyon
Azure Media Redactor ölçeklenebilir yüz Redaksiyon hello bulutta sunan medya analizi medya işlemcisi ' dir. Yüz Redaksiyon kullanarak, seçilen kişilerin, video tooblur yüzeyleri değiştirebilirsiniz. Toouse hello yüz Redaksiyon hizmet haber ortamda veya ortak güvenlik söz konusu olduğunda isteyebilirsiniz. Saat tooredact el ile birden çok yüzeyleri içeren çekimi birkaç dakika sürebilir, ancak bu hizmetle yüz Redaksiyon birkaç basit adımla alır. Merhaba daha fazla bilgi için bkz: [Redaksiyon yüzeyleri Azure medya Analizi ile](media-services-face-redaction.md) makalesi.

## <a name="common-scenarios"></a>Genel senaryolar
Medya analizi kuruluşlara yardımcı olur ve işletmelerin video ilişkin yeni bilgiler glean ve daha etkili bir şekilde video içeriği büyük miktarda yönetin. Burada, çeşitli senaryolar vardır:

* **Çağrı merkezleri**. Hatta hello geliştirilirken sosyal medya ile müşteri çağrı merkezleri hala müşteri hizmetleri işlemleri büyük bir yüzdesini kolaylaştırır. Bu ses verilerde büyük miktarda olabilir müşteri bilgi tooachieve daha yüksek müşteri memnuniyetini analiz kodlanır. Kuruluşlar, medya Dizin Oluşturucu kullanarak metin ayıklayın ve arama dizinlerini ve panolar oluşturmaya başlayın. Ardından bunlar yaygın şikayetlerinden, şikayetlerinden kaynaklarını ve diğer ilgili verileri çevresinde Intelligence ayıklayabilirsiniz.
* **Kullanıcı tarafından oluşturulmuş içerik yönetimini**. Haber medya çıkışlar toopolice bölümlerden çoğu kuruluş, videolar ve resimler gibi kullanıcı tarafından oluşturulan medya kabul genel kullanıma yönelik portalları sahiptir. İçerik Hello hacmi toounexpected olaylar ani değişiklik. Bu senaryolarda, bu site için içeriği etkili el ile incelemeler zor tooconduct olur. Müşteriler, uygun olan içerik üzerinde hello içerik yönetimini hizmet toofocus üzerinde güvenebilirsiniz.
* **İzleme**. Merhaba ile kullanımı büyüme IP kamera gözetleme video büyüyen bir envanterini gelir. El ile izleme video gözden geçirme zamanı yoğun ve saldırıya toohuman hatasına neden olur. Medya analizi hareket algılama, yüz algılama ve gözden geçirme, yönetme ve türevleri daha kolay oluşturma Hyperlapse toomake hello işlemi gibi hizmetleri sağlar.

## <a name="media-analytics-media-processors"></a>Medya analizi medya işlemcileri
Bu bölümün listeleri hello medya analizi medya işlemcileri ve programlarını nasıl toouse .NET veya REST tooget medya işlemci (MP) nesnesi.

### <a name="mp-names"></a>MP adları
* Azure Media Indexer 2 Önizleme
* Azure Media Indexer
* Azure Media Hyperlapse
* Azure Media Face Detector
* Azure Media Motion Detector
* Azure Media Video Thumbnails
* Azure Media OCR

### <a name="net"></a>.NET
Merhaba, bir işlev alır aşağıdaki hello belirtilen MP adları ve bir MP nesnesi döndürür.

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
            .Where(p => p.Name == mediaProcessorName)
            .ToList()
            .OrderBy(p => new Version(p.Version))
            .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }


### <a name="rest"></a>REST
İsteği:

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Azure%20Media%20OCR' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.12
    Host: media.windows.net

Yanıtı:

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:074c3899-d9fb-448f-9ae1-4ebcbe633056",
             "Description":"Azure Media OCR",
             "Name":"Azure Media OCR",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }

## <a name="demos"></a>Gösterileri
Bkz: [Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html).

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>İlgili makaleler
Bkz: [medya Hizmetleri analizi duyuru](https://azure.microsoft.com/blog/introducing-azure-media-analytics/).

<!-- Images -->

[overview]: ./media/media-services-video-on-demand-workflow/media-services-video-on-demand.png
