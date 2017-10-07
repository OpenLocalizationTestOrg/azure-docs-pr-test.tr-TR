---
title: "hello Azure portal kullanarak şirket içi kodlayıcılarda olan aaaLive akış | Microsoft Docs"
description: "Bu öğretici, doğrudan teslimat için yapılandırılmış bir kanal oluşturulması hello adım adım anlatılmaktadır."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 6f4acd95-cc64-4dd9-9e2d-8734707de326
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 1fb341e022f66f33903e13e07d3e84c0216cad77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-with-on-premises-encoders-using-hello-azure-portal"></a>Nasıl tooperform ile canlı akış kodlayıcılar hello Azure portal kullanarak şirket içi
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-live-passthrough-get-started.md)
> * [.NET](media-services-dotnet-live-encode-with-onpremises-encoders.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Bu öğreticide Azure portal toocreate hello kullanmanın hello adımlarda size yol gösterir bir **kanal** doğrudan teslimat için yapılandırılmış. 

## <a name="prerequisites"></a>Ön koşullar
Merhaba, gerekli toocomplete hello öğretici şunlardır:

* Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).
* Bir Web kamerası. Örneğin, [Telestream Wirecast kodlayıcı](http://www.telestream.net/wirecast/overview.htm).

Aşağıdaki makaleleri tooreview hello önerilir:

* [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](https://azure.microsoft.com/blog/2014/09/18/azure-media-services-rtmp-support-and-live-encoders/)
* [Azure Media Services kullanarak Canlı Akış’a genel bakış](media-services-manage-channels-overview.md)
* [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md)

## <a id="scenario"></a>Ortak canlı akış senaryosu
Hello aşağıdaki adımlar, doğrudan teslimat için yapılandırılan kanalları kullanan ortak canlı akış uygulamaları oluşturmaya dahil olan görevleri açıklamaktadır. Bu öğreticide gösterilmiştir nasıl toocreate bir geçiş kanalı ve canlı olayları ve yönetin.

>[!NOTE]
>Akış uç noktası toostream içerik istediğiniz hello hello olduğundan emin olun **çalıştıran** durumu. 
    
1. Bir video kamera tooa bilgisayara bağlayın. Çoklu bit hızlı RTMP ya da Parçalı MP4 akışı çıktısı veren bir şirket içi gerçek zamanlı kodlayıcı çalıştırın ve yapılandırın. Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.
2. Geçiş Kanalı oluşturun ve başlatın.
3. Alma hello kanal URL'sini alma. 
   
    Merhaba alma URL hello gerçek zamanlı Kodlayıcı toosend hello akış toohello kanal tarafından kullanılır.
4. Merhaba kanal Önizleme URL'sini alın. 
   
    Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.
5. Canlı olay/program oluşturun. 
   
    Azure portal kullanarak hello zaman canlı bir olay oluşturma bir varlık da oluşturur. 

6. Akışı ve arşivlemeyi hazır toostart olduğunuzda hello olayı/programı başlatın.
7. İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir. Merhaba tanıtım hello çıktı akışına eklenir.
8. Toostop akış ve arşivleme hello olayı istediğinizde hello olayı/programı durdurun.
9. Merhaba olayı/programı silin (ve isteğe bağlı olarak hello varlığını silme).     

> [!IMPORTANT]
> Lütfen gözden [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarda canlı akış](media-services-live-streaming-with-onprem-encoders.md) kavramları ve konuları hakkında toolearn ilgili toolive şirket içi kodlayıcılarda ve geçiş kanallarında canlı akış.
> 
> 

## <a name="tooview-notifications-and-errors"></a>tooview bildirimleri ve hataları
Tooview bildirimleri istiyorsanız ve hataları tarafından hello Azure portalında üretilen hello bildirim simgesine tıklayın.

![Bildirimler](./media/media-services-portal-passthrough-get-started/media-services-notifications.png)

## <a name="create-and-start-pass-through-channels-and-events"></a>Geçiş kanalları ve olayları oluşturma ve başlatma
Bir kanal toocontrol hello yayımlama ve canlı akıştaki kesimleri depolanmasını sağlayan olaylar/programlarla ilişkilidir. Kanallar olayları yönetir. 

İstediğiniz tooretain kaydedilen hello içerik hello programı ayarını hello tarafından saatleri hello sayısını belirtebilirsiniz **arşiv penceresi** uzunluğu. Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz. Arşiv penceresi uzunluğu hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler. Olayları hello belirtilen sürede çalıştırabilirsiniz ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır. Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.

Her olay bir varlıkla ilişkilidir. toopublish hello olay hello ilişkili varlığa yönelik bir OnDemand Bulucu oluşturmanız gerekir. Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild sağlar.

Bir kanal hello birden çok arşivini oluşturabilmesi için olayları eşzamanlı olarak çalışan toothree destekler, aynı gelen akışın. Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar. Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir program, ancak toobroadcast yalnızca son 10 dakikadır. tooaccomplish Bu, iki eşzamanlı olarak çalışan program toocreate gerekir. Bir program tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz. Merhaba başka bir programı kümesi tooarchive 10 dakika için ve bu program yayımlanır.

Mevcut canlı olayları yeniden kullanmamalısınız. Bunun yerine, her olay için yeni bir olay oluşturun ve başlatın.

Akışı ve arşivlemeyi hazır toostart olduğunda hello olayı başlatın. Toostop akış ve arşivleme hello olayı istediğinizde hello programı durdurun. 

Arşivlenen toodelete içerik durdurup hello olay silme ve ardından hello ilişkili varlığı silin. Bir olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir. 

Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.

Arşivlenen tooretain hello içerik istiyor ancak değil bulundurursunuz akış için, Bulucu akış hello silin.

### <a name="toouse-hello-portal-toocreate-a-channel"></a>toouse hello portal toocreate bir kanal
Bu bölümde gösterilmiştir nasıl toouse hello **hızlı Oluştur** seçeneği toocreate bir geçiş kanalı.

Geçiş kanalları hakkında daha fazla ayrıntı için bkz. [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md).

1. Merhaba, [Azure portal](https://portal.azure.com/), Azure Media Services hesabınızı seçin.
2. Merhaba, **ayarları** penceresinde tıklatın **canlı akış**. 
   
    ![Başlarken](./media/media-services-portal-passthrough-get-started/media-services-getting-started.png)
   
    Merhaba **canlı akış** penceresi görüntülenir.
3. Tıklatın **hızlı Oluştur** toocreate bir geçiş kanalı hello RTMP alma protokolüyle.
   
    Merhaba **Yeni Kanal Oluştur** penceresi görüntülenir.
4. Merhaba yeni kanala bir ad verin ve tıklayın **oluşturma**. 
   
    Bu bir geçiş kanalı ile Merhaba oluşturur RTMP alma protokolüyle.

## <a name="create-events"></a>Olay oluşturma
1. Bir olay tooadd istediğiniz bir kanal toowhich seçin.
2. **Canlı Olay** düğmesine basın.

![Olay](./media/media-services-portal-passthrough-get-started/media-services-create-events.png)

## <a name="get-ingest-urls"></a>Alma URL’leri alma
Merhaba kanal oluşturulduktan sonra alabileceğiniz toohello gerçek zamanlı Kodlayıcı sağlayacak URL'lerini alabilirsiniz. Merhaba Kodlayıcı bu URL'leri tooinput canlı akış kullanır.

![Oluşturulan](./media/media-services-portal-passthrough-get-started/media-services-channel-created.png)

## <a name="watch-hello-event"></a>Gözcü hello olay
toowatch hello olay tıklatın **izleme** akış URL'si Azure portal ya da kopyalama hello hello ve tercih ettiğiniz bir oynatıcı kullanın. 

![Oluşturulan](./media/media-services-portal-passthrough-get-started/media-services-default-event.png)

Canlı olay otomatik olarak durduğunda dönüştürülmüş tooon isteğe bağlı içerik alın.

## <a name="clean-up"></a>Temizleme
Geçiş kanalları hakkında daha fazla ayrıntı için bkz. [Çoklu bit hızı akışları oluşturan şirket içi kodlayıcılarla canlı akış](media-services-live-streaming-with-onprem-encoders.md).

* Yalnızca tüm olaylar/programlar hello kanalda vermemeye başladığında bir kanal durdurulabilir.  Merhaba kanal durdurulduktan sonra herhangi bir ücret doğurur değil. Toostart gerektiğinde bunu yeniden olacaktır kodlayıcıyı tooreconfigure gerekmeyecek şekilde hello aynı URL alma.
* Bir kanal yalnızca hello kanaldaki tüm Canlı olaylar silindiğinde silinebilir.

## <a name="view-archived-content"></a>Arşivlenen içeriği görüntüleme
Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır. Bir olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir. 

varlıklarınızı, toomanage seçin **ayarı** tıklatıp **varlıklar**.

![Varlıklar](./media/media-services-portal-passthrough-get-started/media-services-assets.png)

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

