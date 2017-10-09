---
title: "aaaReplicate çok katmanlı IIS tabanlı Azure Site Recovery kullanarak web uygulaması | Microsoft Docs"
description: "Bu makalede nasıl tooreplicate IIS web grubu sanal makine Azure Site RECOVERY'yi kullanarak açıklanmaktadır."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Azure Site Recovery kullanan çok katmanlı tabanlı IIS web uygulamasına Çoğalt

## <a name="overview"></a>Genel Bakış


Uygulama yazılımı, bir kuruluştaki iş üretkenlik hello altyapısıdır. Çeşitli web uygulamaları bir kuruluşta farklı amaçla kullanılabilir. Bordro işleme, finansal uygulamalar ve müşteri kullanıma yönelik Web siteleri gibi bazılarını utmost olabilir bir kuruluş için kritik. Merhaba kuruluş toohave bunları yukarı ve çalışan her zaman tooprevent üretkenlik kaybını en önemli ve daha da önemlisi herhangi bir zarar toohello marka görüntü hello kuruluşun engelleyebilirsiniz.

Kritik web uygulamaları genellikle çok katmanlı uygulamalar hello web, veritabanı ve uygulama farklı katmanlardaki olarak ayarlanır. Çeşitli katmanları arasında yayılmasını dışında hello uygulamalar aynı zamanda birden çok sunucu her katman tooload Bakiye hello trafiği kullanıyor olabilir. Ayrıca, statik IP adreslerini hello eşlemeleri çeşitli katmanları arasında hello web sunucusuna bağlı olabilir. Hello web sunucusunda yapılandırılmış birden çok Web sitesi varsa, yük devretme, bu eşlemelerin bazıları güncelleştirildi, özellikle, toobe gerekir. SSL kullanan web uygulamaları durumunda güncelleştirilmiş toobe sertifikası bağlamaları gerekir.

Çeşitli yapılandırma dosyaları, kayıt defteri ayarlarını, bağlamaları, özel bileşenleri (COM veya .NET), içerik ve ayrıca sertifikaları ve kurtarma hello dosyalar el ile adımlar kümesi ile yedekleme geleneksel çoğaltma olmayan tabanlı kurtarma yöntemleri içerir. Bu teknikler açıkça sıkıcı hata potansiyeli ve ölçeklenebilir olmaması. Örneğin, sertifikalarını yedekleme tooforget kolayca mümkün olduğundan ve hiçbir seçenek ancak toobuy yeni sertifikalar hello sunucusu için yük devretme sonrasında kalmış olabilir.

İyi olağanüstü durum kurtarma çözümü kurtarma planları hello geçici modelleme karmaşık uygulama mimarilerindeki izin ver ve bu nedenle sağlayan çeşitli katmanları arasındaki hello özelliği özelleştirilmiş tooadd adımları toohandle uygulama eşlemeleri de bir tek çözüm hello tooa önde gelen bir olağanüstü durumda görüntüsü tıklatma emin RTO düşürün.


Nasıl tooprotect bir IIS web uygulama tabanlı kullanarak bu makalede bir [Azure Site Recovery](site-recovery-overview.md). Bu makalede, temel IIS web uygulama tooAzure, nasıl bir olağanüstü durum kurtarma detaylandırma yapabilirsiniz ve yük devretme hello uygulama tooAzure işlemine üç katmanı çoğaltmak için en iyi yöntemler ele alınacaktır.


## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce hello aşağıdaki anladığınızdan emin olun:

1. [Bir sanal makine tooAzure çoğaltma](site-recovery-vmware-to-azure.md)
1. Nasıl çok[kurtarma ağını tasarlama](site-recovery-network-design.md)
1. [Bir test yük devretme tooAzure yapılması](./site-recovery-test-failover-to-azure.md)
1. [Bir yük devretme tooAzure yapılması](site-recovery-failover.md)
1. Nasıl çok[bir etki alanı denetleyicisi çoğaltma](site-recovery-active-directory.md)
1. Nasıl çok[SQL Server çoğaltma](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Dağıtım modelleri
Bir temel IIS web uygulamasını genellikle bir dağıtım desenler izleyen hello aşağıdaki gibidir:

** Dağıtım modeli 1 ** bir IIS web grubu uygulama isteği Routing(ARR), IIS sunucusu ve Microsoft SQL Server ile bağlı.

![Dağıtım modeli](./media/site-recovery-iis/deployment-pattern1.png)

**Dağıtım modeli 2** bir IIS web grubu uygulama isteği Routing(ARR), IIS sunucusunu, uygulama sunucusu ve Microsoft SQL Server ile bağlı.


![Dağıtım modeli](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Site kurtarma desteği

IIS sunucusu Windows Server 2012 R2 Enterprise 7.5 sürümünde bu makale VMware sanal makinelerini oluşturma hello amaçla kullanılmıştır. Site recovery çoğaltma uygulama belirsiz olduğu gibi hello önerileri burada beklenen toohold aşağıdaki senaryolar ve farklı IIS sürümü için sağlanır.

### <a name="source-and-target"></a>Kaynak ve hedef

**Senaryo** | **tooa ikincil site** | **tooAzure**
--- | --- | ---
**Hyper-V** | Evet | Evet
**VMware** | Evet | Evet
**Fiziksel sunucu** | Hayır | Evet

## <a name="replicate-virtual-machines"></a>Çoğaltma sanal makineler

İzleyin [bu kılavuz](site-recovery-vmware-to-azure.md) toostart tüm hello IIS web grubu sanal makineleri tooAzure çoğaltılıyor.

Bir statik IP kullanarak yeniden hello içinde sanal makine tootake hello istediğiniz hello IP belirtin [ **hedef IP** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) işlem ve ağ ayarlarını.

![Hedef IP](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Bir kurtarma planı oluşturma

Bir kurtarma planı çeşitli katmanlarda çok katmanlı bir uygulama, bu nedenle, uygulama tutarlılığını sağlamak hello yük devretme sıralama sağlar. Çok katmanlı web uygulaması için bir kurtarma planı oluşturulurken Hello aşağıdaki adımları izleyin.  [Bir kurtarma planı oluşturma hakkında daha fazla bilgi](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>Sanal makineler toofailover grupları ekleme
Tipik bir çok katmanlı IIS web uygulamasını SQL sanal makineler, bir IIS sunucusu tarafından constituted hello web katmanı ve bir uygulama katmanı ile veritabanı katmanından oluşur. Katman olarak göre tüm bu sanal makineleri toodifferent grubunu ekleyin. [Kurtarma planı customising hakkında daha fazla bilgi](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Bir kurtarma planı oluşturun. Merhaba veritabanı katman sanal makinelerde kapandığından son ve ilk duruma Grup 1 tooensure altında ekleyin.

1. Merhaba veritabanı katmanı duruma sonra bunlar getirildiği gibi hello uygulama katman sanal makinelerde Grup 2 altında ekleyin.

1. Merhaba uygulama katmanı duruma sonra bunlar getirildiği şekilde hello web katman sanal makinelerde grubu 3'te ekleyin.

1. Yük Dengeleme sanal makineleri Hello web katmanı duruma sonra bunlar getirildiği gibi Grup 4'te ekleyin.


### <a name="adding-scripts-toohello-recovery-plan"></a>Toohello kurtarma planı komutlar ekleme
Hello Azure sanal makineleri post yük devretme ve Test yük devretme toomake IIS web grubu işlevi üzerindeki bazı işlemler doğru toodo gerekebilir. Site bağlaması değiştirme DNS girişi, güncelleştirme gibi hello post yük devretme işlemi otomatikleştirmek, aşağıdaki şekilde hello kurtarma planında betikleri ekleyerek bağlantı dizesini değiştirin. [Komut dosyası kurtarma planı ekleme hakkında daha fazla bilgi edinin](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>DNS güncelleştirme
Merhaba DNS genellikle dinamik DNS güncelleştirme sonra sanal makineler için yapılandırılmışsa, başladıktan sonra hello DNS hello yeni IP ile güncelleştirin. Tooadd hello ile açık adım tooupdate DNS yeni istiyorsanız hello sanal makinelerin IP sonra eklemek bu [tooupdate IP DNS'de komut dosyası](https://aka.ms/asr-dns-update) kurtarma planı grupları sonrası eylemi olarak.  

#### <a name="connection-string-in-an-applications-webconfig"></a>Bir uygulamanın web.config dosyasında bağlantı dizesi
web sitesi hello hello veritabanı ile iletişim kurar Hello bağlantı dizesini belirtir.

Hello bağlantı dizesi hello veritabanı sanal makinenin hello adı taşır, başka bir adım gerekli post yük devretme olacaktır ve Merhaba uygulaması okuyamayacak tooautomatically toohello DB iletişim kurar. Ayrıca, hello veritabanı sanal makine için başlangıç IP adresi korunup korunmadığını olmayacaktır gerekli tooupdate hello bağlantı dizesi. Merhaba bağlantı dizesi bir IP adresi kullanarak toohello veritabanı sanal makine başvuruyorsa, güncelleştirilmiş toobe post yük devretme gerekir. Örneğin bağlantı dizesi aşağıda Hello toohello DB IP 127.0.1.2 işaret eder

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

Ekleyerek web katmanı hello bağlantı dizesinde güncelleştirebilirsiniz [IIS bağlantı güncelleştirme betiğini](https://aka.ms/asr-update-webtier-script-classic) Grup 3 hello kurtarma planında sonra.

#### <a name="site-bindings-for-hello-application"></a>Merhaba uygulaması için site bağlamaları
Her site bağlaması hello türü içeren bilgiler, hangi hello IIS sunucusu hello site, başlangıç bağlantı noktası numarasını ve hello hello site için ana bilgisayar adları için toohello istekleri dinler hello IP adresi bağlama oluşur. Bir yük devretme Hello sırasında bu bağlamaların başlangıç IP adresi ilişkili bir değişiklik olursa güncelleştirilmiş toobe gerekebilir.

> [!NOTE]
>
> 'Tüm atanmamış' hello örnekte olduğu gibi hello site bağlaması için işaretlenmiş durumunda bu bağlama post yük devretme tooupdate gerekmez. Ayrıca, bir site ile ilişkili başlangıç IP adresi yük devretme sonrası değiştirilmezse hello site bağlaması güncelleştirilmesi (Merhaba IP adresinin bekletme hello ağ mimarisine bağlıdır ve alt ağları toohello atanan birincil ve kurtarma siteler ve bu nedenle olabilir veya olmayabilir Kuruluşunuz için uygun olabilir.)

![SSL bağlama](./media/site-recovery-iis/sslbinding.png)

Bir site ile başlangıç IP adresi ilişkilendirirseniz tooupdate hello yeni IP adresiyle tüm site bağlamaları gerekir. Ekleyebileceğiniz [IIS Web Katmanı güncelleştirme betiğini](https://aka.ms/asr-web-tier-update-runbook-classic) grubu 3'te kurtarma planı toochange hello site bağlamaları sonra.


#### <a name="update-load-balancer-ip-address"></a>Yük Dengeleyici IP adresi güncelleştir
Uygulama isteği yönlendirme sanal makine varsa eklemeniz [IIS ARR yük devretme betiği](https://aka.ms/asr-iis-arrtier-failover-script-classic) sonra Grup 4 tooupdate başlangıç IP adresi.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>bir https bağlantısı için Hello SSL sertifikası bağlama
Web siteleri hello Web sunucusu ve hello kullanıcının tarayıcısı arasında güvenli iletişim sağlamak için yardımcı olan ilişkili bir SSL sertifikası olabilir. Merhaba Web bir https bağlantısı ve hello IIS sunucusunun SSL sertifikası bağlaması ile ilişkili https site bağlama toohello IP adresi varsa, yeni bir site bağlaması IP hello IIS sanal makinenin yük devretme sonrası hello için sertifika hello ile eklenen toobe gerekir.

Merhaba SSL sertifikası verilen karşı-

bir) Merhaba Web hello tam etki alanı adı<br>
b) Merhaba sunucu hello adı<br>
c) hello etki alanı adı için joker sertifikası<br>
d) Merhaba SSL sertifikası karşı hello IP hello IIS sunucusunun verilir, IIS hello Azure site sunucusunda başka bir SSL sertifikası gereksinimlerini toobe veren karşı hello hello IP adresi ve bu sertifika için ek SSL bağlaması oluşturulan toobe gerekir bir IP adresi –. Bu nedenle, bir SSL sertifikası IP karşı verilen önerilir toonot kullanımı içindir. Bu daha az yaygın olarak kullanılan bir seçenektir ve yeni CA/tarayıcı Forumu değişiklikleri göredir yakında kullanım dışı kalacaktır.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Merhaba bağımlılık hello web hello uygulama katmanı arasındaki güncelleştir
Merhaba sanal makinelerin IP adresini hello temel bir uygulama belirli bağımlılığı varsa, bu bağımlılık post yük devretme tooupdate gerekir.

## <a name="doing-a-test-failover"></a>Yük devretme sınamasını yapmak
İzleyin [bu kılavuz](site-recovery-test-failover-to-azure.md) toodo yük devretme sınaması.

1.  TooAzure portal gidin ve kurtarma hizmeti kasanızı seçin.
1.  IIS web grubu için oluşturulan hello kurtarma planı tıklayın.
1.  'Test yük devretme üzerinde' tıklayın.
1.  Kurtarma noktası ve Azure sanal ağı toostart hello test yük devretme işlemi seçin.
1.  Merhaba ikincil ortamı kurma olduğunda, doğrulama gerçekleştirebilirsiniz.
1.  Hello doğrulama tamamlandıktan sonra 'Doğrulamaları tamamlamak' seçin ve yük devretme sınama ortamı hello temizlenecek.

## <a name="doing-a-failover"></a>Bir yük devretme işleminden
İzleyin [bu kılavuz](site-recovery-failover.md) , yaparken bir yük devretme.

1.  TooAzure portal gidin ve kurtarma hizmeti kasanızı seçin.
1.  IIS web grubu için oluşturulan hello kurtarma planı tıklayın.
1.  'Failover' üzerinde'ı tıklatın.
1.  Kurtarma noktası toostart hello yük devretme işlemini seçin.

## <a name="next-steps"></a>Sonraki adımlar
Hakkında daha fazla bilgiyi [diğer uygulamaları çoğaltmak](site-recovery-workload.md) Site RECOVERY'yi kullanarak.
