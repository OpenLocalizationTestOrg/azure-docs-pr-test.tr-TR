---
title: "aaaRun OpenFOAM Linux VM'ler üzerinde HPC Pack ile | Microsoft Docs"
description: "Azure Microsoft HPC Pack kümede dağıtın ve bir RDMA ağ üzerinden birden çok Linux işlem düğümlerinde OpenFOAM işi çalıştırın."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>Azure’daki bir Linux RDMA kümesinde Microsoft HPC Pack ile OpenFoam çalıştırma
Bu makalede, Azure sanal makinelerinde tek yönlü toorun OpenFoam gösterir. Bir Microsoft HPC Pack kümesinde Linux işlem düğümleri ile Azure ve Çalıştır burada dağıttığınız bir [OpenFoam](http://openfoam.com/) Intel MPI işlemiyle. Böylece Hello işlem düğümleri hello Azure RDMA ağ üzerinden iletişim RDMA özellikli Azure VM'ler, hello işlem düğümleri için kullanabilirsiniz. Ticari görüntüleri hello UberCloud'ın gibi Market kullanılabilir diğer seçenekleri toorun azure'da OpenFoam dahil tam olarak yapılandırılmış [OpenFoam 2.3 CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)ve çalıştırarak [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

(İçin alan işlemi açın ve düzenleme) OpenFOAM mühendislik ve Bilim hem ticari hem de akademik kuruluşlarda yaygın olarak kullanılan bir açık kaynak hesaplama sıvı dinamiği (CFD) yazılım paketidir. Meshing, özellikle snappyHexMesh, bir parallelized mesher karmaşık CAD geometri ve öncesi ve sonrası işleme için Araçlar içerir. Neredeyse tüm işlemleri kullanıcılar tootake tam anlamıyla kendi elden bilgisayar donanımı etkinleştirme paralel olarak çalışır.  

Microsoft HPC Pack sağlayan özellikler toorun büyük ölçekli HPC ve Microsoft Azure sanal makinelerin kümelerde MPI uygulamaları da dahil olmak üzere paralel uygulamalar. HPC Pack de uygulamaların Linux işlem düğümü VM'ler bir HPC Pack kümede dağıtılmış çalışan Linux HPC destekler. Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) için bir giriş toousing Linux işlem düğümlerini HPC paketi ile.

> [!NOTE]
> Bu makalede gösterilmektedir nasıl toorun Linux MPI iş yükü HPC paketi ile. Bu, Linux sistem yönetimi ile Linux kümelerinde MPI iş yükleri çalıştıran bazı benzer olduğunu varsayar. MPI ve OpenFOAM hello bu makalede gösterilen olanları farklı sürümlerini kullanıyorsanız, bazı yükleme ve yapılandırma adımlarının toomodify olabilir. 
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* **HPC Pack küme RDMA özellikli Linux işlem düğümlerini** - HPC paketi küme boyutu A8, A9, H16r, dağıtmak veya H16rm Linux işlem düğümlerini kullanarak bir [Azure Resource Manager şablonu](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) veya bir [Azure PowerShell Betiği](hpcpack-cluster-powershell-script.md). Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) hello Önkoşullar ve adımlar her iki seçenek için. Merhaba PowerShell komut dosyası dağıtım seçeneği seçerseniz, bu makalenin hello sonunda hello örnek dosyalarında hello örnek yapılandırma dosyasına bakın. 2 boyutu A8 SUSE Linux Enterprise Server 12 işlem düğümlerini ve boyutu A8 Windows Server 2012 R2 baş düğümü oluşan bu yapılandırma toodeploy Azure tabanlı HPC paketi küme kullanın. Aboneliği ve hizmet adları için uygun değerleri değiştirin. 
  
  **Ek işlemler tooknow**
  
  * Linux RDMA ağ ön koşulu için Azure bkz [yüksek performanslı işlem VM boyutları](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Merhaba Powershell komut dosyası dağıtım seçeneğini kullanırsanız, bir bulut hizmeti toouse hello RDMA ağ bağlantısı içindeki tüm hello Linux işlem düğümlerini dağıtın.
  * Merhaba Linux düğümleri dağıttıktan sonra ek yönetim görevleri tarafından SSH tooperform bağlayın. Merhaba SSH bağlantı ayrıntıları için her bir Linux VM hello Azure portalı bulun.  
* **Intel MPI** -toorun OpenFOAM SLES 12 HPC üzerinde işlem düğümlerini Azure, tooinstall hello Intel MPI kitaplığı 5 çalışma zamanı hello gelen gerek [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/). (Intel MPI 5 CentOS tabanlı HPC görüntülerinde önceden yüklenir.)  Bir sonraki adımda gerekiyorsa, Linux işlem düğümlerinde Intel MPI yükleyin. Bu adım için tooprepare Intel ile kaydettikten sonra hello onay e-posta toohello ilgili web sayfası hello bağlantıyı izleyin. Ardından, kopyalama hello hello .tgz dosyası Intel MPI hello uygun sürümü için bağlantısını indirin. Bu makalede, Intel MPI sürüm 5.0.3.048 temel alır.
* **OpenFOAM kaynak paketi** -indirme hello OpenFOAM kaynak paketi yazılım Linux için hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/). Bu makalede kaynak paketi sürümü 2.3.1, indirme için kullanılabilir OpenFOAM 2.3.1.tgz temel alır. Daha sonra bu makalede toounpack Hello yönergeleri izleyin ve OpenFOAM hello Linux işlem düğümlerinde derleyin.
* **EnSight** (isteğe bağlı) - toosee hello OpenFOAM benzetim, sonuçlarını yükleyip hello [EnSight](https://www.ceisoftware.com/download/) Görselleştirme ve analiz program. Merhaba EnSight sitede lisans ve yükleme bilgileri var.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>İşlem düğümleri arasında karşılıklı güven ayarlama
Bir geçici düğüm işi birden çok Linux düğümler üzerinde çalışan gerektirir hello düğümleri tootrust birbirine (tarafından **rsh** veya **ssh**). Microsoft HPC Pack Iaas dağıtım betiği hello ile Merhaba HPC Pack kümesi oluşturduğunuzda, hello betik kalıcı karşılıklı güven belirttiğiniz hello yönetici hesabı için otomatik olarak ayarlar. Bir iş toothem ayrılır ve hello işi tamamlandıktan sonra hello ilişki destroy hello kümenin etki alanında oluşturduğunuz yönetici olmayan kullanıcılar için tooset hello düğümler arasında geçici karşılıklı güveni vardır. Her kullanıcı için tooestablish güven HPC Pack Merhaba güven ilişkisi kullanan bir RSA anahtar çifti toohello kümesi sağlar.

### <a name="generate-an-rsa-key-pair"></a>RSA anahtar çifti oluşturma
Kolay toogenerate bir ortak anahtar ve özel anahtarı içeren bir RSA anahtar çifti, Linux hello çalıştırarak **ssh-keygen** komutu.

1. Üzerinde tooa Linux bilgisayarda oturum açın.
2. Merhaba aşağıdaki komutu çalıştırın:
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Tuşuna **Enter** hello komut tamamlanıncaya kadar toouse hello varsayılan ayarlar. Burada bir parola girmeyin; için bir parola istendiğinde, yalnızca basın **Enter**.
   > 
   > 
   
   ![RSA anahtar çifti oluşturma][keygen]
3. Dizin toohello ~/.ssh dizini değiştirin. Merhaba özel anahtarı id_rsa.pub id_rsa ve hello ortak anahtarında depolanır.
   
   ![Özel ve genel anahtarlar][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Merhaba anahtar çifti toohello HPC paketi küme ekleme
1. Bir Uzak Masaüstü Bağlantısı tooyour baş düğüm HPC Pack Yönetici hesabınızla (Merhaba dağıtım betiğini çalıştırdığınızda ayarladığınız hello yönetici hesabı) olun.
2. Standart Windows Server yordamları toocreate bir etki alanı kullanıcı hesabı hello kümenin Active Directory etki alanında kullanın. Örneğin, hello baş düğümünde hello Active Directory Kullanıcıları ve Bilgisayarları aracını kullanın. Bu makaledeki örneklerde Hello hpclab\hpcuser adlı bir etki alanı kullanıcısı oluşturun varsayalım.
3. C:\cred.XML ve kopyalama hello RSA anahtar verilerini içine adlı bir dosya oluşturun. Bir örnek cred.xml hello bu makalenin sonundaki dosyasıdır.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Bir komut istemi açın ve tooset hello veri hello hpclab\hpcuser hesabı için kimlik bilgileri komutu aşağıdaki hello girin. Merhaba kullandığınız **extendeddata** parametresi toopass hello hello anahtar verileri için oluşturduğunuz C:\cred.xml dosyasının adı.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Bu komut çıktısı başarıyla tamamlanır. Toorun işleri ihtiyacınız hello kullanıcı hesapları için hello kimlik bilgilerini ayarlama sonra hello cred.xml dosyayı güvenli bir konumda depolayın veya silin.
5. Linux düğümlerinden biri üzerinde hello RSA anahtar çifti oluşturursa, bunları kullanmayı bitirdikten sonra toodelete hello anahtarları unutmayın. HPC Pack varolan id_rsa dosyaya veya id_rsa.pub dosyası bulursa, karşılıklı güven ayarlı değil.

> [!IMPORTANT]
> Bir yönetici tarafından gönderilen bir işin hello kök hesapta hello Linux düğümleri üzerinde çalıştığı için Linux iş paylaşılan bir kümede bir Küme Yöneticisi olarak çalışan öneririz yok. Ancak, yönetici olmayan bir kullanıcı tarafından gönderilen bir işi hello aynı hello işi kullanıcı adı ile bir yerel Linux kullanıcı hesabı altında çalışır. Bu durumda, HPC Pack bu Linux kullanıcı için karşılıklı güven toohello iş ayrılan hello düğümlere ayarlar. Merhaba Linux kullanıcı hello Linux düğümlerde el ile Merhaba işi çalıştırmadan önce ayarlayabilirsiniz veya hello iş gönderildiğinde HPC Pack Merhaba kullanıcı otomatik olarak oluşturur. HPC Pack Merhaba kullanıcı oluşturursa, HPC Pack Merhaba işi tamamlandıktan sonra onu siler. tooreduce güvenlik tehditlerine karşı HPC Pack Merhaba anahtarları işi tamamlandıktan sonra kaldırır.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Linux düğümleri için bir dosya paylaşımı ayarlama
Şimdi hello baş düğüm üzerinde bir klasör standart bir SMB paylaşımında ayarlayın. tooallow hello Linux düğümleri tooaccess uygulama dosyalarını ortak bir yol ile bağlama hello paylaşılan klasörün hello Linux düğümlerde'ü tıklatın. İsterseniz, başka bir dosya paylaşımı gibi birçok senaryo - ya da bir NFS paylaşımına için önerilen bir Azure dosya paylaşımı - seçeneği kullanabilirsiniz. Merhaba dosya bilgileri ve ayrıntılı adımlar paylaşımı bkz [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md).

1. Merhaba baş düğüm üzerinde bir klasör oluşturun ve okuma/yazma ayrıcalıklarına ayarlayarak tooEveryone paylaşın. Örneğin, hello baş düğümü olarak C:\OpenFOAM paylaşım \\ \\SUSE12RDMA HN\OpenFOAM. Burada, *SUSE12RDMA HN* hello baş düğümü hello ana bilgisayar adıdır.
2. Bir Windows PowerShell penceresi açın ve hello aşağıdaki komutları çalıştırın:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

Merhaba ilk komut hello LinuxNodes grubundaki tüm düğümlerde /openfoam adlı bir klasör oluşturur. Merhaba ikinci komut hello paylaşılan klasör //SUSE12RDMA-HN/OpenFOAM dir_mode ve file_mode BITS kümesi too777 ile Merhaba Linux düğümlerde bağlar. Merhaba *kullanıcıadı* ve *parola* hello komutu hello baş düğüm üzerinde bir kullanıcının kimlik bilgilerini hello olması gerekir.

> [!NOTE]
> Merhaba "\`" Merhaba ikinci komut dosyasındaki simge olan PowerShell bir kaçış simgesi. "\`,"anlamına gelir hello"," (virgül karakteri) hello komutu bir parçasıdır.
> 
> 

## <a name="install-mpi-and-openfoam"></a>MPI ve OpenFOAM yükleyin
toorun OpenFOAM MPI işi hello RDMA ağ üzerinde toocompile OpenFOAM hello Intel MPI kitaplıklarla gerekir. 

Öncelikle birkaç çalıştırın **clusrun** Linux düğümlerinde (henüz yüklenmemişse) tooinstall Intel MPI kitaplıkları ve OpenFOAM komutları. Kullanım hello baş düğüm paylaşımı tooshare hello yükleme dosyalarını hello Linux düğümleri arasında daha önce yapılandırılmış.

> [!IMPORTANT]
> Bu yükleme ve derleniyor adımları verilebilir. Bazı Linux sistem yönetim tooensure bağımlı derleyicileri ve kitaplıklarını düzgün yüklendiğini bilgisine gerekir. Intel MPI ve OpenFOAM sürümü için belirli ortam değişkenleri veya diğer ayarları toomodify gerekebilir. Ayrıntılar için bkz [Linux Yükleme Kılavuzu için Intel MPI Kitaplığı](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) ve [OpenFOAM kaynak paketi yüklemesi](http://openfoam.org/download/2-3-1-source/) ortamınız için.
> 
> 

### <a name="install-intel-mpi"></a>Intel MPI yükleyin
Bu dosya /openfoam Hello Linux düğümleri erişebilmesi hello karşıdan yükleme paketi C:\OpenFoam içinde Intel MPI (Bu örnekte l_mpi_p_5.0.3.048.tgz) için hello baş düğümünde kaydedin. Ardından çalıştırın **clusrun** tüm hello Linux düğümlerde tooinstall Intel MPI kitaplığı.

1. Merhaba aşağıdaki komutları kopyasını hello yükleme paketini ve çok/opt/her bir düğümde Intel ayıklayın.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI kitaplığı sessizce silent.cfg dosyasını kullanın. Bu makalenin hello sonunda örnek dosyalarını hello bir örnek bulabilirsiniz. Merhaba bu dosyada yer klasörü /openfoam paylaşılan. Merhaba silent.cfg dosyası hakkında daha fazla ayrıntı için bkz: [Linux Yükleme Kılavuzu - sessiz yükleme için Intel MPI Kitaplığı](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Silent.cfg dosyanız Linux sahip bir metin dosyası olarak kaydettiğinizde satır sonlarını (yalnızca LF, CR LF) emin olun. Bu adım, düzgün şekilde hello Linux düğümlerinde çalıştığını sağlar.
   > 
   > 
3. Intel MPI kitaplığı sessiz modda yükleyin.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>MPI yapılandırın
Test etmek için her hello Linux düğümleri satırları toohello /etc/security/limits.conf aşağıdaki hello eklemeniz gerekir:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Merhaba limits.conf dosya güncelleştirdikten sonra hello Linux düğümleri yeniden başlatın. Örneğin, hello aşağıdaki kullanın **clusrun** komutu:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Yeniden başlattıktan sonra hello paylaşılan klasörü /openfoam bağlandığından emin olun.

### <a name="compile-and-install-openfoam"></a>Derleme ve OpenFOAM yükleyin
Bu dosya /openfoam Hello Linux düğümleri erişebilmesi hello karşıdan yükleme paketi hello OpenFOAM kaynak paketi (Bu örnekte, OpenFOAM-2.3.1.tgz) tooC:\OpenFoam için hello baş düğümünde kaydedin. Ardından çalıştırın **clusrun** toocompile OpenFOAM tüm hello Linux düğümleri komutları.

1. Bir klasör /opt/OpenFOAM her Linux düğümde kopyalama hello paket toothis, kaynak klasörü oluşturun ve orada ayıklayın.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. ilk Intel MPI ve OpenFOAM için bazı ortam değişkenlerini ayarlamak hello Intel MPI kitaplığı ile toocompile OpenFOAM. Settings.sh tooset hello değişkenleri olarak adlandırılan bir bash komut dosyasını kullanın. Bu makalenin hello sonunda örnek dosyalarını hello bir örnek bulabilirsiniz. Yerleştir (Linux satır sonları ile kaydedilmiş) bu dosyada hello klasörü /openfoam paylaşılan. Bu dosya ayrıca hello MPI ve OpenFOAM çalışma zamanları sonraki toorun OpenFOAM iş kullanmak için ayarları içerir.
3. Gerekli bağımlı paketler toocompile OpenFOAM yükleyin. Linux dağıtımınız bağlı olarak, ilk tooadd depo gerekebilir. Çalıştırma **clusrun** benzer toohello aşağıdaki komutlar:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    Gerekirse, SSH tooeach Linux düğümü toorun hello düzgün çalışması tooconfirm komutları.
4. Çalışma hello aşağıdaki toocompile OpenFOAM komutu. Merhaba derleme işlemi biraz zaman toocomplete alır ve büyük miktarda günlük bilgileri toostandard çıkışını oluşturur, bu nedenle hello kullanın **/ araya eklemeli** seçeneği, araya eklemeli toodisplay hello çıktı.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Merhaba "\`" hello komut dosyasındaki simge olan PowerShell bir kaçış simgesi. "\`&" anlamına gelir Merhaba "&" Merhaba komutu, bir parçasıdır.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Toorun OpenFOAM iş hazırlama
Şimdi get hazır toorun MPI iş hello OpenFoam örnekleri olan sloshingTank3D iki Linux düğümlerinde çağrılır. 

### <a name="set-up-hello-runtime-environment"></a>Merhaba çalışma zamanı ortamını ayarlama
tooset düğümlerde hello baş düğümünde komutu bir Windows PowerShell penceresinde aşağıdaki hello çalıştırmak hello Linux hello çalışma zamanı ortamları MPI ve OpenFOAM için ayarlama. (Bu komut, yalnızca SUSE Linux için geçerlidir.)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Örnek verileri hazırlama
Kullanım hello baş düğüm Paylaşımı (/openfoam takılı) hello Linux düğümleri arasında tooshare dosyaları daha önce yapılandırılmış.

1. SSH tooone, Linux işlem düğümlerini.
2. Bunu zaten yapmadıysanız komutu tooset hello OpenFOAM çalışma zamanı ortamı kurma aşağıdaki hello çalıştırın.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Merhaba sloshingTank3D örnek toohello paylaşılan klasöre kopyalayın ve tooit gidin.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Bu örnek hello varsayılan parametrelerini kullandığınızda, toomodify isteyebilirsiniz şekilde bunu dakika toorun onlarca çalıştırmak daha hızlı bazı parametreler toomake alabilir. Bir basit toomodify hello zaman adım değişkenleri deltaT ve writeInterval hello sistem/controlDict dosyasındaki bir seçimdir. Bu dosya toohello denetim saati ve okuma ve çözüm veri yazma ile ilgili tüm giriş verilerini depolar. Örneğin, 0,05 too0.5 gelen deltaT hello değerini ve 0,05 too0.5 gelen writeInterval hello değerini değiştirebilir.
   
   ![Adım değişkenleri değiştirin][step_variables]
5. Merhaba sistem/decomposeParDict dosyasında hello değişkenleri için istenen değerleri belirtin. Bu örnek iki kullanır Linux düğümleri her 8 çekirdek sahip olacak şekilde ayarlamanız numberOfSubdomains too16 ve hierarchicalCoeffs n too(1 1 16), 16 süreçleri ile paralel OpenFOAM anlamına çalıştırın. Daha fazla bilgi için bkz: [OpenFOAM Kullanıcı Kılavuzu: paralel 3.4 çalışan uygulamaları](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).
   
   ![İşlemler parçalayın][decompose]
6. Merhaba sloshingTank3D directory tooprepare hello örnek verilerden komutları aşağıdaki hello çalıştırın.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. Merhaba baş düğümünde hello örnek veri dosyalarını C:\OpenFoam\sloshingTank3D kopyalanır görmeniz gerekir. (C:\OpenFoam hello paylaşılan hello baş düğümünde klasörüdür.)
   
   ![Merhaba baş düğüm üzerinde veri dosyaları][data_files]

### <a name="host-file-for-mpirun"></a>Ana bilgisayar dosyası mpirun için
Bu adımda, bir ana bilgisayar dosyası (işlem düğümleri listesi) hangi hello oluşturduğunuz **mpirun** komutunu kullanır.

1. Merhaba Linux düğümleri her birinde bu dosyayı /openfoam/hostfile tüm Linux düğümlerde üzerinde erişilebilir şekilde /openfoam altında hostfile adlı bir dosya oluşturun.
2. Linux düğüm adları bu dosyaya yazma. Bu örnekte, adları aşağıdaki hello hello dosya içerir:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > Bu dosya C:\OpenFoam\hostfile hello baş düğümünde de oluşturabilirsiniz. Bu seçeneği seçerseniz, Linux bir metin dosyası olarak kaydedin (yalnızca LF, CR LF) satır sonlarını. Bu, düzgün şekilde hello Linux düğümlerinde çalıştığını sağlar.
   > 
   > 
   
   **Bash betik sarmalayıcı**
   
   Hangi düğümlerin tooyour iş ayrılır tanımadığınız birçok Linux düğümleri varsa ve bazı yalnızca, iş toorun istediğiniz sabit bir ana bilgisayar dosya, iyi bir fikir toouse değildir, çünkü. Bu durumda, bir bash betik sarmalayıcı için yazma **mpirun** toocreate hello ana bilgisayar dosyası otomatik olarak. Bu makalenin hello sonunda hpcimpirun.sh olarak adlandırılan bir örnek bash betik sarmalayıcı bulmak ve /openfoam/hpcimpirun.sh kaydedin. Bu örnek komut aşağıdaki hello:
   
   1. Merhaba ortam değişkenleri için ayarlar **mpirun**ve bazı ek komut parametreleri toorun hello MPI iş hello RDMA ağ üzerinden. Bu durumda, değişkenleri aşağıdaki hello ayarlar:
      
      * I_MPI_FABRICS shm:dapl =
      * I_MPI_DAPL_PROVIDER bir v2 ib0 =
      * I_MPI_DYNAMIC_CONNECTION = 0
   2. Toohello ortam değişkeni $ göre bir ana bilgisayar dosyası oluşturur hello iş etkinleştirildiğinde, hello HPC baş düğümü tarafından ayarlanan CCP_NODES_CORES.
      
      Merhaba $CCP_NODES_CORES biçimlerinin bu deseni izler:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      Burada
      
      * `<Number of nodes>`-hello düğüm sayısını ayrılan toothis işi.  
      * `<Name of node_n_...>`-her düğümün hello adı ayrılmış toothis işi.
      * `<Cores of node_n_...>`-hello hello düğüm ayrılmış toothis işinde çekirdek sayısı.
      
      Örneğin, Hello iş iki düğüm toorun gerekirse, $CCP_NODES_CORES benzer.
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Çağrıları hello **mpirun** komut ve iki parametreleri toohello komut satırı ekler.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-hello ana bilgisayar dosyası hello betiği hello yolunu oluşturur
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-Toplam çekirdek sayısı hello depolayan hello HPC paketi üstbilgi düğümü tarafından ayarlanmış bir ortam değişkeni toothis iş ayrılmış. Bu durumda, işlemler için hello sayısını belirtir **mpirun**.

## <a name="submit-an-openfoam-job"></a>Bir OpenFOAM işi gönderin
Şimdi bir işi HPC Küme Yöneticisi'nde gönderebilirsiniz. Bazı hello iş görevleri için toopass hello betik hpcimpirun.sh hello komut satırlarında gerekir.

1. Tooyour küme baş düğümüne bağlanmak ve HPC Küme Yöneticisi'ni başlatın.
2. **Kaynak Yönetimi'nde**, hello Linux işlem düğümlerini hello olduğundan emin olun **çevrimiçi** durumu. Değilse, bunları seçin ve tıklatın **çevrimiçine**.
3. İçinde **iş yönetimi**, tıklatın **yeni iş**.
4. İş için bir ad girin *sloshingTank3D*.
   
   ![İş ayrıntıları][job_details]
5. İçinde **iş kaynakları**, kaynak olarak "Düğümü" Merhaba türünü seçin ve hello Minimum too2 ayarlayın. Bu yapılandırma, bu örnekte, her biri sekiz çekirdeği olması iki Linux düğümlerde hello işi çalıştırır.
   
   ![İş kaynakları][job_resources]
6. Tıklatın **Düzenle görevleri** hello sol gezinti bölmesinde ve ardından **Ekle** tooadd görev toohello işi. Merhaba dört görevleri toohello işlemiyle Ekle komut satırları ve ayarlar aşağıdaki.
   
   > [!NOTE]
   > Çalışan `source /openfoam/settings.sh` her görevleri aşağıdaki hello OpenFOAM komutu hello önce çağırır hello OpenFOAM ve MPI çalışma zamanı ortamları, ayarlar.
   > 
   > 
   
   * **Görev 1**. Çalıştırma **decomposePar** toogenerate veri dosyalarını çalıştırmak için **interDyMFoam** paralel.
     
     * Bir düğüm toohello görev atama
     * **Komut satırı** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Çalışma dizini** -/ openfoam/sloshingTank3D
     
     Aşağıdaki şekilde hello bakın. Merhaba kalan görevlere benzer şekilde yapılandırın.
     
     ![Görev 1 ayrıntıları][task_details1]
   * **Görev 2**. Çalıştırma **interDyMFoam** paralel toocompute hello örnek.
     
     * İki düğüm toohello görev atama
     * **Komut satırı** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Çalışma dizini** -/ openfoam/sloshingTank3D
   * **Görev 3**. Çalıştırma **reconstructPar** toomerge hello her processor_N_ dizininden zaman dizinleri tek kümesi olarak ayarlar.
     
     * Bir düğüm toohello görev atama
     * **Komut satırı** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Çalışma dizini** -/ openfoam/sloshingTank3D
   * **Görev 4**. Çalıştırma **foamToEnsight** paralel tooconvert EnSight hello OpenFOAM sonuç dosyalarıyla biçimlendirmek ve hello servis talebi dizinde Ensight adlı bir dizin hello EnSight dosyaları yerleştirir.
     
     * İki düğüm toohello görev atama
     * **Komut satırı** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Çalışma dizini** -/ openfoam/sloshingTank3D
7. Bağımlılıklar toothese görevler, görev sırası artan düzende ekleyin.
   
   ![Görev bağımlılıkları][task_dependencies]
8. Tıklatın **gönderme** toorun bu işi.
   
   Varsayılan olarak, HPC Pack Merhaba iş geçerli oturum açmış kullanıcı hesabınız olarak gönderir. Tıklattıktan sonra **gönderme**, tooenter hello kullanıcı adı ve parola isteyen bir iletişim kutusu görebilirsiniz.
   
   ![İş kimlik bilgileri][creds]
   
   Bazı koşullarda HPC Pack önce giriş ve bu iletişim kutusunu göstermez hello kullanıcı bilgilerini hatırlıyor. toomake HPC paketi yeniden göstermek, komutu bir komut isteminde aşağıdaki hello girin ve hello işi göndermek.
   
   ```
   hpccred delcreds
   ```
9. Merhaba iş hello örnek için ayarladığınız toohello parametreleri göre dakika tooseveral saat onlarca arasında geçen süredir. Merhaba ısı Haritası hello Linux düğümleri üzerinde çalışan hello işi bakın. 
   
   ![Isı Haritası][heat_map]
   
   Her düğümde sekiz işlemleri başlatıldı.
   
   ![Linux işlemleri][linux_processes]
10. Merhaba işi tamamlandığında hello iş sonuçları C:\OpenFoam\sloshingTank3D ve C:\OpenFoam hello günlüğü dosyalarını altındaki klasörleri bulun.

## <a name="view-results-in-ensight"></a>EnSight görünümü sonuçları
İsteğe bağlı olarak kullanmak [EnSight](https://www.ceisoftware.com/) toovisualize ve hello OpenFOAM iş hello sonuçlarını çözümleyin. Bu Görselleştirme ve EnSight animasyonda hakkında daha fazla bilgi için bkz [video Kılavuzu](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Merhaba baş düğümünde EnSight yükledikten sonra başlatın.
2. C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case açın.
   
   Merhaba Görüntüleyicisi'nde tank bakın.
   
   ![EnSight tank][tank]
3. Oluşturma bir **Isosurface** gelen **internalMesh**ve ardından hello değişkeni **alpha_water**.
   
   ![Bir isosurface oluşturma][isosurface]
4. Merhaba rengini ayarlama **Isosurface_part** hello önceki adımda oluşturduğunuz. Örneğin, toowater mavi ayarlayın.
   
   ![İsosurface renk Düzenle][isosurface_color]
5. Oluşturma bir **ISO hacimli** gelen **duvarları** seçerek **duvarları** hello içinde **bölümleri** panel ve Başlangıç'ı tıklatın **Isosurfaces**  hello araç çubuğu düğmesi.
6. Merhaba iletişim kutusunda seçin **türü** olarak **Isovolume** ve minimum hello **Isovolume aralığı** too0.5. toocreate isovolume Merhaba, tıklatın **Create seçilen parçaları ile**.
7. Merhaba rengini ayarlama **Iso_volume_part** hello önceki adımda oluşturduğunuz. Örneğin, toodeep su mavi ayarlayın.
8. Merhaba rengini ayarlama **duvarları**. Örneğin, tootransparent beyaz ayarlayın.
9. Şimdi **yürütmek** hello benzetimi toosee hello sonuçları.
   
    ![Tank sonucu][tank_result]

## <a name="sample-files"></a>Örnek dosyaları
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>PowerShell komut dosyası tarafından küme dağıtımı için örnek XML yapılandırma dosyası
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a>Örnek cred.xml dosyası
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Örnek silent.cfg dosya tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Örnek settings.sh komut dosyası
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Örnek hpcimpirun.sh komut dosyası
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
