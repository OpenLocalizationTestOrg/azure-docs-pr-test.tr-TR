---
title: "aaaCreate bir Internet'e yönelik Yük Dengeleyici - Klasik Azure portalı | Microsoft Docs"
description: "Klasik Azure portalı toocreate Klasik dağıtım modeli kullanarak bir Internet'e yönelik Yük Dengeleyici hello nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Internet'e yönelik yük dengeleyicisi (Klasik) hello Klasik Azure portalı oluşturmaya başlamak

> [!div class="op_single_selector"]
> * [Klasik Azure Portalı](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik. Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun. Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz. Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Sanal makineler için İnternet’e yönelik yük dengeleyici kurma

Sipariş tooload Bakiye gelen ağ trafiğinin içinde hello Internet hello sanal makineler bir bulut hizmeti arasında yük dengeli kümesi oluşturmanız gerekir. Bu yordam hello sanal makineleri oluşturmuş ve tüm varsayar hello içinde aynı bulut hizmeti.

**sanal makineler için yük dengeli kümesi tooconfigure**

1. Hello Klasik Azure portalı, tıklatın **sanal makineleri**ve ardından Yük dengeli hello kümesindeki bir sanal makine hello adına tıklayın.
2. **Uç noktaları**’na ve ardından **Ekle**’ye tıklayın.
3. Merhaba üzerinde **bir uç nokta tooa sanal makine eklemek** sayfasında, hello sağ oka tıklayın.
4. Merhaba üzerinde **hello hello uç nokta ayrıntılarını belirtin** sayfa:

   * İçinde **adı**hello uç noktası için bir ad yazın veya yaygın protokoller için önceden tanımlanmış uç noktaları hello listeden hello adı seçin.
   * İçinde **Protokolü**, gerektiğinde uç noktası, TCP veya UDP, hello türü tarafından gerekli hello protokolü seçin.
   * İçinde **genel bağlantı noktası ve özel bağlantı noktası**, sanal makine toouse hello gerektiği gibi istediğiniz başlangıç bağlantı noktası numaralarını yazın. Uygulamanız için uygun şekilde hello sanal makine tooredirect trafiği üzerinde hello özel bağlantı noktası ve güvenlik duvarı kuralları'nı kullanabilirsiniz. Merhaba özel bağlantı noktası olması hello hello genel bağlantı noktası ile aynı. Örneğin, web (HTTP) trafiği için bir uç nokta için bağlantı noktası, 80 tooboth hello ortak ve özel bağlantı noktası atayabilirsiniz.

5. Seçin **bir yük dengeli kümesi oluşturma**ve ardından hello sağ oka tıklayın.
6. Merhaba üzerinde **hello yük dengeli küme Yapılandır** sayfasında, hello yük dengeli kümesi için bir ad yazın ve hello Azure yük dengeleyici araştırması davranışını hello değerlerini atayın. Merhaba yük dengeli kümesi Hello sanal makinelerin kullanılabilir tooreceive gelen trafiği varsa hello yük dengeleyici araştırmalar toodetermine kullanır.
7. Merhaba onay işareti toocreate hello yük dengeli uç'a tıklayın. Görürsünüz **Evet** hello içinde **yük dengeli kümesi adı** hello sütunu **uç noktaları** hello sanal makine için sayfa.
8. Merhaba Portalı'nda tıklatın **sanal makineleri**, ek bir sanal makine yükü dengelenmiş hello kümesindeki hello adına tıklayın, tıklatın **uç noktaları**ve ardından **Ekle**.
9. Merhaba üzerinde **bir uç nokta tooa sanal makine eklemek** sayfasında, **uç nokta tooan varolan yük dengeli kümesi ekleme**hello yük dengeli kümesi hello adını seçin ve ardından hello sağ oka tıklayın.
10. Merhaba üzerinde **hello hello uç nokta ayrıntılarını belirtin** sayfasında, hello uç noktası için bir ad yazın ve ardından hello onay işaretine tıklayın.

Merhaba ek sanal makineler için yük dengeli hello kümesinde, 8-10 adımları yineleyin.

## <a name="next-steps"></a>Sonraki adımlar

[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
