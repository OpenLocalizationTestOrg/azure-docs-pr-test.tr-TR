---
title: "Site kurtarma aaaAzure Azure Azure çoğaltma sorunlarını ve hataları için sorun giderme | Microsoft Docs"
description: "Olağanüstü durum kurtarma için Azure sanal makineleri çoğaltırken hatalarını ve sorunlarını giderme"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Azure Azure VM çoğaltma sorunlarını giderme

Bu makalede çoğaltılması ve tek bir bölge tooanother bölgesinden Azure sanal makinelerini kurtarma Azure Site kurtarma hello yaygın sorunları açıklar ve açıklar nasıl tootroubleshoot bunları. Desteklenen yapılandırmalar hakkında daha fazla bilgi için bkz: Merhaba [Azure Vm'lerini çoğaltma için destek matrisi](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Azure kaynak kotası sorunları (hata kodu 150097)
Aboneliğinizi etkin toocreate Azure VM'ler olağanüstü durum kurtarma bölgeniz olarak toouse planlama hello hedef bölgede olmalıdır. Ayrıca, aboneliğiniz olmalıdır yeterli etkin kotası toocreate VM'ler belirli büyüklükte. Varsayılan olarak, Site Recovery Çekmeleri hello hedef kaynak VM hello olarak VM için aynı boyutta hello. Merhaba eşleşen boyutu kullanılabilir değilse, hello yakın olası boyutu otomatik olarak çekilir. Kaynak VM yapılandırmayı destekleyen eşleşen boyut ise, bu hata iletisi görüntülenir:

**Hata kodu** | **Olası nedenler** | **Öneri**
--- | --- | ---
150097<br></br>**İleti**: VmName hello sanal makinesi için çoğaltma etkinleştirilemedi. | -Kimliği olmayabilir aboneliğiniz toocreate hello hedef bölge konumda herhangi bir VM etkin.</br></br>-Abonelik Kimliğinizi etkinleştirilmemiş veya yeterli kota toocreate belirli VM boyutları hello hedef bölge konumunda yok.</br></br>-Merhaba kaynak VM NIC sayısı (2) ile eşleşen uygun hedef VM boyutu hello abonelik kimliği için hello hedef bölge konumunda bulunan değil.| Kişi [Azure Fatura Desteği](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable VM oluşturmak için hello hello hedef konumdaki VM boyutlarını, aboneliğiniz için gerekli. Bu özellik etkinleştirildikten sonra yeniden deneme hello işlemi başarısız oldu.

### <a name="fix-hello-problem"></a>Merhaba sorunu düzeltin
Sizinle iletişim [Azure Fatura Desteği](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable, abonelik toocreate hello hedef konumda gerekli boyutlarda VM'ler.

Merhaba hedef konumu bir kapasite kısıtlaması yoksa, çoğaltmayı devre dışı bırakın ve aboneliğinizi yeterli kota toocreate hello gerekli boyutlarda VM'ler sahip olduğu tooa farklı bir konuma etkinleştirin.

## <a name="trusted-root-certificates-error-code-151066"></a>Güvenilen kök sertifikaları (hata kodu 151066)

Tüm hello son güvenilen kök sertifikalar hello VM üzerinde mevcut değilse, "çoğaltma etkinleştir" işinizi başarısız olabilir. Merhaba sertifikalar, hello kimlik doğrulama ve yetkilendirme Site Recovery hizmeti olmadan hello VM gelen çağrıları başarısız. Merhaba hello başarısız oldu "çoğaltma etkinleştir" Site kurtarma işi için hata iletisi görüntülenir:

**Hata kodu** | **Olası neden** | **Öneriler**
--- | --- | ---
151066<br></br>**İleti**: Site Recovery yapılandırma başarısız oldu. | yetkilendirme için kullanılan güvenilir kök sertifikaları Hello gerekli ve kimlik doğrulama hello makinede mevcut değil. | -Merhaba Windows işletim sistemi çalıştıran bir VM için o hello kök sertifikaları hello makinede güvenilir emin olun. Bilgi için bkz: [yapılandırma Güvenilen Kökleri ve izin verilmeyen sertifikaları](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Merhaba Linux işletim sistemi çalıştıran bir VM için hello Linux işletim sistemi sürümü dağıtımcı tarafından yayımlanan güvenilen kök sertifikalar için hello yönergeleri izleyin.

### <a name="fix-hello-problem"></a>Merhaba sorunu düzeltin
**Windows**

Böylece tüm hello güvenilen kök sertifikalar hello makinede bulunan tüm hello en son Windows güncelleştirmeleri hello VM üzerinde yükleyin. Bağlantısı kesilmiş bir ortamda değilseniz, hello standart Windows update işleminde kuruluş tooget hello sertifikalarınızı izleyin. Merhaba sertifikaları hello VM üzerinde mevcut değil gerekirse hello çağrıları toohello Site Recovery hizmeti güvenlik nedenleriyle başarısız.

Merhaba tipik Windows update Yönetimi veya sertifika güncelleştirme yönetimi işleminin tüm hello son kök sertifikaları ve güncelleştirilmiş hello sertifika iptal listesi, kuruluş tooget hello VM'ler üzerinde izleyin.

sorunu hello tooverify çözümlenir, bir tarayıcıdan, VM'deki toologin.microsoftonline.com gidin.

**Linux**

Linux dağıtıcı tooget hello son güvenilen kök sertifikaları ve hello son sertifika iptal listesi hello VM üzerinde tarafından sağlanan hello yönergeleri izleyin.

SuSE Linux simgesel bağlantı toomaintain sertifika listesini kullandığından, aşağıdaki adımları izleyin:

1.  Kök kullanıcı olarak oturum açın.

2.  Şu komutu çalıştırın:

      ``# cd /etc/ssl/certs``

3.  toosee hello Symantec kök CA sertifikası mevcut değilse ya da değildir, bu komutu çalıştırın:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Merhaba dosya bulunamazsa, şu komutları çalıştırın:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  toocreate simgesel b204d74a.0 ile VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem ->, bu komutu çalıştırın:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Bu komut çıktı aşağıdaki hello varsa toosee denetleyin. Aksi halde, bir simgesel toocreate vardır:

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Simgesel 653b494a.0 yoksa, bu komutu toocreate bir simgesel kullanın:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Site kurtarma URL'lerini veya IP aralıkları (hata kodu 151037 veya 151072) için giden bağlantı

Site Recovery çoğaltma toowork için URL veya IP aralıkları giden bağlantı toospecific VM hello gereklidir. VM arkasında ise ağ güvenlik grubu (NSG) kuralları toocontrol giden Bağlantısı Güvenlik Duvarı veya kullanır, bu hata iletilerinden birini görebilirsiniz:

**Hata kodları** | **Olası nedenler** | **Öneriler**
--- | --- | ---
151037<br></br>**İleti**: tooregister Site Recovery ile Azure sanal makine başarısız oldu. | -NSG toocontrol giden erişim hello VM üzerinde kullanıyorsanız ve hello gerekli IP aralıkları giden erişim için Güvenilenler listesine değil.</br></br>-Üçüncü taraf güvenlik duvarı araçları kullanıyorsanız ve hello gerekli IP aralıklarını/URL'leri Güvenilenler listesine yok.</br>| -Hello VM üzerinde güvenlik duvarı proxy toocontrol giden ağ bağlantısı kullanıyorsanız, bu hello önkoşul URL'leri emin olun veya veri merkezi IP aralıkları Güvenilenler listesine:. Bilgi için bkz: [güvenlik duvarı proxy Kılavuzu](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-NSG kuralları toocontrol giden ağ bağlantısı hello VM üzerinde kullanıyorsanız, hello önkoşul veri merkezi IP aralıkları Güvenilenler listesine olduğundan emin olun. Bilgi için bkz: [ağ güvenlik grubu Kılavuzu](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**İleti**: Site Recovery yapılandırma başarısız oldu. | Bağlantı kurulan tooSite kurtarma hizmet uç noktaları olamaz. | -Hello VM üzerinde güvenlik duvarı proxy toocontrol giden ağ bağlantısı kullanıyorsanız, bu hello önkoşul URL'leri emin olun veya veri merkezi IP aralıkları Güvenilenler listesine:. Bilgi için bkz: [güvenlik duvarı proxy Kılavuzu](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-NSG kuralları toocontrol giden ağ bağlantısı hello VM üzerinde kullanıyorsanız, hello önkoşul veri merkezi IP aralıkları Güvenilenler listesine olduğundan emin olun. Bilgi için bkz: [ağ güvenlik grubu Kılavuzu](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Merhaba sorunu düzeltin
toowhitelist [hello gerekli URL'leri](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) veya hello [gerekli IP aralıkları](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), hello hello adımları [Ağ Kılavuzu belge](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Disk Hello makine (hata kodu 150039) bulunamadı

Yeni bir disk VM başlatılmalıdır toohello eklendi.

**Hata kodu** | **Olası nedenler** | **Öneriler**
--- | --- | ---
150039<br></br>**İleti**: mantıksal birim numarası (LUN) (LUNValue) ile Azure veri diski (DiskName) (DiskURI) eşlenen tooa karşılık gelen disk hello hello sahip VM içinde rapor edilen değildi aynı LUN değeri. | -Ekli toohello VM yeni bir veri diskini oldu, ancak başlatılmış değildi.</br></br>-hello veri diski hello VM içinde doğru şekilde raporlama hangi hello disk olduğu ekli toohello VM hello LUN değeri.| Merhaba veri diskleri başlatılır ve hello işlemi yeniden deneyin emin olun.</br></br>Windows: [Attach ve başlatma yeni bir disk](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Linux: [Linux yeni bir veri diski başlatma](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Merhaba sorunu düzeltin
Merhaba veri diskleri başlatılmış olması ve hello işlemi yeniden deneyin emin olun:

- Windows: [Attach ve başlatma yeni bir disk](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Linux: [Linux yeni bir veri diski başlatma](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Merhaba sorun devam ederse, desteğe başvurun.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>"Çoğaltma etkinleştirme" seçilmek oluşturulamıyor toosee hello Azure VM

Azure VM'nizi seçilmek üzere göremeyebilirsiniz [çoğaltmasını etkinleştir: 2. adım](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Bu sorunu hello Azure VM üzerinde sol toostale Site kurtarma yapılandırması nedeniyle olabilir. Aşağıdaki durumlarda hello içinde Azure VM'de Hello eski yapılandırma sol:

- Site RECOVERY'yi kullanarak hello Azure VM için çoğaltmayı etkinleştirmiş ve ardından hello Site Recovery kasası hello VM üzerindeki çoğaltma açıkça devre dışı bırakma olmadan silinir.
- Site RECOVERY'yi kullanarak hello Azure VM için çoğaltmayı etkinleştirmiş ve açıkça hello VM çoğaltmasını devre dışı bırakmadan hello Site Recovery kasası içeren hello kaynak grubu silindi.

### <a name="fix-hello-problem"></a>Merhaba sorunu düzeltin

Kullanabileceğiniz [kaldırmak eski ASR yapılandırma komut dosyası](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) ve hello eski Site kurtarma yapılandırması hello Azure VM üzerinde kaldırın. Görmeniz gerekir VM ile Merhaba [çoğaltmasını etkinleştir: 2. adım](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) sonra hello eski yapılandırma kaldırılıyor.


## <a name="next-steps"></a>Sonraki adımlar
[Azure sanal makinelerini çoğaltma](site-recovery-replicate-azure-to-azure.md)
