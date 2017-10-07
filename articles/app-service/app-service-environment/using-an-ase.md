---
title: "aaaUse Azure uygulama hizmeti ortamı"
description: "Nasıl toocreate, yayımlama ve uygulamaları Azure uygulama hizmeti ortamı ölçeklendirme"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a><span data-ttu-id="44f78-103">Bir uygulama hizmeti ortamı'nı kullanma</span><span class="sxs-lookup"><span data-stu-id="44f78-103">Use an App Service environment</span></span> #

## <a name="overview"></a><span data-ttu-id="44f78-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="44f78-104">Overview</span></span> ##

<span data-ttu-id="44f78-105">Azure uygulama hizmeti ortamı bir Azure uygulama hizmeti dağıtımı bir müşterinin Azure sanal ağındaki bir alt ağ ile değil.</span><span class="sxs-lookup"><span data-stu-id="44f78-105">Azure App Service Environment is a deployment of Azure App Service into a subnet in a customer’s Azure virtual network.</span></span> <span data-ttu-id="44f78-106">Aşağıdakilerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="44f78-106">It consists of:</span></span>

- <span data-ttu-id="44f78-107">**Ön Uçları**: hello ön uçlar olduğunuz nerede bir uygulama hizmeti ortamı'nda (ana) HTTP/HTTPS sonlandırır.</span><span class="sxs-lookup"><span data-stu-id="44f78-107">**Front ends**: hello front ends are where HTTP/HTTPS terminates in an App Service environment (ASE).</span></span>
- <span data-ttu-id="44f78-108">**Çalışanlar**: hello çalışanlardır uygulamalarınızı barındırmak hello kaynakları.</span><span class="sxs-lookup"><span data-stu-id="44f78-108">**Workers**: hello workers are hello resources that host your apps.</span></span>
- <span data-ttu-id="44f78-109">**Veritabanı**: hello veritabanı hello ortamı tanımlayan bilgileri tutar.</span><span class="sxs-lookup"><span data-stu-id="44f78-109">**Database**: hello database holds information that defines hello environment.</span></span>
- <span data-ttu-id="44f78-110">**Depolama**: hello depolama olduğu kullanılan toohost hello müşteri yayımlanan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="44f78-110">**Storage**: hello storage is used toohost hello customer-published apps.</span></span>

> [!NOTE]
> <span data-ttu-id="44f78-111">Uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2.</span><span class="sxs-lookup"><span data-stu-id="44f78-111">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="44f78-112">ASEv1 içinde kullanabilmek için önce hello kaynakları yönetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44f78-112">In ASEv1, you must manage hello resources before you can use them.</span></span> <span data-ttu-id="44f78-113">toolearn nasıl tooconfigure ve ASEv1 yönetmek için bkz: [bir uygulama hizmeti ortamı v1 yapılandırma][ConfigureASEv1].</span><span class="sxs-lookup"><span data-stu-id="44f78-113">toolearn how tooconfigure and manage ASEv1, see [Configure an App Service environment v1][ConfigureASEv1].</span></span> <span data-ttu-id="44f78-114">Merhaba, bu makalenin kalanında ASEv2 odaklanır.</span><span class="sxs-lookup"><span data-stu-id="44f78-114">hello rest of this article focuses on ASEv2.</span></span>
>
>

<span data-ttu-id="44f78-115">Uygulama erişimi için bir harici veya dahili VIP ile bir ana (ASEv1 ve ASEv2) dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-115">You can deploy an ASE (ASEv1 and ASEv2) with an external or internal VIP for app access.</span></span> <span data-ttu-id="44f78-116">bir dış VIP ile Merhaba dağıtımı genellikle bir dış ana olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="44f78-116">hello deployment with an external VIP is commonly called an External ASE.</span></span> <span data-ttu-id="44f78-117">bir iç yük dengeleyici (ILB) kullandığından hello iç sürüm hello ILB ana adı verilir.</span><span class="sxs-lookup"><span data-stu-id="44f78-117">hello internal version is called hello ILB ASE because it uses an internal load balancer (ILB).</span></span> <span data-ttu-id="44f78-118">toolearn hello ILB ana hakkında daha fazla bilgi görmek [oluşturma ve kullanma bir ILB ana][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="44f78-118">toolearn more about hello ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span>

## <a name="create-a-web-app-in-an-ase"></a><span data-ttu-id="44f78-119">ASE'de bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="44f78-119">Create a web app in an ASE</span></span> ##

<span data-ttu-id="44f78-120">toocreate bir ana web uygulamasında, ne zaman normalde oluşturmak, ancak bazı küçük farklar ile aynı işlemi hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="44f78-120">toocreate a web app in an ASE, you use hello same process as when you create it normally, but with a few small differences.</span></span> <span data-ttu-id="44f78-121">Yeni bir uygulama hizmeti planı oluşturduğunuzda:</span><span class="sxs-lookup"><span data-stu-id="44f78-121">When you create a new App Service plan:</span></span>

- <span data-ttu-id="44f78-122">Uygulamanızın hangi toodeploy coğrafi bir konum seçmek yerine bir ana konumunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="44f78-122">Instead of choosing a geographic location in which toodeploy your app, you choose an ASE as your location.</span></span>
- <span data-ttu-id="44f78-123">ASE'de oluşturulan tüm uygulama hizmeti planları, fiyatlandırma katmanı bir Isolated olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44f78-123">All App Service plans created in an ASE must be in an Isolated pricing tier.</span></span>

<span data-ttu-id="44f78-124">Bir ana yoksa, bir hello yönergeleri izleyerek oluşturabilirsiniz [uygulama hizmeti ortamı oluşturma][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="44f78-124">If you don't have an ASE, you can create one by following hello instructions in [Create an App Service environment][MakeExternalASE].</span></span>

<span data-ttu-id="44f78-125">bir ana web uygulamasında toocreate:</span><span class="sxs-lookup"><span data-stu-id="44f78-125">toocreate a web app in an ASE:</span></span>

1. <span data-ttu-id="44f78-126">Seçin **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="44f78-126">Select **New** > **Web + Mobile** > **Web App**.</span></span>

2. <span data-ttu-id="44f78-127">Merhaba web uygulaması için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="44f78-127">Enter a name for hello web app.</span></span> <span data-ttu-id="44f78-128">ASE'de zaten bir uygulama hizmeti planı seçtiyseniz hello uygulamasının hello etki alanı adı hello ana etki alanı adını hello yansıtır.</span><span class="sxs-lookup"><span data-stu-id="44f78-128">If you already selected an App Service plan in an ASE, hello domain name for hello app reflects hello domain name of hello ASE.</span></span>

    ![Web uygulaması adı seçimi][1]

3. <span data-ttu-id="44f78-130">Bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="44f78-130">Select a subscription.</span></span>

4. <span data-ttu-id="44f78-131">Yeni bir kaynak grubu için bir ad girin veya seçin **var olanı kullan** bir hello aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="44f78-131">Enter a name for a new resource group, or select **Use existing** and select one from hello drop-down list.</span></span>

5. <span data-ttu-id="44f78-132">Var olan bir uygulama hizmeti planı, ana seçin veya aşağıdaki adımları izleyerek yeni bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="44f78-132">Select an existing App Service plan in your ASE, or create a new one by following these steps:</span></span>

    <span data-ttu-id="44f78-133">a.</span><span class="sxs-lookup"><span data-stu-id="44f78-133">a.</span></span> <span data-ttu-id="44f78-134">Seçin **Yeni Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="44f78-134">Select **Create New**.</span></span>

    <span data-ttu-id="44f78-135">b.</span><span class="sxs-lookup"><span data-stu-id="44f78-135">b.</span></span> <span data-ttu-id="44f78-136">Uygulama hizmeti planınız için Hello adı girin.</span><span class="sxs-lookup"><span data-stu-id="44f78-136">Enter hello name for your App Service plan.</span></span>

    <span data-ttu-id="44f78-137">c.</span><span class="sxs-lookup"><span data-stu-id="44f78-137">c.</span></span> <span data-ttu-id="44f78-138">Ana hello seçin **konumu** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="44f78-138">Select your ASE in hello **Location** drop-down list.</span></span>

    <span data-ttu-id="44f78-139">d.</span><span class="sxs-lookup"><span data-stu-id="44f78-139">d.</span></span> <span data-ttu-id="44f78-140">Seçin bir **Isolated** fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="44f78-140">Select an **Isolated** pricing tier.</span></span> <span data-ttu-id="44f78-141">Seçin **seçin**.</span><span class="sxs-lookup"><span data-stu-id="44f78-141">Select **Select**.</span></span>

    <span data-ttu-id="44f78-142">e.</span><span class="sxs-lookup"><span data-stu-id="44f78-142">e.</span></span> <span data-ttu-id="44f78-143">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="44f78-143">Select **OK**.</span></span>
    
    ![Yalıtılmış fiyatlandırma katmanları][2]

6. <span data-ttu-id="44f78-145">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="44f78-145">Select **Create**.</span></span>

## <a name="how-scale-works"></a><span data-ttu-id="44f78-146">Nasıl çalışır ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="44f78-146">How scale works</span></span> ##

<span data-ttu-id="44f78-147">Her uygulama hizmeti uygulaması bir uygulama hizmeti planında çalışır.</span><span class="sxs-lookup"><span data-stu-id="44f78-147">Every App Service app runs in an App Service plan.</span></span> <span data-ttu-id="44f78-148">Merhaba kapsayıcı ortamları uygulama hizmeti planları basılı tutun ve uygulama hizmeti planları uygulamaları barındıracak modelidir.</span><span class="sxs-lookup"><span data-stu-id="44f78-148">hello container model is environments hold App Service plans, and App Service plans hold apps.</span></span> <span data-ttu-id="44f78-149">Bir uygulama ölçeklendirme, ölçeklendirme hello uygulama hizmeti planı ve böylece tüm hello uygulamalar hello ölçeklendirmek aynı planı.</span><span class="sxs-lookup"><span data-stu-id="44f78-149">When you scale an app, you scale hello App Service plan and thus scale all hello apps in hello same plan.</span></span>

<span data-ttu-id="44f78-150">Bir uygulama hizmeti planı ölçeklendirdiğinizde ASEv2 içinde gerekli hello altyapı otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="44f78-150">In ASEv2, when you scale an App Service plan, hello needed infrastructure is automatically added.</span></span> <span data-ttu-id="44f78-151">Yoktur gecikme süresini tooscale işlemleri hello altyapı eklenirken.</span><span class="sxs-lookup"><span data-stu-id="44f78-151">There is a time delay tooscale operations while hello infrastructure is added.</span></span> <span data-ttu-id="44f78-152">Oluşturma veya uygulama hizmeti planınızı ölçeklendirin önce ASEv1 içinde gerekli hello altyapı eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="44f78-152">In ASEv1, hello needed infrastructure must be added before you can create or scale out your App Service plan.</span></span> 

<span data-ttu-id="44f78-153">Kaynak havuzu kullanıma hazır toosupport hello multitenant App Service, ölçekleme genellikle hemen olduğundan bu.</span><span class="sxs-lookup"><span data-stu-id="44f78-153">In hello multitenant App Service, scaling is usually immediate because a pool of resources is readily available toosupport it.</span></span> <span data-ttu-id="44f78-154">Bir ana böyle bir arabellek yoktur ve kaynakları gerek ayrılır.</span><span class="sxs-lookup"><span data-stu-id="44f78-154">In an ASE, there is no such buffer, and resources are allocated upon need.</span></span>

<span data-ttu-id="44f78-155">ASE'de, too100 örneği ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-155">In an ASE, you can scale up too100 instances.</span></span> <span data-ttu-id="44f78-156">Bu 100 örnekleri arasında birden çok uygulama hizmeti planları dağıtılmış veya tüm tek tek uygulama hizmeti planında olabilir.</span><span class="sxs-lookup"><span data-stu-id="44f78-156">Those 100 instances can be all in one single App Service plan or distributed across multiple App Service plans.</span></span>

## <a name="ip-addresses"></a><span data-ttu-id="44f78-157">IP adresleri</span><span class="sxs-lookup"><span data-stu-id="44f78-157">IP addresses</span></span> ##

<span data-ttu-id="44f78-158">Uygulama hizmeti hello özelliği tooallocate ayrılmış bir IP adresi tooan uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="44f78-158">App Service has hello ability tooallocate a dedicated IP address tooan app.</span></span> <span data-ttu-id="44f78-159">Bir IP tabanlı SSL yapılandırdıktan sonra bu özellik açıklandığı gibi kullanılabilir [bir var olan özel SSL sertifikası tooAzure web uygulamaları bağlamak][ConfigureSSL].</span><span class="sxs-lookup"><span data-stu-id="44f78-159">This capability is available after you configure an IP-based SSL, as described in [Bind an existing custom SSL certificate tooAzure web apps][ConfigureSSL].</span></span> <span data-ttu-id="44f78-160">Ancak, ASE'de, önemli bir özel durum yoktur.</span><span class="sxs-lookup"><span data-stu-id="44f78-160">However, in an ASE, there is a notable exception.</span></span> <span data-ttu-id="44f78-161">Ek IP eklenemez bir ILB ana bir IP tabanlı SSL için kullanılan toobe yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="44f78-161">You can't add additional IP addresses toobe used for an IP-based SSL in an ILB ASE.</span></span>

<span data-ttu-id="44f78-162">Kullanabilmek için önce ASEv1 içinde tooallocate hello IP adreslerini kaynaklar olarak gerekir.</span><span class="sxs-lookup"><span data-stu-id="44f78-162">In ASEv1, you need tooallocate hello IP addresses as resources before you can use them.</span></span> <span data-ttu-id="44f78-163">Merhaba multitenant uygulama hizmeti gibi ASEv2, bunları uygulamanızdan kullanın.</span><span class="sxs-lookup"><span data-stu-id="44f78-163">In ASEv2, you use them from your app just as you do in hello multitenant App Service.</span></span> <span data-ttu-id="44f78-164">Her zaman bir yedek adres yok ASEv2 içinde too30 IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="44f78-164">There is always one spare address in ASEv2 up too30 IP addresses.</span></span> <span data-ttu-id="44f78-165">Bir adresi her zaman kullanıma hazır olmasını sağlamak her birini kullanın, başka bir eklenir.</span><span class="sxs-lookup"><span data-stu-id="44f78-165">Each time you use one, another is added so that an address is always readily available for use.</span></span> <span data-ttu-id="44f78-166">Gecikme süresi tooallocate IP ekleme engelleyen başka bir IP adresi gerekli hızlı art arda adresleri.</span><span class="sxs-lookup"><span data-stu-id="44f78-166">A time delay is required tooallocate another IP address, which prevents adding IP addresses in quick succession.</span></span>

## <a name="front-end-scaling"></a><span data-ttu-id="44f78-167">Ön uç ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="44f78-167">Front-end scaling</span></span> ##

<span data-ttu-id="44f78-168">Uygulama hizmeti planlarınızı ölçeklendirdiğinizde ASEv2 içinde çalışanları otomatik olarak toosupport eklenir bunları.</span><span class="sxs-lookup"><span data-stu-id="44f78-168">In ASEv2, when you scale out your App Service plans, workers are automatically added toosupport them.</span></span> <span data-ttu-id="44f78-169">Her ana iki ön uçlar ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="44f78-169">Every ASE is created with two front ends.</span></span> <span data-ttu-id="44f78-170">Ayrıca, hello ön uçlar otomatik olarak her 15 örnekleri için bir ön uç hızında uygulama hizmeti planlarında ölçeğini.</span><span class="sxs-lookup"><span data-stu-id="44f78-170">In addition, hello front ends automatically scale out at a rate of one front end for every 15 instances in your App Service plans.</span></span> <span data-ttu-id="44f78-171">15 örneği varsa, örneğin, daha sonra üç ön uçlar sahip.</span><span class="sxs-lookup"><span data-stu-id="44f78-171">For example, if you have 15 instances, then you have three front ends.</span></span> <span data-ttu-id="44f78-172">Too30 örnekleri ölçeklendirme sonra dört ön uçları vb. varsa.</span><span class="sxs-lookup"><span data-stu-id="44f78-172">If you scale too30 instances, then you have four front ends, and so on.</span></span>

<span data-ttu-id="44f78-173">Ön Uçları sayısı fazlasıyla yeterlidir çoğu için senaryolar olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="44f78-173">This number of front ends should be more than enough for most scenarios.</span></span> <span data-ttu-id="44f78-174">Ancak, çıkışı daha hızlı bir oranda ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-174">However, you can scale out at a faster rate.</span></span> <span data-ttu-id="44f78-175">Her beş örnekleri için bir ön uç olarak tooas düşük hello oranı değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-175">You can change hello ratio tooas low as one front end for every five instances.</span></span> <span data-ttu-id="44f78-176">Merhaba oranı değiştirmek bir ücret yoktur.</span><span class="sxs-lookup"><span data-stu-id="44f78-176">There is a charge for changing hello ratio.</span></span> <span data-ttu-id="44f78-177">Daha fazla bilgi için bkz: [Azure uygulama hizmeti fiyatlandırması][Pricing].</span><span class="sxs-lookup"><span data-stu-id="44f78-177">For more information, see [Azure App Service pricing][Pricing].</span></span>

<span data-ttu-id="44f78-178">Merhaba HTTP/HTTPS uç noktası hello ana için ön uç kaynaklardır.</span><span class="sxs-lookup"><span data-stu-id="44f78-178">Front-end resources are hello HTTP/HTTPS endpoint for hello ASE.</span></span> <span data-ttu-id="44f78-179">Merhaba varsayılan ön uç yapılandırma ile ön uç başına bellek kullanımı sürekli olarak yaklaşık yüzde 60'tır.</span><span class="sxs-lookup"><span data-stu-id="44f78-179">With hello default front-end configuration, memory usage per front end is consistently around 60 percent.</span></span> <span data-ttu-id="44f78-180">Müşteri iş yükleri bir ön uç üzerinde çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="44f78-180">Customer workloads don't run on a front end.</span></span> <span data-ttu-id="44f78-181">Merhaba anahtar saygı tooscale ile ön uç için öncelikle HTTPS trafiği tarafından yönlendirilen hello CPU faktördür.</span><span class="sxs-lookup"><span data-stu-id="44f78-181">hello key factor for a front end with respect tooscale is hello CPU, which is driven primarily by HTTPS traffic.</span></span>

## <a name="app-access"></a><span data-ttu-id="44f78-182">Uygulama erişimi</span><span class="sxs-lookup"><span data-stu-id="44f78-182">App access</span></span> ##

<span data-ttu-id="44f78-183">Dış ASE'de uygulamaları oluştururken kullanılan hello etki alanı hello çok kullanıcılı App Service ' farklıdır.</span><span class="sxs-lookup"><span data-stu-id="44f78-183">In an External ASE, hello domain that's used when you create apps is different from hello multitenant App Service.</span></span> <span data-ttu-id="44f78-184">Merhaba ana hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="44f78-184">It includes hello name of hello ASE.</span></span> <span data-ttu-id="44f78-185">Hakkında daha fazla bilgi için bkz toocreate bir dış ana [uygulama hizmeti ortamı oluşturma][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="44f78-185">For more information on how toocreate an External ASE, see [Create an App Service environment][MakeExternalASE].</span></span> <span data-ttu-id="44f78-186">bir dış ana Hello etki alanı adı arar gibi *.&lt; asename&gt;. p.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="44f78-186">hello domain name in an External ASE looks like *.&lt;asename&gt;.p.azurewebsites.net*.</span></span> <span data-ttu-id="44f78-187">Örneğin, ana adlı, _dış ana_ ve adlı bir uygulama ana bilgisayar _contoso_ o ana, bunu aşağıdaki URL'lere hello ulaşana:</span><span class="sxs-lookup"><span data-stu-id="44f78-187">For example, if your ASE is named _external-ase_ and you host an app called _contoso_ in that ASE, you reach it at hello following URLs:</span></span>

- <span data-ttu-id="44f78-188">contoso.external ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="44f78-188">contoso.external-ase.p.azurewebsites.net</span></span>
- <span data-ttu-id="44f78-189">contoso.SCM.external ase.p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="44f78-189">contoso.scm.external-ase.p.azurewebsites.net</span></span>

<span data-ttu-id="44f78-190">Merhaba URL contoso.scm.external-ase.p.azurewebsites.net kullanılan tooaccess hello Kudu konsol ya da web kullanarak uygulamanızı yayımlama için dağıtın.</span><span class="sxs-lookup"><span data-stu-id="44f78-190">hello URL contoso.scm.external-ase.p.azurewebsites.net is used tooaccess hello Kudu console or for publishing your app by using web deploy.</span></span> <span data-ttu-id="44f78-191">Merhaba Kudu Konsolu hakkında daha fazla bilgi için bkz: [Kudu Konsolu Azure App Service için][Kudu].</span><span class="sxs-lookup"><span data-stu-id="44f78-191">For information on hello Kudu console, see [Kudu console for Azure App Service][Kudu].</span></span> <span data-ttu-id="44f78-192">Merhaba Kudu konsol, web kullanıcı Arabirimi sağlar hata ayıklama, dosyalar, dosyalar ve çok daha fazlasını düzenleme için.</span><span class="sxs-lookup"><span data-stu-id="44f78-192">hello Kudu console gives you a web UI for debugging, uploading files, editing files, and much more.</span></span>

<span data-ttu-id="44f78-193">ILB ASE'de dağıtım sırasında hello etki alanı belirler.</span><span class="sxs-lookup"><span data-stu-id="44f78-193">In an ILB ASE, you determine hello domain at deployment time.</span></span> <span data-ttu-id="44f78-194">Toocreate bir ILB ana, nasıl görürüm hakkında daha fazla bilgi için [oluşturma ve kullanma bir ILB ana][MakeILBASE].</span><span class="sxs-lookup"><span data-stu-id="44f78-194">For more information on how toocreate an ILB ASE, see [Create and use an ILB ASE][MakeILBASE].</span></span> <span data-ttu-id="44f78-195">Merhaba etki alanı adı belirtirseniz, _ılb ase.info_, ana kullanın, bu etki alanı app oluşturma sırasında uygulamaları hello.</span><span class="sxs-lookup"><span data-stu-id="44f78-195">If you specify hello domain name _ilb-ase.info_, hello apps in that ASE use that domain during app creation.</span></span> <span data-ttu-id="44f78-196">Adlı hello uygulama için _contoso_, hello URL'ler:</span><span class="sxs-lookup"><span data-stu-id="44f78-196">For hello app named _contoso_, hello URLs are:</span></span>

- <span data-ttu-id="44f78-197">contoso.ilb ase.info</span><span class="sxs-lookup"><span data-stu-id="44f78-197">contoso.ilb-ase.info</span></span>
- <span data-ttu-id="44f78-198">contoso.SCM.ilb ase.info</span><span class="sxs-lookup"><span data-stu-id="44f78-198">contoso.scm.ilb-ase.info</span></span>

## <a name="publishing"></a><span data-ttu-id="44f78-199">Yayımlama</span><span class="sxs-lookup"><span data-stu-id="44f78-199">Publishing</span></span> ##

<span data-ttu-id="44f78-200">Merhaba çok kullanıcılı olarak App Service ile ASE'de ile yayımlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44f78-200">As with hello multitenant App Service, in an ASE you can publish with:</span></span>

- <span data-ttu-id="44f78-201">Web dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="44f78-201">Web deployment.</span></span>
- <span data-ttu-id="44f78-202">FTP.</span><span class="sxs-lookup"><span data-stu-id="44f78-202">FTP.</span></span>
- <span data-ttu-id="44f78-203">Sürekli Tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="44f78-203">Continuous integration.</span></span>
- <span data-ttu-id="44f78-204">Merhaba Kudu konsolunda sürükleyip yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="44f78-204">Drag and drop in hello Kudu console.</span></span>
- <span data-ttu-id="44f78-205">Visual Studio, Eclipse ya da Intellij Idea gibi bir IDE.</span><span class="sxs-lookup"><span data-stu-id="44f78-205">An IDE, such as Visual Studio, Eclipse, or IntelliJ IDEA.</span></span>

<span data-ttu-id="44f78-206">Bir dış ana ile tüm davranır Bu yayımlama seçeneklerini aynı hello.</span><span class="sxs-lookup"><span data-stu-id="44f78-206">With an External ASE, these publishing options all behave hello same.</span></span> <span data-ttu-id="44f78-207">Daha fazla bilgi için bkz: [Azure App Service'te dağıtım][AppDeploy].</span><span class="sxs-lookup"><span data-stu-id="44f78-207">For more information, see [Deployment in Azure App Service][AppDeploy].</span></span> 

<span data-ttu-id="44f78-208">Yayımlama Hello önemli fark saygı tooan ILB ana ' dir.</span><span class="sxs-lookup"><span data-stu-id="44f78-208">hello major difference with publishing is with respect tooan ILB ASE.</span></span> <span data-ttu-id="44f78-209">Bir ILB ana ile yayımlama hello uç noktalar yalnızca hello ILB tüm büyük/küçük harf kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="44f78-209">With an ILB ASE, hello publishing endpoints are all available only through hello ILB.</span></span> <span data-ttu-id="44f78-210">Merhaba ILB özel IP hello ana alt hello sanal ağında açıktır.</span><span class="sxs-lookup"><span data-stu-id="44f78-210">hello ILB is on a private IP in hello ASE subnet in hello virtual network.</span></span> <span data-ttu-id="44f78-211">Ağ erişim toohello ILB yoksa, o ana tüm uygulamaların yayımlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="44f78-211">If you don’t have network access toohello ILB, you can't publish any apps on that ASE.</span></span> <span data-ttu-id="44f78-212">İçinde belirtildiği gibi [oluşturma ve kullanma bir ILB ana][MakeILBASE], tooconfigure DNS hello sistemde hello uygulamaları için gerekir.</span><span class="sxs-lookup"><span data-stu-id="44f78-212">As noted in [Create and use an ILB ASE][MakeILBASE], you need tooconfigure DNS for hello apps in hello system.</span></span> <span data-ttu-id="44f78-213">Merhaba SCM uç noktasının dahildir.</span><span class="sxs-lookup"><span data-stu-id="44f78-213">That includes hello SCM endpoint.</span></span> <span data-ttu-id="44f78-214">Bunlar düzgün tanımlanmamış, yayımlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="44f78-214">If they're not defined properly, you can't publish.</span></span> <span data-ttu-id="44f78-215">IDE toohave ağ erişim toohello ILB sipariş toopublish etmeniz doğrudan tooit.</span><span class="sxs-lookup"><span data-stu-id="44f78-215">Your IDEs also need toohave network access toohello ILB in order toopublish directly tooit.</span></span>

<span data-ttu-id="44f78-216">Yayımlama Hello endpoint Internet erişilebilir olmadığı için Internet tabanlı CI sistemler, GitHub ve Visual Studio Team Services gibi bir ILB ana ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="44f78-216">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint is not Internet accessible.</span></span> <span data-ttu-id="44f78-217">Bunun yerine, toouse Dropbox gibi bir çekme modeli kullanan bir CI sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="44f78-217">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="44f78-218">Yayımlama Hello uç noktaları bir ILB ana uygulamalar için ILB ana oluşturulması sırasında bu hello hello etki alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="44f78-218">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="44f78-219">Merhaba uygulamanın yayımlama profili ve hello uygulamanızın portal dikey görebilirsiniz (içinde **genel bakış** > **Essentials** ve ayrıca **özellikleri**).</span><span class="sxs-lookup"><span data-stu-id="44f78-219">You can see it in hello app's publishing profile and in hello app's portal blade (in **Overview** > **Essentials** and also in **Properties**).</span></span> 

## <a name="pricing"></a><span data-ttu-id="44f78-220">Fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="44f78-220">Pricing</span></span> ##

<span data-ttu-id="44f78-221">adlı SKU fiyatlandırma hello **Isolated** yalnızca ASEv2 ile kullanmak için oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="44f78-221">hello pricing SKU called **Isolated** was created for use only with ASEv2.</span></span> <span data-ttu-id="44f78-222">Tüm ASEv2 içinde barındırılan uygulama hizmeti planları, SKU fiyatlandırma Isolated hello.</span><span class="sxs-lookup"><span data-stu-id="44f78-222">All App Service plans that are hosted in ASEv2 are in hello Isolated pricing SKU.</span></span> <span data-ttu-id="44f78-223">Yalıtılmış uygulama hizmeti planı hızları, bölge başına farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="44f78-223">Isolated App Service plan rates can vary per region.</span></span> 

<span data-ttu-id="44f78-224">Ayrıca uygulama hizmetiniz için toohello fiyatı planları, ana kendisi için bir düz oranı.</span><span class="sxs-lookup"><span data-stu-id="44f78-224">In addition toohello price for your App Service plans, there is a flat rate for ASE itself.</span></span> <span data-ttu-id="44f78-225">Merhaba düz oranı, ana hello boyutuyla değiştirmez ve 1 ek oranını ölçeklendirme varsayılan hello ana altyapısının için ödenen her 15 uygulama hizmeti planı örnekleri için ön uç.</span><span class="sxs-lookup"><span data-stu-id="44f78-225">hello flat rate doesn't change with hello size of your ASE and pays for hello ASE infrastructure at a default scaling rate of 1 additional front-end for every 15 App Service plan instances.</span></span>  

<span data-ttu-id="44f78-226">Merhaba varsayılan ölçek oranı 1 ön uç her 15 uygulama hizmeti planı örnekleri için yeterince hızlı değilse, ön uç eklenir veya hello ön uç boyutunu hello hello oranı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-226">If hello default scale rate of 1 front end for every 15 App Service plan instances is not fast enough, you can adjust hello ratio at which front-ends are added or hello size of hello front-ends.</span></span>  <span data-ttu-id="44f78-227">Merhaba oranı veya boyutunu ayarladığınızda, varsayılan olarak ekleneceği değil hello ön uç çekirdekleri ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-227">When you adjust hello ratio or size, you pay for hello front-end cores that would not be added by default.</span></span>  

<span data-ttu-id="44f78-228">Örneğin, bir ön uç hello ölçek oranı too10 ayarlarsanız, her 10 örnekleri için uygulama hizmeti planları eklenir.</span><span class="sxs-lookup"><span data-stu-id="44f78-228">For example, if you adjust hello scale ratio too10, a front end is added for every 10 instances in your App Service plans.</span></span> <span data-ttu-id="44f78-229">Merhaba ücret her 15 örnekleri için bir ön uç ölçek oranını kapsar.</span><span class="sxs-lookup"><span data-stu-id="44f78-229">hello flat fee covers a scale rate of one front end for every 15 instances.</span></span> <span data-ttu-id="44f78-230">10 ölçek oranını ile Merhaba 10 uygulama hizmeti plan örneği eklediği hello üçüncü ön uç için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-230">With a scale ratio of 10, you pay a fee for hello third front end that's added for hello 10 App Service plan instances.</span></span> <span data-ttu-id="44f78-231">Otomatik olarak eklendiğinden 15 örnekleri ulaştığında toopay için gerekmez.</span><span class="sxs-lookup"><span data-stu-id="44f78-231">You don't need toopay for it when you reach 15 instances because it was added automatically.</span></span>

<span data-ttu-id="44f78-232">Merhaba ön uç too2 çekirdek hello boyutunu ayarlanmış, ancak için ödeme sonra hello oranı ayarlama ek çekirdek hello.</span><span class="sxs-lookup"><span data-stu-id="44f78-232">If you adjusted hello size of hello front-ends too2 cores but do not adjust hello ratio then you pay for hello extra cores.</span></span>  <span data-ttu-id="44f78-233">Bir ana 2 ön uç, hello boyutu too2 çekirdek ön uç artan varsa ek 2 Çekirdek için ödeme böylece bile hello otomatik ölçeklendirme eşiğin altına oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="44f78-233">An ASE is created with 2 front-ends, so even below hello automatic scaling threshold you would pay for 2 extra cores if you increased hello size too2 core front-ends.</span></span>

<span data-ttu-id="44f78-234">Daha fazla bilgi için bkz: [Azure uygulama hizmeti fiyatlandırması][Pricing].</span><span class="sxs-lookup"><span data-stu-id="44f78-234">For more information, see [Azure App Service pricing][Pricing].</span></span>

## <a name="delete-an-ase"></a><span data-ttu-id="44f78-235">Bir ana Sil</span><span class="sxs-lookup"><span data-stu-id="44f78-235">Delete an ASE</span></span> ##

<span data-ttu-id="44f78-236">bir ana toodelete:</span><span class="sxs-lookup"><span data-stu-id="44f78-236">toodelete an ASE:</span></span> 

1. <span data-ttu-id="44f78-237">Kullanım **silmek** hello hello üstündeki **uygulama hizmeti ortamı** dikey.</span><span class="sxs-lookup"><span data-stu-id="44f78-237">Use **Delete** at hello top of hello **App Service Environment** blade.</span></span> 

2. <span data-ttu-id="44f78-238">Toodelete istediğiniz, ana tooconfirm Hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="44f78-238">Enter hello name of your ASE tooconfirm that you want toodelete it.</span></span> <span data-ttu-id="44f78-239">Bir ana sildiğinizde, tüm içeriğini hello içindeki da silersiniz.</span><span class="sxs-lookup"><span data-stu-id="44f78-239">When you delete an ASE, you delete all of hello content within it as well.</span></span> 

    ![Ana silme][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
