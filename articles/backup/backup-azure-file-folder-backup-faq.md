---
title: "aaaAzure Yedekleme aracısı ile ilgili SSS | Microsoft Docs"
description: "Hakkında toocommon soruları yanıtlar: Azure Yedekleme aracısı çalışır, yedekleme ve bekletme sınırları'nasıl hello."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
keywords: "yedekleme ve olağanüstü durum kurtarma; backup hizmeti"
ms.assetid: 778c6ccf-3e57-4103-a022-367cc60c411a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/18/2017
ms.author: trinadhk;pullabhk;
ms.openlocfilehash: bdefb4efb39301f38cdf692bdc93c841a2bbb441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="questions-about-hello-azure-backup-agent"></a>Hello Azure Yedekleme aracısı hakkında sorular
Bu makalede yanıtlar toocommon sorular toohelp hızlı bir şekilde hello Azure Yedekleme aracısı bileşenlerini anlama sahiptir. Bazı hello yanıtlar kapsamlı bilgiler bağlantılar toohello makaleler vardır. Hello Azure Backup hizmeti hakkında sorular hello nakledebilirsiniz [tartışma Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup).

## <a name="configure-backup"></a>Yedeklemeyi yapılandırma
### <a name="where-can-i-download-hello-latest-azure-backup-agent-br"></a>Merhaba en son Azure Backup aracısını nereden indirebilirim? <br/>
Windows Server, System Center DPM veya Windows İstemcisi yedeklemeye yönelik en son aracı hello indirebilirsiniz [burada](http://aka.ms/azurebackup_agent). Bir sanal makineyi tooback istiyorsanız hello VM (otomatik olarak hello uygun uzantıyı yükler) aracı kullanın. Merhaba VM Aracısı, Azure galerisinde hello oluşturulan sanal makineler üzerinde zaten mevcuttur.

### <a name="when-configuring-hello-azure-backup-agent-i-am-prompted-tooenter-hello-vault-credentials-do-vault-credentials-expire"></a>Hello Azure Backup aracısını yapılandırırken, istendiğinde tooenter hello kasa kimlik bilgileri istiyorum. Kasa kimlik bilgilerinin süresi dolar mı?
Evet, hello kasa kimlik bilgileri 48 saat sonra süresi dolacak. Hello dosyanın süresi dolarsa, toohello içinde Azure portal ve indirme hello kasa kimlik bilgileri Kasası'nı günlük dosyaları.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Ne tür sürücülerden dosya ve klasör yedekleyebilirim? <br/>
Aşağıdaki sürücüler/birimler hello yedekleyemezsiniz:

* Çıkarılabilir Medya: Tüm yedekleme öğesi kaynaklarının sabit olarak bildirilmesi gerekir.
* Salt okunur birimler: hello birim hello Birim Gölge Kopyası Hizmeti (VSS) toofunction için yazılabilir olmalıdır.
* Çevrimdışı birimler: hello birim için VSS toofunction çevrimiçi olması gerekir.
* Ağ paylaşımı: hello birimin çevrimiçi yedekleme kullanılarak yedeklenen yerel toohello sunucu toobe olması gerekir.
* BitLocker korumalı birimler: hello yedeklemenin gerçekleşebilmesi hello birimin kilidi olmalıdır.
* Dosya sistemi tanımlaması: NTFS desteklenen hello tek dosya sistemidir.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Sunucumdan hangi dosya ve klasör hangi türlerini yedekleyebilirim?<br/>
şu türlerini hello desteklenir:

* Şifreli
* Sıkıştırılmış
* Seyrek
* Sıkıştırılmış + Seyrek
* Sabit Bağlantılar: Desteklenmez, atlanır
* Yeniden Ayrıştırma Noktası: Desteklenmez, atlanır
* Şifreli + Seyrek: Desteklenmez, atlanır
* Sıkıştırılmış Akış: Desteklenmez, atlanır
* Seyrek Akış: Desteklenmez, atlanır

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-already-backed-by-hello-azure-backup-service-using-hello-vm-extension-br"></a>Zaten hello VM uzantısı kullanılarak hello Azure Backup hizmeti tarafından yedeklenmiş Azure VM'de hello Azure Yedekleme aracısı yükleyebilir miyim? <br/>
Kesinlikle. Azure Backup hello VM uzantısını kullanan Azure VM'ler için VM düzeyinde yedekleme sağlar. Merhaba Konuk Windows işletim sistemi üzerindeki tooprotect dosyaları ve klasörleri hello Konuk Windows işletim sistemi hello Azure Backup aracısını yükleyin.

### <a name="can-i-install-hello-azure-backup-agent-on-an-azure-vm-tooback-up-files-and-folders-present-on-temporary-storage-provided-by-hello-azure-vm-br"></a>Dosya ve klasörleri geçici depolama hello Azure VM tarafından sağlanan mevcut bir Azure VM tooback üzerinde hello Azure Yedekleme aracısı yükleyebilir miyim? <br/>
Evet. Merhaba Konuk Windows işletim sistemi Hello Azure Yedekleme aracısı yükleyin ve dosya ve klasörleri tootemporary depolamasını yedeklemek. Geçici depolama verileri silindikten sonra yedeklemeler başarısız olur. Ayrıca, Hello geçici depolama verilerinin silinmiş olması durumunda toonon geçici depolama yalnızca geri yükleyebilirsiniz.

### <a name="whats-hello-minimum-size-requirement-for-hello-cache-folder-br"></a>Merhaba hello Önbellek klasörü için minimum boyut gereksinimini nedir? <br/>
Merhaba hello Önbellek klasörü boyutunu hello yedeklediğiniz veri miktarını belirler. Önbellek klasörü % 5'veri depolama için gerekli hello alanı olmalıdır.

### <a name="how-do-i-register-my-server-tooanother-datacenterbr"></a>My server tooanother datacenter nasıl kaydettirebilirim?<br/>
Yedekleme verilerini, kayıtlı olduğu hello kasa toowhich toohello veri merkezi gönderilir. Merhaba en kolay yolu toochange hello datacenter toouninstall hello aracısıdır ve hello aracısını yeniden yükleyin ve toodesired datacenter ait yeni bir kasa tooa kaydedin.

### <a name="does-hello-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Hello Azure Yedekleme aracısı, Windows Server 2012 yinelenenleri kaldırma özelliğini kullanan bir sunucuda çalışmak mu? <br/>
Evet. Merhaba yedekleme işlemini hazırlarken yinelenenleri kaldırılmış hello veri toonormal veri hello Aracısı hizmeti dönüştürür. Ardından hello veri yedekleme için en iyi duruma getirir, hello verileri şifreler ve şifrelenmiş hello veri toohello çevrimiçi yedekleme hizmetine gönderir.

## <a name="backup"></a>Backup
### <a name="how-do-i-change-hello-cache-location-specified-for-hello-azure-backup-agentbr"></a>Hello Azure Backup aracısı için belirtilen hello önbellek konumunu nasıl değişiyor?<br/>
Liste toochange hello önbellek konumu aşağıdaki hello kullanın.

1. Yükseltilmiş bir komut istemi komutunda aşağıdaki hello yürüterek Hello Backup altyapısını durdurun:

    ```PS C:\> Net stop obengine``` 
  
2. Merhaba dosyaları taşımayın. Bunun yerine, hello önbellek alanı klasörünü tooa farklı bir sürücü yeterli alana sahip kopyalayın. Merhaba yedeklemeleri hello yeni önbellek alanı ile çalıştığı onaylandıktan sonra Hello özgün önbellek alanı kaldırılabilir.
3. Merhaba yolu toohello yeni önbellek alanı klasörünün ile kayıt defteri girdileri aşağıdaki hello güncelleştirin.<br/>

    | Kayıt defteri yolu | Kayıt Defteri Anahtarı | Değer |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Yeni önbellek klasörü konumu* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Yeni önbellek klasörü konumu* |

4. Yükseltilmiş bir komut istemi komutunda aşağıdaki hello yürüterek Hello Backup altyapısını yeniden başlatın:

    ```PS C:\> Net start obengine```

Merhaba yedekleme oluşturma hello yeni önbellek konumunda başarıyla tamamlandıktan sonra hello özgün önbellek klasörünü kaldırabilirsiniz.


### <a name="where-can-i-put-hello-cache-folder-for-hello-azure-backup-agent-toowork-as-expectedbr"></a>Burada hello Önbellek klasörü için beklendiği gibi hello Azure Yedekleme aracısı toowork koyabilirsiniz?<br/>
Merhaba hello Önbellek klasörü için aşağıdaki konumlar önerilmez:

* Ağ paylaşımı veya çıkarılabilir medya: hello Önbellek klasörü, çevrimiçi yedekleme kullanılarak yedeklenmesi gereken yerel toohello sunucusu olmalıdır. Ağ konumlarını veya USB sürücüleri gibi çıkarılabilir medyalar desteklenmez.
* Çevrimdışı birimler: Önbellek klasörü hello Azure Backup Aracısı kullanılarak gerçekleştirilecek beklenen yedekleme için çevrimiçi olması gerekir.

### <a name="are-there-any-attributes-of-hello-cache-folder-that-are-not-supportedbr"></a>Desteklenmeyen herhangi bir özniteliği hello Önbellek klasörü var mı?<br/>
Merhaba aşağıdaki öznitelikler veya bunların bileşimleri hello Önbellek klasörü için desteklenmez:

* Şifreli
* Yinelenenleri kaldırma işlemi uygulanmış
* Sıkıştırılmış
* Seyrek
* Yeniden Ayrıştırma Noktası

Merhaba Önbellek klasörü ve hello meta verileri VHD hello Azure Backup aracısı için gerekli öznitelikler hello gerekmez.

### <a name="is-there-a-way-tooadjust-hello-amount-of-bandwidth-used-by-hello-backup-servicebr"></a>Bir şekilde tooadjust hello hello Backup hizmeti tarafından kullanılan bant genişliği miktarı var mı?<br/>
  Evet, hello kullan **özelliklerini değiştirme** hello Backup Aracısı tooadjust bant seçeneği. Bu bant genişliği kullandığınızda, bant genişliği ve hello kez hello miktarını ayarlayabilirsiniz. Adım adım yönergeler için bkz. **[Ağ kapasitesi azaltmayı etkinleştirme](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Yedekleri yönetme
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-tooazurebr"></a>Veri tooAzure yedekleyen bir Windows server adlandırırsanız ne olur?<br/>
Bir sunucuyu yeniden adlandırdığınızda, geçerli olarak yapılandırılmış olan tüm yedeklemeler durdurulur.
Merhaba sunucunun yeni adını Hello hello yedekleme kasasıyla birlikte kaydedin. Merhaba kasayla hello yeni adı kaydettiğinizde hello ilk yedekleme işlemi olduğundan bir *tam* yedekleme. Merhaba eski sunucu adı toohello kasaya yedeklenen toorecover veri gerekirse hello kullanın [ **başka bir sunucuya** ](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) hello seçeneğinde **verileri kurtarabilirsiniz** Sihirbazı.

### <a name="what-is-hello-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Azure Backup aracısını kullanan yedekleme ilkesinde belirtilen hello en fazla dosya yolu uzunluğu nedir? <br/>
Azure Backup aracısı NTFS kullanır. Merhaba [yolu uzunluğu belirtimi hello Windows API tarafından sınırlı](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Tooprotect istediğiniz hello hello Windows API tarafından izin daha uzun bir dosya yolu uzunluğu dosyalarınız varsa, hello üst klasörü veya hello disk sürücüsü yedekleme.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Azure Backup aracısını kullanan Azure Yedekleme ilkesinin dosya yolunda hangi karakterlere izin verilir? <br>
 Azure Backup aracısı NTFS kullanır. [NTFS destekli karakterleri](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) dosya belirtiminin bir parçası olarak etkinleştirir. 
 
### <a name="i-receive-hello-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Bir yedekleme İlkesi yapılandırılmış olsa bile "Azure yedeklemeleri bu sunucu için yapılandırılmamış" Uyarısı, hello alma <br/>
Bu uyarı Hello yerel sunucuda depolanan hello yedekleme zamanlaması ayarları aynı hello yedekleme kasasında depolanan ayarları hello hello olmadığında oluşur. Merhaba sunucu veya hello ayarları kurtarılan tooa bilinen iyi bir durumda bırakıldı, hello yedekleme zamanlamaları eşitlemesini kaybedebilir. Bu uyarıyı alırsanız [hello yedekleme ilkesini yeniden yapılandırın](backup-azure-manage-windows-server.md) ve ardından **çalıştırmak Şimdi Yedekle** tooresynchronize hello yerel sunucuyu Azure ile.
