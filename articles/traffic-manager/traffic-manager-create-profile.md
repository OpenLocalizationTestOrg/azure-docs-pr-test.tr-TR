---
title: "aaaCreate Azure trafik Yöneticisi profili | Microsoft Docs"
description: "Bu makalede nasıl toocreate bir Traffic Manager profili"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Traffic Manager profili oluşturma

Bu makalede bir profille nasıl **öncelik** yönlendirme türü tooroute kullanıcılar tootwo Azure Web Apps uç noktaları oluşturulabilir. Hello kullanarak **öncelik** hello ikinci bir yedek olarak tutarken türü yönlendirme, tüm trafik yönlendirilmiş toohello ilk uç noktadır. Sonuç olarak, kullanıcılar Hello ilk uç noktası bozulursa yönlendirilmiş toohello ikinci uç nokta olabilir.

Bu makalede, iki önceden oluşturulmuş Azure Web uygulaması yeni oluşturulan ilişkili toothis trafik Yöneticisi profili noktalarıdır. toolearn nasıl hakkında daha fazla toocreate Azure Web uygulaması uç noktaları, ziyaret hello [Azure Web Apps belge sayfasının](https://docs.microsoft.com/azure/app-service-web/). Bir DNS adı ve üzerinden erişilebilen herhangi bir uç nokta ekleyebilirsiniz hello ortak Internet ve biz örnek olarak Azure Web Apps uç noktaları kullanıyoruz.

### <a name="create-a-traffic-manager-profile"></a>Traffic Manager profili oluşturma
1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com). Zaten bir hesabınız yoksa, kaydolmak için yapabileceğiniz bir [ücretsiz bir aylık deneme](https://azure.microsoft.com/free/). 
2. Merhaba üzerinde **Hub** menüsünde tıklatın **yeni** > **ağ** > **tümünü görmek**, tıklatın **trafiği Yöneticisi** profil tooopen hello **oluşturma trafik Yöneticisi profili** dikey penceresinde, ardından **oluşturma**.
3. Merhaba üzerinde **oluşturma trafik Yöneticisi profili** dikey penceresinde, aşağıdaki gibi tamamlandı:
    1. **Ad** alanında profiliniz için bir ad belirtin. Bu ad toobe hello trafficmanager.net bölge içinde benzersiz olmalıdır ve sonuçları hello DNS adıyla <name>, kullanılan tooaccess olan trafficmanager.net Traffic Manager profilinizin.
    2. İçinde **yönlendirme yöntemi**seçin hello **öncelik** yönlendirme yöntemi.
    3. İçinde **abonelik**, bu profili altında toocreate istediğiniz hello abonelik seçin
    4. İçinde **kaynak grubu**, yeni bir kaynak grubu tooplace altında bu profili oluşturun.
    5. İçinde **kaynak grubu konumu**, hello hello kaynak grubu konumunu seçin. Bu ayar, hello kaynak grubu toohello konumunu gösterir ve genel olarak dağıtılacak trafik Yöneticisi profili hello üzerinde hiçbir etkisi olmaz.
    6. **Oluştur**'a tıklayın.
    7. Trafik Yöneticisi profilinize Hello genel dağıtım tamamlandıktan sonra ilgili kaynak grubunda hello kaynaklardan biri listelenir.

    ![Traffic Manager profili oluşturma](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Trafik Yöneticisi uç noktaları ekleme

1. Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** hello bölümü ve tıklatın hello trafik Yöneticisi profili hello önceki bölümünde oluşturduğunuz ad görüntülenen o hello sonuçları.
2. Merhaba, **trafik Yöneticisi profili** dikey penceresinde hello **ayarları** 'yi tıklatın **uç noktaları**.
3. Merhaba, **uç noktaları** görüntülenir, dikey tıklayın **Ekle**.
4. Merhaba, **uç nokta ekleme** dikey penceresinde, aşağıdaki gibi tamamlandı:
    1. **Tür** için **Azure uç noktası**’na tıklayın.
    2. Sağlayan bir **adı** istediğiniz toorecognize bu bitiş noktası.
    3. İçin **hedef kaynak türünün**, tıklatın **uygulama hizmeti**.
    4. İçin **hedef kaynak**, tıklatın **uygulama hizmeti seçin** tooshow hello hello altında Web uygulamaları hello listesi aynı abonelik. Merhaba, **kaynak** görüntülenir, dikey çekme hello ilk uç noktası hello gibi tooadd istediğiniz uygulama hizmeti.
    5. **Öncelik** için **1** seçin. Bu, sağlıklı ise toothis endpoint giden tüm trafiği içinde sonuçlanır.
    6. **Devre dışı olarak ekle** seçeneğini işaretsiz bırakın.
    7. **Tamam**’a tıklayın.
5.  Merhaba sonraki Azure Web Apps uç noktası için 3 ve 4 numaralı adımları tekrarlayın. Emin tooadd olun ile kendi **öncelik** değerini ayarlayın adresindeki **2**.
6.  Her iki uç noktaları Hello eklenmesi tamamlandığında hello görüntülendikleri **trafik Yöneticisi profili** dikey izleme durumlarını birlikte **çevrimiçi**.

    ![Trafik Yöneticisi uç noktası ekleme](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Merhaba trafik Yöneticisi profili kullanın
1.  Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** hello önceki bölümde oluşturduğunuz adı. Görüntülenen hello sonuçlarında hello trafik Yöneticisi profili tıklayın.
2. Merhaba, **trafik Yöneticisi profili** dikey penceresinde tıklatın **genel bakış**.
3. Merhaba **trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin hello DNS adını görüntüler. Bu herhangi (örneğin, göre bir web tarayıcısı kullanarak tooit gezinme) istemcileri yönlendirilen tooget toohello sağ uç nokta hello yönlendirme türü tarafından belirlendiği şekilde tarafından kullanılabilir. Bu durumda, tüm istekleri yönlendirilmiş toohello Birinci uç nokta olan ve trafik Yöneticisi algılarsa sağlıksız, hello trafiği toohello sonraki uç noktası üzerinden otomatik olarak başarısız olur.

## <a name="delete-hello-traffic-manager-profile"></a>Merhaba trafik Yöneticisi profilini Sil
Artık gerekli olduğunda, hello kaynak grubu ve oluşturduğunuz hello trafik Yöneticisi profilini silin. toodo bu nedenle, hello hello kaynak grubu seçin **trafik Yöneticisi profili** tıklayın ve dikey **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [yönlendirme türleri](traffic-manager-routing-methods.md).
- Uç nokta türleri hakkında daha fazla bilgi [uç nokta türleri](traffic-manager-endpoint-types.md).
- Daha fazla bilgi edinmek [uç nokta izleme](traffic-manager-monitoring.md).



