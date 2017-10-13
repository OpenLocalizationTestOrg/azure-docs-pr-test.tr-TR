---
title: "Azure Traffic Manager'da uç noktaları yönetme | Microsoft Belgeleri"
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
ms.openlocfilehash: 765d12bc283d991783fb3190ce7917b573f9fc78
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Uç noktaları ekleme, devre dışı bırakma, etkinleştirme veya silme

Azure App Service'teki Web Apps özelliği, web sitesi modundan bağımsız olarak bir veri merkezi içindeki web siteleri için yük devretme ve hepsini bir kez deneme trafik yönlendirme işlevini zaten sağlamaktadır. Azure Traffic Manager, farklı veri merkezlerinde bulunan web siteleri ve bulut hizmetleri için yük devretme ve hepsini bir kez deneme trafik yönlendirmesini belirtmenize olanak tanır. Bu işlevin sağlanması için gereken ilk adım, bulut hizmeti veya web sitesi uç noktasını Traffic Manager'a eklemektir.

Aynı zamanda bir Traffic Manager profilinin parçası olan tekil uç noktalarını da devre dışı bırakabilirsiniz. Devre dışı bırakılan bir uç nokta profilin parçası olmaya devam eder ancak profil, uç nokta profile dahil edilmemiş gibi davranır. Bu eylem, bakım modunda veya yeniden dağıtılmakta olan bir uç noktanın geçici olarak kaldırılmasında yararlı olur. Uç nokta yeniden çalışır duruma geldiği zaman etkinleştirilebilir.

> [!NOTE]
> Bir uç noktanın devre dışı bırakılması Azure'daki dağıtım durumu ile hiçbir şekilde bağlantılı değildir. Sağlıklı bir uç nokta Traffic Manager'da devre dışı bırakıldığında bile çalışır durumda kalır ve trafik alabilir. Ek olarak, bir uç noktanın bir profilde devre dışı bırakılması başka bir profildeki durumunu etkilemez.

## <a name="to-add-a-cloud-service-or-an-app-service-endpoint-to-a-traffic-manager-profile"></a>Bir Traffic Manager profiline bulut hizmeti veya App Service uç noktası ekleme

1. Bir tarayıcıdan [Azure portalında](http://portal.azure.com) oturum açın.
2. Portalın arama çubuğunda, değiştirmek istediğiniz **Traffic Manager profili** adını arayın ve ardından gösterilen sonuçlardaki Traffic Manager profiline tıklayın.
3. **Ayarlar** bölümündeki **Traffic Manager profili** dikey penceresinde **Uç noktalar** öğesine tıklayın.
4. Gösterilen **Uç noktalar** dikey penceresinde **Ekle**’ye tıklayın.
5. **Uç nokta ekle** dikey penceresinde, aşağıdaki işlemleri tamamlayın:
    1. **Tür** için **Azure uç noktası**’na tıklayın.
    2. Bu uç noktayı tanımak istediğiniz bir **Ad** belirtin.
    3. **Hedef kaynak türü** için açılır listeden uygun kaynak türünü seçin.
    4. **Hedef kaynak** için, açılır listeden **Kaynaklar** dikey penceresindeki aynı abonelik altında listeleme kaynaklarını göstermek üzere uygun hedef kaynağı seçin. Gösterilen **Kaynak** dikey penceresinde, birinci uç nokta olarak eklemek istediğiniz hizmeti seçin.
    5. **Öncelik** için **1** seçin. Bu durum, sağlıksız olması durumunda tüm trafiğin bu uç noktaya gitmesiyle sonuçlanır.
    6. **Devre dışı olarak ekle** seçeneğini işaretsiz bırakın.
    7. **Tamam**’a tıklayın.
6.  Sonraki Azure uç noktasını eklemek için 4. ve 5. adımları tekrarlayın. Uç noktayı eklerken **Öncelik** değerinin **2** olarak ayarlandığından emin olun.
7.  Her iki uç noktanın eklenmesi tamamlandığında, **Çevrimiçi** izleme durumuyla birlikte **Traffic Manager profili** dikey penceresinde gösterilir.

> [!NOTE]
> *Yük devretme* trafik yönlendirme yöntemini kullanarak bir uç noktayı profile eklediğinizde veya profilden kaldırdığınızda, yük devretme öncelik listesi istediğiniz şekilde sıralanmayabilir. Yapılandırma sayfasında, Yük Devretme Önceliği Listesinin sırasını ayarlayabilirsiniz. Daha fazla bilgi için bkz. [Yük devretme trafik yönlendirmesini yapılandırma](traffic-manager-configure-failover-routing-method.md).

## <a name="to-disable-an-endpoint"></a>Bir uç noktayı devre dışı bırakma

1. Bir tarayıcıdan [Azure portalında](http://portal.azure.com) oturum açın.
2. Portalın arama çubuğunda, değiştirmek istediğiniz **Traffic Manager profili** adını arayın ve ardından gösterilen sonuçlardaki Traffic Manager profiline tıklayın.
3. **Ayarlar** bölümündeki **Traffic Manager profili** dikey penceresinde **Uç noktalar** öğesine tıklayın. 
4. Devre dışı bırakmak istediğiniz uç noktaya tıklayın ve sonra gösterilen **Uç Nokta** dikey penceresinde **Düzenle**’ye tıklayın.
5. **Uç Nokta** dikey penceresinde, uç nokta durumunu **Devre Dışı** olarak değiştirip **Kaydet**’e tıklayın.
6. İstemciler, Yaşam Süresi (TTL) boyunca uç noktaya trafik göndermeye devam eder. Traffic Manager profilinin Yapılandırma sayfasında TTL'yi değiştirebilirsiniz.

## <a name="to-enable-an-endpoint"></a>Bir uç noktayı etkinleştirme

1. Bir tarayıcıdan [Azure portalında](http://portal.azure.com) oturum açın.
2. Portalın arama çubuğunda, değiştirmek istediğiniz **Traffic Manager profili** adını arayın ve ardından gösterilen sonuçlardaki Traffic Manager profiline tıklayın.
3. **Ayarlar** bölümündeki **Traffic Manager profili** dikey penceresinde **Uç noktalar** öğesine tıklayın. 
4. Devre dışı bırakmak istediğiniz uç noktaya tıklayın ve sonra gösterilen **Uç Nokta** dikey penceresinde **Düzenle**’ye tıklayın.
5. **Uç Nokta** dikey penceresinde, uç nokta durumunu **Etkin** olarak değiştirip **Kaydet**’e tıklayın.
6. İstemciler, Yaşam Süresi (TTL) boyunca uç noktaya trafik göndermeye devam eder. Traffic Manager profilinin Yapılandırma sayfasında TTL'yi değiştirebilirsiniz.

## <a name="to-delete-an-endpoint"></a>Uç noktayı silmek için

1. Bir tarayıcıdan [Azure portalında](http://portal.azure.com) oturum açın.
2. Portalın arama çubuğunda, değiştirmek istediğiniz **Traffic Manager profili** adını arayın ve ardından gösterilen sonuçlardaki Traffic Manager profiline tıklayın.
3. **Ayarlar** bölümündeki **Traffic Manager profili** dikey penceresinde **Uç noktalar** öğesine tıklayın. 
4. Devre dışı bırakmak istediğiniz uç noktaya tıklayın ve sonra gösterilen **Uç Nokta** dikey penceresinde **Düzenle**’ye tıklayın.
5. **Uç Nokta** dikey penceresinde, uç nokta durumunu **Etkin** olarak değiştirip **Kaydet**’e tıklayın.


## <a name="next-steps"></a>Sonraki adımlar

* [Traffic Manager profillerini yönetme](traffic-manager-manage-profiles.md)
* [Yönlendirme yöntemlerini yapılandırma](traffic-manager-configure-routing-method.md)
* [Düzeyi düşürülmüş Traffic Manager durumu için sorun giderme](traffic-manager-troubleshooting-degraded.md)
* [Traffic Manager için performans konuları](traffic-manager-performance-considerations.md)
* [Traffic Manager üzerindeki işlemler (REST API Başvurusu)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

