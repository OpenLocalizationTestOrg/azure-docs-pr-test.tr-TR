---
title: "aaaManage uç noktaları Azure trafik Yöneticisi'nde | Microsoft Docs"
description: "Bu makale, Azure Traffic Manager'da uç noktalar ekleme, kaldırma, etkinleştirme ve devre dışı bırakma konularında size yardımcı olacaktır."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Uç noktaları ekleme, devre dışı bırakma, etkinleştirme veya silme

Azure App Service Web Apps özelliğini Hello zaten yük devretme ve hepsini bir kez deneme trafik yönlendirme işlevini hello Web sitesi modu ne olursa olsun, veri merkezi içindeki Web siteleri için sağlar. Azure Traffic Manager toospecify yük devretme ve farklı veri merkezlerinde bulunan Web siteleri ve bulut Hizmetleri için hepsini bir kez deneme trafik yönlendirme sağlar. İlk adım gerekli tooprovide tooadd hello bulut hizmeti veya Web sitesi uç nokta tooTraffic Yöneticisi işlevdir hello.

Aynı zamanda bir Traffic Manager profilinin parçası olan tekil uç noktalarını da devre dışı bırakabilirsiniz. Bir uç nokta devre dışı bırakma hello profilinin bir parçası olarak bırakır, ancak hello profil hello endpoint içine dahil edilmemişse gibi davranır. Bu eylem, bakım modunda veya yeniden dağıtılmakta olan bir uç noktanın geçici olarak kaldırılmasında yararlı olur. Merhaba uç nokta yeniden çalışır hale geldikten sonra etkinleştirilebilir.

> [!NOTE]
> Bir uç nokta devre dışı bırakma, sahip hiçbir şey toodo azure'da dağıtım durumuna sahip. Sağlıklı bir uç nokta kalır yukarı ve mümkün bile trafik Yöneticisi'nde devre dışı bırakıldığında tooreceive trafiği. Ek olarak, bir uç noktanın bir profilde devre dışı bırakılması başka bir profildeki durumunu etkilemez.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd bir bulut hizmeti ya da bir uygulama Hizmeti uç noktası tooa trafik Yöneticisi profili

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** toomodify istediğiniz ve hello hello trafik Yöneticisi profiline ardından adı görüntülenen o hello sonuçlanır.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde hello **ayarları** 'yi tıklatın **uç noktaları**.
4. Merhaba, **uç noktaları** görüntülenir, dikey tıklayın **Ekle**.
5. Merhaba, **uç nokta ekleme** dikey penceresinde, aşağıdaki gibi tamamlandı:
    1. **Tür** için **Azure uç noktası**’na tıklayın.
    2. Sağlayan bir **adı** istediğiniz toorecognize bu bitiş noktası.
    3. İçin **hedef kaynak türünün**, gelen açılan Merhaba, hello uygun kaynak türü seçin.
    4. İçin **hedef kaynak**, gelen açılan Merhaba, hello uygun hedef kaynak seçin tooshow hello listeleme kaynaklarınıza hello hello aynı abonelikte **kaynaklar dikey**. Merhaba, **kaynak** görüntülenir, dikey ilk uç noktası hello gibi tooadd istediğiniz çekme hello hizmet.
    5. **Öncelik** için **1** seçin. Bu, sağlıklı ise toothis endpoint giden tüm trafiği içinde sonuçlanır.
    6. **Devre dışı olarak ekle** seçeneğini işaretsiz bırakın.
    7. **Tamam**’a tıklayın.
6.  Adım 4 ve 5 tooadd hello sonraki Azure endpoint yineleyin. Emin tooadd olun ile kendi **öncelik** değerini ayarlayın adresindeki **2**.
7.  Her iki uç noktaları Hello eklenmesi tamamlandığında hello görüntülendikleri **trafik Yöneticisi profili** dikey izleme durumlarını birlikte **çevrimiçi**.

> [!NOTE]
> Hello kullanarak bir profilden bir uç nokta ekleyip sonra *yük devretme* trafik yönlendirme metodu, hello yük devretme öncelik değil sıralı liste, istediğiniz biçimde. Merhaba yük devretme öncelik listesini hello yapılandırma sayfasında hello sırasını ayarlayabilirsiniz. Daha fazla bilgi için bkz. [Yük devretme trafik yönlendirmesini yapılandırma](traffic-manager-configure-failover-routing-method.md).

## <a name="toodisable-an-endpoint"></a>toodisable bir uç nokta

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** adı toomodify istediğiniz ve sonra görüntülenen hello sonuçlarında hello trafik Yöneticisi profili seçin.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde hello **ayarları** 'yi tıklatın **uç noktaları**. 
4. Toodisable, istediğiniz hello uç noktasına tıklayın ve ardından hello **Endpoint** görüntülenir, dikey tıklayın **Düzenle**.
5. Merhaba, **Endpoint** dikey penceresinde hello uç nokta durumu çok değiştirme**devre dışı**ve ardından **kaydetmek**.
6. İstemciler toosend trafiği toohello endpoint hello süresince için-yaşam süresi (TTL) devam eder. Merhaba TTL hello trafik Yöneticisi profili hello yapılandırma sayfasında değiştirebilirsiniz.

## <a name="tooenable-an-endpoint"></a>tooenable bir uç nokta

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** adı toomodify istediğiniz ve sonra görüntülenen hello sonuçlarında hello trafik Yöneticisi profili seçin.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde hello **ayarları** 'yi tıklatın **uç noktaları**. 
4. Toodisable, istediğiniz hello uç noktasına tıklayın ve ardından hello **Endpoint** görüntülenir, dikey tıklayın **Düzenle**.
5. Merhaba, **Endpoint** dikey penceresinde hello uç nokta durumu çok değiştirme**etkin**ve ardından **kaydetmek**.
6. İstemciler toosend trafiği toohello endpoint hello süresince için-yaşam süresi (TTL) devam eder. Merhaba TTL hello trafik Yöneticisi profili hello yapılandırma sayfasında değiştirebilirsiniz.

## <a name="toodelete-an-endpoint"></a>toodelete bir uç nokta

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** adı toomodify istediğiniz ve sonra görüntülenen hello sonuçlarında hello trafik Yöneticisi profili seçin.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde hello **ayarları** 'yi tıklatın **uç noktaları**. 
4. Toodisable, istediğiniz hello uç noktasına tıklayın ve ardından hello **Endpoint** görüntülenir, dikey tıklayın **Düzenle**.
5. Merhaba, **Endpoint** dikey penceresinde hello uç nokta durumu çok değiştirme**etkin**ve ardından **kaydetmek**.


## <a name="next-steps"></a>Sonraki adımlar

* [Traffic Manager profillerini yönetme](traffic-manager-manage-profiles.md)
* [Yönlendirme yöntemlerini yapılandırma](traffic-manager-configure-routing-method.md)
* [Düzeyi düşürülmüş Traffic Manager durumu için sorun giderme](traffic-manager-troubleshooting-degraded.md)
* [Traffic Manager için performans konuları](traffic-manager-performance-considerations.md)
* [Traffic Manager üzerindeki işlemler (REST API Başvurusu)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

