---
title: "Microsoft azure'da bulut Foundry ilk uygulamanızı dağıtma | Microsoft Docs"
description: "Bulut Foundry azure'da bir uygulamayı dağıtma"
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
ms.openlocfilehash: b617127fc0a3f8dcae293e356ea669edcfa5deff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-your-first-app-to-cloud-foundry-on-microsoft-azure"></a><span data-ttu-id="b7a5d-103">Microsoft azure'da bulut Foundry ilk uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="b7a5d-103">Deploy your first app to Cloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="b7a5d-104">[Bulut Foundry](http://cloudfoundry.org) popüler açık kaynak uygulama platformu Microsoft Azure üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="b7a5d-105">Bu makalede, dağıtmak ve uygulamayı bulut Foundry üzerinde bir Azure ortamı yönetmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-105">In this article, we show how to deploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="b7a5d-106">Bir bulut Foundry ortam oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7a5d-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="b7a5d-107">Azure üzerinde bir bulut Foundry ortamı oluşturmak için birkaç seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="b7a5d-108">Kullanım [Bileşendirler bulut Foundry teklif] [ pcf-azuremarketplace] PCF Ops Manager ve Azure hizmet aracısı içeren standart bir ortam oluşturmak için Azure Market'te.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-108">Use the [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in the Azure Marketplace to create a standard environment that includes PCF Ops Manager and the Azure Service Broker.</span></span> <span data-ttu-id="b7a5d-109">Bulabileceğiniz [tamamlamak yönergeleri] [ pcf-azuremarketplace-pivotaldocs] Market dağıtmak için Bileşendirler belgelerde sunar.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying the marketplace offer in the Pivotal documentation.</span></span>
- <span data-ttu-id="b7a5d-110">Tarafından özelleştirilmiş bir ortam oluşturmak [Bileşendirler bulut Foundry el ile dağıtma][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="b7a5d-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="b7a5d-111">[Açık kaynak bulut Foundry paketlerini doğrudan dağıtma] [ oss-cf-bosh] ayarıyla bir [BOSH](http://bosh.io) director, bulut Foundry ortamı dağıtımını koordine eden bir VM.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-111">[Deploy the open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates the deployment of the Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b7a5d-112">Azure Marketi'nden PCF dağıtıyorsanız, SYSTEMDOMAINURL ve her ikisi de Market Dağıtım Kılavuzu'nda açıklanan Bileşendirler uygulamaları Yöneticisi'ne erişmek için gereken yönetici kimlik bilgilerini not edin.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-112">If you are deploying PCF from the Azure Marketplace, make a note of the SYSTEMDOMAINURL and the admin credentials required to access the Pivotal Apps Manager, both of which are described in the marketplace deployment guide.</span></span> <span data-ttu-id="b7a5d-113">Bu öğreticiyi tamamlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-113">They are needed to complete this tutorial.</span></span> <span data-ttu-id="b7a5d-114">Market dağıtımları için SYSTEMDOMAINURL form https://system ' dir. *IP adresi*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-114">For marketplace deployments, the SYSTEMDOMAINURL is in the form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-to-the-cloud-controller"></a><span data-ttu-id="b7a5d-115">Bulut denetleyicisine bağlanma</span><span class="sxs-lookup"><span data-stu-id="b7a5d-115">Connect to the Cloud Controller</span></span>

<span data-ttu-id="b7a5d-116">Bulut denetleyicisi uygulamaları dağıtma ve yönetme için bir bulut Foundry ortam için birincil giriş noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-116">The Cloud Controller is the primary entry point to a Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="b7a5d-117">Çekirdek bulut denetleyicisi API (CCAPI), REST API olmakla birlikte çeşitli araçları üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-117">The core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="b7a5d-118">Bu durumda, biz üzerinden etkileşimde [bulut Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="b7a5d-118">In this case, we interact with it through the [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="b7a5d-119">Linux, MacOS veya Windows CLI yükleyebilirsiniz, ancak bunu hiç yüklemeyi tercih ediyorsanız, önceden yüklenmiş kullanılabilir [Azure bulut Kabuk][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="b7a5d-119">You can install the CLI on Linux, MacOS, or Windows, but if you'd prefer not to install it at all, it is available pre-installed in the [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="b7a5d-120">Oturum açmak için başına `api` Market dağıtımından elde SYSTEMDOMAINURL için.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-120">To log in, prepend `api` to the SYSTEMDOMAINURL that you obtained from the marketplace deployment.</span></span> <span data-ttu-id="b7a5d-121">Varsayılan dağıtım otomatik olarak imzalanan bir sertifika kullandığından, da bulundurmalısınız `skip-ssl-validation` geçin.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-121">Since the default deployment uses a self-signed certificate, you should also include the `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="b7a5d-122">Bulut Denetleyicisi oturum istenir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-122">You are prompted to log in to the Cloud Controller.</span></span> <span data-ttu-id="b7a5d-123">Market dağıtım yer alan adımları aldığınız Yönetici hesap kimlik bilgilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-123">Use the admin account credentials that you acquired from the marketplace deployment steps.</span></span>

<span data-ttu-id="b7a5d-124">Bulut Foundry sağlar *düzenlemeler* ve *alanları* ekipleri ve ortamlar paylaşılan bir dağıtım içinde yalıtmak için ad alanları olarak.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-124">Cloud Foundry provides *orgs* and *spaces* as namespaces to isolate the teams and environments within a shared deployment.</span></span> <span data-ttu-id="b7a5d-125">Varsayılan PCF Market dağıtımının *sistem* org ve alanları temel bileşenler içerecek şekilde oluşturulmuş bir dizi gibi otomatik ölçeklendirmeyi hizmeti ve Azure hizmet Aracısı.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-125">The PCF marketplace deployment includes the default *system* org and a set of spaces created to contain the base components, like the autoscaling service and the Azure service broker.</span></span> <span data-ttu-id="b7a5d-126">Şimdilik, seçin *sistem* alanı.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-126">For now, choose the *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="b7a5d-127">Bir kuruluş oluşturup alanı</span><span class="sxs-lookup"><span data-stu-id="b7a5d-127">Create an org and space</span></span>

<span data-ttu-id="b7a5d-128">Yazarsanız, `cf apps`, sistem Krlş. içinde sistem alanında dağıtılan sistem uygulamaları bakın</span><span class="sxs-lookup"><span data-stu-id="b7a5d-128">If you type `cf apps`, you see a set of system applications that have been deployed in the system space within the system org.</span></span> 

<span data-ttu-id="b7a5d-129">Bulundurmanız gereken *sistem* sistem uygulamaları için ayrılmış org dolayısıyla oluşturun org ve örnek uygulamamız barındırmak için alanı.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-129">You should keep the *system* org reserved for system applications, so create an org and space to house our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="b7a5d-130">Yeni org ve alan geçiş yapmak için hedef komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-130">Use the target command to switch to the new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="b7a5d-131">Şimdi, bir uygulamayı dağıttığınızda, otomatik olarak yeni org ve alanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-131">Now, when you deploy an application, it is automatically created in the new org and space.</span></span> <span data-ttu-id="b7a5d-132">Olduğunu şu anda hiçbir uygulamanın yeni org/alan doğrulamak için şunu yazın `cf apps` yeniden.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-132">To confirm that there are currently no apps in the new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="b7a5d-133">Düzenlemeler ve alanları ve rol tabanlı erişim denetimi (RBAC) bunlar nasıl kullanılabileceği hakkında daha fazla bilgi için bkz: [bulut Foundry belgelerine][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="b7a5d-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see the [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b7a5d-134">Uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="b7a5d-134">Deploy an application</span></span>

<span data-ttu-id="b7a5d-135">Merhaba yay Java'da yazılmış ve temel bulut adlı örnek bir bulut Foundry uygulama kullanalım [yay Framework](http://spring.io) ve [yay önyükleme](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="b7a5d-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on the [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-the-hello-spring-cloud-repository"></a><span data-ttu-id="b7a5d-136">Merhaba yay bulut depoyu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="b7a5d-136">Clone the Hello Spring Cloud repository</span></span>

<span data-ttu-id="b7a5d-137">Merhaba yay bulut örnek uygulama, GitHub üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-137">The Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="b7a5d-138">Ortamınız için kopyalama ve yeni dizine değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-138">Clone it to your environment and change into the new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-the-application"></a><span data-ttu-id="b7a5d-139">Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="b7a5d-139">Build the application</span></span>

<span data-ttu-id="b7a5d-140">Uygulamasını kullanarak yapı [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="b7a5d-140">Build the app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-the-application-with-cf-push"></a><span data-ttu-id="b7a5d-141">Uygulama cf itme ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="b7a5d-141">Deploy the application with cf push</span></span>

<span data-ttu-id="b7a5d-142">Bulut Foundry kullanmanın çoğu uygulamaları dağıtabilirsiniz `push` komutu:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-142">You can deploy most applications to Cloud Foundry using the `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="b7a5d-143">Olduğunda, *itme* bir uygulama, bulut Foundry uygulamada (Bu durumda, Java uygulaması) türünü algılar ve bağımlılıklarını (Bu durumda, yay framework) tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-143">When you *push* an application, Cloud Foundry detects the type of application (in this case, a Java app) and identifies its dependencies (in this case, the Spring framework).</span></span> <span data-ttu-id="b7a5d-144">Bunun ardından olarak bilinen bir tek başına kapsayıcı görüntüsü kodunuzu çalıştırmak için gereken her şeyi paketleri bir *Damlacık*.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-144">It then packages everything required to run your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="b7a5d-145">Son olarak, bulut Foundry ortamınızdaki kullanılabilir makineleri birindeki uygulama zamanlar ve size, komut çıktısında kullanılabilir olduğu ulaşabilecekleri bir URL oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-145">Finally, Cloud Foundry schedules the application on one of the available machines in your environment and creates a URL where you can reach it, which is available in the output of the command.</span></span>

![Cf itme komut çıktısı][cf-push-output]

<span data-ttu-id="b7a5d-147">Merhaba yay bulut uygulaması görmek için sağlanan URL'nin tarayıcınızda açın:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-147">To see the hello-spring-cloud application, open the provided URL in your browser:</span></span>

![Merhaba yay bulut için varsayılan kullanıcı Arabirimi][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="b7a5d-149">Sırasında neler olduğu hakkında daha fazla bilgi için `cf push`, bkz: [uygulamaları nasıl hazırlanır] [ cf-push-docs] bulut Foundry belgelerinde.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-149">To learn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in the Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="b7a5d-150">Uygulama günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="b7a5d-150">View application logs</span></span>

<span data-ttu-id="b7a5d-151">Bulut Foundry CLI adını kullanarak bir uygulama için günlükleri görüntülemek için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-151">You can use the Cloud Foundry CLI to view logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="b7a5d-152">Varsayılan olarak, günlükler kullanan komut *tail*, yazıldığı gibi yeni günlükler gösterir.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-152">By default, the logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="b7a5d-153">Yeni günlükler görünür görmek için tarayıcıda hello yay bulut uygulama yenileyin.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-153">To see new logs appear, refresh the hello-spring-cloud app in the browser.</span></span>

<span data-ttu-id="b7a5d-154">Zaten yazılmış günlükleri görüntülemek için add `recent` geçin:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-154">To view logs that have already been written, add the `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-the-application"></a><span data-ttu-id="b7a5d-155">Uygulama ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="b7a5d-155">Scale the application</span></span>

<span data-ttu-id="b7a5d-156">Varsayılan olarak, `cf push` yalnızca uygulamanızın tek bir örneğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="b7a5d-157">Yüksek kullanılabilirlik sağlamak ve ölçek genişletme için daha yüksek verimlilik etkinleştirmek için genellikle uygulamalarınızı birden fazla örneğini çalıştıran istersiniz.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-157">To ensure high availability and enable scale out for higher throughput, you generally want to run more than one instance of your applications.</span></span> <span data-ttu-id="b7a5d-158">Zaten dağıtılmış uygulamalarının kullanarak kolayca ölçeklendirebilirsiniz `scale` komutu:</span><span class="sxs-lookup"><span data-stu-id="b7a5d-158">You can easily scale out already deployed applications using the `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="b7a5d-159">Çalışan `cf app` uygulama komutunda gösterir bulut Foundry uygulama başka bir örneği oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-159">Running the `cf app` command on the application shows that Cloud Foundry is creating another instance of the application.</span></span> <span data-ttu-id="b7a5d-160">Uygulama başlatıldıktan sonra bulut Foundry Yük Dengeleme trafiğini onu otomatik olarak başlar.</span><span class="sxs-lookup"><span data-stu-id="b7a5d-160">Once the application has started, Cloud Foundry automatically starts load balancing traffic to it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b7a5d-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7a5d-161">Next steps</span></span>

- <span data-ttu-id="b7a5d-162">[Bulut Foundry belgeleri okuyun][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="b7a5d-162">[Read the Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="b7a5d-163">[Visual Studio Team Services eklentisi bulut Foundry için ayarlama][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="b7a5d-163">[Set up the Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="b7a5d-164">[Microsoft günlük analizi kafa bulut Foundry için yapılandırma][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="b7a5d-164">[Configure the Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

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