---
title: "Windows ve Linux Iaas VM'ler için Disk şifrelemesi aaaAzure | Microsoft Docs"
description: "Bu makale için Microsoft Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler genel bakış sağlar."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a>Windows ve Linux Iaas VM'ler için Azure Disk şifrelemesi
Microsoft Azure veri gizliliğinizi veri egemenliği kesinlikle taahhüt tooensuring olduğundan ve Azure barındırılan toocontrol sağlayan gelişmiş teknolojiler tooencrypt çeşitli verilerine denetlemek ve şifreleme anahtarlarını yönetmek veri denetim & Denetim erişimi. Bu Azure müşterilerin kendi iş ihtiyaçlarına en iyi karşılayan hello esneklik toochoose hello çözümü sağlar. Bu yazıda, biz, tooa yeni teknoloji çözümü "Windows ve Linux Iaas VM'in Azure Disk şifrelemesi" tanıtılacaktır toohelp korumak ve veri toomeet, kuruluş güvenlik ve uyumluluk taahhüt koruyun. Merhaba kağıt senaryoları ve hello kullanıcı deneyimleri hello dahil olmak üzere toouse hello Azure disk şifrelemesi özelliklerini nasıl desteklenmiyor ayrıntılı kılavuz sunar.

> [!NOTE]
> Bazı öneriler verileri, ağ veya ek lisans ya da abonelik maliyetlerinizi kaynaklanan hesaplama kaynak kullanımını artırabilir.

## <a name="overview"></a>Genel Bakış
Azure Disk şifrelemesi, Windows ve Linux Iaas sanal makine disklerinizi şifrelemek yardımcı olan yeni bir özelliktir. Azure Disk şifrelemesi yararlanır hello endüstri standardı [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) özelliği Windows hello ve [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) hello işletim sistemi ve hello veri diskleri için Linux tooprovide birim şifrelemesi özelliğidir. Merhaba çözümü ile tümleştirildiğinde [Azure anahtar kasası](https://azure.microsoft.com/documentation/services/key-vault/) denetlemek ve hello disk şifreleme anahtarları ve gizli anahtar kasası aboneliğinizi yönetmek toohelp. Merhaba çözüm ayrıca hello sanal makine disklerdeki tüm veriler Azure depolama alanınızı bekleyen şifrelenmesini sağlar.

Azure disk şifrelemesi Windows ve Linux Iaas VM'ler için şimdi olan **genel kullanılabilirlik** tüm Azure genel bölgeler ve premium depolama ile standart VM'ler ve sanal makineleri için AzureGov bölgeler.

### <a name="encryption-scenarios"></a>Şifreleme senaryosu
Hello Azure Disk şifrelemesi çözüm müşteri senaryoları aşağıdaki hello destekler:

* Önceden şifrelenmiş VHD ve şifreleme anahtarlarını oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin
* Desteklenen hello Azure galeri görüntüleri kullanılarak oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin
* Azure'da çalışan Iaas VM'ler şifrelemeyi etkinleştirin
* Windows Iaas Vm'leri üzerinde şifrelemeyi devre dışı bırak
* Veri sürücülerini şifreleme Linux Iaas VM'ler için devre dışı bırak
* Yönetilen diskin VM'ler şifrelemeyi etkinleştir
* Mevcut şifrelenmiş premium olmayan depolama VM şifreleme ayarlarını güncelleştir
* Yedekleme ve geri yükleme anahtar şifreleme anahtarıyla şifrelenir şifrelenmiş VM'ler

Microsoft Azure'da etkinleştirildiğinde senaryoları Iaas VM'ler için aşağıdaki hello Hello çözümünü destekler:

* Azure anahtar kasası ile tümleştirme
* Standart katmanı VMs: [A, D, DS, G, GS, F ve benzeri serisi Iaas VM'ler](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Windows ve Linux Iaas Vm'leri ve hello yönetilen diskten VM'ler etkinleştir şifreleme Azure galeri görüntüleri desteklenen
* Windows Iaas Vm'leri ve yönetilen disk VM'ler için işletim sistemi ve veri sürücülerde şifreleme devre dışı bırak
* Veri sürücülerini şifreleme Linux Iaas Vm'leri ve yönetilen disk VM'ler için devre dışı bırak
* Iaas Windows istemci işletim sistemi çalıştıran VM'ler şifrelemeyi etkinleştirin
* Bağlama yolları birimlerle şifrelemeyi etkinleştirin
* Linux VM diskle yapılandırılmış şifrelemeyi etkinleştirin mdadm kullanarak şeritleme (RAID)
* Veri diskleri için LVM kullanarak Linux VM'ler şifrelemeyi etkinleştirin
* Windows VM depolama alanları ile yapılandırılmış şifrelemeyi etkinleştirin
* Mevcut şifrelenmiş premium olmayan depolama VM şifreleme ayarlarını güncelleştir
* Tüm Azure genel ve AzureGov bölgeleri desteklenir

Merhaba çözüm senaryoları, özellikleri ve teknoloji aşağıdaki hello desteklemez:

* Temel katman Iaas VM'ler
* Bir işletim sistemi sürücüsünde Linux Iaas VM'ler için şifrelemeyi devre dışı bırakma
* Merhaba işletim sistemi sürücüsü Linux Iaas VM'ler için şifreliyse, şifreleme veri sürücüsünde devre dışı bırakma
* Merhaba Klasik VM oluşturma yöntemini kullanarak oluşturduğunuz Iaas VM'ler
* Windows ve Linux Iaas VM'ler müşteri özel resimler desteklenmiyor şifrelemeyi etkinleştirin. Enccryption etkinleştirmek Linux LVM işletim sisteminde disk şu anda desteklenmiyor. Bu destek yakında gelecektir.
* Şirket içi anahtar yönetimi hizmeti ile tümleştirme
* Azure dosyaları (paylaşılan dosya sistemi), ağ dosya sistemi (NFS), dinamik birimler ve yazılım tabanlı RAID sistemler ile yapılandırılmış Windows VM'ler
* Yedekleme ve geri yükleme anahtar şifreleme anahtarı olmadan şifrelenmiş şifrelenmiş VM'lerin.
* Varolan bir şifrelenmiş premium Storage VM şifreleme ayarlarını güncelleştirin.

> [!NOTE]
> Yedekleme ve geri yükleme şifrelenmiş VM'lerin hello KEK yapılandırmayla şifrelenmiş VM'ler için desteklenir. KEK şifrelenmiş vm'lerde desteklenmez. KEK VM şifreleme sağlayan isteğe bağlı bir parametredir. Bu desteği yakında geliyor.
> VM desteklenmez varolan bir şifrelenmiş premium Storage şifreleme ayarlarını güncelleştirin. Bu desteği yakında geliyor.

### <a name="encryption-features"></a>Şifreleme özellikleri
Etkinleştirme ve Azure Iaas VM'ler için Azure Disk şifrelemesi dağıtma hello aşağıdaki özellikleri, sağlanan hello yapılandırmasına bağlı olarak etkinleştirilir:

* Merhaba işletim sistemi birimi tooprotect hello önyükleme biriminin depolama alanınızın bekleyen şifreleme
* Veri birimleri tooprotect hello veri birimleri depolama alanınızın bekleyen şifreleme
* Windows Iaas VM'ler için sürücüleri hello işletim sistemi ve veri şifreleme devre dışı bırakma
* (Yalnızca işletim sistemi şifreli değil sürücü varsa) hello veriler üzerinde şifrelemeyi devre dışı bırakma Linux Iaas VM'ler için sürücüler
* Merhaba şifreleme anahtarları ve gizli anahtar kasası aboneliğinizde koruma
* Iaas VM şifrelenmiş hello Hello şifreleme durumu raporlama
* Disk şifrelemesi yapılandırma ayarlarını hello Iaas sanal makinesinden kaldırılması
* Yedekleme ve geri yükleme hello Azure Yedekleme hizmetini kullanarak şifrelenmiş VM'ler

> [!NOTE]
> Yedekleme ve geri yükleme şifrelenmiş VM'lerin hello KEK yapılandırmayla şifrelenmiş VM'ler için desteklenir. KEK şifrelenmiş vm'lerde desteklenmez. KEK VM şifreleme sağlayan isteğe bağlı bir parametredir.

Windows ve Linux çözüm için Iaas VM'ler için Azure Disk şifrelemesi içerir:

* için Windows Hello disk şifrelemesi uzantısı.
* Linux için Hello disk şifrelemesi uzantısı.
* Merhaba disk şifrelemesi PowerShell cmdlet'leri.
* disk şifrelemesi Azure komut satırı arabirimi (CLI) cmdlet'leri hello.
* Merhaba disk şifrelemesi Azure Resource Manager şablonları.

Hello Azure Disk şifrelemesi çözüm Iaas Vm'leri üzerinde Windows veya Linux işletim sistemi çalıştıran desteklenir. Merhaba desteklenen işletim sistemleri hakkında daha fazla bilgi için bkz: hello "Önkoşullar" bölümü.

> [!NOTE]
> VM diskleri Azure Disk şifrelemesi ile şifrelemek için ek ücret yoktur.

### <a name="value-proposition"></a>Değer önerisi
Hello Azure Disk şifrelemesi yönetimi çözümü uyguladığınızda, hello aşağıdaki iş gereksinimlerini karşılayabilen:

* Endüstri standardı şifreleme teknolojisi tooaddress kuruluş güvenlik ve uyumluluk gereksinimleri kullanabileceğinizden Iaas Vm'leri, bekleyen güvenli hale getirilir.
* Iaas Vm'leri önyükleme müşteri denetlenen anahtarlar ve ilkeleri ve altında kullanımları anahtar kasanızdaki denetleyebilirsiniz.

### <a name="encryption-workflow"></a>Şifreleme iş akışı
Windows ve Linux VM'ler için tooenable disk şifrelemesi hello aşağıdaki:

1. Bir şifreleme senaryosu şifreleme senaryosu önceki hello kümelerini seçin.
2. Tooenabling disk şifrelemesi'hello Azure Disk şifrelemesi Resource Manager şablonu, PowerShell cmdlet'lerini veya CLI komutu aracılığıyla kabul ve hello şifreleme yapılandırması belirtin.

   * Merhaba müşteri şifrelenmiş VHD senaryosu için şifrelenmiş hello VHD tooyour depolama hesabı ve hello şifreleme anahtar malzeme tooyour anahtar kasası karşıya yükleyin. Sonra yeni bir Iaas VM hello şifreleme yapılandırması tooenable şifreleme sağlar.
   * Market hello oluşturulan yeni VM'ler ve Azure'da zaten çalıştıran var olan VM'ler için hello Iaas VM üzerinde hello şifreleme yapılandırması tooenable şifreleme sağlar.

3. GRANT erişim toohello Azure platformu tooread hello şifreleme anahtar malzemesini (BitLocker şifreleme anahtarları Windows sistemleri için) ve Linux için parola hello Iaas VM, anahtar kasası tooenable şifreleme.

4. Hello Azure Active Directory (Azure AD) uygulama kimliği toowrite hello şifreleme anahtar malzeme tooyour anahtar kasası sağlar. Bunun yapılması, 2. adımda bahsedilen hello senaryoları için hello Iaas VM üzerinde şifrelemeyi etkinleştirir.

5. Azure hello VM hizmet modeli hello anahtar kasası yapılandırma ve şifreleme ile güncelleştirir ve şifrelenmiş VM'nizi ayarlar.

 ![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a>Şifre çözme iş akışı
toodisable disk şifrelemesi Iaas VM'ler, aşağıdaki üst düzey adımları tam hello için:

1. Hello Azure Disk şifrelemesi Resource Manager şablonu veya PowerShell cmdlet'leri aracılığıyla azure'da çalışan bir Iaas VM üzerinde toodisable şifreleme (şifre çözme) seçin ve hello şifre çözme yapılandırma belirtin.

 Bu adım hello işletim sistemi veya hello veri biriminin veya hem de Windows Iaas VM çalıştıran hello şifreleme devre dışı bırakır. Ancak, hello önceki bölümünde belirtildiği gibi Linux işletim sistemi disk şifrelemesi devre dışı bırakma desteklenmiyor. Merhaba işletim sistemi diski şifrelenmemiş sürece hello şifre çözme adım yalnızca Linux VM'ler veri sürücülerinde izin verilir.
2. VM hizmet modeli Azure güncelleştirmeleri hello ve hello Iaas VM şifresi çözülmüş işaretlenir. Merhaba VM Merhaba içeriğine artık bekleyen şifrelenir.

> [!NOTE]
> Merhaba şifreleme devre dışı bırakma işlemi, anahtar kasasını ve hello şifreleme anahtar malzemesi (BitLocker şifreleme anahtarları Windows sistemleri için) veya Linux için parola silmez.
 > Linux işletim sistemi disk şifrelemesi devre dışı bırakma desteklenmiyor. Merhaba şifre çözme adım yalnızca Linux VM'ler veri sürücülerinde izin verilir.
Merhaba işletim sistemi sürücüsü şifrelenmiş verileri disk şifrelemesi Linux için devre dışı bırakma desteklenmiyor.

## <a name="prerequisites"></a>Ön koşullar
Merhaba "Genel bakış" bölümünde ele alınan hello desteklenen senaryolar için Azure Disk şifrelemesi Azure Iaas Vm'leri üzerinde etkinleştirmeden önce önkoşulları aşağıdaki hello bakın:

* Geçerli etkin Azure aboneliği toocreate kaynakları Azure desteklenen hello bölgelerde olmalıdır.
* Azure Disk şifrelemesi, Windows Server sürümleri aşağıdaki hello üzerinde desteklenir: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016.
* Azure Disk şifrelemesi, Windows istemci sürümleri aşağıdaki hello üzerinde desteklenir: Windows 8 istemci ve Windows 10 istemci.

> [!NOTE]
> Windows Server 2008 R2 için .NET Framework 4.5 Azure şifreleme etkinleştirmeden önce yüklü olması gerekir. Windows Update'ten hello isteğe bağlı güncelleştirme Windows Server 2008 R2 x64 tabanlı sistemler için Microsoft .NET Framework 4.5.2 yükleyerek yükleyebilirsiniz ([KB2901983](https://support.microsoft.com/kb/2901983)).

* Azure Disk şifrelemesi desteklenir üzerinde hello Azure Galerisi aşağıdaki Linux sunucu dağıtımları ve sürümleri göre:

| Linux dağıtım | Sürüm | Şifreleme için desteklenen birim türü|
| --- | --- |--- |
| Ubuntu | 16.04 GÜNLÜK LTS | İşletim sistemi ve veri diski |
| Ubuntu | 14.04.5-DAILY-LTS | İşletim sistemi ve veri diski |
| Ubuntu | 12.10 | Veri diski |
| Ubuntu | 12.04 | Veri diski |
| RHEL | 7.3 | İşletim sistemi ve veri diski |
| RHEL | 7.2 | İşletim sistemi ve veri diski |
| RHEL | 6.8 | İşletim sistemi ve veri diski |
| RHEL | 6.7 | Veri diski |
| CentOS | 7.3 | İşletim sistemi ve veri diski |
| CentOS | 7.2n | İşletim sistemi ve veri diski |
| CentOS | 6.8 | İşletim sistemi ve veri diski |
| CentOS | 7.1 | Veri diski |
| CentOS | 7.0 | Veri diski |
| CentOS | 6.7 | Veri diski |
| CentOS | 6.6 | Veri diski |
| CentOS | 6.5 | Veri diski |
| openSUSE | 13.2 | Veri diski |
| SLES | 12 SP1 | Veri diski |
| SLES | 12-SP1 (Premium) | Veri diski |
| SLES | HPC 12 | Veri diski |
| SLES | 11-SP4 (Premium) | Veri diski |
| SLES | 11 SP4 | Veri diski |

* Azure Disk şifrelemesi gerektirir anahtar kasası ve VM'lerin hello aynı bulunması Azure bölgesi ve abonelik.

> [!NOTE]
> Bir hata, ayrı bölgelerde Hello kaynaklarını yapılandırma hello Azure Disk Şifrelemesi özelliğini etkinleştirme neden olur.

* tooset yukarı ve anahtar kasanızı Azure Disk şifrelemesi için yapılandırma, bölümüne bakın **ayarlamak ayarlama ve Azure Disk şifrelemesi için anahtar kasanızı yapılandırma** hello içinde *Önkoşullar* bu makalenin.
* tooset yukarı ve Azure AD uygulaması, Azure Disk şifrelemesi için Azure Active Directory'de yapılandırmak, bölümüne bakın **hello Azure AD uygulama Azure Active Directory'de ayarlama** hello içinde *Önkoşullar* Bu makalede bölümü.
* tooset yukarı ve Merhaba Azure AD uygulaması için hello anahtar kasası erişim ilkesini yapılandırmak için bölümüne bakın **Merhaba Azure AD uygulaması için hello anahtar kasası erişim ilkesi ayarlama** hello içinde *Önkoşullar* bölümü Bu makalede.
* tooprepare önceden şifrelenmiş bir Windows VHD bölümüne bakın **önceden şifrelenmiş Windows VHD hazırlama** hello içinde *ek*.
* tooprepare önceden şifrelenmiş bir Linux VHD bölümüne bakın **önceden şifrelenmiş Linux VHD hazırlama** hello içinde *ek*.
* Hello Azure platformu erişim toohello şifreleme anahtarları veya anahtar kasası toomake parolalarında gereken bunları kullanılabilir toohello sanal makine önyüklenir ve hello sanal makine işletim sistemi birimi şifresini çözer. toogrant izinleri tooAzure platform, kümesi hello **EnabledForDiskEncryption** hello anahtar kasası özelliği. Daha fazla bilgi için bkz: **ayarlamak ayarlama ve Azure Disk şifrelemesi için anahtar kasanızı yapılandırma** hello ek olarak.
* Anahtar kasası gizliliği ve KEK URL'leri sürümlü olmalıdır. Azure, bu sürüm kısıtlamasını zorlar. Geçerli gizli ve KEK URL'ler için örnek hello bakın:

  * Geçerli bir gizli URL örneği: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Geçerli bir KEK URL örneği: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* Azure Disk şifrelemesi anahtar kasasına gizli anahtarları ve KEK URL'leri parçası olarak belirterek bağlantı noktası numaralarını desteklemiyor. Desteklenmeyen ve desteklenen anahtar kasası URL'leri örnekler için hello aşağıdakilere bakın:

  * Kabul edilebilir anahtar kasası URL'si *https://contosovault.vault.azure.net:443/gizli/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*
  * Kabul edilebilir anahtar kasası URL'si: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*

* tooenable hello Azure Disk şifrelemesi özelliği, ağ uç noktası yapılandırması gereksinimleri aşağıdaki hello hello Iaas VM'ler karşılaması gerekir:
  * tooget bir belirteç tooconnect tooyour anahtar kasası, hello Iaas VM mümkün tooconnect tooan Azure Active Directory uç noktası, olmalıdır \[login.microsoftonline.com\].
  * toowrite hello şifreleme anahtarları tooyour anahtar kasası, hello Iaas VM mümkün tooconnect toohello anahtar kasası uç noktası olması gerekir.
  * Merhaba Iaas VM konakları Azure uzantısı depo ve ana VHD dosyaları hello Azure storage hesabı hello mümkün tooconnect tooan Azure storage uç olması gerekir.

  > [!NOTE]
  > Güvenlik ilkeniz Azure Vm'leri toohello Internet erişimi sınırlar, URI önceki hello çözün ve bir özel kural tooallow giden bağlantı toohello IP'leri yapılandırın.
  >
  >tooconfigure ve erişim Azure anahtar kasası (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall) bir güvenlik duvarının arkasında

* Azure PowerShell SDK sürüm tooconfigure Azure Disk şifrelemesi Hello en son sürümünü kullanın. Merhaba en son sürümünü indirme [Azure PowerShell sürüm](https://github.com/Azure/azure-powershell/releases)

 > [!NOTE]
  > Azure Disk şifrelemesi desteklenmiyor [Azure PowerShell SDK sürüm 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016). Bir hata alıyorsanız toousing Azure PowerShell 1.1.0, ilgili görmek [Azure Disk şifrelemesi ilgili hata tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).

* toorun herhangi bir Azure CLI komutu ve Azure aboneliğinizle ilişkilendirmek, Azure CLI yüklemelisiniz:
  * tooinstall Azure CLI ve Azure aboneliğinizle ilişkilendirmek için bkz: [nasıl tooinstall ve Azure CLI yapılandırma](../cli-install-nodejs.md).
  * toouse Mac, Linux ve Windows Azure Resource Manager ile Azure CLI bkz [Kaynak Yöneticisi modunda Azure CLI komutları](../virtual-machines/azure-cli-arm-commands.md).

* Yönetilen bir disk şifreleme zorunlu önkoşul tootake yönetilen hello diskin anlık görüntüsünü veya Azure Disk şifrelemesi önceki tooenabling şifreleme dışında hello disk yedeğini olur.  Yerinde bir yedekleme olmadan şifreleme sırasında beklenmeyen bir hata hello disk ve VM kurtarma seçeneği olmaksızın erişilemez hale getirebilir.  Set-AzureRmVMDiskEncryptionExtension şu anda yönetilen diskleri yedekleme ve hata hello - skipVmBackup parametresini belirtmediyseniz yönetilen bir diske karşı kullandıysanız çalışacaktır.  Bir yedekleme Azure Disk şifrelemesi dışında kılmadığınız sürece bu parametre güvensiz toouse olur.   Merhaba - skipVmBackup parametresi belirtildiğinde, hello cmdlet yönetilen hello disk önceki tooencryption yedeğini yapmaz.  Bu nedenle, bir zorunlu önkoşul toomake kurtarma sonraki olması durumunda VM yer önceki tooenabling Azure Disk şifrelemesi hello yönetilen disk yedeğini gerekli emin olarak değerlendirilir.  
> [!NOTE]
 > Azure Disk şifrelemesi dışında bir anlık görüntü veya yedekleme zaten yapılmış sürece hello - skipVmBackup parametresi hiçbir zaman kullanılmalıdır. 

* Hello Azure Disk şifrelemesi çözüm hello BitLocker dış anahtar koruyucusu Windows Iaas VM'ler için kullanır. Etki alanı için TPM koruyucusu zorla tüm grup ilkeleri birleştirilmiş VM'ler, vermeyin iletin. "Uyumlu TPM'siz BitLocker izin ver" Merhaba Grup İlkesi hakkında bilgi için bkz: [BitLocker Grup İlkesi başvurusu](https://technet.microsoft.com/library/ee706521).
* Özel Grup İlkesi ile etki alanına katılmış sanal makinelerde BitLocker İlkesi ayarı aşağıdaki hello içermelidir: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` Bitlocker için özel Grup İlkesi ayarları uyumsuz olduğunda Azure Disk şifrelemesi başarısız olur. Merhaba sahip değilse makinelerde hello yeni ilke tooupdate (gpupdate.exe/Force) zorlama ve yeniden başlatarak hello yeni ilke, uygulama doğru ilke ayarı, gerekli olabilir.  
* toocreate Azure AD uygulaması, bir anahtar kasası oluşturma veya varolan bir anahtar kasasını oluşturup ve şifrelemeyi etkinleştirmek, hello bkz [Azure Disk şifrelemesi önkoşul PowerShell Betiği](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).
* Hello Azure CLI kullanarak tooconfigure disk şifrelemesi önkoşulları bkz [bu Bash betik](https://github.com/ejarvi/ade-cli-getting-started).
* toouse hello Azure Backup hizmeti tooback yukarı ve şifreleme Azure Disk şifrelemesi ile etkinleştirilmişse, şifrelenmiş geri yükleme VM'ler Vm'leriniz hello Azure Disk şifrelemesi anahtar yapılandırmayı kullanarak şifreler. Merhaba Backup hizmeti yalnızca KEK yapılandırma kullanılarak şifrelenmiş Vm'leri destekler. Bkz: [tooback yedeklemek ve geri yükleme Azure yedekleme şifreleme ile sanal makineleri nasıl şifrelenmiş](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).

* Linux işletim sistemi birimi şifrelerken VM yeniden başlatma hello hello işleminin sonunda şu anda gerekli olmadığını unutmayın. Bu hello portal, powershell veya CLI yapılabilir.   Şifreleme tootrack hello ilerlemesini, Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus tarafından döndürülen hello durum iletisi düzenli aralıklarla yoklar.  Şifreleme işlemi tamamlandıktan sonra bu komutu tarafından döndürülen hello hello durum iletisi bunun belirtir.  Örneğin, "ProgressMessage: işletim sistemi diski başarıyla şifrelendi, lütfen hello VM yeniden başlatma" VM yeniden ve kullanılan bu noktası hello adresindeki.  

* Veri diskleri toohave Linux önceki tooencryption bağlı dosya sisteminde Linux için Azure Disk şifrelemesi gerektirir

* Yinelemeli olarak bağlı veri diskleri için Linux hello Azure Disk Şifrelemesi tarafından desteklenmez. Örneğin, Merhaba, hedef sistemin bir disk üzerinde /foo/bar bağladı ve ardından başka bir /foo/bar/baz, /foo/bar/baz hello şifrelenmesi başarılı olur ancak şifreleme/foo/çubuğunun başarısız olur. 

* Azure Disk şifrelemesi yalnızca hello daha önce bahsedilen önkoşulları karşılayan desteklenen Azure galeri görüntüleri desteklenir. Müşteri özel resimler son toocustom bölümleme şeması ve bu görüntülerinde bulunabilecek işlemi davranışları desteklenmez. Ayrıca, hatta galeri görüntüsü başlangıçta önkoşulların ancak oluşturma uyumsuz sonra değiştirilmiş VM'in temel.  İçin nedeni, bir Linux VM şifrelemek için yordamı hello önerilen bir temiz galeri görüntüsünden toostart olduğundan, hello VM şifrelemek ve ardından özel yazılım ya da veri toohello gerektiği gibi VM ekleyin.  

> [!NOTE]
> Yedekleme ve geri yükleme şifrelenmiş VM'lerin hello KEK yapılandırmayla şifrelenmiş VM'ler için desteklenir. KEK şifrelenmiş vm'lerde desteklenmez. KEK VM sağlayan isteğe bağlı bir parametredir.

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a>Hello Azure Active Directory'de Azure AD uygulaması ayarlayın
Azure'da çalışan bir VM etkin şifreleme toobe gerektiğinde Azure Disk şifrelemesi oluşturur ve hello şifreleme anahtarları tooyour anahtar kasası yazar. Anahtar kasanızı şifreleme anahtarlarını yönetme, Azure AD kimlik doğrulaması gerektirir.

Bu amaç için Azure AD uygulaması oluşturun. Uygulama hello "Merhaba uygulama için bir kimlik Get" bölümünde hello blog gönderisi kaydetme için ayrıntılı adımlar bulabilirsiniz [Azure anahtar kasası - adım adım](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). Bu post ayarlama ve anahtar kasanızı yapılandırma için yararlı örnekler sayısı da içerir. Kimlik doğrulama amacıyla istemci gizli anahtarı tabanlı kimlik doğrulaması veya istemci Azure AD sertifika tabanlı kimlik doğrulaması kullanabilirsiniz.

#### <a name="client-secret-based-authentication-for-azure-ad"></a>Azure AD için istemci gizli anahtarı tabanlı kimlik doğrulaması
izleyin hello bölümler bir istemci gizli anahtarı tabanlı kimlik doğrulaması için Azure AD yapılandırmanıza yardımcı olabilir.

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a>Azure PowerShell kullanarak Azure AD uygulaması oluşturma
PowerShell cmdlet toocreate Azure AD uygulaması aşağıdaki hello kullan:

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> $azureAdApplication.ApplicationId hello Azure AD ClientID ve $aadClientSecret hello istemci parolası sonraki tooenable Azure Disk şifrelemesi kullanmanız gerekir. Hello Azure AD gizli uygun şekilde koruyun.

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a>Hello Azure AD istemci kimliği ve parolası hello Klasik Azure Portalı ' ayarlama
Hello kullanarak Azure AD İstemci Kimliğini ve parolasını de ayarlayabilirsiniz [Klasik Azure portalı]( https://manage.windowsazure.com). tooperform bu görev, aşağıdaki hello:

1. Merhaba tıklatın **Active Directory** sekmesi.

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. Tıklatın **uygulama Ekle**ve ardından türü hello uygulama adı.

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. Hello ok düğmesine tıklayın ve ardından hello uygulama özelliklerini yapılandırın.

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. Merhaba alt sol köşe toofinish Hello onay işaretine tıklayın. Merhaba uygulama yapılandırma sayfası görünür ve hello Azure AD istemci kimliği hello sayfasının hello altında görüntülenir.

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. Merhaba tıklayarak Hello Azure AD gizli Kaydet **kaydetmek** düğmesi. Merhaba anahtarları metin kutusuna Hello Azure AD gizli unutmayın. Uygun şekilde koruyun.

 ![Azure Disk Şifrelemesi](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > Akış önceki hello hello Klasik Azure portalı üzerinde desteklenmiyor.

##### <a name="use-an-existing-application"></a>Varolan bir uygulama kullanın
tooexecute komutları aşağıdaki Merhaba, elde edilir ve hello [Azure AD PowerShell Modülü](https://technet.microsoft.com/library/jj151815.aspx).

> [!NOTE]
> Merhaba aşağıdaki komutları yeni bir PowerShell penceresinden yürütülmelidir. Azure PowerShell veya hello Azure Resource Manager penceresi tooexecute hello komutları kullanmayın. Bu cmdlet'ler hello MSOnline modül veya Azure AD PowerShell olduğundan bu yaklaşım öneririz.

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a>Azure AD için sertifika tabanlı kimlik doğrulaması
> [!NOTE]
> Azure AD sertifika tabanlı kimlik doğrulaması Linux VM'ler üzerinde şu anda desteklenmiyor.

Merhaba Göster nasıl izleyen bölümlerde tooconfigure bir sertifika tabanlı kimlik doğrulaması için Azure AD.

##### <a name="create-an-azure-ad-application"></a>Azure AD uygulaması oluştur
toocreate Azure AD uygulaması, PowerShell cmdlet'leri aşağıdaki hello yürütün:

> [!NOTE]
> Merhaba aşağıdaki değiştirin `yourpassword` , güvenli parola ve koruma hello parolayı dize.

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

Bu adımı tamamladıktan sonra bir PFX dosyası tooyour anahtar kasası karşıya yükleyin ve bu sertifikayı tooa VM hello erişim gerektirdiği ilke toodeploy etkinleştirin.

##### <a name="use-an-existing-azure-ad-application"></a>Var olan Azure AD uygulaması kullanın
Sertifika tabanlı kimlik doğrulaması olan bir uygulamanın yapılandırıyorsanız, burada gösterilen hello PowerShell cmdlet'lerini kullanın. Emin tooexecute olması atamalarını yeni bir PowerShell penceresi kaldırın.

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

Bu adımı tamamladıktan sonra bir PFX dosyası tooyour anahtar kasası karşıya yükleme ve toodeploy hello sertifika tooa VM gerekli olan hello erişim ilkesini etkinleştir.

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a>Bir PFX dosyası tooyour anahtar kasası karşıya yükle
Bu işlem ayrıntılı bir açıklaması için bkz: [resmi Azure anahtar kasası ekip blogu hello](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx). Ancak, PowerShell cmdlet'leri aşağıdaki hello hello görev için gereken her şeyi değildir. Emin tooexecute olması bunları Azure PowerShell konsolundan.

> [!NOTE]
> Merhaba aşağıdaki değiştirin `yourpassword` , güvenli parola ve koruma hello parolayı dize.

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a>Var olan VM, anahtar kasası tooan sertifikada dağıtma
Merhaba PFX yüklemeyi tamamladıktan sonra VM hello aşağıdakilerle varolan hello anahtar kasası tooan sertifikada dağıtın:
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a>Merhaba Azure AD uygulaması için hello anahtar kasası erişim ilkesi ayarlama
Azure AD uygulaması hakları tooaccess hello anahtarları veya hello kasadaki gizli anahtarları gerekiyor. Kullanım hello [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) (Merhaba uygulaması kaydolurken oluşturuldu) hello istemci kimliği hello kullanarak cmdlet toogrant izinleri toohello uygulaması, _– ServicePrincipalName_ parametre değeri. toolearn daha hello blog yayınına bakın [Azure anahtar kasası - adım adım](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx). İşte tooperform bu nasıl görev aracılığıyla, bir örnek PowerShell:

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> Azure Disk şifrelemesi erişim ilkeleri tooyour Azure AD istemci uygulaması aşağıdaki tooconfigure hello gerektirir: _WrapKey_ ve _ayarlamak_ izinleri.

## <a name="terminology"></a>Terminoloji
Merhaba Ortak terimleri bazıları bu teknoloji, aşağıdaki terimler tablonun kullanım hello tarafından kullanılan toounderstand:

| Terminoloji | Tanım |
| --- | --- |
| Azure AD | Azure ad [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/). Bir Azure AD hesabının kimlik doğrulaması, depolama ve gizli anahtar Kasası'nı almak için bir önkoşuldur. |
| Azure Key Vault | Anahtar kasası, şifreleme anahtarlarını ve gizli gizli korumaya yardımcı olmak Federal Bilgi işleme standartları FIPS doğrulamalı donanım güvenlik modülleri üzerinde temel bir şifreleme, anahtar yönetim hizmetidir. Daha fazla bilgi için bkz: [anahtar kasası](https://azure.microsoft.com/services/key-vault/) belgeleri. |
| ARM | Azure Resource Manager |
| BitLocker'ı |[BitLocker'ı](https://technet.microsoft.com/library/hh831713.aspx) tooenable disk şifrelemesi Windows Iaas sanal makinelerin kullandığı bir endüstri tanınan Windows birim şifreleme teknolojisidir. |
| BEK | BitLocker şifreleme anahtarları kullanılan tooencrypt hello işletim sistemi önyükleme birimi ve veri birimlerini ' dir. Merhaba BitLocker anahtarları anahtar kasasına gizli korunur. |
| CLI | Bkz: [Azure komut satırı arabirimi](../cli-install-nodejs.md). |
| DM-Crypt |[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) tooenable disk şifrelemesi Linux Iaas VM'ler üzerinde kullanılan hello Linux tabanlı, saydam disk şifreleme alt sistemi. |
| KEK | Anahtar şifreleme anahtarı tooprotect kullanın veya hello gizli sarmalamak hello asimetrik (RSA 2048) anahtardır. Bir donanım güvenlik modülleri (HSM) sağlayabilir-korumalı anahtar veya yazılım korumalı anahtarı. Daha fazla ayrıntı için bkz: [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) belgeleri. |
| PS cmdlet'leri | Bkz: [Azure PowerShell cmdlet'lerini](/powershell/azure/overview). |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a>Ayarlama ve anahtar kasanızı Azure Disk şifrelemesi için yapılandırma
Azure Disk şifrelemesi koruma hello disk şifreleme anahtarları ve anahtar kasanızdaki gizli anahtarları yardımcı olur. tooset anahtar kasanızı Azure Disk şifrelemesi için yukarı tam hello her hello bölümleri aşağıdaki adımları.

#### <a name="create-a-key-vault"></a>Bir anahtar kasası oluşturma
toocreate bir anahtar kasası seçenekleri aşağıdaki hello birini kullanın:

* ["101-anahtar-kasa-" Resource Manager şablonu oluştur](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [Azure PowerShell anahtar kasası cmdlet'leri](/powershell/module/azurerm.keyvault/#key_vault)
* Azure Resource Manager
* Nasıl çok[anahtar kasanızı güvenli](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)

> [!NOTE]
> Aboneliğiniz için bir anahtar kasasını zaten ayarladıysanız toohello sonraki bölüme atlayın.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a>Bir anahtar şifreleme anahtarı (isteğe bağlı) ayarlama
Ek bir hello BitLocker şifreleme anahtarları için güvenlik katmanı için toouse bir KEK istiyorsanız bir KEK tooyour anahtar kasası ekleyin. Kullanım hello [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate hello anahtar kasasına bir anahtar şifreleme anahtarı. Ayrıca, şirket içi Anahtar Yönetimi'nden HSM bir KEK içeri aktarabilirsiniz. Daha fazla ayrıntı için bkz: [anahtar kasası belgelerine](https://azure.microsoft.com/documentation/services/key-vault/).

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

Anahtar kasası arabirimi kullanarak veya tooAzure Resource Manager giderek hello KEK ekleyebilirsiniz.

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a>Anahtar kasası izinleri ayarlama
Hello Azure platformu erişim toohello şifreleme anahtarları veya anahtar kasası toomake parolalarında gereken bunları kullanılabilir toohello önyüklenmesini ve hello birimleri şifresini çözmek için VM. toogrant izinleri toohello Azure platformu kümesi hello **EnabledForDiskEncryption** hello anahtar özelliğinde kasa hello anahtar kasası PowerShell cmdlet'ini kullanarak:

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

Merhaba de ayarlayabilirsiniz **EnabledForDiskEncryption** hello ziyaret özelliğini [Azure kaynak Gezgini](https://resources.azure.com).

Daha önce belirtildiği gibi hello ayarlamalısınız **EnabledForDiskEncryption** anahtar kasanızı özelliği. Aksi takdirde hello dağıtım başarısız olur.

Aşağıda gösterildiği gibi Azure AD uygulamanız hello anahtar kasası arabiriminden için erişim ilkeleri ayarlayabilirsiniz:

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

Merhaba üzerinde **Gelişmiş erişim ilkeleri** sekmesinde, anahtar kasanızı Azure Disk şifrelemesi için etkinleştirildiğinden emin olun:

![Azure anahtar kasası](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a>Disk şifrelemesi dağıtım senaryoları ve kullanıcı deneyimleri
Çok sayıda disk şifrelemesi senaryolarına olanak sağlayabilirsiniz ve hello adımlar according toohello senaryo değişebilir. Merhaba aşağıdaki bölümlerde daha ayrıntılı hello senaryoları kapsar.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a>Market hello oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin
Disk şifrelemesi'hello Azure Marketi'nde yeni Iaas Windows VM'den hello kullanarak etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).

1. Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.

2. Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** yeni bir Iaas VM tooenable şifreleme.

> [!NOTE]
> Bu şablon, yeni bir şifrelenmiş Windows hello Windows Server 2012 galeri görüntüsü kullanan VM oluşturur.

Bu kullanarak yeni bir Iaas RedHat Linux 7.2 VM 200 GB RAID-0 diziye sahip disk şifrelemeyi etkinleştirebilirsiniz [Resource Manager şablonu](https://aka.ms/fde-rhel). Merhaba şablon dağıttıktan sonra hello kullanarak hello VM şifreleme durumunu doğrulamak `Get-AzureRmVmDiskEncryptionStatus` açıklandığı gibi cmdlet [şifreleme işletim sistemi üzerinde çalışan bir Linux VM sürücü](#encrypting-os-drive-on-a-running-linux-vm). Merhaba makine durumu döndüğünde _VMRestartPending_, hello VM yeniden başlatın.

Merhaba aşağıdaki tabloda hello Resource Manager şablonu parametreleri hello Market senaryodan Azure AD İstemci Kimliğini kullanarak yeni VM'ler listelenmektedir:

| Parametre | Açıklama |
| --- | --- |
| adminUserName | Merhaba sanal makine için yönetici kullanıcı adı. |
| Admınpassword | Merhaba sanal makine için yönetici kullanıcı parolası. |
| newStorageAccountName | Merhaba depolama hesabı toostore işletim sistemi ve veri VHD'ler adı. |
| vmSize | Merhaba VM boyutu. Şu anda yalnızca standart bir, D ve G serisi desteklenir. |
| virtualNetworkName | Merhaba VNet bu hello VM NIC adını ait. |
| subnetName | Merhaba VNet bu hello VM NIC hello alt ağ adı için ait olmalıdır. |
| Aadclientıd | İzinleri toowrite gizli tooyour anahtar kasası olan hello Azure AD uygulama istemci kimliği. |
| AADClientSecret | İzinleri toowrite gizli tooyour anahtar kasası olan hello Azure AD uygulama istemci gizli anahtarı. |
| keyVaultURL | Başlangıç anahtarı URL'sini kasa bu hello BitLocker anahtarını karşıya yüklenmelidir. Merhaba cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`. |
| keyEncryptionKeyURL | Kullanılan tooencrypt hello hello anahtar şifreleme anahtarı URL'sini (isteğe bağlı) BitLocker anahtarı oluşturulur. |
| keyVaultResourceGroup | Merhaba anahtar kasasının kaynak grubu. |
| vmName | Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır. |

> [!NOTE]
> _KeyEncryptionKeyURL_ isteğe bağlı bir parametredir. Anahtar kasanızı kendi KEK toofurther koruma hello veri şifreleme anahtarı (parola gizli) kullanıma sunabilirsiniz.

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a>VHD müşteri şifrelenmiş ve şifreleme anahtarlarını oluşturulan yeni Iaas VM'ler şifrelemeyi etkinleştirin
Bu senaryoda, hello Resource Manager şablonu, PowerShell cmdlet'leri veya CLI komutları kullanarak şifreleme etkinleştirebilirsiniz. Merhaba aşağıdaki bölümlerde daha fazla ayrıntı hello Resource Manager şablonu ve CLI komutları açıklanmaktadır.

Azure'da kullanılabilen önceden şifrelenmiş görüntüleri hazırlama için bu bölümleri birinden Hello yönergeleri izleyin. Merhaba görüntü oluşturulduktan sonra hello sonraki bölümde toocreate içinde şifrelenmiş bir Azure VM hello adımları kullanabilirsiniz.

* [Önceden şifrelenmiş Windows VHD hazırlama](#preparing-a-pre-encrypted-windows-vhd)
* [Önceden şifrelenmiş Linux VHD hazırlama](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a>Merhaba Resource Manager şablonu kullanarak
Hello kullanarak, şifrelenmiş VHD disk şifrelemesi etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).

1. Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.

2. Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** tooenable şifreleme hello yeni Iaas VM.

Merhaba aşağıdaki tabloda hello Resource Manager şablonu parametreleri, şifrelenmiş VHD için listelenmektedir:

| Parametre | Açıklama |
| --- | --- |
| newStorageAccountName | Merhaba depolama hesabı toostore hello adını OS VHD şifrelenir. Bu depolama hesabı zaten hello aynı oluşturulmuş kaynak grubu ve hello VM ile aynı konumda. |
| osVhdUri | Merhaba depolama hesabından hello OS VHD URI'si. |
| osType | İşletim sistemi ürün türü (Windows/Linux). |
| virtualNetworkName | Merhaba VNet bu hello VM NIC adını ait. Merhaba adı zaten hello aynı oluşturulmuş olmalıdır kaynak grubu ve hello VM ile aynı konumda. |
| subnetName | Merhaba VNet bu hello VM NIC üzerinde hello alt ağ adı için ait olmalıdır. |
| vmSize | Merhaba VM boyutu. Şu anda yalnızca standart bir, D ve G serisi desteklenir. |
| Keyvaultresourceıd | Merhaba hello anahtar kasası kaynağı Azure Kaynak Yöneticisi'nde tanımlayan ResourceId. Merhaba PowerShell cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`. |
| keyVaultSecretUrl | Merhaba anahtar kasasına ayarlamak hello disk şifreleme anahtarı URL'si. |
| keyVaultKekUrl | Oluşturulan hello disk şifreleme anahtarı şifrelemek için anahtar şifreleme anahtarı hello URL'si. |
| vmName | Merhaba Iaas VM adıdır. |

#### <a name="using-powershell-cmdlets"></a>PowerShell cmdlet'lerini kullanarak
Merhaba PowerShell cmdlet'ini kullanarak, şifrelenmiş VHD disk şifrelemesi etkinleştirebilirsiniz [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).  

#### <a name="using-cli-commands"></a>CLI komutları kullanarak
CLI komutları kullanarak bu senaryo için tooenable disk şifrelemesi hello aşağıdaki:

1. Erişim ilkeleri, anahtar kasanızı ayarlayın:

   * Set hello **EnabledForDiskEncryption** bayrağı:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * İzinleri tooAzure AD uygulama toowrite gizli tooyour anahtar kasası ayarlayın:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. bir var olan veya çalışan VM türü tooenable şifreleme:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Şifreleme durumu alın:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. Yeni bir VM, şifrelenmiş VHD'den hello parametrelerle aşağıdaki kullanım hello tooenable şifreleme `azure vm create` komutu:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a>Var olan veya Iaas Windows VM Azure'da çalışan şifrelemeyi etkinleştir
Bu senaryoda, hello Resource Manager şablonu, PowerShell cmdlet'leri veya CLI komutları kullanarak şifreleme etkinleştirebilirsiniz. Merhaba aşağıdaki bölümlerde açıklanmıştır daha ayrıntılı biçimde nasıl Resource Manager şablonu ve CLI komutları kullanarak hello tooenable.

#### <a name="using-hello-resource-manager-template"></a>Merhaba Resource Manager şablonu kullanarak
Var olan veya hello kullanarak Iaas Windows Vm'lerini Azure'da çalışan disk şifrelemesi etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).

1. Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.

2. Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** varolan veya Iaas VM çalıştıran hello tooenable şifreleme.

Merhaba aşağıdaki tabloda hello Resource Manager şablonu parametrelerinin varolan veya bir Azure AD İstemci Kimliğini kullanan sanal makineleri çalıştıran listelenmektedir:

| Parametre | Açıklama |
| --- | --- |
| Aadclientıd | İzinleri toowrite gizli toohello anahtar kasası olan hello Azure AD uygulama istemci kimliği. |
| AADClientSecret | İzinleri toowrite gizli toohello anahtar kasası olan hello Azure AD uygulama istemci gizli anahtarı. |
| keyVaultName | Merhaba anahtarın adını kasa bu hello BitLocker anahtarını karşıya yüklenmelidir. Merhaba cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | Kullanılan tooencrypt hello hello anahtar şifreleme anahtarı URL'sini BitLocker anahtarı oluşturulur. Bu seçerseniz isteğe bağlı bir parametredir **nokek** hello UseExistingKek aşağı açılan listesinde. Seçerseniz **kek** hello UseExistingKek aşağı açılan listesinde, hello girmelisiniz _keyEncryptionKeyURL_ değeri. |
| volumeType | Merhaba şifreleme işlemi gerçekleştirilir birim türü. Geçerli değerler _OS_, _veri_, ve _tüm_. |
| sequenceVersion | Merhaba BitLocker işlemi sürümü dizisi. Disk şifrelemesi işlemi hello üzerinde gerçekleştirilen her zaman bu sürüm numarasını Artır aynı VM. |
| vmName | Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır. |

> [!NOTE]
> _KeyEncryptionKeyURL_ isteğe bağlı bir parametredir. Merhaba anahtar kasasına kendi KEK toofurther koruma hello veri şifreleme anahtarı (BitLocker şifreleme gizli) kullanıma sunabilirsiniz.

#### <a name="using-powershell-cmdlets"></a>PowerShell cmdlet'lerini kullanarak
Merhaba blog gönderileri PowerShell cmdlet'lerini kullanarak şifreleme Azure Disk şifrelemesi ile etkinleştirme hakkında daha fazla bilgi için bkz: [keşfedin Azure Disk şifrelemesi Azure PowerShell - bölüm 1 ile](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) ve [Azure Disk şifrelemesi keşfedin Azure PowerShell ile - bölüm 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

#### <a name="using-cli-commands"></a>CLI komutları kullanarak
var olan veya Iaas Windows VM CLI komutları kullanarak Azure'da çalışan tooenable şifreleme hello aşağıdaki:

1. Merhaba anahtar kasası erişim ilkelerini tooset:
   * Set hello **EnabledForDiskEncryption** bayrağı:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * İzinleri tooAzure AD uygulama toowrite gizli tooyour anahtar kasası ayarlayın:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. var olan veya çalışan VM tooenable şifreleme:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. tooget şifreleme durumu:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. Yeni bir VM, şifrelenmiş VHD'den hello parametrelerle aşağıdaki kullanım hello tooenable şifreleme `azure vm create` komutu:

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a>Azure'da bir var olan veya çalışan Iaas Linux VM şifrelemeyi etkinleştirin
Hello kullanarak var olan veya çalışan Iaas Linux VM'de Azure disk şifrelemesi etkinleştirebilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).

1. Tıklatın **tooAzure dağıtmak** hello Azure hızlı başlangıç şablona hello şifreleme yapılandırması üzerinde hello girin **parametreleri** dikey ve ardından **Tamam**.

2. Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** varolan veya Iaas VM çalıştıran hello tooenable şifreleme.

Aşağıdaki tablonun hello Resource Manager şablonu parametrelerinin varolan veya bir Azure AD İstemci Kimliğini kullanan sanal makineleri çalıştıran listeler:

| Parametre | Açıklama |
| --- | --- |
| Aadclientıd | İzinleri toowrite gizli toohello anahtar kasası olan hello Azure AD uygulama istemci kimliği. |
| AADClientSecret | İzinleri toowrite gizli tooyour anahtar kasası olan hello Azure AD uygulama istemci gizli anahtarı. |
| keyVaultName | Merhaba anahtarın adını kasa bu hello BitLocker anahtarını karşıya yüklenmelidir. Merhaba cmdlet'ini kullanarak elde edebilirsiniz `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`. |
|  keyEncryptionKeyURL | Kullanılan tooencrypt hello hello anahtar şifreleme anahtarı URL'sini BitLocker anahtarı oluşturulur. Bu seçerseniz isteğe bağlı bir parametredir **nokek** hello UseExistingKek aşağı açılan listesinde. Seçerseniz **kek** hello UseExistingKek aşağı açılan listesinde, hello girmelisiniz _keyEncryptionKeyURL_ değeri. |
| volumeType | Merhaba şifreleme işlemi gerçekleştirilir birim türü. Geçerli desteklenen değerler _OS_ veya _tüm_ (için RHEL 7.2, CentOS 7.2 ve Ubuntu 16.04), ve _veri_ (için tüm diğer dağıtımlar için). |
| sequenceVersion | Merhaba BitLocker işlemi sürümü dizisi. Disk şifrelemesi işlemi hello üzerinde gerçekleştirilen her zaman bu sürüm numarasını Artır aynı VM. |
| vmName | Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır. |
| Parola | Merhaba veri şifreleme anahtarı güçlü bir parola yazın. |

> [!NOTE]
> _KeyEncryptionKeyURL_ isteğe bağlı bir parametredir. Anahtar kasanızı kendi KEK toofurther koruma hello veri şifreleme anahtarı (parola gizli) kullanıma sunabilirsiniz.

#### <a name="cli-commands"></a>CLI komutları
Disk şifrelemesi yükleme ve hello kullanma, şifreli VHD etkinleştirebilirsiniz [CLI komutu](../cli-install-nodejs.md). var olan veya CLI komutları kullanarak Azure Iaas Linux VM'ler çalıştıran tooenable şifreleme hello aşağıdaki:

1. Erişim ilkeleri hello anahtar kasasına ayarlayın:

 * Set hello **EnabledForDiskEncryption** bayrağı:

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * İzinleri tooAzure AD uygulama toowrite gizli tooyour anahtar kasası ayarlayın:

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. var olan veya çalışan VM tooenable şifreleme:

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. Şifreleme durumu alın:

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. Yeni bir VM, şifrelenmiş VHD'den hello parametrelerle aşağıdaki kullanım hello tooenable şifreleme `azure vm create` komutu:
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a>Şifrelenmiş bir Iaas VM'nin Hello şifreleme durumunu Al
Azure Resource Manager kullanarak hello şifreleme durumu alabilirsiniz [PowerShell cmdlet'leri](/powershell/azure/overview), veya CLI komutları. Aşağıdaki bölümlerde hello nasıl toouse hello Klasik Azure portalı ve CLI komutları tooget şifreleme durumu hello açıklanmaktadır.

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a>Azure Resource Manager kullanılarak şifrelenmiş bir Windows VM Hello şifreleme durumunu Al
Merhaba Iaas VM hello şifreleme durumu hello aşağıdakileri yaparak Azure Kaynak Yöneticisi'nden alabilirsiniz:

1. İçinde toohello oturum [Klasik Azure portalı](https://portal.azure.com/)ve ardından **sanal makineleri** hello sol bölmede toosee hello sanal makineleri aboneliğinizde Özet görünümünü de. Hello hello abonelik adını seçerek hello sanal makineleri görünümünü filtreleyebilirsiniz **abonelik** aşağı açılan liste.

2. Merhaba hello üstündeki **sanal makineleri** sayfasında, **sütunları**.

3. Merhaba üzerinde **Seç sütun** dikey penceresinde, select **Disk şifrelemesi**ve ardından **güncelleştirme**. Merhaba disk şifrelemesi sütun gösteren hello şifreleme durumunu görmelisiniz _etkin_ veya _etkin_ hello aşağıdaki şekilde gösterildiği gibi her VM için:

 ![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a>Merhaba disk şifrelemesi PowerShell cmdlet'ini kullanarak bir şifrelenmiş (Windows/Linux) Iaas VM Hello şifreleme durumunu Al
Merhaba disk şifrelemesi PowerShell cmdlet'inden hello Iaas VM hello şifreleme durumu alabilirsiniz `Get-AzureRmVMDiskEncryptionStatus`. tooget hello şifreleme ayarları, VM için hello aşağıdakileri girin:

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

Merhaba çıktısını inceleyebilirsiniz _Get-AzureRmVMDiskEncryptionStatus_ URL'ler için şifreleme anahtarı.

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

Merhaba OSVolumeEncrypted ve DataVolumesEncrypted ayarlarının değerleri her iki birimin Azure Disk şifrelemesi kullanılarak şifrelenmiş olduğunu gösteren too_Encrypted_ ayarlanır. Merhaba blog gönderileri PowerShell cmdlet'lerini kullanarak şifreleme Azure Disk şifrelemesi ile etkinleştirme hakkında daha fazla bilgi için bkz: [keşfedin Azure Disk şifrelemesi Azure PowerShell - bölüm 1 ile](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) ve [Azure Disk şifrelemesi keşfedin Azure PowerShell ile - bölüm 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).

> [!NOTE]
> İsteğe bağlı olarak Linux VM'ler üzerinde hello üç toofour dakika sürer `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello şifreleme durumu.

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a>Hello disk şifrelemesi CLI komuttan hello Iaas VM Hello şifreleme durumunu Al
Merhaba Iaas VM hello şifreleme durumu hello disk şifrelemesi CLI komutunu kullanarak alabileceğiniz `azure vm show-disk-encryption-status`. tooget hello şifreleme ayarları, VM için Azure CLI oturumunuz girin:

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a>Windows Iaas VM çalıştıran üzerinde şifrelemeyi devre dışı
Hello Azure Disk şifrelemesi Resource Manager şablonu veya PowerShell cmdlet'leri üzerinden çalışan bir Windows ya da Linux Iaas VM üzerinde şifrelemeyi devre dışı bırakabilir ve hello şifre çözme yapılandırması belirtin.

##### <a name="windows-vm"></a>Windows VM
Merhaba şifreleme devre dışı bırakma adımı hello işletim sistemi, hello veri birimi ya da hem de Windows Iaas VM çalıştıran hello şifreleme devre dışı bırakır. Merhaba işletim sistemi birimi devre dışı bırakın ve şifrelenmiş hello veri birimi bırakın. Merhaba devre dışı bırak-şifreleme adım gerçekleştirildiğinde, hello Azure Klasik dağıtım modeli hello VM hizmet modeli güncelleştirir ve hello Windows Iaas VM şifresi çözülmüş işaretlenir. Merhaba VM Merhaba içeriğine artık bekleyen şifrelenir. Merhaba şifre çözme, anahtar kasasını ve hello şifreleme anahtar malzemesi (Windows ve Linux için parola için BitLocker şifreleme anahtarları) silmez.

##### <a name="linux-vm"></a>Linux VM
Merhaba şifreleme devre dışı bırakma adımı Linux Iaas VM çalıştıran hello hello veri birimi şifreleme devre dışı bırakır. Bu adım yalnızca Hello işletim sistemi diski şifreli değilse çalışır.

> [!NOTE]
> Merhaba işletim sistemi diski şifreleme devre dışı bırakma Linux VM'ler üzerinde izin verilmiyor.

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Var olan veya çalışan bir Iaas VM üzerinde şifrelemeyi devre dışı bırak
Hello kullanarak Windows Iaas Vm'leri çalıştırma disk şifrelemesi devre dışı bırakabilirsiniz [Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).

1. Hello Azure hızlı başlangıç şablonuna tıklayın **tooAzure dağıtmak**, üzerinde hello hello şifre çözme yapılandırma girin **parametreleri** dikey ve ardından **Tamam**.

2. Merhaba abonelik, kaynak grubu, kaynak grubu konumu, yasal koşulları ve anlaşma seçin ve ardından **oluşturma** yeni bir Iaas VM tooenable şifreleme.

Linux VM'ler için şifreleme hello kullanarak devre dışı bırakabilirsiniz [çalışan bir Linux VM üzerinde şifrelemeyi devre dışı bırakma](https://aka.ms/decrypt-linuxvm) şablonu.

Merhaba aşağıdaki tabloda çalışan bir Iaas VM üzerinde şifrelemeyi devre dışı bırakmak için Resource Manager şablonu parametreleri listelenmektedir:

| Parametre | Açıklama |
| --- | --- |
| vmName | Üzerinde gerçekleştirilen toobe hello şifreleme işlemi hello VM adıdır.
| volumeType | Bir şifre çözme işlemi gerçekleştirilir birim türü. Geçerli değerler _OS_, _veri_, ve _tüm_. Windows Iaas VM OS/önyükleme birimi hello şifreleme devre dışı bırakmadan çalıştırma şifreleme devre dışı bırakamazsınız _veri_ birim. Ayrıca hello işletim sistemi diski şifreleme devre dışı bırakma Linux VM'ler verilmiyor unutmayın. |
| sequenceVersion | Merhaba BitLocker işlemi sürümü dizisi. Merhaba her bir disk şifre çözme işlemi gerçekleştirildiğinde bu sürüm numarasını Artır aynı VM. |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a>Var olan veya çalışan bir Iaas VM üzerinde şifrelemeyi devre dışı bırak
bkz: hello PowerShell cmdlet'ini kullanarak var olan veya çalışan Iaas VM'de toodisable şifreleme [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption). Bu cmdlet, Windows ve Linux VM'ler destekler. toodisable şifreleme, bir uzantı hello sanal makineye yükler. Merhaba, _adı_ parametresi belirtilmezse, hello varsayılan ad olan uzantı _Windows VM'ler için AzureDiskEncryption_ oluşturulur.

Linux VM'ler üzerinde hello AzureDiskEncryptionForLinux uzantısı kullanılır.

> [!NOTE]
> Bu cmdlet hello sanal makine yeniden başlatır.

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a>Azure yönetilen diski ile önceden şifrelenmiş Iaas VM şifrelemeyi etkinleştirin
Merhaba ARM şablonunu kullanarak önceden şifrelenmiş bir VHD şifrelenmiş bir VM'den konumundaki hello Azure yönetilen Disk ARM şablonu toocreate kullanın   
[Yeni bir şifrelenmiş yönetilen disk önceden şifrelenmiş bir VHD/depolama blobundan Oluştur] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a>Azure yönetilen diski olan yeni bir Linux Iaas VM şifrelemeyi etkinleştirin
Yeni bir konumda bulunan hello ARM şablonu kullanarak Linux Iaas VM şifrelenmiş hello Azure yönetilen Disk ARM şablonu toocreate kullanın   
[Tam disk şifrelemesi ile RHEL 7.2 dağıtım] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a>Azure yönetilen diski olan yeni bir Windows Iaas VM şifrelemeyi etkinleştirin
 Yeni bir konumda bulunan hello ARM şablonu kullanarak Linux Iaas VM şifrelenmiş hello Azure yönetilen Disk ARM şablonu toocreate kullanın   
 [Yeni bir şifrelenmiş Windows Iaas yönetilen Disk VM galeri görüntüden oluşturun] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)

  > [!NOTE]
  >Bu zorunlu toosnapshot ve/veya yedekleme yönetilen bir disk dışında VM örneği ve önceki tooenabling Azure Disk şifrelemesi göre.  Merhaba yönetilen diskin anlık görüntüsünü hello portalından alınabilir veya Azure yedekleme kullanılabilir.  Yedeklemeleri kurtarma seçeneğini şifreleme sırasında beklenmeyen bir hata hello durumda mümkün olduğundan emin olun.  Bir yedekleme yapıldıktan sonra hello kümesi AzureRmVMDiskEncryptionExtension cmdlet hello - skipVmBackup parametresini belirterek yönetilen kullanılan tooencrypt diskler olabilir.  Bu komut, yönetilen disk tabanlı VM'in karşı bir yedekleme yaptıysanız ve bu parametre belirtilen kadar başarısız olacak.    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a>Mevcut bir şifrelenmiş premium olmayan VM'yi şifreleme ayarlarını güncelleştir
  VM [PS cmdlet'leri, CLI veya ARM şablonlarını] tooupdate hello şifreleme ayarları çalıştırmak için kullanım hello mevcut Azure disk desteklenen şifreleme arabirimleri AAD istemci kimliği/gizli anahtar şifreleme anahtarı [KEK] BitLocker şifreleme anahtarı Windows VM veya için parolayı ister Linux VM vb. hello güncelleştirme şifreleme ayarını, yalnızca premium olmayan Depolama tarafından yedeklenen VM'ler için desteklenir. Premium Depolama tarafından yedeklenen VM'ler için desteklenen NNOT olur.

## <a name="appendix"></a>Ek
### <a name="connect-tooyour-subscription"></a>Tooyour. abonelik'e bağlanma
Devam etmeden önce hello gözden *Önkoşullar* bu makalenin bölümünde. Tüm önkoşulların karşılandığından emin olduktan sonra tooyour abonelik hello aşağıdakileri yaparak Bağlan:

1. Bir Azure PowerShell oturumu Başlat ve tooyour Azure hesabı komutu aşağıdaki hello ile oturum açın:

    `Login-AzureRmAccount`

2. Birden çok aboneliğiniz varsa ve toospecify bir toouse istediğiniz, hesabınız için toosee hello abonelikleri aşağıdaki hello yazın:

    `Get-AzureRmSubscription`

3. toouse, istediğiniz toospecify hello abonelik türü:

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. yapılandırılmış hello aboneliği doğru olduğunu tooverify, türü:

    `Get-AzureRmSubscription`

5. tooconfirm hello Azure Disk cmdlet'leri yüklenir, şifreleme türü:

    `Get-command *diskencryption*`

6. Çıktı aşağıdaki hello hello Azure Disk şifrelemesi PowerShell yükleme onaylar:

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a>Önceden şifrelenmiş Windows VHD hazırlama
izleyen hello gerekli tooprepare Azure Iaas şifrelenmiş bir VHD olarak dağıtım için önceden şifrelenmiş Windows VHD bölümleridir. Azure Site Recovery veya Azure yeni Windows VM (VHD) önyükleme ve Hello bilgi tooprepare kullanın.

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a>Grup İlkesi tooallow TPM olmayan işletim sistemi koruma için güncelleştirme
Merhaba BitLocker Grup İlkesi ayarını yapılandırma **BitLocker Sürücü Şifrelemesi**, hangi altında bulabilirsiniz **yerel bilgisayar ilkesi** > **Bilgisayar Yapılandırması**  >  **Yönetim Şablonları** > **Windows bileşenleri**. Bu ayar çok değiştirmek**işletim sistemi sürücüleri** > **başlangıçta ek kimlik doğrulamasını gerektiren** > **uyumluTPM'sizBitLockerizinver**hello aşağıdaki şekilde gösterildiği gibi:

![Azure’da Microsoft Kötü Amaçlı Yazılımdan Koruma](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a>BitLocker özelliği bileşenlerini yükle
Windows Server 2012 ve daha sonra komutu aşağıdaki hello kullan:

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

Windows Server 2008 R2 için komutu aşağıdaki hello kullan:

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a>Hello işletim sistemi birimi için BitLocker'ı kullanarak hazırlama`bdehdcfg`
toocompress işletim sistemi bölümü Merhaba ve hello makineyi BitLocker için hazırlama, hello aşağıdaki komutu yürütün:

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a>BitLocker'ı kullanarak Hello işletim sistemi birimi koruma
Kullanım hello [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) komutu tooenable şifreleme dış bir anahtar koruyucusu kullanarak hello önyükleme birimi. Ayrıca hello dış sürücü veya birim üzerinde hello dış anahtar (.bek dosyası) yerleştirin. Şifreleme hello sistem/önyükleme birimini hello sonraki yeniden başlatmanın ardından etkinleştirilir.

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> BitLocker'ı kullanarak hello dış anahtar almak için ayrı bir veri/kaynak VHD ile VM Hello hazırlayın.

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a>Çalışan bir Linux VM işletim sistemi sürücüsünde şifreleme
Çalışan bir Linux VM işletim sistemi sürücüsünde şifrelenmesi dağıtımları aşağıdaki hello üzerinde desteklenir:

* RHEL 7.2
* CentOS 7.2
* Ubuntu 16.04

##### <a name="prerequisites-for-os-disk-encryption"></a>İşletim sistemi disk şifrelemesi önkoşulları

* Azure Kaynak Yöneticisi'nde hello Market görüntüsünden Hello VM yeniden oluşturulması gerekir.
* Azure VM ile en az 4 GB RAM (boyutu 7 GB önerilir).
* (RHEL ve CentOS) SELinux devre dışı bırakın. toodisable SELinux, bkz: "4.4.2. SELinux hello devre dışı bırakma" [SELinux kullanıcının ve Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) hello VM üzerinde.
* Merhaba VM SELinux devre dışı bıraktıktan sonra en az bir kez yeniden başlatın.

##### <a name="steps"></a>Adımlar
1. Daha önce belirtilen hello dağıtımları birini kullanarak bir VM oluşturun.

 CentOS 7.2 için işletim sistemi disk şifrelemesi özel görüntüsü aracılığıyla desteklenir. toouse bu görüntü, "7.2n" Merhaba VM oluşturduğunuzda SKU hello gibi belirtin:
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. Merhaba VM according tooyour gereksinimlerini yapılandırın. Tüm hello (işletim sistemi + veri) sürücüleri tooencrypt kullanacaksanız, hello veri sürücüleri belirtilen ve /etc/fstab gelen edilebilme toobe gerekir.

 > [!NOTE]
 > UUID kullanmak... veri sürücüleri hello blok aygıt adı (örneğin, /dev/sdb1) belirtme yerine/etc/fstab toospecify =. Şifreleme sırasında VM hello üzerinde sürücüleri hello sırasını değiştirir. VM engelleme aygıtları belirli bir sırada dayalıysa, toomount başarısız olur şifreleme sonra bunları.

3. Merhaba SSH oturumları dışında oturum açın.

4. tooencrypt hello işletim sistemi, belirtin volumeType olarak **tüm** veya **OS** olduğunda, [şifrelemeyi etkinleştirmek](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).

 > [!NOTE]
 > Olarak çalışan tüm kullanıcı alanı işlemleri `systemd` Hizmetleri sonlandırıldı ile bir `SIGKILL`. Merhaba VM yeniden başlatın. İşletim sistemi disk şifrelemesi çalışan bir VM üzerinde etkinleştirdiğinizde, VM kapalı kalma süresi üzerinde planlayın.

5. Düzenli aralıklarla hello hello yönergeleri kullanarak şifreleme hello ilerlemesini izlemek [sonraki bölümde](#monitoring-os-encryption-progress).

6. Get-AzureRmVmDiskEncryptionStatus "VMRestartPending" gösterir sonra VM tooit imzalama veya hello portal, PowerShell veya CLI kullanarak yeniden başlatın.
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
Yeniden önce kaydetmeniz önerilir [önyükleme tanılama](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) hello VM.

#### <a name="monitoring-os-encryption-progress"></a>İşletim sistemi şifreleme ilerlemesini izleme
Üç yolla işletim sistemi şifreleme ilerleme durumunu izleyebilirsiniz:

* Kullanım hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet'i ve hello ProgressMessage alan inceleyin:
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 "Şifreleme başlatılan işletim sistemi diski" Merhaba VM ulaştıktan sonra yaklaşık 40 sürdüğünü too50 dakika Premium depolama yedeklenen VM.

 Nedeniyle [sorun #388](https://github.com/Azure/WALinuxAgent/issues/388) WALinuxAgent içinde `OsVolumeEncrypted` ve `DataVolumesEncrypted` olarak görünmesini `Unknown` bazı dağıtımları içinde. WALinuxAgent sürüm 2.1.5 ile ve daha sonra bu sorunu otomatik olarak sabit. Görürseniz `Unknown` hello çıktısında hello Azure kaynak Gezgini'ni kullanarak disk şifrelemesi durumu doğrulayabilirsiniz.

 Çok Git[Azure kaynak Gezgini](https://resources.azure.com/)ve ardından bu hiyerarşide hello Seçim Bölmesi Sol tarafta genişletin:

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 Hello InstanceView, Itanium tabanlı sistemler için toosee hello şifreleme durumu sürücünüz kaydırın.

 ![VM örnek görünümü](./media/azure-security-disk-encryption/vm-instanceview.png)

* Bakmak [önyükleme tanılama](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/). Merhaba ADE uzantısı iletilerden önekiyle `[AzureDiskEncryption]`.

* Toohello VM SSH aracılığıyla imzalamak ve hello uzantısı günlüğü'nden alın:

    /var/log/Azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux

 İşletim sistemi şifreleme işlemi devam ederken toohello VM oturumunuzu değil, öneririz. Yalnızca hello diğer iki yöntemden yanıt vermediğinde hello günlüklerini kopyalayın.

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a>Önceden şifrelenmiş Linux VHD hazırlama
##### <a name="ubuntu-16"></a>Ubuntu 16
Şifreleme hello dağıtım yüklemesi sırasında hello aşağıdakileri yaparak yapılandırın:

1. Seçin **yapılandırma şifrelenmiş birimler** hello diskleri bölümlemek zaman.

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. Şifrelenmemiş olması bir ayrı önyükleme sürücüsü oluşturun. Kök sürücüsünde şifreleyin.

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. Bir parola girin. Merhaba parola toohello anahtar kasası karşıya budur.

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. Bölümleme tamamlayın.

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. Merhaba VM önyükleme için bir parola istendiğinde, adım 3'te sağlanan hello parolası kullanın.

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. Merhaba VM Azure kullanarak yüklemek için hazırlama [bu yönergeleri](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/). Merhaba son adım (sağlamayı hello VM) henüz çalıştırmayın.

Şifreleme toowork hello aşağıdakileri yaparak Azure ile yapılandırın:

1. Komut dosyası izleyen hello hello içerikle /usr/local/sbin/azure_crypt_key.sh altında bir dosya oluşturun. Azure tarafından kullanılan hello parola dosya adı olduğundan dikkat toohello KeyFileName, ücret ödersiniz.

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. Değiştirme hello crypt yapılandırmada */etc/crypttab*. Şu şekilde görünmelidir:
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. Düzenlemekte olduğunuz varsa *azure_crypt_key.sh* Windows ve, tooLinux çalıştırmak, kopyalanan `dos2unix /usr/local/sbin/azure_crypt_key.sh`.

4. Yürütülebilir izinleri toohello komut dosyası ekleyin:
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. Düzen */etc/initramfs-tools/modules* satırları ekleyerek:
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. Çalıştırma `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` etkili.

7. Şimdi hello VM yetkisini kaldırma.

 ![Ubuntu 16.04 Kurulumu](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. Toohello sonraki adıma devam etmek ve [, VHD'yi karşıya](#upload-encrypted-vhd-to-an-azure-storage-account) Azure içine.

##### <a name="opensuse-132"></a>openSUSE 13.2
tooconfigure şifreleme hello dağıtım yüklemesi sırasında hello aşağıdaki:
1. Merhaba diskleri ayırırken seçin **şifrelemek birim grubu**ve ardından bir parola girin. Bu, tooyour anahtar kasası karşıya hello paroladır.

 ![openSUSE 13.2 Kurulumu](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. Önyükleme hello parolanızı kullanarak VM.

 ![openSUSE 13.2 Kurulumu](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. Prepare hello yönergeleri takip ederek tooAzure yüklemek için VM hello [SLES veya openSUSE bir sanal makine için Azure hazırlama](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131). Merhaba son adım (sağlamayı hello VM) henüz çalıştırmayın.

tooconfigure şifreleme toowork, Azure ile Merhaba aşağıdaki:
1. Merhaba /etc/dracut.conf düzenleyin ve hello aşağıdaki satırı ekleyin:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. Açıklama tarafından hello hello sonuna şu satırları /usr/lib/dracut/modules.d/90crypt/module-setup.sh dosya:
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. Satır hello dosya /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello başında aşağıdaki hello ekleyin:
 ```
    DRACUT_SYSTEMD=0
 ```
Ve tüm oluşumlarını değiştirin:
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
yerine şunu yazın:
```
    if [ 1 ]; then
```
4. /Usr/lib/dracut/Modules.d/90crypt/cryptroot-ASK.sh düzenleyin ve çok Ekle "# açık LUKS aygıt":

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. Çalıştırma `/usr/sbin/dracut -f -v` tooupdate hello initrd.

6. VM yetkisini kaldırma artık hello ve [, VHD'yi karşıya](#upload-encrypted-vhd-to-an-azure-storage-account) Azure içine.

##### <a name="centos-7"></a>CentOS 7
tooconfigure şifreleme hello dağıtım yüklemesi sırasında hello aşağıdaki:
1. Seçin **verilerimi şifrelemek** diskleri bölümlemek zaman.

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. Emin olun **şifrele** kök bölüm için seçilir.

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. Bir parola girin. Merhaba parola tooyour anahtar kasası karşıya yükleyecek budur.

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. Merhaba VM önyükleme için bir parola istendiğinde, adım 3'te sağlanan hello parolası kullanın.

 ![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. Azure'da hello "CentOS 7.0 +" konusundaki yönergeleri kullanarak karşıya yükleme için hazırlık hello VM [CentOS tabanlı sanal makine için Azure hazırlama](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70). Merhaba son adım (sağlamayı hello VM) henüz çalıştırmayın.

6. VM yetkisini kaldırma artık hello ve [, VHD'yi karşıya](#upload-encrypted-vhd-to-an-azure-storage-account) Azure içine.

tooconfigure şifreleme toowork, Azure ile Merhaba aşağıdaki:

1. Merhaba /etc/dracut.conf düzenleyin ve hello aşağıdaki satırı ekleyin:
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. Açıklama tarafından hello hello sonuna şu satırları /usr/lib/dracut/modules.d/90crypt/module-setup.sh dosya:
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. Satır hello dosya /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh hello başında aşağıdaki hello ekleyin:
```
    DRACUT_SYSTEMD=0
```
Ve tüm oluşumlarını değiştirin:
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
-
```
    if [ 1 ]; then
```
4. /Usr/lib/dracut/Modules.d/90crypt/cryptroot-ASK.sh düzenleyin ve bu "# açık LUKS aygıt" Merhaba sonra Ekle:
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. Merhaba Çalıştır "/ sbin/usr/dracut - f - v" tooupdate hello initrd.

![CentOS 7 Kurulumu](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a>Şifrelenmiş VHD tooan Azure depolama hesabı karşıya yükle
BitLocker şifrelemesi veya DM-Crypt şifreleme etkinleştirildikten sonra hello yerel VHD gereksinimlerini karşıya toobe tooyour depolama hesabı şifrelenir.

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a>Merhaba disk şifrelemesi gizli hello önceden şifrelenmiş VM tooyour anahtar kasası için karşıya yükleme
elde ettiğiniz hello disk şifrelemesi gizli anahtar kasanızdaki gizli olarak daha önce yüklenmelidir. Merhaba anahtar kasası toohave disk şifrelemesi ve Azure AD istemciniz etkin izinleri gerekir.

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a>Disk şifreleme parolası ile KEK şifrelenmez
anahtar kasanızı, kullanım hello gizliliği yukarı tooset [kümesi AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret). Windows sanal makine varsa, hello bek dosya kodlanmış bir base64 dizesi ve tooyour anahtar kasası hello kullanarak karşıya `Set-AzureKeyVaultSecret` cmdlet'i. Linux için hello parola base64 dizesi olarak kodlanmış ve toohello anahtar kasası karşıya yüklendi. Ayrıca, emin olun etiketleri aşağıdaki o hello ayarlanır hello anahtar kasasına hello gizli oluşturduğunuzda.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

Kullanım hello `$secretUrl` için hello sonraki adımda [KEK kullanmadan bağlanmasını hello işletim sistemi disk](#without-using-a-kek).

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a>KEK ile şifrelenmiş disk şifreleme parolası
Merhaba gizli toohello anahtar kasası karşıya yüklemeden önce bir anahtar şifreleme anahtarı kullanarak isteğe bağlı olarak şifreleyebilirsiniz. Kullanım hello kaydırma [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst şifrelemek hello anahtar şifreleme anahtarı kullanılarak hello gizli anahtarı. Merhaba bu kaydırma işlemi hello kullanarak ardından bir gizlilik olarak yükleyebilirsiniz Base64 ile kodlanmış URL dizesi çıkışıdır [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet'i.

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

Kullanım `$KeyEncryptionKey` ve `$secretUrl` için hello sonraki adımda [KEK kullanarak bağlanmasını hello işletim sistemi diski](#using-a-kek).

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a>İşletim sistemi diski taktığınızda gizli bir URL belirtin
#### <a name="without-using-a-kek"></a>Bir KEK kullanmadan
Merhaba işletim sistemi disk ekleme olsa da, toopass gerek `$secretUrl`. Merhaba URL hello "ile bir KEK şifrelenmez Disk şifrelemesi gizli" bölümünde oluşturuldu.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a>Bir KEK kullanma
Merhaba işletim sistemi disk taktığınızda geçirmek `$KeyEncryptionKey` ve `$secretUrl`. Merhaba URL hello "ile bir KEK şifrelenmez Disk şifrelemesi gizli" bölümünde oluşturuldu.

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a>Bu Kılavuzu'nu indirin
Bu kılavuz hello indirebilirsiniz [TechNet Galerisi](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).

## <a name="for-more-information"></a>Daha fazla bilgi için
[Azure PowerShell - bölüm 1 ile Azure Disk şifrelemesi keşfedin](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)  
[Azure PowerShell - bölüm 2 ile Azure Disk şifrelemesi keşfedin](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
