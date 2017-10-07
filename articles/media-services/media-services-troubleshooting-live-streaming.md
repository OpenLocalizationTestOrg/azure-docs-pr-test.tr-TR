---
title: "Canlı akış için aaaTroubleshooting Kılavuzu | Microsoft Docs"
description: "Bu konuda nasıl tootroubleshoot canlı akış sorunları hakkında öneriler sağlar."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Canlı akış sorun giderme kılavuzu
Bu konu hakkında öneriler sunar tootroubleshoot bazı canlı akış sorunları.

## <a name="issues-related-tooon-premises-encoders"></a>Tooon içi kodlayıcılar ilgili sorunlar
Bu bölüm, gerçek zamanlı kodlama için etkinleştirilmiş bir tek bit hızlı akış tooAMS kanallar olan tootroubleshoot sorunları ilgili tooon içi kodlayıcılar toosend nasıl yapılandırılacağı hakkında öneriler sağlar.

### <a name="problem-would-like-toosee-logs"></a>Sorun: toosee günlükleri istiyorsunuz
* **Olası sorun**: Kodlayıcı günlüklerini bulma sorunları hata ayıklamaya yardımcı olabilecek olamaz.
  
  * **Telestream Wirecast**: logs C:\Users altında genellikle bulabilirsiniz\{username} \AppData\Roaming\Wirecast\ 
  * **Elemental canlı**: sahip bağlantılar toologs hello yönetim portalında bulabilirsiniz. Tıklayın **istatistiği**, ardından **günlükleri**. Merhaba üzerinde **günlük dosyalarını** sayfası, tüm günlükleri listesi LiveEvent öğeleri hello; seçin, mevcut oturumunuzun eşleşen hello görürsünüz. 
  * **Canlı medya Kodlayıcı flash**: hello bulabilirsiniz **günlük dizini...**  toohello gezinme tarafından **kodlama günlük** sekmesi.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Sorun: Aşamalı bir akış çıktısı için bir seçenek yoktur
* **Olası sorun**: kullanılan hello Kodlayıcı değil otomatik olarak Titreşimi Kaldırma. 
  
    **Sorun giderme adımları**: hello Kodlayıcı arabiriminden Titreşim seçeneği arayın. XML'deki tarama etkinleştirildikten sonra yeniden aşamalı çıkış ayarlarını denetleyin. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Sorun: birkaç encoder çıkış ayarları ve hala tooconnect çalıştı.
* **Olası sorun**: Azure kodlama kanal değil düzgün sıfırlandı. 
  
    **Sorun giderme adımları**: tooAMS yapma emin hello Kodlayıcı Ftp'den artık, durdurmak ve hello kanalını sıfırlayın. Yeniden çalıştırmayı sonra kodlayıcıyı hello yeni ayarlarla bağlanmayı deneyin. Merhaba sorunu bu hala gidermezse, tamamen yeni bir kanal oluşturma deneyin, başarısız birkaç denemeden sonra bazen kanalları bozulabilir.  
* **Olası sorun**: Merhaba GOP boyutu veya anahtar çerçeve ayarları en uygun değildir. 
  
    **Sorun giderme adımları**: önerilen GOP boyutu veya ana kare aralığıdır 2 saniye. Başkalarının saniye kullanırken bazı kodlayıcılar çerçeve sayısı bu ayarda hesaplayın. Örneğin: 30 fps alırken hello GOP boyutu 60 çerçeve eşdeğer too2 saniye olduğu olacaktır.  
* **Olası sorun**: kapalı bağlantı noktalarını hello akış engelleme. 
  
    **Sorun giderme adımları**: RTMP akış, güvenlik duvarı ve/veya proxy ayarlarını tooconfirm 1935 ve 1936 giden bağlantı noktalarının açık olduğunu denetleyin. RTP akış kullanırken, giden bağlantı noktası 2010 açık olduğundan emin olun. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Sorun: RTP Protokolü hello ile Merhaba Kodlayıcı toostream yapılandırma olduğunda yer yok tooenter bir ana bilgisayar adı.
* **Olası sorun**: birçok RTP kodlayıcılar ana bilgisayar adları için izin vermez ve bir IP adresi toobe alınan ihtiyacınız olacaktır.  
  
    **Sorun giderme adımları**: toofind Merhaba IP adresinin, herhangi bir bilgisayarda bir komut istemi açın. Windows, toodo açık çalışma Başlatıcısı (WIN + R) hello ve "cmd" tooopen yazın.  
  
    Merhaba komut istemi açıldıktan sonra "Ping [AMS ana bilgisayar adı]" yazın. 
  
    Merhaba ana bilgisayar adı aşağıdaki örneğine hello vurgulu olarak hello Azure alım URL'sini, başlangıç bağlantı noktası numarasından kaldırarak türetilmiş olmalıdır: 
  
    RTP://Test2-amstest009.RTP.Channel.mediaservices.Windows.NET:2010 / 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Aşağıdaki ise, hala başarıyla akış uygulayamazsınız hello sorun giderme adımları sonra hello Azure portal kullanarak bir destek bileti gönderin.
> 
> 

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

