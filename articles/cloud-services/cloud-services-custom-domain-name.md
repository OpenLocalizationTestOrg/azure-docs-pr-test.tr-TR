---
title: "Bulut Hizmetleri'nde bir özel etki alanı adı yapılandırma | Microsoft Docs"
description: "Azure uygulama veya özel bir etki alanı veri DNS ayarlarını yapılandırarak öğrenin."
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
ms.openlocfilehash: 9f872fd5119042945356225a80331da18f3a6d99
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a><span data-ttu-id="72768-103">Bir Azure bulut hizmeti için bir özel etki alanı adı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="72768-103">Configuring a custom domain name for an Azure cloud service</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72768-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="72768-104">Azure portal</span></span>](cloud-services-custom-domain-name-portal.md)
> * [<span data-ttu-id="72768-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="72768-105">Azure classic portal</span></span>](cloud-services-custom-domain-name.md)
> 
> 

<span data-ttu-id="72768-106">Azure bulut hizmeti oluşturduğunuzda, bir etki alanının alt cloudapp.net için atar.</span><span class="sxs-lookup"><span data-stu-id="72768-106">When you create a Cloud Service, Azure assigns it to a subdomain of cloudapp.net.</span></span> <span data-ttu-id="72768-107">Örneğin, bulut hizmetinizin "contoso" ise, kullanıcılarınız uygulamanızda http://contoso.cloudapp.net gibi bir URL erişebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="72768-107">For example, if your Cloud Service is named "contoso", your users will be able to access your application on a URL like http://contoso.cloudapp.net.</span></span> <span data-ttu-id="72768-108">Azure de bir sanal IP adresi atar.</span><span class="sxs-lookup"><span data-stu-id="72768-108">Azure also assigns a virtual IP address.</span></span>

<span data-ttu-id="72768-109">Ancak, kendi etki alanı adı, örneğin, contoso.com üzerinde uygulamanız getirebilir. Bu makalede, ayırmak veya Bulut hizmeti web rolleri için bir özel etki alanı adı yapılandırma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="72768-109">However, you can also expose your application on your own domain name, such as contoso.com. This article explains how to reserve or configure a custom domain name for Cloud Service web roles.</span></span>

<span data-ttu-id="72768-110">CNAME ve A kayıtlarını nelerdir zaten biliyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="72768-110">Do you already understand what CNAME and A records are?</span></span> <span data-ttu-id="72768-111">[Açıklama geçmiş atlama](#add-a-cname-record-for-your-custom-domain).</span><span class="sxs-lookup"><span data-stu-id="72768-111">[Jump past the explanation](#add-a-cname-record-for-your-custom-domain).</span></span>

> [!NOTE]
> <span data-ttu-id="72768-112">Daha hızlı giderek olun!</span><span class="sxs-lookup"><span data-stu-id="72768-112">Get going faster!</span></span> <span data-ttu-id="72768-113">Azure kullanmak [izlenecek destekli](http://support.microsoft.com/kb/2990804).</span><span class="sxs-lookup"><span data-stu-id="72768-113">Use the Azure [guided walkthrough](http://support.microsoft.com/kb/2990804).</span></span> <span data-ttu-id="72768-114">Özel etki alanı adı ilişkilendirme ve bir ek Azure Cloud Services veya Azure Web siteleri ile iletişim (SSL) güvenli hale getirme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="72768-114">It makes associating a custom domain name and securing communication (SSL) with Azure Cloud Services or Azure Websites a snap.</span></span>
> 
> 

<p/>

> [!NOTE]
> <span data-ttu-id="72768-115">Bu görevde yordamlar Azure bulut Hizmetleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="72768-115">The procedures in this task apply to Azure Cloud Services.</span></span> <span data-ttu-id="72768-116">Uygulama hizmetleri için bkz: [bu](../app-service-web/web-sites-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="72768-116">For App Services, see [this](../app-service-web/web-sites-custom-domain-name.md).</span></span> <span data-ttu-id="72768-117">Depolama hesapları için bkz: [bu](../storage/blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="72768-117">For storage accounts, see [this](../storage/blobs/storage-custom-domain-name.md).</span></span>
> 
> 

## <a name="understand-cname-and-a-records"></a><span data-ttu-id="72768-118">CNAME ve A kayıtları anlama</span><span class="sxs-lookup"><span data-stu-id="72768-118">Understand CNAME and A records</span></span>
<span data-ttu-id="72768-119">CNAME (veya diğer ad kayıtları) ve her iki A kayıtlarını belirli bir sunucuyla bir etki alanı adı ilişkilendirmek (veya bu durumda, hizmet) ancak bunlar farklı şekilde çalışır izin verir.</span><span class="sxs-lookup"><span data-stu-id="72768-119">CNAME (or alias records) and A records both allow you to associate a domain name with a specific server (or service in this case,) however they work differently.</span></span> <span data-ttu-id="72768-120">Aynı zamanda bir kayıtları kullanılacak karar vermeden önce dikkate almanız gereken Azure bulut Hizmetleri ile kullanırken ayrıca bazı belirli noktalar vardır.</span><span class="sxs-lookup"><span data-stu-id="72768-120">There are also some specific considerations when using A records with Azure Cloud services that you should consider before deciding which to use.</span></span>

### <a name="cname-or-alias-record"></a><span data-ttu-id="72768-121">CNAME veya diğer ad kaydı</span><span class="sxs-lookup"><span data-stu-id="72768-121">CNAME or Alias record</span></span>
<span data-ttu-id="72768-122">Bir CNAME kaydı eşleyen bir *belirli* etki alanı gibi **contoso.com** veya **www.contoso.com**, kurallı etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="72768-122">A CNAME record maps a *specific* domain, such as **contoso.com** or **www.contoso.com**, to a canonical domain name.</span></span> <span data-ttu-id="72768-123">Bu durumda, kurallı etki alanı adıdır **[Uygulamam] .cloudapp .net** Azure etki alanı adını barındırılan uygulama.</span><span class="sxs-lookup"><span data-stu-id="72768-123">In this case, the canonical domain name is the **[myapp].cloudapp.net** domain name of your Azure hosted application.</span></span> <span data-ttu-id="72768-124">Oluşturduktan sonra CNAME için diğer ad oluşturur **[Uygulamam] .cloudapp .net**.</span><span class="sxs-lookup"><span data-stu-id="72768-124">Once created, the CNAME creates an alias for the **[myapp].cloudapp.net**.</span></span> <span data-ttu-id="72768-125">CNAME girişi IP adresine çözümleyecek, **[Uygulamam] .cloudapp .net** bulut hizmeti IP adresi değişirse, herhangi bir eylemde bulunmanız gerekmez şekilde otomatik olarak, hizmet.</span><span class="sxs-lookup"><span data-stu-id="72768-125">The CNAME entry will resolve to the IP address of your **[myapp].cloudapp.net** service automatically, so if the IP address of the cloud service changes, you do not have to take any action.</span></span>

> [!NOTE]
> <span data-ttu-id="72768-126">Bazı etki alanı kayıt yalnızca www.contoso.com ve contoso.com gibi kök adları değil gibi bir CNAME kaydı kullanırken alt etki alanlarını eşleme izin verir. CNAME kayıtları hakkında daha fazla bilgi için şirketiniz tarafından sağlanan belgelere bakın [CNAME kaydı Wikipedia girişinde](http://en.wikipedia.org/wiki/CNAME_record), veya [IETF etki alanı adları - uygulama ve belirtim](http://tools.ietf.org/html/rfc1035) belge.</span><span class="sxs-lookup"><span data-stu-id="72768-126">Some domain registrars only allow you to map subdomains when using a CNAME record, such as www.contoso.com, and not root names, such as contoso.com. For more information on CNAME records, see the documentation provided by your registrar, [the Wikipedia entry on CNAME record](http://en.wikipedia.org/wiki/CNAME_record), or the [IETF Domain Names - Implementation and Specification](http://tools.ietf.org/html/rfc1035) document.</span></span>
> 
> 

### <a name="a-record"></a><span data-ttu-id="72768-127">Bir kayıt</span><span class="sxs-lookup"><span data-stu-id="72768-127">A record</span></span>
<span data-ttu-id="72768-128">Bir A kaydı bir etki alanı gibi eşleştirir **contoso.com** veya **www.contoso.com**, *veya bir joker karakter etki alanı* gibi  **\*. contoso.com**, bir IP adresi için.</span><span class="sxs-lookup"><span data-stu-id="72768-128">An A record maps a domain, such as **contoso.com** or **www.contoso.com**, *or a wildcard domain* such as **\*.contoso.com**, to an IP address.</span></span> <span data-ttu-id="72768-129">Azure bulut hizmeti söz konusu olduğunda, sanal IP hizmetinin.</span><span class="sxs-lookup"><span data-stu-id="72768-129">In the case of an Azure Cloud Service, the virtual IP of the service.</span></span> <span data-ttu-id="72768-130">Bir A kaydı bir CNAME kaydı üzerinden ana avantajı gibi bir joker karakter kullanan bir giriş olduğunu nedenle \* **. contoso.com**, hangi işlemek birden çok alt etki alanı için istekleri gibi **mail.contoso.com**, **login.contoso.com**, veya **www.contso.com**.</span><span class="sxs-lookup"><span data-stu-id="72768-130">So the main benefit of an A record over a CNAME record is that you can have one entry that uses a wildcard, such as \***.contoso.com**, which would handle requests for multiple sub-domains such as **mail.contoso.com**, **login.contoso.com**, or **www.contso.com**.</span></span>

> [!NOTE]
> <span data-ttu-id="72768-131">Bir A kaydı bir statik IP adresine eşlenmiş olduğundan, bu değişiklikleri otomatik olarak bulut hizmetinizin IP adresi çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="72768-131">Since an A record is mapped to a static IP address, it cannot automatically resolve changes to the IP address of your Cloud Service.</span></span> <span data-ttu-id="72768-132">Bulut hizmeti tarafından kullanılan IP adresi boş bir yuvaya (üretim veya hazırlama.) dağıtmak ilk kez ayrılır Dağıtım yuvası için silerseniz, IP adresi Azure tarafından yayımlanan ve gelecekteki tüm dağıtımlar yuvaya verilen yeni bir IP adresi.</span><span class="sxs-lookup"><span data-stu-id="72768-132">The IP address used by your Cloud Service is allocated the first time you deploy to an empty slot (either production or staging.) If you delete the deployment for the slot, the IP address is released by Azure and any future deployments to the slot may be given a new IP address.</span></span>
> 
> <span data-ttu-id="72768-133">Uygun şekilde, bir belirtilen dağıtım yuvası (üretim veya hazırlama) IP adresini hazırlama ve üretim dağıtımları veya varolan bir dağıtım yerinde yükseltme gerçekleştirme arasında takası zaman kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="72768-133">Conveniently, the IP address of a given deployment slot (production or staging) is persisted when swapping between staging and production deployments or performing an in-place upgrade of an existing deployment.</span></span> <span data-ttu-id="72768-134">Bu eylemler gerçekleştirme hakkında daha fazla bilgi için bkz: [bulut hizmetlerini yönetmek nasıl](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="72768-134">For more information on performing these actions, see [How to manage cloud services](cloud-services-how-to-manage.md).</span></span>
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="72768-135">Özel etki alanınız için bir CNAME kaydı ekleyin</span><span class="sxs-lookup"><span data-stu-id="72768-135">Add a CNAME record for your custom domain</span></span>
<span data-ttu-id="72768-136">Bir CNAME kaydı oluşturmak için yeni bir giriş DNS tabloda özel etki alanınız için şirketiniz tarafından sağlanan araçları kullanarak eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="72768-136">To create a CNAME record, you must add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="72768-137">Her kayıt için bir CNAME kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, kavramlar aynıdır.</span><span class="sxs-lookup"><span data-stu-id="72768-137">Each registrar has a similar but slightly different method of specifying a CNAME record, but the concepts are the same.</span></span>

1. <span data-ttu-id="72768-138">Bulmak için aşağıdaki yöntemlerden birini kullanın **. cloudapp.net** bulut Hizmetinize atanmış etki alanı adı.</span><span class="sxs-lookup"><span data-stu-id="72768-138">Use one of these methods to find the **.cloudapp.net** domain name assigned to your cloud service.</span></span>
   
   * <span data-ttu-id="72768-139">Oturum açma [Klasik Azure portalı], bulut hizmetinizi seçin, **Pano**ve ardından bulmak **Site URL'si** girişi **Hızlı Bakış**bölümü.</span><span class="sxs-lookup"><span data-stu-id="72768-139">Login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Site URL** entry in the **quick glance** section.</span></span>
     
       ![Hızlı Bakış bölümüne site URL'si gösterme][csurl]
     
       <span data-ttu-id="72768-141">**VEYA**</span><span class="sxs-lookup"><span data-stu-id="72768-141">**OR**</span></span>  
   * <span data-ttu-id="72768-142">Yükleme ve yapılandırma [Azure Powershell](/powershell/azure/overview)ve ardından aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="72768-142">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     <span data-ttu-id="72768-143">Her iki yöntemi tarafından döndürülen URL bir CNAME kaydı oluştururken gerekir olarak kullanılan etki alanı adı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72768-143">Save the domain name used in the URL returned by either method, as you will need it when creating a CNAME record.</span></span>
2. <span data-ttu-id="72768-144">DNS kaydedicinizin Web sitesinde oturum açın ve DNS Yönetme sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="72768-144">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="72768-145">Bağlantıları veya olarak etiketli sitesinin alanları arayın **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="72768-145">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="72768-146">Şimdi burada seçin veya CNAME'ın girin bulun.</span><span class="sxs-lookup"><span data-stu-id="72768-146">Now find where you can select or enter CNAME's.</span></span> <span data-ttu-id="72768-147">Aşağı açılır bir kayıt türü seçin veya Gelişmiş Ayarları sayfasına gitmek zorunda kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72768-147">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span> <span data-ttu-id="72768-148">Sözcükleri göz önünde bulundurmanız gerekenler **CNAME**, **diğer**, veya **alt etki alanları**.</span><span class="sxs-lookup"><span data-stu-id="72768-148">You should look for the words **CNAME**, **Alias**, or **Subdomains**.</span></span>
4. <span data-ttu-id="72768-149">Ayrıca etki alanı ya da alt etki alanı diğer adı için CNAME, gibi sağlamanız gereken **www** için diğer ad oluşturmak istiyorsanız **www.customdomain.com**. Kök etki alanı için diğer ad oluşturmak istiyorsanız, bunu olarak listelenmeyebilir '**@**' kayıt şirketinizin DNS araçlarında simgesi.</span><span class="sxs-lookup"><span data-stu-id="72768-149">You must also provide the domain or subdomain alias for the CNAME, such as **www** if you want to create an alias for **www.customdomain.com**. If you want to create an alias for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="72768-150">Ardından, uygulamanızın bir kurallı ana bilgisayar adı sağlamalısınız **cloudapp.net** bu durumda etki alanı.</span><span class="sxs-lookup"><span data-stu-id="72768-150">Then, you must provide a canonical host name, which is your application's **cloudapp.net** domain in this case.</span></span>

<span data-ttu-id="72768-151">Örneğin, aşağıdaki CNAME kaydı gelen tüm trafiği iletir **www.contoso.com** için **contoso.cloudapp.net**, dağıtılan uygulamanız özel etki alanı adı:</span><span class="sxs-lookup"><span data-stu-id="72768-151">For example, the following CNAME record forwards all traffic from **www.contoso.com** to **contoso.cloudapp.net**, the custom domain name of your deployed application:</span></span>

| <span data-ttu-id="72768-152">Diğer ad/ana bilgisayar adı/alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="72768-152">Alias/Host name/Subdomain</span></span> | <span data-ttu-id="72768-153">Kurallı etki alanı</span><span class="sxs-lookup"><span data-stu-id="72768-153">Canonical domain</span></span> |
| --- | --- |
| <span data-ttu-id="72768-154">www</span><span class="sxs-lookup"><span data-stu-id="72768-154">www</span></span> |<span data-ttu-id="72768-155">contoso.cloudapp.NET</span><span class="sxs-lookup"><span data-stu-id="72768-155">contoso.cloudapp.net</span></span> |

<span data-ttu-id="72768-156">Bir ziyaretçi, **www.contoso.com** iletmeyi işlemdir son kullanıcıya görünmez şekilde doğru ana bilgisayar (contoso.cloudapp.net) hiçbir zaman görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="72768-156">A visitor of **www.contoso.com** will never see the true host (contoso.cloudapp.net), so the forwarding process is invisible to the end user.</span></span>

> [!NOTE]
> <span data-ttu-id="72768-157">Yukarıdaki örnekte yalnızca trafiğinin uygular **www** alt etki alanı.</span><span class="sxs-lookup"><span data-stu-id="72768-157">The example above only applies to traffic at the **www** subdomain.</span></span> <span data-ttu-id="72768-158">Sahip CNAME kayıtlarına joker karakterler kullanılamaz olduğundan, her etki alanı/alt etki alanı için bir CNAME oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72768-158">Since you cannot use wildcards with CNAME records, you must create one CNAME for each domain/subdomain.</span></span> <span data-ttu-id="72768-159">Alt etki alanları, gelen trafiği gibi doğrudan isteyip istemediğinizi \*. contoso.com cloudapp.net adresinizi yapılandırabilirsiniz bir **yeniden yönlendirme URL'si** veya **İleri URL** DNS ayarlarınız girişi veya oluşturun bir A kaydı.</span><span class="sxs-lookup"><span data-stu-id="72768-159">If you want to direct  traffic from subdomains, such as \*.contoso.com, to your cloudapp.net address, you can configure a **URL Redirect** or **URL Forward** entry in your DNS settings, or create an A record.</span></span>
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a><span data-ttu-id="72768-160">Özel etki alanınız için bir A kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="72768-160">Add an A record for your custom domain</span></span>
<span data-ttu-id="72768-161">Bir A kaydı oluşturmak için öncelikle sanal IP adresine bulut hizmetinizin bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72768-161">To create an A record, you must first find the virtual IP address of your cloud service.</span></span> <span data-ttu-id="72768-162">Ardından yeni bir giriş özel etki alanınız için DNS tablosundaki kayıt şirketiniz tarafından sağlanan araçları kullanarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72768-162">Then add a new entry in the DNS table for your custom domain by using the tools provided by your registrar.</span></span> <span data-ttu-id="72768-163">Her kayıt için bir A kaydı belirtmenin benzer ancak biraz farklı bir yöntem olsa da, kavramlar aynıdır.</span><span class="sxs-lookup"><span data-stu-id="72768-163">Each registrar has a similar but slightly different method of specifying an A record, but the concepts are the same.</span></span>

1. <span data-ttu-id="72768-164">Bulut hizmetinizin IP adresini almak için aşağıdaki yöntemlerden birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="72768-164">Use one of the following methods to get the IP address of your cloud service.</span></span>
   
   * <span data-ttu-id="72768-165">oturum açma [Klasik Azure portalı], bulut hizmetinizi seçin, **Pano**ve ardından bulmak **ortak sanal IP (VIP) adresi** girişi  **Hızlı Bakış** bölümü.</span><span class="sxs-lookup"><span data-stu-id="72768-165">login to the [Azure classic portal], select your cloud service, select **Dashboard**, and then find the **Public Virtual IP (VIP) address** entry in the **quick glance** section.</span></span>
     
       ![Hızlı Bakış bölümüne VIP gösterme][vip]
     
       <span data-ttu-id="72768-167">**VEYA**</span><span class="sxs-lookup"><span data-stu-id="72768-167">**OR**</span></span>  
   * <span data-ttu-id="72768-168">Yükleme ve yapılandırma [Azure Powershell](/powershell/azure/overview)ve ardından aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="72768-168">Install and configure [Azure Powershell](/powershell/azure/overview), and then use the following command:</span></span>
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     <span data-ttu-id="72768-169">Bulut hizmetiniz ile ilişkili birden fazla uç noktası varsa, IP adresini içeren birden fazla satır alırsınız, ancak tüm aynı adres görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="72768-169">If you have multiple endpoints associated with your cloud service, you will receive multiple lines containing the IP address, but all should display the same address.</span></span>
     
     <span data-ttu-id="72768-170">Bir A kaydı oluştururken gerekir olarak IP adresini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="72768-170">Save the IP address, as you will need it when creating an A record.</span></span>
2. <span data-ttu-id="72768-171">DNS kaydedicinizin Web sitesinde oturum açın ve DNS Yönetme sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="72768-171">Log on to your DNS registrar's website and go to the page for managing DNS.</span></span> <span data-ttu-id="72768-172">Bağlantıları veya olarak etiketli sitesinin alanları arayın **etki alanı adı**, **DNS**, veya **adı sunucu yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="72768-172">Look for links or areas of the site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span>
3. <span data-ttu-id="72768-173">Şimdi burada seçin veya bir kaydın girin bulun.</span><span class="sxs-lookup"><span data-stu-id="72768-173">Now find where you can select or enter A record's.</span></span> <span data-ttu-id="72768-174">Aşağı açılır bir kayıt türü seçin veya Gelişmiş Ayarları sayfasına gitmek zorunda kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72768-174">You may have to select the record type from a drop down, or go to an advanced settings page.</span></span>
4. <span data-ttu-id="72768-175">Etki alanı ya da bu A kaydı kullanacağı alt etki alanı girin veya seçin.</span><span class="sxs-lookup"><span data-stu-id="72768-175">Select or enter the domain or subdomain that will use this A record.</span></span> <span data-ttu-id="72768-176">Örneğin, seçin **www** için diğer ad oluşturmak istiyorsanız **www.customdomain.com**. Tüm alt etki alanları için bir joker karakter girişi oluşturmak istiyorsanız, girin '__*__'.</span><span class="sxs-lookup"><span data-stu-id="72768-176">For example, select **www** if you want to create an alias for **www.customdomain.com**. If you want to create a wildcard entry for all subdomains, enter '__*__'.</span></span> <span data-ttu-id="72768-177">Bu gibi tüm alt etki alanlarını kapsar **mail.customdomain.com**, **login.customdomain.com**, ve **www.customdomain.com**.</span><span class="sxs-lookup"><span data-stu-id="72768-177">This will cover all sub-domains such as **mail.customdomain.com**, **login.customdomain.com**, and **www.customdomain.com**.</span></span>
   
    <span data-ttu-id="72768-178">Kök etki alanı için bir A kaydı oluşturmak istiyorsanız, bunu olarak listelenmeyebilir '**@**' kayıt şirketinizin DNS araçlarında simgesi.</span><span class="sxs-lookup"><span data-stu-id="72768-178">If you want to create an A record for the root domain, it may be listed as the '**@**' symbol in your registrar's DNS tools.</span></span>
5. <span data-ttu-id="72768-179">IP adresi bulut hizmetinizin sağlanan alana girin.</span><span class="sxs-lookup"><span data-stu-id="72768-179">Enter the IP address of your cloud service in the provided field.</span></span> <span data-ttu-id="72768-180">Bu, bulut hizmeti dağıtımınızın IP adresiyle bir kayıttaki kullanılan etki alanı girdisi ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="72768-180">This associates the domain entry used in the A record with the IP address of your cloud service deployment.</span></span>

<span data-ttu-id="72768-181">Örneğin, bir kayıt iletir gelen tüm trafiği aşağıdaki **contoso.com** için **137.135.70.239**, dağıtılan uygulamanız IP adresi:</span><span class="sxs-lookup"><span data-stu-id="72768-181">For example, the following A record forwards all traffic from **contoso.com** to **137.135.70.239**, the IP address of your deployed application:</span></span>

| <span data-ttu-id="72768-182">Ana bilgisayar adı/alt etki alanı</span><span class="sxs-lookup"><span data-stu-id="72768-182">Host name/Subdomain</span></span> | <span data-ttu-id="72768-183">IP adresi</span><span class="sxs-lookup"><span data-stu-id="72768-183">IP address</span></span> |
| --- | --- |
| @ |<span data-ttu-id="72768-184">137.135.70.239</span><span class="sxs-lookup"><span data-stu-id="72768-184">137.135.70.239</span></span> |

<span data-ttu-id="72768-185">Bu örnekte, kök etki alanı için bir A kaydı oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="72768-185">This example demonstrates creating an A record for the root domain.</span></span> <span data-ttu-id="72768-186">Tüm alt etki alanları kapsayacak şekilde bir joker karakter girişi oluşturmak isterseniz, girersiniz '__*__' alt etki alanı olarak.</span><span class="sxs-lookup"><span data-stu-id="72768-186">If you wish to create a wildcard entry to cover all subdomains, you would enter '__*__' as the subdomain.</span></span>

> [!WARNING]
> <span data-ttu-id="72768-187">Azure'daki IP adresleri, varsayılan olarak dinamik.</span><span class="sxs-lookup"><span data-stu-id="72768-187">IP addresses in Azure are dynamic by default.</span></span> <span data-ttu-id="72768-188">Kullanmak istersiniz bir [ayrılmış IP adresi](../virtual-network/virtual-networks-reserved-public-ip.md) IP adresiniz değişmeyen emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="72768-188">You will probably want to use a [reserved IP address](../virtual-network/virtual-networks-reserved-public-ip.md) to ensure that your IP address does not change.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="72768-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72768-189">Next steps</span></span>
* [<span data-ttu-id="72768-190">Cloud Services nasıl yönetilir?</span><span class="sxs-lookup"><span data-stu-id="72768-190">How to Manage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="72768-191">CDN İçeriğini Özel Etki Alanı ile Eşleme</span><span class="sxs-lookup"><span data-stu-id="72768-191">How to Map CDN Content to a Custom Domain</span></span>](../cdn/cdn-map-content-to-custom-domain.md)
* <span data-ttu-id="72768-192">[Genel yapılandırma bulut hizmetinizin](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="72768-192">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="72768-193">Bilgi edinmek için nasıl [bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="72768-193">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="72768-194">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="72768-194">Configure [ssl certificates](cloud-services-configure-ssl-certificate.md).</span></span>

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates the subdomain with the storage account]: #create-cname
[Klasik Azure portalı]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png
