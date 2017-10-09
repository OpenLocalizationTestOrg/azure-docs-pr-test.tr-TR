---
title: "aaaUse işlem yoğunluklu toplu olan Azure VM'ler | Microsoft Docs"
description: "Azure Batch havuzlarında nasıl tootake avantajı RDMA özellikli GPU etkinleştirilmiş veya VM boyutları"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Batch havuzları, RDMA özellikli GPU etkinleştirilmiş veya örnekleri kullanın

toorun belirli toplu işlerin büyük ölçekli hesaplama için tasarlanmış Azure VM boyutlarını tootake avantajlarından isteyebilirsiniz. Örneğin, toorun çok örnekli [MPI iş yükleri](batch-mpi.md), A8, A9, seçebilir veya bir ağ sahip H-serisi boyutları arabirim uzaktan doğrudan bellek erişimi (RDMA için). Bu boyutlar MPI uygulamaları hızlandırabilir düğümler arası iletişim için tooan InfiniBand ağına bağlayın. Veya CUDA uygulamalar için NVIDIA Tesla grafik işlem birimi (GPU) kartları dahil N-serisi boyutları seçebilirsiniz.

Bu makale Azure Batch havuzlarında özel boyutları bazıları yönergeler ve örnekler toouse sağlar. Belirtimlerin ve arka plan için bkz:

* Yüksek performanslı işlem VM boyutları ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)) 

* GPU etkin VM boyutları ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)) 


## <a name="subscription-and-account-limits"></a>Aboneliği ve hesabı sınırları

* **Kotalar** -bir veya daha fazla Azure kotaları hello numarası veya türü sınırlayabilir düğümlerinin tooa Batch havuzu ekleyebilirsiniz. RDMA özellikli GPU özellikli seçtiğinizde sınırlı büyük olasılıkla toobe veya diğer çok çekirdekli VM boyutları var. Oluşturduğunuz toplu işlem hesabı Hello türüne bağlı olarak, toohello hesabının kendisi veya tooyour abonelik hello kotaları uygulayabilirsiniz.

    * Hello Batch hesabı oluşturduysanız **Batch hizmeti** yapılandırması tarafından hello sınırlıdır [toplu işlem hesabı başına ayrılmış çekirdek kotası](batch-quota-limit.md#resource-quotas). Varsayılan olarak, bu kota 20 çekirdek ' dir. Ayrı bir kota çok uygulanır[düşük öncelikli sanal makineleri](batch-low-pri-vms.md), bunları kullanın. 

    * Hello hello hesabı oluşturduysanız **kullanıcı aboneliği** yapılandırma, aboneliğinizi hello bölge başına VM çekirdek sayısını sınırlar. Bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md). Aboneliğinizi HPC ve GPU örnekleri dahil olmak üzere bir bölgesel kota toocertain VM boyutları için de geçerlidir. Merhaba kullanıcı abonelik yapılandırmasında toohello toplu işlem hesabı hiçbir ek kotalar uygulanır. 

  Özelleştirilmiş bir VM boyutu toplu işlemde kullanırken bir veya daha fazla kotaları tooincrease gerekebilir. toorequest kota artışı, açık bir [çevrimiçi müşteri destek isteği](../azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz.

* **Bölge kullanılabilirliği** - işlem yoğunluklu VM'ler olabilir kullanılabilir, Batch hesabınızı oluşturduğunuz hello bölgelerde. bir boyut kullanılabilir olduğunu toocheck bkz [bölgeye göre ürünleri](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Bağımlılıklar

Merhaba RDMA ve işlem yoğunluklu boyutları GPU özelliklerini yalnızca belirli işletim sistemlerinde desteklenir. İşletim sistemine bağlı olarak ek sürücü veya diğer yazılım yapılandırın veya tooinstall ihtiyacınız olabilir. Aşağıdaki tablolar hello Bu bağımlılıklar özetler. Ayrıntılar için bağlantılı makalelerine bakın. Seçenekler tooconfigure Batch havuzları için bu makalenin sonraki bölümlerinde bkz.


### <a name="linux-pools---virtual-machine-configuration"></a>Linux havuzları - sanal makine yapılandırması

| Boyut | Özellik | İşletim sistemleri | Gerekli yazılım | Havuzu ayarları |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | SUSE Linux Enterprise Server 12 HPC veya<br/>CentOS tabanlı HPC<br/>(Azure Market) | Intel MPI 5 | Düğümler arası iletişimi etkinleştirmek, eşzamanlı görev yürütme devre dışı bırakma |
| [NC serisi *](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | NVIDIA Tesla K80 GPU | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3, veya<br/>CentOS tabanlı 7.3<br/>(Azure Market) | NVIDIA CUDA Araç Seti 8.0 sürücüleri | Yok | 
| [NV serisi](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | NVIDIA Tesla M60 GPU | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>CentOS tabanlı 7.3<br/>(Azure Market) | NVIDIA Kılavuz 4.3 sürücüleri | Yok |

* RDMA bağlantısı NC24r vm'lerde CentOS tabanlı 7.3 HPC Intel MPI ile desteklenir.



### <a name="windows-pools---virtual-machine-configuration"></a>Windows havuzları - sanal makine yapılandırması

| Boyut | Özellik | İşletim sistemleri | Gerekli yazılım | Havuzu ayarları |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 veya<br/>Windows Server 2012 (Azure Market) | Microsoft MPI 2012 R2 veya sonraki bir sürümü veya<br/> Intel MPI 5<br/><br/>HpcVMDrivers Azure VM uzantısı | Düğümler arası iletişimi etkinleştirmek, eşzamanlı görev yürütme devre dışı bırakma |
| [NC serisi *](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla K80 GPU | Windows Server 2016 veya <br/>Windows Server 2012 R2 (Azure Market) | NVIDIA Tesla sürücüleri veya CUDA Araç Seti 8.0 sürücülerini| Yok | 
| [NV serisi](../virtual-machines/windows/n-series-driver-setup.md) | NVIDIA Tesla M60 GPU | Windows Server 2016 veya<br/>Windows Server 2012 R2 (Azure Market) | NVIDIA Kılavuz 4.3 sürücüleri | Yok |

* RDMA bağlantısı NC24r vm'lerde HpcVMDrivers uzantısı ve Microsoft MPI veya Intel MPI ile Windows Server 2012 R2'de desteklenir.

### <a name="windows-pools---cloud-services-configuration"></a>Windows havuzları - Cloud services yapılandırması

> [!NOTE]
> N-serisi boyutları hello cloud services yapılandırması ile Batch havuzlarında desteklenmez.
>

| Boyut | Özellik | İşletim sistemleri | Gerekli yazılım | Havuzu ayarları |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2<br/>Windows Server 2012 veya<br/>Windows Server 2008 R2 (konuk işletim sistemi ailesi) | Microsoft MPI 2012 R2 veya sonraki bir sürümü veya<br/>Intel MPI 5<br/><br/>HpcVMDrivers Azure VM uzantısı | Düğümler arası iletişimi etkinleştirmek,<br/> eşzamanlı görev yürütme devre dışı bırak |





## <a name="pool-configuration-options"></a>Havuz yapılandırma seçenekleri

tooconfigure Batch havuzu, hello Batch API'lerini ve araçları için özelleştirilmiş bir VM boyutu birkaç seçenekleri tooinstall gerekli yazılım veya sürücüler dahil olmak üzere, sağlayın:

* [Başlangıç görevi](batch-api-basics.md#start-task) -kaynak dosya tooan hello Azure depolama hesabında farklı bir yükleme paketi karşıya hello toplu işlem hesabı ile aynı bölgeye. Hello havuzu başlatıldığında başlangıç görevi komut satırı tooinstall hello kaynak dosyası sessizce oluşturun. Daha fazla bilgi için bkz: Merhaba [REST API belgeleri](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > Merhaba başlangıç görevi yükseltilmiş (Yönetici) izinleriyle çalıştırılmalıdır ve başarı için beklemeniz gerekir.
  >

* [Uygulama paketi](batch-application-packages.md) - sıkıştırılmış yükleme paketini tooyour toplu işlem hesabı ekleyin ve bir paket başvuru hello havuzunda yapılandırın. Bu ayar hello paket hello havuzundaki tüm düğümlerde unzips ve yükler. Hello paket bir yükleyici ise, tüm havuzu düğümler üzerinde bir başlangıç görevi komut satırı toosilently yükleme hello uygulaması oluşturursunuz. İsteğe bağlı olarak, bir görev bir düğüm üzerinde zamanlanmış toorun olduğunda hello paketini yükleyin.

* [Özel havuzu görüntü](batch-api-basics.md#pool) - özel Windows oluşturma veya sürücüleri, yazılım veya diğer ayarları içeren bir Linux VM görüntüsü gerekli Merhaba VM boyutu. Batch hesabınıza hello kullanıcı abonelik Yapılandırması'nda oluşturulan hello özel görüntü toplu havuzunuz için belirtin. (Özel görüntüleri hello toplu hizmet yapılandırmasında hesaplarındaki desteklenmez.) Özel resimler yalnızca hello sanal makine yapılandırması havuzları ile kullanılabilir.

  > [!IMPORTANT]
  > Batch havuzlarında yönetilen diskleri veya Premium depolama ile oluşturulan özel bir görüntü şu anda kullanamazsınız.
  >



* [Toplu Shipyard](https://github.com/Azure/batch-shipyard) otomatik olarak hello GPU ve RDMA toowork saydam Azure batch kapsayıcılı iş yükleri ile yapılandırır. Toplu Shipyard tamamen yapılandırma dosyaları ile yönetilir. GPU ve RDMA iş yükleri gibi hello sağlayan birçok örnek tarif yapılandırmaları kullanılabilir vardır [CNTK GPU tarif](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) N-serisi vm'lerde GPU sürücüleri önceden yapılandırır ve Microsoft Bilişsel Araç Seti yazılım Docker görüntü olarak yükler.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Örnek: Microsoft MPI A8 VM havuzunda

toorun Windows MPI uygulamaları Azure A8 düğümlerinin havuzunda tooinstall desteklenen MPI uygulanması gerekir. Örnek adımları tooinstall işte [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) Windows havuz Batch uygulama paketini kullanarak.

1. Merhaba karşıdan [Kurulum paketini](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) Microsoft MPI en son sürümünü hello için.
2. Merhaba paketi zip dosyası oluşturun.
3. Merhaba paket tooyour toplu işlem hesabı karşıya yükleyin. Merhaba adımları için bkz [uygulama paketleri](batch-application-packages.md) Kılavuzu. Bir uygulama kimliği gibi belirtin *MSMPI*ve sürüm gibi *8.1*. 
4. Merhaba Batch API'leri veya Azure portal kullanarak, düğümleri ve ölçek istenen hello numarasıyla hello bulut Hizmetleri Yapılandırması'nda bir havuzu oluşturun. Merhaba aşağıdaki tabloda örnek ayarları tooset MPI oluşturan bir başlangıç görevi kullanarak katılımsız modda gösterilmektedir:

| Ayar | Değer |
| ---- | ----- | 
| **Görüntü türü** | Cloud Services |
| **İşletim sistemi ailesi** | Windows Server 2012 R2 (işletim sistemi ailesi 4) |
| **Düğüm boyutu** | A8 standart |
| **Düğümler arası iletişim etkinleştirildi** | True |
| **Düğüm başına en fazla görev** | 1 |
| **Uygulama paketi başvuruları** | MSMPI |
| **Etkin başlangıç görevi** | True<br>**Komut satırı** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Kullanıcı Kimliği** -havuzu autouser, yönetici<br/>**Başarı için bekleyin** - True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Örnek: NVIDIA Tesla sürücüleri NC VM havuzu

toorun CUDA uygulamaları Linux NC düğümlerinin havuzunda tooinstall CUDA Araç Seti 8.0 hello düğümlerde gerekir. Merhaba Araç Seti hello gerekli NVIDIA Tesla GPU sürücüleri yükler. Örnek adımları toodeploy hello GPU sürücüleri ile özel bir Ubuntu 16.04 LTS görüntü şunlardır:

1. Bir Azure NC6 Ubuntu 16.04 LTS çalıştıran VM dağıtın. Örneğin, hello VM hello BİZE Güney merkez bölgede oluşturun. Standart depolama ile Merhaba VM oluşturduğunuzdan emin olun ve *olmadan* yönetilen diskler.
2. Merhaba adımları tooconnect toohello VM izleyin ve [CUDA sürücülerini yüklemek](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Merhaba Linux Aracısı yetkisini kaldırma ve ardından hello Azure CLI 1.0 komutları kullanarak Linux VM görüntüsünü yakalayın. Adımlar için bkz: [Azure üzerinde çalışan Linux sanal makine yakalama](../virtual-machines/linux/capture-image-nodejs.md). Merhaba görüntü URI not edin.
  > [!IMPORTANT]
  > Azure CLI 2.0 komutları toocapture hello görüntüsü için Azure Batch kullanmayın. Şu anda hello CLI 2.0 komutlar, yalnızca yönetilen diskleri kullanılarak oluşturulan sanal makineleri yakalayın.
  >
4. NC sanal makineleri destekleyen bir bölgede hello kullanıcı aboneliği yapılandırması ile bir toplu işlem hesabı oluşturun.
5. Merhaba özel görüntü kullanarak havuz oluşturma ve düğümler ve ölçek sayısı ile Merhaba istenen Hello Batch API'leri veya Azure portal kullanarak. Merhaba aşağıdaki tabloda hello görüntüsü için örnek havuzu ayarları gösterilmektedir:

| Ayar | Değer |
| ---- | ---- |
| **Görüntü türü** | Özel görüntü |
| **Özel görüntü** | Görüntü hello formunun URI`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **Düğüm Aracısı SKU** | Batch.node.ubuntu 16.04 |
| **Düğüm boyutu** | NC6 standart |



## <a name="next-steps"></a>Sonraki adımlar

* bir Azure Batch havuzunda toorun MPI işlerini bkz hello [Windows](batch-mpi.md) veya [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) örnekler.

* Merhaba GPU iş yükleri batch örnekler için bkz [toplu Shipyard](https://github.com/Azure/batch-shipyard/) tarif.
