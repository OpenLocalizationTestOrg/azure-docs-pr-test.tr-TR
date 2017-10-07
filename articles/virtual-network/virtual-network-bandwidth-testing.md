---
title: "aaaTesting Azure VM ağ verimliliği | Microsoft Docs"
description: "Nasıl tootest Azure sanal makine ağ verimliliği öğrenin."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/21/2017
ms.author: steveesp
ms.openlocfilehash: 2da85c27bc8d16a443b215891f4cd0460f41926f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="bandwidththroughput-testing-ntttcp"></a>Bant genişliği/işleme (NTTTCP) test etme

Azure'da ağ verimliliği performansından test ederken, en iyi toouse test hello ağ hedefler ve performansı etkileyen diğer kaynakları hello kullanımını en aza indirir bir araç olan. NTTTCP önerilir.

Merhaba aracı tootwo hello Azure Vm'leri kopyalamak aynı boyutta. Bir VM GÖNDERENİ ve ALICISI olarak diğer hello görür.

#### <a name="deploying-vms-for-testing"></a>Test etmek için sanal makineleri dağıtma
Bu test amacıyla Merhaba, iki VM bulunmalıdır hello aynı bulut hizmetine hello ya da aynı kullanılabilirlik kümesi, böylece biz kendi iç IP'leri kullanın ve hello yük dengeleyici hello testten hariç hello. Merhaba VIP ile olası tootest, ancak bu tür sınama hello bu belgenin kapsamı dışında gelir.
 
Merhaba ALICININ IP adresini not edin. Şimdi bu IP "a.b.c.r" çağırın

Merhaba VM üzerinde hello çekirdek sayısı not edin. Şimdi bu çağırın "\#num\_çekirdek"
 
Hello NTTTCP 300 saniye (veya 5 dakika) test VM hello gönderici ve alıcı VM çalıştırın.

İpucu: Bu test hello için ilk kez ayarlarken, daha kısa bir test dönemi tooget geri bildirim er deneyebilirsiniz. Merhaba aracı beklendiği gibi çalıştığını sonra hello test dönemi too300 saniye hello en doğru sonuçlar için genişletir.

> [!NOTE]
> Merhaba gönderen **ve** alıcı belirtmelisiniz **aynı hello** süresi parametresi test (-t).

10 saniye için tek bir TCP akış tootest:

Alıcı parametreleri: ntttcp - r -t 10 - P 1

Gönderen parametreleri: ntttcp-s10.27.33.7 -t 10 - n 1 -P 1

> [!NOTE]
> Örnek önceki hello kullanılan tooconfirm yapılandırmanızı yalnızca olmalıdır. Sınama geçerli örnekleri bu belgenin sonraki bölümlerinde ele alınmaktadır.

## <a name="testing-vms-running-windows"></a>WINDOWS çalıştıran VM'ler sınama:

#### <a name="get-ntttcp-onto-hello-vms"></a>NTTTCP VM'ler hello alın.

Merhaba en son sürümünü indirin: <https://gallery.technet.microsoft.com/NTttcp-Version-528-Now-f8b12769>

Ya da onu taşınsa arayın: <https://www.bing.com/search?q=ntttcp+download> \< --ilk isabet

C: gibi ayrı bir klasör içinde NTTTCP yerleştirmeyi düşünün\\araçları

#### <a name="allow-ntttcp-through-hello-windows-firewall"></a>NTTTCP hello Windows Güvenlik Duvarı aracılığıyla izin ver
Hello alıcı, NTTTCP trafiği tooarrive hello Windows Güvenlik Duvarı tooallow üzerinde izin verme kuralı oluşturun. Tooallow belirli TCP bağlantı noktalarını gelen yerine onu kolay tooallow hello tüm NTTTCP ada göre programdır.

Bu gibi hello Windows Güvenlik Duvarı aracılığıyla ntttcp izin ver:

Netsh advfirewall güvenlik duvarı kuralı program Ekle =\<yolu\>\\ntttcp.exe adı "ntttcp" protocol = tüm dir = Action = etkinleştir izin yes profile = = ANY

Örneğin, ntttcp.exe toohello kopyaladıysanız "c:\\Araçları" klasörü, bu hello komutu olacaktır: 

Netsh advfirewall güvenlik duvarı kuralı program Ekle = c:\\Araçları\\ntttcp.exe adı "ntttcp" protocol = tüm dir = eylemde = = etkinleştir izin yes profile = = ANY

#### <a name="running-ntttcp-tests"></a>NTTTCP testlerini çalıştırma

Alıcı hello üzerinde NTTTCP Başlat (**CMD'den çalıştırmak**PowerShell dosyalardan değil):

ntttcp - r – m [2\*\#num\_çekirdek],\*, a.b.c.r -t 300

Merhaba VM dört çekirdek ve 10.0.0.4 IP adresi varsa, onu şöyle olabilir:

ntttcp - r – m 8,\*, 10.0.0.4 -t 300


GÖNDEREN hello üzerinde NTTTCP Başlat (**CMD'den çalıştırmak**PowerShell dosyalardan değil):

ntttcp -s-m 8,\*, 10.0.0.4 -t 300 

Merhaba sonuçları için bekleyin.


## <a name="testing-vms-running-linux"></a>LINUX çalıştıran Vm'leri sınama:

Linux için nttcp kullanın. Kullanılabilir <https://github.com/Microsoft/ntttcp-for-linux>

Hello Linux VM'ler (GÖNDERENİ ve ALICISI), ntttcp için linux Vm'lerinizi üzerinde hazırlamak için şu komutları çalıştırın:

CentOS - yükleme Git:
``` bash
  yum install gcc -y  
  yum install git -y
```
Ubuntu - yükleme Git:
``` bash
 apt-get -y install build-essential  
 apt-get -y install git
```
Olun ve hem de yükleyin:
``` bash
 git clone <https://github.com/Microsoft/ntttcp-for-linux>
 cd ntttcp-for-linux/src
 make && make install
```

Merhaba Windows örnekteki biz hello Linux ALICININ IP 10.0.0.4 olduğunu varsayalım.

Linux için NTTTCP alıcı hello üzerinde başlatın:

``` bash
ntttcp -r -t 300
```

Ve hello gönderen, çalıştırın:

``` bash
ntttcp -s10.0.0.4 -t 300
```
 
Test uzunluğu Varsayılanları too60 saniye hiçbir zaman parametresi, verilen

## <a name="testing-between-vms-running-windows-and-linux"></a>Windows ve LINUX çalıştıran VM'ler arasında sınama:

Merhaba test çalıştırabilmeniz için bu senaryoları biz hello eşitlemesi modu etkinleştirmeniz gerekir. Bu hello kullanarak yapılır **-N bayrağı** Linux için ve **-ns bayrağı** Windows için.

#### <a name="from-linux-toowindows"></a>Linux tooWindows:

Alıcı <Windows>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Windows server IP>
```

Gönderen <Linux> :

``` bash
ntttcp -s -m <2 x nr cores>,*,<Windows server IP> -N -t 300
```

#### <a name="from-windows-toolinux"></a>Windows tooLinux:

Alıcı <Linux>:

``` bash
ntttcp -r -m <2 x nr cores>,*,<Linux server IP>
```

Gönderen <Windows>:

``` bash
ntttcp -s -m <2 x nr cores>,*,<Linux  server IP> -ns -t 300
```

## <a name="next-steps"></a>Sonraki adımlar
* Sonuçlar bağlı olarak, olabilir oda çok[ağ verimliliği makineler en iyi duruma getirme](virtual-network-optimize-network-bandwidth.md) senaryonuz için.
* Daha fazla bilgi edinin [Azure Virtual Network sık sorulan sorular (SSS)](virtual-networks-faq.md)
