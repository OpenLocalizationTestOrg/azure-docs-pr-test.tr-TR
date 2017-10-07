---
title: aaaMigrating VM'ler tooAzure Premium depolama | Microsoft Docs
description: "Var olan sanal makineleri tooAzure Premium depolama geçirin. Premium Storage, Azure sanal makinelerde çalışan g/Ç kullanımı yoğun iş yükleri için yüksek performanslı, düşük gecikmeli disk desteği sağlar."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Geçirme tooAzure Premium Storage (yönetilmeyen diskler)

> [!NOTE]
> Bu makalede nasıl toomigrate yönetilmeyen standart diskler tooa kullanan VM kullanan bir VM'yi premium diskleri yönetilmeyen anlatılmaktadır. Azure yönetilen diskleri yeni VM'ler için kullanın ve önceki yönetilmeyen diskleri toomanaged disklerinizi Dönüştür öneririz. Zorunda kalmamak için yönetilen diskleri tanıtıcı hello temel alınan depolama hesapları. Daha fazla bilgi için lütfen bkz bizim [yönetilen diskleri genel bakış](storage-managed-disks-overview.md).
>

Azure Premium depolama g/Ç kullanımı yoğun iş yükleri çalıştıran sanal makineler için yüksek performanslı, düşük gecikmeli disk desteği sunar. Uygulamanızın VM diskleri tooAzure Premium depolama geçirerek avantajı hello hızına ve bu disklerin performansını alabilir.

Bu kılavuzun amacı Hello Azure Premium Storage daha iyi toohelp yeni kullanıcılar, geçerli sistem tooPremium depolama alanından sorunsuz bir geçiş toomake hazırlama ' dir. Merhaba Kılavuzu üç hello anahtar bileşenleri bu süreçte ele alır:

* [Merhaba geçiş tooPremium depolama planlama](#plan-the-migration-to-premium-storage)
* [Hazırlama ve kopyalama sanal sabit diskleri (VHD) tooPremium depolama](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Premium depolama kullanarak Azure sanal makine oluşturun](#create-azure-virtual-machine-using-premium-storage)

Diğer platformlar tooAzure Premium depolama Vm'leri geçirme veya var olan Azure Vm'leri standart depolama tooPremium depolama geçirme. Bu kılavuz, her iki iki senaryo adımları kapsar. Senaryonuza bağlı olarak ilgili hello bölümünde belirtilen hello adımları izleyin.

> [!NOTE]
> Özelliklere genel bakış ve Premium depolama, Premium Storage fiyatlandırma bulabilirsiniz: [Azure sanal makine iş yükleri için yüksek performanslı depolama](storage-premium-storage.md). Merhaba, uygulamanız için en iyi performans için yüksek IOPS tooAzure Premium depolama gerektiren herhangi bir sanal makine disk geçirme öneririz. Diskinizin yüksek IOPS gerektirmiyorsa SSD yerine Sabit Disk sürücülerinin (HDD'ler) üzerinde sanal makine disk verilerini depolayan standart depolama tutarak maliyetleri sınırlayabilirsiniz.
>

Okumalıdır Hello geçiş işlemini tamamlama öncesinde ve sonrasında bu kılavuzda sağlanan hello adımları ek eylemler gerekebilir. Sanal ağlar veya uç noktaların yapılandırma veya uygulamadaki miktar kapalı kalma süresi, uygulamanızda gerektirebilecek hello kendisini kodda değişiklikler yaparak örnek olarak verilebilir. Bu eylemler benzersiz tooeach uygulama olan ve bu kılavuzu toomake hello tam geçiş tooPremium depolama olarak sorunsuz sağlanan hello adımlarını tamamlanmalıdır.

## <a name="plan-the-migration-to-premium-storage"></a>Merhaba geçiş tooPremium depolama planlama
Bu bölümde, hazır toofollow hello geçiş bu makalede adımlardır ve toomake hello en iyi karar VM ve Disk türleri hakkında yardımcı sağlar.

### <a name="prerequisites"></a>Ön koşullar
* Bir Azure aboneliği gerekir. Yoksa, bir aylık oluşturabilirsiniz [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/) abonelik veya ziyaret [Azure fiyatlandırma](https://azure.microsoft.com/pricing/) daha fazla seçenek için.
* tooexecute PowerShell cmdlet'leri, hello Microsoft Azure PowerShell modülü gerekir. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) noktası ve yükleme yönergeleri için hello yükleyin.
* Toouse Azure Premium depolama üzerinde çalışan Vm'leri planlarken, toouse hello özellikli Premium Storage Vm'lerini gerekir. Premium depolama yeteneğine sahip sanal makineleri ile standart ve Premium depolama diskleri kullanabilirsiniz. Premium depolama diskleri hello gelecekte daha fazla VM türleri ile kullanılabilir. Tüm kullanılabilir Azure VM disk türleri ve boyutları hakkında daha fazla bilgi için bkz: [sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ve [Cloud Services boyutları](../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Dikkat edilmesi gerekenler
Bir Azure VM uygulamalarınızı too256 TB depolama alanı VM başına yukarı böylece birkaç Premium depolama diskleri ekleme destekler. Premium depolama ile uygulamalarınızı, ikinci disk işleme VM başına okuma işlemleri için son derece düşük gecikme ile başına VM ve 2000 MB başına 80.000 IOPS (saniye başına girdi/çıktı işlemleri) elde edebilirsiniz. VM'ler ve diskleri çeşitli seçeneğiniz vardır. Bu bölümde toohelp olan İş yükünüzün uygun bir seçeneği toofind.

#### <a name="vm-sizes"></a>VM boyutları
Hello Azure VM boyutu belirtimleri içinde listelenen [sanal makineler için Boyutlar](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Premium Storage ile birlikte çalışmak ve işleminizi iş yükü en çok uyan hello en uygun VM boyutunu seçin sanal makineleri Hello performans özellikleri gözden geçirin. Yeterli bant genişliği kullanılabilir VM toodrive hello disk trafiğinde bulunduğundan emin olun.

#### <a name="disk-sizes"></a>Disk boyutları
VM ile kullanılan diskler beş tür vardır ve her belirli IOPS ve üretilen iş sahip sınırlar. Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın hello gereksinimlerine hello disk türü, VM için seçme temel yaparken dikkate.

| Premium diskler türü  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Disk boyutu           | 128 GB| 512 GB| 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| Disk başına IOPS       | 500   | 2300  | 5000           | 7500           | 7500           | 
| Disk başına aktarım hızı | Saniyede 100 MB | 150 MB / saniye | 200 MB / saniye | Saniye başına 250 MB | Saniye başına 250 MB |

İş yükünüz bağlı olarak, ek veri disklerinin VM için gerekli olup olmadığını belirleyin. Birkaç kalıcı veri diskleri tooyour VM ekleyebilirsiniz. Gerekirse, hello diskleri tooincrease hello kapasite ve performans hello birimin arasında şeritler. (Disk şeritleme görmek [burada](storage-premium-storage-performance.md#disk-striping).) Premium depolama veri diskleri kullanarak şeritler varsa [depolama alanları][4], kullanılan her disk için bir sütun ile yapılandırmanız gerekir. Aksi takdirde, hello genel hello şeritli birim performansını trafiği toouneven dağıtım hello disklerde beklenenden daha düşük olabilir. Linux VM'ler için hello kullanabilirsiniz *mdadm* yardımcı programı tooachieve hello aynı. Makalesine bakın [yapılandırma yazılım RAID Linux'ta](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Ayrıntılar için.

#### <a name="storage-account-scalability-targets"></a>Depolama hesabımın ölçeklenebilirlik hedefleri
Premium depolama hesapları ekleme toohello ölçeklenebilirlik hedeflerini izleyerek hello sahip [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md). Uygulamanızın gereksinimleri tek bir depolama hesabına hello ölçeklenebilirlik hedefleri aşarsa, uygulama toouse birden çok depolama hesabı oluşturun ve bu depolama hesaplarında verilerinizi bölüm.

| Toplam hesabı kapasitesi | Yerel olarak yedekli depolama hesabı için toplam bant genişliği |
|:--- |:--- |
| Disk kapasitesi: 35TB<br />Kapasite anlık görüntü: 10 TB |Gelen + giden için saniye başına too50 Gigabit |

Merhaba Premium depolama özellikleri hakkında daha fazla bilgi için kullanıma [ölçeklenebilirlik ve performans Premium depolama kullanırken hedefleri](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Önbellek İlkesi disk
Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium diskleri hello için ve *okuma-yazma* hello Premium işletim sistemi diski için toohello VM bağlı. Bu yapılandırma ayarının tooachieve hello en iyi performans için uygulamanızın IOs önerilir. (SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın. mevcut veri diskleri için Hello önbellek ayarlarını kullanarak güncelleştirilebilir [Azure Portal](https://portal.azure.com) veya hello *- HostCaching* hello parametresinin *kümesi AzureDataDisk* cmdlet'i.

#### <a name="location"></a>Konum
Azure Premium Storage kullanılabilir olduğu bir konum seçin. Bkz: [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi. Sanal makineleri bulunan hello aynı depolama hesabı hello VM ayrı bölge içinde olup olmadığını daha çok daha iyi performans sağlayacaktır için depoları diskleri hello hello gibi bölge.

#### <a name="other-azure-vm-configuration-settings"></a>Diğer Azure VM yapılandırma ayarları
Bir Azure VM oluşturulurken olacaktır belirli VM ayarları tooconfigure istedi. Değiştirme veya başkalarının daha sonra ekleme sırasında birkaç ayarlar hello VM hello ömrü boyunca sabit unutmayın. Bu Azure VM yapılandırma ayarlarını gözden geçirin ve bu olduğundan emin olun toomatch, iş yükü gereksinimlerinize uygun şekilde yapılandırılmış.

### <a name="optimization"></a>İyileştirme
[Azure Premium Storage: Tasarım için yüksek performanslı](storage-premium-storage-performance.md) Azure Premium Storage kullanarak yüksek performanslı uygulamalar oluşturmak için yönergeler sağlar. Uygulamanız tarafından kullanılan performansı en iyi uygulamalar uygulanabilir tootechnologies birlikte hello yönergeleri takip edebilirsiniz.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Hazırlama ve sanal sabit diskleri (VHD) tooPremium depolama kopyalayın
bölümden hello VHD'ler, sanal makineden hazırlama ve VHD tooAzure depolama kopyalama için yönergeler sağlar.

* [Senaryo 1: "ı mevcut Azure VM'ler tooAzure Premium depolama geçirme."](#scenario1)
* [Senaryo 2: "ı VM'ler diğer platformlar tooAzure Premium depolama geçirme."](#scenario2)

### <a name="prerequisites"></a>Ön koşullar
tooprepare hello VHD'ler geçiş için ihtiyacınız vardır:

* Bir Azure aboneliği, bir depolama hesabı ve kapsayıcı, depolama, VHD kopyalayabilirsiniz toowhich hesap. Merhaba hedef depolama hesabının bir standart veya Premium depolama hesabı ihtiyacınıza olabileceğini unutmayın.
* Bir aracı toogeneralize hello dışarı birden çok VM örnekleri toocreate düşünüyorsanız, VHD. Örneğin, sysprep Windows ya da Sanal Küp Str sysprep Ubuntu için.
* Bir aracı tooupload hello VHD dosyası toohello depolama hesabı. Bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md) veya bir [Azure storage Gezgini](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Bu kılavuzda hello AzCopy aracını kullanarak, VHD kopyalama açıklanmaktadır.

> [!NOTE]
> AzCopy, en iyi performans için zaman uyumlu kopyası seçeneğiyle seçerseniz, VHD'yi Bu araçlardan birini hello olan bir Azure VM çalıştırarak kopyalayın hello hedef depolama hesabının aynı bölgede. Bir VHD farklı bir bölgede bir Azure VM kopyalıyorsanız performansınızı daha yavaş olabilir.
>
> Sınırlı bant genişliği üzerinde büyük miktarda veri kopyalama için göz önünde bulundurun [hello Azure içeri/dışarı aktarma hizmeti tootransfer veri tooBlob depolama kullanarak](storage-import-export-service.md); tootransfer bu sayede verilerinizi sevkiyat sabit disk tarafından tooan Azure sürücüler Veri Merkezi. Hello Azure içeri/dışarı aktarma hizmeti toocopy veri tooa standart depolama hesabı yalnızca kullanabilirsiniz. Standart depolama hesabınızdaki Hello veri olduktan sonra her iki hello kullanabilirsiniz [kopyalama Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) veya AzCopy tootransfer hello veri tooyour premium depolama hesabı.
>
> Microsoft Azure yalnızca sabit boyutlu VHD dosyalarını desteklediğini unutmayın. VHDX dosyaları veya dinamik VHD desteklenmez. Dinamik VHD varsa, hello kullanarak toofixed boyutunu dönüştürebilirsiniz [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet'i.
>
>

### <a name="scenario1"></a>Senaryo 1: "ı mevcut Azure VM'ler tooAzure Premium depolama geçirme."
Azure VM'ler, Dur hello VM, varolan geçiriyorsanız istediğiniz VHD hello türü başına VHD'ler hazırlamak ve hello VHD AzCopy veya PowerShell ile kopyalayın.

Merhaba VM tamamen toomigrate temiz bir duruma aşağı toobe gerekir. Merhaba Geçiş tamamlanana kadar bir kapalı kalma süresi olacaktır.

#### <a name="step-1-prepare-vhds-for-migration"></a>1. Adım VHD'ler geçiş için hazırlama
Var olan Azure Vm'leri tooPremium depolama geçiriyorsanız, VHD olabilir:

* Genelleştirilmiş işletim sistemi görüntüsü
* Benzersiz işletim sistemi diski
* Bir veri diski

Aşağıda Biz bu 3 senaryolar için VHD hazırlama yol.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Birden çok VM örnekleri genelleştirilmiş bir işletim sistemi VHD toocreate kullanın
Birden çok genel Azure VM örnekleri kullanılan toocreate olacak VHD yüklüyorsanız, sysprep yardımcı programını kullanarak VHD generalize gerekir. Bu tooa şirket içi VHD uygulanır veya hello bulutta. Sysprep VHD hello tüm makine özgü bilgileri kaldırır.

> [!IMPORTANT]
> Bir anlık görüntüsünü veya genelleme önce VM'yi yedekleme. Çalışan sysprep durdurun ve hello VM örneğine serbest bırakma. Windows işletim sistemi VHD toosysprep adımları izleyin. Hello Sysprep komutunu çalıştırarak tooshut hello sanal makine kapalı gerektirir olduğunu unutmayın. Sysprep hakkında daha fazla bilgi için bkz: [Sysprep genel bakış](http://technet.microsoft.com/library/hh825209.aspx) veya [Sysprep Teknik Başvurusu](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Yönetici olarak bir komut istemi penceresi açın.
2. Komut tooopen Sysprep aşağıdaki hello girin:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Hello Sistem Hazırlama aracı, select girin sistem Out-of-Box deneyimi (OOBE) select hello Generalize onay kutusunu seçin **kapatma**ve ardından **Tamam**hello resimde gösterildiği gibi. Sysprep hello işletim sistemini genelleştirir ve hello Sistemi kapat.

    ![][1]

Bir Ubuntu VM için kullanım Sanal Küp Str sysprep tooachieve hello aynı. Bkz: [Sanal Küp Str sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) daha fazla ayrıntı için. Ayrıca bazı hello açık kaynak bkz [sunucu Linux sağlama yazılım](http://www.cyberciti.biz/tips/server-provisioning-software.html) diğer Linux işletim sistemleri için.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Benzersiz bir işletim sistemi VHD toocreate tek bir VM örneği kullanın
Merhaba hello makine belirli veri gerektiren VM üzerinde çalışan bir uygulamanız varsa, hello VHD generalize değil. Genelleştirilmiş olmayan bir VHD kullanılan toocreate benzersiz bir Azure VM örneği olabilir. VHD etki alanı denetleyicisi varsa, örneğin, sysprep yürütülürken, bir etki alanı denetleyicisi olarak etkisiz hale getirir. Sysprep hello VHD genelleme önce bunlar üzerinde çalışan VM ve hello etkisi çalışan hello uygulamaları gözden geçirin.

##### <a name="register-data-disk-vhd"></a>Veri diski VHD kaydetme
Varsa Azure toobe'ndeki veri disklerinin geçişi, diskleri kapatma bu verileri kullanmak emin hello VM'ler yapmanız gerekir.

Premium depolama toocopy VHD tooAzure açıklanan başlangıç adımları izleyin ve sağlanan veri diski olarak kaydedin.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>2. Adım Merhaba hedef, VHD için oluşturma
Vhd'lerinizi korumak için bir depolama hesabı oluşturun. Merhaba where planlarken aşağıdaki noktaları göz önünde bulundurun toostore Vhd'lerinizi:

* Merhaba hedef Premium depolama hesabı.
* Merhaba depolama hesap konumu Premium depolama özellikli Azure hello Son aşamada oluşturacak VM'ler ile aynı olması gerekir. Tooa yeni depolama hesabı ya da aynı depolama hesabındaki gereksinimlerinize göre plan toouse hello kopyalamak.
* Kopyalayın ve hello depolama hesabı anahtarı hello hedef depolama hesabının hello sonraki aşaması için kaydedin.

Veri diskleri için bir standart depolama hesabı (örneğin, için depolama alanına sahip diskler) bazı veri diskleri tookeep seçebilirsiniz, ancak, üretim iş yükü toouse premium depolama için tüm verilerin taşınması önerilir.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>3. adım. VHD AzCopy veya PowerShell ile kopyalama
Kapsayıcı yolu ve bu iki seçenekten biri anahtar tooprocess hesap depolama toofind gerekir. Kapsayıcı yolu ve depolama hesabı anahtarı bulunabilir **Azure Portal** > **depolama**. Merhaba kapsayıcı URL "gibi https://myaccount.blob.core.windows.net/mycontainer/" olacaktır.

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Seçenek 1: bir VHD AzCopy (zaman uyumsuz kopya) ile kopyalama
AzCopy kullanarak hello VHD hello Internet üzerinden kolayca karşıya yükleyebilir. Merhaba VHD'ler Hello boyutuna bağlı olarak, bu zaman alabilir. Bu seçenek kullanıldığında toocheck hello depolama hesabı giriş/çıkış sınırları unutmayın. Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) Ayrıntılar için.

1. AzCopy buradan yükleyip: [en güncel AzCopy sürümünü](http://aka.ms/downloadazcopy)
2. Azure PowerShell ve AzCopy yüklendiği gidin toohello klasörünü açın.
3. Kullanım hello şu komutu toocopy hello VHD "Kaynak" dosyasından çok "Hedef".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Örnek:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Açıklamaları hello AzCopy komut kullanılan hello Parametreler şunlardır:

   * **/ Kaynak:  *&lt;kaynak&gt;:***  hello klasör veya hello VHD'yi içeren depolama kapsayıcısı URL konumu.
   * **/ SourceKey:  *&lt;kaynak hesap anahtarı&gt;:***  hello kaynak depolama hesabının depolama hesabı anahtarı.
   * **/ Taşınmaya:  *&lt;hedef&gt;:***  depolama kapsayıcısı URL toocopy hello VHD'ye.
   * **/ DestKey:  *&lt;hedef hesap anahtarı&gt;:***  hello hedef depolama hesabının depolama hesabı anahtarı.
   * **/ Deseni:  *&lt;dosya adı&gt;:***  hello VHD toocopy hello dosya adı belirtin.

Aracı AzCopy kullanımıyla ilgili ayrıntılar için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Seçenek 2: bir VHD PowerShell (Synchronızed kopya) ile kopyalama
Ayrıca, başlangıç AzureStorageBlobCopy hello PowerShell cmdlet'ini kullanarak hello VHD dosyasını kopyalayabilirsiniz. Azure PowerShell toocopy VHD komutu aşağıdaki hello kullanın. Kaynak ve hedef depolama hesabınız karşılık gelen değerlerle <> Hello değerleri değiştirin. toouse bu komut, hedef depolama hesabınız VHD adlı bir kapsayıcıya sahip olmalıdır. Merhaba kapsayıcı yoksa, hello komutu çalıştırmadan önce oluşturun.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Örnek:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Senaryo 2: "ı VM'ler diğer platformlar tooAzure Premium depolama geçirme."
Azure bulut depolama tooAzure VHD geçiriyorsanız, hello VHD tooa yerel dizin dışarı aktarmanız gerekir. VHD depolandığı kullanışlı hello yerel dizin Hello tam kaynak yolu varsa ve AzCopy tooupload kullanarak onu tooAzure depolama.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>1. Adım VHD tooa yerel dizin dışarı aktarma
##### <a name="copy-a-vhd-from-aws"></a>Bir VHD'yi AWS kopyalayın
1. AWS kullanıyorsanız, hello EC2 örneği tooa bir Amazon S3 demetini VHD'yi verin. Hello dışarı aktarma Amazon EC2 örnekleri tooinstall hello Amazon EC2 komut satırı arabirimi (CLI) aracı Amazon belgelerine açıklanan başlangıç adımları izleyin ve hello-örnek-export-Görev Oluştur komutu tooexport hello EC2 örneği tooa VHD dosyasını çalıştırın. Emin toouse olması **VHD** hello DISK &#95; görüntü &#95; Merhaba çalıştırırken biçimi değişkeni **-örnek-export-görev oluştur** komutu. Merhaba dışarı aktarılan VHD dosyasının bu işlem sırasında belirttiğiniz hello Amazon S3 demetini kaydedilir.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Merhaba S3 demetini Hello VHD dosyasını indirin. Select hello VHD dosyasını, ardından **Eylemler** > **karşıdan**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Bir VHD'yi diğer Azure olmayan buluttan kopyalayın
Azure bulut depolama tooAzure VHD geçiriyorsanız, hello VHD tooa yerel dizin dışarı aktarmanız gerekir. Hello tam kaynak yolu VHD depolandığı hello yerel dizine kopyalayın.

##### <a name="copy-a-vhd-from-on-premises"></a>Şirket içi bir VHD'yi kopyalayın
Bir şirket içi ortamından VHD geçiriyorsanız, VHD depolandığı hello tam kaynak yolu gerekir. Merhaba kaynak yolu, bir sunucu konumu veya dosya paylaşımı olabilir.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>2. Adım Merhaba hedef, VHD için oluşturma
Vhd'lerinizi korumak için bir depolama hesabı oluşturun. Merhaba where planlarken aşağıdaki noktaları göz önünde bulundurun toostore Vhd'lerinizi:

* Merhaba hedef depolama hesabı, standart veya premium depolama uygulama ihtiyacınıza olabilir.
* Merhaba depolama hesabı bölgesi Premium depolama özellikli Azure hello Son aşamada oluşturacak VM'ler ile aynı olması gerekir. Tooa yeni depolama hesabı ya da aynı depolama hesabındaki gereksinimlerinize göre plan toouse hello kopyalamak.
* Kopyalayın ve hello depolama hesabı anahtarı hello hedef depolama hesabının hello sonraki aşaması için kaydedin.

Üretim iş yükü toouse premium depolama için tüm veriler hareket öneririz.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>3. Adım Merhaba VHD tooAzure depolama karşıya yükle
VHD hello yerel bir dizine sahip olduğunuza göre AzCopy veya AzurePowerShell tooupload hello .vhd dosyası tooAzure depolama kullanabilirsiniz. Her iki seçenek aşağıda verilmiştir:

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Seçenek 1: Azure PowerShell Ekle-AzureVhd tooupload hello .vhd dosyası kullanma

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Örnek <Uri> olabilir ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***. Örnek <FileInfo> olabilir ***"C:\path\to\upload.vhd"***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Seçenek 2: AzCopy tooupload hello .vhd dosyası kullanma
AzCopy kullanarak hello VHD hello Internet üzerinden kolayca karşıya yükleyebilir. Merhaba VHD'ler Hello boyutuna bağlı olarak, bu zaman alabilir. Bu seçenek kullanıldığında toocheck hello depolama hesabı giriş/çıkış sınırları unutmayın. Bkz: [Azure Storage ölçeklenebilirlik ve performans hedefleri](storage-scalability-targets.md) Ayrıntılar için.

1. AzCopy buradan yükleyip: [en güncel AzCopy sürümünü](http://aka.ms/downloadazcopy)
2. Azure PowerShell ve AzCopy yüklendiği gidin toohello klasörünü açın.
3. Kullanım hello şu komutu toocopy hello VHD "Kaynak" dosyasından çok "Hedef".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Örnek:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Açıklamaları hello AzCopy komut kullanılan hello Parametreler şunlardır:

   * **/ Kaynak:  *&lt;kaynak&gt;:***  hello klasör veya hello VHD'yi içeren depolama kapsayıcısı URL konumu.
   * **/ SourceKey:  *&lt;kaynak hesap anahtarı&gt;:***  hello kaynak depolama hesabının depolama hesabı anahtarı.
   * **/ Taşınmaya:  *&lt;hedef&gt;:***  depolama kapsayıcısı URL toocopy hello VHD'ye.
   * **/ DestKey:  *&lt;hedef hesap anahtarı&gt;:***  hello hedef depolama hesabının depolama hesabı anahtarı.
   * **/ BlobType: sayfa:** bu hello hedef bir sayfa blob'u olduğunu belirtir.
   * **/ Deseni:  *&lt;dosya adı&gt;:***  hello VHD toocopy hello dosya adı belirtin.

Aracı AzCopy kullanımıyla ilgili ayrıntılar için bkz: [hello AzCopy komut satırı yardımcı programı ile veri aktarma](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Bir VHD karşıya yükleme için diğer seçenekleri
Yol aşağıdaki hello birini kullanarak bir VHD'yi tooyour depolama hesabı da yükleyebilirsiniz:

* [Azure depolama kopyalama Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Azure Depolama Gezgini karşıya BLOB'ları](https://azurestorageexplorer.codeplex.com/)
* [Depolama içeri/dışarı aktarma hizmeti REST API Başvurusu](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> İçeri/dışarı aktarma hizmeti 7 günden daha uzun süre karşıya tahmini varsa kullanmanızı öneririz. Kullanabileceğiniz [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) veri boyutu ve aktarım birimi tooestimate başlangıç saati.
>
> İçeri/dışarı aktarma olabilir toocopy tooa standart depolama hesabı kullanılır. AzCopy gibi bir araç kullanarak standart depolama toopremium depolama hesabından toocopy gerekir.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Azure Premium Storage kullanarak VM'ler oluşturma
Karşıya yüklenen ya da kopyalanmış toohello istenen depolama hesabı Hello VHD olduktan sonra bir işletim sistemi görüntüsü veya işletim sistemi diski senaryonuza bağlı olarak bu bölüm tooregister hello VHD hello yönergeleri izleyin ve ardından VM örneği ondan oluşturun. bir kez oluşturulduğunda hello veri diski ekli toohello VM VHD olabilir.
Örnek geçiş dosyası hello bu bölümün sonunda sağlanır. Bu basit bir komut dosyası tüm senaryoları eşleşmiyor. Belirli senaryonuza tooupdate hello betik toomatch gerekebilir. Bu komut dosyası tooyour senaryo geçerliyse toosee bkz aşağıda [bir örnek geçiş komut dosyası](#a-sample-migration-script).

### <a name="checklist"></a>Denetim listesi
1. Tüm hello VHD diskleri kopyalama beklemeniz tamamlanır.
2. Premium depolama, için geçirdiğiniz hello bölgede kullanılabilir olduğundan emin olun.
3. Merhaba, kullanarak yeni VM dizisi karar verin. Premium depolama özelliğine sahip olmalıdır ve başlangıç boyutu hello bölgede hello kullanılabilirliğine bağlı olarak ve gereksinimlerinize göre olmalıdır.
4. Kullanacağınız hello tam VM boyutu karar verin. VM boyutu toobe büyüklükte toosupport hello sahip veri diski sayısı gerekir. Örneğin 4 veri diski varsa, hello VM 2 veya daha fazla çekirdek olması gerekir. Ayrıca, işlemci gücü, bellek göz önünde bulundurun ve ağ bant genişliği gerekiyor.
5. Premium depolama hesabı hello hedef bölgede oluşturun. Bu hello için kullanacağınız hello hesabıdır yeni VM.
6. Merhaba geçerli VM ayrıntıları hello disklerin listesini ve karşılık gelen VHD BLOB'ları da dahil olmak üzere kullanışlı vardır.

Uygulamanızı kapalı kalma süresi için hazırlayın. toodo temiz bir geçiş, toostop hello geçerli sistemi tüm hello işleme sahip. Ancak bundan sonra geçirebileceğiniz tooconsistent durumu alabilirsiniz toohello yeni platformu. Kapalı kalma süresi hello hello diskleri toomigrate veri miktarına bağlıdır.

> [!NOTE]
> Lütfen özel bir VHD diskten bir Azure Kaynak Yöneticisi'ni VM oluşturuyorsanız, çok başvurun[bu şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) Resource Manager mevcut diski kullanarak VM dağıtmak için.
>
>

### <a name="register-your-vhd"></a>VHD kaydetme
işletim sistemi VHD veya tooattach bir veri diski tooa VM'den toocreate yeni VM, ilk kaydetmeniz gerekir bunları. VHD'ler senaryo bağlı olarak aşağıdaki adımları izleyin.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>İşletim sistemi VHD toocreate birden çok Azure VM örnekleri genelleştirilmiş
VHD'nin olduğundan genelleştirilmiş işletim sistemi görüntüsü toohello depolama hesabı karşıya sonra olarak kaydetmek bir **Azure VM görüntüsü** böylece bir veya daha fazla VM örnekleri oluşturabilirsiniz. PowerShell cmdlet'leri tooregister aşağıdaki Merhaba, VHD bir Azure VM işletim sistemi görüntüsü olarak kullanın. VHD için burada kopyalanmıştır hello tam kapsayıcı URL'sini belirtin.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Kopyalayın ve bu yeni Azure VM görüntüsü hello adını kaydedin. Yukarıdaki Hello örnek içinde *OSImageName*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Benzersiz işletim sistemi VHD toocreate tek bir Azure VM örneği
Hello sonra benzersiz OS VHD karşıya yüklenen toohello depolama olduğu hesap, olarak kaydeder bir **Azure işletim sistemi diski** böylece VM örneği oluşturabilirsiniz. Bu PowerShell cmdlet'leri tooregister, VHD Azure işletim sistemi diski kullanın. VHD için burada kopyalanmıştır hello tam kapsayıcı URL'sini belirtin.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Kopyalayın ve bu yeni Azure işletim sistemi diski hello adını kaydedin. Yukarıdaki Hello örnek içinde *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Veri diski VHD toobe toonew Azure VM örnekleri bağlı
Merhaba veri disk VHD karşıya toostorage hesabı sonra ekli tooyour olması için bir Azure veri diski olarak kaydetmek yeni DS serisi, DSv2 serisi veya GS serisi Azure VM örneği.

Bu PowerShell cmdlet'leri tooregister, VHD bir Azure veri diski kullanın. VHD için burada kopyalanmıştır hello tam kapsayıcı URL'sini belirtin.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Kopyalayın ve bu yeni Azure veri diski hello adını kaydedin. Yukarıdaki Hello örnek içinde *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Premium depolama özelliğine sahip VM oluşturma
İşletim sistemi görüntüsü kez hello veya işletim sistemi diski kayıtlı, yeni DS serisi, DSv2 serisi veya GS serisi VM oluşturun. Merhaba işletim sistemi görüntüsü veya kaydettiğiniz işletim sistemi disk adı kullanacaksınız. Merhaba VM türü hello Premium depolama katmanını seçin. Aşağıdaki örnekte hello kullanıyoruz *Standard_DS2* VM boyutu.

> [!NOTE]
> Merhaba disk boyutu toomake kapasite ve performans gereksinimlerini ve hello kullanılabilir Azure disk boyutlarını eşleştiğinden emin güncelleştirin.
>
>

İzleme hello adım adım PowerShell cmdlet'leri toocreate altındaki Yeni VM hello. İlk olarak, hello ortak parametreleri ayarlayın:

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

İlk olarak, yeni VM'ler içinde barındıracak bir bulut hizmeti oluşturun.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

Ardından, senaryonuza bağlı olarak ya da hello işletim sistemi görüntüsü veya işletim sistemi diski, kaydettiğiniz hello Azure VM örneği oluşturun.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>İşletim sistemi VHD toocreate birden çok Azure VM örnekleri genelleştirilmiş
Merhaba hello kullanarak bir veya daha fazla yeni DS serisi Azure VM örnekleri oluşturmak **Azure işletim sistemi görüntüsü** , kayıtlı. Bu işletim sistemi görüntüsü adı, aşağıda gösterildiği gibi yeni VM oluşturulurken hello VM yapılandırması belirtin.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Benzersiz işletim sistemi VHD toocreate tek bir Azure VM örneği
Hello kullanarak yeni DS serisi Azure VM örneği oluşturma **Azure işletim sistemi diski** , kayıtlı. Oluşturma Merhaba, yeni VM aşağıda gösterildiği gibi hello VM yapılandırması bu işletim sistemi Disk adı belirtin.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Bulut hizmeti, bölge, depolama hesabı, kullanılabilirlik kümesi ve önbellek İlkesi gibi diğer Azure VM bilgileri belirtin. Merhaba VM örneği ilişkili işletim sistemiyle birlikte bulunan veya seçili hello bulut hizmeti, bölge ve depolama hesabı tüm olması gerekir böylece veri diskleri, bu disklerin VHD'ler temel hello aynı konumda hello unutmayın.

### <a name="attach-data-disk"></a>Veri diski ekleme
Son olarak, kayıtlı durumunda veri VHD'ler disk, toohello ekleme yeni Premium depolama özellikli Azure VM.

PowerShell cmdlet'ini tooattach veri diski toohello kullanmak yeni VM ve ilke önbelleğe alma hello belirtin. Merhaba aşağıdaki örnekte ilke önbelleğe alma çok kümesindeki*salt okunur*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Ek adımlar gerekli toosupport olabilir, uygulama değil Bu kılavuz kapsamında.
>
>

### <a name="checking-and-plan-backup"></a>Denetleme ve yedekleme planlama
Bir kez yeni VM çalışıyor hello ve çalışan, aynı oturum açma kimliği ve parola kullanarak hello erişim özgün VM hello aynıdır ve her şeyin beklendiği gibi çalıştığını doğrulayın. Merhaba şeritli birimler dahil tüm hello ayarları de mevcut olacaktır yeni VM hello.

Merhaba son adımı tooplan yedekleme ve bakım zamanlaması yeni VM hello uygulamanın gereksinimlerine göre hello için değildir.

### <a name="a-sample-migration-script"></a>Örnek geçiş komut dosyası
Birden çok sanal makineleri toomigrate varsa, automation PowerShell komut yardımcı olacaktır. Bir VM hello geçişini otomatikleştiren bir örnek betiği aşağıdadır. Not, aşağıdaki komut dosyası yalnızca bir örnektir ve hello geçerli VM diskleri hakkında yapılan birkaç varsayımlar vardır. Belirli senaryonuza tooupdate hello betik toomatch gerekebilir.

Merhaba varsayımlar şunlardır:

* Klasik Azure sanal makineleri oluşturuyorsunuz.
* Kaynak işletim sistemi diski ve kaynak veri diskleri aynı depolama hesabı ve aynı kapsayıcı olan. İşletim sistemi diskleri ve veri diskleri içinde değilse aynı hello yerleştirin, AzCopy ya da Azure PowerShell toocopy VHD'ler depolama hesapları ve kapsayıcıları üzerinden kullanabilirsiniz. Toohello önceki adıma bakın: [kopyalama VHD AzCopy veya PowerShell ile](#copy-vhd-with-azcopy-or-powershell). Bu komut dosyası toomeet düzenleme senaryonuz başka bir seçenektir ancak daha kolay ve hızlı olduğundan AzCopy veya PowerShell kullanmanızı öneririz.

Merhaba Otomasyon betiğini aşağıda verilmiştir. Metin bilgilerinizle değiştirin ve belirli senaryonuza hello betik toomatch güncelleştirin.

> [!NOTE]
> Merhaba varolan komut dosyasını kullanarak hello ağ yapılandırması kaynağınızın VM korumaz. Geçirilen Vm'leriniz toore-config hello ağ ayarları gerekir.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>En iyi duruma getirme
Geçerli VM yapılandırmanızı özelleştirilebilir özellikle toowork standart diskler ile iyi. Şeritli birim içinde birçok diskleri kullanarak örneği için tooincrease hello performans. Örneğin, 4 disk ayrı olarak Premium depolama kullanmak yerine, mümkün toooptimize hello maliyet tek bir disk sağlayarak olabilir. En iyi duruma getirme, bir olay temelinde işlenen bu gereksinimi toobe ister ve hello geçişten sonra özel adımlar gerektirir. Ayrıca, bu işlem veritabanları ve hello Ayarları'nda tanımlanan hello disk düzeni kullanan uygulamalar için düzgün çalışmayabilir unutmayın.

##### <a name="preparation"></a>Hazırlama
1. Tam hello basit hello açıklandığı gibi geçiş bölümüne. En iyi duruma getirme hello üzerinde gerçekleştirilecek hello geçişten sonra yeni VM.
2. En iyi duruma getirilmiş hello için gerekli hello yeni disk boyutları tanımlayın.
3. Merhaba geçerli diskleri/birimler toohello yeni disk belirtimleri eşlenmesini belirler.

##### <a name="execution-steps"></a>Yürütme adımları
1. Merhaba hello doğru boyutta hello Premium Storage VM'si üzerinde yeni diskleri oluşturun.
2. Oturum açma toohello VM ve kopyalama hello verileri diskten toothat birimi eşler hello geçerli birim toohello yeni. Toomap tooa yeni disk gereken tüm hello geçerli birimleri için bunu.
3. Ardından, hello uygulama ayarları tooswitch toohello yeni diskleri değiştirme ve hello eski birimlerin ayırma.

Merhaba uygulama daha iyi disk performans ayarlaması için çok başvurun[uygulama performansı en iyi duruma getirme](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Uygulama geçişleri
Veritabanları ve diğer karmaşık uygulamalar hello geçiş hello uygulama sağlayıcısı tarafından tanımlanan özel adımlar gerektirebilir. Lütfen toorespective uygulama belgelerine bakın. Örneğin veritabanlarını yedekleme genellikle geçirilebilecek ve geri yükleme.

## <a name="next-steps"></a>Sonraki adımlar
Sanal makineleri geçirmek için belirli senaryolar için kaynaklar aşağıdaki hello bakın:

* [Azure sanal makineleri depolama hesapları arasında geçiş](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Oluşturun ve Windows Server VHD tooAzure yükleyin.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Oluşturma ve bir Sanal Sabit Disk, Linux işletim sistemi içerir hello karşıya yükleme](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Amazon AWS tooMicrosoft Azure sanal makinelerden geçirme](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Ayrıca, Azure Storage ve Azure sanal makineler hakkında daha fazla kaynak toolearn aşağıdaki hello bakın:

* [Azure Depolama](https://azure.microsoft.com/documentation/services/storage/)
* [Azure sanal makineler](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
