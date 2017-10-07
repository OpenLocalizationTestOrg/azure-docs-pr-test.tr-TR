---
title: "Hyper-V çoğaltma tooa ikincil VMM sitesi Azure Site Recovery ile ağ aaaPlan | Microsoft Docs"
description: "Bu makale, Hyper-V sanal makineleri tooa Azure Site Recovery ile ikincil System Center VMM site çoğaltırken ağ planlama açıklanır."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 095f2d73-994e-4fc0-96f2-e03a7d72e492
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 5934db4a661a2c697a1a799c3848852250ddb451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>3. adım: ağ bağlantısı Hyper-V VM çoğaltma tooa ikincil VMM sitesi için planlama

Hyper-V sanal makineleri (VM'ler) System Center Virtual Machine Manager (VMM) bulutlarında yönetilen çoğaltırken ağ Bu makale tooplan okuma dağıtımının önkoşulları gözden geçirdikten sonra ikincil site tooa kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure Portalı'nda. 

Bu makaleyi okuduktan sonra tüm yorumlar hello altındaki ya da hello sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-overview"></a>Ağ eşlemesi genel bakış

Ağ eşlemesi, Hyper-V Vm'lerini (VMM yönetilen) tooa ikincil veri merkezine çoğaltma yapılırken kullanılır. Bir kaynak VMM sunucusunda VM ağları ve bir hedef VMM sunucusunda VM ağları arasında ağ eşlemesi eşler. Eşleme aşağıdaki hello:

- **Ağ bağlantısı**— bağlayan VM'ler tooappropriate ağları yük devretme sonrasında. Merhaba çoğaltma VM eşlenen toohello kaynak ağ bağlantılı toohello hedef ağ olacaktır.
- **En iyi yerleştirme**— yerler çoğaltma sanal makineleri Hyper-V ana bilgisayar sunucuları üzerinde en iyi şekilde hello. Çoğaltma sanal makineleri erişim hello eşlenen, VM ağları konaklarda yerleştirilir.
- **Ağ eşleme**— ağ eşlemesini yapılandırmazsanız, yük devretme sonrasında çoğaltma sanal makineleri bağlı tooany VM ağları olmayacaktır.


### <a name="example"></a>Örnek

Bir örnek tooillustrate İşte bu mekanizması. New York ve Şikago iki konumda bulunduğu bir kuruluşta atalım.

**Konum** | **VMM sunucusu** | **VM ağları** | **Eşlenen**
---|---|---|---
New York | VMM NewYork| VMNetwork1 NewYork | Eşlenen tooVMNetwork1 Chicago
 |  | VMNetwork2 NewYork | Eşlenmedi
Chicago | VMM Chicago| VMNetwork1 Chicago | Eşlenen tooVMNetwork1 NewYork
 | | VMNetwork1 Chicago | Eşlenmedi

Bu örnekte:

- Bağlı tooVMNetwork1 NewYork olan tüm sanal makine için bir çoğaltma sanal makine oluşturulduğunda, bağlı tooVMNetwork1 Chicago olacaktır.
- Bir çoğaltma sanal makinesi VMNetwork2 NewYork veya VMNetwork2 Chicago oluşturulduğunda, bağlı tooany ağ olmaz.

İşte nasıl VMM Bulutları örnek kuruluş ve hello Mantıksal ağlar hello bulutlarıyla ilişkili ayarlanır.

#### <a name="cloud-protection-settings"></a>Bulut koruma ayarlarını

**Korumalı bulut** | **Bulut koruma** | **Mantıksal ağ (New York)**  
---|---|---
GoldCloud1 | GoldCloud2 |
SilverCloud1| SilverCloud2 |
GoldCloud2 | <p>NA</p><p></p> | <p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p>
SilverCloud2 | <p>NA</p><p></p> | <p>LogicalNetwork1 NewYork</p><p>LogicalNetwork1 Chicago</p>

#### <a name="logical-and-vm-network-settings"></a>Mantıksal ve VM ağ ayarları

**Konum** | **Mantıksal ağ** | **İlişkili bir VM ağı**
---|---|---
New York | LogicalNetwork1 NewYork | VMNetwork1 NewYork
Chicago | LogicalNetwork1 Chicago | VMNetwork1 Chicago
 | LogicalNetwork2Chicago | VMNetwork2 Chicago

#### <a name="target-network-settings"></a>Hedef ağ ayarları

Merhaba hedef VM ağ seçeneğini belirlediğinizde bu ayarları temel alarak, aşağıdaki tablonun hello kullanılabilecek hello seçimler gösterilmektedir.

**Seç** | **Korumalı bulut** | **Bulut koruma** | **Hedef ağ yok**
---|---|---|---
VMNetwork1 Chicago | SilverCloud1 | SilverCloud2 | Kullanılabilir
 | GoldCloud1 | GoldCloud2 | Kullanılabilir
VMNetwork2 Chicago | SilverCloud1 | SilverCloud2 | Kullanılamıyor
 | GoldCloud1 | GoldCloud2 | Kullanılabilir


Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri üzerinde hangi hello kaynak sanal makinenin bulunduğu alt ağ hello gibi aynı adı sonra hello hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.


#### <a name="failback-behavior"></a>Yeniden çalışma davranışı

yeniden çalışma (geriye doğru çoğaltma), hello durumda neler toosee VMNetwork1 NewYork eşlenen tooVMNetwork1-Chicago, ayarlar aşağıdaki hello ile olduğunu varsayalım.


**Sanal makine** | **Bağlı tooVM ağ**
---|---
VM1 | VMNetwork1 ağ
VM2 (VM1 çoğaltma) | VMNetwork1 Chicago

Şimdi bu ayarlarla olası senaryolar birkaç içinde neler gözden geçirin.

**Senaryo** | **Sonucu**
---|---
Yük devretme işleminden sonra VM-2 hello ağ özellikleri değişiklik. | VM 1 bağlı toohello kaynak ağ kalır.
VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve bağlantısı kesilir. | VM 1 kesilir.
VM-2 ağ özellikleri yük devretme işleminden sonra değiştirilir ve bağlı tooVMNetwork2 Chicago değil. | VMNetwork2 Chicago eşlenmediği olduysa, VM-1 kesilecektir.
Ağ eşlemesi VMNetwork1 Chicago değiştirilir. | VM 1 bağlı toohello şimdi eşlenen ağ tooVMNetwork1-Chicago olacaktır.



## <a name="prepare-for-network-mapping"></a>Ağ eşlemesi için hazırlanma

1. Merhaba kaynak ve hedef VMM sunucularında, hello kaynak ve hedef bulutlarıyla ilişkili bir mantıksal ağ olmalıdır. 
2. Merhaba kaynak ve hedef sunucular, bir VM ağ bağlantılı toohello mantıksal ağ olmalıdır.
3. Hyper-V konakları hello kaynak konumda Vm'lerinde bağlantılı toohello kaynak VM ağına olmalıdır. Yalnızca tek bir VMM sunucusu kullanıyorsanız, hello VM ağlarında arasında aynı eşleme yapılandırabilirsiniz sunucu.

Site Recovery dağıtımı sırasında ağ eşlemesini ayarladığınızda şunlar olur:

- Ağ eşlemesi ayarlamanız ve bir hedef VM ağı seçtiğinizde hello kaynak VM ağı kullanan hello VMM kaynak Bulutları, hello kullanılabilir hedef VM ağları hello hedef Bulutları ile birlikte görüntülenir.
- - Eşleme doğru bir şekilde yapılandırıldığından ve çoğaltma etkin olduğunda, bir kaynak VM bağlı tooits kaynak VM ağına olacaktır ve onun çoğaltması hello hedef konumda bağlı tooits VM ağı eşlenmiş.
- Merhaba hedef ağın birden çok alt ağı varsa ve bu alt ağlardan biri üzerinde hangi hello kaynak sanal makinenin bulunduğu alt ağ hello gibi aynı adı sonra hello hello varsa çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello VM bağlı toohello hello ağdaki ilk alt ağ olacaktır.

## <a name="connect-toovms-after-failover"></a>Yük devretme sonrasında tooVMs Bağlan

Çoğaltma ve yük devretme stratejinizi planlarken hello önemli sorular biri nasıl tooconnect toohello çoğaltma yük devretme sonrasında. Birkaç seçeneğiniz vardır: 

- **Farklı bir IP adresi kullanmak**: hello kopyalanan VM için farklı bir IP adresi toouse seçebilirsiniz. Bu senaryo hello VM yük devretme sonrasında yeni bir IP adresi alır ve DNS güncelleştirme gerekli değildir.
- **Korumak hello aynı IP adresini**: bunu istemeyebilirsiniz toouse hello hello çoğaltma VM için aynı IP adresi. Aynı IP adreslerini basitleştirir tutma hello azaltarak hello kurtarma yük devretme sonrasında ilgili sorunlar ağ. 

## <a name="retain-ip-addresses"></a>IP adreslerini korur

Tooretain hello IP adreslerini istiyorsanız hello birincil sitesinden yük devretme toohello ikincil site sonra da tam alt ağ yük devretme işlemi gerçekleştirin ve yolları tooindicate hello yeni konumunu hello IP adreslerini güncelleştirin veya alternatif Uzatılan bir alt ağ hello arasında dağıtma birincil ve kurtarma sitelerinde hello.

### <a name="stretched-subnet"></a>Esnetilen alt ağ

Esnetilen bir alt ağda hello alt ağ aynı anda hem hello birincil ve ikincil sitede kullanılabilir. Bir sunucu ile IP (Katman 3) yapılandırma toohello ikincil sitesi taşırsanız, hello ağ hello trafiği toohello yeni konuma otomatik olarak yönlendirilecek. 

Bir katman 2 (veri bağlantı katmanı) açısından Uzatılan bir VLAN yönetebilirsiniz ağ ekipmanları gerekir. Buna ek olarak, VLAN uzatma hello tarafından hello olası hata etki alanı tooboth siteler, aslında tek hata noktası haline genişletir. Bu bir olası olmakla birlikte, bir yayın storm kullanmaya ve yalıtılmış olamaz meydana gelebilir. 


### <a name="subnet-failover"></a>Alt ağ yük devretme

Gerçekte uzatma olmadan, bir alt ağ yük devretme tooobtain hello uzatılmış hello alt yararları çalıştırabilirsiniz. Bu çözümde, bir alt ağ kullanılabilecek hello kaynak veya hedef sitede, ancak her ikisi de aynı anda. bir yük devretme toomaintain hello IP adres alanı hello olay program aracılığıyla hello yönlendirici altyapı toomove hello alt ağlardan bir site tooanother düzenleyebilirsiniz. Yük devretme gerçekleştiğinde, alt ağlar ile taşıyabilir sonra hello VM'ler ilişkilendirilmiş. Merhaba asıl sakıncası bir hatanın hello olayı, toomove hello tüm alt ağı olmasıdır.

### <a name="example"></a>Örnek

Tam alt ağ yük devretme bir örneği burada verilmiştir. Merhaba birincil site alt 192.168.1.0/24 içinde çalışan uygulamalar vardır. Yük devretme, tüm hello VM'ler bu alt ağ ikincil site toohello başarısız ve IP adreslerini korur. Yollar gerek toobe toosubnet 192.168.1.0/24 ait tüm hello VM sanal makineleri toohello ikincil site şimdi taşıdığınıza tooreflect hello olgu değiştirdi.

Merhaba aşağıdaki grafik hello alt önce ve yük devretme sonrasında göster:

- Yük devretme önce alt 192.168.0.1/24 hello kaynak sitede, yük devretme sonrasında hello ikincil sitede etkin hale etkindir.
- birincil site ve site kurtarma, üçüncü sitesi ve birincil site Hello yönlendirir ve üçüncü sitesini ve kurtarma sitesini uygun şekilde değiştirilmiş toobe gerekir.

**Önce yük devretme**

![Önce yük devretme](./media/vmm-to-vmm-walkthrough-network/network-design2.png)

**Yük devretme sonrasında**

![Yük devretme sonrasında](./media/vmm-to-vmm-walkthrough-network/network-design3.png)

Yük devretme sonrasında, şunlar olur:

- Site Recovery havuzundan hello statik IP adresi her VMM örneği hello ilgili ağ hello VM üzerindeki her ağ arabirimi için bir IP adresi ayırır.
- Başlangıç IP adresi havuzu hello ikincil sitedeki ise hello kaynak sitedeki Site Recovery aynı ayırır hello aynı IP adresidir (Merhaba kaynak VM) toohello çoğaltma VM hello. Başlangıç IP adresi VMM'de ayrılmış, ancak hello Hyper-V ana bilgisayarda hello yük devretme IP adresi olarak ayarlanmamış. bir Hyper-v ana bilgisayar üzerindeki Hello yük devretme IP adresi hello yük devretme işleminden hemen önce ayarlanır.
- Merhaba aynı IP adresi kullanılabilir değilse, Site Recovery hello havuzundan başka bir kullanılabilir IP adresi ayırır.
- Sanal makineleri DHCP kullanıyorsanız, Site Recovery hello IP adreslerini yönetmek değil. DHCP hello toocheck ihtiyacınız hello ikincil site sunucusunda adresi hello hello kaynak site olarak aynı aralığı'ndan ayırabilirsiniz.

### <a name="validate-hello-ip-address"></a>Başlangıç IP adresini doğrulayın

Bir sanal makine için koruma etkinleştirildikten sonra örnek komut dosyası tooverify hello atanan adresi toohello VM kullanabilirsiniz. aynı IP adresini hello yük devretme IP adresi ayarlamak ve olması toohello VM hello yük devretme sırasında atanmış hello:

    ```
    $vm = Get-SCVirtualMachine -Name <VM_NAME>
    $na = $vm[0].VirtualNetworkAdapters>
    $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
    $ip.address 
    ```

## <a name="changing-ip-addresses"></a>IP adreslerinin değiştirilmesi

Bu senaryoda, yük devri VM'ler hello IP adreslerini değiştirilir. Bu çözümün Hello dezavantajı hello bakım gerekli olmasıdır. Genellikle, çoğaltma sanal makineleri başlattıktan sonra DNS güncelleştirilir. DNS girdilerini değiştirilen toobe ihtiyacınız olabilir ya da thenetwork ve güncelleştirilmiş önbelleğe alınan girdileri fluster. Bu, kapalı kalma sürelerine neden olabilir. Kapalı kalma süresi gibi azaltılabilir:

- Düşük TTL değerleri için intranet uygulamalarını kullanın.
- Bir Site Recovery kurtarma planında, tooupdate hello DNS sunucusu tooensure zamanında güncelleştirme komut dosyası izleyen hello kullanın. Dinamik DNS kaydını kullanırsanız hello komut dosyası gerekmez.

    ```
    param(
    string]$Zone,
    [string]$name,
    [string]$IP
    )
    $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
    $newrecord = $record.clone()
    $newrecord.RecordData[0].IPv4Address  =  $IP
    Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord
    ```
    
### <a name="example"></a>Örnek 

Toouse farklı IP adreslerini hello birincil arasında ve hello kurtarma siteleri planlıyorsanız bir senaryo bakalım. Bu örnekte, farklı IP adreslerini birincil ve ikincil siteler arasında sahibiz ve vardır; hello birincil ya da kurtarma sitesinde barındırılan hangi uygulamaların s üçüncü bir siteden erişilebilir.

- Yük devretme önce uygulamaları barındırılan alt 192.168.1.0/24 hello birincil sitede ve alt ağ 172.16.1.0/24 hello ikincil sitede içinde yapılandırılmış toobe bir yük devretme sonrasında.
- Tüm üç siteleri birbirine erişebilmesi için VPN bağlantıları/ağ yolları uygun şekilde yapılandırılmış.
- Yük devretme sonrasında uygulamaları hello kurtarma alt ağda geri yüklenir. Bu senaryoda hello tüm alt ağ üzerinde hiçbir gerek toofail olduğunu, ve hiçbir değişiklik gerekli tooreconfigure VPN veya ağ yolları. Merhaba yük devretme ve bazı DNS güncelleştirmeleri uygulamaları erişilebilir kaldığından emin olun.
- DNS dinamik güncelleştirmeleri yapılandırılan tooallow ise, hello VM'ler kendilerini yük devretme sonrasında başlattığınızda hello yeni IP adresini kullanarak kaydeder.

**Önce yük devretme**

![Farklı bir IP - yük devretme önce](./media/vmm-to-vmm-walkthrough-network/network-design10.png)

**Yük devretme sonrasında**

![Farklı bir IP - yük devretme sonrasında](./media/vmm-to-vmm-walkthrough-network/network-design11.png)



## <a name="next-steps"></a>Sonraki adımlar

Çok Git[4. adım: hazırlama VMM ve Hyper-V](vmm-to-vmm-walkthrough-vmm-hyper-v.md).


