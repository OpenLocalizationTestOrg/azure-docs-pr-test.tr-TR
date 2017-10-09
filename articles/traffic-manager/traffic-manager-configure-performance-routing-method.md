---
title: "aaaConfigure performans trafik yönlendirme yöntemini Azure trafik Yöneticisi'ni kullanarak | Microsoft Docs"
description: "Bu makalede, nasıl tooconfigure trafik Yöneticisi tooroute trafiği toohello bitiş noktası ile düşük gecikme açıklanmaktadır."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Merhaba performans trafik yönlendirme yöntemini yapılandırma

Merhaba performans trafik yönlendirme yöntemini hello hello istemcinin ağdan en düşük gecikme süresi ile toodirect trafiği toohello uç noktası sağlar. Genellikle coğrafi uzaklığı en yakın hello hello datacenter hello en düşük gecikme süresine sahip olur. Bu trafik yönlendirme yöntemini ağ yapılandırmasında gerçek zamanlı değişiklikleri hesaba veya yük.

##  <a name="tooconfigure-performance-routing-method"></a>tooconfigure performans yönlendirme yöntemi

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com). Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz. 
2. Merhaba Hello portal'ın arama çubuğunda arama **Traffic Manager profillerini** ve tooconfigure hello yönlendirme yöntemi için istediğiniz hello profilinin adını tıklatın.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde, hem bulut Hizmetleri hello ve tooinclude yapılandırmanızda istediğiniz Web siteleri mevcut olduğunu doğrulayın.
4. Merhaba, **ayarları** 'yi tıklatın **yapılandırma**ve hello **yapılandırma** dikey penceresinde, aşağıdaki gibi tamamlandı:
    1. İçin **yönlendirme yöntemi ayarları trafiği**, için **yönlendirme yöntemi** seçin **performans**.
    2. Set hello **uç nokta izleme ayarları** aynı şekilde bu profili içindeki tüm her uç noktası için:
        1. Select hello uygun **Protokolü**ve hello belirtin **bağlantı noktası** numarası. 
        2. İçin **yolu** eğik yazın  */* . toomonitor uç noktaları, yol ve dosya adı belirtmelisiniz. Bir eğik çizgi "/" Merhaba göreli yolu geçerli bir girişi ve o hello dosyadır hello kök dizininde (varsayılan) anlamına gelir.
        3. Merhaba hello sayfanın en üstünde, tıklatın **kaydetmek**.
5.  Merhaba değişiklikleri yapılandırmanızda gibi test edin:
    1.  Hello portal'ın arama çubuğunda hello trafik Yöneticisi profili adını arayın ve görüntülenen o hello hello sonuçlarında hello trafik Yöneticisi profiline tıklayın.
    2.  Merhaba, **trafik Yöneticisi** profil dikey penceresinde, tıklatın **genel bakış**.
    3.  Merhaba **trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin hello DNS adını görüntüler. Bu herhangi (örneğin, göre bir web tarayıcısı kullanarak tooit gezinme) istemcileri yönlendirilen tooget toohello sağ uç nokta hello yönlendirme türü tarafından belirlendiği şekilde tarafından kullanılabilir. Bu durumda tüm istekleri hello hello istemcinin ağdan en düşük gecikme süresine sahip yönlendirilmiş toohello uç nokta var.
6. Traffic Manager profilinizin çalışma sonra şirket etki alanı adı toohello trafik yöneticisi etki alanı adı, yetkili DNS sunucusu toopoint hello DNS kaydını düzenleyin.

![Trafik Yöneticisi'ni kullanarak performans trafik yönlendirme yöntemini yapılandırma][1]

## <a name="next-steps"></a>Sonraki adımlar

- Hakkında bilgi edinin [ağırlıklı trafik yönlendirme yöntemini](traffic-manager-configure-weighted-routing-method.md).
- Hakkında bilgi edinin [öncelik yönlendirme yöntemi](traffic-manager-configure-priority-routing-method.md).
- Hakkında bilgi edinin [coğrafi yönlendirme yöntemi](traffic-manager-configure-geographic-routing-method.md).
- Nasıl çok öğrenin[test trafik Yöneticisi Ayarları](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png