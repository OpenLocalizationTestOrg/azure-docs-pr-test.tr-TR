---
title: "aaaAzure RemoteApp sorun giderme - uygulama başlatma ve bağlantı hataları | Microsoft Docs"
description: "Başlangıç ve Azure remoteapp'te tooapplications bağlanma tootroubleshoot nasıl sorunlar hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Azure RemoteApp - sorun giderme uygulama başlatma ve bağlantı hataları
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure Remoteapp'te barındırılan uygulamalar toolaunch birkaç farklı nedenlerle başarısız olabilir. Çeşitli nedenlerle bu makalede açıklanır ve kullanıcıların alıp hata iletileri toolaunch uygulamaları çalışıyor. Ayrıca, bağlantı hataları hakkında alınmaktadır. (Ancak bu makalede sorunları hello Azure RemoteApp istemcisini imzalarken açıklanmaz.)  

Tooapp başlatma ve bağlantı hataları nedeniyle genel hata iletileri hakkında bilgi için okumaya devam edin.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Ki şu anda, ayarladığınız alınıyor... 10 dakika içinde yeniden deneyin.
Bu hata, Azure RemoteApp, Itanium tabanlı sistemler için toomeet hello kapasite gereksinimi kullanıcılarınızın ölçeklendirme anlamına gelir. Merhaba arka planda daha fazla Azure RemoteApp VM örnekleri kullanıcılarınızın toohandle hello kapasite gereksinimlerini oluşturuluyor. Genellikle yaklaşık beş dakika sürer ancak too10 dakika sürebilir. Bazı durumlarda, bu yeterince hızlı gerçekleşmez ve kaynakları hemen gereklidir. Örneğin çok sayıda kullanıcı gereken yeri toouse uygulamanızı Azure RemoteAppn içinde hello 09: 00 senaryo aynı zamanda. Bu tooyou olursa etkinleştirme **kapasite modu** hello üzerinde arka uç. Bu açık bir Azure destek bileti toodo. Belirli tooinclude hello isteğindeki abonelik Kimliğinizi olabilir.  

![Şu anda, ayarladığınız alınıyor](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Otomatik-tooyour yeniden bağlanılamadı uygulamalar, Lütfen uygulamanızı yeniden başlatma
Bu hata iletisini çok Azure RemoteApp kullanmakta olduğunuz ve ardından 4 saatten uzun, PC toosleep alın ve bilgisayarınıza uyandırdı hello Azure RemoteApp istemci girişimi tooauto yeniden bağlanın ve zaman aşımı oluştu görülür.  Kullanıcıların toonavigate geri toohello uygulama istemek ve tooopen denemek hello Azure RemoteApp istemci ondan.

![Otomatik-tooyour uygulamaları yeniden bağlanılamadı](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Merhaba geçici profille sorunları
Kullanıcı profilinizin (kullanıcı profili diski) toomount başarısız oldu ve geçici bir profil hello kullanıcı alınan bu hata oluşur.  Yöneticiler toohello koleksiyonunda hello Azure portalına gidin ve toohello Git **oturumları** sekmesinde ve çok Dene**Oturumu Kapat** hello kullanıcı. Merhaba kullanıcı oturumunu - tam bir oturum zorla sonra hello kullanıcı girişimi toolaunch bir uygulamayı yeniden sahip. Azure desteğine başvurun başarısız olursa.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp çalışmayı durdurdu
Bu hata iletisini hello Azure RemoteApp istemcisi bir sorunu yaşıyor ve yeniden toobe gerekiyor anlamına gelir. Kullanıcıların tooclose isteyin: seçin **Programı Kapat** ve hello Azure RemoteApp istemcisini yeniden başlatın.  Açık ve Azure destek bileti Hello sorun devam ederse.

![Azure RemoteApp çalışmayı durdurdu](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Uzak Masaüstü bağlantısı bu kaynağa erişme bir hata oluştu. Merhaba bağlanmayı yeniden deneyin veya sistem yöneticinize başvurun
Bu genel bir hata iletisi - biz araştırmak için Azure desteğine başvurun. 

![Genel Azure RemoteApp iletisi](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

