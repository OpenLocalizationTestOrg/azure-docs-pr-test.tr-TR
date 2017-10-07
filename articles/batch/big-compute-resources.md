---
title: "batch ve HPC için aaaResources hello Azure bulut içinde | Microsoft Docs"
description: "Büyük ölçekli paralel, toplu işlem ve yüksek performanslı bilgi işlem (HPC), azure'da iş yüklerini çalıştırmak teknik kaynaklar toohelp listeler."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: ab8ba24678bd7ec090306b501d29ca63c4fb83ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Azure'da Big Compute: toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar
Azure'da büyük ölçekli paralel, toplu işlem ve yüksek performanslı bilgi işlem (HPC) iş yükleri çalıştırmak kılavuzunu tootechnical kaynakları toohelp budur. Var olan toplu veya HPC iş yükleri toohello Azure bulut genişletmek veya bir aralığı, Azure hizmetlerini kullanarak yeni Big Compute çözümleri oluşturabilirsiniz.

## <a name="solutions-options"></a>Çözümler seçenekleri
Azure Big Compute seçenekler hakkında bilgi edinin ve iş yükü ve iş gereğiniz için doğru yaklaşım hello seçin.

* [Batch ve HPC çözümleri](batch-hpc-solutions.md)
* [Video: Azure ve HPC hello bulutta Big Compute](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Toplu](https://azure.microsoft.com/services/batch/) kolay toocloud etkinleştir kolaylaştıran bir Linux ve Windows uygulamaları ve ayarlama ve yönetimini bir küme ve iş Zamanlayıcı olmadan çalıştırma işleri platformdur. Merhaba SDK toointegrate istemci uygulamaları ile Azure Batch çeşitli diller, aşama veri tooAzure kullanın ve iş yürütme işlem hatları oluşturabilir.

* [Belgeleri](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), ve [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API Başvurusu
* [Batch yönetimi .NET kitaplığı](https://msdn.microsoft.com/library/mt463120.aspx) başvurusu
* Öğreticiler: kullanmaya başlama [.NET için Azure Batch kitaplığını](batch-dotnet-get-started.md) ve [Batch Python istemcisini](batch-python-tutorial.md)
* [Toplu işlem Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Toplu videolar](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>HPC küme çözümleri
Dağıtabilir veya işlem yoğun iş yükleri, var olan Windows veya Linux HPC küme tooAzure toorun genişletir.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC paketi
HPC Pack Microsoft Azure ve Windows Server teknolojileri üzerinde Windows ve Linux HPC iş yükleri çalıştırabilen yerleşik Microsoft'un ücretsiz HPC çözümüdür.  

* [HPC Pack 2016 indirin](https://www.microsoft.com/download/details.aspx?id=54507)
* [HPC Pack 2012 R2 güncelleştirme 3 indirin](https://www.microsoft.com/download/details.aspx?id=49922)
* [Belgeleri](https://technet.microsoft.com/library/jj899572.aspx)
* HPC Pack küme seçenekleri azure'da: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [HPC Pack ile tooAzure çalışan örnekleri veri bloğu](https://technet.microsoft.com/library/gg481749.aspx)
* [TooAzure HPC paketi ile toplu veri bloğu](https://technet.microsoft.com/library/mt612877.aspx)
* [Windows HPC forumları](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Linux ve OSS küme çözümleri
Linux HPC kümelerinde bu Azure şablonları toodeploy kullanın.

* [Döndürme SLURM küme](https://azure.microsoft.com/documentation/templates/slurm/) ve [blog gönderisi](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Torque küme Döndür](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Kılavuz şablonları ile PBS Professional işlem](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>HPC depolama
* [Azure üzerinde HPC depolama için paralel dosya sistemleri](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Lustre yazılım - Eval için Intel bulut Edition](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [CentOS 7.2 şablonundaki BeeGFS](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) olan hello ileti geçirme arabirimi geliştirmek ve hello Windows platformunda çalışan paralel uygulamalar için standart Microsoft uygulamasıdır.

* [MS-MPI indirin](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [MS-MPI başvurusu](https://msdn.microsoft.com/library/dn473458.aspx)
* [MPI Forumu](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Yoğun işlem gücü kullanımlı örnekler
Azure teklifleri bir [aralığı, VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)dahil [işlem yoğunluklu H-serisi](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) örnekleri Linux ve Windows HPC iş yükleri tooa arka uç RDMA ağ toorun bağlanıp bağlanamayacağını. 

* [Bir Linux RDMA küme toorun MPI uygulama ayarlama](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Microsoft HPC Pack toorun MPI uygulamaları ile Windows RDMA kümesi ayarlama](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

GPU kullanımı yoğun iş yükleri için kullanıma [NC ve NV boyutları](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Örnekler ve gösterileri
* [Azure Batch C# ve Python kod örnekleri](https://github.com/Azure/azure-batch-samples)
* [Toplu Shipyard](https://azure.github.io/batch-shipyard/) toplu stili Dockerized iş yükleri tooAzure toplu kolay dağıtımı için araç seti
* [doAzureParallel](http://www.github.com/Azure/doAzureParallel) Azure Batch üstünde oluşturulmuş R paketi
* [SUSE Linux Enterprise Server HPC için sınayın](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>İlgili Azure Hizmetleri
* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/)
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [Hdınsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Sanal Makineler](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Sanal Makine Ölçek Kümeleri](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/)
* [App Service](https://azure.microsoft.com/documentation/services/app-service/)
* [Media Services](https://azure.microsoft.com/documentation/services/media-services/)
* [İşlevler](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Mimari şemalar
* [Azure Batch ve Azure Data Factory kullanarak HPC ve veriler orchestration](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) ve [makale](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Endüstri çözümleri
* [Banka ve büyük harf pazarda](https://finance.azure.com/)
* [Mühendislik benzetimleri](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Müşteri hikayeleri
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3vıew](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Ludwig Institute of Kanseri araştırma](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ senedi uluslararası](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba Hello son Duyurular için bkz: [Microsoft HPC ve Batch ekip blogu](http://blogs.technet.com/b/windowshpc/) ve hello [Azure blogu](https://azure.microsoft.com/blog/tag/hpc/).
* Ayrıca bkz. [toplu işlemde yenilikler](https://azure.microsoft.com/updates/?service=batch) veya toohello abone [RSS akışı](https://azure.microsoft.com/updates/feed/?service=batch).

