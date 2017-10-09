---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello Telestream Wirecast Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Wirecast Canlı Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Merhaba Wirecast Kodlayıcı toosend tek bit hızlı bir canlı akışı kullanın
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental dinamik](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Bu konuda gösterilmektedir nasıl tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar Kodlayıcı toosend Canlı.  Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).

Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile. Bu araç, yalnızca bir Windows Bilgisayarına çalışır. Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Ön koşullar
* [Bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md)
* Çalıştıran bir akış uç olduğundan emin olun. Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md)
* Merhaba Hello en son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.
* Merhaba aracını başlatmak ve tooyour AMS hesabının bağlanın.

## <a name="tips"></a>İpuçları
* Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.
* Bir iyi bant genişliği gereksinimlerini belirlerken bit akış toodouble hello udur. Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı hello etkisini azaltmaya yardımcı olur.
* Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.

## <a name="create-a-channel"></a>Kanal oluşturma
1. Toohello Hello AMSE aracında gezinmek **canlı** sekmesinde ve hello kanal alanı içinde sağ tıklatın. Seçin **kanal oluştur...** Başlangıç menüsünden.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır. Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTMP**. Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.

    Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.

3. Tıklatın **kanal oluşturmak**.

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> Merhaba kanal 20 dakika toostart olarak uzun sürebilir.
>
>

Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın. Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Merhaba Telestream Wirecast Kodlayıcı yapılandırın
Bu öğretici hello aşağıdaki çıkış ayarları kullanılır. Bu bölümde Hello kalanı daha ayrıntılı yapılandırma adımlarını açıklar.

**Video**:

* Codec: H.264
* Profil: Yüksek (düzeyi 4.0)
* Bit hızı: 5000 KB/sn
* Anahtar kare: 2 saniye (60 saniye)
* Çerçeve oranı: 30

**Ses**:

* Codec: AAC (LC)
* Bit hızı: 192 Kb/sn
* Örnek Hızı: 44,1 kHz

### <a name="configuration-steps"></a>Yapılandırma adımları
1. Merhaba Telestream Wirecast uygulaması makine hello olan üzerinde kullanılan ve RTMP akış için ayarlanan açın.
2. Hello çıktı toohello giderek yapılandırma **çıkış** sekmesi ve seçerek **çıktı ayarları...** .

    Merhaba emin olun **Çıkış hedefini** çok ayarlanır**RTMP sunucusu**.
3. **Tamam** düğmesine tıklayın.
4. Merhaba Hello Ayarları sayfasında ayarlamak **hedef** alan toobe **Azure Media Services**.

    Merhaba kodlama profili önceden seçili çok**Azure H.264 720 p 16:9 (1280 x 720)**. toocustomize bu ayarlar, select hello dişli simgesi toohello hello sağındaki açılan ve ardından **yeni önceden**.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Encoder hazır ayarlarını yapılandırın.

    Ad hello önceden ve için önerilen ayarları hello aşağıdakileri denetleyin:

    **Video**

   * Kodlayıcı: MainConcept H.264
   * Saniyedeki çerçeve sayısı: 30
   * Ortalama bit hızı: 5000 kbit/sn (ayarlanabilir ağ sınırlamalar tabanlı)
   * Profil: ana
   * Anahtar çerçevesi her: 60 çerçeveler

    **Ses**

   * Hedef bit hızı: 192 kbit/sn
   * Örnek Hızı: 44,100 kHz

     ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Tuşuna **kaydetmek**.

    Merhaba Encoding alanı artık yeni oluşturulan hello profili seçilebilir sahiptir.

    Merhaba yeni bir profil seçili olduğundan emin olun.
7. Merhaba kanalın giriş URL sırası tooassign almak, toohello Wirecast **RTMP Endpoint**.

    Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin. Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.

    Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. Merhaba Wirecast içinde **çıkış ayarları** penceresinde hello bu bilgileri yapıştırmak **adresi** hello çıkış bölümü ve ata Akış adı alanı.

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. **Tamam**’ı seçin.
2. Merhaba ana üzerinde **Wirecast** hazır olduğunuzda, video ve ses giriş kaynağı onaylayın ve ardından isabet **akış** hello üst sol alt köşesindeki.

   ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Tıklamadan önce **akış**, size **gerekir** hello kanal hazır olduğundan emin olun.
> Ayrıca, emin olun değil tooleave hello kanal giriş katkı olmadan hazır durumda akışı > 15 dakikadan fazla.
>
>

## <a name="test-playback"></a>Testi kayıttan yürütme

Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın. Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.

Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir. Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.  

## <a name="create-a-program"></a>Bir program oluşturun
1. Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun. Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
2. Ad hello program ve gerekli olursa, hello ayarlamak **arşiv penceresi uzunluğu** (hangi Varsayılanları too4 saat). Ayrıca, bir depolama konumu belirtin veya hello varsayılan olarak bırakın.  
3. Merhaba denetleyin **Şimdi Başlat hello Program** kutusu.
4. Tıklatın **Program oluşturma**.  

   >[!NOTE]
   >Program oluşturma kanal oluşturma daha az zaman alır.
       
5. Merhaba program çalışmaya başladıktan sonra kayıttan yürütme hello program sağ tıklatıp çok gezinme onaylayın**kayıttan yürütme hello edinin** seçilerek **Azure Media Player ile**.  
6. Onaylandıktan sonra sağ hello program yeniden tıklatın ve seçin **kopyalama hello çıkış URL tooClipboard** (veya bu bilgileri hello almak **Program bilgilerine ve ayarlarına** hello menü seçeneğinden).

Merhaba şimdi bir oynatıcı katıştırılmış hazır toobe akışıdır veya dağıtılmış tooan kitlesi Canlı görüntüleme.  

## <a name="troubleshooting"></a>Sorun giderme
Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
