---
title: "bir iç yük dengeleyici - Azure portalında aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir dahili yük dengeleyici kaynak hello Azure portal kullanarak Yöneticisi'nde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Bir iç yük dengeleyici hello Azure portal oluşturma

> [!div class="op_single_selector"]
> * [Azure Portal](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Azure portalını kullanarak iç yük dengeleyici oluşturmaya başlama

Hello Azure Portalı ' adımları toocreate bir iç yük dengeleyici aşağıdaki hello kullanın.

1. Bir tarayıcı açın, toohello gidin [Azure portal](http://portal.azure.com)ve Azure hesabınızla oturum açın.
2. Merhaba üst sol taraftaki hello ekranının, tıklatın **yeni** > **ağ** > **yük dengeleyici**.
3. Merhaba, **oluşturma yük dengeleyici** dikey penceresinde girin bir **adı** , yük dengeleyici için.
4. **Düzen** bölümünde **İç**’e tıklayın.
5. Tıklatın **sanal ağ**, ve ardından istediğiniz yere toocreate hello yük dengeleyici sanal ağ seçin hello.

   > [!NOTE]
   > Merhaba sanal ağ toouse istediğiniz görmüyorsanız hello denetleyin **konumu** hello yük dengeleyicisi kullanıyorsanız ve uygun şekilde değiştirin.

6. Tıklatın **alt**ve ardından istediğiniz yere toocreate hello yük dengeleyici hello alt ağ seçin.
7. Altında **IP adresi ataması**, tıklayın **dinamik** veya **statik**veya başlangıç IP adresi sabit hello yük dengeleyici toobe için (statik) isteyip istemediğinizi bağlı olarak.

   > [!NOTE]
   > Statik bir IP adresi toouse seçerseniz, hello yük dengeleyici için bir adres tooprovide gerekir.

8. Altında **kaynak grubu** hello hello yük dengeleyici için yeni bir kaynak grubu adını belirtin ya da tıklatın **Varolanı seç** ve varolan bir kaynak grubu seçin.
9. **Oluştur**'a tıklayın.

## <a name="configure-load-balancing-rules"></a>Yük dengeleme kurallarını yapılandırma

Merhaba sonra Yük Dengeleyici oluşturma, toohello yük dengeleyici kaynak tooconfigure gidin.
Tooconfigure önce bir arka uç adres havuzu ve bir araştırma Yük Dengeleme kuralı yapılandırmadan önce gerekir.

### <a name="step-1-configure-a-back-end-pool"></a>1. Adım: Arka uç havuzu yapılandırma

1. Hello Azure portal'ı tıklatın **Gözat** > **yük dengeleyici**, yukarıda oluşturduğunuz hello yük dengeleyici'a tıklayın.
2. Merhaba, **ayarları** dikey penceresinde tıklatın **arka uç havuzları**.
3. Merhaba, **arka uç adres havuzlarında** dikey penceresinde tıklatın **Ekle**.
4. Merhaba, **arka uç havuzu ekleme** dikey penceresinde girin bir **adı** hello arka uç havuzu ve ardından **Tamam**.

### <a name="step-2-configure-a-probe"></a>2. Adım: Araştırma yapılandırma

1. Hello Azure portal'ı tıklatın **Gözat** > **yük dengeleyici**, yukarıda oluşturduğunuz hello yük dengeleyici'a tıklayın.
2. Merhaba, **ayarları** dikey penceresinde tıklatın **yoklamaları**.
3. Merhaba, **yoklamaları** dikey penceresinde tıklatın **Ekle**.
4. Merhaba, **Ekle araştırma** dikey penceresinde girin bir **adı** hello araştırma için.
5. **Protokol**’ün altında **HTTP** (web siteleri için) veya **TCP** (diğer TCP tabanlı uygulamalar için) seçin.
6. Altında **bağlantı noktası**, başlangıç bağlantı noktası toouse hello araştırma erişirken belirtin.
7. Altında **yolu** (HTTP için yalnızca araştırmalarının), hello yolu toouse bir araştırma belirtin.
8. Altında **aralığı** ne sıklıkta tooprobe hello uygulama belirtin.
9. Altında **sağlıksız durum eşiği**, hello arka uç sanal makine olarak sağlıksız olarak işaretlenmiş önce kaç tane denemeleri başarısız belirtin.
10. Tıklatın **Tamam** toocreate araştırma.

### <a name="step-3-configure-load-balancing-rules"></a>3. Adım: Yük dengeleme kurallarını yapılandırma

1. Hello Azure portal'ı tıklatın **Gözat** > **yük dengeleyici**, yukarıda oluşturduğunuz hello yük dengeleyici'a tıklayın.
2. Merhaba, **ayarları** dikey penceresinde tıklatın **Yük Dengeleme kuralları**.
3. Merhaba, **Yük Dengeleme kuralları** dikey penceresinde tıklatın **Ekle**.
4. Merhaba, **Ekle Yük Dengeleme kuralını** dikey penceresinde girin bir **adı** hello kuralı için.
5. **Protokol**’ün altında **HTTP** (web siteleri için) veya **TCP** (diğer TCP tabanlı uygulamalar için) seçin.
6. Altında **bağlantı noktası**, başlangıç bağlantı noktası istemcileri bağlama tooin hello yük dengeleyici belirtin.
7. Altında **arka uç bağlantı noktası**, başlangıç bağlantı noktası toobe hello arka uç havuzunda kullanılan belirtin (genellikle hello yük dengeleyici bağlantı noktası ve hello arka uç bağlantı noktası olan hello aynı).
8. Altında **arka uç havuzu**seçin hello arka uç havuzu, yukarıda oluşturduğunuz.
9. Altında **oturum kalıcılığını**, oturumlar toopersist istediğiniz yöntemini seçin.
10. Altında **boşta kalma zaman aşımı (dakika)**, hello boşta kalma zaman aşımı belirtin.
11. **Kayan IP (doğrudan sunucu dönüşü)** bölümünde **Devre dışı** veya **Etkin**’e tıklayın.
12. **Tamam** düğmesine tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

