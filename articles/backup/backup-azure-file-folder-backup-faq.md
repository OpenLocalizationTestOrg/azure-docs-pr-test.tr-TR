---
title: "Azure Backup aracısıyla ilgili SSS | Microsoft Docs"
description: "Azure Backup aracısının çalışması, yedekleme ve bekletme sınırları hakkındaki yaygın soruların yanıtları."
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
ms.openlocfilehash: 227cdc87f3e2c8ed393145f4bbde7f74606bdf3b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="questions-about-the-azure-backup-agent"></a>Azure Backup aracısıyla ilgili sorular
Bu makalede Azure Backup aracısı bileşenlerini kısa süre içinde anlamanıza yardımcı olacak yaygın soruların yanıtları bulunur. Bazı yanıtlarda, kapsamlı bilgiler içeren makalelerin bağlantıları vardır. Ayrıca Azure Backup hizmeti ile ilgili sorularınızı [tartışma forumunda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup) paylaşabilirsiniz.

## <a name="configure-backup"></a>Yedeklemeyi yapılandırma
### <a name="where-can-i-download-the-latest-azure-backup-agent-br"></a>En son Azure Backup aracısını nereden indirebilirim? <br/>
Windows Server, System Center DPM veya Windows istemcisini yedeklemeye yönelik en son aracıyı [buradan](http://aka.ms/azurebackup_agent) indirebilirsiniz. Bir sanal makineyi yedeklemek istiyorsanız VM Aracısı'nı (otomatik olarak uygun uzantıyı yükler) kullanın. VM Aracısı, Azure galerisinden oluşturulan sanal makineler üzerinde zaten mevcuttur.

### <a name="when-configuring-the-azure-backup-agent-i-am-prompted-to-enter-the-vault-credentials-do-vault-credentials-expire"></a>Azure Backup aracısını yapılandırırken kasa kimlik bilgilerini girmem isteniyor. Kasa kimlik bilgilerinin süresi dolar mı?
Evet, kasa kimlik bilgilerinin süresi 48 saat sonra dolar. Dosyanın süresi dolarsa Azure portalında oturum açın ve kasa kimlik bilgileri dosyalarını kasanızdan indirin.

### <a name="what-types-of-drives-can-i-back-up-files-and-folders-from-br"></a>Ne tür sürücülerden dosya ve klasör yedekleyebilirim? <br/>
Aşağıdaki sürücüleri/birimleri yedekleyemezsiniz:

* Çıkarılabilir Medya: Tüm yedekleme öğesi kaynaklarının sabit olarak bildirilmesi gerekir.
* Salt Okunur Birimler: Birimin çalışması için birim gölge kopyası hizmetine (VSS) yönelik olarak yazılabilir olması gerekir.
* Çevrimdışı Birimler: Birimin çalışması için VSS'ye yönelik olarak çevrimiçi olması gerekir.
* Ağ paylaşımı: Birimin çevrimiçi yedekleme kullanılarak yedeklenebilmesi için sunucuya yönelik olarak yerel olması gerekir.
* Bitlocker korumalı birimler: Yedeklemenin gerçekleşebilmesi için birimin kilidinin açık olması gerekir.
* Dosya Sistemi Tanımı: NTFS, desteklenen tek dosya sistemidir.

### <a name="what-file-and-folder-types-can-i-back-up-from-my-serverbr"></a>Sunucumdan hangi dosya ve klasör hangi türlerini yedekleyebilirim?<br/>
Aşağıdaki türler desteklenir:

* Şifreli
* Sıkıştırılmış
* Seyrek
* Sıkıştırılmış + Seyrek
* Sabit Bağlantılar: Desteklenmez, atlanır
* Yeniden Ayrıştırma Noktası: Desteklenmez, atlanır
* Şifreli + Seyrek: Desteklenmez, atlanır
* Sıkıştırılmış Akış: Desteklenmez, atlanır
* Seyrek Akış: Desteklenmez, atlanır

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-already-backed-by-the-azure-backup-service-using-the-vm-extension-br"></a>Azure Backup aracısını, önceden VM uzantısı kullanılarak Azure Backup hizmeti tarafından yedeklenmiş olan bir Azure VM üzerine yükleyebilir miyim? <br/>
Kesinlikle. Azure Backup, VM uzantısını kullanan Azure VM'ler için VM düzeyinde yedekleme sağlar. Konuk Windows işletim sistemi üzerindeki dosya ve klasörleri korumak için Azure Backup aracısını konuk Windows işletim sistemine yükleyin.

### <a name="can-i-install-the-azure-backup-agent-on-an-azure-vm-to-back-up-files-and-folders-present-on-temporary-storage-provided-by-the-azure-vm-br"></a>Azure Backup aracısını bir Azure VM'ye yükleyerek mevcut dosya ve klasörleri Azure VM tarafından sağlanan geçici depolama alanına yedekleyebilir miyim? <br/>
Evet. Azure Backup aracısını Konuk Windows işletim sistemine yükleyin ve dosya ve klasörleri geçici depolama alanına yedekleyin. Geçici depolama verileri silindikten sonra yedeklemeler başarısız olur. Ayrıca, geçici depolama verilerinin silinmiş olması durumunda, yalnızca geçici olmayan depolama alanına geri yükleme gerçekleştirebilirsiniz.

### <a name="whats-the-minimum-size-requirement-for-the-cache-folder-br"></a>Önbellek klasörü için minimum boyut gereksinimini nedir? <br/>
Önbellek klasörünün boyutu, yedeklediğiniz veri miktarını belirler. Önbellek klasörü, veri depolama için gerekli olan alanın % 5'ini oluşturmalıdır.

### <a name="how-do-i-register-my-server-to-another-datacenterbr"></a>Sunucumu başka bir veri merkezine nasıl kaydederim?<br/>
Yedekleme verileri, kasanın kayıtlı olduğu veri merkezine gönderilir. Veri merkezini değiştirmenin en kolay yolu, aracıyı kaldırmak ve aracıyı yeniden yükleyip istenilen veri merkezine ait yeni bir kasa kaydetmektir.

### <a name="does-the-azure-backup-agent-work-on-a-server-that-uses-windows-server-2012-deduplication-br"></a>Azure Backup aracısı, Windows Server 2012 yinelenenleri kaldırma özelliğini kullanan bir sunucu üzerinde çalışır mı? <br/>
Evet. Aracı hizmeti, yedekleme işlemini hazırlarken yinelenenleri kaldırma işlemi uygulanmış verileri normal verilere dönüştürür. Ardından verileri yedekleme için en iyi duruma getirir, verileri şifreler ve daha sonra, şifreli verileri çevrimiçi yedekleme hizmetine gönderir.

## <a name="backup"></a>Backup
### <a name="how-do-i-change-the-cache-location-specified-for-the-azure-backup-agentbr"></a>Azure Backup aracısı için belirtilen önbellek konumunu nasıl değiştiririm?<br/>
Önbellek konumunu değiştirmek için aşağıdaki listeyi kullanın.

1. Yükseltilmiş komut isteminde aşağıdaki komutu çalıştırarak Backup altyapısını durdurun:

    ```PS C:\> Net stop obengine``` 
  
2. Dosyaları taşımayın. Bunun yerine, önbellek alanı klasörünü yeterli alana sahip farklı bir sürücüye kopyalayın. Yedeklemelerin yeni önbellek alanı ile çalıştığı onaylandıktan sonra özgün önbellek alanı kaldırılabilir.
3. Aşağıdaki kayıt defteri girdilerini yeni önbellek alanı klasörünün yolu ile güncelleştirin.<br/>

    | Kayıt defteri yolu | Kayıt Defteri Anahtarı | Değer |
    | --- | --- | --- |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config` |ScratchLocation |*Yeni önbellek klasörü konumu* |
    | `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider` |ScratchLocation |*Yeni önbellek klasörü konumu* |

4. Yükseltilmiş komut isteminde aşağıdaki komutu çalıştırarak Backup altyapısını yeniden başlatın:

    ```PS C:\> Net start obengine```

Yedekleme oluşturma yeni önbellek konumunda başarıyla tamamlandıktan sonra, özgün önbellek klasörünü kaldırabilirsiniz.


### <a name="where-can-i-put-the-cache-folder-for-the-azure-backup-agent-to-work-as-expectedbr"></a>Azure Backup Aracısı'nın beklendiği şekilde çalışması için önbellek klasörünü nereye koyabilirim?<br/>
Önbellek klasörü için aşağıdaki konumlar önerilmez:

* Ağ paylaşımı veya Çıkarılabilir Medya: Önbellek klasörü, çevrimiçi yedekleme kullanılarak yedeklenmesi gereken sunucu için yerel olmalıdır. Ağ konumlarını veya USB sürücüleri gibi çıkarılabilir medyalar desteklenmez.
* Çevrimdışı Birimler: Önbellek klasörü, Azure Backup Aracısı kullanılarak gerçekleştirilecek beklenen yedekleme için çevrimiçi olmalıdır.

### <a name="are-there-any-attributes-of-the-cache-folder-that-are-not-supportedbr"></a>Önbellek klasörünün desteklenmeyen herhangi bir özniteliği var mıdır?<br/>
Aşağıdaki öznitelikler veya bunların bileşimleri, önbellek klasörü için desteklenmez:

* Şifreli
* Yinelenenleri kaldırma işlemi uygulanmış
* Sıkıştırılmış
* Seyrek
* Yeniden Ayrıştırma Noktası

Önbellek klasörü ve meta veri VHD’si, Azure Backup aracısı için gerekli özniteliklere sahip değildir.

### <a name="is-there-a-way-to-adjust-the-amount-of-bandwidth-used-by-the-backup-servicebr"></a>Backup hizmeti tarafından kullanılan bant genişliği miktarını ayarlamanın bir yolu var mıdır?<br/>
  Evet, bant genişliğini ayarlamak için Backup Aracısı'ndaki **Özellikleri Değiştir** seçeneğini kullanın. Bant genişliği miktarını ve bu bant genişliğini kullanma zamanlarınızı ayarlayabilirsiniz. Adım adım yönergeler için bkz. **[Ağ kapasitesi azaltmayı etkinleştirme](backup-configure-vault.md#enable-network-throttling)**.

## <a name="manage-backups"></a>Yedekleri yönetme
### <a name="what-happens-if-i-rename-a-windows-server-that-is-backing-up-data-to-azurebr"></a>Azure'a veri yedekleyen bir Windows sunucusunu yeniden adlandırırsam ne olur?<br/>
Bir sunucuyu yeniden adlandırdığınızda, geçerli olarak yapılandırılmış olan tüm yedeklemeler durdurulur.
Sunucunun yeni adını Backup kasasına kaydedin. Yeni adı kasaya kaydettiğinizde, ilk yedekleme işlemi *tam* yedekleme olur. Eski sunucu adıyla kasaya yedeklenen verileri kurtarmanız gerekiyorsa **Veri Kurtarma** sihirbazındaki [**Başka bir sunucu**](backup-azure-restore-windows-server.md#use-instant-restore-to-restore-data-to-an-alternate-machine) seçeneğini kullanın.

### <a name="what-is-the-maximum-file-path-length-that-can-be-specified-in-backup-policy-using-azure-backup-agent-br"></a>Yedekleme ilkesinde Azure Backup aracısını kullanarak belirtilebilecek dosya yolu uzunluğu için üst sınır nedir? <br/>
Azure Backup aracısı NTFS kullanır. [Dosya yolu uzunluğu belirtimi, Windows API ile sınırlıdır](https://msdn.microsoft.com/library/aa365247.aspx#fully_qualified_vs._relative_paths). Korumak istediğiniz dosyalar Windows API tarafından izin verilenden daha uzun dosya yollarına sahipse, üst klasörü veya disk sürücüsünü yedekleyin.  

### <a name="what-characters-are-allowed-in-file-path-of-azure-backup-policy-using-azure-backup-agent-br"></a>Azure Backup aracısını kullanan Azure Yedekleme ilkesinin dosya yolunda hangi karakterlere izin verilir? <br>
 Azure Backup aracısı NTFS kullanır. [NTFS destekli karakterleri](https://msdn.microsoft.com/library/aa365247.aspx#naming_conventions) dosya belirtiminin bir parçası olarak etkinleştirir. 
 
### <a name="i-receive-the-warning-azure-backups-have-not-been-configured-for-this-server-even-though-i-configured-a-backup-policy-br"></a>Bir yedekleme ilkesi zamanlamış olmama karşın "Azure Yedeklemeleri bu sunucu için yapılandırılmamış" uyarısını alıyorum <br/>
Bu uyarı, yerel sunucuda depolanan yedekleme zamanlaması ayarları, yedekleme kasasında depolanan ayarlarla aynı olmadığında oluşur. Sunucu ya da ayarlar bilinen bir iyi duruma getirilerek kurtarıldığında, yedekleme zamanlamaları eşitlemesini kaybedebilir. Bu uyarıyı alırsanız [yedekleme ilkesini yeniden yapılandırın](backup-azure-manage-windows-server.md) ve ardından yerel sunucuyu Azure ile yeniden eşitlemek için **Run Back Up Now (Yedeklemeyi Şimdi Çalıştır)** işlemini uygulayın.
