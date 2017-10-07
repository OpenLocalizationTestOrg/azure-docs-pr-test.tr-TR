---
title: "aaaHow toouse hello Hizmet Yönetimi API'si (Python) - özellik Kılavuzu"
description: "Nasıl tooprogrammatically ortak hizmet yönetim görevleri gerçekleştirebilir Python öğrenin."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="78f39-103">Nasıl toouse python'dan Hizmet Yönetimi</span><span class="sxs-lookup"><span data-stu-id="78f39-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="78f39-104">Bu kılavuz size nasıl tooprogrammatically ortak hizmet yönetim görevleri gerçekleştirebilir Python gösterir.</span><span class="sxs-lookup"><span data-stu-id="78f39-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="78f39-105">Merhaba **ServiceManagementService** hello sınıfında [Python için Azure SDK](https://github.com/Azure/azure-sdk-for-python) programlı erişim toomuch hello kullanılabilirhelloservisyönetimiyleilgiliişlevselliğidestekler[Klasik azure portalı] [ management-portal] (gibi **oluşturma, güncelleştirme ve bulut Hizmetleri, dağıtımları, Veri Yönetimi Hizmetleri ve sanal makineleri silme**).</span><span class="sxs-lookup"><span data-stu-id="78f39-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="78f39-106">Bu işlev programlı erişim tooservice yönetim ihtiyaç duyan uygulamalar oluşturmada faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="78f39-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="78f39-107"><a name="WhatIs"></a>Hizmet yönetimi nedir</span><span class="sxs-lookup"><span data-stu-id="78f39-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="78f39-108">Merhaba Hizmet Yönetimi API'si sağlar hello hello kullanılabilen hizmet yönetim işlevlerinin programlı erişim toomuch [Klasik Azure portalı][management-portal].</span><span class="sxs-lookup"><span data-stu-id="78f39-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="78f39-109">Merhaba Python için Azure SDK toomanage sağlayan bulut Hizmetleri ve depolama hesapları.</span><span class="sxs-lookup"><span data-stu-id="78f39-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="78f39-110">toouse hello Hizmet Yönetimi API'si, gereksinim duyduğunuz çok[bir Azure hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="78f39-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="78f39-111"><a name="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="78f39-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="78f39-112">Merhaba Python için Azure SDK sarmalar hello [Azure Hizmet Yönetimi API'si][svc-mgmt-rest-api], REST API olduğu.</span><span class="sxs-lookup"><span data-stu-id="78f39-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="78f39-113">Tüm API işlemleri SSL üzerinden gerçekleştirilir ve X.509 v3 sertifikaları kullanılarak karşılıklı kimlik doğrulaması yapılır.</span><span class="sxs-lookup"><span data-stu-id="78f39-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="78f39-114">Merhaba Yönetim Hizmeti gelen içinde Azure veya hello Internet üzerinden doğrudan bir HTTPS isteği göndermek ve bir HTTPS yanıt herhangi bir uygulamadan çalışan bir hizmete erişebilir.</span><span class="sxs-lookup"><span data-stu-id="78f39-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="78f39-115"><a name="Installation"></a>Yükleme</span><span class="sxs-lookup"><span data-stu-id="78f39-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="78f39-116">Bu makalede açıklanan tüm hello özellikleri hello kullanılabilir `azure-servicemanagement-legacy` paketi olarak PIP kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78f39-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="78f39-117">Bu makalede (örneğin, yeni tooPython varsa) yükleme hakkında daha fazla bilgi için bkz: [yükleme Python ve hello Azure SDK'sı](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="78f39-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="78f39-118"><a name="Connect"></a>Nasıl yapılır: tooservice Yönetimi bağlama</span><span class="sxs-lookup"><span data-stu-id="78f39-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="78f39-119">tooconnect toohello Hizmet Yönetimi uç nokta, Azure abonelik Kimliğinizi ve geçerli bir yönetim sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="78f39-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="78f39-120">Abonelik Kimliğinizi hello aracılığıyla elde edebilirsiniz [Klasik Azure portalı][management-portal].</span><span class="sxs-lookup"><span data-stu-id="78f39-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="78f39-121">Bu olası toouse sertifikaları Windows üzerinde çalışan OpenSSL ile oluşturulan sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="78f39-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="78f39-122">Python 2.7.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="78f39-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="78f39-123">.Pfx sertifikaları büyük ihtimalle hello gelecekte kaldırılacaktır desteği itibaren .pfx, yerine kullanıcıların toouse OpenSSL öneririz.</span><span class="sxs-lookup"><span data-stu-id="78f39-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="78f39-124">Yönetim sertifikaları Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="78f39-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="78f39-125">Kullanabileceğiniz [OpenSSL](http://www.openssl.org/) toocreate yönetim sertifikası.</span><span class="sxs-lookup"><span data-stu-id="78f39-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="78f39-126">Gerçekte toocreate iki sertifika, hello sunucu için bir tane gerekir (bir `.cer` dosyası) hello istemci için bir tane (bir `.pem` dosyası).</span><span class="sxs-lookup"><span data-stu-id="78f39-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="78f39-127">toocreate hello `.pem` dosya, yürütün:</span><span class="sxs-lookup"><span data-stu-id="78f39-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="78f39-128">toocreate hello `.cer` sertifika, yürütün:</span><span class="sxs-lookup"><span data-stu-id="78f39-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="78f39-129">Azure sertifikaları hakkında daha fazla bilgi için bkz: [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="78f39-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="78f39-130">OpenSSL parametreler tam bir açıklaması için hello belgelerine bakın [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="78f39-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="78f39-131">Bu dosyalar oluşturduktan sonra tooupload hello gereksinim `.cer` tooAzure hello "Karşıya Yükle" eylemin hello hello "Ayarlar" sekmesini aracılığıyla dosya [Klasik Azure portalı][management-portal], ve toomake Not gerekiyor Merhaba kaydettiğiniz `.pem` dosya.</span><span class="sxs-lookup"><span data-stu-id="78f39-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="78f39-132">Abonelik Kimliğinizi aldıktan sonra bir sertifika oluşturulur ve hello karşıya `.cer` dosya tooAzure hello abonelik kimliği ve hello yolu toohello geçirerek toohello Azure yönetim uç noktasına bağlanabilir `.pem` çok dosya**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="78f39-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="78f39-133">Örneğin, önceki hello içinde `sms` olan bir **ServiceManagementService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78f39-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="78f39-134">Merhaba **ServiceManagementService** sınıfı hello kullanılan birincil sınıf toomanage Azure hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="78f39-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="78f39-135">Yönetim sertifikaları Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="78f39-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="78f39-136">Otomatik imzalı yönetim sertifikası, makine kullanarak oluşturabileceğiniz `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="78f39-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="78f39-137">Açık bir **Visual Studio komut istemi** olarak bir **yönetici** ve aşağıdaki komut, değiştirme hello *AzureCertificate* gibi hello sertifika adına sahip toouse.</span><span class="sxs-lookup"><span data-stu-id="78f39-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="78f39-138">Merhaba komut oluşturur hello `.cer` dosya ve hello yükler **kişisel** sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="78f39-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="78f39-139">Daha fazla bilgi için bkz: [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="78f39-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="78f39-140">Merhaba sertifika oluşturduktan sonra tooupload hello gereksinim `.cer` tooAzure hello "Karşıya Yükle" eylemin hello hello "Ayarlar" sekmesini aracılığıyla dosya [Klasik Azure portalı][management-portal].</span><span class="sxs-lookup"><span data-stu-id="78f39-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="78f39-141">Abonelik Kimliğinizi aldıktan sonra bir sertifika oluşturulur ve hello karşıya `.cer` dosya tooAzure hello abonelik kimliği ve hello sertifika hello konumunu, geçirerektoohelloAzureyönetimuçnoktasınabağlanabilir**Kişisel** çok sertifika deposunu**ServiceManagementService** (yeniden Değiştir *AzureCertificate* sertifikanızın hello adıyla):</span><span class="sxs-lookup"><span data-stu-id="78f39-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="78f39-142">Örneğin, önceki hello içinde `sms` olan bir **ServiceManagementService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="78f39-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="78f39-143">Merhaba **ServiceManagementService** sınıfı hello kullanılan birincil sınıf toomanage Azure hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="78f39-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="78f39-144"><a name="ListAvailableLocations"></a>Nasıl yapılır: kullanılabilir konumlarını listeleyin</span><span class="sxs-lookup"><span data-stu-id="78f39-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="78f39-145">hizmetlerini barındırmak için kullanılabilir toolist hello konumlarını kullanın hello **listesi\_konumları** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="78f39-146">Bir bulut hizmeti veya depolama hizmeti oluşturduğunuzda tooprovide geçerli bir konum gerekir.</span><span class="sxs-lookup"><span data-stu-id="78f39-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="78f39-147">Merhaba **listesi\_konumları** yöntem her zaman güncel bir hello şu anda kullanılabilir konumların listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="78f39-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="78f39-148">Bu makalenin yazıldığı sırada hello kullanılabilir konumlarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="78f39-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="78f39-149">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="78f39-149">West Europe</span></span>
* <span data-ttu-id="78f39-150">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="78f39-150">North Europe</span></span>
* <span data-ttu-id="78f39-151">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="78f39-151">Southeast Asia</span></span>
* <span data-ttu-id="78f39-152">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="78f39-152">East Asia</span></span>
* <span data-ttu-id="78f39-153">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="78f39-153">Central US</span></span>
* <span data-ttu-id="78f39-154">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="78f39-154">North Central US</span></span>
* <span data-ttu-id="78f39-155">Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="78f39-155">South Central US</span></span>
* <span data-ttu-id="78f39-156">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="78f39-156">West US</span></span>
* <span data-ttu-id="78f39-157">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="78f39-157">East US</span></span>
* <span data-ttu-id="78f39-158">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="78f39-158">Japan East</span></span>
* <span data-ttu-id="78f39-159">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="78f39-159">Japan West</span></span>
* <span data-ttu-id="78f39-160">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="78f39-160">Brazil South</span></span>
* <span data-ttu-id="78f39-161">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="78f39-161">Australia East</span></span>
* <span data-ttu-id="78f39-162">Avustralya Güneydoğu</span><span class="sxs-lookup"><span data-stu-id="78f39-162">Australia Southeast</span></span>

## <span data-ttu-id="78f39-163"><a name="CreateCloudService"></a>Nasıl yapılır: bir bulut hizmeti oluştur</span><span class="sxs-lookup"><span data-stu-id="78f39-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="78f39-164">Bir uygulama oluşturduğunuzda ve Azure'da çalıştırmak, hello kod ve yapılandırma birlikte Azure adlandırılır [bulut hizmeti] [ cloud service] (olarak bilinen bir *barındırılan hizmetin* içinde daha önce Azure serbest bırakır).</span><span class="sxs-lookup"><span data-stu-id="78f39-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="78f39-165">Merhaba **oluşturma\_barındırılan\_hizmet** yöntemi verir toocreate yeni bir barındırılan hizmet (hangi Azure içinde benzersiz olması gerekir) barındırılan hizmet adını sağlayarak bir etiket (otomatik olarak kodlanmış toobase64), bir Açıklama ve bir konum.</span><span class="sxs-lookup"><span data-stu-id="78f39-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="78f39-166">Tüm hello barındırılan hizmetler hello aboneliğinizle için listeleyebilirsiniz **listesi\_barındırılan\_Hizmetleri** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="78f39-167">Belirli bir barındırılan hizmet tooget öğrenmek istiyorsanız, bunu hello barındırılan hizmet adı toohello geçirerek yapabilirsiniz **almak\_barındırılan\_hizmet\_özellikleri** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="78f39-168">Bir bulut hizmeti oluşturduktan sonra kodu toohello hizmetiniz hello ile dağıtabilirsiniz **oluşturma\_dağıtım** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="78f39-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="78f39-169"><a name="DeleteCloudService"></a>Nasıl yapılır: bir bulut hizmetini silin</span><span class="sxs-lookup"><span data-stu-id="78f39-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="78f39-170">Merhaba hizmet adı toohello geçirerek bir bulut hizmeti silebilirsiniz **silmek\_barındırılan\_hizmet** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="78f39-171">Bir hizmet silmeden önce hello hizmeti için tüm dağıtımlar silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="78f39-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="78f39-172">(Bkz [nasıl yapılır: bir dağıtımı silin](#DeleteDeployment) Ayrıntılar için.)</span><span class="sxs-lookup"><span data-stu-id="78f39-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="78f39-173"><a name="DeleteDeployment"></a>Nasıl yapılır: bir dağıtımı silin</span><span class="sxs-lookup"><span data-stu-id="78f39-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="78f39-174">toodelete bir dağıtımı kullanmak hello **silmek\_dağıtım** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="78f39-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="78f39-175">Merhaba aşağıdaki örnek bir dağıtım toodelete nasıl adlı gösterir `v1`.</span><span class="sxs-lookup"><span data-stu-id="78f39-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="78f39-176"><a name="CreateStorageService"></a>Nasıl yapılır: bir depolama birimi hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="78f39-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="78f39-177">A [depolama birimi hizmeti](../storage/common/storage-create-storage-account.md) , tooAzure erişmenizi [BLOB'lar](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabloları](../cosmos-db/table-storage-how-to-use-python.md), ve [sıraları](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="78f39-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="78f39-178">bir depolama birimi hizmeti toocreate hello hizmeti (3 ila 24 küçük harf karakter ve Azure içinde benzersiz) için bir ad, açıklama, bir etiket (yukarı too100 karakter, otomatik olarak kodlanmış toobase64) ve bir konum gerekir.</span><span class="sxs-lookup"><span data-stu-id="78f39-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="78f39-179">Aşağıdaki örnek hello nasıl toocreate bir depolama hizmeti bir konum belirterek gösterir.</span><span class="sxs-lookup"><span data-stu-id="78f39-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="78f39-180">Örnek önceki hello hello hello durumu Not **oluşturma\_depolama\_hesap** işlemi tarafından döndürülen hello sonuç geçirerek alınabilir **oluşturma\_depolama \_hesap** toohello **almak\_işlemi\_durum** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="78f39-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="78f39-181">Depolama hesaplarınızı ve bunların özelliklerini hello ile listeleyebilirsiniz **listesi\_depolama\_hesapları** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="78f39-182"><a name="DeleteStorageService"></a>Nasıl yapılır: bir depolama birimi hizmeti Sil</span><span class="sxs-lookup"><span data-stu-id="78f39-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="78f39-183">Merhaba depolama hizmeti adı toohello geçirerek bir depolama birimi hizmeti silebilirsiniz **silmek\_depolama\_hesap** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="78f39-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="78f39-184">Bir depolama birimi hizmeti silme (BLOB'lar, tablolar ve Kuyruklar) hello hizmetinde depolanan tüm verileri siler.</span><span class="sxs-lookup"><span data-stu-id="78f39-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="78f39-185"><a name="ListOperatingSystems"></a>Nasıl yapılır: listesinde kullanılabilir işletim sistemleri</span><span class="sxs-lookup"><span data-stu-id="78f39-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="78f39-186">hizmetlerini barındırmak için kullanılabilir toolist hello işletim sistemleri kullanan hello **listesi\_işletim\_sistemleri** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="78f39-187">Alternatif olarak, hello kullanabilirsiniz **listesi\_işletim\_sistem\_aileleri** hello işletim sistemi ailesi tarafından grupları yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="78f39-188"><a name="CreateVMImage"></a>Nasıl yapılır: bir işletim sistemi görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="78f39-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="78f39-189">tooadd bir işletim sistemi görüntüsü toohello görüntü deposuna kullanmak hello **ekleme\_os\_görüntü** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

<span data-ttu-id="78f39-190">kullanılabilir toolist hello işletim sistemi görüntüleri kullanmak hello **listesi\_os\_görüntüleri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="78f39-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="78f39-191">Tüm platform görüntüleri ve kullanıcı görüntüleri içerir:</span><span class="sxs-lookup"><span data-stu-id="78f39-191">It includes all platform images and user images:</span></span>

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <span data-ttu-id="78f39-192"><a name="DeleteVMImage"></a>Nasıl yapılır: bir işletim sistemi görüntüsünü silme</span><span class="sxs-lookup"><span data-stu-id="78f39-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="78f39-193">toodelete kullanıcı görüntüsü kullanmak hello **silmek\_os\_görüntü** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="78f39-194"><a name="CreateVM"></a>Nasıl yapılır: bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="78f39-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="78f39-195">bir sanal makine toocreate, ilk ihtiyacınız toocreate bir [bulut hizmeti](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="78f39-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="78f39-196">Hello kullanarak hello sanal makine dağıtımı oluşturmak **oluşturma\_sanal\_makine\_dağıtım** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <span data-ttu-id="78f39-197"><a name="DeleteVM"></a>Nasıl yapılır: bir sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="78f39-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="78f39-198">bir sanal makine toodelete silmeniz hello kullanarak hello dağıtım **silmek\_dağıtım** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="78f39-199">Merhaba bulut hizmeti sonra silinebilir hello kullanarak **silmek\_barındırılan\_hizmet** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="78f39-200">Nasıl yapılır: bir sanal makine yakalanan görüntüden sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="78f39-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="78f39-201">toocapture bir VM görüntüsü, ilk çağırmanız hello **yakalama\_vm\_görüntü** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="78f39-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

<span data-ttu-id="78f39-202">İleri toomake hello görüntüsü başarıyla yakalandı, hello kullan emin **listesi\_vm\_görüntüleri** API'sini ve görüntünüzü hello sonuçlarında görüntülenen emin olun:</span><span class="sxs-lookup"><span data-stu-id="78f39-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="78f39-203">toofinally hello yakalanan görüntüyü kullanarak hello sanal makine oluşturun, hello kullan **oluşturma\_sanal\_makine\_dağıtım** önce ancak bu kez hello vm_image_name yerine geçirirken yöntemi</span><span class="sxs-lookup"><span data-stu-id="78f39-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

<span data-ttu-id="78f39-204">toolearn toocapture bir Linux sanal makine nasıl görürüm hakkında daha fazla bilgi [nasıl tooCapture Linux sanal makine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="78f39-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="78f39-205">toolearn toocapture bir Windows sanal makine nasıl görürüm hakkında daha fazla bilgi [nasıl tooCapture Windows sanal makine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="78f39-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="78f39-206"><a name="What's Next"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78f39-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="78f39-207">Hizmet Yönetimi hello temellerini öğrendiğinize göre hello erişebilirsiniz [hello Azure Python SDK'sı için tam API başvuru belgeleri](http://azure-sdk-for-python.readthedocs.org/) ve gerçekleştirmek karmaşık görevleri kolayca python uygulamanızı toomanage.</span><span class="sxs-lookup"><span data-stu-id="78f39-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="78f39-208">Daha fazla bilgi için bkz: Merhaba [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="78f39-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
