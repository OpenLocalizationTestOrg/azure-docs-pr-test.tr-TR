---
title: "Bir web uygulaması için özel DNS kayıtlarını oluşturun | Microsoft Docs"
description: "Azure DNS kullanarak web uygulaması için DNS kayıtlarını özel etki alanı oluşturma"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: b054a41ecd69ee1c802d8403fe4b25128f016e3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="d9568-103">Özel bir etki alanındaki bir web uygulaması için DNS kayıtlarını oluşturun</span><span class="sxs-lookup"><span data-stu-id="d9568-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="d9568-104">Azure DNS, özel bir etki alanı için web uygulamalarınızı barındırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9568-104">You can use Azure DNS to host a custom domain for your web apps.</span></span> <span data-ttu-id="d9568-105">Örneğin, bir Azure web uygulaması oluşturma ve kullanıcılarınızın ya da erişmek istediğiniz contoso.com ya da www.contoso.com bir FQDN kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d9568-105">For example, you are creating an Azure web app and you want your users to access it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="d9568-106">Bunu yapmak için iki kaydı oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d9568-106">To do this, you have to create two records:</span></span>

* <span data-ttu-id="d9568-107">Contoso.com etki alanına işaret eden bir kök "A" kaydı</span><span class="sxs-lookup"><span data-stu-id="d9568-107">A root "A" record pointing to contoso.com</span></span>
* <span data-ttu-id="d9568-108">A kaydına işaret www adı için bir "CNAME" kaydı</span><span class="sxs-lookup"><span data-stu-id="d9568-108">A "CNAME" record for the www name that points to the A record</span></span>

<span data-ttu-id="d9568-109">Unutmayın web uygulama değişikliklerini alttaki IP adresi güncelleştirilmiş Azure'da bir web uygulaması için bir A kaydı oluşturursanız, A kaydını el ile olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9568-109">Keep in mind that if you create an A record for a web app in Azure, the A record must be manually updated if the underlying IP address for the web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d9568-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="d9568-110">Before you begin</span></span>

<span data-ttu-id="d9568-111">Başlamadan önce öncelikle Azure DNS'de bir DNS bölgesi oluşturma ve Azure DNS'ye kayıt içinde bölgeye temsilci.</span><span class="sxs-lookup"><span data-stu-id="d9568-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate the zone in your registrar to Azure DNS.</span></span>

1. <span data-ttu-id="d9568-112">Bir DNS bölgesi oluşturmak için adımları [bir DNS bölgesi oluşturma](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="d9568-112">To create a DNS zone, follow the steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="d9568-113">Azure DNS, DNS temsilci seçmek için adımları [DNS etki alanı temsilcisi](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="d9568-113">To delegate your DNS to Azure DNS, follow the steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="d9568-114">Bölge oluşturma ve Azure DNS'ye temsilci sonra özel etki alanınız için daha sonra kayıt oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9568-114">After creating a zone and delegating it to Azure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="d9568-115">1. Özel etki alanınız için bir A kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d9568-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="d9568-116">Bir A kaydı bir adı IP adresine eşlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d9568-116">An A record is used to map a name to its IP address.</span></span> <span data-ttu-id="d9568-117">Aşağıdaki örnekte biz @ bir IPv4 adresi için bir A kaydı olarak atanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d9568-117">In the following example we will assign @ as an A record to an IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="d9568-118">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-118">Step 1</span></span>

<span data-ttu-id="d9568-119">Bir A kaydını oluşturun ve bir değişkene $rs atayın</span><span class="sxs-lookup"><span data-stu-id="d9568-119">Create an A record and assign to a variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="d9568-120">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-120">Step 2</span></span>

<span data-ttu-id="d9568-121">Önceden oluşturulmuş kayıt kümesine IPv4 değer ekleme "@" atanan $rs değişkenini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="d9568-121">Add the IPv4 value to the previously created record set "@" using the $rs variable assigned.</span></span> <span data-ttu-id="d9568-122">Atanan IPv4 değerini web uygulamanız için IP adresi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d9568-122">The IPv4 value assigned will be the IP address for your web app.</span></span>

<span data-ttu-id="d9568-123">Bir web uygulaması için IP adresini bulmak için adımları [Azure App Service'te özel etki alanı adı yapılandırma](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="d9568-123">To find the IP address for a web app, follow the steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="d9568-124">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-124">Step 3</span></span>

<span data-ttu-id="d9568-125">Kayıt kümesi değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="d9568-125">Commit the changes to the record set.</span></span> <span data-ttu-id="d9568-126">Kullanım `Set-AzureRMDnsRecordSet` değişiklikleri kayıt Azure DNS'ye kümesine karşıya yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="d9568-126">Use `Set-AzureRMDnsRecordSet` to upload the changes to the record set to Azure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="d9568-127">2. Özel etki alanınız için bir CNAME kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d9568-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="d9568-128">Etki alanınız zaten Azure DNS tarafından yönetiliyorsa (bkz [DNS etki alanı temsilcisi](dns-domain-delegation.md), aşağıdakileri kullanabilirsiniz örnek contoso.azurewebsites.net için bir CNAME kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9568-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use the following the example to create a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="d9568-129">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-129">Step 1</span></span>

<span data-ttu-id="d9568-130">PowerShell'i açın ve yeni bir CNAME kayıt kümesi oluşturma ve bir değişkene $rs atayın.</span><span class="sxs-lookup"><span data-stu-id="d9568-130">Open PowerShell and create a new CNAME record set and assign to a variable $rs.</span></span> <span data-ttu-id="d9568-131">Bu örnek DNS bölgesinde "contoso.com" adlı 600 saniye olarak "Canlı zaman" bir kayıt kümesi türüyle CNAME oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9568-131">This example will create a record set type CNAME with a "time to live" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="d9568-132">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="d9568-132">The following example is the response.</span></span>

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="d9568-133">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-133">Step 2</span></span>

<span data-ttu-id="d9568-134">CNAME kayıt kümesi oluşturulduktan sonra web uygulaması'na işaret edecek bir diğer ad değeri oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9568-134">Once the CNAME record set is created, you need to create an alias value which will point to the web app.</span></span>

<span data-ttu-id="d9568-135">Önceden atanmış değişken "$rs" kullanarak web uygulaması contoso.azurewebsites.net için diğer adı oluşturmak için aşağıdaki PowerShell komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9568-135">Using the previously assigned variable "$rs" you can use the PowerShell command below to create the alias for the web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="d9568-136">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="d9568-136">The following example is the response.</span></span>

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="d9568-137">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-137">Step 3</span></span>

<span data-ttu-id="d9568-138">Kullanarak değişiklikleri `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d9568-138">Commit the changes using the `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="d9568-139">Kaydı doğrulamak için aşağıda gösterildiği gibi "www.contoso.com" nslookup kullanarak sorgulayarak doğru bir şekilde oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="d9568-139">You can validate the record was created correctly by querying the "www.contoso.com" using nslookup, as shown below:</span></span>

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="d9568-140">Web uygulamaları için bir "awverify" kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="d9568-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="d9568-141">Web uygulamanız için bir A kaydını kullanmaya karar verirseniz, özel etki alanına sahip olmak için bir doğrulama işlem yapması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d9568-141">If you decide to use an A record for your web app, you must go through a verification process to ensure you own the custom domain.</span></span> <span data-ttu-id="d9568-142">Bu doğrulama adımı "awverify" adlı özel bir CNAME kaydı oluşturarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="d9568-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="d9568-143">Bu bölüm, yalnızca bir kayıtlar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d9568-143">This section applies to A records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="d9568-144">1. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-144">Step 1</span></span>

<span data-ttu-id="d9568-145">"Awverify" kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d9568-145">Create the "awverify" record.</span></span> <span data-ttu-id="d9568-146">Aşağıdaki örnekte, özel etki alanı için sahipliği doğrulamak contoso.com "aweverify" kaydı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="d9568-146">In the example below, we will create the "aweverify" record for contoso.com to verify ownership for the custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="d9568-147">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="d9568-147">The following example is the response.</span></span>

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a><span data-ttu-id="d9568-148">2. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-148">Step 2</span></span>

<span data-ttu-id="d9568-149">"Awverify" kayıt kümesi oluşturulduktan sonra diğer adı ayarlama CNAME kaydı atayın.</span><span class="sxs-lookup"><span data-stu-id="d9568-149">Once the record set "awverify" is created, assign the CNAME record set alias.</span></span> <span data-ttu-id="d9568-150">Aşağıdaki örnekte, biz awverify.contoso.azurewebsites.net için diğer adı ayarlama CNAMe kaydı atar.</span><span class="sxs-lookup"><span data-stu-id="d9568-150">In the example below, we will assign the CNAMe record set alias to awverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="d9568-151">Aşağıdaki örnek, yanıttır.</span><span class="sxs-lookup"><span data-stu-id="d9568-151">The following example is the response.</span></span>

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a><span data-ttu-id="d9568-152">3. Adım</span><span class="sxs-lookup"><span data-stu-id="d9568-152">Step 3</span></span>

<span data-ttu-id="d9568-153">Kullanarak değişiklikleri `Set-AzureRMDnsRecordSet cmdlet`komutta gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="d9568-153">Commit the changes using the `Set-AzureRMDnsRecordSet cmdlet`, as shown in the command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="d9568-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9568-154">Next steps</span></span>

<span data-ttu-id="d9568-155">Adımları [uygulama hizmeti için bir özel etki alanı adı yapılandırma](../app-service-web/web-sites-custom-domain-name.md) özel bir etki alanı kullanmak için web Uygulamanızı yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="d9568-155">Follow the steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) to configure your web app to use a custom domain.</span></span>
