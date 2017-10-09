---
title: "aaaAzure Disk şifreleme sorunlarını giderme | Microsoft Docs"
description: "Bu makalede, Microsoft Azure Disk şifrelemesi for Windows ve Linux Iaas VM'ler için sorun giderme ipuçları sağlar."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Azure Disk şifrelemesi sorun giderme kılavuzu

Bu kılavuz bilgi teknolojisi (BT) uzmanları, bilgi güvenlik Çözümleyicileri olduğu ve bulut Yöneticiler, kuruluşlarının Azure disk şifrelemesi kullanan ve kılavuz tootroubleshoot disk şifrelemesi gereksinim ilgili sorunlar.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Linux işletim sistemi disk şifrelemesi sorunlarını giderme

Linux işletim sistemi disk şifrelemesi hello işletim sistemi sürücüsünün önceki toorunning çıkarmanız gerekir hello tam disk şifreleme işlemi üzerinden.   Başaramazsa, hata iletisi, "toounmount sonra başarısız..." hata iletisi büyük olasılıkla toooccur ' dir.

İşletim sistemi disk şifrelemesi değiştirilmiş veya kendi desteklenen stok galeri görüntüden değiştirilmiş bir hedef VM ortamına çalışırken en olası nedeni budur.  Merhaba uzantının özelliği toounmount hello işletim sistemi sürücüsü ile etkileyebilir desteklenen hello görüntü sapmaları örnekleri şunlardır:
- Desteklenen dosya sistemi ve/veya bölümleme düzeni artık eşleşmeyen özelleştirilmiş görüntüler.
- Virüsten koruma gibi uygulamalar, Docker, SAP, MongoDB veya Apache hello OS önceki tooencryption içinde çalışan Cassandra özelleştirilmiş görüntülerle.  Bu uygulamalar zor tooterminate olan ve açık dosya tanıtıcıları toohello işletim sistemi sürücüsü korurlar zaman hello sürücü, hataya neden olan, kaldırılan olamaz.
- Çalıştır özel komut dosyaları yakınlık toohello şifreleme adım müdahale ve bu hataya neden zaman kapatın. Bu bir Resource Manager şablonunu aynı anda birden çok uzantıları tooexecute tanımladığında ya da bir özel betik uzantısı veya diğer eylem toodisk şifreleme aynı anda çalıştırıldığında meydana gelebilir.   Seri hale getirme ve bu tür adımları yalıtma hello sorun çözülebilir.
- SELinux devre dışı önceki tooenabling şifreleme ayarlanmadı, hello adım başarısız çıkarın.  Şifreleme tamamlandıktan sonra SELinux yeniden etkinleştirilebilir.
- Merhaba işletim sistemi disk LVM düzenini kullanarak ne zaman (sınırlı LVM veri disk desteği kullanılabilir olsa da, LVM işletim sistemi diski değil)
- Ne zaman en düşük bellek gereksinimleri karşılanmadığı (işletim sistemi disk şifrelemesi için 7GB önerilen)
- Veri sürücüleri /mnt/ dizin veya birbiriyle (örneğin, /mnt/data1, /mnt/data2, /data3 + /data3/data4, vb.) altında takılı yinelemeli olarak ne zaman silinmiş
- Zaman diğer Azure Disk şifrelemesi [Önkoşullar](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) Linux için karşılanmadı

## <a name="unable-tooencrypt"></a>%S tooencrypt

Bazı durumlarda, hello Linux disk şifrelemesi "başlatılan işletim sistemi disk şifrelemesi" toobe takılmış ve SSH devre dışı görünür. Bu işlem, bir stok galeri görüntüsüne 3-16 saat toocomplete arasında sürebilir.  Çoklu TB boyutu veri diski eklenirse hello işlem gün sürebilir. Merhaba Linux işletim sistemi disk şifreleme dizisi hello işletim sistemi sürücüsü geçici olarak çıkarır ve şifrelenmiş durumundayken çıkarmadan önce hello tüm işletim sistemi diski, blok blok şifreleme gerçekleştirir.   Merhaba şifreleme işlemi devam ederken Windows Azure Disk şifrelemesi hello VM eşzamanlı kullanımı Linux Disk şifrelemesi izin vermiyor.  Merhaba hello boyutunu hello disk ve hello depolama hesabı standart veya premium (SSD) Depolama tarafından desteklenen olup olmadığı dahil olmak üzere VM Hello performans özellikleri hello gereken süre toocomplete şifreleme önemli ölçüde etkileyebilir.

toocheck durum hello ProgressMessage alan döndürdü hello [Get-AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) komutu sorgulanan.   Merhaba işletim sistemi sürücüsü şifrelenir, hello VM bakım durumuna geçtiğinde, ve SSH de devre dışı tooprevent sırada herhangi kesinti toohello devam eden işlem.  Şifreleme sürüyor, birkaç saat sonra toorestart hello VM isteyen bir VMRestartPending ileti ile izlenen olsa EncryptionInProgress hello zaman hello çoğunluğu için raporlanır.  Örneğin:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Bir kez tooreboot hello VM istenir ve hello VM yeniden başlatma ve 2-3 dakika hello hedefte gerçekleştirilen son adımlar toobe ve hello yeniden başlatma için vermiş sonra hello durum iletisi, şifreleme son tamamlandı gösterir.   Bu ileti kullanılabilir olduğunda, şifrelenmiş hello OS beklenen toobe hello VM toobe kullanılabilir ve kullanım için hazır yeniden sürücüdür.

Burada bu sırası Görülemedi, durumlarda veya önyükleme bilgileri, ilerleme iletisi veya diğer hata göstergeleri işletim sistemi şifreleme (örneğin) Bu kılavuzda açıklanan hello "toounmount başarısız oldu" hatayı görüyorsanız, bu işlemin hello ortasında başarısız olduğunu rapor varsa toorestore hello VM geri toohello anlık görüntü ya da hemen önceki tooencryption alınan yedeklemeyi önerilir.  Önceki toohello sonraki girişimi, önerilen toore olduğu-hello VM hello özelliklerini değerlendirmek ve tüm Önkoşullar uyduğunuzdan emin olun.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Azure Disk şifrelemesi bir güvenlik duvarının arkasında sorunlarını giderme
Ne zaman bağlantı görevlerini kesintiye bir güvenlik duvarı, proxy gereksinim veya ağ güvenlik grubu (NSG) ayarları, hello yeteneklerini hello uzantısı tooperform tarafından kısıtlanıyor.   Bu durum iletileri "Uzantı durumunu hello VM üzerinde kullanılabilir değil" gibi neden olabilir ve beklenen senaryolarda toofinish başarısız.  izleyin hello bölümü araştırmak bazı genel güvenlik duvarı sorunlar vardır.

### <a name="network-security-groups"></a>Ağ güvenlik grupları
Uygulanan ağ güvenlik grubu ayarlar hello uç nokta toomeet belgelenen hello ağ yapılandırması izin vermelidir [Önkoşullar](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) disk şifrelemesi için.

### <a name="azure-keyvault-behind-firewall"></a>Güvenlik duvarının arkasında Azure Keyvault
Merhaba VM mümkün tooaccess anahtar kasası olması gerekir. Erişim tookey hataya hello tarafından korunan bir güvenlik duvarı ardından erişiyorsa üzerinde tooguidance başvuran [anahtar kasası](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) takım.

### <a name="linux-package-management-behind-firewall"></a>Güvenlik duvarının arkasında Linux paket Yönetimi
Çalışma zamanında hello hedefi dağıtımı'nın paket yönetim sistemi tooinstall gerekli önkoşul bileşenleri önceki tooenabling şifreleme üzerinde Linux için Azure Disk şifrelemesi kullanır.  Güvenlik Duvarı ayarlarını mümkün toodownload hello VM engelleyen ve bu bileşenleri yüklemek, sonraki hataları beklenir.    Merhaba adımları tooconfigure bu dağıtım göre farklılık gösterebilir.  Red Hat üzerinde Abonelik Yöneticisi ve yum düzgün şekilde ayarlandığını sağlayarak, bir proxy gerektiğinde yaşamsal önem taşır.  Bkz: [bu](https://access.redhat.com/solutions/189533) Red Hat destek makalesi bu konuda.  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Windows Server 2016 Sunucu Çekirdeği sorunlarını giderme

Windows Server 2016 Server Core üzerinde hello bdehdcfg bileşeni varsayılan olarak kullanılamıyor. Bu bileşen tarafından Azure Disk şifrelemesi gereklidir.

tooworkaround Bu sorun, bir Windows Server 2016 veri merkezi VM toohello c:\windows\system32 hello Sunucu Çekirdeği görüntüsünün klasöründen aşağıdaki 4 dosyaları kopyalama hello:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Ardından, hello aşağıdaki komutu çalıştırın:

```
bdehdcfg.exe -target default
```

Bu 550 MB sistem bölümü oluşturur ve sonra bir yeniden başlatmadan sonra Diskpart toocheck hello birimler kullanmak ve devam edin.  

Örneğin:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, Azure disk şifrelemesi, bazı ortak sorunları hakkında daha fazla öğrenilen ve nasıl tootroubleshoot. Bu hizmet ve onun özelliği hakkında daha fazla bilgi için okumaya devam edin:

- [Azure Güvenlik Merkezi'nde disk şifrelemesi Uygula](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Azure sanal Makine'yi şifreleme](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure veri şifreleme çalışmıyorken-](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
