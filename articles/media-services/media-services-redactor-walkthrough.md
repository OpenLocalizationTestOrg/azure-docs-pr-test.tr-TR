---
title: "Azure medya analizi kılavuza aaaRedact yüzeyleri | Microsoft Docs"
description: "Bu konu hakkında adım adım yönergeler gösterir toorun Azure Media Services Gezgini (AMSE) ve Azure Media Redactor Görselleştirici (açık kaynak aracı) kullanarak bir tam Redaksiyon iş akışı."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a>Azure medya analizi kılavuza yüzeyleri Redaksiyon

## <a name="overview"></a>Genel Bakış

**Azure Media Redactor** olan bir [Azure medya analizi](media-services-analytics-overview.md) medya işlemcisi (MP) ölçeklenebilir yüz Redaksiyon hello bulutta sunar. Yüz Redaksiyon sipariş tooblur yüzeyleri seçilen kişilerin, video, toomodify sağlar. Toouse hello yüz Redaksiyon hizmeti ortak güvenliği ve haber medya senaryolarda isteyebilirsiniz. Saat tooredact el ile birden çok yüzeyleri içeren çekimi birkaç dakika sürebilir, ancak bu hizmet hello yüz ile birkaç basit adımla Redaksiyon işlem gerektirir. Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/blog/azure-media-redactor/) blogu.

Hakkındaki ayrıntılar için **Azure medya Redactor**, hello bkz [yüz Redaksiyon genel bakış](media-services-face-redaction.md) konu.

Bu konu hakkında adım adım yönergeler gösterir toorun Azure Media Services Gezgini (AMSE) ve Azure Media Redactor Görselleştirici (açık kaynak aracı) kullanarak bir tam Redaksiyon iş akışı.

Merhaba **Azure medya Redactor** MP şu anda önizlemede. Tüm ortak Azure bölgeleri yanı sıra ABD devlet kurumları ve Çin veri merkezleri kullanılabilir. Bu önizleme şu anda ücretsizdir. Merhaba geçerli sürümde, işlenen video uzunluk 10 dakikalık sınırı yoktur.

Daha fazla bilgi için bkz: [bu](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blogu.

## <a name="azure-media-services-explorer-workflow"></a>Azure Media Services Gezgini iş akışı

Merhaba en kolay yolu tooget kullanmaya Redactor araçtır toouse hello açık kaynak AMSE github'da. Basitleştirilmiş bir iş akışı aracılığıyla çalıştırabilirsiniz **birleştirilmiş** modu toohello ek açıklama json ya da hello yüz jpg görüntüleri erişim yoktur.

### <a name="download-and-setup"></a>Karşıdan yükleme ve Kurulum

1. Merhaba AMSE aracını indirin [burada](https://github.com/Azure/Azure-Media-Services-Explorer).
1. Tooyour hizmeti anahtarınızı kullanarak Media Services hesabı oturum açın.

    hesap adı ve anahtar bilgilerini, Git toohello tooobtain hello [Azure portal](https://portal.azure.com/) ve AMS hesabınızı seçin. Ardından, ayarları seçin > anahtarları. Merhaba Yönet anahtarları windows hello hesap adını gösterir ve hello birincil ve ikincil anahtarlar görüntülenir. Merhaba hesap adı ve hello birincil anahtar değerlerini kopyalayın.

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a>İlk geçirmek – modu Çözümle

1. Karşıya yükleme, ortam dosyası aracılığıyla varlığını –> karşıya yükleme, ya da sürükle ve bırak aracılığıyla. 
1. Sağ tıklayın ve medya dosyanızı medya analizi kullanarak işlem Azure medya Redactor –> Çözümle modu –>. 


![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

Merhaba çıkış jpg algılanan her yazıtipinin yanı sıra, yüz konum verilerini içeren bir ek açıklamaları json dosyası içerir. 

![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a>İkinci geçirmek – modu Redaksiyon

1. Merhaba ilk pass çıkış ve birincil bir varlık ayarlamak, özgün bir varlığı toohello karşıya yükleyin. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. (İsteğe bağlı) Merhaba tooredact istediğiniz kimlikleri yeni satır ayrılmış listesini içeren bir 'Dance_idlist.txt' dosyasını karşıya yükleyin. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. (İsteğe bağlı) Sınırlama kutusu sınırlarını hello artırma gibi tüm düzenlemeleri toohello annotations.json dosya olun. 
4. Merhaba ilk geçişi hello çıkış varlığından sağ tıklayın, hello Redactor seçin ve hello ile Çalıştır **Redact** modu. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. İndirme veya hello son Redaksiyonu yapılmış çıkış varlığına paylaşabilirsiniz. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a>Azure Media Redactor Görselleştirici açık kaynak aracı

Bir açık kaynak [Görselleştirici aracı](https://github.com/Microsoft/azure-media-redactor-visualizer) tasarlanmış toohelp geliştiriciler ayrıştırma ve hello çıkış kullanan hello ek açıklama biçimi yalnızca başlayarak olduğunu.

Sipariş toorun hello projesinde hello depoyu kopyalama sonra toodownload FFMPEG gerekir gelen kendi [resmi sitesi](https://ffmpeg.org/download.html).

Tooparse hello JSON ek açıklama verilerini çalışırken bir geliştirici iseniz içinde Models.MetaData için örnek kod örnekleri arayın.

### <a name="set-up-hello-tool"></a>Merhaba aracı ayarlamak

1.  Karşıdan yükle ve hello tüm çözümü oluşturun. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  Gelen FFMPEG karşıdan [burada](https://ffmpeg.org/download.html). Bu projede statik bağlama ile sürüm be1d324 (2016-10-04) ile ilk olarak geliştirilmiştir. 
3.  Ffmpeg.exe ve ffprobe.exe toohello kopyalamak aynı çıkış klasörü AzureMediaRedactor.exe olarak. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. AzureMediaRedactor.exe çalıştırın. 

### <a name="use-hello-tool"></a>Merhaba aracını kullanın

1. Azure Media Services hesabınızla hello Redactor MP Çözümle modunu, videoda işleyin. 
2. Merhaba özgün video dosyası ve hello Redaksiyon hello çıktısını yükle - iş analiz edin. 
3. Merhaba Görselleştirici uygulamayı çalıştırın ve yukarıdaki hello dosyalar'ı seçin. 

    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. Dosyanızı önizlemede. Hangi, yüzler seçin hello Kenar çubuğunda hello aracılığıyla tooblur sağ ister. 
    
    ![Yüz flulaştırma](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  Merhaba alt metin alanı hello yüz kimlikleri ile güncelleştirir. "İdlist.txt" adlı bir dosya Bu kimliklerle yeni satır ayrılmış liste olarak oluşturun. 

    >[!NOTE]
    > Merhaba idlist.txt ANSI kaydedilmesi gerekir. Not Defteri'ni toosave ANSI kullanabilirsiniz.
    
6.  Bu dosya toohello çıkış varlık 1. adımdaki karşıya yükleyin. Merhaba özgün video toothis varlık da karşıya yükleyin ve birincil varlık ayarlayın. 
7.  Bu varlık "Redact" modu tooget hello son Redaksiyonu yapılmış video Redaksiyon işi çalıştırın. 

## <a name="next-steps"></a>Sonraki adımlar 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure medya analizi gösterileri](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[Azure medya analizi için yüz Redaksiyon Duyurusu](https://azure.microsoft.com/blog/azure-media-redactor/)
