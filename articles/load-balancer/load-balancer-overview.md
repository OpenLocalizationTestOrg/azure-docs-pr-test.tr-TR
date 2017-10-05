---
title: "Azure yük dengeleyici genel bakış | Microsoft Docs"
description: "Azure yük dengeleyici özellikleri, mimari ve uygulama genel bakış. Yük Dengeleyici nasıl çalıştığını öğrenin ve bulutta yararlanın."
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
ms.openlocfilehash: 617da1cf41db08d319d6fe9fa7bc96b794a0001e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-load-balancer-overview"></a>Azure Load Balancer’a genel bakış

Azure Load Balancer, uygulamalarınıza yüksek düzeyde kullanılabilirlik ve ağ performansı sağlar. Gelen trafiği yükü dengelenmiş bir kümede tanımlanmış Hizmetleri sağlıklı örnekleri arasında dağıtır bir katman 4 (TCP, UDP) yük dengeleyici olur.

Azure yük dengeleyici için yapılandırılabilir:

* Gelen Internet trafiği dengelemek için sanal makineler yükleyin. Bu yapılandırma olarak bilinir [Internet'e yönelik Yük Dengeleme](load-balancer-internet-overview.md).
* Yük Dengeleme trafiği sanal ağ içindeki sanal makineler arasında bulut Hizmetleri içindeki sanal makineler arasında veya şirket içi bilgisayarlar ve bir şirket içi sanal ağdaki sanal makineler arasında. Bu yapılandırma olarak bilinir [iç Yük Dengeleme](load-balancer-internal-overview.md).
* Belirli bir sanal makine için dış trafiğin iletin.

Buluttaki tüm kaynaklara Internet'ten erişilebilir olması için bir ortak IP adresi gerekir. Azure bulut altyapısında kaynaklarını için yönlendirilebilir olmayan IP adreslerini kullanır. Azure Internet ile iletişim kurmak için ortak IP adresi ile ağ adresi çevirisi (NAT) kullanır.

## <a name="azure-deployment-models"></a>Azure dağıtım modelleri

Azure Klasik ve Resource Manager arasındaki farkları anlamak önemlidir [dağıtım modellerini](../azure-resource-manager/resource-manager-deployment-model.md). Azure yük dengeleyici farklı her modelinde yapılandırılır.

### <a name="azure-classic-deployment-model"></a>Azure Klasik dağıtım modeli

Bir yük dengeleyici kullanmak için bir bulut hizmeti sınırı içinde dağıtılan sanal makineleri gruplandırılabilir. Bu genel bir IP adresi model ve bir bulut hizmeti, bir tam etki alanı adı (FQDN) atanır. Yük Dengeleyici çeviri bağlantı noktası ve bulut hizmeti için genel IP adresini kullanarak ağ trafiğinin yükünü dengeleyen.

Yükü dengelenmiş trafiği uç noktaları tarafından tanımlanır. Bağlantı noktası çevirisi uç genel IP adresi genel atanan bağlantı noktasını ve belirli bir sanal makine hizmetine atanan yerel bağlantı noktası arasında bire bir ilişki var. Yük Dengeleme uç genel IP adresi ve Hizmetleri bulut hizmetindeki sanal makinelere atanan yerel bağlantı noktaları arasında bir-çok ilişkisi vardır.

![Klasik dağıtım modelinde Azure yük dengeleyici](./media/load-balancer-overview/asm-lb.png)

Şekil 1 - Klasik dağıtım modelinde Azure yük dengeleyici

Bu dağıtım modeli için yük dengeleyici kullanan ortak IP adresi için etki alanı etiketi \<bulut hizmeti adı\>. cloudapp.net. Aşağıdaki grafikte Azure yük dengeleyici Bu modelde gösterir.

### <a name="azure-resource-manager-deployment-model"></a>Azure Resource Manager dağıtım modeli

Resource Manager dağıtım modelinde bir bulut hizmeti oluşturmak için gerek yoktur. Yük Dengeleyici açıkça birden çok sanal makineler arasında trafiği yönlendirmek için oluşturulur.

Bir ortak IP adresi bir etki alanı etiketi (DNS adı) sahip tek bir kaynaktır. Ortak IP adresi yük dengeleyici kaynağıyla ilişkili değil. Yük Dengeleyici kuralları ve gelen NAT kuralları genel IP adresi için yük dengeli ağ trafiği alma kaynakları Internet uç noktası olarak kullanın.

Bir özel veya genel IP adresi, bir sanal makineye bağlı ağ arabirimi kaynağına atanır. Bir ağ arabirimi yük dengeleyicinin arka uç IP adresi havuzuna eklendikten sonra Yük Dengeleyici yük dengeli kurallarına göre oluşturulan yük dengeli ağ trafiğinin gönderebilir.

Aşağıdaki grafikte Azure yük dengeleyici Bu modelde gösterir:

![Azure yük dengeleyici Kaynak Yöneticisi'nde](./media/load-balancer-overview/arm-lb.png)

Şekil 2 - Azure yük dengeleyici Kaynak Yöneticisi'nde

Yük Dengeleyici, Resource Manager tabanlı şablonlar, API ve araçları yönetilebilir. Kaynak Yöneticisi hakkında daha fazla bilgi edinmek için [Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).

## <a name="load-balancer-features"></a>Yük Dengeleyici özelliği

* Karma tabanlı dağıtım

    Azure yük dengeleyici bir karma tabanlı dağıtım algoritması kullanır. Varsayılan olarak, trafiği kullanılabilir sunuculara eşlemek için kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası ve protokol türü oluşan bir 5 bölütlü karma kullanır. Yalnızca sürekliliği sağlar *içinde* bir aktarım oturumu. Yük dengeli uç nokta arkasındaki aynı örneğini paketleri aynı TCP veya UDP oturumda yönlendirilir. İstemci kapatır ve bağlantı açana veya aynı kaynak IP yeni bir oturum başlatıldığında, kaynak bağlantı noktası değiştirir. Bu, farklı bir uç noktası farklı bir veri merkezinde gitmek trafiği neden olabilir.

    Daha fazla ayrıntı için bkz: [yük dengeleyici dağıtım modu](load-balancer-distribution-mode.md). Aşağıdaki grafikte karma tabanlı dağılımını gösterir:

    ![Karma tabanlı dağıtım](./media/load-balancer-overview/load-balancer-distribution.png)

    Şekil 3 - karma tabanlı dağıtım

* Bağlantı noktası iletme

    Nasıl gelen iletişimi yönetilen denetim azure yük dengeleyici sağlar. Bu iletişim Internet konakları, sanal makineler diğer bulut Hizmetleri ya da sanal ağlar başlatılan trafiği içerir. Bu denetim (bir giriş uç noktası olarak da bilinir) bir uç nokta temsil edilir.

    Bir giriş uç noktası ortak bir bağlantı noktasını dinler ve dahili bir bağlantı noktası trafiğini iletir. Bir iç veya dış uç noktası için aynı bağlantı noktalarını eşleştirmek veya farklı bir bağlantı noktası için bunları kullanın. Örneğin, bağlantı noktası 80 olsa da genel bir uç nokta eşleme bağlantı noktası 81 dinlemek üzere yapılandırılmış bir web sunucusu olabilir. Genel bir uç nokta oluşturulması, bir yük dengeleyici örneği oluşturulmasını tetikler.

    Azure portalını kullanarak oluşturduğunuz zaman, portal Uzak Masaüstü Protokolü (RDP) ve uzak Windows PowerShell oturumu trafik için otomatik olarak uç noktaları sanal makine oluşturur. Bu uç noktalar, sanal makine Internet üzerinden uzaktan yönetmek için kullanabilirsiniz.

* Otomatik yeniden yapılandırma

    Yukarı veya aşağı örnekleri ölçeklendirdiğinizde azure yük dengeleyici anında kendisini yeniden yapılandırır. Örneğin, bir bulut hizmeti web/çalışan rolleri için örnek sayısı artırdığınızda veya aynı yük dengeli kümesi olarak ek sanal makineler eklediğinizde, bu yeniden yapılandırma olur.

* Hizmet izleme

    Azure yük dengeleyici çeşitli sunucu örneklerinin sistem durumu araştırması. Yanıt bir araştırma başarısız olduğunda, yük dengeleyici sağlıksız örneklerine yeni bağlantılar gönderme durdurur. Var olan bağlantıların etkilenmez.

    Üç tür araştırmalar desteklenir:

    + **Konuk Aracısı araştırma (olarak bir hizmet yalnızca sanal makineler platformunda):** yük dengeleyici sanal makine içinde Konuk Aracısı'nı kullanır. Konuk Aracısı dinler ve örneği (yani örnek geri dönüştürülüyor veya durduruluyor meşgul gibi bir durumda değil) hazır durumda olduğunda yalnızca bir HTTP 200 Tamam yanıt ile yanıt verir. Aracı bir HTTP 200 Tamam ile yanıt vermiyorsa, yük dengeleyici örneği yanıt olarak işaretler ve trafiği için bu örneği göndermeye durdurur. Yük Dengeleyici örneği ping işlemi devam eder. Bir HTTP 200 ile Konuk aracısı yanıt verirse, yük dengeleyici trafiği için bu örneği yeniden gönderir. Web rolü kullanırken, Web sitesi kodunuz genellikle Azure tarafından izlenmeyen w3wp.exe çalışan doku veya konuk Aracısı. Bu hatalar w3wp.exe (örneğin HTTP 500 yanıtları) Konuk aracıya raporlanmayacaktır ve yük dengeleyici döndürme dışında bu örneği yapılacak anlayamazsınız anlamına gelir.
    + **HTTP özel araştırma:** Bu araştırma varsayılan (konuk Aracısı) araştırma geçersiz kılar. Rol örneğinin sistem durumunu belirlemek için kendi özel mantık oluşturmak için kullanabilirsiniz. Yük Dengeleyici uç noktanızı (15 dakikada, varsayılan olarak) düzenli olarak araştırma. Örnek bir ACK TCP veya HTTP 200 (varsayılan 31 saniye cinsinden) zaman aşımı süresi içinde yanıt verirse dönüş olarak kabul edilir. Bu, yük dengeleyicinin döndürme örneklerini kaldırmak için kendi mantığı uygulamak için kullanışlıdır. Örneğin, % 90 CPU örneğiyse 200 olmayan durumuna döndürmek için örnek yapılandırabilirsiniz. W3wp.exe kullanan web rolleri için aynı zamanda otomatik alırsınız, Web sitesini, Web sitesi kodunuzdaki hataları dönüş 200 olmayan durumu araştırması için bu yana izleme.
    + **TCP özel araştırma:** tanımlanan araştırma bağlantı noktasına başarılı TCP oturumu oluşturulması bu araştırma dayanır.

    Daha fazla bilgi için bkz: [LoadBalancerProbe şema](https://msdn.microsoft.com/library/azure/jj151530.aspx).

* Kaynak NAT

    Tüm giden trafiği hizmetinizden kaynaklandığı internet gelen trafiği aynı VIP adresi kullanarak kaynak NAT (SNAT) uğradığında. SNAT önemli avantajları sağlar:

    + VIP başka bir hizmet örneği için dinamik olarak eşlenebilir olduğundan, hizmetlerin kolay yükseltme ve olağanüstü durum kurtarma etkinleştirir.
    + Erişim denetimi listesi (ACL) yönetimini kolaylaştırır. VIP'ler bakımından ifade ACL Hizmetleri ölçek büyütme, olarak aşağı değiştirmeyin veya imzalanmasını.

    Yük Dengeleyici yapılandırması için UDP tam koni NAT destekler. Tam koni NAT burada bağlantı noktası (yanıtta bir giden talep) herhangi bir dış ana bilgisayardan gelen bağlantıları sağlar NAT türüdür.

    Bir sanal makine başlatan her yeni giden bağlantı için giden bağlantı noktası da yük dengeleyici tarafından ayrılmış. Dış konak trafiği bir sanal IP VIP tahsis edilen bağlantı noktasıyla görür. Kullanmak için önerilen çok sayıda giden bağlantılar gerektiren senaryolar için [örnek düzeyinde ortak IP](../virtual-network/virtual-networks-instance-level-public-ip.md) VM'ler ayrılmış giden bir IP adresi için SNAT böylece giderir. Bu bağlantı noktası tükenmesi riskini azaltır.

    Lütfen bakın [giden bağlantılar](load-balancer-outbound-connections.md) Bu konu hakkında daha fazla ayrıntı için makale.

### <a name="support-for-multiple-load-balanced-ip-addresses-for-virtual-machines"></a>Sanal makineler için birden çok yük dengeli IP adresleri için destek
Sanal makineler kümesi için birden fazla yük dengeli genel IP adresi atayabilirsiniz. Bu özelliği sayesinde, birden çok SSL Web sitelerine ve/veya sanal makineleri aynı kümesi üzerinde birden çok SQL Server AlwaysOn Kullanılabilirlik grubu dinleyicileri barındırabilir. Daha fazla bilgi için bkz: [bulut hizmeti başına birden çok Vip](load-balancer-multivip.md).

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="limitations"></a>Sınırlamalar

Yük Dengeleyici arka uç havuzları temel katmana dışındaki tüm VM SKU içerebilir.

## <a name="next-steps"></a>Sonraki adımlar

- Daha fazla bilgi edinmek [Internet'e yönelik Yük Dengeleyici](load-balancer-internet-overview.md)

- Daha fazla bilgi edinmek [iç yük dengeleyiciye genel bakış](load-balancer-internal-overview.md)

- Oluşturma bir [Internet'e yönelik Yük Dengeleyici](load-balancer-get-started-internet-portal.md)

- Başka bir anahtar bazıları hakkında bilgi edinin [ağı yetenekleri](../networking/networking-overview.md) Azure

