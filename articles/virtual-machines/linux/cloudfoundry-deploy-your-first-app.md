---
title: aaaDeploy ilk uygulama tooCloud Foundry Microsoft Azure | Microsoft Docs
description: "Bir uygulama tooCloud Foundry Azure üzerinde dağıtma"
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="c7fc7-103">İlk app tooCloud Foundry Microsoft Azure üzerinde dağıtma</span><span class="sxs-lookup"><span data-stu-id="c7fc7-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="c7fc7-104">[Bulut Foundry](http://cloudfoundry.org) popüler açık kaynak uygulama platformu Microsoft Azure üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="c7fc7-105">Bu makalede, gösteriyoruz nasıl toodeploy ve uygulamayı bulut Foundry üzerinde bir Azure ortamı yönetin.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="c7fc7-106">Bir bulut Foundry ortam oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7fc7-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="c7fc7-107">Azure üzerinde bir bulut Foundry ortamı oluşturmak için birkaç seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="c7fc7-108">Kullanım hello [Bileşendirler bulut Foundry teklif] [ pcf-azuremarketplace] hello Azure Marketi toocreate PCF Ops Manager ve hello Azure hizmet aracısı içeren standart bir ortam içinde.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="c7fc7-109">Bulabileceğiniz [tamamlamak yönergeleri] [ pcf-azuremarketplace-pivotaldocs] hello Market dağıtmak için hello Bileşendirler belgelerine sunar.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="c7fc7-110">Tarafından özelleştirilmiş bir ortam oluşturmak [Bileşendirler bulut Foundry el ile dağıtma][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="c7fc7-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="c7fc7-111">[Merhaba açık kaynak bulut Foundry paketlerini doğrudan dağıtma] [ oss-cf-bosh] ayarıyla bir [BOSH](http://bosh.io) director hello dağıtım hello bulut Foundry ortamının koordine eden bir VM.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c7fc7-112">Azure Market hello PCF dağıtıyorsanız, hello SYSTEMDOMAINURL not edin ve tooaccess Bileşendirler uygulamaları Yöneticisi, her ikisi de hello Market Dağıtım Kılavuzu'nda açıklanan hello hello yönetici kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="c7fc7-113">Bunlar Bu öğreticide gerekli toocomplete şunlardır.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="c7fc7-114">Market dağıtımları için hello SYSTEMDOMAINURL hello form https://system ' dir. *IP adresi*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="c7fc7-115">Toohello bulut denetleyicisi Bağlan</span><span class="sxs-lookup"><span data-stu-id="c7fc7-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="c7fc7-116">Merhaba bulut denetleyicisi uygulamaları dağıtma ve yönetme için hello birincil giriş noktası tooa bulut Foundry ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="c7fc7-117">Merhaba çekirdek bulut denetleyicisi API (CCAPI), REST API olmakla birlikte çeşitli araçları üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="c7fc7-118">Bu durumda, biz ile Merhaba etkileşim [bulut Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="c7fc7-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="c7fc7-119">Linux, MacOS veya Windows hello CLI yükleyebilirsiniz, ancak hiç, bu durumda kullanılabilir hello önceden yüklenmiş tooinstall tercih ederseniz [Azure bulut Kabuk][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="c7fc7-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="c7fc7-120">' de, toolog başına `api` toohello hello Market dağıtımından elde SYSTEMDOMAINURL.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="c7fc7-121">Merhaba varsayılan dağıtım otomatik olarak imzalanan bir sertifika kullandığından, ayrıca hello içermelidir `skip-ssl-validation` geçin.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="c7fc7-122">İstendiğinde toolog toohello bulut denetleyicisi içinde var.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="c7fc7-123">Merhaba Market dağıtım adımları aldığınız hello yönetici hesabı kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="c7fc7-124">Bulut Foundry sağlar *düzenlemeler* ve *alanları* ad alanları tooisolate hello ekipleri ve paylaşılan bir dağıtım ortamlarında olarak.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="c7fc7-125">Merhaba PCF Market dağıtım içerir hello varsayılan *sistem* org ve bir dizi alanları hello otomatik ölçeklendirmeyi hizmet ve hello Azure hizmet aracısı gibi hello temel bileşenler toocontain oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="c7fc7-126">Şimdilik, hello seçin *sistem* alanı.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="c7fc7-127">Bir kuruluş oluşturup alanı</span><span class="sxs-lookup"><span data-stu-id="c7fc7-127">Create an org and space</span></span>

<span data-ttu-id="c7fc7-128">Yazarsanız, `cf apps`, hello sistem Krlş. Sistem boşluğu hello olarak dağıtılan sistem uygulamaları bakın</span><span class="sxs-lookup"><span data-stu-id="c7fc7-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="c7fc7-129">Merhaba tutmalısınız *sistem* org sistem uygulamalar için ayrılmış örnek uygulamamız dolayısıyla bir kurum ve alan toohouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="c7fc7-130">Merhaba hedef komutu tooswitch toohello yeni org ve alan kullanın:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="c7fc7-131">Şimdi, bir uygulamayı dağıttığınızda, otomatik olarak hello yeni org ve alanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="c7fc7-132">şu anda tooconfirm hiçbir alanındaki hello yeni org/türdeki `cf apps` yeniden.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="c7fc7-133">Merhaba düzenlemeler ve alanları ve rol tabanlı erişim denetimi (RBAC) bunlar nasıl kullanılabileceği hakkında daha fazla bilgi için bkz: [bulut Foundry belgelerine][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="c7fc7-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="c7fc7-134">Uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="c7fc7-134">Deploy an application</span></span>

<span data-ttu-id="c7fc7-135">Java'da yazılmış ve hello üzerinde temel Hello yay bulut adlı örnek bir bulut Foundry uygulama kullanalım [yay Framework](http://spring.io) ve [yay önyükleme](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="c7fc7-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="c7fc7-136">Merhaba Hello yay bulut depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="c7fc7-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="c7fc7-137">Merhaba Hello yay bulut örnek uygulama, GitHub üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="c7fc7-138">Tooyour ortam kopyalamak ve hello yeni dizine değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="c7fc7-139">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c7fc7-139">Build hello application</span></span>

<span data-ttu-id="c7fc7-140">Yapı hello uygulamasını kullanarak [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="c7fc7-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="c7fc7-141">Merhaba uygulama cf itme oluşturup dağıtın</span><span class="sxs-lookup"><span data-stu-id="c7fc7-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="c7fc7-142">Çoğu uygulamalar tooCloud Foundry dağıtabilirsiniz hello kullanarak `push` komutu:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="c7fc7-143">Olduğunda, *itme* bir uygulama, bulut Foundry (Bu durumda, bir uygulamasında Java) uygulamasının hello türü algılar ve bağımlılıklarını (Framework'teki bu durumda, hello yay) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="c7fc7-144">Bunu daha sonra her şeyi paketleri olarak bilinen bir tek başına kapsayıcı görüntüsü kodunuzu toorun gerekli bir *Damlacık*.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="c7fc7-145">Son olarak, bulut Foundry zamanlamaları hello kullanılabilir makineleri ortamınızdaki birindeki uygulama hello ve size, hello hello komut çıktısında kullanılabilir olduğu ulaşabilecekleri bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Cf itme komut çıktısı][cf-push-output]

<span data-ttu-id="c7fc7-147">toosee Merhaba hello yay bulut uygulaması, tarayıcınızda açık hello sağlanan URL:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Merhaba yay bulut için varsayılan kullanıcı Arabirimi][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="c7fc7-149">toolearn sırasında neler olduğu hakkında daha fazla `cf push`, bkz: [uygulamaları nasıl hazırlanır] [ cf-push-docs] hello bulut Foundry belge içinde.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="c7fc7-150">Uygulama günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="c7fc7-150">View application logs</span></span>

<span data-ttu-id="c7fc7-151">Merhaba bulut Foundry CLI tooview günlükleri için bir uygulama adıyla kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="c7fc7-152">Varsayılan olarak, komut kullanır hello günlüklerini *tail*, yazıldığı gibi yeni günlükler gösterir.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="c7fc7-153">toosee yeni günlükler görünen hello hello yay bulut uygulamayı hello tarayıcıda yenileyin.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="c7fc7-154">yazılan tooview günlükleri eklemek hello `recent` geçin:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="c7fc7-155">Merhaba uygulamayı Ölçeklendir</span><span class="sxs-lookup"><span data-stu-id="c7fc7-155">Scale hello application</span></span>

<span data-ttu-id="c7fc7-156">Varsayılan olarak, `cf push` yalnızca uygulamanızın tek bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="c7fc7-157">tooensure yüksek kullanılabilirlik ve yüksek verimlilik için etkinleştir ölçek genişletme, uygulamalarınızı bir örneğine birden çok toorun genellikle istersiniz.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="c7fc7-158">Zaten dağıtılmış uygulamalarının hello kullanarak kolayca ölçeklendirebilirsiniz `scale` komutu:</span><span class="sxs-lookup"><span data-stu-id="c7fc7-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="c7fc7-159">Çalışan hello `cf app` Merhaba uygulaması komutunda gösterir bulut Foundry hello uygulama başka bir örneği oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="c7fc7-160">Merhaba uygulaması başladıktan sonra bulut Foundry Yük Dengeleme trafik tooit otomatik olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="c7fc7-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7fc7-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7fc7-161">Next steps</span></span>

- <span data-ttu-id="c7fc7-162">[Okuma hello bulut Foundry belgeleri][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="c7fc7-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="c7fc7-163">[Hello Visual Studio Team Services eklentisi için bulut Foundry ayarlayın][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="c7fc7-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="c7fc7-164">[Merhaba Microsoft günlük analizi kafa bulut Foundry için yapılandırma][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="c7fc7-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png