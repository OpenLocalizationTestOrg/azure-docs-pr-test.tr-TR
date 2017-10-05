---
title: "Azure içinde birden fazla IP yapılandırması dengelemesini | Microsoft Docs"
description: "Birincil ve ikincil IP yapılandırmaları yükdengeleme"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: cf1e68c7b37b2506de007bdf24eea63a27187a33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-the-azure-portal"></a>Azure portalını kullanarak birden fazla IP yapılandırması üzerinde yükdengeleme

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

Bu makalede, bir ikincil ağ arabirimi (NIC) üzerinde birden çok IP adresleriyle Azure yük dengeleyici kullanmayı açıklar. Bu senaryo için Windows, her birincil ve ikincil bir NIC ile çalışan iki VM sahibiz Her ikincil NIC'ler, iki IP yapılandırmaları vardır. Her VM Web siteleri contoso.com ve fabrikam.com barındırır. Her Web sitesi IP yapılandırmaları birine ikincil NIC üzerinde bağlı Azure yük dengeleyici iki ön uç IP adresi, bir Web sitesi için ilgili IP yapılandırmasını trafiğini dağıtmak için her Web sitesi için kullanıma sunmak için kullanırız. Bu senaryo aynı bağlantı noktası numarası hem ön uçlar yanı sıra arasında her iki arka uç havuzu IP adreslerini kullanır.

![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Ön koşullar
Bu örnek, adlı bir kaynak grubu sahibi olduğunuzu varsayar *contosofabrikam* aşağıdaki yapılandırmaya sahip:
 -  adlı bir sanal ağ içerir *myVNet*, iki VM adlı *VM1* ve *VM2* adlandırılmış sırasıyla aynı kullanılabilirlik kümesi içinde *myAvailset*. 
 - Her VM birincil NIC ve ikincil bir NIC'e sahip. Birincil NIC adlı *VM1NIC1* ve *VM2NIC1* ve ikincil NIC'ler adlı *VM1NIC2* ve *VM2NIC2*. Birden çok NIC VM'ler oluşturma hakkında daha fazla bilgi için bkz: [ile birden çok NIC PowerShell kullanarak bir VM oluşturma](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a>Birden çok IP yapılandırmaları dengelemek için adımları

Bu makalede açıklanan senaryo elde etmek için bu adımları izleyin:

### <a name="step-1-configure-the-secondary-nics-for-each-vm"></a>1. adım: ikincil NIC'ler her VM için yapılandırma

Sanal ağınızdaki her VM için ikincil NIC IP yapılandırmasını aşağıdaki şekilde ekleyin:  

1. Bir tarayıcı üzerinden Azure portalına gidin: http://portal.azure.com ve Azure hesabınızda oturum açın.
2. Ekranın sol üst tarafındaki kaynak grubu simgesine tıklayın ve sanal makineleri içinde bulunur kaynak grubunu tıklatın (örneğin, *contosofabrikam*). **Kaynak grupları** VM'ler için ağ arabirimleri ile birlikte tüm kaynakları listeler dikey şimdi görüntülenir.
3. Her VM ikincil NIC'ye IP yapılandırması aşağıdaki şekilde ekleyin:
    1. IP yapılandırması için eklemek istediğiniz ağ arabirimi seçin.
    2. Seçtiğiniz NIC görünür dikey penceresinde, tıklayın **IP yapılandırmaları**. Ardından **Ekle** görüntülenir dikey pencerenin üstündeki bulunun.
    3. İçinde **eklemek IP yapılandırmaları** dikey penceresinde, ikinci bir IP yapılandırması NIC'ye aşağıdaki şekilde ekleyin: 
        1. İkincil IP yapılandırması için bir ad yazın (örneğin, IP yapılandırmaları olarak VM1 ve VM2 adı için *VM1NIC2 ipconfig2* ve *VM2NIC2 ipconfig2* sırasıyla).
        2. İçin **özel IP adresi**, için **ayırma**seçin **statik**.
        3. **Tamam** düğmesine tıklayın.
        4. İkinci IP yapılandırmasını ikincil NIC tamamlandığında görüntülenir **IP yapılandırmaları** verilen NIC için ayarlar dikey penceresi

### <a name="step-2-create-a-load-balancer"></a>2. adım: bir yük dengeleyici oluşturma

Bir yük dengeleyici gibi oluşturun:

1. Bir tarayıcı üzerinden Azure portalına gidin: http://portal.azure.com ve Azure hesabınızda oturum açın.
2. Ekranın sol üst tarafında tıklatın **yeni** > **ağ** > **yük dengeleyici**. Bundan sonra öğesini **oluşturma**.
3. **Yük dengeleyici oluştur** dikey penceresinde yük dengeleyiciniz için bir ad girin. Burada adlı *mylb*.
4. Ortak IP adresi altında adlı yeni bir genel IP oluşturun **PublicIP1**.
5. Kaynak grubu altında Vm'leriniz var olan kaynak grubunu seçin (örneğin, *contosofabrikam*). Ardından, uygun bir konum seçin ve ardından **Tamam**. Yük dengeleyici dağıtımı başlayacak ve birkaç dakika içinde başarıyla tamamlanacaktır.
6. Uygulama dağıtıldıktan sonra Yük Dengeleyici bir kaynak, kaynak grubu olarak görüntülenir.

### <a name="step-3-configure-the-frontend-ip-pool"></a>3. adım: ön uç IP havuzu yapılandırma

Her Web sitesi (Contoso ve Fabrikam) için ön uç IP havuzu aşağıdaki gibi yapılandırın:

1. Portalı'nda tıklatın **daha fazla hizmet** > türü **genel IP adresi** filtre kutusuna ve ardından **ortak IP adresleri**. Tıklatın **Ekle** görüntülenir dikey pencerenin üstündeki bulunun.
2. İki ortak IP adreslerini yapılandırın (*PublicIP1* ve *PublicIP2*) aşağıdaki gibi iki Web sitesi (contoso ve fabrikam) için:
    1. Ön uç IP adresi için bir ad yazın.
    2. İçin **kaynak grubu**, sanal makineleri var olan kaynak grubunu seçin (örneğin, *contosofabrikam*).
    3. İçin **konumu**, VM'ler aynı konumu seçin.
    4. **Tamam** düğmesine tıklayın.
    5. İki ortak IP adresi oluşturulduktan sonra bunların her ikisi de görüntülenen **genel IP** adresleri dikey.
3. Portalı'nda tıklatın **daha fazla hizmet** > türü **yük dengeleyici** filtre kutusuna ve ardından **yük dengeleyici**.  
4. Yük Dengeleyici seçin (*mylb*) ön uç IP havuzuna eklemek istediğiniz.
5. Altında **ayarları**seçin **ön uç havuzları**. Ardından **Ekle** görüntülenir dikey pencerenin üstündeki bulunun.
6. Ön uç IP adresi için bir ad yazın (*farbikamfe* veya **contosofe*).
7. Tıklatın **IP adresi** ve **seçin genel IP adresi** IP adreslerini dikey penceresinde, seçin, ön uç (*PublicIP1* veya *PublicIP2*).
8. İkinci ön uç IP adresi oluşturmak için bu bölümü içindeki 3 ila 7 adımları yineleyin.
9. Ön uç IP havuzu yapılandırması tamamlandığında, hem ön uç IP adreslerini görüntülenen **ön uç IP havuzu** dikey penceresinde, yük dengeleyicinin. 
    
### <a name="step-4-configure-the-backend-pool"></a>4. adım: arka uç havuzunu yapılandırma   
Arka uç adres havuzu, yük dengeleyici (Contoso ve Fabrikam) her Web sitesi için aşağıdaki gibi yapılandırın:
        
1. Portalı'nda tıklatın **daha fazla hizmet** > Yük Dengeleyici filtre kutusuna yazın ve ardından **yük dengeleyici**.  
2. Yük Dengeleyici seçin (*mylb*) için arka uç havuzları eklemek istediğiniz.
3. Altında **ayarları**seçin **arka uç havuzları**. Arka uç havuzu için bir ad yazın (örneğin, *contosopool* veya *fabrikampool*). Ardından **Ekle** düğmesi görüntülenir dikey pencerenin üstündeki bulunun. 
4. İçin **ilişkili**seçin **kullanılabilirlik kümesi**.
5. İçin **kullanılabilirlik kümesi**seçin **myAvailset**.
6. Her iki VM için hedef ağ IP yapılandırmaları (bkz: Şekil 2) aşağıdaki şekilde ekleyin:  
    1. İçin **hedef sanal makine**, (örneğin, VM1 veya VM2) arka uç havuzu eklemek istediğiniz VM seçin.
    2. İçin **ağ IP yapılandırması**, (örneğin, VM1NIC2 ipconfig2 veya VM2NIC2 ipconfig2) bu VM ikincil NIC IP yapılandırmasını seçin.
    ![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Şekil 2**: yük dengeleyici arka uç havuzları ile yapılandırma  
7. **Tamam** düğmesine tıklayın.
8. Arka uç havuzu yapılandırması tamamlandığında, her iki arka uç adres havuzlarında görüntülenen **arka uç havuzu dikey** , yük dengeleyicinin.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>Adım 5: sistem durumu araştırması, yük dengeleyici için yapılandırma
Yük Dengeleyici için bir sistem durumu araştırma aşağıdaki gibi yapılandırın:
    1. Daha fazla hizmet Portalı'nda tıklayın > Yük Dengeleyici filtre kutusuna yazın ve ardından **yük dengeleyici**.  
    2. Arka uç havuzları eklemek istediğiniz yük dengeleyici seçin.
    3. Altında **ayarları**seçin **durumu araştırması**. Ardından **Ekle** görüntülenir dikey pencerenin üstündeki bulunun.
    4. Sistem durumu araştırması (örneğin, HTTP) için bir ad yazın ve'ı tıklatın **Tamam**.

### <a name="step-6-configure-load-balancing-rules"></a>6. adım: Yük Dengeleme kuralları yapılandırma
Yük Dengeleme kuralları yapılandırın (*HTTPc* ve *HTTPf*) aşağıdaki gibi her Web sitesi için:
    
1. Altında **ayarları**seçin **durumu araştırması**. Ardından **Ekle** görüntülenir dikey pencerenin üstündeki bulunun.
2. İçin **adı**, Yük Dengeleme kuralı için bir ad yazın (örneğin, *HTTPc* contoso, veya *HTTPf* Fabrikam için)
3. Ön uç IP adresini seçin Ön uç IP adresi (örneğin *Contosofe* veya *Fabrikamfe*)
4. İçin **bağlantı noktası** ve **arka uç bağlantı noktası**, varsayılan değer tutmak **80**.
5. İçin **kayan IP (doğrudan sunucu dönüşü)**, tıklatın **etkin**.
6. **Tamam** düğmesine tıklayın.
7. 1 ile 6 ikinci yük dengeleyici kuralı oluşturmak için bu bölümü içindeki adımları yineleyin.
8. Ne zaman Yapılandırma tamamlandığında Yük Dengeleme kuralları, hem kuralları ((*HTTPc* ve *HTTPf*) görüntülenen **Yük Dengeleme kuralları** dikey penceresinde, yük dengeleyicinin.

### <a name="step-7-configure-dns-records"></a>7. adım: DNS kayıtlarını Yapılandır
Son olarak, DNS kaynak kayıtlarını yük dengeleyici ilgili ön uç IP adresine işaret edecek şekilde yapılandırmanız gerekir. Azure DNS'de etki alanlarınızı barındırabilir. Azure DNS yük dengeleyici ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure DNS diğer Azure hizmetleriyle](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Sonraki adımlar
- Yük Dengeleme Azure hizmetlerinde birleştirme hakkında daha fazla bilgi edinin [Azure'da Yük Dengeleme hizmetlerini kullanarak](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Günlükleri farklı türde Azure'da yönetmek ve yük dengeleyici sorunlarını gidermek için nasıl kullanabileceğinizi öğrenin [analytics Azure yük dengeleyici için oturum](../load-balancer/load-balancer-monitor-log.md).
