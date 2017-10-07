---
title: "bir web uygulaması için özel DNS kayıtlarını aaaCreate | Microsoft Docs"
description: "Azure DNS kullanarak web uygulaması için toocreate özel etki alanı DNS kayıtları nasıl."
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
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a><span data-ttu-id="5b979-103">Özel bir etki alanındaki bir web uygulaması için DNS kayıtlarını oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b979-103">Create DNS records for a web app in a custom domain</span></span>

<span data-ttu-id="5b979-104">Azure DNS toohost özel bir etki alanı, web uygulamaları için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b979-104">You can use Azure DNS toohost a custom domain for your web apps.</span></span> <span data-ttu-id="5b979-105">Örneğin, bir Azure web uygulaması oluşturma ve kullanıcılara tooaccess istediğiniz ya da tarafından contoso.com ya da www.contoso.com bir FQDN kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5b979-105">For example, you are creating an Azure web app and you want your users tooaccess it by either using contoso.com, or www.contoso.com as an FQDN.</span></span>

<span data-ttu-id="5b979-106">toodo bunu toocreate iki kayıtları içerir:</span><span class="sxs-lookup"><span data-stu-id="5b979-106">toodo this, you have toocreate two records:</span></span>

* <span data-ttu-id="5b979-107">Bir kök "A" kaydı işaret toocontoso.com</span><span class="sxs-lookup"><span data-stu-id="5b979-107">A root "A" record pointing toocontoso.com</span></span>
* <span data-ttu-id="5b979-108">Bir "CNAME" toohello işaret hello www adı için bir kayıt kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5b979-108">A "CNAME" record for hello www name that points toohello A record</span></span>

<span data-ttu-id="5b979-109">Azure üzerinde bir web uygulaması için bir A kaydı oluşturursanız, bir kayıt, el ile güncelleştirilmelidir hello hello web uygulama değişikliklerini için temel alınan IP adresi hello aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5b979-109">Keep in mind that if you create an A record for a web app in Azure, hello A record must be manually updated if hello underlying IP address for hello web app changes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5b979-110">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5b979-110">Before you begin</span></span>

<span data-ttu-id="5b979-111">Başlamadan önce öncelikle Azure DNS'de bir DNS bölgesi oluşturma ve hello bölgesi, kayıt tooAzure DNS temsilci.</span><span class="sxs-lookup"><span data-stu-id="5b979-111">Before you begin, you must first create a DNS zone in Azure DNS, and delegate hello zone in your registrar tooAzure DNS.</span></span>

1. <span data-ttu-id="5b979-112">toocreate bir DNS bölgesi içinde hello adımları izleyin [bir DNS bölgesi oluşturma](dns-getstarted-create-dnszone.md).</span><span class="sxs-lookup"><span data-stu-id="5b979-112">toocreate a DNS zone, follow hello steps in [Create a DNS zone](dns-getstarted-create-dnszone.md).</span></span>
2. <span data-ttu-id="5b979-113">toodelegate, DNS, DNS tooAzure izleyin hello adımlarda [DNS etki alanı temsilcisi](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="5b979-113">toodelegate your DNS tooAzure DNS, follow hello steps in [DNS domain delegation](dns-domain-delegation.md).</span></span>

<span data-ttu-id="5b979-114">Bölge oluşturma ve tooAzure DNS temsilci sonra özel etki alanınız için daha sonra kayıt oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b979-114">After creating a zone and delegating it tooAzure DNS, you can then create records for your custom domain.</span></span>

## <a name="1-create-an-a-record-for-your-custom-domain"></a><span data-ttu-id="5b979-115">1. Özel etki alanınız için bir A kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b979-115">1. Create an A record for your custom domain</span></span>

<span data-ttu-id="5b979-116">Bir A kaydı kullanılan toomap adı tooits IP adresi değil.</span><span class="sxs-lookup"><span data-stu-id="5b979-116">An A record is used toomap a name tooits IP address.</span></span> <span data-ttu-id="5b979-117">Aşağıdaki örnek hello biz @ bir A kaydı tooan IPv4 adresi atanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="5b979-117">In hello following example we will assign @ as an A record tooan IPv4 address:</span></span>

### <a name="step-1"></a><span data-ttu-id="5b979-118">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-118">Step 1</span></span>

<span data-ttu-id="5b979-119">Bir A kaydını oluşturun ve değişken $rs tooa atayın</span><span class="sxs-lookup"><span data-stu-id="5b979-119">Create an A record and assign tooa variable $rs</span></span>

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a><span data-ttu-id="5b979-120">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-120">Step 2</span></span>

<span data-ttu-id="5b979-121">Başlangıç IPv4 değeri daha önce oluşturduğunuz toohello kayıt kümesi Ekle "@" atanan hello $rs değişkenini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5b979-121">Add hello IPv4 value toohello previously created record set "@" using hello $rs variable assigned.</span></span> <span data-ttu-id="5b979-122">Merhaba atanan IPv4 değerini web uygulamanız için başlangıç IP adresi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5b979-122">hello IPv4 value assigned will be hello IP address for your web app.</span></span>

<span data-ttu-id="5b979-123">bir web uygulaması için toofind başlangıç IP adresi hello adımları izleyin [Azure App Service'te özel etki alanı adı yapılandırma](../app-service-web/app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="5b979-123">toofind hello IP address for a web app, follow hello steps in [Configure a custom domain name in Azure App Service](../app-service-web/app-service-web-tutorial-custom-domain.md).</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a><span data-ttu-id="5b979-124">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-124">Step 3</span></span>

<span data-ttu-id="5b979-125">Merhaba değişiklikleri toohello kayıt kümesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5b979-125">Commit hello changes toohello record set.</span></span> <span data-ttu-id="5b979-126">Kullanım `Set-AzureRMDnsRecordSet` tooupload hello toohello kayıt kümesi tooAzure DNS değiştirir:</span><span class="sxs-lookup"><span data-stu-id="5b979-126">Use `Set-AzureRMDnsRecordSet` tooupload hello changes toohello record set tooAzure DNS:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a><span data-ttu-id="5b979-127">2. Özel etki alanınız için bir CNAME kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b979-127">2. Create a CNAME record for your custom domain</span></span>

<span data-ttu-id="5b979-128">Etki alanınız zaten Azure DNS tarafından yönetiliyorsa (bkz [DNS etki alanı temsilcisi](dns-domain-delegation.md), hello örnek toocreate contoso.azurewebsites.net için bir CNAME kaydı aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b979-128">If your domain is already managed by Azure DNS (see [DNS domain delegation](dns-domain-delegation.md), you can use hello following hello example toocreate a CNAME record for contoso.azurewebsites.net.</span></span>

### <a name="step-1"></a><span data-ttu-id="5b979-129">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-129">Step 1</span></span>

<span data-ttu-id="5b979-130">PowerShell'i açın ve yeni bir CNAME kaydı kümesi oluşturun ve değişken $rs tooa atayın.</span><span class="sxs-lookup"><span data-stu-id="5b979-130">Open PowerShell and create a new CNAME record set and assign tooa variable $rs.</span></span> <span data-ttu-id="5b979-131">Bu örnekte, "" contoso.com"adlı bir süresi olan toolive" DNS bölgesinde 600 saniye kayıt kümesi türü CNAME oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5b979-131">This example will create a record set type CNAME with a "time toolive" of 600 seconds in DNS zone named "contoso.com".</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="5b979-132">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="5b979-132">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="5b979-133">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-133">Step 2</span></span>

<span data-ttu-id="5b979-134">Merhaba CNAME kayıt kümesi oluşturulduktan sonra toohello web uygulaması işaret edecek bir diğer ad değeri toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b979-134">Once hello CNAME record set is created, you need toocreate an alias value which will point toohello web app.</span></span>

<span data-ttu-id="5b979-135">Daha önce atanan değişkeni "$rs" Merhaba kullanarak hello web uygulama contoso.azurewebsites.net için hello toocreate hello diğer aşağıdaki PowerShell komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b979-135">Using hello previously assigned variable "$rs" you can use hello PowerShell command below toocreate hello alias for hello web app contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

<span data-ttu-id="5b979-136">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="5b979-136">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="5b979-137">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-137">Step 3</span></span>

<span data-ttu-id="5b979-138">Hello kullanarak hello değişiklikleri `Set-AzureRMDnsRecordSet` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5b979-138">Commit hello changes using hello `Set-AzureRMDnsRecordSet` cmdlet:</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

<span data-ttu-id="5b979-139">Doğrulamak için hello kayıt oluşturulduğu doğru aşağıda gösterildiği gibi "nslookup kullanarak hello www.contoso.com" sorgulayarak:</span><span class="sxs-lookup"><span data-stu-id="5b979-139">You can validate hello record was created correctly by querying hello "www.contoso.com" using nslookup, as shown below:</span></span>

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

## <a name="create-an-awverify-record-for-web-apps"></a><span data-ttu-id="5b979-140">Web uygulamaları için bir "awverify" kaydı oluşturun</span><span class="sxs-lookup"><span data-stu-id="5b979-140">Create an "awverify" record for web apps</span></span>

<span data-ttu-id="5b979-141">Web uygulamanız için bir A kaydı toouse karar verirseniz, kendi hello özel etki alanı doğrulama işlemi tooensure gitmelidir.</span><span class="sxs-lookup"><span data-stu-id="5b979-141">If you decide toouse an A record for your web app, you must go through a verification process tooensure you own hello custom domain.</span></span> <span data-ttu-id="5b979-142">Bu doğrulama adımı "awverify" adlı özel bir CNAME kaydı oluşturarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="5b979-142">This verification step is done by creating a special CNAME record named "awverify".</span></span> <span data-ttu-id="5b979-143">Bu bölüm, yalnızca tooA kayıtlar geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5b979-143">This section applies tooA records only.</span></span>

### <a name="step-1"></a><span data-ttu-id="5b979-144">1. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-144">Step 1</span></span>

<span data-ttu-id="5b979-145">Merhaba "awverify" kaydı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5b979-145">Create hello "awverify" record.</span></span> <span data-ttu-id="5b979-146">Merhaba aşağıdaki örnekte, contoso.com tooverify sahipliği hello özel etki alanı için hello "aweverify" kaydı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="5b979-146">In hello example below, we will create hello "aweverify" record for contoso.com tooverify ownership for hello custom domain.</span></span>

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

<span data-ttu-id="5b979-147">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="5b979-147">hello following example is hello response.</span></span>

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

### <a name="step-2"></a><span data-ttu-id="5b979-148">2. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-148">Step 2</span></span>

<span data-ttu-id="5b979-149">Merhaba kayıt kümesi "awverify" oluşturulduktan sonra diğer adı ayarlama hello CNAME kaydı atayın.</span><span class="sxs-lookup"><span data-stu-id="5b979-149">Once hello record set "awverify" is created, assign hello CNAME record set alias.</span></span> <span data-ttu-id="5b979-150">Merhaba aşağıdaki örnekte, biz hello CNAMe kayıt kümesi diğer tooawverify.contoso.azurewebsites.net atar.</span><span class="sxs-lookup"><span data-stu-id="5b979-150">In hello example below, we will assign hello CNAMe record set alias tooawverify.contoso.azurewebsites.net.</span></span>

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

<span data-ttu-id="5b979-151">Aşağıdaki örnek hello hello yanıt ' dir.</span><span class="sxs-lookup"><span data-stu-id="5b979-151">hello following example is hello response.</span></span>

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

### <a name="step-3"></a><span data-ttu-id="5b979-152">3. Adım</span><span class="sxs-lookup"><span data-stu-id="5b979-152">Step 3</span></span>

<span data-ttu-id="5b979-153">Hello kullanarak hello değişiklikleri `Set-AzureRMDnsRecordSet cmdlet`hello komutta aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="5b979-153">Commit hello changes using hello `Set-AzureRMDnsRecordSet cmdlet`, as shown in hello command below.</span></span>

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a><span data-ttu-id="5b979-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b979-154">Next steps</span></span>

<span data-ttu-id="5b979-155">Merhaba adımları [uygulama hizmeti için bir özel etki alanı adı yapılandırma](../app-service-web/web-sites-custom-domain-name.md) tooconfigure web uygulama toouse özel bir etki alanı.</span><span class="sxs-lookup"><span data-stu-id="5b979-155">Follow hello steps in [Configuring a custom domain name for App Service](../app-service-web/web-sites-custom-domain-name.md) tooconfigure your web app toouse a custom domain.</span></span>
