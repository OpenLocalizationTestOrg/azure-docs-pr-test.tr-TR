---
title: "Site Recovery ile Hyper-V VM çoğaltması için aaaPlan ağ eşlemesi | Microsoft Docs"
description: "Hyper-V sanal makine çoğaltmasını bir şirket içi veri merkezi tooAzure veya tooa ikincil site için Ağ eşlemesi ayarlayın."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: tysonn
ms.assetid: fcaa2f52-489d-4c1c-865f-9e78e000b351
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/23/2017
ms.author: raynew
ms.openlocfilehash: 86199b5840ea10fd33630bcc75d14340a49e01bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-network-mapping-for-hyper-v-vm-replication-with-site-recovery"></a>Ağ eşlemesi Site Recovery ile Hyper-V VM çoğaltması için planlama



Bu makale, toounderstand ve Hyper-V sanal makineleri tooAzure veya tooa ikincil sitenin çoğaltma sırasında eşleme, hello kullanarak ağ planlamanıza yardımcı olur [Azure Site Recovery hizmeti](site-recovery-overview.md).

Okuma sonra bu makalede, bu makalenin hello altındaki tüm yorumlar gönderin ya da hello hakkında teknik sorular sormak [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="network-mapping-for-replication-tooazure"></a>Ağ eşlemesi çoğaltma tooAzure için

Ağ eşlemesi, Hyper-V Vm'lerini (VMM yönetilen) tooAzure çoğaltırken kullanılır. Bir kaynak VMM sunucusunda VM ağları arasındaki eşlemeyi eşlemeleri ağ ve hedef Azure ağları. Eşleme aşağıdaki hello:

- **Ağ bağlantısı**— çoğaltılan Azure Vm'lerinin bağlı toohello eşlenen ağ olmasını sağlar. Merhaba üzerinde aynı yük devri tüm makineler bunlar farklı kurtarma planları devredilir olsa bile ağ tooeach diğer bağlanabilir.
- **Ağ geçidi**— bir ağ geçidi hello hedef Azure ağında ayarlanıp ayarlanmadığını VM'ler tooother şirket içi sanal makinelere bağlanabilir.

Şunlara dikkat edin:

- Kaynak VMM VM ağ tooan Azure sanal ağı eşleyin.
- Merhaba, Azure Vm'lerinin yük devretme sonrasında kaynak ağ bağlı toohello eşlenmiş hedef sanal ağ olacaktır.
- Yeni VM'ler eklenen toohello kaynak VM ağına bağlı Çoğaltma gerçekleştiğinde eşlenen Azure ağ toohello.
- Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri olan hello adıyla aynı alt ağda hangi hello kaynak sanal makinenin bulunduğu sonra hello çoğaltma sanal makinesi yük devretme sonrasında toothat hedef alt bağlanır.
- Eşleşen ada sahip bir hedef alt ağ varsa, hello sanal makine toohello hello ağdaki ilk alt ağa bağlanır.


## <a name="network-mapping-for-replication-tooa-secondary-datacenter"></a>Ağ eşlemesi için çoğaltma tooa ikincil veri merkezi

Ağ eşleme (System Center Virtual Machine Manager (VMM) yönetilen) Hyper-V sanal makineleri tooa ikincil veri merkezine çoğaltma yapılırken kullanılır. Bir kaynak VMM sunucusunda VM ağları ve bir hedef VMM sunucusunda VM ağları arasında ağ eşlemesi eşler. Eşleme aşağıdaki hello:

- **Ağ bağlantısı**— bağlayan VM'ler tooappropriate ağları yük devretme sonrasında. Merhaba çoğaltma VM eşlenen toohello kaynak ağ bağlantılı toohello hedef ağ olacaktır.
- **En iyi yerleştirme**— yerler çoğaltma sanal makineleri Hyper-V ana bilgisayar sunucuları üzerinde en iyi şekilde hello. Çoğaltma sanal makineleri erişim hello eşlenen, VM ağları konaklarda yerleştirilir.
- **Ağ eşleme**— ağ eşlemesini yapılandırmazsanız, yük devretme sonrasında çoğaltma sanal makineleri bağlı tooany VM ağları olmayacaktır.

Şunlara dikkat edin:

- Ağ eşlemesi iki VMM sunucusu üzerinde VM ağları arasındaki yapılandırılabilir veya iki site tarafından yönetilen, tek bir VMM sunucusunda aynı hello sunucu.
- Eşleme doğru bir şekilde yapılandırıldığından ve çoğaltma etkin olduğunda, bir VM hello birincil konumda bağlı tooa ağ olacaktır ve onun çoğaltması hello hedef konumda bağlı tooits ağ eşlenmiş.
-
- Bir hedef VM ağı sırasında ağ eşlemesini seçtiğinizde ağlar doğru VMM'de ayarlanan, hello kaynak VM ağı kullanan hello VMM kaynak Bulutları, hello kullanılabilir hedef VM ağları için kullanılan hello hedef Bulutları ile birlikte görüntülenir koruma.
- Merhaba hedef ağ birden çok alt ağı varsa ve bu alt ağlardan biri üzerinde hangi hello kaynak sanal makinenin bulunduğu alt ağ hello gibi aynı adı sonra hello hello çoğaltma sanal makinesi yük devretme sonrasında bağlı toothat hedef alt olacaktır. Eşleşen ada sahip bir hedef alt ağ ise hello sanal makineye bağlı toohello hello ağdaki ilk alt ağ olacaktır.



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



## <a name="next-steps"></a>Sonraki adımlar

Hakkında bilgi edinin [hello ağ altyapısını planlama](site-recovery-network-design.md).
