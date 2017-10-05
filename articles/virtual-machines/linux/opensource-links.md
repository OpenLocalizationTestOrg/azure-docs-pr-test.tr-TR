---
title: "Linux ve açık kaynaklı Azure üzerinde bilgi işlem | Microsoft Docs"
description: "Linux ve açık kaynak bilgisayar makaleleri çalıştıran veya Linux görüntülerinde Azure ve belirli teknolojileri ve en iyi duruma getirme ile ilgili diğer içerik karşıya yükleme hakkında bazı temel kavramları dahil olmak üzere temel Linux kullanım, azure'da listelenmektedir."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 1cdd0e68368d2dc376ee45df67bf5e75288d4ca3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Azure'da Linux ve açık kaynaklı işlem
Oluşturmanız ve Linux tabanlı sanal makineleri Klasik dağıtım modelinde yönetmek için gereken tüm belgeleri bulur.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../resource-manager-deployment-model.md). Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.

## <a name="get-started"></a>Kullanmaya Başlama
* [Azure Linux için giriş](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Sık sorulan soruya hakkında Azure Klasik dağıtım modeliyle oluşturulan sanal makineler](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Sanal makineler için görüntüler hakkında](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Kendi Distro görüntünüzü karşıya](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (ve kullanma yönergeleri de bir [Azure-Endorsed dağıtım](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))
* [Klasik Azure portalı kullanarak bir Linux VM oturum açın](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>Kurulum
* [Azure yükleme komut satırı arabirimi (Azure CLI)](../../cli-install-nodejs.md)

## <a name="tutorials"></a>Öğreticiler
* [Azure'da bir Linux sanal makine AMPUL yığını yükleyin.](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM'de rayları Web uygulaması üzerinde Ruby](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [Nasıl yapılır: yükleme Apache Qpid Proton-C AMQP ve hizmet veri yolu](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>Veritabanları
* [Azure üzerinde MySQL performansını en iyi duruma getirme](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MySQL kümeleri](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Cassandra ile Linux Azure üzerinde çalışan ve adresinden node.js'yi erişme](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MariaDbs birden çok yöneticili kümesi oluşturma](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack NAMD çalıştırın](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [Docker Sanal Makine Uzantısını Azure Komut Satırı Arabirimi (Azure CLI) ile kullanma](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Docker Sanal Makine Uzantısını Azure portalından kullanma](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Azure’da docker-machine kullanma](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [Nasıl yapılır: MySQL kümeleri](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Nasıl yapılır: Node.js ve Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [Nasıl yapılır: yükleme ve çalıştırma MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [Nasıl yapılır: Azure üzerinde CoreOS kullanın](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>Planlama
* [Azure altyapı hizmetleri uygulama yönergeleri](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Linux kullanıcı adları seçme](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Kullanılabilirlik kümesi Klasik dağıtım modelinde sanal makineler için yapılandırma](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Azure Vm'lerinde nasıl zamanlanacağını planlı bakım](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Sanal makinelerin kullanılabilirliğini yönetme](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure'daki Linux sanal makineler için planlı bakım](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>Dağıtım
* [Linux çalıştıran özel bir sanal makine oluşturma](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Temel Kavramları: bir şablon yapmak için bir Linux VM yakalama](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Desteklenmeyen dağıtımlarla bilgi](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>Yönetim
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Linux için bir parola veya SSH özellikleri sıfırlama](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Kök kullanma](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Azure Kaynakları
* [Azure Linux Aracısı](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VM uzantıları ve özellikleri](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bulut başlatma ile kullanmak için bir VM injecting özel verileri](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Depolama
* [Bir Linux VM için bir veri diski ekleme](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Bir Linux VM veri diskten ayırma](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Ağ
* [Uç noktaları klasik bir sanal makinede Azure kurma](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>Sorun giderme
* [Linux tabanlı bir Azure sanal makine için güvenli Kabuk (SSH) bağlantı sorunlarını giderme](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure'da yeni bir Linux sanal makine oluşturma ile klasik dağıtım sorunlarını giderme](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Yeniden başlatmadan veya varolan bir Linux sanal makinesini Azure yeniden boyutlandırma Klasik dağıtım sorunlarını giderme](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>Başvuru
* [Azure Hizmet Yönetimi (asm) modunda Azure CLI komutları](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Azure Hizmet Yönetimi REST API'si](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>Genel bağlantılar
Aşağıdaki Microsoft Web günlükleri, Technet sayfaları ve dış sitelere yerine yukarıdaki Azure.com belgelemek için bağlantılardır. Hem Azure hem de açık kaynak bilgisayar world hızlı taşıma gibi hedefler, aşağıdaki bağlantılardan güncel, neredeyse kesin *rağmen* biz sürekli olarak yeni konular eklemek ve güncel kaldırmak için elimizden geleni yapacağız olgusu olanları. Biz biri eksik varsa, lütfen bize açıklamaları biliyorsanız veya bir çekme isteği göndermek bizim [GitHub deposuna](https://github.com/Azure/azure-content/).

* [ASP.NET 5 Docker kapsayıcıları kullanma Linux üzerinde çalışan](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [OpenLogic CentOS VM görüntüden dağıtma](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [SUSE güncelleştirme altyapısı](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server SAP bulut Gereci kitaplığı](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [Yüksek oranda kullanılabilir Linux 12 adımlarda Azure üzerinde oluşturma](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Sağlama Linux Azure üzerinde Azure CLI, node.js, jhawk sahip otomatikleştirme](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [Azure üzerinde GlusterFS](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [FreeBSD Azure'da çalışan](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [Kolay FreeBSD dağıtma](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [Özelleştirilmiş bir FreeBSD görüntü dağıtma](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Kaspersky AV Linux dosya sunucusu](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>NoSQL
* [Azure için 8 açık kaynak NoSql veritabanları](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech): Azure üzerinde CouchDb deneyimleriyle](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [CouchDB-bir node.js, CORS ve Grunt hizmet olarak çalışıyor](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Windows Azure Redis önbelleği hizmetindeki redis](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [Redis Önizleme sürümü için ASP.NET oturum durumu sağlayıcısı Duyurusu](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [Blog: RavenHQ hizmetinizde Azure markette](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>Büyük Veri
* [Azure Linux VM'ler üzerinde Hadoop yükleme](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure Hdınsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>İlişkisel veritabanı
* [Microsoft azure'da MySQL yüksek kullanılabilirlik mimarisi](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [Postgres corosync, ILB kullanarak pg_bouncer yükleme](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Linux yüksek performanslı bilgi işlem (HPC)
* [Hızlı Başlatma şablonunu: döndürme SLURM küme](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (ve [blog gönderisi](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [Hızlı Başlatma şablonunu: Linux işlem düğümleri ile bir HPC kümesi oluşturma](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>Devops, yönetim ve en iyi duruma getirme
Devops world, yönetim ve en iyi duruma getirme oldukça korunmalarını ve çok hızlı bir şekilde değiştirmeden, bir başlangıç noktası aşağıdaki liste düşünmelisiniz.

* [Video: Azure sanal makineler: kullanarak Chef, Puppet ve Linux sanal makineleri yönetmek için Docker](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [CoreOS ve Weave ile otomatikleştirilmiş Kubernetes küme dağıtımı konusunda bilmeniz gereken her şey](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Jenkins bağımlı için Azure eklentisi](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [GitHub deposu: Azure için Jenkins Depolama Eklentisi](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [Üçüncü Taraf: Azure için Hudson Bağımlı Eklentisi](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [Üçüncü Taraf: Azure için Hudson Depolama Eklentisi](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Video: Chef nedir ve nasıl çalışır?](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [Video: Azure Otomasyonunu Linux Sanal Makineleri ile Kullanma](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [Blog: Linux için Powershell DSC gerçekleştirme](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub: Docker İstemcisi DSC](https://github.com/anweiss/DockerClientDSC)
* [Azure için packer eklentisi](https://github.com/msopentech/packer-azure)

