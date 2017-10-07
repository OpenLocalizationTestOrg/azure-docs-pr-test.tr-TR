---
title: "aaaHow tooperform Azure Media Services toocreate Çoklu bit hızı akışları hello Azure portal ile kullanarak canlı akış gerçekleştirme | Microsoft Docs"
description: "Bir kanal oluşturulması hello adımlarında, tek bit hızında bir canlı akışı alır ve hello Azure portal kullanarak toomulti bit hızında akışa kodlayan Bu öğretici yetenekte."
services: media-services
documentationcenter: 
author: anilmur
manager: cfowler
editor: 
ms.assetid: 504f74c2-3103-42a0-897b-9ff52f279e23
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 963a25b8ba4683a2ce34d9fb0e19499874b4707c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-live-streaming-using-azure-media-services-toocreate-multi-bitrate-streams-with-hello-azure-portal"></a>Azure Media Services toocreate Çoklu bit hızlı kullanarak tooperform canlı akış hello Azure portal ile nasıl akışları
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-creating-live-encoder-enabled-channel.md)
> * [.NET](media-services-dotnet-creating-live-encoder-enabled-channel.md)
> * [REST API](https://docs.microsoft.com/rest/api/media/operations/channel)
> 
> 

Bu öğretici, oluşturma hello adımlarda size bir **kanal** , tek bit hızında bir canlı akışı alıp toomulti bit hızında akışa kodlayan.

> [!NOTE]
> Daha fazla kavramsal bilgi için bkz: Gerçek zamanlı kodlama için etkinleştirilmiş ilgili tooChannels [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).
> 
> 

## <a name="common-live-streaming-scenario"></a>Ortak Canlı Akış Senaryosu
Merhaba, ortak canlı akış uygulamaları oluşturmaya dahil genel adımlar verilmiştir.

> [!NOTE]
> Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir. Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.
> 
> 

1. Bir video kamera tooa bilgisayara bağlayın. Başlatma ve protokolleri aşağıdaki hello birinde tek bit hızlı akış çıkışı sağlayabilecek bir şirket içi gerçek zamanlı Kodlayıcı yapılandırın: RTMP, kesintisiz akış veya RTP (MPEG-TS). Daha fazla bilgi için bkz. [Azure Media Services RTMP Desteği ve Gerçek Zamanlı Kodlayıcılar](http://go.microsoft.com/fwlink/?LinkId=532824).
   
    Bu adım, Kanalınızı oluşturduktan sonra da gerçekleştirilebilir.
2. Bir Kanal oluşturup başlatın. 
3. Alma hello kanal URL'sini alma. 
   
    Merhaba alma URL hello gerçek zamanlı Kodlayıcı toosend hello akış toohello kanal tarafından kullanılır.
4. Merhaba kanal Önizleme URL'sini alın. 
   
    Kanalınızı hello Canlı akışı düzgün şekilde aldığını bu URL tooverify kullanın.
5. Bir olay/program oluşturun (ayrıca bir varlık oluşturur). 
6. (Merhaba ilişkili varlığa yönelik bir OnDemand Bulucu oluşturulur) hello olayı yayımlayın.    
7. Akışı ve arşivlemeyi hazır toostart olduğunda hello olayı başlatın.
8. İsteğe bağlı olarak, gerçek zamanlı Kodlayıcı hello iş toostart bir tanıtım olabilir. Merhaba tanıtım hello çıktı akışına eklenir.
9. Toostop akış ve arşivleme hello olayı istediğinizde hello olayı durdurun.
10. Merhaba olay silin (ve isteğe bağlı olarak hello varlığını silme).   

## <a name="in-this-tutorial"></a>Bu öğreticide
Bu öğreticide, hello Azure portal kullanılan tooaccomplish hello görevleri aşağıdaki gibidir: 

1. Bir kanal oluşturmak diğer bir deyişle etkin tooperform gerçek zamanlı kodlama.
2. Get hello alım URL'sini sipariş toosupply onu toolive Kodlayıcı. Merhaba gerçek zamanlı Kodlayıcı bu URL tooingest hello akış kanal hello kullanır.
3. Bir olay/program (ve bir varlık) oluşturma.
4. Merhaba varlık yayımlama ve akış URL'lerini alma.  
5. İçeriğinizi oynatın.
6. Temizleme.

## <a name="prerequisites"></a>Ön koşullar
Merhaba, gerekli toocomplete hello öğretici verilmiştir.

* toocomplete Bu öğretici bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. 
  Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/).
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [hesap oluştur](media-services-portal-create-account.md).
* Bir web kamerası ve tek bit hızlı bir canlı akış gönderebilen bir kodlayıcı.

## <a name="create-a-channel"></a>Kanal oluşturma
1. Merhaba, [Azure portal](https://portal.azure.com/), Media Services seçin ve ardından, Media Services hesap adına tıklayın.
2. **Canlı Akış**’ı seçin.
3. **Özel oluştur**’u seçin. Bu seçenek canlı kodlama için etkinleştirilmiş bir kanal oluşturmanızı sağlar.
   
    ![Kanal oluşturma](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-channel.png)
4. **Ayarlar**’a tıklayın.
   
   1. Merhaba seçin **gerçek zamanlı kodlama** kanal türü. Bu tür, gerçek zamanlı kodlama için etkinleştirilmiş bir kanal toocreate istediğinizi belirtir. Anlamına gelen tek bit hızlı hello akış toohello kanal gönderilir ve belirlenmiş gerçek zamanlı Kodlayıcı ayarları kullanılarak Çoklu bit hızında akışa kodlanır. Daha fazla bilgi için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md). Tamam'a tıklayın.
   2. Bir kanalın adını belirtin.
   3. Merhaba ekranın hello Tamam düğmesini tıklatın.
5. Select hello **alma** sekmesi.
   
   1. Bu sayfada bir akış protokolü seçebilirsiniz. Hello için **gerçek zamanlı kodlama** kanal türü, geçerli protokol Seçenekler şunlardır:
      
      * Tek bit hızlı Parçalanmış MP4 (Kesintisiz Akış)
      * Tek bit hızlı RTMP
      * RTP (MPEG-TS): RTP üzerinden MPEG-2 Aktarım Akışı.
        
        Her protokolü hakkında ayrıntılı açıklamalar için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).
        
        Merhaba kanal hatayla hello protokol seçeneği değiştirilemiyor veya ilişkili olaylar/programları çalışmıyor. Farklı protokollere ihtiyacınız varsa her bir akış protokolü için farklı bir kanal oluşturmalısınız.  
   2. IP kısıtlama üzerinde hello geçerli alma. 
      
       Merhaba IP tanımlayabilirsiniz adreslerinin bir video toothis kanal tooingest izin verilir. İzin verilen IP adresleri, tek bir IP adresi (ör. '10.0.0.1'), bir IP adresi ve CIDR alt ağ maskesi kullanarak bir IP aralığı (ör. ‘10.0.0.1/22’) veya bir IP adresi ve noktalı ondalık alt ağ maskesi kullanarak bir IP aralığı (ör. '10.0.0.1(255.255.252.0)').
      
       Herhangi bir IP adresi belirtilmezse ve bir kural tanımı yoksa hiçbir IP adresine izin verilmez. tooallow herhangi bir IP adresi, bir kural oluşturun ve 0.0.0.0/0 olarak ayarlayın.
6. Merhaba üzerinde **Önizleme** sekmesinde, IP kısıtlama hello preview geçerli.
7. Merhaba üzerinde **kodlama** sekmesinde, hello kodlama hazır belirtin. 
   
    Şu anda yalnızca sistem hello seçebileceğiniz hazır **720 p varsayılan**. toospecify özel hazır ayarı, Microsoft destek bileti açın. Merhaba hello adını enter sizin için oluşturduğu hazır. 

> [!NOTE]
> Şu anda hello kanalın başlaması too30 dakika sürebilir. Kanal sıfırlanması too5 dakika sürebilir.
> 
> 

Merhaba kanalı oluşturduktan sonra hello kanalda tıklatın ve seçin **ayarları** kanal yapılandırmalarınızı görüntüleyebileceğiniz. 

Daha fazla bilgi için bkz: [toocreate Çoklu bit hızı akışları Azure Media Services kullanarak canlı akış](media-services-manage-live-encoder-enabled-channels.md).

## <a name="get-ingest-urls"></a>Alma URL’leri alma
Merhaba kanal oluşturulduktan sonra alabileceğiniz toohello gerçek zamanlı Kodlayıcı sağlayacak URL'lerini alabilirsiniz. Merhaba Kodlayıcı bu URL'leri tooinput canlı akış kullanır.

![ingesturls](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-ingest-urls.png)

## <a name="create-and-manage-events"></a>Olay oluşturma ve yönetme
### <a name="overview"></a>Genel Bakış
Bir kanal toocontrol hello yayımlama ve canlı akıştaki kesimleri depolanmasını sağlayan olaylar/programlarla ilişkilidir. Olayları/programları kanallar yönetir. Merhaba kanal ve Program burada bir kanal sabit bir içerik akışının bulunduğu ve bir programın bu kanalda zaman aşımına kapsamlı toosome olay çok benzer tootraditional medya ilişkidir.

İstediğiniz tooretain kaydedilen hello içerik hello olayı için ayarı hello tarafından saatleri hello sayısını belirtebilirsiniz **arşiv penceresi** uzunluğu. Bu değer en az 5 dakika tooa en çok 25 saat ayarlayabilirsiniz. Arşiv penceresi uzunluğu hello maksimum istemcileri hello geçerli Canlı konumdan geçmişe arama süre miktarını da belirler. Olayları hello belirtilen sürede çalıştırabilirsiniz ancak hello pencere uzunluğunun gerisine düşen içerik sürekli olarak atılır. Bu özelliğin bu değeri bildirimleri büyüyebilir ne kadar süreyle hello istemci de belirler.

Her olay bir Varlıkla ilişkilidir. Merhaba yönelik bir OnDemand Bulucu oluşturmanız gerekir toopublish hello olay varlık ilişkilendirilmiş. Bu bulucuya sahip olmak tooyour istemcileri sağlayabilen bir akış URL'si toobuild olanak sağlar.

Bir kanal hello birden çok arşivini oluşturabilmesi için olayları eşzamanlı olarak çalışan toothree destekler, aynı gelen akışın. Bu, gerektiği gibi bir olay toopublish ve Arşiv farklı kısımlarını sağlar. Örneğin, iş gereksiniminiz tooarchive 6 saatlik bir olay, ancak toobroadcast yalnızca son 10 dakikadır. tooaccomplish Bu, iki eşzamanlı olarak çalışan toocreate gereken olay. Bir olay tooarchive hello olay 6 saatlik ayarlandı ancak hello program yayımlanamaz. Merhaba diğer olay kümesi tooarchive 10 dakika için ve bu program yayımlanır.

Yeni olaylar için mevcut programları yeniden kullanmamalısınız. Bunun yerine, her olay için yeni bir program oluşturup başlatın.

Akışı ve arşivlemeyi hazır toostart olduğunuzda olayı/programı başlatın. Toostop akış ve arşivleme hello olayı istediğinizde hello olayı durdurun. 

Arşivlenen toodelete içerik durdurup hello olay silme ve ardından hello ilişkili varlığı silin. Merhaba olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir. 

Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır.

Arşivlenen tooretain hello içerik istiyor ancak değil bulundurursunuz akış için, Bulucu akış hello silin.

### <a name="createstartstop-events"></a>Olay oluşturma/başlatma/durdurma
Merhaba kanala akması hello akış olduktan sonra olay bir varlık, Program ve akış Bulucu oluşturarak akış hello başlayabilirsiniz. Merhaba akış arşivlemek ve hello akış uç noktası aracılığıyla kullanılabilir tooviewers yapın. 

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

İki yolu toostart olay vardır: 

1. Merhaba gelen **kanal** sayfasında, basın **canlı olay** tooadd yeni bir olay.
   
    Şunları belirleyin: olay adı, varlık adı, arşiv penceresi ve şifreleme seçeneği.
   
    ![createprogram](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-create-program.png)
   
    Bırakılırsa **bu canlı olay Şimdi Yayımla** işaretli hello olay hello yayımlama URL'leri oluşturulur.
   
    Basabilirsiniz **Başlat**, hazır toostream hello olay olduğunda.
   
    Merhaba olay başladıktan sonra basabilirsiniz **izleme** hello içeriği oynatmayı toostart.
2. Alternatif olarak, bir kısayol ve tuşuna kullanabilirsiniz **Go Live** hello düğmesinde **kanal** sayfası. Bunun yapılması varsayılan bir Varlık, Program ve Akış Bulucu oluşturur.
   
    Merhaba olay adlandırılan **varsayılan** ve hello arşiv penceresi ayarlanmış too8 saat.

Merhaba yayımlanan hello olayından izleyebilirsiniz **canlı olay** sayfası. 

**Çevrimdışı** seçeneğine tıklarsanız tüm canlı olaylar durdurulur. 

## <a name="watch-hello-event"></a>Gözcü hello olay
toowatch hello olay tıklatın **izleme** akış URL'si Azure portal ya da kopyalama hello hello ve tercih ettiğiniz bir oynatıcı kullanın. 

![Oluşturulan](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-play-event.png)

Canlı olay otomatik olarak durduğunda olayları tooon isteğe bağlı içerik dönüştürür.

## <a name="clean-up"></a>Temizleme
Olayların akışla yapılır ve önceden sağlanan hello kaynakları tooclean istiyorsanız hello aşağıdaki yordamı izleyin.

* Merhaba kodlayıcıdan Hello akışı göndermeyi durdurun.
* Merhaba kanalı durdurun. Merhaba kanal durdurulduktan sonra herhangi bir ücret uygulanmaz. Toostart gerektiğinde bunu yeniden olacaktır kodlayıcıyı tooreconfigure gerekmeyecek şekilde hello aynı URL alma.
* Canlı olayınızın bir isteğe bağlı akış olarak toocontinue tooprovide hello arşiv istemiyorsanız akış uç noktanızı durdurabilirsiniz. Merhaba kanal durdurulmuş durumda ise, herhangi bir ücret uygulanmaz.

## <a name="view-archived-content"></a>Arşivlenen içeriği görüntüleme
Durdur ve hello olay silme bile sonra kullanıcılar hello hello varlığı silmediğiniz sürece mümkün toostream, arşivlenen içeriğinizin isteğe bağlı video için olacaktır. Bir olay tarafından kullanılıyorsa varlık silinemez; Merhaba olay silinmesi gerekir. 

varlıklarınızı, toomanage seçin **ayarı** tıklatıp **varlıklar**.

![Varlıklar](./media/media-services-portal-creating-live-encoder-enabled-channel/media-services-assets.png)

## <a name="considerations"></a>Dikkat edilmesi gerekenler
* Şu anda hello en fazla canlı bir olay süresi önerilen 8 saattir. Uzun süreyle toorun bir kanal gerekiyorsa lütfen amslived@Microsoft.com adresine başvurun.
* Akış içeriğinizi toostream istediğiniz uç hello hello olduğundan emin olun **çalıştıran** durumu.

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

