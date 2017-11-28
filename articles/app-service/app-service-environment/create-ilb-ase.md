---
title: "aaaCreate ve bir iç yük dengeleyici Azure uygulama hizmeti ortamı ile kullanma"
description: "Hakkında ayrıntılar toocreate ve bir internet yalıtılmış Azure uygulama hizmeti ortamı'nı kullanma"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a><span data-ttu-id="c4071-103">Oluşturma ve bir iç yük dengeleyici ile uygulama hizmeti ortamı kullanma</span><span class="sxs-lookup"><span data-stu-id="c4071-103">Create and use an internal load balancer with an App Service environment</span></span> #

 <span data-ttu-id="c4071-104">Azure uygulama hizmeti ortamı bir Azure uygulama hizmeti dağıtımı bir Azure sanal ağındaki (VNet) bir alt ağ ile değil.</span><span class="sxs-lookup"><span data-stu-id="c4071-104">Azure App Service Environment is a deployment of Azure App Service into a subnet in an Azure virtual network (VNet).</span></span> <span data-ttu-id="c4071-105">Uygulama hizmeti ortamı (ana) iki yolu toodeploy vardır:</span><span class="sxs-lookup"><span data-stu-id="c4071-105">There are two ways toodeploy an App Service environment (ASE):</span></span> 

- <span data-ttu-id="c4071-106">Dış IP adresi üzerinde bir VIP ile genellikle bir dış ana çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c4071-106">With a VIP on an external IP address, often called an External ASE.</span></span>
- <span data-ttu-id="c4071-107">Bir iç yük dengeleyici (ILB) Hello iç uç nokta olduğu için bir iç IP adresinde bir VIP ile genellikle bir ILB ana çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c4071-107">With a VIP on an internal IP address, often called an ILB ASE because hello internal endpoint is an internal load balancer (ILB).</span></span> 

<span data-ttu-id="c4071-108">Bu makale size nasıl gösterir toocreate bir ILB ana.</span><span class="sxs-lookup"><span data-stu-id="c4071-108">This article shows you how toocreate an ILB ASE.</span></span> <span data-ttu-id="c4071-109">Merhaba ana üzerinde bir genel bakış için bkz: [giriş tooApp hizmeti ortamları][Intro].</span><span class="sxs-lookup"><span data-stu-id="c4071-109">For an overview on hello ASE, see [Introduction tooApp Service environments][Intro].</span></span> <span data-ttu-id="c4071-110">bir dış ana toocreate nasıl görürüm toolearn [bir dış ana oluşturma][MakeExternalASE].</span><span class="sxs-lookup"><span data-stu-id="c4071-110">toolearn how toocreate an External ASE, see [Create an External ASE][MakeExternalASE].</span></span>

## <a name="overview"></a><span data-ttu-id="c4071-111">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c4071-111">Overview</span></span> ##

<span data-ttu-id="c4071-112">Bir ana internet'ten erişilebilen bir uç nokta veya bir IP adresi ile sanal ağınızda dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4071-112">You can deploy an ASE with an internet-accessible endpoint or with an IP address in your VNet.</span></span> <span data-ttu-id="c4071-113">tooset başlangıç IP adresi tooa VNet adres, hello ana bir ILB ile dağıtılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-113">tooset hello IP address tooa VNet address, hello ASE must be deployed with an ILB.</span></span> <span data-ttu-id="c4071-114">Bir ILB ile ana dağıttığınızda, sağlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4071-114">When you deploy your ASE with an ILB, you must provide:</span></span>

-   <span data-ttu-id="c4071-115">Uygulamalarınızı oluştururken kullandığınız kendi etki alanı.</span><span class="sxs-lookup"><span data-stu-id="c4071-115">Your own domain that you use when you create your apps.</span></span>
-   <span data-ttu-id="c4071-116">HTTPS için kullanılan hello sertifikası.</span><span class="sxs-lookup"><span data-stu-id="c4071-116">hello certificate used for HTTPS.</span></span>
-   <span data-ttu-id="c4071-117">Etki alanınız için DNS yönetimi.</span><span class="sxs-lookup"><span data-stu-id="c4071-117">DNS management for your domain.</span></span>

<span data-ttu-id="c4071-118">Buna karşılık, sizin gibi şeyler yapabilir:</span><span class="sxs-lookup"><span data-stu-id="c4071-118">In return, you can do things such as:</span></span>

-   <span data-ttu-id="c4071-119">İntranet uygulamalarını bulutta bir siteden siteye veya Azure ExpressRoute VPN aracılığıyla erişebileceğiniz güvenli bir şekilde hello, ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="c4071-119">Host intranet applications securely in hello cloud, which you access through a site-to-site or Azure ExpressRoute VPN.</span></span>
-   <span data-ttu-id="c4071-120">Genel DNS sunucuları listelenmeyen konak uygulamalar hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="c4071-120">Host apps in hello cloud that aren't listed in public DNS servers.</span></span>
-   <span data-ttu-id="c4071-121">Ön uç uygulamalarınızı güvenli bir şekilde ile tümleştirebilirsiniz Internet yalıtılmış arka uç uygulamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4071-121">Create internet-isolated back-end apps, which your front-end apps can securely integrate with.</span></span>

### <a name="disabled-functionality"></a><span data-ttu-id="c4071-122">Devre dışı bırakılan işlevsellik</span><span class="sxs-lookup"><span data-stu-id="c4071-122">Disabled functionality</span></span> ###

<span data-ttu-id="c4071-123">Bir ILB ana kullandığınızda, bunu yapamazsınız bazı şeyler vardır:</span><span class="sxs-lookup"><span data-stu-id="c4071-123">There are some things that you can't do when you use an ILB ASE:</span></span>

-   <span data-ttu-id="c4071-124">IP tabanlı SSL kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4071-124">Use IP-based SSL.</span></span>
-   <span data-ttu-id="c4071-125">IP adresleri toospecific uygulamaları atayın.</span><span class="sxs-lookup"><span data-stu-id="c4071-125">Assign IP addresses toospecific apps.</span></span>
-   <span data-ttu-id="c4071-126">Satın alma ve hello Azure portal aracılığıyla bir uygulama ile bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4071-126">Buy and use a certificate with an app through hello Azure portal.</span></span> <span data-ttu-id="c4071-127">Doğrudan bir sertifika yetkilisinden sertifika almak ve bunları uygulamalarınızı ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4071-127">You can obtain certificates directly from a certificate authority and use them with your apps.</span></span> <span data-ttu-id="c4071-128">Bunları hello Azure portal elde edilemiyor.</span><span class="sxs-lookup"><span data-stu-id="c4071-128">You can't obtain them through hello Azure portal.</span></span>

## <a name="create-an-ilb-ase"></a><span data-ttu-id="c4071-129">Bir ILB ana oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4071-129">Create an ILB ASE</span></span> ##

<span data-ttu-id="c4071-130">bir ILB ana toocreate:</span><span class="sxs-lookup"><span data-stu-id="c4071-130">toocreate an ILB ASE:</span></span>

1. <span data-ttu-id="c4071-131">Hello Azure portal, seçin **yeni** > **Web + mobil** > **uygulama hizmeti ortamı**.</span><span class="sxs-lookup"><span data-stu-id="c4071-131">In hello Azure portal, select **New** > **Web + Mobile** > **App Service Environment**.</span></span>

2. <span data-ttu-id="c4071-132">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-132">Select your subscription.</span></span>

3. <span data-ttu-id="c4071-133">Kaynak grubunu seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4071-133">Select or create a resource group.</span></span>

4. <span data-ttu-id="c4071-134">Bir VNet oluşturun veya seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-134">Select or create a VNet.</span></span>

5. <span data-ttu-id="c4071-135">Varolan bir sanal ağ seçerseniz, bir alt ağ toohold hello ana toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-135">If you select an existing VNet, you need toocreate a subnet toohold hello ASE.</span></span> <span data-ttu-id="c4071-136">Tooset bir alt ağ boyutunu büyüklükte tooaccommodate gelecekteki büyümesine, ana emin olun.</span><span class="sxs-lookup"><span data-stu-id="c4071-136">Make sure tooset a subnet size large enough tooaccommodate any future growth of your ASE.</span></span> <span data-ttu-id="c4071-137">Dosya boyutu öneririz `/25`, 128 adresi olduğunu ve en büyük ölçekli bir ana işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="c4071-137">We recommend a size of `/25`, which has 128 addresses and can handle a maximum-sized ASE.</span></span> <span data-ttu-id="c4071-138">Merhaba minimum boyutu seçebileceğiniz bir `/28`.</span><span class="sxs-lookup"><span data-stu-id="c4071-138">hello minimum size you can select is a `/28`.</span></span> <span data-ttu-id="c4071-139">Altyapı gereken sonra bu boyut 11 örneklerinin ölçeklendirilmiş tooa en olabilir.</span><span class="sxs-lookup"><span data-stu-id="c4071-139">After infrastructure needs, this size can be scaled tooa maximum of 11 instances.</span></span>

    * <span data-ttu-id="c4071-140">Uygulama hizmeti planlarında Hello varsayılan en fazla 100 örneklerinin gidin.</span><span class="sxs-lookup"><span data-stu-id="c4071-140">Go beyond hello default maximum of 100 instances in your App Service plans.</span></span>

    * <span data-ttu-id="c4071-141">100 yakın ancak daha hızlı ön uç ölçeklendirme ile ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="c4071-141">Scale near 100 but with more rapid front-end scaling.</span></span>

6. <span data-ttu-id="c4071-142">Seçin **sanal ağ konumu** > **sanal ağ yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="c4071-142">Select **Virtual Network/Location** > **Virtual Network Configuration**.</span></span> <span data-ttu-id="c4071-143">Set hello **VIP türü** çok**dahili**.</span><span class="sxs-lookup"><span data-stu-id="c4071-143">Set hello **VIP Type** too**Internal**.</span></span>

7. <span data-ttu-id="c4071-144">Bir etki alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="c4071-144">Enter a domain name.</span></span> <span data-ttu-id="c4071-145">Bu ana içinde oluşturulan uygulamaları için kullanılan hello bu etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="c4071-145">This domain is hello one used for apps created in this ASE.</span></span> <span data-ttu-id="c4071-146">Bazı kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="c4071-146">There are some restrictions.</span></span> <span data-ttu-id="c4071-147">Olamaz:</span><span class="sxs-lookup"><span data-stu-id="c4071-147">It can't be:</span></span>

    * <span data-ttu-id="c4071-148">NET</span><span class="sxs-lookup"><span data-stu-id="c4071-148">net</span></span>   

    * <span data-ttu-id="c4071-149">azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="c4071-149">azurewebsites.net</span></span>

    * <span data-ttu-id="c4071-150">p.azurewebsites.NET</span><span class="sxs-lookup"><span data-stu-id="c4071-150">p.azurewebsites.net</span></span>

    * <span data-ttu-id="c4071-151">&lt;asename&gt;. p.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="c4071-151">&lt;asename&gt;.p.azurewebsites.net</span></span>

   <span data-ttu-id="c4071-152">Merhaba etki alanı adı, ana tarafından kullanılan çakışamaz ve uygulamalar için Hello özel etki alanı adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4071-152">hello custom domain name used for apps and hello domain name used by your ASE can't overlap.</span></span> <span data-ttu-id="c4071-153">Bir ILB ana hello etki alanı adıyla için _contoso.com_, özel etki alanı adları gibi uygulamalar için kullanılamaz:</span><span class="sxs-lookup"><span data-stu-id="c4071-153">For an ILB ASE with hello domain name _contoso.com_, you can't use custom domain names for your apps like:</span></span>

    * <span data-ttu-id="c4071-154">www.contoso.com</span><span class="sxs-lookup"><span data-stu-id="c4071-154">www.contoso.com</span></span>

    * <span data-ttu-id="c4071-155">ABCD.def.contoso.com</span><span class="sxs-lookup"><span data-stu-id="c4071-155">abcd.def.contoso.com</span></span>

    * <span data-ttu-id="c4071-156">ABCD.contoso.com</span><span class="sxs-lookup"><span data-stu-id="c4071-156">abcd.contoso.com</span></span>

   <span data-ttu-id="c4071-157">Uygulamalarınız için hello özel etki alanı adlarını biliyorsanız, bu özel etki alanı adları ile bir çakışma olmaz ILB ana hello için bir etki alanı seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-157">If you know hello custom domain names for your apps, choose a domain for hello ILB ASE that won’t have a conflict with those custom domain names.</span></span> <span data-ttu-id="c4071-158">Bu örnekte, aşağıdakine benzer kullanabilirsiniz *contoso internal.com* , ana hello etki alanı için sonunda özel etki alanı adları ile çakışmaz çünkü *. contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="c4071-158">In this example, you can use something like *contoso-internal.com* for hello domain of your ASE because that won't conflict with custom domain names that end in *.contoso.com*.</span></span>

8. <span data-ttu-id="c4071-159">Seçin **Tamam**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="c4071-159">Select **OK**, and then select **Create**.</span></span>

    ![ASE oluşturma][1]

<span data-ttu-id="c4071-161">Merhaba üzerinde **sanal ağ** dikey penceresinde, var olan bir **sanal ağ yapılandırması** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="c4071-161">On hello **Virtual Network** blade, there is a **Virtual Network Configuration** option.</span></span> <span data-ttu-id="c4071-162">Bir dış VIP veya iç VIP tooselect kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4071-162">You can use it tooselect an External VIP or an Internal VIP.</span></span> <span data-ttu-id="c4071-163">Merhaba varsayılandır **dış**.</span><span class="sxs-lookup"><span data-stu-id="c4071-163">hello default is **External**.</span></span> <span data-ttu-id="c4071-164">Seçerseniz **dış**, ana internet'ten erişilebilen bir VIP kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4071-164">If you select **External**, your ASE uses an internet-accessible VIP.</span></span> <span data-ttu-id="c4071-165">Seçerseniz **iç**, ana sanal ağınızın içinde bir IP adresinde bir ILB ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="c4071-165">If you select **Internal**, your ASE is configured with an ILB on an IP address within your VNet.</span></span>

<span data-ttu-id="c4071-166">Siz seçtikten sonra **iç**, hello özelliği tooadd daha fazla IP adresleri tooyour ana kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="c4071-166">After you select **Internal**, hello ability tooadd more IP addresses tooyour ASE is removed.</span></span> <span data-ttu-id="c4071-167">Bunun yerine, hello ana tooprovide hello etki alanı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-167">Instead, you need tooprovide hello domain of hello ASE.</span></span> <span data-ttu-id="c4071-168">ASE'de bir dış VIP ile hello hello ana adını hello etki alanında o ana oluşturulan uygulamalar için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c4071-168">In an ASE with an External VIP, hello name of hello ASE is used in hello domain for apps created in that ASE.</span></span>

<span data-ttu-id="c4071-169">Ayarlarsanız **VIP türü** çok**iç**, ana adınızı hello etki alanında ana hello için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="c4071-169">If you set **VIP Type** too**Internal**, your ASE name is not used in hello domain for hello ASE.</span></span> <span data-ttu-id="c4071-170">Merhaba etki alanını açıkça belirtin.</span><span class="sxs-lookup"><span data-stu-id="c4071-170">You specify hello domain explicitly.</span></span> <span data-ttu-id="c4071-171">Etki alanınız varsa *contoso.corp.net* ve ana adlı içeren bir uygulama oluşturmak *timereporting*, bu uygulama timereporting.contoso.corp.net için URL hello.</span><span class="sxs-lookup"><span data-stu-id="c4071-171">If your domain is *contoso.corp.net* and you create an app in that ASE named *timereporting*, hello URL for that app is timereporting.contoso.corp.net.</span></span>


## <a name="create-an-app-in-an-ilb-ase"></a><span data-ttu-id="c4071-172">ILB ASE'de bir uygulama oluşturun</span><span class="sxs-lookup"><span data-stu-id="c4071-172">Create an app in an ILB ASE</span></span> ##

<span data-ttu-id="c4071-173">ILB ASE'de hello bir uygulama oluşturun, bir uygulama ASE'de normalde oluşturmanızı aynı şekilde.</span><span class="sxs-lookup"><span data-stu-id="c4071-173">You create an app in an ILB ASE in hello same way that you create an app in an ASE normally.</span></span>

1. <span data-ttu-id="c4071-174">Hello Azure portal, seçin **yeni** > **Web + mobil** > **Web** veya **mobil** veya  **API uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="c4071-174">In hello Azure portal, select **New** > **Web + Mobile** > **Web** or **Mobile** or **API App**.</span></span>

2. <span data-ttu-id="c4071-175">Merhaba hello uygulama adını girin.</span><span class="sxs-lookup"><span data-stu-id="c4071-175">Enter hello name of hello app.</span></span>

3. <span data-ttu-id="c4071-176">Merhaba aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-176">Select hello subscription.</span></span>

4. <span data-ttu-id="c4071-177">Kaynak grubunu seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4071-177">Select or create a resource group.</span></span>

5. <span data-ttu-id="c4071-178">Bir uygulama hizmeti planı oluşturun veya seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-178">Select or create an App Service plan.</span></span> <span data-ttu-id="c4071-179">Yeni bir uygulama hizmeti planı toocreate istiyorsanız, ana hello konumu olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-179">If you want toocreate a new App Service plan, select your ASE as hello location.</span></span> <span data-ttu-id="c4071-180">Oluşturulan, uygulama hizmeti planı toobe istediğiniz hello çalışan havuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-180">Select hello worker pool where you want your App Service plan toobe created.</span></span> <span data-ttu-id="c4071-181">Merhaba uygulama hizmeti planı oluşturduğunuzda, ana hello konumu ve hello çalışan havuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-181">When you create hello App Service plan, select your ASE as hello location and hello worker pool.</span></span> <span data-ttu-id="c4071-182">Merhaba uygulamasının hello adı belirttiğinizde, uygulama adı altında hello etki alanı için ana hello etki alanı tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="c4071-182">When you specify hello name of hello app, hello domain under your app name is replaced by hello domain for your ASE.</span></span>

6. <span data-ttu-id="c4071-183">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="c4071-183">Select **Create**.</span></span> <span data-ttu-id="c4071-184">Panonuzda hello uygulama tooappear istiyorsanız seçin **PIN toodashboard** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="c4071-184">If you want hello app tooappear on your dashboard, select the **Pin toodashboard** check box.</span></span>

    ![Uygulama hizmeti planı oluşturma][2]

    <span data-ttu-id="c4071-186">Altında **uygulama adı**, hello etki alanı adıdır, ana güncelleştirilmiş tooreflect hello etki alanı.</span><span class="sxs-lookup"><span data-stu-id="c4071-186">Under **App name**, hello domain name is updated tooreflect hello domain of your ASE.</span></span>

## <a name="post-ilb-ase-creation-validation"></a><span data-ttu-id="c4071-187">POST ILB ana oluşturma doğrulama</span><span class="sxs-lookup"><span data-stu-id="c4071-187">Post-ILB ASE creation validation</span></span> ##

<span data-ttu-id="c4071-188">Bir ILB ana hello olmayan - ILB ana değerinden biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="c4071-188">An ILB ASE is slightly different than hello non-ILB ASE.</span></span> <span data-ttu-id="c4071-189">Önceden belirtildiği gibi toomanage kendi DNS ihtiyacınız var.</span><span class="sxs-lookup"><span data-stu-id="c4071-189">As already noted, you need toomanage your own DNS.</span></span> <span data-ttu-id="c4071-190">Ayrıca, kendi sertifika HTTPS bağlantıları için tooprovide vardır.</span><span class="sxs-lookup"><span data-stu-id="c4071-190">You also have tooprovide your own certificate for HTTPS connections.</span></span>

<span data-ttu-id="c4071-191">Hello etki alanı adı, ana oluşturduktan sonra belirttiğiniz hello etki alanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c4071-191">After you create your ASE, hello domain name shows hello domain you specified.</span></span> <span data-ttu-id="c4071-192">Yeni bir öğe görünür **ayarı** adlı menüsü **ILB sertifika**.</span><span class="sxs-lookup"><span data-stu-id="c4071-192">A new item appears in the **Setting** menu called **ILB Certificate**.</span></span> <span data-ttu-id="c4071-193">Merhaba ana hello ILB ana etki alanı belirtmeyen bir sertifika ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c4071-193">hello ASE is created with a certificate that doesn't specify hello ILB ASE domain.</span></span> <span data-ttu-id="c4071-194">Bu sertifika ile Merhaba ana kullanıyorsanız, tarayıcınızı geçersiz olduğunu söyler.</span><span class="sxs-lookup"><span data-stu-id="c4071-194">If you use hello ASE with that certificate, your browser tells you that it's invalid.</span></span> <span data-ttu-id="c4071-195">Bu sertifika daha kolay tootest HTTPS kolaylaştırır, ancak bağlı tooyour ILB ana etki alanı kendi sertifikanızı tooupload gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-195">This certificate makes it easier tootest HTTPS, but you need tooupload your own certificate that's tied tooyour ILB ASE domain.</span></span> <span data-ttu-id="c4071-196">Bu adım sertifikanız veya otomatik olarak imzalanan bir sertifika yetkilisinden alınan bağımsız olarak gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c4071-196">This step is necessary regardless of whether your certificate is self-signed or acquired from a certificate authority.</span></span>

![ILB ana etki alanı adı][3]

<span data-ttu-id="c4071-198">ILB ana geçerli bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-198">Your ILB ASE needs a valid SSL certificate.</span></span> <span data-ttu-id="c4071-199">İç sertifika yetkilileri kullanın, bir dış veren bir sertifika satın veya otomatik olarak imzalanan bir sertifika kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4071-199">Use internal certificate authorities, purchase a certificate from an external issuer, or use a self-signed certificate.</span></span> <span data-ttu-id="c4071-200">Bağımsız olarak Hello kaynak hello SSL sertifikasının hello aşağıdaki sertifika öznitelikleri düzgün yapılandırılmış toobe gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4071-200">Regardless of hello source of hello SSL certificate, hello following certificate attributes need toobe configured properly:</span></span>

* <span data-ttu-id="c4071-201">**Konu**: kök etki alanı burada too*.your bu özniteliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4071-201">**Subject**: This attribute must be set too*.your-root-domain-here.</span></span>
* <span data-ttu-id="c4071-202">**Konu alternatif adı**: Bu öznitelik her ikisini de içermelidir **kök etki alanı burada .your* ve **.scm.your-kök-etki-burada*.</span><span class="sxs-lookup"><span data-stu-id="c4071-202">**Subject Alternative Name**: This attribute must include both **.your-root-domain-here* and **.scm.your-root-domain-here*.</span></span> <span data-ttu-id="c4071-203">SSL bağlantıları toohello SCM/Kudu site her uygulamayla ilişkili hello formunun bir adres kullanın *your-app-name.scm.your-root-domain-here*.</span><span class="sxs-lookup"><span data-stu-id="c4071-203">SSL connections toohello SCM/Kudu site associated with each app use an address of hello form *your-app-name.scm.your-root-domain-here*.</span></span>

<span data-ttu-id="c4071-204">Convert/hello SSL sertifikası bir .pfx dosyası olarak Kaydet.</span><span class="sxs-lookup"><span data-stu-id="c4071-204">Convert/save hello SSL certificate as a .pfx file.</span></span> <span data-ttu-id="c4071-205">Hello .pfx dosyası, tüm ara içerir ve sertifikaları kök gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-205">hello .pfx file must include all intermediate and root certificates.</span></span> <span data-ttu-id="c4071-206">Bir parola ile güvenli hale getirin.</span><span class="sxs-lookup"><span data-stu-id="c4071-206">Secure it with a password.</span></span>

<span data-ttu-id="c4071-207">Toocreate otomatik olarak imzalanan bir sertifika isterseniz, burayı hello PowerShell komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4071-207">If you want toocreate a self-signed certificate, you can use hello PowerShell commands here.</span></span> <span data-ttu-id="c4071-208">ILB ana etki alanı adınızı yerine emin toouse olması *internal.contoso.com*:</span><span class="sxs-lookup"><span data-stu-id="c4071-208">Be sure toouse your ILB ASE domain name instead of *internal.contoso.com*:</span></span> 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

<span data-ttu-id="c4071-209">Merhaba sertifika tarayıcınızın güven zincirinde olan bir sertifika yetkilisi tarafından oluşturulmadıysa çünkü bu PowerShell komutlarını oluşturan hello sertifika tarayıcılar tarafından işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="c4071-209">hello certificate that these PowerShell commands generate is flagged by browsers because hello certificate wasn't created by a certificate authority that's in your browser's chain of trust.</span></span> <span data-ttu-id="c4071-210">tooget tarayıcınız güvenler, bir sertifika edinin, tarayıcınızın zincirinde güven, ticari sertifika yetkilisinden.</span><span class="sxs-lookup"><span data-stu-id="c4071-210">tooget a certificate that your browser trusts, procure it from a commercial certificate authority in your browser's chain of trust.</span></span> 

![ILB sertifikayı ayarlayın][4]

<span data-ttu-id="c4071-212">tooupload kendi sertifikaları ve test erişim:</span><span class="sxs-lookup"><span data-stu-id="c4071-212">tooupload your own certificates and test access:</span></span>

1. <span data-ttu-id="c4071-213">Merhaba ana oluşturulduktan sonra toohello ana UI gidin.</span><span class="sxs-lookup"><span data-stu-id="c4071-213">After hello ASE is created, go toohello ASE UI.</span></span> <span data-ttu-id="c4071-214">Seçin **ana** > **ayarları** > **ILB sertifika**.</span><span class="sxs-lookup"><span data-stu-id="c4071-214">Select **ASE** > **Settings** > **ILB Certificate**.</span></span>

2. <span data-ttu-id="c4071-215">tooset hello ILB sertifika hello sertifika .pfx dosyasını seçin ve hello parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="c4071-215">tooset hello ILB certificate, select hello certificate .pfx file and enter hello password.</span></span> <span data-ttu-id="c4071-216">Bu adım, bazı zaman tooprocess alır.</span><span class="sxs-lookup"><span data-stu-id="c4071-216">This step takes some time tooprocess.</span></span> <span data-ttu-id="c4071-217">Bir karşıya yükleme işlemi devam ediyor belirten bir ileti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c4071-217">A message appears stating that an upload operation is in progress.</span></span>

3. <span data-ttu-id="c4071-218">Merhaba ILB adresi için ana alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c4071-218">Get hello ILB address for your ASE.</span></span> <span data-ttu-id="c4071-219">Seçin **ana** > **özellikleri** > **sanal IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="c4071-219">Select **ASE** > **Properties** > **Virtual IP Address**.</span></span>

4. <span data-ttu-id="c4071-220">Merhaba ana oluşturulduktan sonra ana bir web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4071-220">Create a web app in your ASE after hello ASE is created.</span></span>

5. <span data-ttu-id="c4071-221">Bu VNet içinde yoksa, bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4071-221">Create a VM if you don't have one in that VNet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4071-222">Bu VM toocreate denemeyin başarısız veya sorunlara neden olduğundan ana hello gibi aynı alt ağda hello.</span><span class="sxs-lookup"><span data-stu-id="c4071-222">Don't try toocreate this VM in hello same subnet as hello ASE because it will fail or cause problems.</span></span>
    >
    >

6. <span data-ttu-id="c4071-223">Merhaba DNS ana etki alanınız için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c4071-223">Set hello DNS for your ASE domain.</span></span> <span data-ttu-id="c4071-224">DNS, etki alanı ile bir joker karakter kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4071-224">You can use a wildcard with your domain in your DNS.</span></span> <span data-ttu-id="c4071-225">bazı basit toodo testleri, VM tooset hello web uygulaması adı toohello VIP IP adresi üzerinde hello hosts dosyasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="c4071-225">toodo some simple tests, edit hello hosts file on your VM tooset hello web app name toohello VIP IP address:</span></span>

    <span data-ttu-id="c4071-226">a.</span><span class="sxs-lookup"><span data-stu-id="c4071-226">a.</span></span> <span data-ttu-id="c4071-227">Merhaba etki alanı adı, ana sahipse, _. ilbase.com_ ve adlı hello web uygulaması oluşturma _mytestapp_, adresindeki ele _mytestapp.ilbase.com_. Ardından _mytestapp.ilbase.com_ tooresolve toohello ILB adresi.</span><span class="sxs-lookup"><span data-stu-id="c4071-227">If your ASE has hello domain name _.ilbase.com_ and you create hello web app named _mytestapp_, it's addressed at _mytestapp.ilbase.com_. You then set _mytestapp.ilbase.com_ tooresolve toohello ILB address.</span></span> <span data-ttu-id="c4071-228">(Windows üzerinde hello hosts _C:\Windows\System32\drivers\etc dosyasıdır\_.)</span><span class="sxs-lookup"><span data-stu-id="c4071-228">(On Windows, hello hosts file is at _C:\Windows\System32\drivers\etc\_.)</span></span>

    <span data-ttu-id="c4071-229">b.</span><span class="sxs-lookup"><span data-stu-id="c4071-229">b.</span></span> <span data-ttu-id="c4071-230">konsolunda, Gelişmiş tootest web dağıtımı yayımlama veya erişim toohello oluşturmak için bir kayıt _mytestapp.scm.ilbase.com_.</span><span class="sxs-lookup"><span data-stu-id="c4071-230">tootest web deployment publishing or access toohello advanced console, create a record for _mytestapp.scm.ilbase.com_.</span></span>

7. <span data-ttu-id="c4071-231">Bu VM üzerinde bir tarayıcı kullanın ve http://mytestapp.ilbase.com için gidin. (Veya web uygulaması adı, etki alanı ile olan toowhatever gidin.)</span><span class="sxs-lookup"><span data-stu-id="c4071-231">Use a browser on that VM and go to http://mytestapp.ilbase.com. (Or go toowhatever your web app name is with your domain.)</span></span>

8. <span data-ttu-id="c4071-232">Bu VM üzerinde bir tarayıcı kullanın ve https://mytestapp.ilbase.com için gidin. Kendinden imzalı bir sertifika kullanıyorsanız, güvenlik hello eksikliği kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c4071-232">Use a browser on that VM and go to https://mytestapp.ilbase.com. If you use a self-signed certificate, accept hello lack of security.</span></span>

    <span data-ttu-id="c4071-233">Başlangıç IP adresi, ILB için altında listelenen **IP adreslerini**.</span><span class="sxs-lookup"><span data-stu-id="c4071-233">hello IP address for your ILB is listed under **IP addresses**.</span></span> <span data-ttu-id="c4071-234">Bu liste hello dış VIP ve gelen yönetim trafiği için kullanılan hello IP adresleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="c4071-234">This list also has hello IP addresses used by hello external VIP and for inbound management traffic.</span></span>

    ![ILB IP adresi][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a><span data-ttu-id="c4071-236">Web işleri, İşlevler ve ILB ana hello</span><span class="sxs-lookup"><span data-stu-id="c4071-236">Web jobs, Functions and hello ILB ASE</span></span>

<span data-ttu-id="c4071-237">Bir ILB ana işlevleri ve web işleri desteklenmektedir, ancak hello portal toowork için onlarla, ağ erişim toohello SCM site olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-237">Both Functions and web jobs are supported on an ILB ASE but for hello portal toowork with them, you must have network access toohello SCM site.</span></span>  <span data-ttu-id="c4071-238">Bu, tarayıcınızı ya da kullanılıyor veya toohello sanal ağa bağlı bir konak üzerinde olması gerektiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c4071-238">This means your browser must either be on a host that is either in or connected toohello virtual network.</span></span>  

<span data-ttu-id="c4071-239">Bir ILB ana Azure işlevleri kullandığınızda, "biz işlevlerinizi şu anda mümkün tooretrieve değildir. bildiren bir hata iletisi alabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c4071-239">When you use Azure Functions on an ILB ASE, you might get an error message that says "We are not able tooretrieve your functions right now.</span></span> <span data-ttu-id="c4071-240">Lütfen daha sonra yeniden deneyin."</span><span class="sxs-lookup"><span data-stu-id="c4071-240">Please try again later."</span></span> <span data-ttu-id="c4071-241">Merhaba işlevleri UI hello SCM site HTTPS üzerinden yararlanır ve hello kök sertifikası hello tarayıcı zincirindeki güven olmadığından bu hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="c4071-241">This error occurs because hello Functions UI leverages hello SCM site over HTTPS and hello root certificate is not in hello browser chain of trust.</span></span> <span data-ttu-id="c4071-242">Web işleri benzer bir sorun vardır.</span><span class="sxs-lookup"><span data-stu-id="c4071-242">Web jobs has a similar problem.</span></span> <span data-ttu-id="c4071-243">tooavoid bu sorunu hello aşağıdakilerden birini yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4071-243">tooavoid this problem you can do one of hello following:</span></span>

- <span data-ttu-id="c4071-244">Merhaba sertifika tooyour güvenilen sertifika deposuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c4071-244">Add hello certificate tooyour trusted certificate store.</span></span> <span data-ttu-id="c4071-245">Bu sınır ve Internet Explorer kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c4071-245">This unblocks Edge and Internet Explorer.</span></span>
- <span data-ttu-id="c4071-246">Chrome kullanın ve ilk toohello SCM sitesine gidin, hello güvenilmeyen sertifikayı kabul ve toohello portal gidin.</span><span class="sxs-lookup"><span data-stu-id="c4071-246">Use Chrome and go toohello SCM site first, accept hello untrusted certificate and then go toohello portal.</span></span>
- <span data-ttu-id="c4071-247">Güven, tarayıcı zincirindeki bir ticari sertifikası kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4071-247">Use a commercial certificate that is in your browser chain of trust.</span></span>  <span data-ttu-id="c4071-248">Merhaba en iyi seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="c4071-248">This is hello best option.</span></span>  

## <a name="dns-configuration"></a><span data-ttu-id="c4071-249">DNS yapılandırması</span><span class="sxs-lookup"><span data-stu-id="c4071-249">DNS configuration</span></span> ##

<span data-ttu-id="c4071-250">Bir dış VIP kullandığınızda, DNS hello Azure tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="c4071-250">When you use an External VIP, hello DNS is managed by Azure.</span></span> <span data-ttu-id="c4071-251">Ana oluşturulan herhangi bir uygulama, Genel DNS olduğu tooAzure DNS, otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="c4071-251">Any app created in your ASE is automatically added tooAzure DNS, which is a public DNS.</span></span> <span data-ttu-id="c4071-252">ILB ASE'de kendi DNS yönetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-252">In an ILB ASE, you must manage your own DNS.</span></span> <span data-ttu-id="c4071-253">Gibi belirli bir etki alanının _contoso.net_, DNS A kayıtlarını DNS'e bu noktası tooyour ILB adresini toocreate gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4071-253">For a given domain such as _contoso.net_, you need toocreate DNS A records in your DNS that point tooyour ILB address for:</span></span>

- <span data-ttu-id="c4071-254">*. contoso.net</span><span class="sxs-lookup"><span data-stu-id="c4071-254">*.contoso.net</span></span>
- <span data-ttu-id="c4071-255">*. scm.contoso.net</span><span class="sxs-lookup"><span data-stu-id="c4071-255">*.scm.contoso.net</span></span>

<span data-ttu-id="c4071-256">Bu ana dışında birden çok şey için ILB ana etki alanı kullandıysanız, toomanage DNS başına uygulamanızın-adı temelinde gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c4071-256">If your ILB ASE domain is used for multiple things outside this ASE, you might need toomanage DNS on a per-app-name basis.</span></span> <span data-ttu-id="c4071-257">Oluşturduğunuzda, tooadd her yeni uygulama adı, DNS gerektiği için bu yöntemi bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="c4071-257">This method is challenging because you need tooadd each new app name into your DNS when you create it.</span></span> <span data-ttu-id="c4071-258">Bu nedenle, ayrılmış bir etki alanı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c4071-258">For this reason, we recommend that you use a dedicated domain.</span></span>

## <a name="publish-with-an-ilb-ase"></a><span data-ttu-id="c4071-259">Bir ILB ana ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="c4071-259">Publish with an ILB ASE</span></span> ##

<span data-ttu-id="c4071-260">Oluşturulan her uygulama için iki uç nokta vardır.</span><span class="sxs-lookup"><span data-stu-id="c4071-260">For every app that's created, there are two endpoints.</span></span> <span data-ttu-id="c4071-261">ILB ASE'de elinizde  *&lt;uygulama adı >.&lt; ILB ana etki alanı >* ve  *&lt;uygulama adı > .scm.&lt; ILB ana etki alanı >*.</span><span class="sxs-lookup"><span data-stu-id="c4071-261">In an ILB ASE, you have *&lt;app name>.&lt;ILB ASE Domain>* and *&lt;app name>.scm.&lt;ILB ASE Domain>*.</span></span> 

<span data-ttu-id="c4071-262">Merhaba SCM site adını alır, hello adlı toohello Kudu konsol **Gelişmiş portal**, içinde Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="c4071-262">hello SCM site name takes you toohello Kudu console, called hello **Advanced portal**, within hello Azure portal.</span></span> <span data-ttu-id="c4071-263">Merhaba Kudu konsol, ortam değişkenleri görüntülemek, hello disk keşfetmek, bir konsol ve çok daha fazlasını kullanın sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4071-263">hello Kudu console lets you view environment variables, explore hello disk, use a console, and much more.</span></span> <span data-ttu-id="c4071-264">Daha fazla bilgi için bkz: [Kudu Konsolu Azure App Service için][Kudu].</span><span class="sxs-lookup"><span data-stu-id="c4071-264">For more information, see [Kudu console for Azure App Service][Kudu].</span></span> 

<span data-ttu-id="c4071-265">Merhaba çok kullanıcılı uygulama hizmeti ve bir dış ana yoktur çoklu oturum açma hello Azure portal ve hello Kudu Konsolu arasında.</span><span class="sxs-lookup"><span data-stu-id="c4071-265">In hello multitenant App Service and in an External ASE, there's single sign-on between hello Azure portal and hello Kudu console.</span></span> <span data-ttu-id="c4071-266">Merhaba ILB ana ancak toouse yayımlama kimlik bilgileri toosign hello Kudu konsoluna gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-266">For hello ILB ASE, however, you need toouse your publishing credentials toosign into hello Kudu console.</span></span>

<span data-ttu-id="c4071-267">Yayımlama Hello endpoint Internet erişilebilir olmadığı için Internet tabanlı CI sistemler, GitHub ve Visual Studio Team Services gibi bir ILB ana ile çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="c4071-267">Internet-based CI systems, such as GitHub and Visual Studio Team Services, don't work with an ILB ASE because hello publishing endpoint isn't internet accessible.</span></span> <span data-ttu-id="c4071-268">Bunun yerine, toouse Dropbox gibi bir çekme modeli kullanan bir CI sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4071-268">Instead, you need toouse a CI system that uses a pull model, such as Dropbox.</span></span>

<span data-ttu-id="c4071-269">Yayımlama Hello uç noktaları bir ILB ana uygulamalar için ILB ana oluşturulması sırasında bu hello hello etki alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4071-269">hello publishing endpoints for apps in an ILB ASE use hello domain that hello ILB ASE was created with.</span></span> <span data-ttu-id="c4071-270">Bu etki alanı hello uygulamanın yayımlama profili ve hello uygulamanızın portal dikey penceresinde görünür (**genel bakış** > **Essentials** ve ayrıca **özellikleri**).</span><span class="sxs-lookup"><span data-stu-id="c4071-270">This domain appears in hello app's publishing profile and in hello app's portal blade (**Overview** > **Essentials** and also **Properties**).</span></span> <span data-ttu-id="c4071-271">Merhaba alt etki alanı ile bir ILB ana varsa *contoso.net* ve adlı bir uygulama *mytest*, kullanın *mytest.contoso.net* FTP ve *mytest.scm.contoso.net*  web dağıtımı için.</span><span class="sxs-lookup"><span data-stu-id="c4071-271">If you have an ILB ASE with hello subdomain *contoso.net* and an app named *mytest*, use *mytest.contoso.net* for FTP and *mytest.scm.contoso.net* for web deployment.</span></span>

## <a name="couple-an-ilb-ase-with-a-waf-device"></a><span data-ttu-id="c4071-272">Bir ILB ana WAF aygıt ile eşleştiği</span><span class="sxs-lookup"><span data-stu-id="c4071-272">Couple an ILB ASE with a WAF device</span></span> ##

<span data-ttu-id="c4071-273">Azure uygulama hizmeti hello sistemini koruma birçok güvenlik önlemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c4071-273">Azure App Service provides many security measures that protect hello system.</span></span> <span data-ttu-id="c4071-274">Bir uygulama ele olup olmadığını da toodetermine yardımcı olurlar.</span><span class="sxs-lookup"><span data-stu-id="c4071-274">They also help toodetermine whether an app was hacked.</span></span> <span data-ttu-id="c4071-275">Merhaba en iyi bir web uygulaması için bir barındırma platformuyla, Azure uygulama hizmeti gibi bir web uygulaması Güvenlik Duvarı (WAF) toocouple korumadır.</span><span class="sxs-lookup"><span data-stu-id="c4071-275">hello best protection for a web application is toocouple a hosting platform, such as Azure App Service, with a web application firewall (WAF).</span></span> <span data-ttu-id="c4071-276">Merhaba ILB ana ağ yalıtılmış uygulama uç noktası olduğundan, bu tür bir kullanım için uygundur.</span><span class="sxs-lookup"><span data-stu-id="c4071-276">Because hello ILB ASE has a network-isolated application endpoint, it's appropriate for such a use.</span></span>

<span data-ttu-id="c4071-277">toolearn tooconfigure, ILB ana WAF aygıtla nasıl görürüm hakkında daha fazla [, uygulama hizmeti ortamınızı ile bir web uygulaması güvenlik duvarı yapılandırma][ASEWAF].</span><span class="sxs-lookup"><span data-stu-id="c4071-277">toolearn more about how tooconfigure your ILB ASE with a WAF device, see [Configure a web application firewall with your App Service environment][ASEWAF].</span></span> <span data-ttu-id="c4071-278">Bu makalede gösterilmektedir nasıl toouse Barracuda sanal gereç, ana ile.</span><span class="sxs-lookup"><span data-stu-id="c4071-278">This article shows how toouse a Barracuda virtual appliance with your ASE.</span></span> <span data-ttu-id="c4071-279">Toouse Azure uygulama ağ geçidi başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="c4071-279">Another option is toouse Azure Application Gateway.</span></span> <span data-ttu-id="c4071-280">Uygulama ağ geçidi herhangi bir uygulama arkasında yerleştirilen hello OWASP çekirdek kuralları toosecure kullanır.</span><span class="sxs-lookup"><span data-stu-id="c4071-280">Application Gateway uses hello OWASP core rules toosecure any applications placed behind it.</span></span> <span data-ttu-id="c4071-281">Uygulama ağ geçidi hakkında daha fazla bilgi için bkz: [giriş toohello Azure web uygulaması güvenlik duvarı][AppGW].</span><span class="sxs-lookup"><span data-stu-id="c4071-281">For more information about Application Gateway, see [Introduction toohello Azure web application firewall][AppGW].</span></span>

## <a name="get-started"></a><span data-ttu-id="c4071-282">başlarken</span><span class="sxs-lookup"><span data-stu-id="c4071-282">Get started</span></span> ##

<span data-ttu-id="c4071-283">Tüm makaleler ve nasıl tooinstructions ASEs için kullanılabilir olan [uygulama hizmeti ortamları için Benioku][ASEReadme].</span><span class="sxs-lookup"><span data-stu-id="c4071-283">All articles and how-tooinstructions for ASEs are available in the [README for App Service environments][ASEReadme].</span></span>

* <span data-ttu-id="c4071-284">ASEs ile başlatılan tooget bkz [giriş tooApp hizmeti ortamları][Intro].</span><span class="sxs-lookup"><span data-stu-id="c4071-284">tooget started with ASEs, see [Introduction tooApp Service environments][Intro].</span></span>
* <span data-ttu-id="c4071-285">Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span><span class="sxs-lookup"><span data-stu-id="c4071-285">For more information about hello Azure App Service platform, see [Azure App Service](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).</span></span>
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

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
