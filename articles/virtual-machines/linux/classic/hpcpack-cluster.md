---
title: "aaaLinux bir HPC Pack kümede sanal makineleri işlem | Microsoft Docs"
description: "Nasıl toocreate ve kullanım bir HPC Pack Linux yüksek performanslı bilgi işlem (HPC) iş yükleri için Azure'da küme öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Azure’daki bir HPC Pack kümesinde Linux işlem düğümleri kullanmaya başlama
Ayarlanmış bir [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) küme Windows Server ve birkaç çalıştıran bir baş düğüm içeren Azure işlem desteklenen Linux dağıtım çalışan düğümleri. Merhaba Linux düğümleri ve hello Windows hello küme baş düğümüne arasındaki seçenekleri toomove verileri keşfedin. Nasıl toohello küme toosubmit Linux HPC iş öğrenin.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Yüksek bir düzeyde hello Aşağıdaki diyagramda hello HPC paketi küme oluşturun ve çalışmak gösterilmektedir.

![Linux düğümleri ile HPC Pack kümesi][scenario]

Diğer Seçenekler toorun Linux HPC için azure'da iş yüklerini bkz [toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar](../../../batch/big-compute-resources.md).

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a>Linux işlem düğümlerini içeren bir HPC Pack kümeyi dağıtma
Bu makalede, iki seçenek toodeploy bir HPC paketi küme Linux işlem düğümleri ile Azure'da gösterilmektedir. İki yöntem HPC Pack toocreate hello baş düğüm ile Windows Server Market görüntüsünü kullanır. 

* **Azure Resource Manager şablonu** -hello Azure Marketi bir şablondan ya da hello topluluktan hello Resource Manager dağıtım modelinde hello kümesinin tooautomate oluşturulması hızlı başlatma şablonunu kullanın. Örneğin, hello [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) hello Azure Marketi şablonunda Linux HPC için eksiksiz bir HPC paketi küme altyapı iş yükleri oluşturur.
* **PowerShell Betiği** -kullanım hello [Microsoft HPC Pack Iaas dağıtım betiği](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**yeni HpcIaaSCluster.ps1**) tooautomate hello Klasik dağıtım modeli tam küme dağıtımında. Bu Azure PowerShell komut dosyasını bir HPC Pack VM görüntüsü hello Azure Marketi hızlı dağıtımı için kullanır ve Linux işlem düğümlerini yapılandırma parametreleri toodeploy kapsamlı bir kümesini sağlar.

Azure içindeki HPC paketi küme dağıtım seçenekleri hakkında daha fazla bilgi için bkz: [seçenekleri toocreate ve Microsoft HPC paketi ile Azure yüksek performanslı bilgi işlem (HPC) bir kümede yönetmek](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="prerequisites"></a>Ön koşullar
* **Azure aboneliği** -ya da hello Azure genel ya da Azure Çin hizmeti bir aboneliği kullanabilirsiniz. Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.
* **Çekirdek kota** -özellikle çok çekirdekli VM boyutları birkaç küme düğümleri toodeploy seçerseniz tooincrease hello kota çekirdek, gerekebilir. tooincrease bir kota ücretsiz bir çevrimiçi müşteri destek isteği açın.
* **Linux dağıtımları** -şu anda HPC Pack Merhaba işlem düğümleri için Linux dağıtımları aşağıdaki destekler. Bu dağıtımları Market sürümleri kullanılabiliyorsa kullanın veya kendi sağlayın.
  
  * **CentOS tabanlı**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC
  * **Red Hat Enterprise Linux**: 6.7, 6,8, 7.2
  * **SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 HPC, SLES 12 HPC (Premium) için için
  * **Ubuntu Server**: 14.04 LTS, 16.04 LTS
    
    > [!TIP]
    > toouse hello Azure RDMA ağ hello RDMA özelliğine sahip VM boyutları, biri ile bir SUSE Linux Enterprise Server 12 HPC veya CentOS tabanlı HPC hello Azure Market görüntüsünden belirtin. Daha fazla bilgi için bkz: [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

Merhaba HPC Pack Iaas dağıtım komut dosyası kullanarak toodeploy hello küme ek önkoşulları:

* **İstemci bilgisayar** -bir Windows tabanlı bir istemci bilgisayar toorun hello küme dağıtım betiğinin gerekir.
* **Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.
* **HPC Pack Iaas dağıtım betiği** - karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Merhaba komut dosyasının hello sürümünü çalıştırarak denetleyebilirsiniz `.\New-HPCIaaSCluster.ps1 –Version`. Bu makalede, sürüm 4.4.1 veya daha sonra hello komut dosyasının temel alır.

### <a name="deployment-option-1-use-a-resource-manager-template"></a>Dağıtım seçeneği 1. Resource Manager şablonu kullanın
1. Toohello Git [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) şablonunda Azure Marketi hello öğesini tıklatıp **dağıtma**.
2. İçinde Azure portal Merhaba, hello bilgileri gözden geçirin ve ardından **oluşturma**.
   
    ![Portal oluşturma][portal]
3. Merhaba üzerinde **Temelleri** dikey penceresinde de hello baş düğüm VM adları hello küme için bir ad girin. Varolan bir kaynak grubu seçin veya kullanılabilir tooyou olan bir konuma hello dağıtım için bir grup oluşturun. Merhaba konumu hello kullanılabilirliğini belirli VM boyutları ve diğer Azure hizmetleriyle etkiler (bkz [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/)).
4. Merhaba üzerinde **düğümü ayarları Head** dikey penceresinde, ilk dağıtım için genellikle hello varsayılan ayarları kabul edebilirsiniz. 
   
   > [!NOTE]
   > Merhaba **sonrası yapılandırma betiği URL'si** isteğe bağlı bir toospecify çalışmaya başladıktan sonra hello baş düğümünde VM toorun istediğiniz genel kullanıma açık bir Windows PowerShell komut dosyası da ayarlıyor. 
   > 
   > 
5. Merhaba üzerinde **düğümü ayarları işlem** dikey penceresinde hello düğümleri, hello sayısını ve boyutunu hello düğümler için bir adlandırma deseni seçin ve Linux dağıtım toodeploy hello.
6. Merhaba üzerinde **Altyapı ayarlarını** dikey penceresinde hello sanal ağ ve Active Directory adlarını girin etki alanı, etki alanı ve VM yönetici kimlik bilgileri ve hello depolama hesapları için bir adlandırma deseni.
   
   > [!NOTE]
   > HPC Pack Merhaba Active Directory etki alanı tooauthenticate küme kullanıcıları kullanır. 
   > 
   > 
7. Merhaba doğrulama testlerini çalıştırmak ve hello kullanım koşullarını gözden geçirin sonra tıklayın **satın alma**.

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a>Dağıtım seçeneği 2. Merhaba Iaas dağıtım betiği kullanın
Aşağıda hello HPC Pack Iaas dağıtım komut dosyası kullanarak ek önkoşulları toodeploy hello küme verilmiştir:

* **İstemci bilgisayar** -bir Windows tabanlı bir istemci bilgisayar toorun hello küme dağıtım betiğinin gerekir.
* **Azure PowerShell** - [yükleyin ve Azure PowerShell yapılandırma](/powershell/azure/overview) (sürüm 0.8.10 veya üzeri) istemci bilgisayarınızda.
* **HPC Pack Iaas dağıtım betiği** - karşıdan yükle ve en son sürümünü hello hello betikten hello paket [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Merhaba komut dosyasının hello sürümünü çalıştırarak denetleyebilirsiniz `.\New-HPCIaaSCluster.ps1 –Version`. Bu makalede, sürüm 4.4.1 veya daha sonra hello komut dosyasının temel alır.

**XML yapılandırma dosyası**

Merhaba HPC Pack Iaas dağıtım betiği giriş toodescribe hello HPC kümesi olarak bir XML yapılandırma dosyasını kullanır. Merhaba aşağıdaki örnek yapılandırma dosyası bir HPC paketi üstbilgi düğümü ve iki boyutu A7 CentOS 7.0 Linux işlem düğümleri oluşan küçük bir küme belirtir. 

Merhaba dosya ortamınız ve istenen küme yapılandırması için gereken şekilde değiştirin ve HPCDemoConfig.xml gibi bir adla kaydedin. Örneğin, toosupply abonelik adı ve benzersiz depolama hesabı adı ve bulut hizmeti adı gerekir. Ayrıca, farklı bir toochoose Linux görüntü hello işlem düğümleri için desteklenen isteyebilirsiniz. Hello yapılandırma dosyasında hello öğeler hakkında daha fazla bilgi için bkz: hello betik klasöründeki hello Manual.rtf dosyasını ve [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

**toorun hello HPC Pack Iaas dağıtım komut dosyası**

1. Windows PowerShell hello istemci bilgisayarda yönetici olarak açın.
2. Değişiklik hello betik olduğu dizin toohello klasörü yüklü (Bu örnekte E:\IaaSClusterScript).
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. Komut toodeploy hello HPC paketi küme aşağıdaki hello çalıştırın. Bu örnekte hello yapılandırma dosyasının E:\HPCDemoConfig.xml içinde bulunan varsayılmaktadır.
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    a. Çünkü hello **Admınpassword** belirtilmezse komut önceki hello olduğunuz istendiğinde tooenter hello kullanıcının parolasını *MyAdminName*.
   
    b. Merhaba betik sonra toovalidate hello yapılandırma dosyasını başlatır. Yukarı hello ağ bağlantısı bağlı olarak tooseveral dakika sürebilir.
   
    ![Doğrulama][validate]
   
    c. Doğrulama geçirmek sonra hello betik hello küme kaynakları toocreate listeler. Girin *Y* toocontinue.
   
    ![Kaynaklar][resources]
   
    d. Merhaba betik toodeploy hello HPC paketi küme başlar ve daha fazla el ile adımlar olmadan hello yapılandırmasını tamamlar. Merhaba komut dosyası için birkaç dakika çalışabilir.
   
    ![Dağıtma][deploy]
   
   > [!NOTE]
   > Bu örnekte, hello komut dosyası günlük dosyası otomatik olarak bu yana hello oluşturur **- günlük dosyası** parametresinde değil. Merhaba günlükleri gerçek zamanlı olarak yazılmış değil, ancak hello sonunda hello doğrulama ve başlangıç dağıtım toplanır. Merhaba betik çalışırken hello PowerShell işlem durursa, bazı günlükleri kaybolur.
   > 
   > 

## <a name="connect-toohello-head-node"></a>Toohello baş düğümüne bağlanmak
Azure'da hello HPC paketi küme dağıttıktan sonra [tarafından Uzak Masaüstü Bağlantısı](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello baş düğüm VM kullanarak hello hello kümeyi dağıttığınızda sağlanan etki alanı kimlik bilgilerini (örneğin, *hpc\\ clusteradmin*). Merhaba küme hello baş düğümünden yönetin.

Merhaba baş düğümünde HPC Küme Yöneticisi'ni toocheck hello hello HPC paketi küme durumunu başlatın. Yönetme ve Linux işlem düğümlerini izleme hello Windows ile birlikte çalıştığınız aynı şekilde işlem düğümlerini. Örneğin, listelenen hello Linux düğümleri bkz **kaynak yönetimi** (Bu düğümler hello ile dağıtılan **LinuxNode** şablonu).

![Düğüm Yönetimi][management]

Merhaba hello Linux düğümleri Ayrıca bkz: **ısı Haritası** görünümü.

![Isı Haritası][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a>Nasıl Linux düğümleri ile bir kümede toomove veri
Linux düğümleri ve hello Windows hello küme baş düğümüne arasında birkaç seçenek toomove veri içeriyor. Merhaba aşağıdaki bölümlerde daha ayrıntılı açıklanan üç yaygın yöntemleri şunlardır:

* **Azure dosya** -yönetilen bir SMB dosya paylaşımı toostore verileri Azure depolama alanında dosyaları açığa çıkarır. Windows düğümleri ve Linux düğümleri takma bir Azure dosya paylaşımı bir sürücü veya klasöre hello olarak aynı zaman, farklı sanal ağlarda dağıtmış olsa bile.
* **Baş düğüm SMB paylaşımı** -Linux düğümleri üzerinde Windows standart bir paylaşılan klasör hello baş düğümü bağlar.
* **Baş düğüm NFS sunucusu** -karma Windows ve Linux ortamı için bir dosya paylaşımı çözümü sağlar.

### <a name="azure-file-storage"></a>Azure dosya depolama
Merhaba [Azure dosya](https://azure.microsoft.com/services/storage/files/) hizmetini hello standart SMB 2.1 protokolünü kullanan dosya paylaşımları sunar. Azure VM'ler ve cloud services bağlı paylaşımlar üzerinden uygulama bileşenleri arasında dosya verileri paylaşabilir ve şirket içi uygulamalara hello File storage API'si dosya verilerine erişebilir. 

Bir Azure dosya paylaşımı ve hello baş düğümünde bağlama ayrıntılı adımlar toocreate için bkz: [Windows Azure File storage ile çalışmaya başlama](../../../storage/files/storage-how-to-use-files-windows.md). Merhaba Linux düğümleri toomount hello Azure dosya paylaşımında bkz [nasıl toouse Linux Azure File storage](../../../storage/files/storage-how-to-use-files-linux.md). kalıcı bağlantılar kurma tooset bkz [Persisting bağlantıları tooMicrosoft Azure dosyaları](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).

Aşağıdaki örneğine hello Azure dosya paylaşımı bir depolama hesabı oluşturun. toomount hello hello baş düğümünde, açık bir komut istemi paylaşma ve hello aşağıdaki komutları girin:

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

Bu örnekte, depolama hesabınızın adını allvhdsje olduğundan, depolama alanı hesabı anahtarınız storageaccountkey ise ve rdma hello Azure dosya paylaşımı adı.. Hello Azure dosya paylaşımı Z: hello baş düğümünde bağlı.

çalıştırma Linux düğümleri toomount hello Azure dosya paylaşımında bir **clusrun** hello baş düğümünde komutu. **[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)**  yararlı bir HPC Pack aracı toocarry yönetim görevlerini birden çok düğümde değil. (Ayrıca bkz. [Clusrun Linux düğümleri için](#Clusrun-for-Linux-nodes) bu makalede.)

Bir Windows PowerShell penceresi açın ve aşağıdaki komutları hello girin:

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /rdma adlı bir klasör oluşturur. Merhaba ikinci komut hello Azure dosya paylaşımı allvhdsjw.file.core.windows.net/rdma hello /rdma dir ve dosya modu BITS kümesi too777 klasörüyle üzerine bağlar. Merhaba ikinci komutta allvhdsje depolama hesabınızın adını ve storageaccountkey depolama hesabı anahtarınızı.

> [!NOTE]
> Merhaba "\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi. "\`,"anlamına gelir, hello"," (virgül karakteri) hello komutu bir parçasıdır.
> 
> 

### <a name="head-node-share"></a>Baş düğüm paylaşımı
Alternatif olarak, paylaşılan bir klasöre hello baş düğümü Linux düğümleri üzerinde bağlayın. Bir paylaşım hello en basit yolu tooshare dosyaları sağlar, ancak hello baş düğümü ve tüm Linux düğümleri hello dağıtılmalıdır aynı sanal ağ. Merhaba adımlar şunlardır.

1. Merhaba baş düğüm üzerinde bir klasör oluşturun ve okuma/yazma izinlerine sahip tooEveryone paylaşın. Örneğin, hello baş düğümü olarak D:\OpenFOAM paylaşım \\CentOS7RDMA HN\OpenFOAM. Burada CentOS7RDMA HN hello baş düğüm hello barındırıcı adıdır.
   
    ![Dosya paylaşım izinleri][fileshareperms]
   
    ![Dosya Paylaşımı][filesharing]
2. Bir Windows PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /openfoam adlı bir klasör oluşturur. Merhaba ikinci komut hello paylaşılan klasör //CentOS7RDMA-HN/OpenFOAM dir ve dosya modu BITS kümesi too777 hello klasörüyle üzerine bağlar. Merhaba kullanıcı adı ve parola hello komutta hello kullanıcı adı ve parola bir küme kullanıcının hello baş düğüm üzerinde olmalıdır. (Bkz [ekleme veya kaldırma küme kullanıcılar](https://technet.microsoft.com/library/ff919330.aspx).)

> [!NOTE]
> Merhaba "\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi. "\`,"anlamına gelir, hello"," (virgül karakteri) hello komutu bir parçasıdır.
> 
> 

### <a name="nfs-server"></a>NFS sunucusu
Merhaba NFS hizmeti ve dosyalar hello SMB protokolünü kullanarak hello Windows Server 2012 işletim sistemi çalıştıran bilgisayarlar ile hello NFS protokolünü kullanarak Linux tabanlı bilgisayarlar arasında geçirmek tooshare sağlar. Merhaba NFS sunucusu ve diğer tüm düğümlere dağıtılan hello toobe sahip aynı sanal ağ. Linux düğümleriyle SMB paylaşımı ile karşılaştırıldığında daha iyi uyumluluk sağlar. Örneğin, dosya bağlantıları destekler.

1. tooinstall ve bir NFS sunucusunun ayarlama izleyin hello adımlarda [sunucusu için ağ dosya sistemi ilk paylaşımını uçtan uca](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).
   
    Örneğin, aşağıdaki özelliklere hello ile nfs adlı bir NFS paylaşımına oluşturun:
   
    ![NFS yetkilendirme][nfsauth]
   
    ![NFS paylaşım izinlerini][nfsshare]
   
    ![NFS NTFS izinleri][nfsperm]
   
    ![NFS yönetim özellikleri][nfsmanage]
2. Bir Windows PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /nfsshared adlı bir klasör oluşturur. Merhaba ikinci komutu başlatmalar hello NFS paylaşım CentOS7RDMA HN: / nfs üzerine hello klasör. Burada CentOS7RDMA HN: nfs olduğu, bir NFS paylaşımına hello uzak yolu.

## <a name="how-toosubmit-jobs"></a>Nasıl toosubmit işleri
Çeşitli yolları toosubmit işleri toohello HPC paketi küme vardır:

* HPC Küme Yöneticisi'ni veya HPC İş Yöneticisi GUI
* HPC web portalı
* REST API

HPC Pack GUI araçları ve hello HPC web Portalı aracılığıyla Azure toohello küme olan hello aynı Windows işlem düğümleri için olduğu gibi iş gönderme. Bkz: [HPC Pack İş Yöneticisi](https://technet.microsoft.com/library/ff919691.aspx) ve [nasıl toosubmit bir şirket içi istemci bilgisayarından işleri](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Merhaba REST API aracılığıyla toosubmit işleri başvurmak çok[oluşturma ve gönderme işleri kullanarak REST API Microsoft HPC Pack Merhaba](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx). bir Linux istemciden toosubmit işleri ayrıca hello toohello Python örnek başvuru [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).

## <a name="clusrun-for-linux-nodes"></a>Linux düğümleri için Clusrun
HPC Pack Merhaba [clusrun](https://technet.microsoft.com/library/cc947685.aspx) aracı Linux düğümleri ya da bir komut istemini veya HPC Küme Yöneticisi aracılığıyla kullanılan tooexecute komutlarını olabilir. Temel bazı örnekler verilmiştir.

* Merhaba kümedeki tüm düğümlerde geçerli kullanıcı adlarını gösterir.
  
    ```command
    clusrun whoami
    ```
* Merhaba yüklemek **gdb** hata ayıklayıcısı aracı ile **yum** linuxnodes grup ve hello düğümleri 10 dakika sonra yeniden hello tüm düğümlerde.
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* Hello kümedeki her numarası 1 ile 10 her Linux düğümde bir saniye için görüntüleme bir kabuk betiği oluşturmak, çalıştırmak ve çıktı hello düğümlerinden hemen göster.
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> Toouse gerekebilecek belirli kaçış karakterleri **clusrun** komutları. Bu örnekte gösterildiği gibi kullanın ^ bir komut istemi tooescape hello içinde ">" simgesi.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba küme tooa fazla sayıda düğüm ölçeklendirme deneyin veya Linux iş yükü hello kümede çalıştırmayı deneyin. Bir örnek için bkz: [çalıştırmak NAMD Microsoft HPC Pack Linux işlem düğümlerini Azure](hpcpack-cluster-namd.md).
* Bir küme ile deneyin [RDMA özellikli, işlem yoğunluklu VM'ler](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI iş yükleri. Bir örnek için bkz: [çalıştırmak OpenFOAM Linux RDMA üzerinde Microsoft HPC Pack ile küme Azure'da](hpcpack-cluster-openfoam.md).
* İçinde bir şirket içi HPC Pack kümesindeki Linux düğümleri ile çalışma ilgileniyorsanız hello bkz [TechNet Kılavuzu](https://technet.microsoft.com/library/mt595803.aspx).

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
