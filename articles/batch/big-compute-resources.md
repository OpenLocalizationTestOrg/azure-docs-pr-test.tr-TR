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
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="41b73-103">Azure'da Big Compute: toplu işlem ve yüksek performanslı bilgi işlem için teknik kaynaklar</span><span class="sxs-lookup"><span data-stu-id="41b73-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="41b73-104">Büyük ölçekli paralel, toplu işlem ve yüksek performanslı bilgi işlem (HPC) iş yükleri Azure'da çalıştırdığınızda Yardım için teknik kaynaklar Kılavuzu budur.</span><span class="sxs-lookup"><span data-stu-id="41b73-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="41b73-105">Var olan toplu veya HPC iş yüklerinin Azure buluta genişletmek veya bir aralığı, Azure hizmetlerini kullanarak yeni Big Compute çözümleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41b73-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="41b73-106">Çözümler seçenekleri</span><span class="sxs-lookup"><span data-stu-id="41b73-106">Solutions options</span></span>
<span data-ttu-id="41b73-107">Azure Big Compute seçenekler hakkında bilgi edinin ve iş yükü ve iş gereğiniz için doğru yaklaşım seçin.</span><span class="sxs-lookup"><span data-stu-id="41b73-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="41b73-108">Batch ve HPC çözümleri</span><span class="sxs-lookup"><span data-stu-id="41b73-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="41b73-109">Video: Azure ve HPC ile bulutta Big Compute</span><span class="sxs-lookup"><span data-stu-id="41b73-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="41b73-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="41b73-110">Azure Batch</span></span>
<span data-ttu-id="41b73-111">[Toplu](https://azure.microsoft.com/services/batch/) bulut-Linux ve Windows uygulamaları etkinleştirme ve kurma ve bir küme ve iş Zamanlayıcı yönetme işlerini çalıştırmak kolaylaştıran bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="41b73-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="41b73-112">İstemci uygulamaları çeşitli diller, Azure, aşama veri aracılığıyla Azure Batch ile tümleştirmek için SDK'yi kullanın ve iş yürütme işlem hatları oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="41b73-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="41b73-113">Belgeleri</span><span class="sxs-lookup"><span data-stu-id="41b73-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="41b73-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), ve [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="41b73-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="41b73-115">[Batch yönetimi .NET kitaplığı](https://msdn.microsoft.com/library/mt463120.aspx) başvurusu</span><span class="sxs-lookup"><span data-stu-id="41b73-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="41b73-116">Öğreticiler: kullanmaya başlama [.NET için Azure Batch kitaplığını](batch-dotnet-get-started.md) ve [Batch Python istemcisini](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="41b73-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="41b73-117">Toplu işlem Forumu</span><span class="sxs-lookup"><span data-stu-id="41b73-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="41b73-118">Toplu videolar</span><span class="sxs-lookup"><span data-stu-id="41b73-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="41b73-119">HPC küme çözümleri</span><span class="sxs-lookup"><span data-stu-id="41b73-119">HPC cluster solutions</span></span>
<span data-ttu-id="41b73-120">Dağıtma veya var olan Windows veya Linux HPC kümeniz, işlem yoğunluklu iş yüklerini çalıştırmak için Azure'a genişletin.</span><span class="sxs-lookup"><span data-stu-id="41b73-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="41b73-121">Microsoft HPC paketi</span><span class="sxs-lookup"><span data-stu-id="41b73-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="41b73-122">HPC Pack Microsoft Azure ve Windows Server teknolojileri üzerinde Windows ve Linux HPC iş yükleri çalıştırabilen yerleşik Microsoft'un ücretsiz HPC çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="41b73-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="41b73-123">HPC Pack 2016 indirin</span><span class="sxs-lookup"><span data-stu-id="41b73-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="41b73-124">HPC Pack 2012 R2 güncelleştirme 3 indirin</span><span class="sxs-lookup"><span data-stu-id="41b73-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="41b73-125">Belgeleri</span><span class="sxs-lookup"><span data-stu-id="41b73-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="41b73-126">HPC Pack küme seçenekleri azure'da: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="41b73-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="41b73-127">HPC paketi ile Azure çalışan örneklerine veri bloğu</span><span class="sxs-lookup"><span data-stu-id="41b73-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="41b73-128">HPC paketi ile Azure toplu işlem için veri bloğu</span><span class="sxs-lookup"><span data-stu-id="41b73-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="41b73-129">Windows HPC forumları</span><span class="sxs-lookup"><span data-stu-id="41b73-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="41b73-130">Linux ve OSS küme çözümleri</span><span class="sxs-lookup"><span data-stu-id="41b73-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="41b73-131">Linux HPC Küme dağıtımı için Azure bu şablonları kullanın.</span><span class="sxs-lookup"><span data-stu-id="41b73-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="41b73-132">[Döndürme SLURM küme](https://azure.microsoft.com/documentation/templates/slurm/) ve [blog gönderisi](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="41b73-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="41b73-133">Torque küme Döndür</span><span class="sxs-lookup"><span data-stu-id="41b73-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="41b73-134">Kılavuz şablonları ile PBS Professional işlem</span><span class="sxs-lookup"><span data-stu-id="41b73-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="41b73-135">HPC depolama</span><span class="sxs-lookup"><span data-stu-id="41b73-135">HPC storage</span></span>
* [<span data-ttu-id="41b73-136">Azure üzerinde HPC depolama için paralel dosya sistemleri</span><span class="sxs-lookup"><span data-stu-id="41b73-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="41b73-137">Lustre yazılım - Eval için Intel bulut Edition</span><span class="sxs-lookup"><span data-stu-id="41b73-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="41b73-138">CentOS 7.2 şablonundaki BeeGFS</span><span class="sxs-lookup"><span data-stu-id="41b73-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="41b73-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="41b73-139">Microsoft MPI</span></span>
<span data-ttu-id="41b73-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI), ileti geçirme arabirimi standart geliştirmek ve Windows platformu üzerinde paralel uygulamalarını çalıştırmak için bir Microsoft uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="41b73-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="41b73-141">MS-MPI indirin</span><span class="sxs-lookup"><span data-stu-id="41b73-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="41b73-142">MS-MPI başvurusu</span><span class="sxs-lookup"><span data-stu-id="41b73-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="41b73-143">MPI Forumu</span><span class="sxs-lookup"><span data-stu-id="41b73-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="41b73-144">Yoğun işlem gücü kullanımlı örnekler</span><span class="sxs-lookup"><span data-stu-id="41b73-144">Compute-intensive instances</span></span>
<span data-ttu-id="41b73-145">Azure teklifleri bir [aralığı, VM boyutları](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)dahil [işlem yoğunluklu H-serisi](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) örnekleri Linux ve Windows HPC iş yüklerini çalıştırmak için bir arka uç RDMA ağa bağlanıp bağlanamayacağını.</span><span class="sxs-lookup"><span data-stu-id="41b73-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="41b73-146">MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama</span><span class="sxs-lookup"><span data-stu-id="41b73-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="41b73-147">MPI uygulamaları çalıştırmak için Microsoft HPC Pack ile Windows RDMA kümesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="41b73-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="41b73-148">GPU kullanımı yoğun iş yükleri için kullanıma [NC ve NV boyutları](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="41b73-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="41b73-149">Örnekler ve gösterileri</span><span class="sxs-lookup"><span data-stu-id="41b73-149">Samples and demos</span></span>
* [<span data-ttu-id="41b73-150">Azure Batch C# ve Python kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="41b73-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="41b73-151">[Toplu Shipyard](https://azure.github.io/batch-shipyard/) Azure Batch toplu stili Dockerized iş yüklerinin kolay dağıtım için araç seti</span><span class="sxs-lookup"><span data-stu-id="41b73-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="41b73-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) Azure Batch üstünde oluşturulmuş R paketi</span><span class="sxs-lookup"><span data-stu-id="41b73-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="41b73-153">SUSE Linux Enterprise Server HPC için sınayın</span><span class="sxs-lookup"><span data-stu-id="41b73-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="41b73-154">İlgili Azure Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="41b73-154">Related Azure services</span></span>
* [<span data-ttu-id="41b73-155">Data Factory</span><span class="sxs-lookup"><span data-stu-id="41b73-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="41b73-156">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="41b73-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="41b73-157">Hdınsight</span><span class="sxs-lookup"><span data-stu-id="41b73-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="41b73-158">Sanal Makineler</span><span class="sxs-lookup"><span data-stu-id="41b73-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="41b73-159">Sanal Makine Ölçek Kümeleri</span><span class="sxs-lookup"><span data-stu-id="41b73-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="41b73-160">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="41b73-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="41b73-161">App Service</span><span class="sxs-lookup"><span data-stu-id="41b73-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="41b73-162">Media Services</span><span class="sxs-lookup"><span data-stu-id="41b73-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="41b73-163">İşlevler</span><span class="sxs-lookup"><span data-stu-id="41b73-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="41b73-164">Mimari şemalar</span><span class="sxs-lookup"><span data-stu-id="41b73-164">Architecture blueprints</span></span>
* <span data-ttu-id="41b73-165">[Azure Batch ve Azure Data Factory kullanarak HPC ve veriler orchestration](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) ve [makale](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="41b73-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="41b73-166">Endüstri çözümleri</span><span class="sxs-lookup"><span data-stu-id="41b73-166">Industry solutions</span></span>
* [<span data-ttu-id="41b73-167">Banka ve büyük harf pazarda</span><span class="sxs-lookup"><span data-stu-id="41b73-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="41b73-168">Mühendislik benzetimleri</span><span class="sxs-lookup"><span data-stu-id="41b73-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="41b73-169">Müşteri hikayeleri</span><span class="sxs-lookup"><span data-stu-id="41b73-169">Customer stories</span></span>
* [<span data-ttu-id="41b73-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="41b73-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="41b73-171">d3vıew</span><span class="sxs-lookup"><span data-stu-id="41b73-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="41b73-172">Ludwig Institute of Kanseri araştırma</span><span class="sxs-lookup"><span data-stu-id="41b73-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="41b73-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="41b73-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="41b73-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="41b73-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="41b73-175">Mitsubishi UFJ senedi uluslararası</span><span class="sxs-lookup"><span data-stu-id="41b73-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="41b73-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="41b73-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="41b73-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="41b73-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="41b73-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="41b73-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="41b73-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41b73-179">Next steps</span></span>
* <span data-ttu-id="41b73-180">Son duyurular için bkz. [Microsoft HPC ve Batch ekip blogu](http://blogs.technet.com/b/windowshpc/) ve [Azure blogu](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="41b73-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="41b73-181">Ayrıca bkz. [toplu işlemde yenilikler](https://azure.microsoft.com/updates/?service=batch) veya abone olmak [RSS akışı](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="41b73-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

