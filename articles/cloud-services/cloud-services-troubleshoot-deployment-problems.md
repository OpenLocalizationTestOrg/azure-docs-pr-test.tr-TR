---
title: "aaaTroubleshoot bulut hizmeti dağıtım sorunlarını | Microsoft Docs"
description: "Bir bulut hizmeti tooAzure dağıtırken çalışabilir bazı yaygın sorunlar vardır. Bu makale, bunların çözümleri toosome sağlar."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Bulut hizmeti dağıtım sorunlarını giderme
Bir bulut hizmeti uygulama paketi tooAzure dağıttığınızda, hello hello dağıtımı hakkında bilgi edinebilirsiniz **özellikleri** Bölmesi'nde hello Azure portalı. Merhaba ayrıntıları kullanabilirsiniz Bu bölmesinde toohelp hello bulut hizmeti sorun giderme ve yeni bir destek isteği açarken bu bilgileri tooAzure desteği sağlayabilir.

Merhaba bulabilirsiniz **özellikleri** şekilde bölmesi:

* İçinde Azure portal Merhaba, bulut hizmetinizin hello dağıtım tıklatın, **tüm ayarları**ve ardından **özellikleri**.
* Buna Klasik Azure portalı Merhaba, bulut hizmetinizin hello dağıtım tıklatın, **PANO**hello sayfasının hello sağ alt köşesinde bulunan (altında **Hızlı Bakış**). Bu bölmede yok "Özellikler" etiketli olduğunu unutmayın.

> [!NOTE]
> Merhaba Merhaba içeriğine kopyalayabilirsiniz **özellikleri** hello bölmesini hello sağ üst köşesindeki hello simgesini tıklatarak bölmesinde toohello Pano.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Sorun: my Web sitesi dosyasına erişemiyor, ancak my dağıtım başlatılır ve tüm rol örneklerini hazır
Merhaba Portalı'nda gösterilen hello Web sitesi URL'si bağlantısı hello bağlantı noktası içermez. Web siteleri için Hello varsayılan bağlantı noktası 80'dir. Uygulamanız farklı bir bağlantı noktasında yapılandırılmış toorun ise hello doğru bağlantı noktası numarası toohello URL'si hello Web sitesi erişirken eklemeniz gerekir.

1. Hello Azure portal'de, bulut hizmetinizin hello dağıtım'ı tıklatın.
2. Merhaba, **özellikleri** hello Azure portal bölmesinde hello rol örnekleri için hello bağlantı noktalarını denetleyin (altında **giriş uç noktaları**).
3. Başlangıç bağlantı noktası 80 değilse hello uygulama eriştiğinde hello doğru bağlantı noktası değeri toohello URL'sini ekleyin. toospecify varsayılan olmayan bağlantı noktası hello URL'sini yazın, boşluk hello bağlantı noktası numarası ve ardından iki nokta (:), arkasından.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Sorun: hiçbir şey bana geri dönüşüm My rol örnekleri
Azure sorun düğümleri algılar ve bu nedenle rol örnekleri toonew düğümleri taşır iyileştirme hizmeti otomatik olarak oluşur. Bu durumda, rolü örneklerinizi otomatik olarak geri dönüştürme görebilirsiniz. IF toofind hizmeti oluştu düzeltme:

1. Hello Azure portal'de, bulut hizmetinizin hello dağıtım'ı tıklatın.
2. Merhaba, **özellikleri** hello Azure portal bölmesinde hello bilgileri gözden geçirin ve hizmet onarma geri dönüştürme hello rolleri gözlenen hello zamanı sırasında oluşup oluşmadığını belirleyin.

Rolleri aynı zamanda kabaca ayda bir kez ana bilgisayar işletim sistemi ve konuk işletim sistemi güncelleştirmeleri sırasında geri.  
Daha fazla bilgi için bkz: hello blog gönderisi [rol örneği yeniden son tooOS yükseltmeleri](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Sorun: t olamaz bir VIP takası yapın ve bir hata alıyorsunuz
Dağıtım güncelleştirme işlemi devam ediyorsa bir VIP takası izin verilmiyor. Dağıtım güncelleştirmeleri otomatik olarak oluşabilir zaman:

* Yeni bir konuk işletim sistemi kullanılabilir ve otomatik güncelleştirmeler için yapılandırılır.
* Hizmet iyileştirme oluşur.

Otomatik güncelleştirirseniz toofind çıkışı bir VIP takası engel engelliyor:

1. Hello Azure portal'de, bulut hizmetinizin hello dağıtım'ı tıklatın.
2. Merhaba, **özellikleri** hello Azure portal bölmesinde arayın hello değerinde **durum**. Eğer öyleyse **hazır**, ardından denetleyin **son işlem** biri son, oluştuysa, toosee hello VIP takas engelleyebilir.
3. Adım 1 ve 2 hello Üretim dağıtımı için yineleyin.
4. Bir otomatik güncelleştirme işlemi varsa, bekleyin toofinish çalışırken toodo hello VIP takas önce.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Sorun: Rol örneği başlatıldı, başlatılıyor, meşgul ve durdurulmuş arasında döngü
Bu durum, uygulama kodunuz, paketiniz veya yapılandırma dosyanızla ilgili bir sorundan kaynaklanıyor olabilir. Bu durumda, birkaç dakikada değiştirmek mümkün toosee hello durum olmalıdır ve hello Azure portal şöyle gözükebilir **geri dönüştürme**, **meşgul**, veya **başlatılıyor**. Bu olduğunu hello rol örneği çalışmasını engelliyor hello uygulamayla yanlış bir şeyler gösterir.

Hakkında daha fazla bilgi için bu sorun için tootroubleshoot hello blog yayınına bakın [Azure PaaS işlem tanılama verilerini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) ve [ortak sorunları bu neden rolleri toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Sorun: Uygulamam durdu
1. Hello Azure portal, hello rol örneği'ı tıklatın.
2. Merhaba, **özellikleri** hello Azure portal bölmesinde göz önünde bulundurun koşullar tooresolve aşağıdaki hello sorununuzu:
   * Merhaba rol örneği yakın zamanda durdurulmuşsa (Merhaba değerini kontrol edebilirsiniz **Abort sayısı**), hello dağıtım güncelleştiriyor. Merhaba rol örneği, kendi çalışmasını sürdürülürse toosee bekleyin.
   * Merhaba rol örneği ise **meşgul**, uygulama kodu toosee hello olup olmadığını denetleyin [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) olayı işlenir. Tooadd ihtiyacınız veya bu olayını işler biraz kod düzeltin.
   * Merhaba tanılama verilerine gidin ve sorun giderme senaryoları hello blog yayını içinde [Azure PaaS işlem tanılama verilerini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Bulut hizmetinizi Geri Dönüşüm, hello özellikleri hello dağıtımı için etkili bir şekilde hello bilgi hello özgün sorun için silme sıfırlayın.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi görüntülemek [sorun giderme makalelerini](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) bulut Hizmetleri için.

tootroubleshoot bulut hizmet rolü nasıl sorunları Azure PaaS bilgisayar tanılama verilerini kullanarak toolearn bkz [Kevin Williamson'ın blog dizisini](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
