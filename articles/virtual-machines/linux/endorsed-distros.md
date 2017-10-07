---
title: "Linux aaaEndorsed dağıtımları | Microsoft Docs"
description: "Linux hakkında Ubuntu ve CentOS, Oracle ve SUSE için yönergeler de dahil olmak üzere, Azure destekli dağıtımlar hakkında bilgi edinin."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: 2777a526-c260-4cb9-a31a-bdfe1a55fffc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: f006972d4611434c62b72a1d8df60caf753e15f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-on-distributions-endorsed-by-azure"></a>Linux üzerinde tarafından Azure destekli dağıtımlar
İş ortakları hello Azure Marketi Linux görüntüleri sağlar. Daha fazla özellikleri toohello destekli dağıtım listesi ile çeşitli Linux toplulukları tooadd çalışıyoruz. Hello sırada olmayan için dağıtımları hello Market, bulunan her zaman kendi Linux hello yönergeleri izleyerek getirebilir [oluşturma ve hello Linux işletim sistemiiçerenbirsanalsabitdiskkarşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="supported-distributions-and-versions"></a>Desteklenen dağıtımları ve sürümleri
Merhaba aşağıdaki tabloda hello Linux dağıtımları ve Azure üzerinde desteklenen sürümleri listelenmiştir. Çok başvuran[Linux desteği görüntüleri Microsoft Azure'da](https://support.microsoft.com/en-us/kb/2941892) daha ayrıntılı bilgi için.

Hyper-V ve Azure Hello Linux Tümleştirme hizmetleri (LIS) sürücüleri Microsoft doğrudan toohello Yukarı Akış Linux çekirdek katkı çekirdek modülleri edilir.  Bazı LIS sürücüleri hello dağıtım'ın çekirdeğe varsayılan olarak oluşturulur. Red Hat Enterprise (RHEL) tabanlı eski dağıtımları / CentOS ayrı bir yükleme olarak kullanılabilir [Hyper-V için Linux Tümleştirme hizmetleri sürümü 4.1](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409). Bkz: [Linux çekirdek gereksinimleri](create-upload-generic.md#linux-kernel-requirements) hello LIS sürücüleri hakkında daha fazla bilgi için.

Hello Azure Linux Aracısı'hello Azure Marketi görüntülerinde önceden yüklü olan ve hello dağıtım'ın paket depodan genellikle kullanılabilir. Kaynak kodu bulunabilir [GitHub](https://github.com/azure/walinuxagent).

| Dağıtım | Sürüm | Sürücüler | Aracı |
| --- | --- | --- | --- |
| CentOS |CentOS 6.3 + 7.0 + |CentOS 6.3: [LIS indirin](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409)<p>CentOS 6.4 +: çekirdek |Paketi: İçinde [repo](http://olcentgbl.trafficmanager.net/openlogic/6/openlogic/x86_64/RPMS/) "WALinuxAgent" altında <br/>Kaynak kodu: [GitHub](https://github.com/Azure/WALinuxAgent) |
| [CoreOS](https://coreos.com/docs/running-coreos/cloud-providers/azure/) |494.4.0+ |Çekirdek |Kaynak kodu: [GitHub](https://github.com/coreos/coreos-overlay/tree/master/app-emulation/wa-linux-agent) |
| Debian |Debian 7,9 +, 8.2 + |Çekirdek |Paketi: "waagent" altında bağlantıların bulunması <br/>Kaynak kodu: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Oracle Linux |6.4+, 7.0+ |Çekirdek |Paketi: "WALinuxAgent" altında bağlantıların bulunması <br/>Kaynak kodu: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| Red Hat Enterprise Linux |RHEL 6.7 + 7.1 + |Çekirdek |Paketi: "WALinuxAgent" altında bağlantıların bulunması <br/>Kaynak kodu: [GitHub](https://github.com/Azure/WALinuxAgent) |
| SUSE Linux Enterprise |SLES/SLES SAP için<br>11 SP4<br>12 SP1 +|Çekirdek |Paketi:<p> 11 inç için [bulut: Araçlar](https://build.opensuse.org/project/show/Cloud:Tools) deposu<br>için "Genel bulut" modülünde "python-azure-agent" altında bulunan 12<br/>Kaynak kodu: [GitHub](http://go.microsoft.com/fwlink/p/?LinkID=250998) |
| openSUSE |openSUSE artık 42.1 + |Çekirdek |Paketi: İçinde [bulut: Araçlar](https://build.opensuse.org/project/show/Cloud:Tools) "python-azure-agent" altında deposu <br/>Kaynak kodu: [GitHub](https://github.com/Azure/WALinuxAgent) |
| Ubuntu |Ubuntu 12.04, 14.04, 16.04, 16.10 |Çekirdek |Paketi: "walinuxagent" altında bağlantıların bulunması <br/>Kaynak kodu: [GitHub](https://github.com/Azure/WALinuxAgent) |

## <a name="partners"></a>İş Ortakları

### <a name="coreos"></a>CoreOS
[https://CoreOS.com/docs/Running-CoreOS/cloud-providers/Azure/](https://coreos.com/docs/running-coreos/cloud-providers/azure/)

Merhaba CoreOS Web sitesinden:

*CoreOS güvenlik, tutarlılık ve güvenilirlik için tasarlanmıştır. Paketleri yum aracılığıyla veya apt yüklemek yerine, CoreOS Linux kapsayıcıları toomanage hizmetlerinizi daha yüksek bir soyutlama düzeyinde kullanır. Tek bir hizmetin kodu ve tüm bağımlılıkları, bir veya daha çok CoreOS makinelerde çalıştırılabilir bir kapsayıcıdaki paketlenir.*

### <a name="credativ"></a>Credativ
[http://www.credativ.co.uk/credativ-blog/debian-images-Microsoft-Azure](http://www.credativ.co.uk/credativ-blog/debian-images-microsoft-azure)

Credativ bağımsız danışmanlık ve ücretsiz yazılımlar kullanarak hello geliştirme ve profesyonel çözümleri uyarlamasını uzmanlaşmış Hizmetleri şirket ' dir. Önde gelen açık kaynak uzmanlarıyla Credativ destek kullanan çok sayıda BT departmanları ile uluslararası tanıma sahip. Microsoft ile birlikte Credativ şu anda karşılık gelen Debian görüntüleri Debian 8 (Jessie) ve Debian için 7 (Wheezy) önce hazırlanıyor. Her iki görüntüleri özel olarak tasarlanmış toorun Azure ile ilgili olan ve hello platform kolayca yönetilebilir. Credativ hello uzun süreli Bakım ve kendi açık kaynak destek merkezleri aracılığıyla Azure hello Debian görüntülerini güncelleştirme de destekler.

### <a name="oracle"></a>Oracle
[http://www.Oracle.com/technetwork/topics/cloud/FAQ-1963009.HTML](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html)

Oracle'nın, toooffer çözümleri ortak ve özel Bulutlar için geniş bir yelpazesini stratejidir. Merhaba stratejisi müşteriler seçim ve bunlar Oracle bulutlarındaki Oracle yazılım ve diğer Bulutları nasıl dağıtıldığına esneklik sağlar. Microsoft Oracle'nın yöneticileriyle müşteriler toodeploy Oracle Microsoft Genel ve özel Bulutlar yazılımda sertifika ve Oracle Destek'ten hello güvenle sağlar.  Oracle'nın taahhüt ve Oracle ortak ve özel bulut çözümleri yatırım değişmez.

### <a name="red-hat"></a>Red Hat
[http://www.RedHat.com/en/partners/Strategic-Alliance/Microsoft](http://www.redhat.com/en/partners/strategic-alliance/microsoft)

açık kaynak çözümlerinin dünyanın en önde gelen sağlayıcısı Merhaba, Red Hat birden fazla % 90'ını iş sorunlarını çözmesine, kendi BT Hizala Fortune 500 şirketleri yardımcı olur ve iş stratejilerini ve teknoloji hello gelecek için hazırlayın. Red Hat bunu bir açık iş modeli ve uygun maliyetli, tahmin edilebilir abonelik modeli aracılığıyla güvenli çözümler sağlayarak gerçekleştirir.

### <a name="suse"></a>SUSE
[http://www.SuSE.com/SuSE-Linux-Enterprise-Server-on-Azure](http://www.suse.com/suse-linux-enterprise-server-on-azure)

SUSE Linux Enterprise Server Azure ile ilgili üst düzey güvenilirlik ve güvenlik için bulut sağlayan bir kanıtlanmış platformudur. SUSE'ın çok yönlü Linux platformuna kolayca yönetilebilir bulut ortamı Azure bulut Hizmetleri toodeliver ile sorunsuz şekilde entegre olur. SUSE Linux Enterprise Server için 1800'den fazla bağımsız yazılım satıcılarından birden fazla 9,200 sertifikalı uygulamaları ile desteklenen hello veri merkezinde çalışan iş yüklerini güvenle Azure'da dağıtılabilir SUSE sağlar.

### <a name="canonical"></a>Canonical
[http://www.ubuntu.com/cloud/Azure](http://www.ubuntu.com/cloud/azure)

Kurallı mühendislik ve açık bir topluluk idare sürücü Ubuntu'nın başarılı olan istemci, sunucu ve bulut tüketicileri için kişisel bulut hizmetlerini içerir. Kurallı'nin sunulmasıyla birleştirilmiş ve ücretsiz platformundan Ubuntu içinde telefon toocloud hello telefon, tablet, TV ve Masaüstü için tutarlı arabirimleri ailesi sağlar. Bu Vizyon tüketici elektronik olarak genel bulut sağlayıcıları toohello alıcılar öğesinden farklı kurumlar için Ubuntu hello ilk seçim ve sık kullanılan tek tek ekiplerindeki arasında hale getirir.

Geliştiriciler ve Merhaba Dünya mühendislik merkezleri ile Canonical donanım üreticileri, içerik sağlayıcıları ve yazılım geliştiriciler toobring Ubuntu çözümleri toomarket PC'ler, sunucular ve el aygıtları için benzersiz olarak konumlandırılmış toopartner içindir.
