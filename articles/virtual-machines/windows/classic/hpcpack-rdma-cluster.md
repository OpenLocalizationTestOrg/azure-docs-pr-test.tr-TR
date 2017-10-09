---
title: "bir Windows RDMA küme toorun MPI uygulamaları aaaSet | Microsoft Docs"
description: "Nasıl toocreate boyutu H16r, H16mr, A8 veya A9 Vm'lerde toouse Microsoft HPC Pack kümeyle hello Azure RDMA ağ toorun MPI uygulamaları hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 7d9f5bc8-012f-48dd-b290-db81c7592215
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 23bc8740dbd05a7c7ab3f998489a41d0df4520a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-windows-rdma-cluster-with-hpc-pack-toorun-mpi-applications"></a>HPC Pack toorun MPI uygulamaları ile Windows RDMA kümesi ayarlama
Azure ile Windows RDMA kümedeki ayarlamak [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) ve [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun paralel ileti geçirme arabirimi (MPI) uygulamalarını. RDMA özelliğine sahip, Windows Server tabanlı bir HPC Pack kümedeki düğümlerin ayarladığınızda, MPI uygulamaları düşük gecikme, doğrudan uzak bellek erişimi (RDMA) teknolojisine dayalı azure'da yüksek verimlilik ağ üzerinden verimli bir şekilde iletişim kurar.

Linux sanal makineleri bu erişim hello Azure RDMA ağ üzerinde toorun MPI iş yükleri istiyorsanız, bkz: [Linux RDMA küme toorun MPI uygulamalar ayarlamak](../../linux/classic/rdma-cluster.md).

## <a name="hpc-pack-cluster-deployment-options"></a>HPC Pack küme dağıtım seçenekleri
Microsoft HPC Pack bir hiçbir ek maliyet toocreate şirket içi HPC kümelerinde sağlanan veya Azure toorun Windows veya Linux HPC uygulamalarında aracıdır. HPC Pack Merhaba ileti geçirme arabirimi for Windows (MS-MPI) hello Microsoft uygulaması için bir çalışma zamanı ortamı içerir. Desteklenen bir Windows Server işletim sistemi çalıştıran RDMA özellikli örnekleriyle birlikte kullanıldığında, HPC paketi bu erişim hello Azure RDMA ağ verimli seçeneği toorun Windows MPI uygulamaları sağlar. 

Bu makalede iki senaryo sunar ve Microsoft HPC paketi ile Windows RDMA kümesi toodetailed Kılavuzu tooset bağlar. 

* Senaryo 1. İşlem yoğunluklu çalışan rolü örnekleri (PaaS) dağıtma
* Senaryo 2. İşlem yoğunluklu VM'ler (Iaas) hesaplama düğümlerini dağıtmak

Genel Önkoşullar toouse işlem yoğunluklu örnekler için Windows ile bkz: [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="scenario-1-deploy-compute-intensive-worker-role-instances-paas"></a>Senaryo 1: işlem yoğunluklu çalışan rolü örnekleri (PaaS) dağıtma
Mevcut bir HPC Pack kümeden ek işlem kaynaklarında bir bulut hizmeti (PaaS) çalışan Azure çalışan rolü örnekleri (Azure düğümleri) ekleyin. HPC paketi, "veri bloğu tooAzure" olarak da adlandırılan bu özellik, bir dizi boyutları hello çalışan rolü örnekleri için destekler. Azure düğümleri ekleme hello olduğunda hello RDMA özellikli boyutlarından birini belirtin.

Mevcut bir kümeden değerlendirmeler ve adımlar tooburst tooRDMA özellikli Azure örnekleri aşağıda verilmiştir (genellikle şirket içi) küme. Bir Azure VM dağıtılan benzer yordamları tooadd çalışan rolü örnekleri tooan HPC paketi üstbilgi düğümü kullanın.

> [!NOTE]
> HPC paketi ile bir öğretici tooburst tooAzure için bkz: [HPC paketi ile karma küme ayarlama](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Özellikle tooRDMA özellikli Azure düğümlerini uygulayabileceğiniz adımların hello Hello konuları unutmayın.
> 
> 

![TooAzure veri bloğu][burst]

### <a name="steps"></a>Adımlar
1. **HPC Pack 2012 R2 baş düğüm yapılandırmak ve dağıtmak**
   
    Hello Hello son HPC Pack yükleme paketini indirme [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922). Bir Azure veri bloğu dağıtım için gereksinimleri ve yönergeleri tooprepare için bkz: [tooAzure çalışan örnekleri Microsoft HPC paketi ile veri bloğu](https://technet.microsoft.com/library/gg481749.aspx).
2. **Bir yönetim sertifikası hello Azure aboneliği yapılandırma**
   
    Merhaba baş düğüm ve Azure arasında bir sertifika toosecure hello bağlantı yapılandırın. Seçenekler ve yordamlar için bkz: [senaryoları tooConfigure hello HPC paketi için Azure yönetim sertifikası](http://technet.microsoft.com/library/gg481759.aspx). Test dağıtımları için HPC Pack bir varsayılan Microsoft HPC Azure Yönetimi tooyour Azure aboneliği hızlı bir şekilde yükleyebilirsiniz sertifikası yükler.
3. **Yeni bir bulut hizmeti ve bir depolama hesabı oluştur**
   
    Hello Azure portal toocreate hello RDMA özellikli örnekleri kullanılabildiği bir bölgede hello dağıtımı için bir bulut hizmeti ve bir depolama hesabı kullanın.
4. **Bir Azure düğüm şablonu oluşturma**
   
    HPC Küme Yöneticisi'nde Hello oluşturma düğüm Şablonu Sihirbazı'nı kullanın. Adımlar için bkz: [Azure düğüm şablonu oluşturma](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Templ) "Adımları tooDeploy Microsoft HPC paketi ile Azure düğümleri" içinde.
   
    İlk sınamalar için el ile kullanılabilirlik İlkesi hello şablonunda yapılandırma öneririz.
5. **Toohello küme düğümleri Ekle**
   
    HPC Küme Yöneticisi'nde Hello düğümü Ekleme Sihirbazı kullanın. Daha fazla bilgi için bkz: [Azure düğümleri Ekle toohello Windows HPC Kümesi](http://technet.microsoft.com/library/gg481758.aspx#BKMK_Add).
   
    Merhaba düğümleri Hello boyutunu belirtirken, hello RDMA özellikli örneği boyutlarından birini seçin.
   
   > [!NOTE]
   > Merhaba işlem yoğunluklu örnekler olan her veri bloğu tooAzure dağıtımında, HPC Pack en az iki RDMA özellikli örneği (örneğin, A8) proxy düğümleri olarak otomatik olarak dağıtır., ayrıca toohello Azure çalışan rolü örnekleri, belirtin. Merhaba proxy düğümleri toohello abonelik ayrılır ve ücretleri hello Azure çalışan rolü örnekleri yanı sıra çekirdeğe kullanın.
   > 
   > 
6. **(Sağlayamaz) hello düğümleri başlatın ve çevrimiçi toorun işleri Getir**
   
    Merhaba düğümleri seçin ve hello kullan **Başlat** eylem HPC Küme Yöneticisi'nde. Sağlama tamamlandıktan sonra hello düğümleri seçip hello kullanabileceğiniz **çevrimiçine** eylem HPC Küme Yöneticisi'nde. Merhaba düğümler hazır toorun işleri ' dir.
7. **İşlerini toohello küme gönderme**
   
   HPC Pack iş gönderme araçları toorun küme işlerini kullanın. Bkz: [Microsoft HPC paketi: iş yönetimi](http://technet.microsoft.com/library/jj899585.aspx).
8. **(Deprovision) hello düğümler durdurun**
   
   Çalışan işleri bittiğinde hello düğümleri çevrimdışı duruma getirin ve hello kullan **durdurmak** eylem HPC Küme Yöneticisi'nde.

## <a name="scenario-2-deploy-compute-nodes-in-compute-intensive-vms-iaas"></a>Senaryo 2: Dağıtmak işlem düğümleri işlem yoğunluklu VM'ler (Iaas) olarak
Bu senaryoda, hello HPC paketi üstbilgi düğümü ve küme işlem düğümlerinde sanal makineleri bir Azure sanal ağında dağıtın. HPC Pack sağlayan birkaç [dağıtım seçenekleri Azure VM'de](../../linux/hpcpack-cluster-options.md)otomatik dağıtım betikleri ve Azure hızlı başlangıç şablonlarını dahil olmak üzere. Örnek olarak, konuları hello ve adımları toouse hello kılavuzuna [HPC Pack Iaas dağıtım betiği](hpcpack-cluster-powershell-script.md) Azure HPC Pack 2012 R2 kümesinde hello dağıtımını otomatik hale getirmek için.

![Azure sanal makineleri kümedeki][iaas]

### <a name="steps"></a>Adımlar
1. **Bir küme baş düğümüne oluşturmak ve bir istemci bilgisayarda hello HPC Pack Iaas dağıtım betiği çalıştırarak düğümü VM'ler işlem**
   
    Hello Hello HPC Pack Iaas dağıtım betiği paketini indirin [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49922).
   
    tooprepare hello istemci bilgisayar, hello betiği yapılandırma ve çalıştırma hello betik oluşturmak, bkz: [hello HPC Pack Iaas dağıtım betiği ile bir HPC kümesi oluşturma](hpcpack-cluster-powershell-script.md). 
   
    RDMA özellikli toodeploy işlem düğümleri, ek hususlar aşağıdaki Not hello:
   
   * **Sanal ağ**: hangi hello RDMA özellikli örnek boyutu içinde bir bölgede istediğiniz toouse kullanılabilir yeni bir sanal ağ belirtin.
   * **Windows Server işletim sisteminin**: toosupport RDMA bağlantısı hello işlem düğümü VM'ler için bir Windows Server 2012 R2 veya Windows Server 2012 işletim sistemi belirtin.
   * **Bulut Hizmetleri**: baş düğümünüz bir bulut hizmeti ve işlem düğümleriniz farklı bir bulut hizmeti dağıtma öneririz.
   * **Baş düğüm boyutu**: Bu senaryo için boyutu en az göz önünde bulundurun A4 (çok büyük) hello baş düğüm için.
   * **HpcVmDrivers uzantısı**: hello dağıtım betiği yükler hello Azure VM aracısı ve hello HpcVmDrivers uzantısı otomatik olarak bir Windows Server işletim sistemi ile boyutu A8 veya A9 işlem düğümleri dağıttığınızda. Toohello RDMA ağ bağlanabilmeleri HpcVmDrivers hello işlem düğümünde VM'ler sürücüleri yükler. RDMA özellikli H-serisi Vm'lerinde hello HpcVmDrivers uzantısı el ile yüklemeniz gerekir. Bkz: [yüksek performanslı işlem VM boyutları](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
   * **Küme ağ yapılandırması**: hello dağıtım komut dosyası otomatik olarak ayarlayan hello HPC paketi küme topolojisi 5 (Merhaba kurumsal ağ üzerindeki tüm düğümler). Bu topoloji VM'ler tüm HPC paketi küme dağıtımları için gereklidir. Merhaba küme ağ topolojisi daha sonra değişmez.
2. **Merhaba işlem düğümleri çevrimiçi toorun işleri Getir**
   
    Merhaba düğümleri seçin ve hello kullan **çevrimiçine** eylem HPC Küme Yöneticisi'nde. Merhaba düğümler hazır toorun işleri ' dir.
3. **İşlerini toohello küme gönderme**
   
    Toohello baş düğüm toosubmit işleri bağlanın veya bir şirket içi bilgisayar toodo bunu ayarlayın. Bilgi için bkz: [işleri gönderme tooan HPC küme Azure'da](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
4. **Take hello düğümleri çevrimdışı ve Dur (bunları serbest bırakma)**
   
    Çalışan işleri bittiğinde HPC Küme Yöneticisi'nde hello düğümleri çevrimdışı alın. Daha sonra Azure Yönetim Araçları tooshut kullanın aşağı bunları.

## <a name="run-mpi-applications-on-hello-cluster"></a>Merhaba kümede MPI uygulamaları çalıştırma
### <a name="example-run-mpipingpong-on-an-hpc-pack-cluster"></a>Örnek: mpipingpong bir HPC Pack kümede çalıştırın.
tooverify Çalıştır hello RDMA özellikli örneklerinin bir HPC Pack dağıtımı HPC Pack Merhaba **mpipingpong** hello kümede komutu. **mpipingpong** eşleştirilmiş düğümler arasında veri paketleri art arda toocalculate gecikme süresi ve verimlilik ölçümleri gönderir ve hello uygulama RDMA özellikli ağ istatistikleri. Bu örnek, bir MPI işini çalıştırmak için tipik bir düzen gösterir (Bu durumda, **mpipingpong**) hello kümesi kullanarak **mpiexec** komutu.

Bu örnekte "tooAzure veri bloğu" bir yapılandırmada Azure düğümleri eklenen varsayılır ([Senaryo 1](#scenario-1.-deploy-compute-intensive-worker-role-instances-\(PaaS\) in this article). HPC Pack Azure Vm'leri bir kümede dağıtılmışsa, toomodify hello komut sözdizimi toospecify farklı bir düğüme Grup gerekir ve ek ortam değişkenleri toodirect ağ trafiği toohello RDMA ağ ayarlayın.

Merhaba kümede toorun mpipingpong:

1. Merhaba baş düğüm veya düzgün yapılandırılmış istemci bilgisayarda, bir komut istemi açın.
2. bir Azure veri bloğu dağıtım türü hello komutu toosubmit küçük paket boyutu ve fazla yineleme iş toorun mpipingpong aşağıdaki dört düğümlerinin düğüm çifti arasındaki tooestimate gecikme süresi:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 1:100000 -op -s nul
    ```
   
    Merhaba komutu gönderildiğinde hello işin hello kimliği döndürür.
   
    Azure Vm'lerinde dağıtılan hello HPC paketi küme dağıttıysanız içeren bir düğüm grubu işlem düğümü VM'ler tek bulut hizmet'te belirtin ve hello değiştirme **mpiexec** gibi komut:
   
    ```Command
    job submit /nodegroup:vmcomputenodes /numnodes:4 mpiexec -c 1 -affinity -env MSMPI_DISABLE_SOCK 1 -env MSMPI_PRECONNECT all -env MPICH_NETMASK 172.16.0.0/255.255.0.0 mpipingpong -p 1:100000 -op -s nul
    ```
3. Merhaba işi tamamlandığında tooview hello (Bu durumda, görev 1 hello işin hello çıktısını), aşağıdaki türü hello çıktı.
   
    ```Command
    task view <JobID>.1
    ```
   
    Burada &lt; *JobId* &gt; gönderilen hello iş hello kimliğidir.
   
    Merhaba çıkış gecikme süresi sonuçları benzer toohello aşağıdakileri içerir.
   
    ![Ping pong gecikme süresi][pingpong1]
4. tooestimate verimlilik Azure çiftleri arasındaki veri bloğu düğümleri, türü hello şu komutu toosubmit iş toorun **mpipingpong** büyük paket boyutu ve birkaç yinelemeleri ile:
   
    ```Command
    job submit /nodegroup:azurenodes /numnodes:4 mpiexec -c 1 -affinity mpipingpong -p 4000000:1000 -op -s nul
    ```
   
    Merhaba komutu gönderildiğinde hello işin hello kimliği döndürür.
   
    Azure Vm'lerinde dağıtılan bir HPC Pack kümede 2. adımda not ettiğiniz gibi hello komutu değiştirin.
5. Merhaba işi tamamlandığında tooview hello (Bu durumda, görev 1 hello işin hello çıktısını), aşağıdaki türü hello çıktı:
   
    ```Command
    task view <JobID>.1
    ```
   
   Merhaba çıkış üretilen iş sonuçları benzer toohello aşağıdakileri içerir.
   
   ![Ping pong işleme][pingpong2]

### <a name="mpi-application-considerations"></a>MPI uygulama konuları
HPC Pack Azure MPI uygulamaları çalıştırmak için dikkat edilecek noktalar aşağıda verilmiştir. Bazı yalnızca toodeployments Azure düğümleri (çalışan rolü örnekleri "veri bloğu tooAzure" yapılandırmasında eklenen) uygulanır.

* Bir bulut hizmetinde çalışan rolü örnekleri düzenli aralıklarla bildirilmeksizin Azure tarafından (örneğin, Sistem Bakımı veya örneği başarısız durumda) sağlama. Bir MPI iş çalışırken örneği sağlama, hello örneği verilerini kaybeder ve, hello MPI iş toofail neden dağıtılmayan başlandığı ilk toohello durumu döndürür. Hello için tek bir MPI işi kullanan ve hello daha fazla düğüm artık hello işi çalıştırır, bir iş çalışırken hello örnekleri birini sağlama, büyük olasılıkla hello. Ayrıca tek bir düğüm hello dağıtımda dosya sunucusu olarak belirtirseniz bu düşünün.
* toorun MPI işlerini Azure toouse hello RDMA özellikli örnekleri yok. HPC paketi tarafından desteklenen herhangi bir örnek boyutu kullanabilirsiniz. Ancak, RDMA özellikli örnekleri hello hassas toohello gecikme süresi ve hello düğümlerini bağlayan hello ağ bant genişliği hello görece büyük ölçekli MPI işlerini çalıştırmak için önerilir. Diğer boyutları toorun gecikme süresi ve bant genişliği duyarlı MPI işlerini kullanırsanız, tek bir görev yalnızca birkaç düğüm üzerinde çalışır, küçük bir iş çalışmadığı öneririz.
* Dağıtılan uygulamalar tooAzure hello uygulama ile ilişkili lisans konu toohello örnekleridir. Lisans için ticari uygulamaları veya diğer kısıtlamaları hello bulutta çalıştırmak için hello üreticisine danışın. Satıcıların tümü kullandıkça öde lisansı sunmaz.
* Azure örnekleri, daha fazla tooaccess şirket içi düğümleri, paylaşımları ve lisans sunucuları kurmaktır. Örneğin, tooenable hello Azure düğümleri tooaccess bir şirket içi lisans sunucusuna bir siteden siteye Azure sanal ağı yapılandırabilirsiniz.
* Azure örnekleri üzerinde toorun MPI uygulamaları kaydetmek her MPI uygulama Özellikli Windows Güvenlik Duvarı hello örneklerinde hello çalıştırarak **hpcfwutil** komutu. Bu MPI iletişimleri tootake yer hello güvenlik duvarı tarafından dinamik olarak atanan bir bağlantı noktası sağlar.
  
  > [!NOTE]
  > Veri bloğu tooAzure dağıtımları için aynı zamanda bir güvenlik duvarı özel durum komutu toorun otomatik olarak tooyour küme eklenen tüm yeni Azure düğümlerine yapılandırabilirsiniz. Merhaba çalıştırdıktan sonra **hpcfwutil** komut ve, uygulama works hello tooa başlangıç komut Azure düğümleri için ekleme doğrulayın. Daha fazla bilgi için bkz: [Azure düğümleri için bir başlangıç komut dosyası kullanma](https://technet.microsoft.com/library/jj899632.aspx).
  > 
  > 
* HPC Pack Merhaba CCP_MPI_NETMASK küme ortam değişkeni toospecify kabul edilebilir adres aralığını MPI iletişimi için kullanır. HPC Pack 2012 R2'de başlayarak, hello CCP_MPI_NETMASK küme ortam değişkeni, yalnızca etki alanına katılmış küme bilgi işlem düğümleri arasındaki MPI iletişimi etkiler (ya da şirket içi veya Azure VM'de). Merhaba değişken bir veri bloğu tooAzure yapılandırmasında eklenen düğümler tarafından göz ardı edilir.
* MPI işlerini farklı bulut Hizmetleri (örneğin, farklı bir düğüme şablonları ya da birden çok bulut Hizmetleri'nde dağıtılan Azure VM işlem düğümleri veri bloğu tooAzure dağıtımlar) dağıtılan Azure örnekleri üzerinde çalıştırılamaz. Farklı bir düğüme şablonlarla çalışmaya birden çok Azure düğümlü dağıtımlar varsa, hello MPI işi yalnızca bir Azure düğümleri kümesi üzerinde çalıştırmanız gerekir.
* Ne zaman Azure düğümleri tooyour küme ekleyin ve bunları hemen çevrimiçi hello HPC İş Zamanlayıcısı hizmeti Getir toostart işleri hello düğümlerde çalışır. Yalnızca İş yükünüzün bir kısmını Azure üzerinde çalıştırabilir, güncelleştirmek veya iş şablonları toodefine türleri Azure üzerinde çalıştırabilirsiniz hangi işi oluşturma emin olun. Örneğin, yalnızca Azure düğümlerinde çalıştırmak bir proje şablonu ile gönderilen işler hello düğüm grupları özelliği toohello iş şablonuna ekleyin ve AzureNodes hello seçin tooensure değeri gerekiyor. toocreate özel grupları, Azure düğümleri için hello Ekle HpcGroup HPC PowerShell cmdlet'ini kullanın.

## <a name="next-steps"></a>Sonraki adımlar
* Bir alternatif toousing HPC Pack, hello Azure Batch hizmeti toorun ile yönetilen Azure işlem düğümleri havuzlarının MPI uygulamaları geliştirin. Bkz: [kullanımı çok örnekli görevler toorun ileti geçirme arabirimi (MPI) Azure Batch uygulamalarda](../../../batch/batch-mpi.md).
* Toorun Linux MPI istiyorsanız, bkz: hello Azure RDMA ağ erişim uygulamaları [Linux RDMA küme toorun MPI uygulamalar ayarlamak](../../linux/classic/rdma-cluster.md).

<!--Image references-->
[burst]:media/hpcpack-rdma-cluster/burst.png
[iaas]:media/hpcpack-rdma-cluster/iaas.png
[pingpong1]:media/hpcpack-rdma-cluster/pingpong1.png
[pingpong2]:media/hpcpack-rdma-cluster/pingpong2.png
