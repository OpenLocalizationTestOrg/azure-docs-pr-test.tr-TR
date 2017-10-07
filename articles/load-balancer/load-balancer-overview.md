---
title: "aaaAzure yük dengeleyici genel bakış | Microsoft Docs"
description: "Azure yük dengeleyici özellikleri, mimari ve uygulama genel bakış. Merhaba yük dengeleyici nasıl çalıştığını öğrenin ve hello bulutta yararlanın."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
ms.assetid: 0f313dc0-f007-4cee-b2b9-f542357925a3
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2376a02f7cbbbed6a90f216419c0c3d30f594272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-load-balancer-overview"></a>Azure Load Balancer’a genel bakış

Azure yük dengeleyici tooyour uygulamaları yüksek kullanılabilirlik ve ağ performansı sunar. Gelen trafiği yükü dengelenmiş bir kümede tanımlanmış Hizmetleri sağlıklı örnekleri arasında dağıtır bir katman 4 (TCP, UDP) yük dengeleyici olur.

Azure yük dengeleyici için yapılandırılabilir:

* Gelen Internet trafiği toovirtual makinelerin yük dengelemesini. Bu yapılandırma olarak bilinir [Internet'e yönelik Yük Dengeleme](load-balancer-internet-overview.md).
* Yük Dengeleme trafiği sanal ağ içindeki sanal makineler arasında bulut Hizmetleri içindeki sanal makineler arasında veya şirket içi bilgisayarlar ve bir şirket içi sanal ağdaki sanal makineler arasında. Bu yapılandırma olarak bilinir [iç Yük Dengeleme](load-balancer-internal-overview.md).
* Dış trafiğin tooa belirli bir sanal makine iletin.

Merhaba buluttaki tüm kaynaklara bir ortak IP adresi toobe hello Internet erişilebildiğini gerekir. azure'da Hello bulut altyapısı için kaynaklarını yönlendirilebilir olmayan IP adreslerini kullanır. Azure ortak IP adresleri toocommunicate toohello ile Internet ağ adresi çevirisi (NAT) kullanır.

## <a name="azure-deployment-models"></a>Azure dağıtım modelleri

Önemli toounderstand hello farklarını hello Azure Klasik ve Resource Manager olan [dağıtım modellerini](../azure-resource-manager/resource-manager-deployment-model.md). Azure yük dengeleyici farklı her modelinde yapılandırılır.

### <a name="azure-classic-deployment-model"></a>Azure Klasik dağıtım modeli

Bir bulut hizmeti sınırı içinde dağıtılan sanal makineleri gruplandırılmış toouse bir yük dengeleyici olabilir. Bu genel bir IP adresi model ve tooa bulut hizmeti, bir tam etki alanı adı (FQDN) atanır. Merhaba yük dengeleyici çeviri bağlantı noktası ve hello bulut hizmeti için hello ortak IP adresini kullanarak yük hello ağ trafiği dengeler.

Yükü dengelenmiş trafiği uç noktaları tarafından tanımlanır. Bağlantı noktası çevirisi uç noktaları hello ortak atanan bağlantı noktası hello genel IP adresi ve toohello hizmeti belirli bir sanal makineye atanan hello yerel bağlantı noktası arasında bire bir ilişki var. Yük Dengeleme uç noktaları hello sanal makineleri hello bulut hizmetindeki hello genel IP adresi hello atanan yerel bağlantı noktaları toohello hizmetleri arasında bir-çok ilişkisi vardır.

![Merhaba Klasik dağıtım modelinde Azure yük dengeleyici](./media/load-balancer-overview/asm-lb.png)

Şekil 1 - hello Klasik dağıtım modelinde Azure yük dengeleyici

Merhaba etki alanı etiketi, bu dağıtım modeli için yük dengeleyici kullanan hello hello ortak IP adresi için \<bulut hizmeti adı\>. cloudapp.net. Merhaba aşağıdaki grafikte hello Azure yük dengeleyici Bu modelde gösterir.

### <a name="azure-resource-manager-deployment-model"></a>Azure Resource Manager dağıtım modeli

Merhaba Resource Manager dağıtım modelinde bir bulut hizmeti hiçbir gerek toocreate yoktur. Merhaba yük dengeleyici tooexplicitly birden çok sanal makineler arasında trafiği yönlendirme oluşturulur.

Bir ortak IP adresi bir etki alanı etiketi (DNS adı) sahip tek bir kaynaktır. Merhaba ortak IP adresi hello yük dengeleyici kaynağıyla ilişkili değil. Merhaba genel IP adresi, yük dengeli ağ trafiği alma hello kaynaklar için Internet endpoint hello olarak yük dengeleyici kuralları ve gelen NAT kuralları kullanın.

Toohello ağ arabirimi bağlı kaynak tooa sanal makineyi bir özel veya genel IP adresi atanır. Bir ağ arabirimi tooa yük dengeleyicinin arka uç IP adresi havuzu eklendikten sonra hello yük dengeleyici oluşturulan hello yük dengeli kurallara göre mümkün toosend yük dengeli ağ trafiğidir.

Merhaba aşağıdaki grafikte hello Azure yük dengeleyici Bu modelde gösterir:

![Azure yük dengeleyici Kaynak Yöneticisi'nde](./media/load-balancer-overview/arm-lb.png)

Şekil 2 - Azure yük dengeleyici Kaynak Yöneticisi'nde

Merhaba yük dengeleyici, Resource Manager tabanlı şablonlar, API ve araçları yönetilebilir. toolearn daha fazla kaynak yöneticisi hakkında bkz: Merhaba [Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Yük Dengeleyici özelliği

* Karma tabanlı dağıtım

    Azure yük dengeleyici bir karma tabanlı dağıtım algoritması kullanır. Varsayılan olarak, kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası ve protokol türü toomap trafiği tooavailable sunucuları oluşan bir 5 bölütlü karma kullanır. Yalnızca sürekliliği sağlar *içinde* bir aktarım oturumu. Aynı TCP veya UDP oturum olacak hello paketlerinde aynı hello yük dengeli uç nokta örnek toohello yönlendirilmiş. Merhaba istemci kapatır ve hello bağlantı açana veya yeni bir oturumdan başlatıldığında, aynı kaynak IP, hello kaynak bağlantı noktası değişikliklerini hello. Bu, farklı bir veri merkezinde hello trafiği toogo tooa farklı endpoint neden olabilir.

    Daha fazla ayrıntı için bkz: [yük dengeleyici dağıtım modu](load-balancer-distribution-mode.md). Merhaba aşağıdaki grafikte hello karma tabanlı dağılımını gösterir:

    ![Karma tabanlı dağıtım](./media/load-balancer-overview/load-balancer-distribution.png)

    Şekil 3 - karma tabanlı dağıtım

* Bağlantı noktası iletme

    Nasıl gelen iletişimi yönetilen denetim azure yük dengeleyici sağlar. Bu iletişim Internet konakları, sanal makineler diğer bulut Hizmetleri ya da sanal ağlar başlatılan trafiği içerir. Bu denetim (bir giriş uç noktası olarak da bilinir) bir uç nokta temsil edilir.

    Bir giriş uç noktası ortak bir bağlantı noktasını dinler ve tooan dahili bağlantı noktası trafiği iletir. Aynı iç veya dış uç noktası için bağlantı noktalarını hello harita veya farklı bir bağlantı noktası için kullanın. Örneğin, Hello ortak uç nokta eşleme bağlantı noktası 80 olsa da, bir web sunucusu yapılandırılmış toolisten tooport 81 olabilir. Genel bir uç nokta Hello oluşturulmasını bir yük dengeleyici örneği hello oluşturulmasını tetikler.

    Oluşturulan kullanarak Merhaba, Azure portal hello portal uç noktaları toohello sanal makine hello Uzak Masaüstü Protokolü (RDP) için ve uzaktan Windows PowerShell oturumu trafiği otomatik olarak oluşturur. Bu uç noktalar kullanabilirsiniz tooremotely hello Internet hello sanal makine yönetme.

* Otomatik yeniden yapılandırma

    Yukarı veya aşağı örnekleri ölçeklendirdiğinizde azure yük dengeleyici anında kendisini yeniden yapılandırır. Örneğin, artırdığınızda, bu yeniden yapılandırma örnek sayısı için bir bulut hizmeti web/çalışan rollerinde hello veya hello içinde ek sanal makineler eklediğinizde, aynı yük dengeli kümesi olur.

* Hizmet izleme

    Azure yük dengeleyici hello hello durumunu çeşitli sunucu örnekleri araştırma. Bir araştırma toorespond başarısız olduğunda, yeni bağlantılar toohello sağlıksız örnekleri gönderme hello yük dengeleyici durdurur. Var olan bağlantıların etkilenmez.

    Üç tür araştırmalar desteklenir:

    + **Konuk Aracısı araştırma (olarak bir hizmet yalnızca sanal makineler platformunda):** hello yük dengeleyici hello Konuk Aracısı hello sanal makine içinde kullanır. Merhaba Konuk Aracısı dinler ve bir HTTP 200 Tamam Yanıtla yalnızca hello zaman örneğidir hello hazır durumda yanıt verir (yani hello örnek geri dönüştürülüyor veya durduruluyor meşgul gibi bir durumda değil). Bir HTTP 200 Tamam toorespond Hello Aracısı başarısız olursa, hello yük dengeleyici işaretleri örneği yanıt olarak ve trafik toothat örneği gönderme durduğunda hello. Merhaba yük dengeleyici tooping hello örneği devam eder. Bir HTTP 200 ile Merhaba Konuk aracısı yanıt verirse, hello yük dengeleyici trafiği toothat örneği yeniden gönderin. Web rolü kullanırken, Web sitesi kodunuz hello Azure dokusunu veya konuk aracısı tarafından izlenmeyen w3wp.exe genellikle çalışır. Bu w3wp.exe (örneğin HTTP 500 yanıtları)'de hataları bildirilen toohello Konuk Aracısı olmaz ve hello yük dengeleyici tootake döndürme dışında bu örneği bilmediği anlamına gelir.
    + **HTTP özel araştırma:** Bu araştırma hello varsayılan (konuk Aracısı) araştırma geçersiz kılar. Toocreate kullanmak, kendi özel mantık toodetermine hello sistem durumunu hello rol örneği. Merhaba yük dengeleyici uç noktanızı (15 dakikada, varsayılan olarak) düzenli olarak araştırma. bir TCP ACK veya HTTP 200 hello zaman aşımı süresi (varsayılan 31 saniye) içinde yanıt verirse hello örneği döndürme toobe olarak kabul edilir. Bu, kendi hello yük dengeleyicinin döndürme mantığı tooremove örneklerden uygulamak için kullanışlıdır. Örneğin, % 90 CPU Hello örneğiyse, hello örneği tooreturn 200 olmayan durum yapılandırabilirsiniz. W3wp.exe kullanan web rolleri için aynı zamanda otomatik alırsınız, Web sitesi Web sitesi kodunuzdaki hataları 200 olmayan durum toohello araştırması dönüş beri izleme.
    + **TCP özel araştırma:** Bu araştırma başarılı oturum kurma tanımlanan tooa araştırma numaralı TCP bağlantı noktasını kullanır.

    Daha fazla bilgi için bkz: Merhaba [LoadBalancerProbe şema](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* Kaynak NAT

    Hizmetinizden kaynaklandığı Internet uğradığında tüm giden trafiği toohello kaynak NAT (SNAT) kullanarak gelen trafiği hello gibi hello aynı VIP adresi. SNAT önemli avantajları sağlar:

    + VIP dinamik olarak olabilir hello hello hizmeti tooanother örneği eşlenmiş olduğundan, hizmetlerin kolay yükseltme ve olağanüstü durum kurtarma etkinleştirir.
    + Erişim denetimi listesi (ACL) yönetimini kolaylaştırır. VIP'ler bakımından ifade ACL Hizmetleri ölçek büyütme, olarak aşağı değiştirmeyin veya imzalanmasını.

    Merhaba yük dengeleyici yapılandırması için UDP tam koni NAT destekler. Tam koni NAT hello bağlantı noktası gelen bağlantıları herhangi bir dış ana bilgisayardan (yanıt tooan giden istekte) burada sağlar NAT türüdür.

    Bir sanal makine başlatan her yeni giden bağlantı için giden bağlantı noktası da hello yük dengeleyici tarafından ayrılmış. Merhaba dış konak trafiği bir sanal IP VIP tahsis edilen bağlantı noktasıyla görür. Çok sayıda giden bağlantılar gerektiren senaryolar için toouse önerilir [örnek düzeyinde ortak IP](../virtual-network/virtual-networks-instance-level-public-ip.md) hello VM'ler ayrılmış giden bir IP adresi için SNAT böylece giderir. Bu bağlantı noktası Tükenme hello riskini azaltır.

    Lütfen bakın [giden bağlantılar](load-balancer-outbound-connections.md) Bu konu hakkında daha fazla ayrıntı için makale.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Sanal makineler için birden çok yük dengeli IP adresleri için destek
Birden fazla yük dengeli ortak IP adresi tooa sanal makineler kümesi atayabilirsiniz. Bu özelliği sayesinde, birden çok SSL Web sitelerine ve/veya hello aynı sanal makinelerin kümesi üzerinde birden çok SQL Server AlwaysOn Kullanılabilirlik grubu dinleyicileri barındırabilir. Daha fazla bilgi için bkz: [bulut hizmeti başına birden çok Vip](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Sınırlamalar

Yük Dengeleyici arka uç havuzları temel katmana dışındaki tüm VM SKU içerebilir.

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [Internet'e yönelik Yük Dengeleyici](load-balancer-internet-overview.md)

- Daha fazla bilgi edinmek [iç yük dengeleyiciye genel bakış](load-balancer-internal-overview.md)

- Oluşturma bir [Internet'e yönelik Yük Dengeleyici](load-balancer-get-started-internet-portal.md)

- Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure

