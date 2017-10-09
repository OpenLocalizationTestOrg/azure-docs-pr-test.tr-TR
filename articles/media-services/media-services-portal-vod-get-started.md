---
title: "aaaGet başlatılan hello Azure portal kullanarak VoD göndermeye | Microsoft Docs"
description: "Bu öğreticide, hello Azure portal kullanarak Azure Media Services (AMS) uygulaması ile temel bir isteğe bağlı video (VoD) içerik teslim hizmeti uygulamanın hello adımları açıklanmaktadır."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 6c98fcfa-39e6-43a5-83a5-d4954788f8a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 5c1c1b1f74ec1f1301120fe8e5a5ae183fe0338f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-delivering-content-on-demand-using-hello-azure-portal"></a>Hello Azure portal kullanarak isteğe bağlı içerik göndermeye başlama
[!INCLUDE [media-services-selector-get-started](../../includes/media-services-selector-get-started.md)]

Bu öğreticide, hello Azure portal kullanarak Azure Media Services (AMS) uygulaması ile temel bir isteğe bağlı video (VoD) içerik teslim hizmeti uygulamanın hello adımları açıklanmaktadır.

## <a name="prerequisites"></a>Ön koşullar
Merhaba, gerekli toocomplete hello öğretici şunlardır:

* Bir Azure hesabı. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/). 
* Bir Media Services hesabı. bir Media Services hesabı toocreate bkz [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).

Bu öğretici hello aşağıdaki görevleri içerir:

1. Akış uç noktasını başlatın.
2. Bir video dosyası yükleyin.
3. Merhaba kaynak dosya bit hızı Uyarlamalı MP4 dosyaları kümesine kodlayın.
4. Merhaba varlık ve get akış ve aşamalı indirme URL'leri yayımlayın.  
5. İçeriğinizi oynatın.

## <a name="start-streaming-endpoints"></a>Akış uç noktalarını başlatma 

Merhaba en sık karşılaşılan senaryolardan biri, video bit hızı Uyarlamalı akış iletmektir Azure Media Services ile çalışırken. Media Services, bit hızı Uyarlamalı MP4 kodlanmış içeriğinizi Media Services (MPEG DASH, HLS, kesintisiz akış) tam zamanında tarafından önceden paketlenmiş toostore kalmadan desteklenen akış biçimlerinde toodeliver sağlayan dinamik paketleme sağlar Bu akış biçimlerine her da sürümleri.

>[!NOTE]
>AMS hesabınızı oluşturulduğunda bir **varsayılan** akış uç noktası ekleniyor tooyour hesabı hello **durduruldu** durumu. İçerik ve Al avantajı dinamik paketleme ve dinamik şifreleme akış toostart hello istediğiniz toostream içeriğe sahip toobe hello akış uç **çalıştıran** durumu. 

toostart akış uç Merhaba, aşağıdaki hello:

1. Merhaba oturum açma [Azure portal](https://portal.azure.com/).
2. Hello Ayarları penceresinde, akış uç noktaları'ı tıklatın. 
3. Merhaba varsayılan akış uç noktası'ı tıklatın. 

    Merhaba varsayılan akış uç noktası AYRINTILAR penceresi görüntülenir.

4. Merhaba başlangıç simgesine tıklayın.
5. Merhaba Kaydet düğmesine toosave değişikliklerinizi'ı tıklatın.

## <a name="upload-files"></a>Dosyaları karşıya yükleme
Azure Media Services kullanarak videoların, tooupload hello kaynak videoları, gereksinim duyduğunuz toostream Çoklu bit hızına kodlamanız ve yayımlama hello sonucu. Merhaba ilk adım, bu bölümde ele alınmıştır. 

1. Merhaba, **ayarı** penceresinde tıklatın **varlıklar**.
   
    ![Dosyaları karşıya yükleme](./media/media-services-portal-vod-get-started/media-services-upload.png)
2. Merhaba tıklatın **karşıya** düğmesi.
   
    Merhaba **bir varlığı karşıya yükle** penceresi görüntülenir.
   
   > [!NOTE]
   > Dosya boyutu sınırlaması yoktur.
   > 
   > 
3. Bilgisayarınızda istenen toohello video göz atın, onu seçin ve Tamam'ı tıklatın.  
   
    Merhaba karşıya yükleme başlar ve hello dosya adı altında hello ilerleme durumunu görebilirsiniz.  

Merhaba karşıya yükleme işlemi tamamlandıktan sonra hello yeni varlık hello listelenen bkz **varlıklar** penceresi. 

## <a name="encode-assets"></a>Varlıkları kodlama

Merhaba en sık karşılaşılan senaryolardan biri, bit hızı Uyarlamalı akış tooyour istemcileri iletmektir Azure Media Services ile çalışırken. Media Services şu bit hızı Uyarlamalı akış teknolojilerini hello destekler: HTTP canlı akışı (HLS), kesintisiz akış, MPEG DASH. tooprepare videolarınızı bit hızı Uyarlamalı akış için tooencode kaynağınız video Çoklu bit hızlı dosyalarıyla gerekir. Merhaba kullanması gereken **Medya Kodlayıcısı standart** Kodlayıcı tooencode videolarınızı.  

Media Services, Çoklu bit hızlı MP4s akış biçimlerine aşağıdaki hello içinde de toodeliver sağlayan dinamik paketleme sağlar: MPEG DASH, HLS, kesintisiz akış, bu akış biçimlerine toorepackage kalmadan olmadan. Dinamik paketleme ile toostore yeterlidir ve ödeme tek bir depolama biçiminde ve Media Services hello dosyaları oluşturur ve istemciden gelen isteklere göre uygun yanıtı hello işlevi görür.

tootake avantajı dinamik paketleme, tooencode kaynak dosyanızı Çoklu bit hızlı MP4 dosyaları (kodlama adımları hello gösterilmektedir daha sonra bu bölümde) kümesine ihtiyacınız.

### <a name="toouse-hello-portal-tooencode"></a>toouse hello portal tooencode
Bu bölüm, içeriğinizi Medya Kodlayıcısı standart ile tooencode uygulayabileceğiniz hello adımları açıklar.

1. Merhaba, **ayarları** penceresinde, seçin **varlıklar**.  
2. Merhaba, **varlıklar** penceresinde, select hello varlık tooencode istersiniz.
3. Tuşuna hello **kodla** düğmesi.
4. Merhaba, **bir varlık kodla** penceresi, select hello "Medya Kodlayıcısı standart" işlemcisini ve bir hazır. Hazır ayarlar hakkında daha fazla bilgi için bkz. [Bit hızı merdivenini otomatik oluşturma](media-services-autogen-bitrate-ladder-with-mes.md) ve [MES Görev Ön Ayarları](media-services-mes-presets-overview.md). Hangi kodlama hazır kullanılır toocontrol planlıyorsanız, bunu göz önünde bulundurun: tooselect hello giriş videonuzun için en uygun olan Önayar önemlidir. Giriş videonuzun 1920 x 1080 piksel çözünürlüğü sahip biliyorsanız, örneğin, hello kullanabilirsiniz "H264 Çoklu bit hızı 1080p" hazır. Düşük çözünürlüklü (640 x 360) bir videonuz olması durumunda "H264 Çoklu Bit hızı 1080p" ön ayarını kullanmamalısınız.
   
   Daha kolay yönetim için hello hello çıkış varlık adını düzenleme ve hello işinin hello adı bir seçeneğiniz vardır.
   
   ![Varlıkları kodlama](./media/media-services-portal-vod-get-started/media-services-encode1.png)
5. **Oluştur**’a basın.

### <a name="monitor-encoding-job-progress"></a>Kodlama işi ilerleme durumunu izleme
İş, kodlama hello toomonitor hello ilerlemesini tıklatın **ayarları** (Merhaba sayfanın en üstündeki hello) ve ardından **işleri**.

![İşler](./media/media-services-portal-vod-get-started/media-services-jobs.png)

## <a name="publish-content"></a>İçerik yayımlama
tooprovide kullanılan toostream ya da içeriğinizi indirme URL'si, kullanıcı, önce çok "varlığınız bir Bulucu oluşturarak yayımlamanız". Bulucular hello varlıkta bulunan erişim toofiles sağlar. Media Services iki tür bulucuyu destekler: 

* Akış (OnDemandOrigin) bulucuları, (örneğin, toostream MPEG DASH, HLS veya kesintisiz akış) Uyarlamalı akış için kullanılır. toocreate akış Bulucusu varlığınız bir .ism dosyası içermelidir. 
* Aşamalı indirme aracılığıyla video teslimi için kullanılan aşamalı (SAS) bulucular.

Bir akış URL'si biçimi aşağıdaki hello sahiptir ve tooplay kesintisiz akış varlıklarını kullanın.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest

HLS akış URL'si, bir toobuild ekleme (format = m3u8-aapl) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

bir akış URL'si, MPEG DASH toobuild ekleme (biçim mpd zaman csf =) toohello URL.

    {streaming endpoint name-media services account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)


Bir SAS URL'si biçimi aşağıdaki hello sahiptir.

    {blob container name}/{asset name}/{file name}/{SAS signature}

> [!NOTE]
> Mart 2015 öncesinde hello portal toocreate bulucular kullandıysanız, iki yıllık sona erme tarihi olan bulucular oluşturulmuştur.  
> 
> 

Kullanım Bulucunun sona erme tarihi bir tooupdate [REST](https://docs.microsoft.com/rest/api/media/operations/locator#update_a_locator) veya [.NET](http://go.microsoft.com/fwlink/?LinkID=533259) API'leri. Bir SAS Bulucu hello sona erme tarihini güncelleştirdiğinizde hello URL değiştirir.

### <a name="toouse-hello-portal-toopublish-an-asset"></a>toouse hello portal toopublish bir varlığı
toouse hello portal toopublish bir varlık hello aşağıdaki:

1. **Ayarlar** > **Varlıklar**’ı seçin.
2. Merhaba varlık toopublish istediğinizi seçin.
3. Merhaba tıklatın **Yayımla** düğmesi.
4. Merhaba Bulucu türünü seçin.
5. **Ekle**’ye basın.
   
    ![Yayımlama](./media/media-services-portal-vod-get-started/media-services-publish1.png)

Merhaba URL toohello listesi eklenen **yayımlanan URL'ler**.

## <a name="play-content-from-hello-portal"></a>Merhaba portaldan içerik oynatma
Hello Azure portalı bir içerik oynatıcı sağlar videonuzu tootest kullanabilirsiniz.

İstenen hello videoya tıklayın ve hello ardından **Yürüt** düğmesi.

![Yayımlama](./media/media-services-portal-vod-get-started/media-services-play.png)

Bazı dikkate alınması gereken noktalar vardır:

* Akış, toobegin Başlat çalışan hello **varsayılan** akış uç noktası.
* Merhaba video yayımlandığından emin olun.
* Bu **Media player** hello varsayılan akış uç noktasından oynatır. Varsayılan olmayan tooplay istiyorsanız akış uç noktası, toocopy hello URL'yi tıklatın ve başka bir oynatıcı kullanın. Örneğin, [Azure Media Services Oynatıcı](http://amsplayer.azurewebsites.net/azuremediaplayer.html).

## <a name="next-steps"></a>Sonraki adımlar
Media Services öğrenme yollarını gözden geçirin.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

