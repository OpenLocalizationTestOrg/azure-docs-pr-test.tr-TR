---
title: "aaaDesigning ağ altyapınızın olağanüstü durum kurtarma | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery için ağ tasarım konuları anlatılmaktadır."
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Ağınız olağanüstü durum kurtarma için tasarlama

Bu makale mimariden, uygulama ve iş sürekliliği ve olağanüstü durum kurtarma (BCDR) altyapısını desteklemek için sorumlu olan ve tooleverage Microsoft Azure Site Kurtarma (ASR) toosupport isteyen yönlendirilmiş tooIT uzmanları içindir ve BCDR hizmetlerini geliştirin. Bu makalede dikkat edilecek noktalar ele veya başka bir site içi olağanüstü durum kurtarma sitesinde ağ yapılandırma içinde Azure olabilir. 

## <a name="overview"></a>Genel Bakış
[Azure Site Kurtarma (ASR)](https://azure.microsoft.com/services/site-recovery/) hello koruma ve kurtarma iş sürekliliği olağanüstü durum kurtarma (BCDR) amacıyla sanallaştırılmış uygulamalarınızın düzenler bir Microsoft Azure hizmetidir. Bu belge IP aralıkları ve alt ağları hello olağanüstü durum kurtarma sitesinde Site Recovery kullanarak sanal makineleri (VM'ler) çoğaltırken mimariden üzerine odaklanan hedeflenen tooguide hello okuyucu hello süreci hello ağları tasarlama değil.

Ayrıca, bu makalede Site Recovery mimarisi oluşturma ve çok siteli sanal datacenter toosupport BCDR Hizmetleri zaman olağanüstü durum ya da test uygulama nasıl sağladığı gösterilmektedir.

7/24 bağlantı herkes bekliyor burada bir dünyanın her zamankinden tookeep daha da önemlisi, altyapı ve uygulamalarınızı çalışır. Merhaba kuruluş hızla normal işlemler devam edebilmek için iş devamlılığı ve olağanüstü durum kurtarma (BCDR) hello amacı başarısız toorestore bileşenleri budur. Tahmin edilemez, devastating olaylarla geliştirme olağanüstü durum kurtarma stratejileri toodeal çok zor. Bu hello gelecekteki tahmin etmeye toohello yapısında zorluğunu, özellikle tooimprobable olaylar ve hello yüksek ilgili olarak tooprovide beklediğinizden çok daha büyük catastrophes karşı koruma yeterli ölçülerin maliyeti.

Önemli planlama BCDR için kurtarma süresi hedefi (RTO) ve kurtarma noktası hedefi (RPO), olağanüstü durum kurtarma planının bir parçası tanımlanması gerekir. Azure Site Recovery, müşteriler hızlı şekilde kullanmaya hello müşterinin veri merkezi (düşük RTO) bir olağanüstü durum sağlar, hello ikincil veri merkezi veya Microsoft Azure içinde en az veri kaybı (düşük RPO'ya) bulunan çoğaltılmış sanal makinelerini çevrimiçi.

Yük devretme hello birincil veri merkezi toohello ikincil veri merkezi veya tooAzure (bağlı olarak hello senaryosu) atanan sanal makine başlangıçta kopyalar ve hello çoğaltmaları düzenli aralıklarla yeniler ASR tarafından mümkün hale getirilir. Altyapı planlama sırasında ağ tasarımı, RTO toplantı şirketten ve RPO hedefleri engelleyebilirsiniz olası performans sorunu düşünülmelidir.  

Yöneticiler toodeploy bir olağanüstü durum kurtarma çözümü planlarken fikirlerini anahtar sorulara hello hello yük devretme tamamlandıktan sonra nasıl hello sanal makine erişilebilir olacaktır biridir. Hello Yöneticisi toochoose hello ağ toowhich bir sanal makineye bağlı tooafter yük devretme olacaktır ASR sağlar. Merhaba birincil site Azure ya da bu ağ eşlemesi kullanılarak elde edilir sonra VMM sunucusu tarafından yönetilen bir şirket içi site ise. Daha fazla bilgi edinmek [Azure tooAzure DR eşlemede ağ](site-recovery-network-mapping-azure-to-azure.md) ve [ağ eşlemesi vmm'den](site-recovery-network-mapping.md)


Hello Yöneticisi hello kurtarma sitesi için Hello ağ tasarlarken, iki seçeneğiniz vardır:

* Kurtarma sitesinde hello ağ için farklı bir IP adresi aralığı kullanın. Bu senaryoda hello sanal makine yük devretme sonrasında yeni bir IP adresi alır ve Merhaba yönetici toodo DNS güncelleştirme olması gerekir. 
* Merhaba kurtarma sitesindeki hello ağ için aynı IP adresi aralığı kullanın. Bazı senaryolarda, yöneticiler hello birincil sitede bile hello yük devretme sonrasında sahip oldukları tooretain hello IP adreslerini tercih eder. Normal bir senaryoda, bir yönetici tooupdate hello yollar tooindicate hello yeni konumunu hello IP adreslerini gerekir. Ancak uzatılan bir alt birincil hello ve hello kurtarma siteleri arasında dağıtıldığı hello senaryoda hello IP adreslerini hello sanal makineler için koruma çekici bir seçenek haline gelir. Bir şirket içi ağ tooan Azure ağı veya iki Azure ağları arasında alt ağ uzatma mümkün değildir.  

Yöneticiler toodeploy bir olağanüstü durum kurtarma çözümü planlarken fikrini anahtar sorulara hello hello yük devretme tamamlandıktan sonra nasıl hello uygulamaları ulaşılabilir biridir. Modern uygulamalar, neredeyse her zaman toosome derece, böylece fiziksel bir site tooanother bir hizmet taşıma ağ sınaması temsil eden ağ bağımlıdır. Bu sorunu olağanüstü durum kurtarma çözümleri ile dağıtılır, başlıca iki yolu vardır. Merhaba ilk sabit IP adresleri toomaintain yaklaşımdır. Taşıma hello Hizmetleri ve barındırma sunucuları farklı fiziksel konumlarda olan hello rağmen uygulamaları hello IP adresi yapılandırması onlarla toohello yeni konuma bırakın. Merhaba İkinci yaklaşımı tamamen hello IP adresi hello kurtarılan site içine hello geçiş sırasında değiştirilmesidir. Her iki yaklaşımın aşağıda özetlenen birkaç uygulama Çeşitlemeler vardır.

Hello Yöneticisi hello kurtarma sitesi için Hello ağ tasarlarken, iki seçeneğiniz vardır:

## <a name="option-1-retain-ip-addresses"></a>Seçenek 1: IP adreslerini korur
Bir olağanüstü durum kurtarma işlemi açısından bakıldığında, sabit IP adresleri kullanarak toobe hello en kolay yöntem tooimplement görünür, ancak bir dizi olası sahip anlamasını uygulamada zorluklar hello az yaygın olan bir yaklaşım. Azure Site Recovery tooretain hello IP adreslerini tüm senaryolarda hello yeteneği sağlar. Bir tooretain IP karar önce uygun düşünce hello yük devretme yetenekleri uygular toohello kısıtlamaları verilmelidir. Bize karar tooretain IP adresleri veya toomake yardımcı olabilecek hello etmenleri arayın. Bu iki yolla Uzatılan bir alt ağ kullanarak veya tam alt ağ yük devretme işleminden elde edilebilir.

### <a name="stretched-subnet"></a>Esnetilen alt ağ
Burada hello alt ağ aynı anda hem birincil hem de DR konumları içinde kullanılabilir hale getirilir. Basitçe bu bir sunucuya taşıyabilirsiniz ve hello ağ ve IP (Katman 3) yapılandırma toohello ikinci site hello trafiği toohello yeni konuma otomatik olarak yönlendirilecek anlamına gelir. Bu sunucu açısından ile Önemsiz toodeal ancak belirli zorluklar var:

* Bir katman 2 (veri bağlantı katmanı) açısından Uzatılan bir VLAN yönetebilirsiniz ağ ekipmanları gerekir, ancak bu daha az soruna şimdi geniş çapta kullanılabilir olduğu gibi bir işlem haline gelmiştir. Merhaba ikinci ve daha zor hello yayarak VLAN hello olası hata etki alanı tooboth siteler, aslında tek hata noktası haline genişletildiğini sorunudur. Bu bir ender olsa da, bir yayın storm başlatıldı ancak yalıtılmış kaldırılamıyor gerçekleştirilmedi. Biz son bu sorun hakkında karma görüşlerini bulduğunuz ve birçok başarılı uygulamalarının yanı sıra "biz hiçbir zaman bu teknoloji burada gerçekleştireceksiniz" gördünüz.
* Esnetilen alt DR sitesi hello gibi Microsoft Azure kullanıyorsanız mümkün değildir.

### <a name="subnet-failover"></a>Alt ağ yük devretme
Bu, olası tooimplement alt ağ yük devretme tooobtain hello yararları hello alt birden çok sitede uzatma olmadan yukarıda açıklanan uzatılmış hello alt çözüm olur. Burada herhangi belirli alt ağ aynı anda Site 1 veya Site 2'ancak hiçbir her iki site de mevcut olacaktır. Sipariş toomaintain hello IP adres alanı bir yük devretme hello olaydaki, olası tooprogrammatically düzenlemek için hello yönlendirici altyapı toomove hello alt ağlardan bir site tooanother. Bir yük devretme senaryosu hello alt ağlar misiniz hello hareket korumalı VM'lerin ilişkili. Merhaba asıl sakıncası toothis bir hatanın hello olayda Tamam olabilen toomove hello tüm alt ağı, sahip ancak hello yük devretme ayrıntı düzeyi konuları etkileyebilecek yaklaşımdır.

Contoso adlı kurgusal bir kuruluş mümkün tooreplicate nasıl yapıldığını inceleyelim VM'ler tooa kurtarma konumuna hello tüm alt ağa yapabilmesini oluştu. Biz öncelikle Contoso mümkün toomanage nasıl yapıldığını en alt ağlarını Vm'lerini iki arasında çoğaltma şirket içi konumları ve ardından alt ağ yük devretme ne zaman nasıl çalışır aşağıdakiler ele alınacaktır görüneceğini [Azure hello olağanüstü durum kurtarma sitesi olarak kullanılan](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Şirket içi tooAzure yük devretmeyi 
Azure Site Kurtarma (ASR) olağanüstü durum kurtarma ile ilgili bir site, sanal makineleriniz için kullanılan Azure toobe sağlar.  

Woodgrove Bank adlı kurgusal bir şirket içi altyapınızı kendi iş kolu uygulamaları barındırma sahip olduğu bir senaryo inceleyelim ve Azure mobil uygulamalarını barındıran. Azure ve şirket içi sunucularda Woodgrove Bank VM'ler arasında bağlantısı, siteden siteye (S2S) sanal özel ağ (VPN) ya da ExpressRoute tarafından sağlanır. S2S VPN Woodgrove Bank'ın sanal ağ Woodgrove Bank'ın bir uzantısı içi ağ gibi görülen Azure toobe sağlar. Bu iletişim, Woodgrove Bank kenarı ve Azure sanal ağı arasında S2S VPN tarafından etkinleştirilir. Şimdi Woodgrove toouse ASR tooreplicate Birincil Azure bölgesi tooanother Azure bölgesi çalışan kendi iş yüklerini istemektedir. Bu seçenek ekonomik bir DR seçeneği istediği ve genel bulut ortamlarında mümkün toostore veriler, Woodgrove hello gereksinimlerini karşılar. Uygulama ve IP adreslerini sabit kodlanmış bağlı olan yapılandırmaları toodeal Woodgrove sahipse, bu nedenle uygulamalarını gereksinim tooretain IP adreslerinde sonra başarısız olan Azure tooanother bölgede üzerinden sahip oldukları.

Woodgrove IP adresi aralığı (172.16.1.0/24, 172.16.2.0/24) tooits kaynakları Azure'da çalışan tooassign IP adreslerinden karar vermiştir.

Woodgrove toobe mümkün tooreplicate hello IP adresleri, korurken, sanal makineleri tooAzure toobe oluşturulan bir Azure sanal ağı gerekir. Uygulamaları hello şirket içi site tooAzure yük devretmeyi sorunsuz bir şekilde böylece hello şirket içi ağ uzantısı olmalıdır. Azure, Azure içinde oluşturulan tooadd noktası site yanı sıra, siteden siteye VPN bağlantısı toohello sanal ağlar sağlar. Azure değil çünkü yalnızca başlangıç IP adresi aralığı hello şirket içi IP adresi aralığından farklıysa, siteden siteye bağlantı kurma, Azure ağ tooroute trafiği toohello şirket içi konumu (Azure yerel ağ çağırır) sağlar Uzatma alt ağları destekler.  Bunun anlamı, varsa alt 192.168.1.0/24 şirket içi, yapamazsınız, yerel ağ 192.168.1.0/24 hello Azure ağı ekleyin. Azure hello alt ağda etkin VM yok ve yalnızca DR amaçları için oluşturulan hello alt bilmiyor çünkü bu beklenir. toobe mümkün toocorrectly ağ trafiğini yönlendirmek hello ağ ve hello yerel ağ bir Azure ağı hello alt dışında çakışmaması gerekir.

![Alt ağ yük devretme önce](./media/site-recovery-network-design/network-design7.png)

Önce yük devretme

toohelp Woodgrove iş gereksinimleri karşılamak, iş akışları şu tooimplement hello ihtiyacımız var:

* Ek bir ağ oluşturun, bize burada hello başarısız üzerinden sanal makineleri oluşturulan kurtarma ağ çağırın.
* Merhaba IP bir VM için bir yük devretme sonrasında tutulur tooensure VM Özellikleri'nin altında toohello yapılandırma sekmesine gidin, VM hello aynı IP şirket içi sahiptir ve Kaydet'i tıklatın hello belirtin. Merhaba VM üzerinden başarısız olduğunda, Azure Site Recovery IP toohello sanal makine sağlanan hello atayın.

![Ağ Özellikleri](./media/site-recovery-network-design/network-design8.png)

Merhaba yük devretme tetiklenir ve hello sanal makineleri hello kurtarma ağ istenen hello IP ile oluşturulan sonra bağlantı toothis ağ kullanılarak kurulabilir bir [Vnet tooVnet bağlantı](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Bu eylem komut dosyasıyla gerekiyorsa.  Biz hello önceki bölümde, yük devretme tooAzure hello durumda bile alt ağ yük devretme hakkında yollar toobe uygun şekilde tooreflect değiştiren açıklandığı gibi bu 192.168.1.0/24 şimdi tooAzure taşınmıştır.

![Alt ağ yük devretme sonrasında](./media/site-recovery-network-design/network-design9.png)

Yük devretme sonrasında

Yukarıdaki hello resimde gösterildiği gibi 'Azure Ağ' yoksa. Merhaba yük devretme sonrasında 'Birincil Site' ve 'Kurtarma Ağ' arasında bir site toosite vpn bağlantısı oluşturabilirsiniz.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Yük devretme tooa ikincil site şirket içi
Bize burada hello IP hello VM'lerin her birinde, korumak istediğiniz bir senaryo konum ve yük devretme hello alt birlikte tamamlayın. Merhaba birincil site alt 192.168.1.0/24 içinde çalışan uygulamalar vardır. Merhaba yük devretme gerçekleştiğinde, bu alt ağın parçası olan tüm hello sanal makinelere toohello kurtarma sitesi başarısız ve IP adreslerini korur. Yollar olacaktır toobe toosubnet 192.168.1.0/24 ait tüm hello sanal makineleri toohello kurtarma sitesini şimdi taşıdığınıza tooreflect hello olgu uygun şekilde değiştirdi.

Merhaba birincil site ve site kurtarma, üçüncü sitesi ve birincil site aşağıdaki çizimde hello yönlendirir ve üçüncü sitesini ve kurtarma sitesini uygun şekilde değiştirilmiş toobe gerekir.

resimleri aşağıdaki hello hello alt hello yük devretme önce gösterir. Alt ağ 192.168.0.1/24 hello yük devretmeden önce birincil Site hello üzerinde etkindir ve hello yük devretme sonrasında kurtarma sitesini Merhaba etkin hale gelir

![Önce yük devretme](./media/site-recovery-network-design/network-design2.png)

Önce yük devretme

Merhaba resimde, yük devretme sonrasında ağlara ve alt ağları gösterilmektedir.

![Yük devretme sonrasında](./media/site-recovery-network-design/network-design3.png)

Yük devretme sonrasında

Şirket içi ikincil sitede olduğunu ve VMM Sunucu toomanage kullanıyorsanız ardından belirli bir sanal makine ASR için koruma etkinleştirme iş akışı aşağıdaki toohello göre ağ kaynaklarını ne zaman ayırır:

* ASR hello ilgili ağ her System Center VMM örneği için tanımlanan hello statik IP adres havuzundan hello sanal makine üzerindeki her ağ arabirimi için bir IP adresi ayırır.
* Hello Yöneticisi başlangıç IP adresi havuzundan Merhaba, başlangıç IP adresi toohello çoğaltma sanal makine ASR ayırma sırasında hello birincil site ağda tahsis, aynı IP adresi havuzu hello kurtarma sitesi olarak hello ağda için hello tanımlıyorsa aynı hello IP adresi, hello birincil sanal makine olarak.  Merhaba IP VMM'de ayrılmış ancak yük devretme IP hello Hyper-v ana bilgisayarda ayarlı değil. Bir Hyper-v konağı yük devretme IP hello yük devretme işleminden hemen önce ayarlanır.


Merhaba aynı IP kullanılabilir durumda değilse, ASR hello tanımlanan IP adresi havuzundan diğer bazı bir kullanılabilir IP adresi ayırın.

Merhaba VM için koruma etkinleştirildikten sonra toohello sanal makineye ayrılmış örnek komut dosyası tooverify hello IP aşağıdaki kullanabilirsiniz. aynı IP ayarlanabilir yük devretme IP ve yük devretme hello zamanında toohello VM atanan hello:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> Burada sanal makineler DHCP kullanmak hello senaryoda hello IP adreslerinin tamamen ASR hello denetimi dışına yönetimidir. Bir yönetici hello DHCP sunucusunun hizmet hello IP adreslerinin hello kurtarma sitesinde hello kullanılabileceği tooensure sahip aynı aralık hello birincil sitesi olarak.
>
>



## <a name="option-2-changing-ip-addresses"></a>Seçenek 2: IP adreslerini değiştirme
Bu yaklaşım toobe hello en yaygın ne anlatıldığı üzerinde temel gibi görünüyor. Merhaba yük devretme kümesinde dahil her VM hello IP adresini değiştirme hello formu alır. Bu yaklaşımın bir dezavantajı hello gelen ağ too'learn gerektirir ' IPX olan bu hello şimdi IPy uygulamadır. IPX ve IPy mantıksal adları olsa bile, DNS girişlerini genellikle değiştirilmiş veya hello ağda Temizlenen toobe sahiptir ve önbelleğe alınmış ağ tablolardaki güncelleştirilmiş veya temizlenen toobe girişleriniz, bu nedenle bir kapalı kalma süresi hello DNS altyapısının nasıl sahip bağlı bağlı olarak görülebilir kuruldu. Bu sorunları intranet uygulamalarını hello durumda düşük TTL değerleri kullanarak ve kullanılarak azaltılabilir [Azure trafik Yöneticisi ASR ile](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) için Internet tabanlı uygulamalar

### <a name="changing-hello-ip-addresses---illustration"></a>Çizim Hello IP adresleri - değiştirme
Burada toouse planlama hello senaryo bize Ara hello birincil ve hello kurtarma siteler arasında farklı IP'leri. Aşağıdaki örneğine hello biz de birincil ya da kurtarma sitesinde barındırılan hello uygulamaları burada erişilip üçüncü sitesinden sahip.

![Farklı bir IP - yük devretme önce](./media/site-recovery-network-design/network-design10.png)


Yapılandırılmış toocome yukarı alt 172.16.1.0/24 hello kurtarma sitesinde bir yük devretme sonrasında kaldıktan ve yukarıdaki Hello resim alt 192.168.1.0/24 alt hello birincil sitede barındırılan bazı uygulamalar vardır. Tüm üç siteleri birbirine erişebilmesi için VPN bağlantıları/ağ yolları uygun şekilde yapılandırılmış.

Bir veya daha fazla uygulama üzerinden başarısız olduktan sonra gösterir aşağıda hello resim olarak bunlar hello kurtarma alt ağda geri yüklenir. Bu durumda biz hello alt kısıtlanmış toofailover hello tüm olmayan aynı anda. Hiçbir değişiklik gerekli tooreconfigure VPN veya ağ yolların edilir. Bir yük devretme ve bazı DNS güncelleştirmeleri, uygulamalar erişilebilir kalır emin olmanızı sağlar. Merhaba DNS dinamik güncelleştirmeleri yapılandırılan tooallow ise hello sanal makineler kendilerini bir yük devretme sonrasında başladığınızda hello yeni IP kullanarak kaydetmeniz.

![Farklı bir IP - yük devretme sonrasında](./media/site-recovery-network-design/network-design11.png)


Başarısız olan üzerinden hello çoğaltma sanal makinesi olmayan bir IP adresi olabilir sonra aynı hello IP adresi hello birincil sanal makine olarak hello. Sanal makineler, kullandıkları hello DNS sunucusu güncelleştirilecek başladıktan sonra. DNS girişlerini genellikle değiştirilmiş veya hello ağda Temizlenen toobe, ve böylece bu durum değişiklikleri yer alırken kapalı kalma süresi ile karşılaştığı seyrek toobe ağ tablolardaki önbelleğe alınmış girişlerin güncelleştirilmiş veya temizlenen, toobe sahiptir. Bu sorunu azaltmak için:

* Düşük TTL değeri için intranet uygulamalarını kullanma.
* Azure trafik Yöneticisi ile ASR kullanarak için internet tabanlı uygulamaları.
* Merhaba aşağıdakileri kullanarak komut dosyası, Kurtarma içinde planlama tooupdate hello DNS sunucusu tooensure zamanında güncelleştirme (Merhaba betik gerekli değildir hello dinamik DNS kayıt yapılandırılmışsa)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Değişen hello IP adresleri – DR tooAzure
Merhaba [ağ altyapı kurulumu bir olağanüstü durum kurtarma sitesi olarak Microsoft Azure](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) blog gönderisi açıklar nasıl IP adreslerini korunurken karşılaşılan Azure ağ altyapısı olmayan bir gereksinim toosetup hello gerekli. Merhaba uygulaması ve sonra Görünüm nasıl toosetup ağ şirket içi ve Azure ve nasıl tamamlanırken açıklayan ile başlayan toodo yük devretme testi ve planlanmış bir yük devretme.

## <a name="next-steps"></a>Sonraki adımlar
[Bilgi](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) kullanılan toomanage hello birincil site bir VMM sunucusu yüklenirken Site Recovery kaynak ve hedef ağlara nasıl eşleştirir.
