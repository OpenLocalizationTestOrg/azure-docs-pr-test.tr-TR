---
title: "Bulut Hizmetleri özel etki alanı adının aaaConfigure | Microsoft Docs"
description: "Bilgi nasıl tooexpose Azure uygulamanızı veya veri DNS ayarları yapılandırarak özel bir etki alanı üzerinde."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="9244d-103">Bir Azure bulut hizmeti için bir özel etki alanı adı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9244d-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9244d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9244d-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="9244d-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="9244d-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="9244d-106">Bir bulut hizmeti oluşturduğunuzda, Azure cloudapp.net tooa etki alanının alt atar.</span><span class="sxs-lookup"><span data-stu-id="9244d-106">When you create a Cloud Service, Azure assigns it tooa subdomain of cloudapp.net.</span></span> <span data-ttu-id="9244d-107">Örneğin, bulut hizmetinizin "contoso" ise, kullanıcılarınızın olacak mümkün tooaccess uygulamanızda http://contoso.cloudapp.net gibi bir URL olabilir.</span><span class="sxs-lookup"><span data-stu-id="9244d-107">For example, if your Cloud Service is named "contoso", your users will be able tooaccess your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="9244d-108">Azure de bir sanal IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="9244d-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="9244d-109">Ancak, kendi etki alanı adı, örneğin, contoso.com üzerinde uygulamanız getirebilir. Bu makalede açıklanır nasıl tooreserve veya Bulut hizmeti web rolleri için özel etki alanı adı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9244d-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how tooreserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="9244d-110">CNAME ve A kayıtlarını nelerdir zaten biliyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="9244d-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="9244d-111">[Atlama hello açıklama geçmiş](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="9244d-111">[Jump past hello explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="9244d-112">Daha hızlı giderek olun!</span><span class="sxs-lookup"><span data-stu-id="9244d-112">Get going faster!</span></span> <span data-ttu-id="9244d-113">Kullanım hello Azure [izlenecek destekli](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="9244d-113">Use hello Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="9244d-114">Özel etki alanı adı ilişkilendirme ve bir ek Azure Cloud Services veya Azure Web siteleri ile iletişim (SSL) güvenli hale getirme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="9244d-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="9244d-115">Bu görevde Hello yordamlar tooAzure bulut Hizmetleri geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9244d-115">hello procedures in this task apply tooAzure Cloud Services.</span></span> <span data-ttu-id="9244d-116">Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="9244d-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="9244d-117">Depolama hesapları için bkz: [bu](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="9244d-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="9244d-118">CNAME ve A kayıtları anlama</span><span class="sxs-lookup"><span data-stu-id="9244d-118">Understand CNAME and A records</span></span>
<span data-ttu-id="9244d-119">CNAME (veya diğer ad kayıtları) ve bir kayıt hem tooassociate belirli bir sunucunun bir etki alanı adıyla izin ver (veya bu durumda, hizmet) ancak bunlar farklı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="9244d-119">CNAME (or alias records) and A records both allow you tooassociate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="9244d-120">Aynı zamanda bir kayıt hangi toouse karar vermeden önce dikkate almanız gereken Azure bulut Hizmetleri ile kullanırken ayrıca bazı belirli noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="9244d-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which toouse.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="9244d-121">CNAME veya diğer ad kaydı</span><span class="sxs-lookup"><span data-stu-id="9244d-121">CNAME or Alias record</span></span>
<span data-ttu-id="9244d-122">Bir CNAME kaydı eşleyen bir *belirli* etki alanı gibi **contoso.com** veya **www.contoso.com**, tooa kurallı etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="9244d-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, tooa canonical domain name.</span></span> <span data-ttu-id="9244d-123">Bu durumda, hello hello kurallı etki alanı adı olduğundan **[Uygulamam] .cloudapp .net** Azure etki alanı adını barındırılan uygulama.</span><span class="sxs-lookup"><span data-stu-id="9244d-123">In this case, hello canonical domain name is hello **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="9244d-124">Bir kez oluşturduktan sonra hello CNAME hello için diğer ad oluşturur **[Uygulamam] .cloudapp .net**.</span><span class="sxs-lookup"><span data-stu-id="9244d-124">Once created, hello CNAME creates an alias for hello **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="9244d-125">Merhaba CNAME girişi toohello IP adresini çözümlenir, **[Uygulamam] .cloudapp .net** hello bulut hizmetinin başlangıç IP adresi değişirse, tootake herhangi bir eylem olmayan şekilde otomatik olarak, hizmet.</span><span class="sxs-lookup"><span data-stu-id="9244d-125">hello CNAME entry will resolve toohello IP address of your **[myapp].cloudapp.net** service automatically, so if hello IP address of hello cloud service changes, you do not have tootake any action.</span></span>

> [!NOTE]
> <span data-ttu-id="9244d-126">Bazı etki alanı kayıt yalnızca toomap alt etki alanları www.contoso.com ve contoso.com gibi kök adları değil gibi bir CNAME kaydı kullanırken sağlar. CNAME kayıtları hakkında daha fazla bilgi için şirketiniz tarafından sağlanan hello belgelerine bakın [CNAME kaydı Wikipedia girişinde hello](http://en.wikipedia.org/wiki/CNAME_record), veya hello [IETF etki alanı adları - uygulama ve belirtim](http://tools.ietf.org/html/rfc1035) Belge.</span><span class="sxs-lookup"><span data-stu-id="9244d-126">Some domain registrars only allow you toomap subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see hello documentation provided by your registrar, [hello Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or hello [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="9244d-127">Bir kayıt</span><span class="sxs-lookup"><span data-stu-id="9244d-127">A record</span></span>
<span data-ttu-id="9244d-128">Bir A kaydı bir etki alanı gibi eşleştirir **contoso.com** veya **www.contoso.com**, *veya bir joker karakter etki alanı* gibi  **\*. contoso.com**, tooan IP adresi.</span><span class="sxs-lookup"><span data-stu-id="9244d-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, tooan IP address.</span></span> <span data-ttu-id="9244d-129">Azure bulut hizmeti Hello durumda hello hizmetinin sanal IP hello.</span><span class="sxs-lookup"><span data-stu-id="9244d-129">In hello case of an Azure Cloud Service, hello virtual IP of hello service.</span></span> <span data-ttu-id="9244d-130">Bir A kaydı bir CNAME kaydı üzerinden ana avantajı Hello gibi bir joker karakter kullanan bir giriş olduğunu nedenle \* **. contoso.com**, hangi işlemek birden çok alt etki alanı için istekleri gibi  **Mail.contoso.com**, **login.contoso.com**, veya **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="9244d-130">So hello main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="9244d-131">Bir A kaydı eşlenen beri tooa statik IP adresi otomatik olarak bulut hizmetinizin değişiklikleri toohello IP adresi çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="9244d-131">Since an A record is mapped tooa static IP address, it cannot automatically resolve changes toohello IP address of your Cloud Service.</span></span> <span data-ttu-id="9244d-132">Başlangıç IP adresi, bulut hizmeti tarafından kullanılan tooan boş yuva (üretim veya hazırlama.) dağıtmak ilk kez hello ayrılır Merhaba dağıtım hello yuva için silerseniz, başlangıç IP adresi Azure tarafından yayınlanan ve tüm gelecekteki dağıtımlar toohello yuvası verilen yeni bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="9244d-132">hello IP address used by your Cloud Service is allocated hello first time you deploy tooan empty slot (either production or staging.) If you delete hello deployment for hello slot, hello IP address is released by Azure and any future deployments toohello slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="9244d-133">Başlangıç IP adresi (üretim veya hazırlama) belirli dağıtım yuvasının rahat, hazırlama ve üretim dağıtımları veya varolan bir dağıtım yerinde yükseltme gerçekleştirme arasında takası zaman kalıcı.</span><span class="sxs-lookup"><span data-stu-id="9244d-133">Conveniently, hello IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="9244d-134">Bu eylemler gerçekleştirme hakkında daha fazla bilgi için bkz: [nasıl toomanage bulut hizmetlerini](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="9244d-134">For more information on performing these actions, see [How toomanage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="9244d-135">Özel etki alanınız için bir CNAME kaydı ekleyin</span><span class="sxs-lookup"><span data-stu-id="9244d-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="9244d-136">toocreate bir CNAME kaydı, kayıt şirketiniz tarafından sağlanan hello araçları kullanarak özel etki alanınız için hello DNS tablosunda yeni bir giriş eklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="9244d-136">toocreate a CNAME record, you must add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="9244d-137">Her kayıt için bir CNAME kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, kavramlar hello hello aynı.</span><span class="sxs-lookup"><span data-stu-id="9244d-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="9244d-138">Bu yöntemleri toofind hello birini kullanın **. cloudapp.net** tooyour bulut hizmetine atanan etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="9244d-138">Use one of these methods toofind hello **.cloudapp.net** domain name assigned tooyour cloud service.</span></span>
   
   * <span data-ttu-id="9244d-139">Oturum açma toohello [Klasik Azure portalı], bulut hizmetinizi seçin, **Pano**, hello bulun **Site URL'si** hello girişi **Hızlı Bakış**  bölümü.</span><span class="sxs-lookup"><span data-stu-id="9244d-139">Login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Site URL** entry in hello **quick glance** section.</span></span>
     
       ![Hızlı Bakış bölümüne Hello site URL'si gösterme][csurl]
     
       <span data-ttu-id="9244d-141">**VEYA**</span><span class="sxs-lookup"><span data-stu-id="9244d-141">**OR**</span></span>  
   * <span data-ttu-id="9244d-142">Yükleme ve yapılandırma [Azure Powershell](/powershell/azure/overview), ve ardından kullanımı hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="9244d-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="9244d-143">Merhaba etki alanı adı ya da yöntemi tarafından döndürülen hello URL'de bir CNAME kaydı oluştururken gerekir olarak kullanılan kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9244d-143">Save hello domain name used in hello URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="9244d-144">Tooyour DNS kayıt şirketinizin sitesinde oturum ve DNS yönetme toohello sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="9244d-144">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="9244d-145">Bağlantıları arayın veya hello sitesinin alanları etiketli olarak **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="9244d-145">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="9244d-146">Şimdi burada seçin veya CNAME'ın girin bulun.</span><span class="sxs-lookup"><span data-stu-id="9244d-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="9244d-147">Bir açılan yazın veya Gelişmiş Ayarları sayfası tooan Git tooselect hello kaydına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9244d-147">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span> <span data-ttu-id="9244d-148">Merhaba sözcükleri göz önünde bulundurmanız gerekenler **CNAME**, **diğer**, veya **alt etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="9244d-148">You should look for hello words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="9244d-149">Ayrıca hello etki alanı ya da alt etki alanı diğer adı Merhaba CNAME, gibi sağlamanız gereken **www** için diğer ad toocreate istiyorsanız **www.customdomain.com**. Hello kök etki alanı için bir diğer ad toocreate istiyorsanız, bunu hello listelenmeyebilir '**@**' kayıt şirketinizin DNS araçlarında simgesi.</span><span class="sxs-lookup"><span data-stu-id="9244d-149">You must also provide hello domain or subdomain alias for hello CNAME, such as **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate an alias for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="9244d-150">Ardından, uygulamanızın bir kurallı ana bilgisayar adı sağlamalısınız **cloudapp.net** bu durumda etki alanı.</span><span class="sxs-lookup"><span data-stu-id="9244d-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="9244d-151">Örneğin, gelen tüm trafiği CNAME kaydını aşağıdaki hello iletir **www.contoso.com** çok**contoso.cloudapp.net**, dağıtılan uygulamanızın hello özel etki alanı adı:</span><span class="sxs-lookup"><span data-stu-id="9244d-151">For example, hello following CNAME record forwards all traffic from **www.contoso.com** too**contoso.cloudapp.net**, hello custom domain name of your deployed application:</span></span>

| <span data-ttu-id="9244d-152">Diğer ad/ana bilgisayar adı/alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="9244d-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="9244d-153">Kurallı etki alanı</span><span class="sxs-lookup"><span data-stu-id="9244d-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="9244d-154">www</span><span class="sxs-lookup"><span data-stu-id="9244d-154">www</span></span> |<span data-ttu-id="9244d-155">contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="9244d-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="9244d-156">Bir ziyaretçi, **www.contoso.com** iletme işlemi hello görünmez toothe son kullanıcı olacak şekilde hello gerçek ana bilgisayar (contoso.cloudapp.net) hiçbir zaman görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9244d-156">A visitor of **www.contoso.com** will never see hello true host (contoso.cloudapp.net), so hello forwarding process is invisible toothe end user.</span></span>

> [!NOTE]
> <span data-ttu-id="9244d-157">Merhaba yukarıdaki örnekte yalnızca hello adresindeki tootraffic geçerlidir **www** alt etki alanı.</span><span class="sxs-lookup"><span data-stu-id="9244d-157">hello example above only applies tootraffic at hello **www** subdomain.</span></span> <span data-ttu-id="9244d-158">Sahip CNAME kayıtlarına joker karakterler kullanılamaz olduğundan, her etki alanı/alt etki alanı için bir CNAME oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9244d-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="9244d-159">Alt etki alanları, toodirect trafiğinden gibi istiyorsanız \*. contoso.com, tooyour cloudapp.net adres, yapılandırabileceğiniz bir **yeniden yönlendirme URL'si** veya **İleri URL** DNS ayarlarınız girişte veya bir A kaydını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9244d-159">If you want toodirect  traffic from subdomains, such as \*.contoso.com, tooyour cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="9244d-160">Özel etki alanınız için bir A kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="9244d-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="9244d-161">toocreate bir A kaydı hello sanal IP adresi bulut hizmetinizin ilk bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9244d-161">toocreate an A record, you must first find hello virtual IP address of your cloud service.</span></span> <span data-ttu-id="9244d-162">Ardından yeni bir giriş hello özel etki alanınız için DNS tablosunda kayıt şirketiniz tarafından sağlanan hello araçları kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9244d-162">Then add a new entry in hello DNS table for your custom domain by using hello tools provided by your registrar.</span></span> <span data-ttu-id="9244d-163">Her kayıt için bir A kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, kavramlar hello hello aynı.</span><span class="sxs-lookup"><span data-stu-id="9244d-163">Each registrar has a similar but slightly different method of specifying an A record, but hello concepts are hello same.</span></span>

1. <span data-ttu-id="9244d-164">Yöntemleri tooget hello IP adresini bulut hizmetinizin izleyen hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9244d-164">Use one of hello following methods tooget hello IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="9244d-165">oturum açma toohello [Klasik Azure portalı], bulut hizmetinizi seçin, **Pano**, hello bulun **ortak sanal IP (VIP) adresi** hello girişi**Hızlı Bakış** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9244d-165">login toohello [Azure classic portal], select your cloud service, select **Dashboard**, and then find hello **Public Virtual IP (VIP) address** entry in hello **quick glance** section.</span></span>
     
       ![Hızlı Bakış bölümüne Hello VIP gösterme][vip]
     
       <span data-ttu-id="9244d-167">**VEYA**</span><span class="sxs-lookup"><span data-stu-id="9244d-167">**OR**</span></span>  
   * <span data-ttu-id="9244d-168">Yükleme ve yapılandırma [Azure Powershell](/powershell/azure/overview), ve ardından kullanımı hello aşağıdaki komutu:</span><span class="sxs-lookup"><span data-stu-id="9244d-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use hello following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="9244d-169">Bulut hizmetiniz ile ilişkili birden çok uç nokta varsa, başlangıç IP adresi içeren birden fazla satır alırsınız, ancak tüm görüntülenmelidir aynı hello adresi.</span><span class="sxs-lookup"><span data-stu-id="9244d-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing hello IP address, but all should display hello same address.</span></span>
     
     <span data-ttu-id="9244d-170">Başlangıç IP adresi, bir A kaydı oluştururken gerekir olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9244d-170">Save hello IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="9244d-171">Tooyour DNS kayıt şirketinizin sitesinde oturum ve DNS yönetme toohello sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="9244d-171">Log on tooyour DNS registrar's website and go toohello page for managing DNS.</span></span> <span data-ttu-id="9244d-172">Bağlantıları arayın veya hello sitesinin alanları etiketli olarak **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="9244d-172">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="9244d-173">Şimdi burada seçin veya bir kaydın girin bulun.</span><span class="sxs-lookup"><span data-stu-id="9244d-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="9244d-174">Bir açılan yazın veya Gelişmiş Ayarları sayfası tooan Git tooselect hello kaydına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9244d-174">You may have tooselect hello record type from a drop down, or go tooan advanced settings page.</span></span>
4. <span data-ttu-id="9244d-175">Merhaba etki alanı ya da bu A kaydı kullanacağı alt etki alanı girin veya seçin.</span><span class="sxs-lookup"><span data-stu-id="9244d-175">Select or enter hello domain or subdomain that will use this A record.</span></span> <span data-ttu-id="9244d-176">Örneğin, seçin **www** için diğer ad toocreate istiyorsanız **www.customdomain.com**. Tüm alt etki alanlarını toocreate bir joker karakter girişi istiyorsanız, '__*__'.</span><span class="sxs-lookup"><span data-stu-id="9244d-176">For example, select **www** if you want toocreate an alias for **www.customdomain.com**. If you want toocreate a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="9244d-177">Bu gibi tüm alt etki alanlarını kapsar **mail.customdomain.com**, **login.customdomain.com**, ve **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="9244d-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="9244d-178">Merhaba kök etki alanı toocreate bir A kaydını istiyorsanız, bunu hello listelenmeyebilir '**@**' kayıt şirketinizin DNS araçlarında simgesi.</span><span class="sxs-lookup"><span data-stu-id="9244d-178">If you want toocreate an A record for hello root domain, it may be listed as hello '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="9244d-179">Bulut Hizmetinizin başlangıç IP adresi alanı sağlanan hello girin.</span><span class="sxs-lookup"><span data-stu-id="9244d-179">Enter hello IP address of your cloud service in hello provided field.</span></span> <span data-ttu-id="9244d-180">Bu, bulut hizmeti dağıtımınızın hello IP adresiyle hello A kaydında kullanılan hello etki alanı girdisi ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="9244d-180">This associates hello domain entry used in hello A record with hello IP address of your cloud service deployment.</span></span>

<span data-ttu-id="9244d-181">Örneğin, bir kaydı takip hello gelen tüm trafiği iletir **contoso.com** çok**137.135.70.239**, hello dağıtılan uygulamanızın IP adresi:</span><span class="sxs-lookup"><span data-stu-id="9244d-181">For example, hello following A record forwards all traffic from **contoso.com** too**137.135.70.239**, hello IP address of your deployed application:</span></span>

| <span data-ttu-id="9244d-182">Ana bilgisayar adı/alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="9244d-182">Host name/Subdomain</span></span> | <span data-ttu-id="9244d-183">IP adresi</span><span class="sxs-lookup"><span data-stu-id="9244d-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="9244d-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="9244d-184">137.135.70.239</span></span> |

<span data-ttu-id="9244d-185">Bu örnek, bir A kaydı hello kök etki alanı oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="9244d-185">This example demonstrates creating an A record for hello root domain.</span></span> <span data-ttu-id="9244d-186">Joker karakter girişi toocover toocreate isterseniz, tüm alt etki alanları, girersiniz '__*__' hello alt etki alanı olarak.</span><span class="sxs-lookup"><span data-stu-id="9244d-186">If you wish toocreate a wildcard entry toocover all subdomains, you would enter '__*__' as hello subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="9244d-187">Azure'daki IP adresleri, varsayılan olarak dinamik.</span><span class="sxs-lookup"><span data-stu-id="9244d-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="9244d-188">Büyük olasılıkla toouse isteyeceksiniz bir [ayrılmış IP adresi](../virtual-network/virtual-networks-reserved-public-ip.md) IP adresiniz değişmeyen tooensure.</span><span class="sxs-lookup"><span data-stu-id="9244d-188">You will probably want toouse a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9244d-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9244d-189">Next steps</span></span>
* [<span data-ttu-id="9244d-190">TooManage Cloud Services nasıl</span><span class="sxs-lookup"><span data-stu-id="9244d-190">How tooManage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="9244d-191">Nasıl tooMap CDN içerik tooa özel etki alanı</span><span class="sxs-lookup"><span data-stu-id="9244d-191">How tooMap CDN Content tooa Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="9244d-192">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="9244d-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="9244d-193">Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9244d-193">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="9244d-194">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="9244d-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[Klasik Azure portalı]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
