---
title: "Azure sanal makineler ile kullanılan aaaAzure güvenlik özellikleri | Microsoft Docs"
description: " Azure sanal makinelerle kullanılabilir hello çekirdek Azure güvenlik özelliklerine genel bakış. Sanallaştırma esnekliği toobuy gerek kalmadan hello ve hello VM çalıştıran fiziksel bir donanım hello korumak, azure sanal makineleri verin. "
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 467b2c83-0352-4e9d-9788-c77fb400fe54
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: terrylan
ms.openlocfilehash: 1a1b9f02bd82a2655f4e2e5d9f9ce7a6671f63fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-security-overview"></a>Azure sanal makineleri güvenliğine genel bakış
Azure Sanal Makineler, çok sayıda bilgi işlem çözümünü çevik bir şekilde dağıtmanızı sağlar. Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM, SAP ve Azure BizTalk Hizmetleri desteği sayesinde, istediğiniz iş yükünü istediğiniz dilde ve neredeyse tüm işletim sistemlerinde dağıtabilirsiniz.

Merhaba sanal makine çalışır toobuy gerek kalmadan sanallaştırma esnekliği hello ve hello fiziksel donanım korumak bir Azure sanal makine sağlar.  Derleme ve verilerinizi korumalı ve yüksek güvenlikli bizim veri merkezlerinde güvenli olduğunu hello güvence uygulamalarınızla dağıtın.

Azure ile gelişmiş güvenlik, uyumlu çözümler oluşturabilir:

* Sanal makinelerinizi virüslerden ve kötü amaçlı yazılımlardan koruyun
* Hassas verilerinizi şifreleyin
* Ağ trafiğinin güvenliğini sağlayın
* Tehditleri belirleyin ve tespit edin
* Uyumluluk gereksinimlerini karşılayın

Merhaba, bu makalenin tooprovide sanal makinelerle kullanılabilir hello çekirdek Azure güvenlik özelliklerine genel bakış hedeftir. Daha fazla bilgi için her bir özelliğin ayrıntılarını veren bağlantılar tooarticles de sunuyoruz.  

Merhaba çekirdek Azure sanal makine güvenlik özellikleri toobe bu makalede ele alınan:

* Kötü Amaçlı Yazılımdan Koruma
* Donanım güvenlik modülü
* Sanal makine disk şifrelemesi
* Sanal makine yedekleme
* Azure Site Recovery
* Sanal ağ
* Güvenlik İlkesi Yönetimi ve Raporlama
* Uyumluluk

## <a name="antimalware"></a>Kötü Amaçlı Yazılımdan Koruma
Azure ile Microsoft, Symantec, eğilim mikro ve Kaspersky tooprotect gibi güvenlik satıcılardan kötü amaçlı yazılımdan koruma yazılımı, sanal makineleriniz kötü amaçlı dosyalar, reklam ve diğer tehditlere kullanabilirsiniz. Merhaba toofind altında daha fazla bölüm makaleler öğrenin iş ortağı çözümlerini bakın.

Azure Cloud Services ve sanal makineleri için Microsoft Antimalware tanımlamak ve virüsler, casus yazılım ve diğer kötü amaçlı yazılım kaldırma yardımcı olan gerçek zamanlı koruma bir özelliktir.  Microsoft Antimalware bilinen kötü amaçlı veya istenmeyen yazılım girişimleri tooinstall kendisini veya Azure sistemlerinize çalıştırdığınızda yapılandırılabilir uyarılar sağlar.

Microsoft Antimalware bir tek Aracısı uygulamaları ve Kiracı ortamları için tasarlanmış toorun İnsan aracılığı olmadan hello arka planda çözümüdür. İle ya da temel güvenli--varsayılan olarak, uygulama iş yüklerinin hello gereksinimlerini temel veya Gelişmiş kötü amaçlı yazılımdan koruma izleme de dahil olmak üzere özel yapılandırma koruması dağıtabilirsiniz.

Çekirdek özellikler aşağıdaki hello dağıtmak ve Microsoft Antimalware etkinleştirmek seçtiğinizde kullanılabilir:

* Gerçek zamanlı koruma - monitör etkinliği bulut Hizmetleri ve sanal makineleri toodetect ve blok kötü amaçlı yazılım yürütme.
* Zamanlanmış tarama - etkin olarak çalışan programlar dahil olmak üzere hedeflenen tarama toodetect kötü amaçlı yazılım, düzenli olarak gerçekleştirir.
* Kötü amaçlı yazılım düzeltme - otomatik olarak gerçekleştirilmesi eylem Algılanan kötü amaçlı yazılım silme veya kötü amaçlı dosyaları karantinaya alma ve kötü amaçlı kayıt defteri girdilerini temizleme gibi üzerinde.
* İmza - otomatik olarak yükler hello son koruma imzaları (virüs tanımları) tooensure koruma önceden belirlenen bir frekansında güncel güncelleştirmesidir.
* Kötü amaçlı yazılımdan koruma Altyapısı güncelleştirmeleri – otomatik olarak güncelleştirmeleri Microsoft Antimalware altyapısı hello.
* Kötü amaçlı yazılımdan koruma platformu güncelleştirmeleri – otomatik olarak güncelleştirmeleri Microsoft Antimalware platform hello.
* Etkin bir koruma - algılanan tehditlere ve şüpheli kaynakları tooensure hızlı yanıt ve etkinleştirir gerçek zamanlı zaman uyumlu imza teslim hello Microsoft etkin koruma sistem (MAPS) aracılığıyla hakkında tooAzure telemetri meta verileri raporlar.
* Örnekleri raporlama - sağlar ve örnek raporları toohello Microsoft Antimalware service toohelp hello service ve enable sorun giderme daraltın.
* Dışlamalar – uygulama ve hizmet yöneticileri tooconfigure işlemleri, belirli dosyaları sağlar ve bunları korumadan ve performans ve diğer nedenler için tarama tooexclude sürücüler.
* Kötü amaçlı yazılımdan koruma olay toplama - hello kötü amaçlı yazılımdan koruma hizmeti durumu, kuşkulu etkinlikleri ve hello işletim sistem olay günlüğünde gerçekleştirilecek düzeltme eylemleri kaydeder ve hello müşterinin Azure Storage hesabınıza toplar.

Daha fazla bilgi edinin: toolearn kötü amaçlı yazılımdan koruma yazılımı tooprotect hakkında daha fazla sanal makinelerinizi bakın:

* [Azure bulut Hizmetleri ve sanal makineleri için Microsoft kötü amaçlı yazılımdan koruma](azure-security-antimalware.md)
* [Azure Sanal Makinelerinde Kötü Amaçlı Yazılıma Karşı Koruma Çözümleri Dağıtma](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Nasıl tooinstall ve bir Windows VM bir hizmet olarak eğilimi mikro derin güvenliği yapılandırma](../virtual-machines/windows/classic/install-trend.md)
* [Nasıl tooinstall ve Symantec Endpoint Protection bir Windows VM yapılandırma](../virtual-machines/windows/classic/install-symantec.md)
* [Hello Azure Marketi güvenlik çözümleri](https://azure.microsoft.com/marketplace/?term=security)

## <a name="hardware-security-module"></a>Donanım güvenlik modülü
Şifreleme ve kimlik doğrulama korumaları anahtar güvenlik geliştirerek geliştirilebilir. Azure anahtar kasası depolayarak hello yönetim ve güvenlik kritik parolaları ve anahtarlar basitleştirebilirsiniz. Anahtar kasası hello seçeneği toostore anahtarlarınızı donanım güvenlik modülleri (HSM'ler) sertifikalı tooFIPS 140-2 Düzey 2 standartları de sağlar. SQL Server şifreleme anahtarları için yedekleme veya [saydam veri şifreleme](https://msdn.microsoft.com/library/bb934049.aspx) herhangi bir anahtar veya gizli, uygulamalardan ile anahtar kasasına tüm depolanabilir. İzinler ve erişim toothese korunan öğeleri üzerinden yönetilir [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).

Daha fazla bilgi edinin:

* [Azure anahtar kasası nedir?](../key-vault/key-vault-whatis.md)
* [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md)
* [Azure anahtar kasası blogu](https://blogs.technet.microsoft.com/kv/)

## <a name="virtual-machine-disk-encryption"></a>Sanal makine disk şifrelemesi
Azure Disk şifrelemesi, Windows ve Linux Azure sanal makine diskleriniz şifrelemek olanak sağlayan yeni bir özelliktir. Azure Disk şifrelemesi kullanır hello endüstri standardı [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) özelliği Windows hello ve [dm-crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello işletim sistemi ve hello veri diskleri için Linux tooprovide birim şifrelemesi özelliğidir.

Merhaba çözüm denetlemek ve hello disk şifreleme anahtarları ve gizli anahtarları Azure depolama alanınızı bekleyen hello sanal makine disklerdeki tüm veriler şifrelenir sağlarken anahtar kasası aboneliğinizi yönetmek Azure anahtar kasası toohelp tümleşiktir.

Daha fazla bilgi edinin:

* [Windows ve Linux Iaas VM'ler için Azure Disk şifrelemesi](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)
* [Linux ve Windows sanal makineler için Azure Disk şifrelemesi](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/azure-disk-encryption-for-linux-and-windows-virtual-machines-public-preview-now-available/)
* [Bir sanal makine şifrele](../security-center/security-center-disk-encryption.md)

## <a name="virtual-machine-backup"></a>Sanal makine yedekleme
Azure Yedekleme, uygulama verilerinizi sıfır sermaye yatırımı ve en az işletim maliyetiyle koruyan ölçeklenebilir bir çözümdür. Uygulama hataları verilerinizi bozabilir ve insan hataları, uygulamalarınızda hatalar oluşturabilir. Azure Backup ile Windows ve Linux çalıştıran sanal makinelerinizi korunur.

Daha fazla bilgi edinin:

* [Azure Backup nedir?](../backup/backup-introduction-to-azure-backup.md)
* [Azure yedekleme öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/backup/)
* [Azure Backup hizmeti - SSS](../backup/backup-azure-backup-faq.md)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Kuruluşunuzun BCDR stratejisinin önemli bir parçası tookeep kurumsal iş yüklerini ve uygulamaları kurma ve Planlı çalışan ve planlanmayan kesintiler meydana nasıl çıkışı çıkarılıyor. Azure Site Recovery birincil konumunuz çökmesi durumunda ikincil konum kullanılabilir olacak şekilde, çoğaltma, yük devretme ve kurtarma iş yüklerini ve uygulamaları düzenlemek yardımcı olur.

Site Recovery:

* **BCDR stratejinize basitleştirir** — Site Recovery kılar kolay toohandle çoğaltma, yük devretme ve tek bir konumdan birden çok iş yükünün ve uygulamanın kurtarılması. Site Recovery, çoğaltma ve yük devretme işlemlerini düzenler ancak uygulama verilerinize müdahale etmez veya uygulamanız hakkında bilgiler toplamaz.
* **Esnek çoğaltma sağlar** — Site Recovery kullanarak Hyper-V sanal makineleri, VMware sanal makineleri ve Windows/Linux fiziksel sunucularında çalışan iş yüklerini çoğaltabilir.
* **Yük devretme ve kurtarma destekler** — Site Recovery sağlayan yük devretme sınaması işlemlerini toosupport olağanüstü durum kurtarma ayrıntılarını üretim ortamlarını etkilemeden. Ayrıca, beklenen kesintilere yönelik olarak sıfır veri kaybı sunan planlanan yük devretmeler veya beklenmeyen olağanüstü durumlar için minimum düzeyde veri kaybıyla sonuçlanan (çoğaltma sıklığına bağlı olarak) planlanmamış yük devretmeler çalıştırabilirsiniz. Yük devretme sonrasında yeniden çalışma tooyour birincil siteleri kullanabilirsiniz. Yük devretme işlemini özelleştirebilmeniz ve çok katmanlı uygulamaları kurtarabilmeniz için Site Recovery, betikleri ve Azure otomasyonu çalışma kitaplarını içeren kurtarma planları sunar.
* **İkincil veri merkezine ortadan** — tooa ikincil şirket içi site veya tooAzure çoğaltabilirsiniz. Olağanüstü durum kurtarma için hedef olarak azure'da hello maliyet ve bir ikincil site Bakımı karmaşıklığını ortadan kaldırır. Çoğaltılan veriler Azure depolama alanında depolanır.
* **Var olan BCDR teknolojileri ile tümleşir** — Site Recovery iş ortaklarına, diğer uygulama BCDR özellikleriyle. Örneğin, Site Recovery tooprotect hello SQL Server arka uç kurumsal iş yüklerinin kullanabilirsiniz. Bu SQL Server AlwaysOn Kullanılabilirlik grupları hello devretmesini toomanage için yerleşik destek içerir.

Daha fazla bilgi edinin:

* [Azure Site Recovery nedir?](../site-recovery/site-recovery-overview.md)
* [Azure Site Recovery nasıl çalışır?](../site-recovery/site-recovery-components.md)
* [Hangi iş yüklerini Azure Site Recovery tarafından korunan?](../site-recovery/site-recovery-workload.md)

## <a name="virtual-networking"></a>Sanal ağ
Sanal makinelerin ağ bağlantısı gerekir. toosupport bu gereksinim, Azure gerektirir bağlı sanal makineleri toobe tooan Azure sanal ağı. Bir Azure sanal ağı hello Azure fiziksel ağ yapısında en üstünde oluşturulmuş mantıksal bir yapıdır. Her mantıksal Azure sanal tüm diğer Azure sanal ağlardan yalıtılmış bir ağdır. Bu yalıtım dağıtımlarınızı ağ trafiğini değil erişilebilir tooother Microsoft Azure müşterilerin olduğunu güvence altına yardımcı olur.

Daha fazla bilgi edinin:

* [Azure ağ güvenliğine genel bakış](security-network-overview.md)
* [Sanal ağ genel bakış](../virtual-network/virtual-networks-overview.md)
* [Ağ özellikleri ve kuruluş senaryolarına yönelik ortaklıkları](https://azure.microsoft.com/blog/networking-enterprise/)

## <a name="security-policy-management-and-reporting"></a>Güvenlik İlkesi Yönetimi ve Raporlama
Azure Güvenlik Merkezi, engellemenize, algılamanıza ve toothreats yanıt yardımcı olur ve artan, görünürlük ve denetim üzerinden, Azure kaynaklarınızın hello güvenlik sağlar. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Azure Güvenlik Merkezi iyileştirmek ve sanal makine güvenliği tarafından izlemenize yardımcı olur:

* Sanal makine sağlama [güvenlik önerileri](../security-center/security-center-recommendations.md) gibi sistem güncelleştirmeleri uygulamak gibi ACL'ler uç noktalarını yapılandırma, kötü amaçlı yazılımdan koruma etkinleştirmek, ağ güvenlik gruplarını etkinleştirmek ve disk şifrelemesi uygulayın.
* Sanal makinelerinizi Hello durumunu izleme

Daha fazla bilgi edinin:

* [Giriş tooAzure Güvenlik Merkezi](../security-center/security-center-intro.md)
* [Azure Güvenlik Merkezi sık sorulan sorular](../security-center/security-center-faq.md)
* [Azure Güvenlik Merkezi planlama ve işlemler](../security-center/security-center-planning-and-operations-guide.md)

## <a name="compliance"></a>Uyumluluk
Azure sanal makineleri FISMA, FedRAMP, HIPAA, PCI DSS düzey 1 ve diğer anahtar uyumluluk programları için sertifikalıdır. Bu sertifika, iş tooaddress ve kendi Azure uygulamalarını toomeet uyumluluk gereksinimleri için çok çeşitli yurtiçi ve uluslararası yönetmelik gereksinimlerine kolaylaştırır.

Daha fazla bilgi edinin:

* [Microsoft Güven Merkezi: uyumluluk](https://www.microsoft.com/TrustCenter/Compliance/default.aspx)
* [Güvenilir bulut: Microsoft Azure güvenlik, gizlilik ve uyumluluk](http://download.microsoft.com/download/1/6/0/160216AA-8445-480B-B60F-5C8EC8067FCA/WindowsAzure-SecurityPrivacyCompliance.pdf)
