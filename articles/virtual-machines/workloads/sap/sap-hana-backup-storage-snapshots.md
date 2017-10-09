---
title: "aaaSAP HANA Azure yedekleme depolama anlık görüntü tabanlı | Microsoft Docs"
description: "İki ana yedekleme olasılıklarını SAP HANA Azure sanal makinelerde vardır, bu makalede, SAP HANA yedekleme depolama anlık görüntü tabanlı yer almaktadır"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: 32bb80f5a928a2cf63699bfe4f4cf5bbad81e6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-backup-based-on-storage-snapshots"></a>Depolama anlık görüntülerine dayalı SAP HANA yedeklemesi

## <a name="introduction"></a>Giriş

Bu üç bölümlük SAP HANA yedeklemede ilgili makaleleri bir parçasıdır. [SAP HANA için yedekleme Kılavuzu Azure sanal makineler üzerinde](sap-hana-backup-guide.md) Başlarken, genel bir bakış ve bilgi sağlar ve [SAP HANA Azure yedekleme dosya düzeyinde](sap-hana-backup-file-level.md) kapsar hello dosya tabanlı yedekleme seçeneği.

Tek Örnekli hepsi bir arada demo sistem için bir VM yedekleme özelliğini kullanarak, bir hello işletim sistemi düzeyinde adresindeki HANA yedeklemeleri yönetmek yerine VM Yedekleme yapmayı düşünmelisiniz. Tootake Azure blob anlık görüntüleri toocreate ekli tooa sanal makine olan ve hello HANA veri dosyalarını tutmak tek tek sanal disk kopyaları alternatiftir. Ancak hello sistem yukarı durumdayken VM yedekleme veya disk anlık görüntü oluşturma ve çalıştırma olduğunda uygulama tutarlılığı kritik noktasıdır. Bkz: _depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığını_ hello ilgili makalede [yedekleme Kılavuzu SAP HANA Azure sanal makineler üzerinde](sap-hana-backup-guide.md). SAP HANA bu tür bir depolama anlık görüntüleri destekleyen bir özelliği vardır.

## <a name="sap-hana-snapshots"></a>SAP HANA anlık görüntüler

SAP HANA içinde depolama anlık destekleyen bir özellik yok. Ancak, aralık 2016 itibariyle bir kısıtlama yoktur toosingle kapsayıcı sistemler. Çok müşterili kapsayıcı yapılandırmaları, bu tür bir veritabanı anlık görüntüsü desteklemez (bkz [depolama anlık görüntü (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm)).

Şu şekilde çalışır:

- Merhaba SAP HANA anlık görüntü başlatarak depolama anlık görüntü için hazırlama
- Merhaba depolama anlık görüntü (anlık görüntü, örneğin Azure blob) çalıştırın
- Merhaba SAP HANA anlık görüntü onaylayın

![Bu ekran görüntüsü, bir SAP HANA veri anlık bir SQL deyimi oluşturduğunuz gösterir.](media/sap-hana-backup-storage-snapshots/image011.png)

Bu ekran, SAP HANA veri anlık görüntüsünü bir SQL deyimi oluşturduğunuz gösterir.

![ardından anlık görüntü hello hello yedekleme kataloğu SAP HANA Studio'da da görüntülenir.](media/sap-hana-backup-storage-snapshots/image012.png)

SAP HANA Studio'da hello yedekleme kataloğunda sonra anlık görüntü hello da görüntülenir.

![Disk üzerinde hello anlık görüntü hello SAP HANA veri dizininde görüntülenir](media/sap-hana-backup-storage-snapshots/image013.png)

Disk üzerinde hello anlık görüntü hello SAP HANA veri dizininde görüntülenir.

Merhaba dosya sistemi tutarlılığı SAP HANA hello anlık görüntü hazırlama modunda çalışırken hello depolama anlık görüntü çalıştırmadan önce de garanti tooensure sahip. Bkz: _depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığını_ hello ilgili makalede [yedekleme Kılavuzu SAP HANA Azure sanal makineler üzerinde](sap-hana-backup-guide.md).

Merhaba depolama anlık görüntü yaptıktan sonra kritik tooconfirm hello SAP HANA anlık görüntüsüdür. Karşılık gelen bir SQL deyimi toorun yoktur: yedekleme verilerini Kapat anlık görüntü (bkz [yedekleme verileri Kapat anlık görüntü deyimi (yedekleme ve kurtarma)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/c3/9739966f7f4bd5818769ad4ce6a7f8/content.htm)).

> [!IMPORTANT]
> Merhaba HANA anlık görüntü onaylayın. Son çok&quot;kopyalama yazarken,&quot; SAP HANA ek disk alanı hazırlama anlık görüntü modu ve hello SAP HANA anlık görüntü onaylandıktan kadar olası toostart yeni yedeklemeler olmadığı gerekebilir.

## <a name="hana-vm-backup-via-azure-backup-service"></a>Azure Backup hizmeti aracılığıyla HANA VM yedekleme

Aralık 2016 itibariyle hello Azure Backup hizmeti yedekleme aracısını hello Linux VM'ler için kullanılabilir değil. Azure yedekleme toomake kullanımını hello dosya/dizin düzeyi, bir SAP HANA yedekleme dosyalarını tooa Windows VM kopyalayın ve hello yedekleme aracısını kullanın. Aksi takdirde, yalnızca tam bir Linux VM yedekleme hello Azure Backup hizmeti mümkündür. Bkz: [hello genel bakış özellikleri Azure Yedekleme'de](../../../backup/backup-introduction-to-azure-backup.md) toofind daha fazla bilgi.

Hello Azure Backup hizmeti bir seçenek tooback sunar ve bir VM geri yükleyin. Bu hizmet ve nasıl çalıştığı hakkında daha fazla bilgi hello makalesinde bulunabilir [azure'da VM yedekleme altyapınızı planlama](../../../backup/backup-azure-vms-introduction.md).

Toothat makale göre iki önemli noktalar şunlardır:

_&quot;Linux eşdeğer platform tooVSS olmadığından Linux sanal makineleri için yalnızca dosya tutarlı yedeklemeler olasılığı vardır.&quot;_

_&quot;Uygulamaların gerekiyor tooimplement kendi &quot;düzeltme&quot; hello mekanizmasını geri veri.&quot;_

Bu nedenle, bir tane toomake hello yedekleme başladığında SAP HANA disk tutarlı bir durumda olduğundan emin içeriyor. Bkz: _SAP HANA anlık görüntüleri_ hello belgenin önceki bölümlerinde açıklanan. Ancak bu anlık görüntü hazırlama modunda SAP HANA kaldığında oluşan olası bir sorunu olduğunu. Bkz: [depolama anlık görüntü (SAP HANA Studio)](https://help.sap.com/saphelp_hanaplatform/helpdata/en/a0/3f8f08501e44d89115db3c5aa08e3f/content.htm) daha fazla bilgi için.

Bu makale durumları:

_&quot;Tooconfirm önerilir veya oluşturulduktan sonra depolama anlık görüntü mümkün olan en kısa sürede bırakın. Anlık görüntü ilgili verileri Hello depolama anlık görüntü hazırlanan ya da oluşturulan hello dondurulmuş. Başlangıç anlık görüntü ilgili verileri dondurulmuş kalırken değişiklikleri hala hello veritabanında yapılabilir. Anlık görüntü ilgili verileri toobe değiştirilen dondurulmuş hello değişikliğe neden olmaz. Bunun yerine, hello değişiklikler hello depolama anlık görüntüden ayrı hello veri alanında toopositions yazılır. Değişiklikleri de toohello günlüğüne yazılır. Ancak, anlık görüntü ilgili verileri uzun hello hello dondurulmuş tutulur, veri birimi büyüyebilir daha fazla hello hello.&quot;_

Azure yedekleme hello dosya sistemi tutarlılığı Azure VM uzantıları aracılığıyla ilgilenir. Bu uzantılar, mevcut tek başına değildir ve yalnızca Azure Backup hizmeti ile birlikte çalışır. Bununla birlikte, yine gereksinim toomanage bir SAP HANA anlık görüntü tooguarantee uygulama tutarlılığı etmektir.

Azure yedekleme iki ana aşamadan oluşur:

- Anlık görüntü alın
- Veri toovault Aktarım

Bir anlık görüntü alma hello Azure Backup hizmeti aşaması tamamlandıktan sonra bu nedenle bir hello SAP HANA anlık görüntü onaylayabilir. Birkaç dakika toosee hello Azure portal geçmesi gerekebilir.

![Bu şekilde hello yedekleme işi listesinin bir Azure Backup hizmeti parçası gösterilmektedir](media/sap-hana-backup-storage-snapshots/image014.png)

Bu şekilde hello yedekleme işi listesinin hello HANA test VM yukarı kullanılan tooback olan bir Azure Backup hizmeti parçası gösterilmektedir.

![tooshow hello iş ayrıntıları, hello yedekleme işinden hello Azure portal'ı tıklatın](media/sap-hana-backup-storage-snapshots/image015.png)

tooshow hello iş ayrıntıları, hello yedekleme işinden hello Azure portal'ı tıklatın. Burada, bir iki aşamaya hello görebilirsiniz. Tamamlandı olarak hello anlık görüntü aşaması görüntüleyene kadar birkaç dakika sürebilir. Başlangıç zamanının çoğunu hello veri aktarımı aşamasında harcanır.

## <a name="hana-vm-backup-automation-via-azure-backup-service"></a>Azure Backup hizmeti aracılığıyla HANA VM yedekleme Otomasyonu

Biri el ile Merhaba SAP HANA anlık görüntü bir kez daha önce açıklandığı gibi hello Azure yedekleme anlık görüntü aşaması tamamlandığında, ancak bir yönetici hello yedekleme işi hello Azure portal listesinde izlemeyecek çünkü bunu yararlı tooconsider Otomasyon onaylayabilir.

Burada, nasıl, Azure PowerShell cmdlet'leri gerçekleştirilmesi bir açıklaması verilmiştir.

![Azure Backup hizmeti hello adı hana-yedekleme-kasayla oluşturuldu](media/sap-hana-backup-storage-snapshots/image016.png)

Azure Backup hizmeti hello adla oluşturuldu &quot;hana-yedekleme-kasası.&quot; PS komutu hello **Get-AzureRmRecoveryServicesVault-ad hana yedekleme kasası** hello karşılık gelen nesnesini alır. Kullanılan tooset hello sonra yedekleme içerik üzerinde hello sonraki şekilde görüldüğü gibi bu nesnesidir.

![Bir yedekleme işi şu anda devam ediyor hello için kontrol edebilirsiniz](media/sap-hana-backup-storage-snapshots/image017.png)

Ayar hello doğru bağlamı sonra bir hello yedekleme işi şu anda devam ediyor için denetleyin ve iş ayrıntılarını bakın. Merhaba alt liste hello anlık görüntü hello Azure yedekleme işi aşaması zaten tamamlanmış gösterir:

```
$ars = Get-AzureRmRecoveryServicesVault -Name hana-backup-vault
Set-AzureRmRecoveryServicesVaultContext -Vault $ars
$jid = Get-AzureRmRecoveryServicesBackupJob -Status InProgress | select -ExpandProperty jobid
Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
```

![Yoklama hello değeri tooCompleted renge kadar döngü](media/sap-hana-backup-storage-snapshots/image018.png)

Bir değişkende Hello iş ayrıntılarını depolandıktan sonra yalnızca PS sözdizimi tooget toohello ilk dizi girişi ve hello durum değeri alın. toocomplete hello otomasyon komut dosyası, bu kadar Döngü yoklama hello değeri bırakır çok&quot;tamamlandı.&quot;

```
$st = Get-AzureRmRecoveryServicesBackupJobDetails -Jobid $jid | select -ExpandProperty subtasks
$st[0] | select -ExpandProperty status
```

## <a name="hana-license-key-and-vm-restore-via-azure-backup-service"></a>HANA lisans anahtarı ve VM Azure Backup hizmeti geri yükleme

Hello Azure Backup hizmeti tasarlanmış toocreate yeni bir VM geri yükleme sırasında ' dir. Toodo artık doğru hiçbir plan yoktur bir &quot;yerinde&quot; mevcut bir Azure VM'i geri yükleme.

![Bu şekilde hello Azure hizmeti hello geri yükleme seçeneği hello Azure portal gösterilmektedir.](media/sap-hana-backup-storage-snapshots/image019.png)

Bu şekilde hello Azure hizmeti hello geri yükleme seçeneği hello Azure portal gösterilmektedir. Bir geri yükleme sırasında bir VM oluşturma hello diskleri geri yükleme arasında seçim yapabilirsiniz. Merhaba diskleri geri yükledikten sonra hala gerekli toocreate üzerine yeni bir VM olur. Her yeni bir VM oluşturulan Azure hello benzersiz VM kimliği değişiklikler (bkz [erişme ve Azure VM benzersiz kimliği kullanarak](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/)).

![Bu şekilde hello Azure VM benzersiz kimliği, önce ve sonra Azure Backup hizmeti ile Merhaba geri yükleme gösterilmektedir.](media/sap-hana-backup-storage-snapshots/image020.png)

Bu şekilde hello Azure VM benzersiz kimliği önce ve sonra Azure Backup hizmeti ile Merhaba geri yükleme gösterilmektedir. Bu benzersiz VM kimliği lisans SAP için kullanılır, hello SAP donanım anahtarı kullanma Sonuç olarak, yeni bir SAP lisans VM geri yüklendikten sonra yüklü toobe sahiptir.

Yeni bir Azure yedekleme özelliği, bu yedekleme Kılavuzu hello oluşturma sırasında önizleme modunda sunulmadı. Merhaba VM yedekleme alınan hello VM üzerinde anlık görüntü tabanlı bir dosya düzeyinde geri yükleme sağlar. Bu hello gerek toodeploy yeni bir VM engeller ve bu nedenle hello benzersiz VM kimliği kalır aynı hello ve hiçbir yeni SAP HANA lisans anahtarı gereklidir. Tamamen test edildikten sonra bu özellik hakkında daha fazla belge sağlanacaktır.

Azure yedekleme sonunda Azure tek tek sanal diskleri yedekleme izin verir ve ayrıca dosyaları ve dizinleri içindeki VM hello. Azure Backup önemli bir avantajı, toodo kalmaktan hello müşteri kaydetme tüm hello yedeklemeler yönetimidir onu. Bir geri yükleme gerekli hale gelirse, Azure Backup hello doğru yedekleme toouse seçer.

## <a name="sap-hana-vm-backup-via-manual-disk-snapshot"></a>SAP HANA VM yedekleme el ile disk anlık görüntü aracılığıyla

Hello Azure Backup hizmeti kullanmak yerine, bir tek tek bir yedekleme çözümü PowerShell aracılığıyla el ile Azure VHD blob anlık görüntüleri oluşturarak yapılandırabilirsiniz. Bkz: [PowerShell ile kullanma blob anlık görüntüleri](https://blogs.msdn.microsoft.com/cie/2016/05/17/using-blob-snapshots-with-powershell/) hello adımları açıklaması.

Daha fazla esneklik sağlar ancak bu belgenin önceki bölümlerinde açıklanan hello sorunları gidermek değil:

- Bir hala SAP HANA tutarlı bir durumda olduğundan emin olmanız gerekir
- VM belirten bir hata nedeniyle bir kira serbest hello varsa bile hello işletim sistemi diski üzerine yazılamaz. Silme hello sonra tooa yeni benzersiz VM kimliği ve hello gerek tooinstall yeni bir SAP lisans sunulmasını VM yalnızca çalışır.

![Olası toorestore yalnızca hello veri disklerinin bir Azure VM değil](media/sap-hana-backup-storage-snapshots/image021.png)

Bu olası toorestore yalnızca hello veri diskleri yeni ve benzersiz bir VM kimliği alma hello sorunu önlemenin bir Azure VM ve, bu nedenle, hello SAP lisans geçersiz:

- Merhaba test için iki Azure veri diskleri ekli tooa VM olan ve yazılım RAID bunların üstüne tanımlandı 
- Bunu SAP HANA tutarlı bir durumda olduğunu SAP HANA anlık görüntü özelliği tarafından onaylanıp
- Dosya sistemi donmasına (bkz _depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığını_ hello ilgili makalede [yedekleme Kılavuzu SAP HANA Azure sanal makineler üzerinde](sap-hana-backup-guide.md))
- BLOB anlık görüntüleri hem veri disklerinden gerçekleştirilen
- Dosya Sistemi Çöz
- SAP HANA anlık görüntü onayı
- toorestore hello veri diskleri hello VM kapatıldı ve her iki diskin ayrılmış
- Hello disk ayırma sonra bunlar sahip hello eski blob anlık görüntüleri verilerinin üzerine yazıldı
- Geri hello sanal diskler bağlı yeniden toohello VM
- Başlangıç hello RAID düzgün çalıştığını ve toohello blob döndürülmek hello yazılım her şeyi VM anlık görüntü saat sonra
- HANA toohello HANA anlık görüntü geri ayarlandı

SAP HANA aşağı olası tooshut hello blob anlık görüntüleri önce yazılmışsa hello yordamı daha az karmaşık olabilir. Bu durumda, bir hello HANA anlık görüntü atlayın ve, hiçbir şey hello sistemde olacağına hello dosya sistemi dondurma de atlayabilirsiniz. Her şeyi çevrimiçi durumdayken gerekli toodo anlık görüntüleri olduğunda eklenen karmaşıklık hello devreye. Bkz: _depolama anlık görüntüleri duruma getirirken SAP HANA veri tutarlılığını_ hello ilgili makalede [yedekleme Kılavuzu SAP HANA Azure sanal makineler üzerinde](sap-hana-backup-guide.md).

## <a name="next-steps"></a>Sonraki adımlar
* [SAP HANA için yedekleme Kılavuzu Azure sanal makineler üzerinde](sap-hana-backup-guide.md) genel bir bakış ve çalışmaya başlama hakkında bilgi sağlar.
* [SAP HANA yedekleme tabanlı dosya düzeyinde](sap-hana-backup-file-level.md) kapsar hello dosya tabanlı yedekleme seçeneği.
* tooestablish yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA planlama (büyük örnekler), azure'da nasıl görürüm toolearn [SAP HANA (büyük örnekler) Azure üzerinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma](hana-overview-high-availability-disaster-recovery.md).
