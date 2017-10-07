---
title: aaaSQL Server FCI - Azure sanal makineleri | Microsoft Docs
description: "Bu makalede açıklanır toocreate SQL Server Yük devretme kümesi örneği nasıl Azure sanal makinelerde."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a>SQL Server Yük devretme kümesi örneği üzerinde Azure sanal makineleri yapılandırma

Bu makalede, nasıl toocreate bir SQL Server Yük devretme küme açıklanmaktadır Resource Manager modelinde Azure sanal makinelerde örneği (FCI). Bu çözümü kullanan [depolama alanları doğrudan Windows Server 2016 Datacenter edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) hello düğümleri (Azure VM) arasındaki hello depolama (veri diskleri) eşitleyen bir yazılım tabanlı sanal SAN olarak bir Windows Küme. S2D, Windows Server 2016'da yeni bir özelliktir.

Merhaba Aşağıdaki diyagramda hello eksiksiz bir çözüm Azure sanal makinelerde gösterilmektedir:

![Kullanılabilirlik grubu](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

Önceki diyagramda gösterildiği hello:

- İki Azure sanal makinelerinde Windows Yük devretme kümesi. Bir sanal makine bir yük devretme kümesinde olduğunda da adlandırılır bir *küme düğümü*, veya *düğümleri*.
- Her sanal makinenin iki veya daha fazla veri diski var.
- S2D hello verileri diskteki hello verileri eşitler ve bir depolama havuzu olarak eşitlenen hello depolama sunar.
- Merhaba depolama havuzu, bir Küme Paylaşılan birimi (CSV) toohello yük devretme kümesi sunar.
- Merhaba SQL Server FCI küme rolünü hello CSV hello veri sürücüleri için kullanır.
- Azure yük dengeleyici toohold hello için bir IP adresi hello SQL Server FCI.
- Bir Azure kullanılabilirlik kümesi tüm hello kaynakları tutar.

   >[!NOTE]
   >Tüm Azure hello şemada kaynaklardır hello olan aynı kaynak grubu.

S2D hakkında daha fazla ayrıntı için bkz: [depolama alanları doğrudan Windows Server 2016 Datacenter edition \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).

S2D mimarileri - yakınsanmış ve hiper yakınsanmış iki türlerini destekler. Merhaba bu belgedeki hiper yakınsanmış bir mimaridir. Bir altyapı hiper yakınsanmış yerler hello depolama aynı sunucuları, konak hello kümelenmiş uygulama hello. Bu mimaride hello depolama her SQL Server FCI düğümde ' dir.

### <a name="example-azure-template"></a>Örnek Azure şablonu

Bir şablondan Azure'da hello tüm çözüm oluşturabilirsiniz. Şablon örneği hello GitHub kullanılabilir [Azure hızlı başlangıç şablonlarını](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad). Bu örnekte değil tasarlanmış veya belirli bir iş yükü için test. Merhaba şablonu toocreate S2D depolama bağlı tooyour etki alanı ile bir SQL Server FCI çalıştırabilirsiniz. Merhaba şablon değerlendirin ve amaçlarınız için değiştirebilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce

Devam etmeden önce tooknow ve gereken şunları yerinde gereken birkaç nokta vardır.

### <a name="what-tooknow"></a>Hangi tooknow
İşletimsel bir teknolojileri aşağıdaki hello anlamış olmanız gerekir:

- [Windows Küme teknolojileri](http://technet.microsoft.com/library/hh831579.aspx)
-  [SQL Server Yük devretme kümesi örnekleri](http://msdn.microsoft.com/library/ms189134.aspx).

Ayrıca, hello teknolojileri aşağıdaki genel bir anlamış olmanız gerekir:

- [Depolama alanları doğrudan Windows Server 2016 kullanarak Hyper-yakınsanmış çözüm](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)
- [Azure kaynak grupları](../../../azure-resource-manager/resource-group-portal.md)

### <a name="what-toohave"></a>Hangi toohave

Bu makaledeki Hello yönergeleri izlemeden önce olmanız gerekir:

- Microsoft Azure aboneliği.
- Bir Windows etki alanı Azure sanal makinelerde.
- Hello Azure sanal makinesi izni toocreate nesneleri olan bir hesap.
- Bir Azure sanal ağ ve alt ağ bileşenleri aşağıdaki hello için yeterli IP adresi alanı ile:
   - Her iki sanal makineler.
   - Merhaba yük devretme küme IP adresi.
   - Her FCI için bir IP adresi.
- Merhaba toohello etki alanı denetleyicileri işaret eden Azure ağ üzerinde yapılandırılmış DNS.

Bu önkoşulları yerine getirilince, yük devretme kümesi oluşturmaya devam edebilirsiniz. Merhaba ilk toocreate hello sanal makineleri bir adımdır.

## <a name="step-1-create-virtual-machines"></a>1. adım: sanal makineler oluşturma

1. İçinde toohello oturum [Azure portal](http://portal.azure.com) aboneliğinizle.

1. [Azure kullanılabilirlik kümesi oluştur](../tutorial-availability-sets.md).

   Merhaba kullanılabilirlik grupları sanal makineleri hata etki alanlarında ayarlayın ve güncelleme etki alanları. Merhaba kullanılabilirlik kümesi, uygulamanızın hatanın Merhaba ağ anahtarı veya bir sunucu rafı hello güç ünitesi gibi tek nokta etkilenmez emin olur.

   Sanal makineleriniz için hello kaynak grubu oluşturmadıysanız, bunu bir Azure kullanılabilirlik kümesi oluşturduğunuzda. Hello Azure portal toocreate hello kullanılabilirlik kümesi kullanıyorsanız, adımları hello:

   - Hello Azure portal'ı tıklatın  **+**  tooopen hello Azure Marketi. Arama **kullanılabilirlik kümesi**.
   - Tıklatın **kullanılabilirlik kümesi**.
   - **Oluştur**'a tıklayın.
   - Merhaba üzerinde **kullanılabilirlik kümesi oluştur** dikey penceresinde, aşağıdaki değerleri kümesi hello:
      - **Ad**: hello kullanılabilirlik kümesi için bir ad.
      - **Abonelik**: bilgisayarınızı Azure aboneliği.
      - **Kaynak grubu**: toouse varolan bir grubu istiyorsanız, **var olanı kullan** ve hello aşağı açılan listeden seçim hello grubu. Seçmediğiniz **Yeni Oluştur** ve hello grubu için bir ad yazın.
      - **Konum**: sanal makinelerinizi planlama nerede toocreate hello konumunu ayarlayın.
      - **Hata etki alanları**: hello varsayılan (3) kullanın.
      - **Güncelleme etki alanları**: hello varsayılan (5) kullanın.
   - Tıklatın **oluşturma** toocreate hello kullanılabilirlik kümesi.

1. Merhaba kullanılabilirlik kümesinde Hello sanal makine oluşturun.

   Hello Azure kullanılabilirlik kümesindeki iki SQL Server sanal makine sağlayın. Yönergeler için bkz: [hello Azure portal'ın SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

   Her iki sanal makine koyun:

   - Hello, kullanılabilirlik kümesi aynı Azure kaynak grubu değil.
   - Merhaba üzerinde aynı etki alanı denetleyicisi olarak ağ.
   - Sanal makineler hem bu kümede sonunda kullanabilir tüm Fcı'lerde için yeterli IP adres alanı ile bir alt ağ üzerinde.
   - Hello Azure kullanılabilirlik kümesinde.   

      >[!IMPORTANT]
      >Ayarlayın veya bir sanal makine oluşturulduktan sonra ayarlanmış kullanılabilirlik değiştirin.

   Azure Market hello bir görüntü seçin. Bir Market kullanabilirsiniz, görüntü, Windows Server ve SQL Server ya da yalnızca hello Windows Server içerir. Ayrıntılar için bkz [genel bakış SQL Server'ın Azure sanal makineler üzerinde](../../virtual-machines-windows-sql-server-iaas-overview.md)

   hello Azure Galerisi Hello resmi SQL Server görüntülerinin bir yüklü SQL Server örneği, artı hello SQL Server yükleme yazılımı ve hello gereken anahtar içerir.

   Merhaba sağ görüntü toopay hello SQL Server Lisans için istediğiniz toohow göre seçin:

   - **Kullanım lisansı başına ödeme**: Bu görüntülerin hello dakika başına maliyet içerir hello SQL Server Lisansı:
      - **Windows Server Datacenter 2016 üzerinde SQL Server 2016 Enterprise**
      - **Windows Server Datacenter 2016 SQL Server 2016 standardı**
      - **Windows Server Datacenter 2016 SQL Server 2016 Geliştirici**

   - **Getir bilgisayarınızı-kendi-lisans (KLG)**

      - **{KLG} Windows Server Datacenter 2016 üzerinde SQL Server 2016 Enterprise**
      - **{KLG} Windows Server Datacenter 2016 SQL Server 2016 standardı**

   >[!IMPORTANT]
   >Merhaba sanal makineyi oluşturduktan sonra hello önceden yüklenmiş tek başına SQL Server örneğini kaldırın. Merhaba yük devretme kümesi ve S2D yapılandırdıktan sonra hello önceden yüklü SQL Server medya toocreate hello SQL Server FCI kullanır.

   Alternatif olarak, yalnızca hello işletim sistemiyle Azure Market görüntülerini kullanabilirsiniz. Seçin bir **Windows Server 2016 Datacenter** görüntü ve hello yük devretme kümesi ve S2D yapılandırdıktan sonra hello SQL Server FCI yükleyin. Bu görüntü, SQL Server yükleme medyasını içermiyor. Merhaba yükleme medyasını hello SQL Server yüklemesi her sunucu için çalıştırdığı bir konuma yerleştirin.

1. Azure sanal makinelerinizi oluşturduktan sonra tooeach sanal makinenin RDP ile bağlanır.

   RDP ile ilk tooa sanal makineye bağlandığınızda hello bilgisayar, tooallow bu PC toobe hello ağ üzerinde bulunabilir isteyip istemediğinizi sorar. **Evet**'e tıklayın.

1. Merhaba SQL Server tabanlı sanal makine görüntülerden birini kullanıyorsanız, hello SQL Server örneğini kaldırın.

   - İçinde **programlar ve Özellikler**, sağ **Microsoft SQL Server 2016 (64 bit)** tıklatıp **Kaldır/Değiştir**.
   - Tıklatın **kaldırmak**.
   - Merhaba varsayılan örneği seçin.
   - Tüm Özellikleri'nin altında kaldırmak **veritabanı altyapısı Hizmetleri**. Kaldırmayın **Paylaşılan Özellikler**. Resim aşağıdaki hello bakın:

      ![Özellikleri Kaldır](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - Tıklatın **sonraki**ve ardından **kaldırmak**.

1. <a name="ports"></a>Merhaba güvenlik duvarı bağlantı noktalarını açın.

   Her sanal makineye hello üzerinde Windows Güvenlik Duvarı bağlantı noktaları aşağıdaki hello açın.

   | Amaç | TCP bağlantı noktası | Notlar
   | ------ | ------ | ------
   | SQL Server | 1433 | SQL Server'ın varsayılan örnekleri için normal bağlantı noktası. Merhaba Galeriden bir görüntü kullandıysanız, bu bağlantı noktası otomatik olarak açılır.
   | Sistem durumu araştırması | 59999 | Herhangi bir TCP bağlantı noktasını açın. Bir sonraki adımda hello yük dengeleyici yapılandırmanız [durumu araştırması](#probe) ve bu bağlantı noktası küme toouse hello.  

1. Depolama toohello sanal makine ekleyin. Ayrıntılı bilgi için bkz: [depolama ekleme](../../../storage/common/storage-premium-storage.md).

   Her iki sanal makinelerin en az iki veri diskleri gerekir.

   Ham diskleri - bağlamanız değil NTFS biçimli disk.
      >[!NOTE]
      >NTFS biçimli disk eklerseniz, yalnızca hiçbir disk uygunluk denetimi ile S2D etkinleştirebilirsiniz.  

   En az iki Premium Storage (SSD diskleri) tooeach VM ekleyin. En az öneririz P30 (1 TB) diskler.

   Çok önbelleğe alma kümesi konak**salt okunur**.

   üretim ortamlarında kullanmak hello depolama kapasitesi, iş yüküne bağlıdır. Bu makalede açıklanan hello tanıtım ve test için değerlerdir.

1. [Merhaba sanal makineleri tooyour önceden var olan etki alanı ekleme](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).

Merhaba sanal makineler oluşturup yapılandırılmış sonra hello yük devretme kümesini yapılandırabilirsiniz.

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a>2. adım: hello Windows Yük devretme kümesi ile S2D yapılandırma

Merhaba sonraki S2D ile tooconfigure hello yük devretme kümesi adımdır. Bu adımda, ne yapacağını hello alt adımlar:

1. Windows Yük Devretme Kümelemesi özelliğini ekleyin
1. Merhaba küme doğrulama
1. Merhaba yük devretme kümesi oluşturma
1. Merhaba bulut tanığı oluşturma
1. Depolama ekleme

### <a name="add-windows-failover-clustering-feature"></a>Windows Yük Devretme Kümelemesi özelliğini ekleyin

1. toobegin, Yerel yöneticilerin üyesi olduğunu ve izinleri toocreate nesneleri Active Directory'de bir etki alanı hesabı kullanarak RDP toohello ilk sanal makineye bağlanın. Bu hesabı hello yapılandırma hello kalanı için kullanın.

1. [Yük Devretme Kümelemesi özelliğini tooeach sanal makine eklemek](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).

   tooinstall Yük Devretme Kümelemesi özelliğini hello UI, hello her iki sanal makine aşağıdaki adımları.
   - İçinde **Sunucu Yöneticisi'ni**, tıklatın **Yönet**ve ardından **rol ve Özellik Ekle**.
   - İçinde **Ekle roller ve Özellikler Sihirbazı**, tıklatın **sonraki** çok alana kadar**Özellikleri Seç**.
   - İçinde **Özellikleri Seç**, tıklatın **Yük Devretme Kümelemesi**. Tüm gerekli özellikleri ve hello yönetim araçlarını içerir. Tıklatın **özelliklere**.
   - Tıklatın **sonraki** ve ardından **son** tooinstall hello özellikleri.

   tooinstall hello Yük Devretme Kümelemesi özelliğiyle PowerShell, komut dosyası bir yönetici PowerShell oturumundan hello sanal makineleri biri üzerinde aşağıdaki hello çalıştırın.

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

Başvuru için sonraki adımlar hello hello adım 3'ün altında yönergeleri [depolama alanları doğrudan Windows Server 2016 kullanarak Hyper-yakınsanmış çözüm](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).

### <a name="validate-hello-cluster"></a>Merhaba küme doğrulama

Bu kılavuz altında tooinstructions başvuruyor [küme doğrulama](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).

Merhaba küme hello kullanıcı Arabirimi veya PowerShell ile doğrulayın.

Merhaba UI, toovalidate hello kümeyle hello hello sanal makineleri birinden aşağıdaki adımları.

1. İçinde **Sunucu Yöneticisi'ni**, tıklatın **Araçları**, ardından **yük devretme kümesi Yöneticisi**.
1. İçinde **yük devretme kümesi Yöneticisi**, tıklatın **eylem**, ardından **yapılandırmasını doğrula...** .
1. **İleri**’ye tıklayın.
1. Üzerinde **sunucuları Seç veya küme**, her iki sanal makine türü hello adı.
1. Üzerinde **testi seçenekleri**, seçin **yalnızca seçtiğim Testleri Çalıştır**. **İleri**’ye tıklayın.
1. Üzerinde **Test seçimi**, dışındaki tüm testleri dahil **depolama**. Resim aşağıdaki hello bakın:

   ![Testleri doğrula](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. **İleri**’ye tıklayın.
1. Üzerinde **onay**, tıklatın **sonraki**.

Merhaba **Yapılandırma Doğrulama Sihirbazı** hello doğrulama sınamalarını çalıştırır.

PowerShell komut dosyası bir yönetici PowerShell oturumundan hello sanal makineleri biri üzerinde aşağıdaki hello çalıştırmak ile toovalidate hello kümesi.

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

Merhaba küme doğrulama sonra hello yük devretme kümesi oluşturun.

### <a name="create-hello-failover-cluster"></a>Merhaba yük devretme kümesi oluşturma

Bu kılavuzda çok başvuruyor[oluşturma hello yük devretme kümesi](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).

toocreate hello yük devretme kümesi, aşağıdakiler gerekir:
- Merhaba adları hello sanal makinelerin, hello küme düğümleri haline gelir.
- Merhaba yük devretme kümesi için bir ad
- Merhaba yük devretme kümesi için bir IP adresi. Merhaba üzerinde kullanılmayan bir IP adresi kullanabileceğiniz aynı Azure sanal ağ ve küme düğümleri hello gibi alt.

PowerShell aşağıdaki hello bir yük devretme kümesi oluşturur. Merhaba betik (Merhaba sanal makine adları) hello düğümlerinin hello adlarla ve hello Azure VNET kullanılabilir bir IP adresinden güncelleştirin:

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a>Bir bulut tanığı oluşturma

Bulut tanığı, küme çekirdek tanığı bir Azure depolama Blob depolanan yeni türüdür. Bu, bir Tanık paylaşımı barındırma ayrı bir VM hello gereksinimini ortadan kaldırır.

1. [Merhaba yük devretme kümesi için bir bulut tanığı oluşturma](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).

1. Bir blob kapsayıcı oluşturun.

1. Merhaba erişim tuşları ve hello kapsayıcı URL'si kaydedin.

1. Merhaba yük devretme kümesi küme çekirdek tanığı yapılandırın. Bakın, [hello çekirdek tanığı hello kullanıcı arabiriminde Yapılandır]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) hello UI içinde.

### <a name="add-storage"></a>Depolama ekleme

S2D Hello diskler boş ve bölümleri veya diğer veri olmadan toobe gerekir. tooclean diskleri izleyin [hello bu kılavuzdaki adımları](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).

1. [Etkinleştirme depolama alanları doğrudan \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).

   PowerShell aşağıdaki hello doğrudan depolama alanları sağlar.  

   ```PowerShell
   Enable-ClusterS2D
   ```

   İçinde **yük devretme kümesi Yöneticisi**, hello depolama havuzu şimdi görebilirsiniz.

1. [Bir birim oluşturmak](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).

   Merhaba özelliklerinden biri S2D, etkinleştirdiğinizde, otomatik olarak bir depolama havuzu oluşturmasıdır. Hazır toocreate bir birim sunulmuştur. PowerShell komutunu hello `New-Volume` biçimlendirme, toohello küme ekleme ve Küme Paylaşılan birimi (CSV) oluşturma gibi hello birim oluşturma işlemini otomatikleştirir. Aşağıdaki örnek hello 800 bir gigabayt (GB) CSV oluşturur.

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   Bu komut tamamlandıktan sonra bir 800 GB birimin küme kaynağı olarak bağlı. Hello birimdir adresindeki `C:\ClusterStorage\Volume1\`.

   Aşağıdaki diyagramda hello S2D ile Küme Paylaşılan birimi gösterir:

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a>3. adım: Test yük devretme küme yük devretmesi

Yük Devretme Kümesi Yöneticisi'nde, diğer küme düğümünde hello depolama kaynak toohello taşıyabildiğinizi doğrulayın. Bağlanabiliyorsa toohello yük devretme kümesi **yük devretme kümesi Yöneticisi** ve tek bir düğüm toohello diğer hello depolama birimini taşımak, hazır tooconfigure hello FCI olur.

## <a name="step-4-create-sql-server-fci"></a>4. adım: SQL Server FCI oluşturma

Merhaba yük devretme kümesi ve depolama da dahil olmak üzere tüm küme bileşenleri yapılandırdıktan sonra SQL Server FCI hello oluşturabilirsiniz.

1. RDP ile toohello ilk sanal makineye bağlanın.

1. İçinde **yük devretme kümesi Yöneticisi**, tüm küme çekirdek kaynakları hello ilk sanal makinede olduğundan emin olun. Gerekirse, tüm kaynakları toothis sanal makineyi taşıyın.

1. Merhaba yükleme medyasını bulun. Merhaba sanal makine hello Azure Marketi görüntülerden birini kullanıyorsa, hello medya konumundadır `C:\SQLServer_<version number>_Full`. Tıklatın **Kurulum**.

1. Merhaba, **SQL Server Yükleme Merkezi'ni**, tıklatın **yükleme**.

1. Tıklatın **yeni SQL Server Yük devretme kümesi yükleme**. Merhaba Sihirbazı tooinstall hello SQL Server FCI'Hello yönergelerini izleyin.

   Merhaba FCI veri dizinlerini toobe kümelenmiş depolama gerekir. S2D ile paylaşılan bir disk, ancak her sunucu üzerindeki bir bağlama noktası tooa birimi değil. Her iki düğüm arasında hello birim S2D eşitler. Merhaba birim toohello Küme Küme Paylaşılan birimi olarak sunulur. Merhaba CSV bağlama noktası hello veri dizinler için kullanın.

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. Merhaba Sihirbazı tamamladıktan sonra kurulumu bir SQL Server FCI hello ilk düğüme yükleyin.

1. Kurulum başarıyla hello ilk düğümde hello FCI yüklendikten sonra toohello İkinci düğüm RDP ile bağlanır.

1. Açık hello **SQL Server Yükleme Merkezi'ni**. Tıklatın **yükleme**.

1. Tıklatın **Ekle düğüm tooa SQL Server Yük devretme kümesi**. Merhaba Sihirbazı tooinstall SQL Server'daki Hello yönergeleri izleyin ve bu sunucu toohello FCI ekleyin.

   >[!NOTE]
   >SQL Server ile bir Azure Market galeri görüntüsü kullandıysanız, SQL Server araçları hello görüntüsüne dahil edilir. Bu görüntü kullanmadıysanız hello SQL Server araçları ayrı olarak yükleyin. Bkz: [karşıdan SQL Server Management Studio'yu (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="step-5-create-azure-load-balancer"></a>5. adım: Azure yük dengeleyici oluşturma

Azure sanal makinelerde kümeleri bir yük dengeleyici toohold aynı anda bir küme düğümünde toobe gerektiren bir IP adresi kullanın. Bu çözümde hello yük dengeleyici hello SQL Server FCI için başlangıç IP adresi tutar.

[Oluşturma ve Azure yük dengeleyici yapılandırma](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a>Hello Azure portal Hello yük dengeleyici oluşturma

toocreate hello yük dengeleyici:

1. Hello Azure portal, hello sanal makinelerle toohello kaynak grubuna gidin.

1. Tıklatın **+ Ekle**. Arama hello Market için **yük dengeleyici**. Tıklatın **yük dengeleyici**.

1. **Oluştur**'a tıklayın.

1. Merhaba yük dengeleyici ile yapılandırın:

   - **Ad**: hello yük dengeleyici tanımlayan bir ad.
   - **Tür**: hello yük dengeleyici, genel veya özel olabilir. Özel yük dengeleyici içinden erişilebilir aynı sanal ağı hello. Çoğu Azure uygulamaları özel yük dengeleyici kullanabilirsiniz. Uygulamanızı hello Internet üzerinden doğrudan erişim tooSQL sunucu gerekiyorsa, bir genel yük dengeleyiciye kullanın.
   - **Sanal ağ**: aynı ağ hello sanal makine olarak hello.
   - **Alt ağ**: Merhaba hello sanal makineler aynı alt ağda.
   - **Özel IP adresi**: Merhaba toohello SQL Server FCI küme ağ kaynağı atanmış aynı IP adresi.
   - **Abonelik**: bilgisayarınızı Azure aboneliği.
   - **Kaynak grubu**: kullanım hello aynı kaynak grubu, sanal makineleriniz olarak.
   - **Konum**: kullanım hello aynı sanal makinelerinizi olarak Azure konumu.
   Resim aşağıdaki hello bakın:

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a>Merhaba yük dengeleyici arka uç havuzunu yapılandırma

1. Toohello Azure kaynak grubu hello sanal makinelerle dönün ve hello Yeni Yük Dengeleyici bulun. Toorefresh hello görünüm olabilir hello kaynak grubu üzerinde. Merhaba yük dengeleyici'ı tıklatın.

1. Merhaba yük dengeleyici dikey penceresinde **arka uç havuzları**.

1. Tıklatın **+ Ekle** tooadd bir arka uç havuzu.

1. Merhaba arka uç havuzu için bir ad yazın.

1. Tıklatın **bir sanal makine Ekle**.

1. Merhaba üzerinde **sanal makineleri seçin** dikey penceresinde tıklatın **bir kullanılabilirlik kümesi seçin**.

1. Merhaba SQL Server sanal makinelerinizde yerleştirilen Hello kullanılabilirlik kümesi'ni seçin.

1. Merhaba üzerinde **sanal makineleri seçin** dikey penceresinde tıklatın **hello sanal makineleri seçin**.

   Azure portal'ınızın hello resim aşağıdaki gibi görünmelidir:

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. Tıklatın **seçin** hello üzerinde **sanal makineleri seçin** dikey.

1. Tıklatın **Tamam** iki kez.

### <a name="configure-a-load-balancer-health-probe"></a>Bir yük dengeleyici durum araştırması yapılandırın

1. Merhaba yük dengeleyici dikey penceresinde **sistem durumu araştırmalarının**.

1. Tıklatın **+ Ekle**.

1. Merhaba üzerinde **Ekle durumu araştırması** dikey penceresinde <a name="probe"> </a>Set hello sistem durumu araştırma Parametreler:

   - **Ad**: hello durumu araştırması için bir ad.
   - **Protokol**: TCP.
   - **Bağlantı noktası**: tooan kullanılabilir TCP bağlantı noktası ayarlayın. Bu bağlantı noktası açık güvenlik duvarı bağlantı noktası gerektirir. Kullanım hello [aynı bağlantı noktasını](#ports) hello güvenlik duvarında hello sistem durumu araştırması için ayarlayın.
   - **Aralığı**: 5 saniye.
   - **Sağlıksız eşik**: 2 art arda hatalar.

1. Tamam'a tıklayın.

### <a name="set-load-balancing-rules"></a>Yük Dengeleme kuralları ayarlama

1. Merhaba yük dengeleyici dikey penceresinde **Yük Dengeleme kuralları**.

1. Tıklatın **+ Ekle**.

1. Merhaba Yük Dengeleme kuralları parametrelerini ayarlayın:

   - **Ad**: hello Yük Dengeleme kuralları için bir ad.
   - **Ön uç IP adresi**: SQL Server FCI küme ağ kaynağı hello için başlangıç IP adresi kullanın.
   - **Bağlantı noktası**: Merhaba SQL Server FCI TCP bağlantı noktası ayarlayın. Merhaba varsayılan örnek bağlantı noktası 1433'tür.
   - **Arka uç bağlantı noktası**: Bu değer aynı bağlantı noktası hello hello kullanan **bağlantı noktası** değeri, etkinleştirdiğinizde **kayan IP (doğrudan sunucu dönüşü)**.
   - **Arka uç havuzu**: daha önce yapılandırılmış hello arka uç havuzu adını kullan.
   - **Sistem durumu araştırma**: daha önce yapılandırılmış hello durumu araştırması kullanın.
   - **Oturum kalıcılığı**: yok.
   - **Boşta kalma zaman aşımı (dakika)**: 4.
   - **Kayan IP (doğrudan sunucu dönüşü)**: etkin

1. **Tamam** düğmesine tıklayın.

## <a name="step-6-configure-cluster-for-probe"></a>Adım 6: küme araştırma için yapılandırın

Merhaba küme araştırma port parametresi PowerShell'de ayarlayın.

tooset küme araştırma port parametresi Merhaba, ortamınızdan komut dosyası izleyen hello değişkenlerde güncelleştirin.

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a>7. adım: Test FCI yük devretme

Merhaba FCI toovalidate küme işlevselliğini yük devretme sınamasını. Adımları hello:

1. Merhaba SQL Server FCI küme düğümlerinin tooone RDP ile bağlanır.

1. Açık **yük devretme kümesi Yöneticisi**. Tıklatın **rolleri**. Merhaba SQL Server FCI rol sahibi olan düğümü dikkat edin.

1. Merhaba SQL Server FCI role sağ tıklayın.

1. Tıklatın **taşıma** tıklatıp **olası iyi düğüme**.

**Yük Devretme Kümesi Yöneticisi** gösterir hello rolü ve kaynaklarını çevrimdışı. Merhaba kaynakları sonra taşıyın ve çevrimiçi duruma açık, başka bir düğüme hello.

### <a name="test-connectivity"></a>Bağlantıyı test etme

tootest bağlantısı, hello tooanother sanal makinede günlüğüne aynı sanal ağ. Açık **SQL Server Management Studio** ve toohello SQL Server FCI adı bağlanın.

>[!NOTE]
>Gerekirse, aşağıdakileri yapabilirsiniz, [SQL Server Management Studio'yu indirme](http://msdn.microsoft.com/library/mt238290.aspx).

## <a name="limitations"></a>Sınırlamalar
Azure sanal makinelerde Hello RPC bağlantı noktası hello yük dengeleyici tarafından desteklenmediği için Microsoft Dağıtılmış İşlem Düzenleyicisi (DTC) Fcı'lerde üzerinde desteklenmiyor.

## <a name="see-also"></a>Ayrıca Bkz.

[Uzak Masaüstü'nü (Azure) S2D Kurulumu](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)

[Depolama alanları doğrudan ile çözüm Hyper yakınsanmış](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).

[Depolama alanına doğrudan genel bakış](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)

[S2D için SQL Server desteği](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)
