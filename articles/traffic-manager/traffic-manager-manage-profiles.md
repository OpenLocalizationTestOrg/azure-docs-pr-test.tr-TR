---
title: aaaManage Azure Traffic Manager profillerini | Microsoft Docs
description: "Bu makale, bir Azure Traffic Manager profili oluşturma, devre dışı bırakma, etkinleştirme ve silme konularında size yardımcı olur."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Bir Azure Traffic Manager profilini yönetme

Trafik Yöneticisi profillerine trafik yönlendirme yöntemleri toocontrol hello dağıtımını trafik tooyour bulut hizmetini veya Web sitesi uç noktaları kullanın. Bu makalede açıklanır nasıl toocreate bu profilleri ve yönetin.

## <a name="create-a-traffic-manager-profile"></a>Traffic Manager profili oluşturma

Hello Azure portal kullanarak bir Traffic Manager profili oluşturabilirsiniz. Profilinizi oluşturduktan sonra hello Azure portalında uç noktaları, izleme ve diğer ayarları yapılandırabilirsiniz. Trafik Yöneticisi profili başına too200 uç noktaları yukarı destekler. Bununla birlikte, çoğu kullanım senaryosu yalnızca birkaç uç nokta gerektirir.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate bir Traffic Manager profili

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com). Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz. 
2. Merhaba üzerinde **Hub** menüsünde tıklatın **yeni** > **ağ** > **tümünü görmek**, tıklatın **trafiği Yöneticisi** profil tooopen hello **oluşturma trafik Yöneticisi profili** dikey penceresinde, ardından **oluşturma**.
3. Merhaba üzerinde **oluşturma trafik Yöneticisi profili** dikey penceresinde, aşağıdaki gibi tamamlandı:
    1. **Ad** alanında profiliniz için bir ad belirtin. Bu ad toobe hello trafficmanager.net bölge içinde benzersiz olmalıdır ve sonuçları hello DNS adıyla <name>, kullanılan tooaccess olan trafficmanager.net Traffic Manager profilinizin.
    2. İçinde **yönlendirme yöntemi**seçin hello **öncelik** yönlendirme yöntemi.
    3. İçinde **abonelik**, bu profili altında toocreate istediğiniz hello abonelik seçin
    4. İçinde **kaynak grubu**, yeni bir kaynak grubu tooplace altında bu profili oluşturun.
    5. İçinde **kaynak grubu konumu**, hello hello kaynak grubu konumunu seçin. Bu ayar, hello kaynak grubu toohello konumunu gösterir ve genel olarak dağıtılacak trafik Yöneticisi profili hello üzerinde hiçbir etkisi olmaz.
    6. **Oluştur**'a tıklayın.
    7. Trafik Yöneticisi profilinize Hello genel dağıtım tamamlandıktan sonra ilgili kaynak grubunda hello kaynaklardan biri listelenir.

## <a name="disable-enable-or-delete-a-profile"></a>Bir profili devre dışı bırakma, etkinleştirme veya silme

Bu trafik Yöneticisi kullanıcı istekleri toohello yapılandırılmış uç noktaları başvurmuyor için varolan bir profili devre dışı bırakabilirsiniz. Trafik Yöneticisi profili devre dışı bıraktığınızda, hello profili ve hello profilinde içerilen hello bilgi olduğu gibi kalır ve hello Traffic Manager arabiriminden düzenlenebilir.  Hello profili yeniden etkinleştirdiğinizde başvurular devam edin. Hello Azure portalında bir Traffic Manager profili oluşturduğunuzda, otomatik olarak etkinleştirilir. Bir profilin artık gerekli olmadığına karar verirseniz profili silebilirsiniz.

### <a name="toodisable-a-profile"></a>toodisable bir profili

1. Özel etki alanı kullanıyorsanız, Internet DNS sunucunuzdaki hello CNAME kaydını artık tooyour trafik Yöneticisi profili işaret şekilde değiştirin.
2. Trafik durur olma toohello uç noktaları hello Traffic Manager profili ayarları yoluyla yönlendirilmiş.
3. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** toomodify istediğiniz ve hello hello trafik Yöneticisi profiline ardından adı görüntülenen o hello sonuçlanır.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde tıklatın **genel bakış**, hello genel bakış dikey penceresinde tıklayın **devre dışı**ve toodisable hello trafik Yöneticisi profili onaylayın.

### <a name="tooenable-a-profile"></a>tooenable bir profili

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com).
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** toomodify istediğiniz ve hello hello trafik Yöneticisi profiline ardından adı görüntülenen o hello sonuçlanır.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde tıklatın **genel bakış**ve'i tıklatın ardından hello genel bakış dikey penceresinde **etkinleştirmek**.
5. Özel etki alanı kullanıyorsanız, Internet DNS sunucusu toopoint toohello etki alanı adını Traffic Manager profilinizin üzerinde bir CNAME kaynak kaydı oluşturun.
6. Yönlendirilmiş toohello uç noktaları yeniden trafiğidir.

### <a name="toodelete-a-profile"></a>toodelete bir profili

1. Merhaba, Internet DNS sunucunuzdaki DNS kaynak kaydını artık toohello Traffic Manager profilinizin etki alanı adına işaret eden bir CNAME kaynak kaydı kullandığından emin olun.
2. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** toomodify istediğiniz ve hello hello trafik Yöneticisi profiline ardından adı görüntülenen o hello sonuçlanır.
3. Merhaba, **trafik Yöneticisi profili** dikey penceresinde tıklatın **genel bakış**, hello genel bakış dikey penceresinde tıklayın **silmek**ve toodelete hello trafik Yöneticisi profili onaylayın.

## <a name="next-steps"></a>Sonraki adımlar

* [Bir uç nokta ekleme](traffic-manager-endpoints.md)
* [Öncelikli yönlendirme yöntemini yapılandırma](traffic-manager-configure-priority-routing-method.md)
* [Coğrafi yönlendirme yöntemini yapılandırma](traffic-manager-configure-geographic-routing-method.md) 
* [Ağırlıklı yönlendirme yöntemini yapılandırma](traffic-manager-configure-weighted-routing-method.md)
* [Performans yönlendirme yöntemini yapılandırma](traffic-manager-configure-performance-routing-method.md)
