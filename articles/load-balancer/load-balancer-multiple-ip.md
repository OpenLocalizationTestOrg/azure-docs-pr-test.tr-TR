---
title: "birden çok IP yapılandırmaları Azure Dengeleme aaaLoad | Microsoft Docs"
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
ms.openlocfilehash: 8619493b8102e9d158d428fe6c59ecf3f32edc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-hello-azure-portal"></a>Yük Dengeleme Hello Azure portal kullanarak birden çok IP yapılandırmaları hakkında

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

Bu makalede, nasıl bir ikincil ağ arabirimi (NIC) toouse Azure yük dengeleyici ile birden çok IP adresleri açıklanmaktadır. Bu senaryo için Windows, her birincil ve ikincil bir NIC ile çalışan iki VM sahibiz Her ikincil hello NIC'lerin iki IP yapılandırmaları vardır. Her VM Web siteleri contoso.com ve fabrikam.com barındırır. İlişkili tooone hello IP yapılandırmalarının hello ikincil NIC üzerinde her Web sitesi olan Azure yük dengeleyici tooexpose iki ön uç IP adresi, her bir Web sitesi, toodistribute trafiği toohello ilgili IP hello Web sitesinin yapılandırması için bir tane kullanırız. Bu senaryoda hem ön uçlar yanı sıra arasında her iki arka uç havuzu IP adreslerini hello aynı bağlantı noktası numarası kullanır.

![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a>Ön koşullar
Bu örnek, adlı bir kaynak grubu sahibi olduğunuzu varsayar *contosofabrikam* yapılandırma aşağıdaki hello ile:
 -  adlı bir sanal ağ içerir *myVNet*, iki VM adlı *VM1* ve *VM2* sırasıyla içinde hello aynı kullanılabilirlik adlandırılmış kümesi *myAvailset*. 
 - Her VM birincil NIC ve ikincil bir NIC'e sahip. Merhaba birincil NIC adlandırıldığı *VM1NIC1* ve *VM2NIC1* ve hello ikincil NIC'ler adlandırıldığı *VM1NIC2* ve *VM2NIC2*. Birden çok NIC VM'ler oluşturma hakkında daha fazla bilgi için bkz: [ile birden çok NIC PowerShell kullanarak bir VM oluşturma](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a>Adımları tooload bakiyesi birden fazla IP yapılandırması

Bu makalede açıklanan tooachieve hello senaryo aşağıdaki adımları izleyin:

### <a name="step-1-configure-hello-secondary-nics-for-each-vm"></a>1. adım: Yapılandırma her VM için ikincil NIC'ler hello

Her bir VM sanal ağınızda eklemek için IP yapılandırmasını ikincil NIC gibi hello:  

1. Tarayıcıdan toohello Azure portalına gidin: http://portal.azure.com ve Azure hesabınızda oturum açın.
2. Merhaba üst sol tarafındaki Merhaba ekranında, hello kaynak grubu simgesine tıklayın ve ardından hello kaynak grubu hello VM'ler içinde bulunur (örneğin, *contosofabrikam*). Merhaba **kaynak grupları** hello VM'ler için hello ağ arabirimleri ile birlikte tüm hello kaynakları listeler dikey şimdi görüntülenir.
3. toohello ikincil her VM NIC IP yapılandırmasını aşağıdaki gibi ekleyin:
    1. Tooadd hello IP yapılandırması için istediğiniz hello ağ arabirimi seçin.
    2. Görüntülenen hello dikey penceresinde hello Seçtiğiniz NIC için tıklayın **IP yapılandırmaları**. Ardından **Ekle** görüntülenir hello dikey penceresinde hello üstündeki bulunun.
    3. Merhaba, **eklemek IP yapılandırmaları** dikey penceresinde, ikinci bir IP yapılandırması toohello NIC aşağıdaki şekilde ekleyin: 
        1. İkincil IP yapılandırması için bir ad yazın (örneğin, VM1 ve VM2 IP yapılandırmaları olarak hello adı için *VM1NIC2 ipconfig2* ve *VM2NIC2 ipconfig2* sırasıyla).
        2. İçin **özel IP adresi**, için **ayırma**seçin **statik**.
        3. **Tamam** düğmesine tıklayın.
        4. Merhaba Hello ikinci IP yapılandırmasını ikincil NIC tamamlandığında hello görüntülenir **IP yapılandırmaları** NIC verilen hello için ayarlar dikey penceresi

### <a name="step-2-create-a-load-balancer"></a>2. adım: bir yük dengeleyici oluşturma

Bir yük dengeleyici gibi oluşturun:

1. Tarayıcıdan toohello Azure portalına gidin: http://portal.azure.com ve Azure hesabınızda oturum açın.
2. Merhaba üst sol tarafında hello ekran'ı tıklatın **yeni** > **ağ** > **yük dengeleyici**. Bundan sonra öğesini **oluşturma**.
3. Merhaba, **oluşturma yük dengeleyici** dikey penceresinde, yük dengeleyici için bir ad yazın. Burada adlı *mylb*.
4. Ortak IP adresi altında adlı yeni bir genel IP oluşturun **PublicIP1**.
5. Kaynak grubu altında seçin, VM'lerin olan bir kaynak grubunu hello (örneğin, *contosofabrikam*). Ardından, uygun bir konum seçin ve ardından **Tamam**. Merhaba yük dengeleyici toodeploy sonra başlar ve toosuccessfully tam dağıtım birkaç dakika sürer.
6. Uygulama dağıtıldıktan sonra hello yük dengeleyici bir kaynak, kaynak grubu olarak görüntülenir.

### <a name="step-3-configure-hello-frontend-ip-pool"></a>3. adım: hello ön uç IP havuzu yapılandırma

Her Web sitesi (Contoso ve Fabrikam) için ön uç IP havuzu aşağıdaki gibi yapılandırın:

1. Merhaba Portalı'nda tıklatın **daha fazla hizmet** > türü **genel IP adresi** hello filtre kutusuna ve ardından **ortak IP adresleri**. Tıklatın **Ekle** görüntülenir hello dikey penceresinde hello üstündeki bulunun.
2. İki ortak IP adreslerini yapılandırın (*PublicIP1* ve *PublicIP2*) aşağıdaki gibi iki Web sitesi (contoso ve fabrikam) için:
    1. Ön uç IP adresi için bir ad yazın.
    2. İçin **kaynak grubu**, hello hello VM'ler, varolan bir kaynak grubu seçin (örneğin, *contosofabrikam*).
    3. İçin **konumu**, VM'ler hello gibi hello aynı konuma seçin.
    4. **Tamam** düğmesine tıklayın.
    5. Merhaba iki genel IP adresleri oluşturulduktan sonra her ikisi de hello görüntülendikleri **genel IP** adresleri dikey.
3. Merhaba Portalı'nda tıklatın **daha fazla hizmet** > türü **yük dengeleyici** hello filtre kutusuna ve ardından **yük dengeleyici**.  
4. Merhaba yük dengeleyici seçin (*mylb*) tooadd hello ön uç IP havuzuna istiyor.
5. Altında **ayarları**seçin **ön uç havuzları**. Ardından **Ekle** görüntülenir hello dikey penceresinde hello üstündeki bulunun.
6. Ön uç IP adresi için bir ad yazın (*farbikamfe* veya **contosofe*).
7. Tıklatın **IP adresi** ve hello **seçin genel IP adresi** dikey penceresinde, select hello IP adresleri, ön uç için (*PublicIP1* veya *PublicIP2*).
8. Bu bölümde toocreate hello ikinci ön uç IP adresi içindeki adımları 3 too7 yineleyin.
9. Merhaba ön uç IP havuzu yapılandırması tamamlandığında, hem ön uç IP adreslerini hello görüntülenen **ön uç IP havuzu** dikey penceresinde, yük dengeleyicinin. 
    
### <a name="step-4-configure-hello-backend-pool"></a>4. adım: hello arka uç havuzunu yapılandırma   
Merhaba arka uç adres havuzu, yük dengeleyici (Contoso ve Fabrikam) her Web sitesi için aşağıdaki gibi yapılandırın:
        
1. Merhaba Portalı'nda tıklatın **daha fazla hizmet** > Yük Dengeleyici hello filtre kutusuna yazın ve ardından **yük dengeleyici**.  
2. Merhaba yük dengeleyici seçin (*mylb*) tooadd hello arka uç havuzları istiyor.
3. Altında **ayarları**seçin **arka uç havuzları**. Arka uç havuzu için bir ad yazın (örneğin, *contosopool* veya *fabrikampool*). Merhaba ardından **Ekle** düğmesi görüntülenir hello dikey penceresinde hello üstündeki bulunun. 
4. İçin **ilişkili**seçin **kullanılabilirlik kümesi**.
5. İçin **kullanılabilirlik kümesi**seçin **myAvailset**.
6. Her iki VM için hedef ağ IP yapılandırmaları (bkz: Şekil 2) aşağıdaki şekilde ekleyin:  
    1. İçin **hedef sanal makine**, hello tooadd toohello arka uç havuzu (örneğin, VM1 veya VM2) istediğiniz VM seçin.
    2. İçin **ağ IP yapılandırması**seçin (örneğin, VM1NIC2 ipconfig2 veya VM2NIC2 ipconfig2) bu VM için hello ikincil NIC IP yapılandırması.
    ![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-backendpool.PNG)
            
        **Şekil 2**: hello yük dengeleyici arka uç havuzları ile yapılandırma  
7. **Tamam** düğmesine tıklayın.
8. Merhaba arka uç havuzu yapılandırması tamamlandığında, her iki arka uç adres havuzlarında hello görüntülenen **arka uç havuzu dikey** , yük dengeleyicinin.

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a>Adım 5: sistem durumu araştırması, yük dengeleyici için yapılandırma
Yük Dengeleyici için bir sistem durumu araştırma aşağıdaki gibi yapılandırın:
    1. Daha fazla hizmet Hello Portalı'nda tıklatın > Yük Dengeleyici hello filtre kutusuna yazın ve ardından **yük dengeleyici**.  
    2. Tooadd hello arka uç havuzları istediğiniz hello yük dengeleyici seçin.
    3. Altında **ayarları**seçin **durumu araştırması**. Ardından **Ekle** görüntülenir hello dikey penceresinde hello üstündeki bulunun.
    4. Merhaba durumu araştırması (örneğin, HTTP) için bir ad yazın ve'ı tıklatın **Tamam**.

### <a name="step-6-configure-load-balancing-rules"></a>6. adım: Yük Dengeleme kuralları yapılandırma
Yük Dengeleme kuralları yapılandırın (*HTTPc* ve *HTTPf*) aşağıdaki gibi her Web sitesi için:
    
1. Altında **ayarları**seçin **durumu araştırması**. Ardından **Ekle** görüntülenir hello dikey penceresinde hello üstündeki bulunun.
2. İçin **adı**, hello Yük Dengeleme kuralı için bir ad yazın (örneğin, *HTTPc* contoso, veya *HTTPf* Fabrikam için)
3. Ön uç IP adresi için hello hello ön uç IP adresini seçin (örneğin *Contosofe* veya *Fabrikamfe*)
4. İçin **bağlantı noktası** ve **arka uç bağlantı noktası**, hello varsayılan değeri tutmak **80**.
5. İçin **kayan IP (doğrudan sunucu dönüşü)**, tıklatın **etkin**.
6. **Tamam** düğmesine tıklayın.
7. Bu bölümde toocreate hello ikinci yük dengeleyici kuralı içinde adımları 1 too6 yineleyin.
8. Ne zaman Yapılandırma tamamlandığında hello Yük Dengeleme kuralları, hem kuralları ((*HTTPc* ve *HTTPf*) hello görüntülenen **Yük Dengeleme kuralları** dikey penceresinde, yük dengeleyicinin.

### <a name="step-7-configure-dns-records"></a>7. adım: DNS kayıtlarını Yapılandır
Son olarak, DNS kaynak kayıtlarını toopoint toohello ilgili ön uç IP adresi hello yük dengeleyici yapılandırmanız gerekir. Azure DNS'de etki alanlarınızı barındırabilir. Azure DNS yük dengeleyici ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure DNS diğer Azure hizmetleriyle](../dns/dns-for-azure-services.md).

## <a name="next-steps"></a>Sonraki adımlar
- Nasıl toocombine Yük Dengeleme Azure hizmetleri hakkında daha fazla bilgi [Azure'da Yük Dengeleme hizmetlerini kullanarak](../traffic-manager/traffic-manager-load-balancing-azure.md).
- Nasıl günlükleri farklı türlerde içinde Azure toomanage kullanın ve yük dengeleyici sorun giderme öğrenin [analytics Azure yük dengeleyici için oturum](../load-balancer/load-balancer-monitor-log.md).
