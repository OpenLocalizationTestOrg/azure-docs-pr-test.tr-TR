---
title: "coğrafi aaaConfigure trafik yönlendirme yöntemini Azure trafik Yöneticisi'ni kullanarak | Microsoft Docs"
description: "Bu makalede, nasıl tooconfigure hello Azure trafik Yöneticisi'ni kullanarak coğrafi trafik yönlendirme yöntemini açıklanmaktadır."
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Trafik Yöneticisi'ni kullanarak hello coğrafi trafik yönlendirme yöntemini yapılandırma

Merhaba coğrafi trafik yönlendirme yöntemini toospecific uç noktalar burada hello istekleri kaynaklanan hello coğrafi konum temelinde, toodirect trafiğine izin verir. Bu öğretici nasıl toocreate trafik Yöneticisi profili ile bu yönlendirme yöntemi gösterir ve belirli coğrafi hello uç noktaları tooreceive trafiğinden yapılandırın.

## <a name="create-a-traffic-manager-profile"></a>Trafik Yöneticisi profili oluştur

1. Toohello içinde bir tarayıcıdan oturum [Azure portal](http://portal.azure.com). Henüz bir hesabınız yoksa, [bir aylık ücretsiz denemeye](https://azure.microsoft.com/free/) kaydolabilirsiniz.
2. Merhaba Hub menüsünde **yeni** > **ağ** > **tümünü görmek**ve ardından **trafik Yöneticisi profili**tooopen hello **oluşturma trafik Yöneticisi profili** dikey.
3. Merhaba üzerinde **oluşturma trafik Yöneticisi profili** dikey penceresinde:
    1. Profiliniz için bir ad sağlayın. Bu ad toobe hello trafficmanager.net bölge içinde benzersiz olmalıdır ve hello DNS adının oluşmasına neden olacak <profilename>, olacak trafficmanager.net Traffic Manager profilinizin kullanılan tooaccess olabilir.
    2. Select hello **Geographic** yönlendirme yöntemi.
    3. Bu profili altında toocreate istediğiniz hello aboneliği seçin.
    4. Varolan bir kaynak grubunu kullanın veya yeni bir kaynak grubu tooplace altında bu profili oluşturun. Yeni bir kaynak grubu toocreate seçerseniz, hello kullanmanız **kaynak grubu konumu** açılır toospecify hello hello kaynak grubu konumunu. Bu ayar, hello kaynak grubu toohello konumunu gösterir ve genel olarak dağıtılacak trafik Yöneticisi profili hello üzerinde hiçbir etkisi olmaz.
    5. Tıklattıktan sonra **oluşturma**, Traffic Manager profilinizin oluşturulur ve genel olarak dağıtıldı.

![Traffic Manager profili oluşturma](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Uç noktaları ekleme

1. Merhaba portal'ın arama çubuğunda oluşturduğunuz hello trafik Yöneticisi profili adını arayın ve gösterildiğinde hello sonuca tıklayın.
2. Çok gidin**ayarları** -> **uç noktaları** hello trafik Yöneticisi dikey penceresinde.
3. Tıklatın **Ekle** tooshow hello **uç nokta Ekle** dikey.
3. Merhaba, **uç noktaları** dikey penceresinde tıklatın **Ekle** ve hello **uç nokta ekleme** görüntülenir, dikey tamamlamak aşağıdaki gibi:
4. Seçin **türü** eklemekte olduğunuz endpoint hello türüne bağlı olarak. Üretimde kullanılan, yönlendirme coğrafi profilleri birden fazla uç alt profiliyle içeren iç içe geçmiş uç nokta türleri kullanarak öneririz. Daha fazla ayrıntı için bkz: [coğrafi trafik yönlendirme yöntemleri hakkında sık sorulan sorular](traffic-manager-FAQs.md).
5. Sağlayan bir **adı** istediğiniz toorecognize bu bitiş noktası.
6. Bu dikey bazı alanları eklediğiniz uç nokta hello türüne bağlıdır:
    1. Azure uç ekliyorsanız hello seçin **hedef kaynak türünün** ve hello **hedef** hello kaynağını temel toodirect trafiği istediğiniz
    2. Ekliyorsanız bir **dış** uç noktasını hello sağlamak **tam etki alanı adı (FQDN)** uç noktanız için.
    3. Ekliyorsanız bir **iç içe endpoint**seçin hello **hedef kaynak** toouse istediğiniz ve hello belirtin toohello alt profili karşılık gelen **Minimum alt uç noktaları sayısı**.
7. Hello coğrafi eşleme bölümüne, kullanım hello açılan trafiği gönderilen toobe toothis endpoint istediğiniz yere tooadd hello bölgeleri. En az bir bölge eklemeniz gerekir ve birden çok bölgeye eşlenmiş olabilir.
8. Bu tüm uç noktaları için işlemi yineleyin tooadd bu profili altında istediğiniz

![Trafik Yöneticisi uç noktası ekleme](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Merhaba trafik Yöneticisi profili kullanın
1.  Merhaba Hello portal'ın arama çubuğunda arama **trafik Yöneticisi profili** hello önceki bölümde oluşturduğunuz ve hello hello trafik Yöneticisi profiline tıklayın sonuçların bu hello görüntülenen ad.
2. Merhaba, **trafik Yöneticisi profili** dikey penceresinde tıklatın **genel bakış**.
3. Merhaba **trafik Yöneticisi profili** dikey penceresinde, yeni oluşturulan Traffic Manager profilinizin hello DNS adını görüntüler. Bu herhangi (örneğin, göre bir web tarayıcısı kullanarak tooit gezinme) istemcileri yönlendirilen tooget toohello sağ uç nokta hello yönlendirme türü tarafından belirlendiği şekilde tarafından kullanılabilir.  Coğrafi üretim hello durumda, trafik Yöneticisi hello gelen isteğin kaynak IP hello arar ve kendisinden kaynaklanan hello bölgeyi belirler. Bu bölge eşlenen tooan uç nokta ise, yönlendirilmiş toothere trafiğidir. Bu bölge eşlenen tooan endpoint değilse, trafik Yöneticisi NODATA sorgu yanıtı döndürür.

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [Geographic trafik yönlendirme yöntemini](traffic-manager-routing-methods.md#geographic).
- Nasıl çok öğrenin[test trafik Yöneticisi Ayarları](traffic-manager-testing-settings.md).
