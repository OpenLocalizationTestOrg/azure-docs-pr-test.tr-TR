---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello NewTek TriCaster Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Tricaster Canlı Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Merhaba NewTek TriCaster Kodlayıcı toosend tek bit hızlı bir canlı akışı kullanın
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental dinamik](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Bu konuda gösterilmektedir nasıl tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar Kodlayıcı toosend Canlı. Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).

Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile. Bu araç, yalnızca bir Windows Bilgisayarına çalışır. Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> Bir katkı göndermek için Tricaster kullanarak gerçek zamanlı kodlama için etkinleştirilmiş tooAMS kanallar akış zaman olabilir video/ses hatalardan Canlı olayınızın hızlı akışları arasında kesme veya grafikten maskeleme görüntülerini değiştirme gibi Tricaster belirli özelliklerini kullanıyorsanız . Merhaba AMS takım çalıştığını o zamana kadar bu sorunları düzeltmeye, onu toouse bu özellikleri değil önerilir.
>
>

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

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır. Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTMP**. Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.

    Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.

3. Tıklatın **kanal oluşturmak**.

   ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> Merhaba kanal 20 dakika toostart olarak uzun sürebilir.
>
>

Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın. Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Merhaba NewTek TriCaster Kodlayıcı yapılandırın
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
1. Yeni bir **NewTek TriCaster** hangi video giriş kaynağı kullanılan bağlı olarak proje.
2. Bu projede hello kez bulma **akış** düğmesine tıklayın ve hello dişli simgesi sonraki tooit tooaccess hello akışı yapılandırma menüsünü tıklatın.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Merhaba menü açtıktan sonra tıklatın **yeni** hello bağlantı başlığı altında. Merhaba bağlantı türü için istendiğinde seçin **Adobe Flash**.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. **Tamam** düğmesine tıklayın.
5. Bir FMLE profili şimdi hello açılan ok altında tıklayarak içeri aktarılabilir **akış profili** ve çok gezinme**Gözat**.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Toowhere gidin yapılandırılmış hello FMLE profili kaydedildi.
7. Seçin ve basın **Tamam**.

    Hello profili yüklendikten sonra toohello sonraki adıma geçin.
8. Merhaba kanalın giriş URL sırası tooassign almak, toohello Tricaster **RTMP Endpoint**.

    Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin. Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.

    Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Bu bilgileri hello yapıştırmak **konumu** altında **Flash Server** hello Tricaster projede. Ayrıca hello bir Akış adı atamak **akış kimliği** alan.

    Akış bilgi toohello FMLE profili eklediyseniz, ayrıca alınabilir toothis bölümünde tıklayarak **ayarları içeri**, kaydedilen toohello FMLE profil gezinme ve tıklatarak **Tamam**. Merhaba ilgili Flash Server alanları FMLE hello bilgileriyle doldurmanız gerekir.

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. Tamamlandığında tıklatarak **Tamam** Merhaba ekranında hello sonundaki. Video ve ses girişleri hello Tricaster içine hazır olduğunuzda hello tıklayarak tooAMS akış başlamadan **akış** düğmesi.

     ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Tıklamadan önce **akış**, size **gerekir** hello kanal hazır olduğundan emin olun.
> Ayrıca, emin olun değil tooleave hello kanal giriş katkı olmadan hazır durumda akışı > 15 dakikadan fazla.
>
>

## <a name="test-playback"></a>Testi kayıttan yürütme
Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın. Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.

Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir. Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.  

## <a name="create-a-program"></a>Bir program oluşturun
1. Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun. Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
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

## <a name="next-step"></a>Sonraki adım
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
