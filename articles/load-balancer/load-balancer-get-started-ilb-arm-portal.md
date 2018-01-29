---
title: "İç yük dengeleyicisi oluşturma - Azure portalı | Microsoft Docs"
description: "Azure portalını kullanarak Resource Manager’da iç yük dengeleyici oluşturmayı öğrenin"
services: load-balancer
documentationcenter: na
author: KumudD
manager: jennoc
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 8f0f575319eec0517366079c637ad7565530ac70
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/11/2018
---
# <a name="create-an-internal-load-balancer-in-the-azure-portal"></a>Azure portalını kullanarak iç yük dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Azure portalı](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-ilb-arm-template.md)


[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Azure portalını kullanarak iç yük dengeleyici oluşturmaya başlama

Azure portalından iç yük dengeleyici oluşturmak için aşağıdaki adımları uygulayın.

1. Tarayıcı penceresi açın, [Azure portalına](http://portal.azure.com) gidin ve Azure hesabınızla oturum açın.
2. Ekranın sol üst kenarından **Yeni** > **Ağ** > **Yük dengeleyici**’yi seçin.
3. **Yük dengeleyici oluştur** dikey penceresinde yük dengeleyiciniz için bir **Ad** girin.
4. **Tür** altında **İç**’e tıklayın.
5. **Sanal ağ**’a tıklayıp yük dengeleyiciyi oluşturmak istediğiniz sanal ağı seçin.

   > [!NOTE]
   > Kullanmak istediğiniz sanal ağ listede yoksa, yük dengeleyici için kullandığınız **Konum** bilgisini denetleyin ve gerekli değişiklikleri yapın.

6. **Alt ağ**’a tıklayıp ve yük dengeleyiciyi oluşturmak istediğiniz alt ağı seçin.
7. **IP adresi atama** bölümünde yük dengeleyici IP adresinin sabit (statik) olup olmayacağını belirlemek için **Dinamik** veya **Statik** seçeneğini belirleyin.

   > [!NOTE]
   > Statik IP adresi kullanmayı tercih ederseniz yük dengeleyici için bir adres belirlemeniz gerekir.

8. **Kaynak grubu** altında yük dengeleyici için yeni bir kaynak grubu adı belirleyin veya var olan kaynak gruplarından birini seçmek için **var olanı seç**’e tıklayın.
9. **Oluştur**’a tıklayın.

## <a name="configure-load-balancing-rules"></a>Yük dengeleme kurallarını yapılandırma

Yük dengeleyiciyi oluşturduktan sonra yük dengeleyici kaynağına giderek yapılandırın.
Yük dengeleme kuralını yapılandırmadan önce arka uç adres havuzu ve araştırma yapılandırın.

### <a name="step-1-configure-a-backend-pool"></a>1. Adım: Arka uç havuzu yapılandırma

1. Azure portalında **Gözat** > **Yük dengeleyiciler**'e ve ardından daha önce oluşturduğunuz yük dengeleyiciye tıklayın.
2. **Ayarlar** sayfasında **Arka uç havuzları**’na tıklayın.
3. **Arka uç adres havuzları** sayfasında **Ekle**’ye tıklayın.
4. **Arka uç havuzu ekle** sayfasında arka uç havuzu için bir **Ad** girin ve ardından **Tamam**’a tıklayın.

### <a name="step-2-configure-a-probe"></a>2. Adım: Araştırma yapılandırma

1. Azure portalında **Gözat** > **Yük dengeleyiciler**'e ve ardından daha önce oluşturduğunuz yük dengeleyiciye tıklayın.
2. **Ayarlar** sayfasında **Durum araştırmaları**’na tıklayın.
3. **Durum araştırmaları** sayfasında **Ekle**’ye tıklayın.
4. **Durum araştırması ekle** sayfasında araştırma için bir **Ad** girin.
5. **Protokol**'ün altında **HTTP** (web siteleri için) veya **TCP** (diğer TCP tabanlı uygulamalar için) seçin.
6. **Bağlantı noktası** bölümünde araştırmaya erişirken kullanılacak bağlantı noktasını belirtin.
7. **Yol**’un altında (yalnızca HTTP araştırmaları için) araştırma olarak kullanılacak yolu belirtin.
8. **Aralık** bölümünde uygulama araştırma sıklığını belirtin.
9. **Sağlıksız durum eşiği** bölümünde arka uç sanal makinesi sağlıksız olarak işaretlenmeden önce yapılacak giriş sayısını belirtin.
10. Araştırmayı oluşturmak için **Tamam**’a tıklayın.

### <a name="step-3-configure-load-balancing-rules"></a>3. Adım: Yük dengeleme kurallarını yapılandırma

1. Azure portalında **Gözat** > **Yük dengeleyiciler**'e ve ardından daha önce oluşturduğunuz yük dengeleyiciye tıklayın.
2. **Ayarlar** sayfasında **Yük dengeleme kuralları**’na tıklayın.
3. **Yük dengeleme kuralları** sayfasında **Ekle**’ye tıklayın.
4. **Yük dengeleme kuralı ekle** sayfasında kural için bir **Ad** girin.
5. **Protokol** altında **TCP** veya **UDP**’yi seçin.
6. **Bağlantı noktası** bölümünde istemcilerin yük dengeleyiciye bağlanmak için kullanacağı bağlantı noktasını belirtin.
7. **Arka uç bağlantı noktası** bölümünde arka uç havuzunda kullanılacak bağlantı noktasını belirtin (genelde yük dengeleyici bağlantı noktası ve arka uç bağlantı noktası aynıdır).
8. **Arka uç havuzu** altında daha önce oluşturduğunuz arka uç havuzunu seçin.
9. **Oturum kalıcılığı** bölümünde oturumların ne kadar sürmesini istediğinizi belirtin.
10. **Boşta kalma zaman aşımı (dakika)** bölümünde boşta kalma zaman aşımını belirtin.
11. **Kayan IP (doğrudan sunucu dönüşü)** bölümünde **Devre dışı** veya **Etkin**’e tıklayın.
12. **Tamam**’a tıklayın.

## <a name="next-steps"></a>Sonraki adımlar

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

