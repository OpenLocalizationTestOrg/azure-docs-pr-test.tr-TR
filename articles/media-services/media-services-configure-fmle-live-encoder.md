---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello FMLE Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Flash medya Canlı Kodlayıcı (FMLE) Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3113f333-517a-47a1-a1b3-57e200c6b2a2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: 780d911c5186ec09c784264f9a0d0c3f8059d305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-fmle-encoder-toosend-a-single-bitrate-live-stream"></a>Merhaba FMLE Kodlayıcı toosend tek bit hızlı bir canlı akışı kullanın
> [!div class="op_single_selector"]
> * [FMLE](media-services-configure-fmle-live-encoder.md)
> * [Elemental dinamik](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
>
>

Bu konuda gösterilmektedir nasıl tooconfigure hello [Flash medya Canlı Kodlayıcı](http://www.adobe.com/products/flash-media-encoder.html) (FMLE) Kodlayıcı toosend tek bit hızlı akış gerçek zamanlı kodlama için etkinleştirilmiş tooAMS kanallar. Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).

Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile. Bu araç, yalnızca bir Windows Bilgisayarına çalışır. Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).

Bu öğretici AAC kullanmayı açıklar unutmayın. Ancak, FMLE değil destekler AAC varsayılan olarak. Toopurchase AAC kodlama için bir eklenti MainConcept uğradıysa gibi ihtiyacınız: [AAC eklentisi](http://www.mainconcept.com/products/plug-ins/plug-ins-for-adobe/aac-encoder-fmle.html)

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

    ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle1.png)

2. Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır. Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTMP**. Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.

    Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.

3. Tıklatın **kanal oluşturmak**.

   ![FMLE](./media/media-services-fmle-live-encoder/media-services-fmle2.png)

> [!NOTE]
> Merhaba kanal 20 dakika toostart olarak uzun sürebilir.
>
>

Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-fmle-live-encoder.md#configure_fmle_rtmp).

> [!IMPORTANT]
> Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın. Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_fmle_rtmp></a>Merhaba FMLE Kodlayıcı yapılandırın
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
1. Flash Media Canlı Kodlayıcısı 's (FMLE) kullanılan hello makinede arabirim toohello gidin.

    Merhaba, bir ana sayfa ayarlarını arabirimidir. Lütfen hello aşağıda önerilen not edin ayarları tooget FMLE kullanarak akış ile başlatıldı.

   * Biçimi: H.264 kare hızı: 30,00
   * Giriş boyutu: 1280 x 720
   * Bit hızı: 5000 (ağ sınırlamalar göre ayarlanabilir) KB/sn  

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle3.png)

     Onay işareti hello "Taramasız Hale Getir'i" seçeneğini kullanarak kaynakları aralıklı, lütfen
2. Select hello İngiliz anahtarı simgesi sonraki tooFormat, bu ek ayarlar olmalıdır:

   * Profil: ana
   * Düzeyi: 4.0
   * Ana kare sıklığı: 2 saniye cinsinden

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle4.png)
3. Önemli ses ayarını aşağıdaki hello ayarlayın:

   * Biçim: AAC
   * Örnek Hızı: 44100 Hz
   * Bit hızı: 192 Kb/sn

     ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle5.png)
4. Merhaba kanalın giriş URL sırası tooassign almak, toohello FMLE's **RTMP Endpoint**.

    Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin. Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.

    Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle6.png)
5. Bu bilgileri hello yapıştırmak **FMS URL** hello çıkış bölümü ve ata Akış adı alanı.

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle7.png)

    Ek artıklık için hello ikincil giriş URL ile bu adımları yineleyin.
6. **Bağlan**’ı seçin.

> [!IMPORTANT]
> Tıklamadan önce **Bağlan**, size **gerekir** hello kanal hazır olduğundan emin olun.
> Ayrıca, emin olun değil tooleave hello kanal giriş katkı olmadan hazır durumda akışı > 15 dakikadan fazla.
>
>

## <a name="test-playback"></a>Testi kayıttan yürütme

Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın. Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle8.png)

Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.

Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir. Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.  

## <a name="create-a-program"></a>Bir program oluşturun
1. Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun. Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.  

    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle9.png)
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
