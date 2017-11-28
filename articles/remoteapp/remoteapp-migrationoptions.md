---
title: "Azure RemoteApp geçirmek için aaaOptions | Microsoft Docs"
description: "Azure RemoteApp geçirmeye hello seçenekleri hakkında bilgi edinin."
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a><span data-ttu-id="b7c48-103">Azure RemoteApp geçiş seçenekleri</span><span class="sxs-lookup"><span data-stu-id="b7c48-103">Options for migrating out of Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b7c48-104">Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır.</span><span class="sxs-lookup"><span data-stu-id="b7c48-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b7c48-105">Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="b7c48-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>


<span data-ttu-id="b7c48-106">Hello nedeniyle Azure RemoteApp kullanarak durduruldu durumunda [devre dışı bırakma Duyurusu](https://go.microsoft.com/fwlink/?linkid=821148) veya değerlendirmeniz bitirdikten sonra olduğundan, Azure RemoteApp tooanother uygulama hizmeti dışına toomigrate gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-106">If you have stopped using Azure RemoteApp because of hello [retirement announcement](https://go.microsoft.com/fwlink/?linkid=821148) or because you've finished your evaluation, you need toomigrate off of Azure RemoteApp tooanother app service.</span></span> <span data-ttu-id="b7c48-107">Geçirmek için iki farklı yaklaşım vardır: bir kendi kendine yönetilen (genellikle [Iaas] hizmet olarak altyapı olarak adlandırılır) bir tam olarak yönetilen (genellikle çağrılan hizmet olarak Platform) veya [PaaS/SaaS] hizmet olarak yazılım dağıtımı veya sunar.</span><span class="sxs-lookup"><span data-stu-id="b7c48-107">There are two different approaches for migrating: a self-managed (often called Infrastructure as a Service [IaaS]) deployment or a fully managed (often called Platform as a Service or Software as a Service [PaaS/SaaS]) offering.</span></span> 

<span data-ttu-id="b7c48-108">Self Servis Iaas olan yönetilen işletilen ve dağıttığınız, doğrudan sanal makineleri (VM'ler) veya fiziksel sistemleri tarafından sahip olunan yazılanları bir dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="b7c48-108">Self-service IaaS is a do-it-yourself deployment that is managed, operated, and owned by you, directly deployed on virtual machines (VMs) or physical systems.</span></span> <span data-ttu-id="b7c48-109">Merhaba diğer end, bir tam olarak yönetilen PaaS/olduğundan daha fazla Azure RemoteApp ister - iş ortağı işlemsel işleme remoting çözüm üzerinde bir hizmet katmanı sağlar sunumu SaaS ve hizmet verme sırasında hello müşterisi olarak, bazı görüntü ve uygulama yönetimi bunu.</span><span class="sxs-lookup"><span data-stu-id="b7c48-109">At hello other end, a fully managed PaaS/SaaS offering is more like Azure RemoteApp - a partner provides a service layer on top of a remoting solution that handles operational and servicing, while you, as hello customer, do some image and app management.</span></span>

<span data-ttu-id="b7c48-110">[Geçiş seçenekleri hello Azure RemoteApp Web Seminerlerini görüntüleyebilir](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), veya (Merhaba seçenekleri barındırma farklı örnekleri dahil) daha fazla bilgi için okumaya devam edin.</span><span class="sxs-lookup"><span data-stu-id="b7c48-110">[View hello Azure RemoteApp webinars on migration options](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), or read on for more information (including examples of hello different hosting options).</span></span>

## <a name="self-managed-iaas-solutions"></a><span data-ttu-id="b7c48-111">Kendi kendine yönetilen (Iaas) çözümleri</span><span class="sxs-lookup"><span data-stu-id="b7c48-111">Self-managed (IaaS) solutions</span></span>
### <a name="rds-on-iaas"></a><span data-ttu-id="b7c48-112">**RDS Iaas üzerinde**</span><span class="sxs-lookup"><span data-stu-id="b7c48-112">**RDS on IaaS**</span></span>
<span data-ttu-id="b7c48-113">RemoteApp veya Masaüstü şirket içi kullanarak bir yerel oturum tabanlı (Windows Server)'deki Uzak Masaüstü Hizmetleri dağıtımı dağıtabilir veya barındırılan bir ortamda (like Azure vm'lerinde).</span><span class="sxs-lookup"><span data-stu-id="b7c48-113">You can deploy a native session-based Remote Desktop Services (in Windows Server) deployment using either RemoteApp or desktops on-premises or in a hosted environment (like on Azure VMs).</span></span> <span data-ttu-id="b7c48-114">RDS Iaas dağıtımlarda zaten aşina müşteriler için en iyi ve RDS dağıtımlar ile var olan teknik uzmanlığı olan.</span><span class="sxs-lookup"><span data-stu-id="b7c48-114">RDS on IaaS deployments are best for customers already familiar with and that have existing technical expertise with RDS deployments.</span></span> 

> [!NOTE]
> <span data-ttu-id="b7c48-115">Toplu Lisanslama Yazılım Güvencesi (SA) ile RDS istemci erişim lisansları toouse için bu dağıtım seçeneğini gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-115">You need Volume Licensing with Software Assurance (SA) for RDS client access licenses toouse this deployment option.</span></span>

<span data-ttu-id="b7c48-116">Azure vm'lerinde RDS dağıtma sürekli dağıtımı ve şablonları düzeltme eki uygulama kullandığınızda, daha kolay (okuma bir [genel bakış](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) ve ardından [bunları getirmek Git](https://aka.ms/rdautomation)).</span><span class="sxs-lookup"><span data-stu-id="b7c48-116">Deploying RDS on Azure VMs is easier than ever when you use deployment and patching templates (read an [overview](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) and then [go get them](https://aka.ms/rdautomation)).</span></span> <span data-ttu-id="b7c48-117">Merhaba hello kullanarak Azure RemoteApp içinde Azure Klasik dağıtım modeli kaynakları (Azure kaynak modeli kaynakları değil) ile aynı esnek ölçeklendirme özelliklerinden elde edebilirsiniz [otomatik komut dosyası ölçeklendirme](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), büyük/küçük vardır, ancak daha fazla Özelleştirmeleri ve yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="b7c48-117">You can get hello same elastic scaling capabilities with Azure classic deployment model resources (not Azure Resource Model resources) within Azure RemoteApp by using hello [auto scaling script](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), although there are more customizations and configurations.</span></span> <span data-ttu-id="b7c48-118">Azure vm'lerinde RDS dağıttığınızda, Destek aracılığıyla sağlanır [Azure Destek](https://azure.microsoft.com/support/plans/), hello Azure RemoteApp ile desteklenen aynı destek uzmanları.</span><span class="sxs-lookup"><span data-stu-id="b7c48-118">When you deploy RDS on Azure VMs, support is provided through [Azure Support](https://azure.microsoft.com/support/plans/), hello same support professionals that supported you with Azure RemoteApp.</span></span> <span data-ttu-id="b7c48-119">İle iletişim kurarak mevcut kullanımınıza bağlı alarak tahmin maliyeti olabilir [Azure Destek](https://azure.microsoft.com/support/plans/), veya kendiniz hesaplamalar gerçekleştirebilir kullanarak bir en kısa sürede toobe maliyet hesaplayıcı yayımlanan.</span><span class="sxs-lookup"><span data-stu-id="b7c48-119">You can get cost estimates based on your existing usage by contacting [Azure Support](https://azure.microsoft.com/support/plans/), or you can perform calculations yourself using a soon toobe released Cost Calculator.</span></span>  <span data-ttu-id="b7c48-120">Ayrıca, N-serisi Vm'lerde (şu anda özel olarak incelenmektedir) ile vGPU - ekleyebilirsiniz ve vGPU ekleme hakkında daha fazla çok duymak[kadar yararlanmak istiyorsanız, Windows Server 2016 RDS yenilikleri](https://myignite.microsoft.com/videos/2794) bizim Ignite oturumunda.</span><span class="sxs-lookup"><span data-stu-id="b7c48-120">Also, with N-series VMs (currently in private preview) you can add vGPU - hear more about adding vGPU and about how too[harness RDS improvements in Windows Server 2016](https://myignite.microsoft.com/videos/2794) in our Ignite session.</span></span>   

<span data-ttu-id="b7c48-121">Adım adım dağıtım kılavuzları için sahip olduğumuz [Windows Server 2012 R2](http://aka.ms/rdsonazure) ve [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist dağıtımınız ile.</span><span class="sxs-lookup"><span data-stu-id="b7c48-121">We have step by step deployment guides for [Windows Server 2012 R2](http://aka.ms/rdsonazure) and [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist with your deployment.</span></span> <span data-ttu-id="b7c48-122">Merhaba denetleyin [Uzak Masaüstü blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) hello en son haberler için.</span><span class="sxs-lookup"><span data-stu-id="b7c48-122">Check out hello [Remote Desktop blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) for hello latest news.</span></span>

### <a name="citrix-on-iaas"></a><span data-ttu-id="b7c48-123">**Citrix Iaas üzerinde**</span><span class="sxs-lookup"><span data-stu-id="b7c48-123">**Citrix on IaaS**</span></span>
<span data-ttu-id="b7c48-124">Şirket içi dağıtımı oturum tabanlı XenApp ya da XenDesktop olabilir yerel bir Citrix dağıtılmış veya barındırılan bir ortamda içinde (gibi Azure vm'lerinde).</span><span class="sxs-lookup"><span data-stu-id="b7c48-124">A native Citrix deployment of session-based XenApp or XenDesktop can be deployed on-premises or within a hosted environment (such as on Azure VMs).</span></span> 

<span data-ttu-id="b7c48-125">Merhaba adım adım Dağıtım Kılavuzu'na göz, denetleme [Citrix XA 7.6 Azure üzerinde](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b7c48-125">Check out hello step-by-step deployment guide, [Citrix XA 7.6 on Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), for more information.</span></span> <span data-ttu-id="b7c48-126">Daha fazla bilgi edinin [Citrix Azure üzerinde](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), fiyat hesaplayıcısını dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="b7c48-126">Read more about [Citrix on Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), including a price calculator.</span></span> <span data-ttu-id="b7c48-127">Bulabileceğiniz bir [Citrix kişi](http://citrix.com/English/contact/index.asp) toodiscuss seçeneklerinizi ile.</span><span class="sxs-lookup"><span data-stu-id="b7c48-127">You can also find a [Citrix contact](http://citrix.com/English/contact/index.asp) toodiscuss your options with.</span></span>

## <a name="fully-managed-paassaas-offerings"></a><span data-ttu-id="b7c48-128">Tam olarak yönetilen (PaaS/SaaS) teklifleri</span><span class="sxs-lookup"><span data-stu-id="b7c48-128">Fully managed (PaaS/SaaS) offerings</span></span>

### <a name="citrix-xenapp-essentials-released-april-2017"></a><span data-ttu-id="b7c48-129">Citrix XenApp (Nisan 2017 yayımlanan) Temelleri</span><span class="sxs-lookup"><span data-stu-id="b7c48-129">Citrix XenApp Essentials (released April 2017)</span></span>
<span data-ttu-id="b7c48-130">Merhaba üzerinde şu anda kullanılabilir [Azure Marketi](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials hizmettir hello yeni uygulama sanallaştırma, hello güç birleştirme ve esnekliğini hello hello basit, düzenleyici, Citrix bulut platformu ve Microsoft Azure RemoteApp görme kolay kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-130">Available now on hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix XenApp Essentials is hello new application virtualization service, combining hello power and flexibility of hello Citrix Cloud platform with hello simple, prescriptive, and easy-to-consume vision of Microsoft Azure RemoteApp.</span></span> 

<span data-ttu-id="b7c48-131">Var olan Azure RemoteApp müşterileri için [ücretsiz deneme için kayıt](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7c48-131">Existing Azure RemoteApp customers can [register for a free trial](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).</span></span>  <span data-ttu-id="b7c48-132">Not: Yalnızca Citrix kullanıcı servis ücreti ücretsizdir, Azure işlem ve depolama ücretleri</span><span class="sxs-lookup"><span data-stu-id="b7c48-132">Note: Only Citrix user service charge is free, Azure compute and storage costs apply</span></span>

<span data-ttu-id="b7c48-133">Daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="b7c48-133">Learn More:</span></span>
- [<span data-ttu-id="b7c48-134">Azure RemoteApp tooCitrix XenApp Essentials ' geçiş</span><span class="sxs-lookup"><span data-stu-id="b7c48-134">Migrate from Azure RemoteApp tooCitrix XenApp Essentials</span></span>](remoteapp-migrate-citrix.md)
- [<span data-ttu-id="b7c48-135">Citrix ve Microsoft</span><span class="sxs-lookup"><span data-stu-id="b7c48-135">Citrix and Microsoft</span></span>](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- <span data-ttu-id="b7c48-136">[Citrix XenApp Essentials sunu](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span><span class="sxs-lookup"><span data-stu-id="b7c48-136">[Citrix XenApp Essentials presentation](https://www.youtube.com/watch?v=91Z7CCfQ-9k).</span></span>  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a><span data-ttu-id="b7c48-137">Citrix bulut XenApp hizmeti ve XenDesktop hizmeti</span><span class="sxs-lookup"><span data-stu-id="b7c48-137">Citrix Cloud XenApp Service and XenDesktop Service</span></span> 

<span data-ttu-id="b7c48-138">[Citrix bulut XenApp hizmeti ve XenDesktop hizmeti](https://www.citrix.com/products/citrix-cloud/services.html) hello teslimini hem uygulamalar ve masaüstü bilgisayarlar, artı Gelişmiş Yönetim ve izleme kapasiteleri için hello en iyi çözümdür.</span><span class="sxs-lookup"><span data-stu-id="b7c48-138">[Citrix Cloud XenApp Service and XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) is hello best solution for hello delivery of both apps and desktops, plus advanced management and monitoring capabilities.</span></span> 

#### <a name="conexlink-platform-name-mycloudit"></a><span data-ttu-id="b7c48-139">Conexlink (Platform ad: MyCloudIT)</span><span class="sxs-lookup"><span data-stu-id="b7c48-139">Conexlink (Platform name: MyCloudIT)</span></span>
<span data-ttu-id="b7c48-140">[MyCloudIT](https://mycloudit.com) bir Otomasyon platformudur BT şirketler toosimplify için en iyi duruma getirme ve ölçeklendirme hello geçiş ve Uzak Masaüstü, uzak uygulamaları ve altyapısında teslimini hello Microsoft Azure bulut.</span><span class="sxs-lookup"><span data-stu-id="b7c48-140">[MyCloudIT](https://mycloudit.com) is an automation platform for IT companies toosimplify, optimize, and scale hello migration and delivery of remote desktops, remote applications, and infrastructure in hello Microsoft Azure Cloud.</span></span> 

<span data-ttu-id="b7c48-141">Merhaba MyCloudIT platform % 95, 30 oranında maliyeti Azure tarafından dağıtım süresini azaltır ve bunların istemcinin tüm BT altyapı sağlasa da, birkaç tuş vuruşlarını hello buluta taşır.</span><span class="sxs-lookup"><span data-stu-id="b7c48-141">hello MyCloudIT platform reduces deployment time by 95%, Azure cost by 30%, and moves their client's entire IT infrastructure into hello cloud in a matter of a few key strokes.</span></span> <span data-ttu-id="b7c48-142">İş ortakları bir genel panodan müşteriler artık yönetebilir, hizmet son kullanıcıların Merhaba Dünya bambaşka ister ve ek yükü veya Azure kapsamlı eğitim eklemeden gelirleri büyümesine.</span><span class="sxs-lookup"><span data-stu-id="b7c48-142">Partners can now manage customers from one global dashboard, service end users around hello world like never before, and grow revenues without adding additional overhead or extensive Azure training.</span></span>  

> <span data-ttu-id="b7c48-143">Birincil konumu: Dallas, TX, ABD</span><span class="sxs-lookup"><span data-stu-id="b7c48-143">Primary location: Dallas, TX, USA</span></span>
> 
> <span data-ttu-id="b7c48-144">İşlemi bölgesi: dünya çapında</span><span class="sxs-lookup"><span data-stu-id="b7c48-144">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="b7c48-145">İş ortağı, durum: [altın](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span><span class="sxs-lookup"><span data-stu-id="b7c48-145">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)</span></span>
> 
> <span data-ttu-id="b7c48-146">Microsoft bulut hizmeti sağlayıcısı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-146">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="b7c48-147">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-147">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="b7c48-148">Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](https://mycloudit.com/remote-app-microsoft/)</span><span class="sxs-lookup"><span data-stu-id="b7c48-148">Azure RemoteApp migration solutions: Yes, [learn more](https://mycloudit.com/remote-app-microsoft/)</span></span>
> 
> <span data-ttu-id="b7c48-149">Brian Garoutte, VP iş geliştirme</span><span class="sxs-lookup"><span data-stu-id="b7c48-149">Brian Garoutte, VP of Business Development</span></span>
> 
> <span data-ttu-id="b7c48-150">Telefon: 972-218-0741</span><span class="sxs-lookup"><span data-stu-id="b7c48-150">Phone: 972-218-0741</span></span>
>   
> <span data-ttu-id="b7c48-151">E-posta:[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span><span class="sxs-lookup"><span data-stu-id="b7c48-151">Email: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)</span></span>

### <a name="frame"></a><span data-ttu-id="b7c48-152">Çerçeve</span><span class="sxs-lookup"><span data-stu-id="b7c48-152">Frame</span></span>

<span data-ttu-id="b7c48-153">BT kuruluşları Kurumsal ve resmi, yönetilen hizmet sağlayıcıları ve önde gelen yazılım satıcıları çerçeve toocreate seçin ve kendi güvenli, yazılım tanımlı çalışma hello bulutta yönetin.</span><span class="sxs-lookup"><span data-stu-id="b7c48-153">IT organizations in enterprise and government, managed service providers, and leading software vendors choose Frame toocreate and manage their secure, software-defined workspaces in hello cloud.</span></span> <span data-ttu-id="b7c48-154">Küçük toolarge kuruluşlardan çerçeve son derece kolay toolet kullanıcılar kolaylaştırır herhangi bir tarayıcıda Windows uygulamaları herhangi bir aygıttan erişim.</span><span class="sxs-lookup"><span data-stu-id="b7c48-154">From small toolarge organizations, Frame makes it incredibly easy toolet users access Windows applications on any browser from any device.</span></span> <span data-ttu-id="b7c48-155">Merhaba çerçeve platform her şeyi hello bulut hello Azure altyapı ve RDS lisansları dahil olmak üzere bir yönetim gereksinimlerini toodeploy uygulamalardan içeren (kendi Azure hesabı ve lisansları getiren isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="b7c48-155">hello Frame platform includes everything an admin needs toodeploy applications from hello cloud including hello Azure infrastructure and RDS licenses (bringing your own Azure account and licenses is optional).</span></span> 

<span data-ttu-id="b7c48-156">Daha fazla bilgi edinmek [Azure çerçevesi](https://www.fra.me/ara).</span><span class="sxs-lookup"><span data-stu-id="b7c48-156">Learn more about [Frame on Azure](https://www.fra.me/ara).</span></span> 

> <span data-ttu-id="b7c48-157">Birincil konumu: San Mateo, CA, ABD</span><span class="sxs-lookup"><span data-stu-id="b7c48-157">Primary location: San Mateo, CA, USA</span></span>
>
> <span data-ttu-id="b7c48-158">İşlemi bölgesi: dünya çapında</span><span class="sxs-lookup"><span data-stu-id="b7c48-158">Operation region: Worldwide</span></span>
>
> <span data-ttu-id="b7c48-159">Microsoft iş ortağı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-159">Microsoft Partner: Yes</span></span>
> 
> <span data-ttu-id="b7c48-160">Telefon: 1-480-269-4668</span><span class="sxs-lookup"><span data-stu-id="b7c48-160">Phone: 1-480-269-4668</span></span>

### <a name="awingu"></a><span data-ttu-id="b7c48-161">Awingu</span><span class="sxs-lookup"><span data-stu-id="b7c48-161">Awingu</span></span>
<span data-ttu-id="b7c48-162">Awingu eski uygulamalar, SaaS ve belgeleri bir html5 tarayıcıdan çalıştıran bir basit çevrimiçi çalışma çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7c48-162">Awingu provides a simple online workspace solution running legacy apps, SaaS and documents from an html5 browser.</span></span> <span data-ttu-id="b7c48-163">Bu nedenle, tüm uygulamaları güvenli bir şekilde kullanılabilir cihaz herhangi bir türde hale getirme.</span><span class="sxs-lookup"><span data-stu-id="b7c48-163">As such, making any applications securely available on any type of device.</span></span> <span data-ttu-id="b7c48-164">SaaS Hizmetleri için çoklu oturum açma çeşitli op seçenekleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-164">For SaaS services, a wide range op Single-Sign-On options is available.</span></span> <span data-ttu-id="b7c48-165">Ayrıca farklı (bulut) dosya sistemleri iç çalışma alanınıza tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-165">Also diverse (cloud) files systems can be deeply integrated into your workspace.</span></span> <span data-ttu-id="b7c48-166">Sonraki toofull mobility (örneğin indirme/karşıya), ayrıntılı denetimler ile tam kullanımını denetleme, çok faktörlü kimlik doğrulaması (örneğin, Azure MFA), oturum kaydı ve daha fazlasını en iyi güvenlik Awingu'nın zengin çevrimiçi çalışma verin.</span><span class="sxs-lookup"><span data-stu-id="b7c48-166">Next toofull mobility, Awingu's rich online workspace will give optimal security with granular controls (e.g. downloading/uploading), full usage auditing, Multi-Factor Authentication (e.g. Azure MFA), session recording and more.</span></span> <span data-ttu-id="b7c48-167">Out-of--box, belge ve en iyi duruma getirilmiş ve güvenli işbirliği için uygulama paylaşım oturumu Awingu sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7c48-167">Out-of-the-box, Awingu enables document and application session sharing for optimized and secure collaboration.</span></span>
<span data-ttu-id="b7c48-168">Awingu'nin, çok kiracılı, birden çok AD ve açık API çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="b7c48-168">Awingu's solution is multi-tenant, multi-AD and open API.</span></span> <span data-ttu-id="b7c48-169">Küçük ve büyük işletmeler tarafından bulut hizmet sağlayıcılarının kullanılır ve [ISV'ler](http://www.isv2saas.com).</span><span class="sxs-lookup"><span data-stu-id="b7c48-169">It is used by small and large businesses, Cloud Service Providers and [ISVs](http://www.isv2saas.com).</span></span> <span data-ttu-id="b7c48-170">Bu müşterilerden Merhaba, kullanımı kolay, özellikle yönetilmesinde kolaylığı yükleme ve düşük toplam sahip olma maliyeti.</span><span class="sxs-lookup"><span data-stu-id="b7c48-170">These customers especially appreciate hello easy-of-use, ease-to-install and low TCO.</span></span>

<span data-ttu-id="b7c48-171">Awingu hepsi bir arada olan [hello Azure Marketi'nde bulunan](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) 2 yerleşik eşzamanlı kullanıcılarla.</span><span class="sxs-lookup"><span data-stu-id="b7c48-171">Awingu All-in-One is [available in hello Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) with 2 built-in concurrent users.</span></span> <span data-ttu-id="b7c48-172">Ek lisanslar aracılığıyla kullanılabilen bir [Dağıtıcıları ve yetkili satıcılar çeşitli](http://www.awingu.com/reseller).</span><span class="sxs-lookup"><span data-stu-id="b7c48-172">Additional licenses are available through a [wide range of distributors and resellers](http://www.awingu.com/reseller).</span></span>

<span data-ttu-id="b7c48-173">Daha fazla bilgi edinmek [üzerinde Awingu alternatif tooAzure RemoteApp olarak](http://alternative-for-azure-remoteapp.awingu.com/).</span><span class="sxs-lookup"><span data-stu-id="b7c48-173">Learn more about [Awingu on as alternative tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).</span></span>


> <span data-ttu-id="b7c48-174">Birincil konumu: Belçika</span><span class="sxs-lookup"><span data-stu-id="b7c48-174">Primary location: Belgium</span></span>
> 
> <span data-ttu-id="b7c48-175">Bölgeler işletim: EMEA, Kuzey Amerika ve Brezilya</span><span class="sxs-lookup"><span data-stu-id="b7c48-175">Operating regions: EMEA, North America and Brazil</span></span>
> 
> <span data-ttu-id="b7c48-176">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-176">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span> 
> 
> <span data-ttu-id="b7c48-177">**Genel**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-177">**Global**:</span></span>
> 
> <span data-ttu-id="b7c48-178">Arnaud Marlière, CMO</span><span class="sxs-lookup"><span data-stu-id="b7c48-178">Arnaud Marlière, CMO</span></span>
> 
> <span data-ttu-id="b7c48-179">E-posta:[arnaud@awingu.com](mailto:arnaud@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="b7c48-179">Email: [arnaud@awingu.com](mailto:arnaud@awingu.com)</span></span>
> 
> <span data-ttu-id="b7c48-180">Telefon: +1 646 583 3025</span><span class="sxs-lookup"><span data-stu-id="b7c48-180">Phone: +1 646 583 3025</span></span>
> 
> <span data-ttu-id="b7c48-181">**Belçika denetim merkezini**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-181">**Belgium HQ**:</span></span>
> 
> <span data-ttu-id="b7c48-182">Ottergemsesteenweg Zuid 808 B44</span><span class="sxs-lookup"><span data-stu-id="b7c48-182">Ottergemsesteenweg-Zuid 808 B44</span></span>
> 
> <span data-ttu-id="b7c48-183">9000 Gent</span><span class="sxs-lookup"><span data-stu-id="b7c48-183">9000 Gent</span></span>
> 
> <span data-ttu-id="b7c48-184">E-posta:[info@awingu.com](mailto:info@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="b7c48-184">Email: [info@awingu.com](mailto:info@awingu.com)</span></span> 
> 
> <span data-ttu-id="b7c48-185">Telefon: + 32 9 296 40 11</span><span class="sxs-lookup"><span data-stu-id="b7c48-185">Phone: +32 9 296 40 11</span></span>
> 
> <span data-ttu-id="b7c48-186">**ABD**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-186">**USA**:</span></span>
> 
> <span data-ttu-id="b7c48-187">7 floor, hello Americas, 1177 Ave,</span><span class="sxs-lookup"><span data-stu-id="b7c48-187">7th floor, 1177 Ave of hello Americas,</span></span>
> 
> <span data-ttu-id="b7c48-188">New York, NY 10036</span><span class="sxs-lookup"><span data-stu-id="b7c48-188">New York, NY 10036</span></span>
> 
> <span data-ttu-id="b7c48-189">E-posta:[info.us@awingu.com](mailto:info.us@awingu.com)</span><span class="sxs-lookup"><span data-stu-id="b7c48-189">Email: [info.us@awingu.com](mailto:info.us@awingu.com)</span></span>

### <a name="microsoft-hosted-service-provider"></a><span data-ttu-id="b7c48-190">Microsoft hizmet sağlayıcısı barındırılan</span><span class="sxs-lookup"><span data-stu-id="b7c48-190">Microsoft Hosted Service Provider</span></span>
<span data-ttu-id="b7c48-191">Barındırma ortakları genellikle sunma tam olarak yönetilen Windows Masaüstü barındırılan ve yönetme içerebilir uygulama hizmeti hello Azure kaynaklarını, işletim sistemleri, uygulamaları ve Yardım Masası hello ortağı kullanarak Microsoft anlaşmalarıyla lisans ve bir hizmet sağlayıcısı lisans sözleşmenize tooallow abone erişim lisansı (SAL), satılması olan yanı sıra diğer yazılım sağlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="b7c48-191">Hosting partners typically offer a fully managed hosted Windows desktop and application service, which may include managing hello Azure resources, operating systems, applications, and helpdesk using hello partner's licensing agreements with Microsoft and other software providers along with being a Service Provider License Agreement tooallow reselling of Subscriber Access License (SAL).</span></span> <span data-ttu-id="b7c48-192">Merhaba aşağıdaki bilgileri ayrıntılarını ve bunların Azure RemoteApp geçiş müşterilerle yardımcı olarak specialize hello barındırıcıların bazıları için kişi bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7c48-192">hello following information provides details and contact information for some of hello hosters that specialize in assisting customers with their Azure RemoteApp migration.</span></span> <span data-ttu-id="b7c48-193">Kullanıma [hello geçerli barındırılan hizmet sağlayıcıların listesini](http://aka.ms/rdsonazurecertified) hello yolu ve değerlendirme öğrenme Iaas üzerinde RDS tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b7c48-193">Check out [hello current list of Hosted Service Providers](http://aka.ms/rdsonazurecertified) that have completed hello RDS on IaaS learning path and assessment.</span></span>  

### <a name="citrix-service-provider-program"></a><span data-ttu-id="b7c48-194">Citrix hizmet sağlayıcısı programı</span><span class="sxs-lookup"><span data-stu-id="b7c48-194">Citrix Service Provider Program</span></span>
<span data-ttu-id="b7c48-195">Merhaba Citrix hizmet sağlayıcısı programı tooSMBs bilgi işlem, bir kolay, Kullandıkça Öde modelinde istedikleri hello hizmetleri sunan sanal bulut hizmeti sağlayıcıları toodeliver hello basitliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="b7c48-195">hello Citrix Service Provider Program makes it easy for service providers toodeliver hello simplicity of virtual cloud computing tooSMBs, offering them hello services they want in an easy, pay-as-you-go model.</span></span> <span data-ttu-id="b7c48-196">Citrix hizmet sağlayıcıları, Microsoft SPLA işlerini büyümesine ve kendi RDS platform Yatırımlar ile herhangi bir aygıtı genişletin, her yerden erişim, en geniş uygulama desteği, bir zengin deneyim, ek güvenlik ve daha yüksek ölçeklenebilirliği hello.</span><span class="sxs-lookup"><span data-stu-id="b7c48-196">Citrix Service Providers grow their Microsoft SPLA businesses and expand their RDS platform investments with any device, anywhere access, hello broadest application support, a rich experience, added security and increased scalability.</span></span> <span data-ttu-id="b7c48-197">Buna karşılık, Citrix hizmet sağlayıcıları daha fazla aboneleri çekebilir, müşteri memnuniyetini artırmak ve kendi işletim maliyetlerini düşürme.</span><span class="sxs-lookup"><span data-stu-id="b7c48-197">In turn, Citrix Service Providers attract more subscribers, increase customer satisfaction and reduce their operational costs.</span></span> <span data-ttu-id="b7c48-198">[Daha fazla bilgi edinin](http://www.citrix.com/products/service-providers.html) veya [bir iş ortağı bulmak](https://www.citrix.com/buy/partnerlocator.html).</span><span class="sxs-lookup"><span data-stu-id="b7c48-198">[Learn more](http://www.citrix.com/products/service-providers.html) or [find a partner](https://www.citrix.com/buy/partnerlocator.html).</span></span>

#### <a name="acuutech"></a><span data-ttu-id="b7c48-199">Acuutech</span><span class="sxs-lookup"><span data-stu-id="b7c48-199">Acuutech</span></span>
<span data-ttu-id="b7c48-200">[Acuutech](http://www.acuutech.com) tam masaüstü ve ISV uygulamaları teslim etmek barındırılan Masaüstü çözümleri sağlama uzmanlaşmış Microsoft teknolojisi tooa genel istemcide temel Azure ve kendi veri merkezlerini yerleşik deneyimleri.</span><span class="sxs-lookup"><span data-stu-id="b7c48-200">[Acuutech](http://www.acuutech.com) specializes in providing hosted desktop solutions, delivering full desktop and ISV applications experiences built on Microsoft technology tooa global client base from Azure and their own datacenters.</span></span>

> <span data-ttu-id="b7c48-201">Birincil konumu: Londra, İngiltere; Singapur; Houston, TX</span><span class="sxs-lookup"><span data-stu-id="b7c48-201">Primary location: London, UK; Singapore; Houston, TX</span></span>
> 
> <span data-ttu-id="b7c48-202">İşlemi bölgesi: dünya çapında</span><span class="sxs-lookup"><span data-stu-id="b7c48-202">Operation region: Worldwide</span></span>
> 
> <span data-ttu-id="b7c48-203">İş ortağı durumu: altın</span><span class="sxs-lookup"><span data-stu-id="b7c48-203">Partner status: Gold</span></span>
> 
> <span data-ttu-id="b7c48-204">Microsoft bulut hizmeti sağlayıcısı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-204">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="b7c48-205">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-205">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="b7c48-206">Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](http://www.acuutech.com/ara-migration/)</span><span class="sxs-lookup"><span data-stu-id="b7c48-206">Azure RemoteApp migration solutions: Yes, [learn more](http://www.acuutech.com/ara-migration/)</span></span>
> 
> <span data-ttu-id="b7c48-207">**Birleşik Krallık**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-207">**United Kingdom**:</span></span>
>   
> <span data-ttu-id="b7c48-208">5/6 York House, Langston yol,</span><span class="sxs-lookup"><span data-stu-id="b7c48-208">5/6 York House, Langston Road,</span></span>
>   
> <span data-ttu-id="b7c48-209">Loughton, Essex IG10 3TQ</span><span class="sxs-lookup"><span data-stu-id="b7c48-209">Loughton, Essex IG10 3TQ</span></span>
>   
> <span data-ttu-id="b7c48-210">Telefon: + 44 (0) 20 8502 2155</span><span class="sxs-lookup"><span data-stu-id="b7c48-210">Phone: +44 (0) 20 8502 2155</span></span>
> 
> <span data-ttu-id="b7c48-211">**Singapur**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-211">**Singapore**:</span></span>
>   
> <span data-ttu-id="b7c48-212">100 CECIL Sokak, #09-02,</span><span class="sxs-lookup"><span data-stu-id="b7c48-212">100 Cecil Street, #09-02,</span></span> 
>   
> <span data-ttu-id="b7c48-213">Merhaba Dünya, Singapur 069532</span><span class="sxs-lookup"><span data-stu-id="b7c48-213">hello Globe, Singapore 069532</span></span>
> 
> <span data-ttu-id="b7c48-214">Telefon: + 65 6709 4933</span><span class="sxs-lookup"><span data-stu-id="b7c48-214">Phone: +65 6709 4933</span></span>
>   
> <span data-ttu-id="b7c48-215">**Kuzey Amerika**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-215">**North America**:</span></span>
>   
> <span data-ttu-id="b7c48-216">3601 S. Sandman St.</span><span class="sxs-lookup"><span data-stu-id="b7c48-216">3601 S. Sandman St.</span></span>
>   
> <span data-ttu-id="b7c48-217">Paketi 200, Houston, TX 77098</span><span class="sxs-lookup"><span data-stu-id="b7c48-217">Suite 200, Houston, TX 77098</span></span>
>   
> <span data-ttu-id="b7c48-218">Telefon: +1 713 691 0800</span><span class="sxs-lookup"><span data-stu-id="b7c48-218">Phone: +1 713 691 0800</span></span>

#### <a name="aspex"></a><span data-ttu-id="b7c48-219">ASPEX</span><span class="sxs-lookup"><span data-stu-id="b7c48-219">ASPEX</span></span>
<span data-ttu-id="b7c48-220">[ASPEX](http://www.aspex.be/en) toohello Bulut ve ISV geçiş ISV'ler içinde uzmanlaşmış ' toooptimize geçerli kendi bulut kurulumları aranıyor.</span><span class="sxs-lookup"><span data-stu-id="b7c48-220">[ASPEX](http://www.aspex.be/en) specializes in ISVs transitioning toohello Cloud and ISV‘ looking toooptimize their current cloud setups.</span></span> <span data-ttu-id="b7c48-221">ASPEX çok çeşitli yönetilen Hizmetleri, devops ve danışmanlık hizmetleri sunar.</span><span class="sxs-lookup"><span data-stu-id="b7c48-221">ASPEX offers a wide range of managed services, devops, and consulting services.</span></span>  

> <span data-ttu-id="b7c48-222">Birincil konumu: Antwerp, Belçika</span><span class="sxs-lookup"><span data-stu-id="b7c48-222">Primary location: Antwerp, Belgium</span></span>
> 
> <span data-ttu-id="b7c48-223">İşlemi bölgesi: Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="b7c48-223">Operation region: Western Europe</span></span>
> 
> <span data-ttu-id="b7c48-224">İş ortağı, durum: [Gümüş](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span><span class="sxs-lookup"><span data-stu-id="b7c48-224">Partner status: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)</span></span>
> 
> <span data-ttu-id="b7c48-225">Microsoft bulut hizmeti sağlayıcısı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-225">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="b7c48-226">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-226">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="b7c48-227">Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](https://www.aspex.be/en/azure-remote-apps)</span><span class="sxs-lookup"><span data-stu-id="b7c48-227">Azure RemoteApp migration solutions: Yes, [learn more](https://www.aspex.be/en/azure-remote-apps)</span></span>
> 
> <span data-ttu-id="b7c48-228">Telefon: +3232202198</span><span class="sxs-lookup"><span data-stu-id="b7c48-228">Phone: +3232202198</span></span>
> 
> <span data-ttu-id="b7c48-229">Posta:[info@aspex.be](mailto:info@aspex.be)</span><span class="sxs-lookup"><span data-stu-id="b7c48-229">Mail: [info@aspex.be](mailto:info@aspex.be)</span></span>
> 
> <span data-ttu-id="b7c48-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span><span class="sxs-lookup"><span data-stu-id="b7c48-230">Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)</span></span>

#### <a name="caasecom"></a><span data-ttu-id="b7c48-231">Caase.com</span><span class="sxs-lookup"><span data-stu-id="b7c48-231">Caase.com</span></span>
<span data-ttu-id="b7c48-232">[Caase.com](http://www.caase.com/) işletmeler, yerel hükümetler, kamu olmayan gövdeleri ve bunların gezisine hello Microsoft Cloud iş daha verimli bir şekilde doğru sağlık kuruluşlarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b7c48-232">[Caase.com](http://www.caase.com/) helps businesses, local governments, non-governmental bodies and healthcare institutions with their journey towards a smarter way of work in hello Microsoft Cloud.</span></span> <span data-ttu-id="b7c48-233">Herhangi bir aygıt ile herhangi bir yerdeki ve düşük BT maliyetle güvenli ve verimli olması.</span><span class="sxs-lookup"><span data-stu-id="b7c48-233">Being productive and secure at any place, with any device and at low IT cost.</span></span> <span data-ttu-id="b7c48-234">Caase.com Microsoft Office365, Azure, Enterprise Mobility ve güvenlik ve Windows için doğru Uzmanı ' dir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-234">Caase.com is a true specialist for Microsoft Office365, Azure, Enterprise Mobility and Security and Windows.</span></span> <span data-ttu-id="b7c48-235">Bizim danışmanlık firması, yükseltme Hizmetleri, benimseme programlar, eğitim ile yönetim ve Destek Caase.com işbirliği hem müşterilerin çalışanlar, iş ortakları ve hangi tedarikçilerin en iyi duruma getirilmiş ve güvenli bir platform oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b7c48-235">With our consultancy, migration services, adoption programs, training, management and support Caase.com creates an optimized and secure platform for collaboration for both customers’ employees, partners and suppliers.</span></span>
<span data-ttu-id="b7c48-236">Caase.com hello beyin hello Azure uzak çalışma alanı (mobil çalışma alanı) ve hello dijital çalışma alanına (sosyal Intranet) olur.</span><span class="sxs-lookup"><span data-stu-id="b7c48-236">Caase.com is hello mastermind of hello Azure Remote Workspace (mobile workplace) and hello Digital Workplace (Social Intranet).</span></span> <span data-ttu-id="b7c48-237">– Benimseme elde her iki çözüm – bu çözümlerin hello kullanıcılar kendi rota toohello Microsoft Cloud hello en eğlenceli, başarılı ve etkili deneyim sahibi olduğunuzu sağlayan hello temelidir.</span><span class="sxs-lookup"><span data-stu-id="b7c48-237">Both solutions – accomplished with adoption – are hello foundation which ensures that hello users of these solutions have hello most pleasant, successful and effective experience in their route toohello Microsoft Cloud.</span></span>
<span data-ttu-id="b7c48-238">Felemenkçe çeviri ánd burada üzerinden destekleyen bir filmi: http://caase.com/over-ons/</span><span class="sxs-lookup"><span data-stu-id="b7c48-238">Dutch translation ánd a supporting movie over here: http://caase.com/over-ons/</span></span>

> <span data-ttu-id="b7c48-239">İşlemi bölgesi: Felemenkçe bağlı olarak, genel erişim</span><span class="sxs-lookup"><span data-stu-id="b7c48-239">Operation region: Dutch based, global reach</span></span>
> 
> <span data-ttu-id="b7c48-240">İş ortağı, durum: [altın](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span><span class="sxs-lookup"><span data-stu-id="b7c48-240">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)</span></span>
> 
> <span data-ttu-id="b7c48-241">Microsoft bulut hizmeti sağlayıcısı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-241">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="b7c48-242">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-242">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="b7c48-243">Azure RemoteApp geçiş çözümleri: Evet, [daha fazla bilgi edinin](http://caase.com/diensten/microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="b7c48-243">Azure RemoteApp migration solutions: Yes, [learn more](http://caase.com/diensten/microsoft-azure/).</span></span>
> 
> 
> <span data-ttu-id="b7c48-244">Hollanda:</span><span class="sxs-lookup"><span data-stu-id="b7c48-244">Netherlands:</span></span>
> 
> <span data-ttu-id="b7c48-245">Rigtersbleek Zandvoort 10 (De Spinnerij)</span><span class="sxs-lookup"><span data-stu-id="b7c48-245">Rigtersbleek-Zandvoort 10 (De Spinnerij)</span></span>
> 
> <span data-ttu-id="b7c48-246">7521 BE, Enschede</span><span class="sxs-lookup"><span data-stu-id="b7c48-246">7521 BE, Enschede</span></span>
> 
> <span data-ttu-id="b7c48-247">Telefon: +31 (0) 88 4320 000</span><span class="sxs-lookup"><span data-stu-id="b7c48-247">Phone: +31 (0) 88 4320 000</span></span>


#### <a name="nerdio"></a><span data-ttu-id="b7c48-248">Nerdio</span><span class="sxs-lookup"><span data-stu-id="b7c48-248">Nerdio</span></span>
<span data-ttu-id="b7c48-249">[Azure için Nerdio](http://getnerdio.com/nfa/) gerçekten basit sağlama, yönetim ve tam BT ortamları en iyi duruma getirilmesi hello Microsoft bulut sunan bir BT Otomasyon platformudur.</span><span class="sxs-lookup"><span data-stu-id="b7c48-249">[Nerdio for Azure](http://getnerdio.com/nfa/) is an IT automation platform that delivers ridiculously simple provisioning, management and optimization of complete IT environments in hello Microsoft cloud.</span></span> <span data-ttu-id="b7c48-250">Sanal Masaüstlerini, uzak uygulamalar ve sunucuları birkaç saat bekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7c48-250">Stand up virtual desktops, remote apps and servers in a couple of hours.</span></span> <span data-ttu-id="b7c48-251">Üç tıklama Hello ortamında yönetmek veya Nerdio Yönetim Portalı ile daha az.</span><span class="sxs-lookup"><span data-stu-id="b7c48-251">Administer hello environment in three clicks or less with Nerdio Admin Portal.</span></span> <span data-ttu-id="b7c48-252">Akıllı otomatik ölçeklendirme kullanın ve Azure Iaas kaynaklarında 40 too60% kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b7c48-252">Use intelligent auto-scaling and save 40 too60% in Azure IaaS resources.</span></span>

> <span data-ttu-id="b7c48-253">Birincil konumu: Chicago, IL işlemi bölgesi: dünya çapında iş ortağı durumu: [altın](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft bulut hizmeti sağlayıcısı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-253">Primary location: Chicago, IL Operation region: Worldwide Partner status: [Gold](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="b7c48-254">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-254">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="b7c48-255">Azure RemoteApp geçiş çözümleri: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-255">Azure RemoteApp migration solutions: Yes</span></span>
> 
> 
> <span data-ttu-id="b7c48-256">8001 Lincoln Ave</span><span class="sxs-lookup"><span data-stu-id="b7c48-256">8001 Lincoln Ave</span></span>
> 
> <span data-ttu-id="b7c48-257">Paketi 212</span><span class="sxs-lookup"><span data-stu-id="b7c48-257">Suite 212</span></span>
> 
> <span data-ttu-id="b7c48-258">IL Skokie, 60077</span><span class="sxs-lookup"><span data-stu-id="b7c48-258">Skokie, IL 60077</span></span>
> 
> <span data-ttu-id="b7c48-259">ABD</span><span class="sxs-lookup"><span data-stu-id="b7c48-259">USA</span></span>
> 
> <span data-ttu-id="b7c48-260">(844) 4NERDIO dahili 6</span><span class="sxs-lookup"><span data-stu-id="b7c48-260">(844) 4NERDIO ext. 6</span></span>
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a><span data-ttu-id="b7c48-261">**SaaSplaza**</span><span class="sxs-lookup"><span data-stu-id="b7c48-261">**SaaSplaza**</span></span>
<span data-ttu-id="b7c48-262">[SaaSplaza](http://www.saasplaza.com/) tam Microsoft Dynamics Portföy (NAV, AX, GP, SL, CRM) özel ve genel buluta (Azure'a) sunar.</span><span class="sxs-lookup"><span data-stu-id="b7c48-262">[SaaSplaza](http://www.saasplaza.com/) offers complete Microsoft Dynamics portfolio (NAV, AX, GP, SL, CRM) private and public cloud (Azure).</span></span>

> <span data-ttu-id="b7c48-263">Birincil konumu: Hollanda</span><span class="sxs-lookup"><span data-stu-id="b7c48-263">Primary location: Netherlands</span></span>
> 
> <span data-ttu-id="b7c48-264">İşlemi bölgesi: dünya çapında</span><span class="sxs-lookup"><span data-stu-id="b7c48-264">Operation Region: Worldwide</span></span>
> 
> <span data-ttu-id="b7c48-265">İş ortağı, durum: [altın](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span><span class="sxs-lookup"><span data-stu-id="b7c48-265">Partner status: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)</span></span>
> 
> <span data-ttu-id="b7c48-266">Microsoft bulut hizmeti sağlayıcısı: Evet</span><span class="sxs-lookup"><span data-stu-id="b7c48-266">Microsoft Cloud Service Provider: Yes</span></span>
> 
> <span data-ttu-id="b7c48-267">Oturum tabanlı RemoteApp ve Masaüstü çözümleri sunar: Evet, her ikisi</span><span class="sxs-lookup"><span data-stu-id="b7c48-267">Offer session-based RemoteApp and Desktop solutions: Yes, both</span></span>
> 
> <span data-ttu-id="b7c48-268">**EMEA**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-268">**EMEA**:</span></span>
> 
> <span data-ttu-id="b7c48-269">Prins Mauritslaan 29-35</span><span class="sxs-lookup"><span data-stu-id="b7c48-269">Prins Mauritslaan 29-35</span></span>
> 
> <span data-ttu-id="b7c48-270">71 LP Badhoevedorp</span><span class="sxs-lookup"><span data-stu-id="b7c48-270">71 LP Badhoevedorp</span></span>
> 
> <span data-ttu-id="b7c48-271">Merhaba Hollanda</span><span class="sxs-lookup"><span data-stu-id="b7c48-271">hello Netherlands</span></span>
> 
> <span data-ttu-id="b7c48-272">Telefon: +31 20 547 8060</span><span class="sxs-lookup"><span data-stu-id="b7c48-272">Phone: +31 20 547 8060</span></span> 
> 
>  <span data-ttu-id="b7c48-273">**Kuzey ve Güney Amerika**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-273">**Americas**:</span></span>
> 
> <span data-ttu-id="b7c48-274">171 Sakson yol, paketi 105</span><span class="sxs-lookup"><span data-stu-id="b7c48-274">171 Saxony Road, Suite 105</span></span>
> 
> <span data-ttu-id="b7c48-275">Encinitas, CA 92024</span><span class="sxs-lookup"><span data-stu-id="b7c48-275">Encinitas, CA 92024</span></span>
> 
> <span data-ttu-id="b7c48-276">San Diego</span><span class="sxs-lookup"><span data-stu-id="b7c48-276">San Diego</span></span>
> 
> <span data-ttu-id="b7c48-277">Amerika Birleşik Devletleri</span><span class="sxs-lookup"><span data-stu-id="b7c48-277">United States</span></span>
> 
> <span data-ttu-id="b7c48-278">Telefon: +1 858 385 8900</span><span class="sxs-lookup"><span data-stu-id="b7c48-278">Phone: +1 858 385 8900</span></span> 
> 
> <span data-ttu-id="b7c48-279">**APAC**:</span><span class="sxs-lookup"><span data-stu-id="b7c48-279">**APAC**:</span></span>
> 
> <span data-ttu-id="b7c48-280">105 CECIL Sokak</span><span class="sxs-lookup"><span data-stu-id="b7c48-280">105 Cecil Street</span></span>
>    
> <span data-ttu-id="b7c48-281">\#11-08 hello Sekizgene</span><span class="sxs-lookup"><span data-stu-id="b7c48-281">\#11-08, hello Octagon</span></span>
> 
> <span data-ttu-id="b7c48-282">Singapur 069534</span><span class="sxs-lookup"><span data-stu-id="b7c48-282">Singapore 069534</span></span>
> 
> <span data-ttu-id="b7c48-283">Singapur</span><span class="sxs-lookup"><span data-stu-id="b7c48-283">Singapore</span></span>
>   
> <span data-ttu-id="b7c48-284">Telefon - Singapur: + 65 6222 6591</span><span class="sxs-lookup"><span data-stu-id="b7c48-284">Phone - Singapore: +65 6222 6591</span></span>
> 
> <span data-ttu-id="b7c48-285">Telefon - Avustralya: +61 2 8310 5568</span><span class="sxs-lookup"><span data-stu-id="b7c48-285">Phone - Australia: +61 2 8310 5568</span></span> 
>    
> <span data-ttu-id="b7c48-286">Telefon - Yeni Zelanda: + 64 4 488 0321</span><span class="sxs-lookup"><span data-stu-id="b7c48-286">Phone - New Zealand: +64 4 488 0321</span></span>
> 
## <a name="need-more-help"></a><span data-ttu-id="b7c48-287">Daha fazla yardım gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="b7c48-287">Need more help?</span></span>
<span data-ttu-id="b7c48-288">Hala seçme Yardım veya başka sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="b7c48-288">Still need help choosing or have further questions?</span></span> <span data-ttu-id="b7c48-289">Yöntemleri tooget Yardım aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b7c48-289">Use one of hello following methods tooget help.</span></span> 

1. <span data-ttu-id="b7c48-290">Adresinden bize e-posta [ arainfo@microsoft.com ](mailto:arainfo@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b7c48-290">Email us at [arainfo@microsoft.com](mailto:arainfo@microsoft.com).</span></span>
2. <span data-ttu-id="b7c48-291">Kişi [Azure Destek](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="b7c48-291">Contact [Azure support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span> <span data-ttu-id="b7c48-292">Başlangıç açarak bir [Azure destek servis talebi](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span><span class="sxs-lookup"><span data-stu-id="b7c48-292">Start by opening an [Azure support case](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).</span></span>
3. <span data-ttu-id="b7c48-293">Bizi arayın.</span><span class="sxs-lookup"><span data-stu-id="b7c48-293">Call us.</span></span> <span data-ttu-id="b7c48-294">[Yerel bir satış numarasını bulmak](https://azure.microsoft.com/overview/sales-number/).</span><span class="sxs-lookup"><span data-stu-id="b7c48-294">[Find a local sales number](https://azure.microsoft.com/overview/sales-number/).</span></span>

