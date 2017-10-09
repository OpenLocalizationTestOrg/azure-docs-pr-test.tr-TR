---
title: "aaaConfigure öncelik trafik yönlendirme yöntemini Azure trafik Yöneticisi'ni kullanarak | Microsoft Docs"
description: "Bu makalede, nasıl tooconfigure hello öncelik trafik yönlendirme yöntemini trafik Yöneticisi'nde açıklanmaktadır."
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
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Trafik Yöneticisi'nde öncelik trafik yönlendirme yöntemini yapılandırma

Merhaba Web sitesi Modu bağımsız olarak, Azure Web siteleri zaten bir veri merkezi (bölge olarak da bilinir) içindeki Web siteleri için yük devretme işlevsellik sağlar. Trafik Yöneticisi, farklı veri merkezlerinde bulunan Web siteleri için yük devretme sağlar.

Hizmet yük devretmesi için genel bir desen toosend trafiği tooa birincil hizmetidir ve aynı yedekleme hizmetleri için yük devretme kümesi sağlar. Merhaba aşağıdaki adımlarda nasıl tooconfigure bu öncelik açıklanmaktadır yük devretme Azure bulut Hizmetleri ve Web siteleri:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>tooconfigure hello öncelik trafik yönlendirme yöntemi

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com). Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz. 
2. Merhaba Hello portal'ın arama çubuğunda arama **Traffic Manager profillerini** ve tooconfigure hello yönlendirme yöntemi için istediğiniz hello profilinin adını tıklatın.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde, hem bulut Hizmetleri hello ve tooinclude yapılandırmanızda istediğiniz Web siteleri mevcut olduğunu doğrulayın.
4. Merhaba, **ayarları** 'yi tıklatın **yapılandırma**ve hello **yapılandırma** dikey penceresinde, aşağıdaki gibi tamamlandı:
    1. İçin **yönlendirme yöntemi ayarları trafiği**, hello trafik yönlendirme yöntemini olduğundan emin olun **öncelik**. Değilse, **öncelik** hello aşağı açılan listeden.
    2. Set hello **uç nokta izleme ayarları** aynı şekilde bu profili içindeki tüm her uç noktası için:
        1. Select hello uygun **Protokolü**ve hello belirtin **bağlantı noktası** numarası. 
        2. İçin **yolu** eğik yazın  */* . toomonitor uç noktaları, yol ve dosya adı belirtmelisiniz. Bir eğik çizgi "/" Merhaba göreli yolu geçerli bir girişi ve o hello dosyadır hello kök dizininde (varsayılan) anlamına gelir.
        3. Merhaba hello sayfanın en üstünde, tıklatın **kaydetmek**.
5. Merhaba, **ayarları** 'yi tıklatın **uç noktaları**.
6. Merhaba, **uç noktaları** dikey penceresinde, noktalarınızı için gözden geçirme hello öncelik sırası. Merhaba seçtiğinizde **öncelik** trafik yönlendirme yöntemini, seçili hello uç noktaları hello sırası önemlidir. Uç noktaları Hello öncelik sırasını doğrulayın.  Merhaba birincil endpoint üstte olur. Görüntüleneceğini hello siparişte denetleyin. tüm istekleri yönlendirilmiş toohello ilk uç noktası ve trafik Yöneticisi algılarsa sağlıksız, hello trafiği toohello sonraki uç noktası üzerinden otomatik olarak başarısız olur. 
7. toochange Merhaba uç noktası öncelik sırasına, hello uç noktasına tıklayın ve hello **Endpoint** görüntülenir, dikey tıklayın **Düzenle** hello değiştirip **öncelik** değeri gerektiğinde . 
8. Tıklatın **kaydetmek** toosave hello uç noktası ayarlarını değiştirin.
9. Yapılandırma değişiklikleri tamamladıktan sonra tıklayın **kaydetmek** hello sayfanın hello sonundaki.
10. Merhaba değişiklikleri yapılandırmanızda gibi test edin:
    1.  Hello portal'ın arama çubuğunda hello trafik Yöneticisi profili adını arayın ve görüntülenen o hello hello sonuçlarında hello trafik Yöneticisi profiline tıklayın.
    2.  Merhaba, **trafik Yöneticisi** profil dikey penceresinde, tıklatın **genel bakış**.
    3.  Merhaba **trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin hello DNS adını görüntüler. Bu herhangi (örneğin, göre bir web tarayıcısı kullanarak tooit gezinme) istemcileri yönlendirilen tooget toohello sağ uç nokta hello yönlendirme türü tarafından belirlendiği şekilde tarafından kullanılabilir. Bu durumda, tüm istekleri yönlendirilmiş toohello Birinci uç nokta olan ve trafik Yöneticisi algılarsa sağlıksız, hello trafiği toohello sonraki uç noktası üzerinden otomatik olarak başarısız olur.
11. Traffic Manager profilinizin çalışma sonra şirket etki alanı adı toohello trafik yöneticisi etki alanı adı, yetkili DNS sunucusu toopoint hello DNS kaydını düzenleyin.

![Trafik Yöneticisi'ni kullanarak öncelik trafik yönlendirme yöntemini yapılandırma][1]

## <a name="next-steps"></a>Sonraki adımlar


- Hakkında bilgi edinin [ağırlıklı trafik yönlendirme yöntemini](traffic-manager-configure-weighted-routing-method.md).
- Hakkında bilgi edinin [performans yönlendirme yöntemini](traffic-manager-configure-performance-routing-method.md).
- Hakkında bilgi edinin [coğrafi yönlendirme yöntemi](traffic-manager-configure-geographic-routing-method.md).
- Nasıl çok öğrenin[test trafik Yöneticisi Ayarları](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png