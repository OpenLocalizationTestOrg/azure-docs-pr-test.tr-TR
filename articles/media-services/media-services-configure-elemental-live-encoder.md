---
title: "tek bit hızlı bir canlı akışı aaaConfigure hello Elemental Canlı Kodlayıcı toosend | Microsoft Docs"
description: "Bu konu, nasıl tooconfigure hello Elemental Canlı Kodlayıcı toosend gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar gösterir."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Tek bit hızlı bir canlı akışı Hello Elemental Canlı Kodlayıcı toosend kullanın
> [!div class="op_single_selector"]
> * [Elemental dinamik](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

Bu konuda gösterilmektedir nasıl tooconfigure hello [Elemental canlı](http://www.elementaltechnologies.com/products/elemental-live) Kodlayıcı toosend tek bit hızlı akış gerçek zamanlı kodlama için etkinleştirilmiş tooAMS kanallar.  Daha fazla bilgi için bkz: [etkin tooPerform Canlı Azure Media Services ile kodlama olan kanallar ile çalışma](media-services-manage-live-encoder-enabled-channels.md).

Bu öğretici nasıl toomanage Azure Media Services gösterir (AMS) Azure Media Services Gezgini (AMSE) aracı ile. Bu araç, yalnızca bir Windows Bilgisayarına çalışır. Mac veya Linux üzerinde hello Azure portal toocreate kullanırsanız [kanalları](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) ve [programlar](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Ön koşullar
* Web arabirimi toocreate Canlı olayları Elemental Canlı kullanma bilgisine sahip olmalıdır.
* [Bir Azure Media Services hesabı oluşturma](media-services-portal-create-account.md)
* Çalıştıran bir akış uç olduğundan emin olun. Daha fazla bilgi için bkz: [akış uç noktalarını yönetme Media Services hesabı](media-services-portal-manage-streaming-endpoints.md).
* Merhaba Hello en son sürümünü yüklemek [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) aracı.
* Merhaba aracını başlatmak ve tooyour AMS hesabının bağlanın.

## <a name="tips"></a>İpuçları
* Mümkün olduğunda, bir sabit Internet bağlantısı kullanır.
* Bir iyi bant genişliği gereksinimlerini belirlerken bit akış toodouble hello udur. Bu zorunlu bir gereksinim olmamasına karşın, Ağ Tıkanıklığı hello etkisini azaltmaya yardımcı olur.
* Kodlayıcılar tabanlı yazılım kullanarak, gereksiz tüm programları kapatın.

## <a name="elemental-live-with-rtp-ingest"></a>RTP ile elemental Canlı alma
Bu bölümde, nasıl tek bit hızlı gönderdiği tooconfigure hello Elemental Canlı gerçek zamanlı kodlayıcıya akış RTP gösterir.  Daha fazla bilgi için bkz: [RTP üzerinden MPEG-TS akış](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Kanal oluşturma

1. Toohello Hello AMSE aracında gezinmek **canlı** sekmesinde ve hello kanal alanı içinde sağ tıklatın. Seçin **kanal oluştur...** Başlangıç menüsünden.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Bir kanal adı belirtin hello açıklama alanı isteğe bağlıdır. Kanal ayarları altında seçin **standart** giriş protokolü ile Merhaba hello gerçek zamanlı kodlama seçeneği için çok ayarlamak**RTP (MPEG-TS)**. Olduğu gibi tüm diğer ayarlar bırakabilirsiniz.

    Merhaba emin olun **başlangıç hello yeni kanal şimdi** seçilir.

3. Tıklatın **kanal oluşturmak**.

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> Merhaba kanal 20 dakika toostart olarak uzun sürebilir.
>
>

Merhaba kanal başlatılırken yapabilecekleriniz [hello Kodlayıcı yapılandırma](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Kanal hazır bir durumuna geçtiğinde hemen faturalama başladığını unutmayın. Daha fazla bilgi için bkz: [kanalın durumları](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Merhaba Elemental Canlı Kodlayıcı yapılandırın
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

#### <a name="configuration-steps"></a>Yapılandırma adımları
1. Toohello gidin **Elemental canlı** web arabirimi ve hello Kodlayıcı için ayarlama **UDP/TS** akış.
2. Yeni bir olay oluşturulduğunda toohello çıktı grupları kaydırın ve hello ekleyin **UDP/TS** çıktı grubu.
3. Seçerek yeni bir çıktı oluşturmak **yeni akış** ve ardından **Çıktı Ekle**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > Merhaba Elemental olay sahip çok ayarlamak hello zaman kodu önerilir "Sistem saati" toohelp hello Kodlayıcı yeniden akışı hatası hello durumda.
   >
   >
4. Merhaba çıkış oluşturuldu, tıklatın **akış eklemek**. Merhaba çıkış ayarları artık yapılandırılabilir.
5. Kaydırma, yeni oluşturduğunuz toohello "Akış 1", hello tıklatın **Video** sekmesinde hello solda ve hello genişletin **Gelişmiş** Ayarlar bölümünde.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Elemental Canlı kullanılabilir özelleştirme çeşitli sahipken hello aşağıdaki ayarlar tooAMS akış ile çalışmaya başlama için önerilir.

   * Çözünürlük: 1280 x 720
   * Kare hızı: 30
   * GOP boyutu: 60 çerçeveler
   * Mod Taramasız hale getirme: aşamalı
   * Bit hızı: 5000000 bit/sn (Bu ağ sınırlamaları göre ayarlanabilir)

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Merhaba kanalın giriş URL'sini alma.

    Geri toohello AMSE aracını gidin ve hello kanal tamamlanma durumunu denetleyin. Merhaba durumu değiştiğinden sonra **başlangıç** çok**çalıştıran**, hello giriş URL elde edebilirsiniz.

    Merhaba kanal çalıştırırken hello kanal adını sağ tıklatın, üzerinden toohover gidin **kopyalama giriş URL tooclipboard** ve ardından **birincil giriş URL**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Bu bilgileri hello yapıştırmak **birincil hedef** hello Elemental alanı. Tüm diğer ayarlar hello varsayılan kalabilir.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Ek artıklık için UDP/TS akış için ayrı bir "Çıktı" sekmesinde oluşturarak hello ikincil giriş URL ile bu adımları yineleyin.
3. Tıklatın **oluşturma** (yeni bir olay oluşturduysanız) veya **güncelleştirme** (önceden var olan bir olay düzenleme varsa) ve toostart hello Kodlayıcı devam edin.

> [!IMPORTANT]
> Tıklamadan önce **Başlat** hello Elemental canlı web arabiriminde, **gerekir** hello kanal hazır olduğundan emin olun.
> Ayrıca, emin olun tooleave hello kanal > 15 dakikadan daha uzun bir olay olmadan hazır durumda değil.
>
>

Merhaba akış 30 saniye yürütüldükten sonra geri toohello AMSE aracını ve test kayıttan yürütme gidin.  

### <a name="test-playback"></a>Testi kayıttan yürütme

Toohello AMSE aracını gidin ve test hello kanal toobe sağ tıklayın. Başlangıç menüsünden üzerine gelerek **kayıttan yürütme hello Önizleme** seçip **Azure Media Player ile**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Merhaba akış hello player görünürse, hello Kodlayıcı düzgün yapılandırılmış tooconnect tooAMS olmuştur.

Bir hata alırsanız, hello kanal ayarlanmış toobe sıfırlama ve Kodlayıcı ayarları gerekir. Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.   

### <a name="create-a-program"></a>Bir program oluşturun
1. Kanal kayıttan yürütme onaylandıktan sonra bir program oluşturun. Merhaba altında **canlı** sekmesinde hello AMSE aracının hello programı alanı içinde sağ tıklatın ve seçin **Yeni Program Oluştur**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Ad hello program ve gerekli olursa, hello ayarlamak **arşiv penceresi uzunluğu** (hangi Varsayılanları too4 saat). Ayrıca, bir depolama konumu belirtin veya hello varsayılan olarak bırakın.  
3. Merhaba denetleyin **Şimdi Başlat hello Program** kutusu.
4. Tıklatın **Program oluşturma**.  

    >[!NOTE]
    > Program oluşturma kanal oluşturma daha az zaman alır.   
      
5. Merhaba program çalışmaya başladıktan sonra kayıttan yürütme hello program sağ tıklatıp çok gezinme onaylayın**kayıttan yürütme hello edinin** seçilerek **Azure Media Player ile**.  
6. Onaylandıktan sonra sağ hello program yeniden tıklatın ve seçin **kopyalama hello çıkış URL tooClipboard** (veya bu bilgileri hello almak **Program bilgilerine ve ayarlarına** hello menü seçeneğinden).

Merhaba şimdi bir oynatıcı katıştırılmış hazır toobe akışıdır veya dağıtılmış tooan kitlesi Canlı görüntüleme.  

## <a name="troubleshooting"></a>Sorun giderme
Lütfen hello bakın [sorun giderme](media-services-troubleshooting-live-streaming.md) Kılavuzu konu.

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
