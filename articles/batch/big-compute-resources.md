---
title: "Batch ve HPC Azure bulut için kaynakları | Microsoft Docs"
description: "Büyük ölçekli paralel, toplu işlem ve yüksek performanslı bilgi işlem (HPC) iş yüklerini azure'da çalıştırdığınızda Yardım için teknik kaynaklar listelenir."
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
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Azure'da Big Compute: toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar
Büyük ölçekli paralel, toplu işlem ve yüksek performanslı bilgi işlem (HPC) iş yükleri Azure'da çalıştırdığınızda Yardım için teknik kaynaklar Kılavuzu budur. Var olan toplu veya HPC iş yüklerinin Azure buluta genişletmek veya bir aralığı, Azure hizmetlerini kullanarak yeni Big Compute çözümleri oluşturabilirsiniz.

## <a name="solutions-options"></a>Çözümler seçenekleri
Azure Big Compute seçenekler hakkında bilgi edinin ve iş yükü ve iş gereğiniz için doğru yaklaşım seçin.

* [Batch ve HPC çözümleri](batch-hpc-solutions.md)
* [Video: Azure ve HPC ile bulutta Big Compute](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Toplu](https://azure.microsoft.com/services/batch/) bulut-Linux ve Windows uygulamaları etkinleştirme ve kurma ve bir küme ve iş Zamanlayıcı yönetme işlerini çalıştırmak kolaylaştıran bir platformdur. İstemci uygulamaları çeşitli diller, Azure, aşama veri aracılığıyla Azure Batch ile tümleştirmek için SDK'yi kullanın ve iş yürütme işlem hatları oluşturabilir.

* [Belgeleri](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), ve [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API Başvurusu
* [Batch yönetimi .NET kitaplığı](https://msdn.microsoft.com/library/mt463120.aspx) başvurusu
* Öğreticiler: kullanmaya başlama [.NET için Azure Batch kitaplığını](batch-dotnet-get-started.md) ve [Batch Python istemcisini](batch-python-tutorial.md)
* [Toplu işlem Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Toplu videolar](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>HPC küme çözümleri
Dağıtma veya var olan Windows veya Linux HPC kümeniz, işlem yoğunluklu iş yüklerini çalıştırmak için Azure'a genişletin.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC paketi
HPC Pack Microsoft Azure ve Windows Server teknolojileri üzerinde Windows ve Linux HPC iş yükleri çalıştırabilen yerleşik Microsoft'un ücretsiz HPC çözümüdür.  

* [HPC Pack 2016 indirin](https://www.microsoft.com/download/details.aspx?id=54507)
* [HPC Pack 2012 R2 güncelleştirme 3 indirin](https://www.microsoft.com/download/details.aspx?id=49922)
* [Belgeleri](https://technet.microsoft.com/library/jj899572.aspx)
* HPC Pack küme seçenekleri azure'da: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [HPC paketi ile Azure çalışan örneklerine veri bloğu](https://technet.microsoft.com/library/gg481749.aspx)
* [HPC paketi ile Azure toplu işlem için veri bloğu](https://technet.microsoft.com/library/mt612877.aspx)
* [Windows HPC forumları](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Linux ve OSS küme çözümleri
Linux HPC Küme dağıtımı için Azure bu şablonları kullanın.

* [Döndürme SLURM küme](https://azure.microsoft.com/documentation/templates/slurm/) ve [blog gönderisi](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Torque küme Döndür](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Kılavuz şablonları ile PBS Professional işlem](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>HPC depolama
* [Azure üzerinde HPC depolama için paralel dosya sistemleri](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Lustre yazılım - Eval için Intel bulut Edition](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [CentOS 7.2 şablonundaki BeeGFS](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>Microsoft MPI
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI), ileti geçirme arabirimi standart geliştirmek ve Windows platformu üzerinde paralel uygulamalarını çalıştırmak için bir Microsoft uygulamasıdır.

* [MS-MPI indirin](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [MS-MPI başvurusu](https://msdn.microsoft.com/library/dn473458.aspx)
* [MPI Forumu](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Yoğun işlem gücü kullanımlı örnekler
Azure teklifleri bir [aralığı, VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)dahil [işlem yoğunluklu H-serisi](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) örnekleri Linux ve Windows HPC iş yüklerini çalıştırmak için bir arka uç RDMA ağa bağlanıp bağlanamayacağını. 

* [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MPI uygulamaları çalıştırmak için Microsoft HPC Pack ile Windows RDMA kümesi ayarlama](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

GPU kullanımı yoğun iş yükleri için kullanıma [NC ve NV boyutları](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Örnekler ve gösterileri
* [Azure Batch C# ve Python kod örnekleri](https://github.com/Azure/azure-batch-samples)
* [Toplu Shipyard](https://azure.github.io/batch-shipyard/) Azure Batch toplu stili Dockerized iş yüklerinin kolay dağıtım için araç seti
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
* Son duyurular için bkz. [Microsoft HPC ve Batch ekip blogu](http://blogs.technet.com/b/windowshpc/) ve [Azure blogu](https://azure.microsoft.com/blog/tag/hpc/).
* Ayrıca bkz. [toplu işlemde yenilikler](https://azure.microsoft.com/updates/?service=batch) veya abone olmak [RSS akışı](https://azure.microsoft.com/updates/feed/?service=batch).

