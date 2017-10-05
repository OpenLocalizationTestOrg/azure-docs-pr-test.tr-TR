---
title: "Hizmet Yönetimi API (Python) - özellik kılavuzu kullanma"
description: "Program aracılığıyla Python ortak hizmet yönetim görevlerini gerçekleştirmek öğrenin."
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
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="a75ed-103">Hizmet Yönetimi python'dan kullanma</span><span class="sxs-lookup"><span data-stu-id="a75ed-103">How to use Service Management from Python</span></span>
<span data-ttu-id="a75ed-104">Bu kılavuz program aracılığıyla Python ortak hizmet yönetim görevlerini gerçekleştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="a75ed-105">**ServiceManagementService** sınıfını [Python için Azure SDK](https://github.com/Azure/azure-sdk-for-python) programlı erişim kullanılabilir servis yönetimiyle ilgili işlevlerinin çoğunu destekler [Azure Klasik portal] [ management-portal] (gibi **oluşturma, güncelleştirme ve bulut Hizmetleri, dağıtımları, Veri Yönetimi Hizmetleri ve sanal makineleri silme**).</span><span class="sxs-lookup"><span data-stu-id="a75ed-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="a75ed-106">Bu işlev hizmet yönetimi için programlı erişim ihtiyaç duyan uygulamalar oluşturmada faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="a75ed-107"><a name="WhatIs"></a>Hizmet yönetimi nedir</span><span class="sxs-lookup"><span data-stu-id="a75ed-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="a75ed-108">Hizmet Yönetimi API aracılığıyla kullanılabilir hizmet yönetim işlevlerinin çoğunu için programlı erişim sağlayan [Klasik Azure portalı][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a75ed-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="a75ed-109">Python için Azure SDK'sı, bulut Hizmetleri ve depolama hesapları yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a75ed-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="a75ed-110">Hizmet Yönetimi API'sini kullanmak için yapmanız [bir Azure hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a75ed-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="a75ed-111"><a name="Concepts"></a>Kavramları</span><span class="sxs-lookup"><span data-stu-id="a75ed-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="a75ed-112">Python için Azure SDK'sı sarmalar [Azure Hizmet Yönetimi API'si][svc-mgmt-rest-api], REST API olduğu.</span><span class="sxs-lookup"><span data-stu-id="a75ed-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="a75ed-113">Tüm API işlemleri SSL üzerinden gerçekleştirilir ve X.509 v3 sertifikaları kullanılarak karşılıklı kimlik doğrulaması yapılır.</span><span class="sxs-lookup"><span data-stu-id="a75ed-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="a75ed-114">Yönetim hizmetine Azure'da çalışan bir hizmetin içinden veya doğrudan İnternet üzerinden, HTTPS isteği gönderebilen ve HTTPS yanıtı alabilen herhangi bir uygulamadan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="a75ed-115"><a name="Installation"></a>Yükleme</span><span class="sxs-lookup"><span data-stu-id="a75ed-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="a75ed-116">Bu makalede açıklanan tüm özellikler mevcuttur `azure-servicemanagement-legacy` paketi olarak PIP kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a75ed-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="a75ed-117">Bu makalede (örneğin, Python için yeni olan) yükleme hakkında daha fazla bilgi için bkz: [yükleme Python ve Azure SDK'sı](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="a75ed-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="a75ed-118"><a name="Connect"></a>Nasıl yapılır: Hizmet Yönetimi için Bağlan</span><span class="sxs-lookup"><span data-stu-id="a75ed-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="a75ed-119">Hizmet Yönetimi uç noktasına bağlanmak için Azure abonelik Kimliğinizi ve geçerli bir yönetim sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="a75ed-120">Abonelik Kimliğinizi aracılığıyla elde edebilirsiniz [Klasik Azure portalı][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a75ed-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="a75ed-121">Artık Windows üzerinde çalışan OpenSSL ile oluşturulan sertifikaları kullanmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="a75ed-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="a75ed-122">Python 2.7.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="a75ed-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="a75ed-123">Kullanıcıların sertifikalar büyük ihtimalle gelecekte kaldırılacaktır .pfx desteği itibaren .pfx yerine OpenSSL kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="a75ed-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="a75ed-124">Yönetim sertifikaları Windows/Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="a75ed-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="a75ed-125">Kullanabileceğiniz [OpenSSL](http://www.openssl.org/) yönetim sertifikası oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a75ed-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="a75ed-126">Aslında iki sertifika, sunucu için bir tane oluşturmanız gerekir (bir `.cer` dosyası) ve bir istemci için (bir `.pem` dosyası).</span><span class="sxs-lookup"><span data-stu-id="a75ed-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="a75ed-127">Oluşturmak için `.pem` dosya, yürütün:</span><span class="sxs-lookup"><span data-stu-id="a75ed-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="a75ed-128">Oluşturmak için `.cer` sertifika, yürütün:</span><span class="sxs-lookup"><span data-stu-id="a75ed-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="a75ed-129">Azure sertifikaları hakkında daha fazla bilgi için bkz: [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a75ed-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="a75ed-130">OpenSSL parametreler tam bir açıklaması için belgelerine bakın [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="a75ed-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="a75ed-131">Bu dosyalar oluşturduktan sonra karşıya yüklemek gereken `.cer` "Ayarlar" sekmesinde "Karşıya Yükle" eylemini aracılığıyla Azure dosyasına [Klasik Azure portalı][management-portal], ve nerede Not gerekiyorsa, kaydedilen `.pem` dosya.</span><span class="sxs-lookup"><span data-stu-id="a75ed-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="a75ed-132">Abonelik Kimliğinizi aldıktan sonra bir sertifika oluşturulur ve karşıya `.cer` dosyasını Azure'a, abonelik kimliği ve yolunu geçirerek Azure yönetim uç noktasına bağlanabilir `.pem` dosya  **ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="a75ed-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="a75ed-133">Önceki örnekte `sms` olan bir **ServiceManagementService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="a75ed-134">**ServiceManagementService** Azure hizmetleri yönetmek için kullanılan birincil sınıf bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="a75ed-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="a75ed-135">Yönetim sertifikaları Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="a75ed-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="a75ed-136">Otomatik imzalı yönetim sertifikası, makine kullanarak oluşturabileceğiniz `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="a75ed-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="a75ed-137">Açık bir **Visual Studio komut istemi** olarak bir **yönetici** ve aşağıdaki komut, değiştirme *AzureCertificate* kullanmak istediğiniz sertifika adına sahip.</span><span class="sxs-lookup"><span data-stu-id="a75ed-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="a75ed-138">Komut oluşturur `.cer` dosya ve içinde yükler **kişisel** sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="a75ed-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="a75ed-139">Daha fazla bilgi için bkz: [Azure Cloud Services sertifikalarına genel bakış](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="a75ed-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="a75ed-140">Sertifika oluşturduktan sonra karşıya yüklemek gereken `.cer` "Ayarlar" sekmesinde "Karşıya Yükle" eylemini aracılığıyla Azure dosyasına [Klasik Azure portalı][management-portal].</span><span class="sxs-lookup"><span data-stu-id="a75ed-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="a75ed-141">Abonelik Kimliğinizi aldıktan sonra bir sertifika oluşturulur ve karşıya `.cer` dosyasını Azure'a, abonelik kimliği ve sertifikada konumunu geçirerek Azure yönetim uç noktasına bağlanabilir, **kişisel**  sertifika deposuna **ServiceManagementService** (yeniden Değiştir *AzureCertificate* sertifikanızın adıyla):</span><span class="sxs-lookup"><span data-stu-id="a75ed-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="a75ed-142">Önceki örnekte `sms` olan bir **ServiceManagementService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="a75ed-143">**ServiceManagementService** Azure hizmetleri yönetmek için kullanılan birincil sınıf bir sınıftır.</span><span class="sxs-lookup"><span data-stu-id="a75ed-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="a75ed-144"><a name="ListAvailableLocations"></a>Nasıl yapılır: kullanılabilir konumlarını listeleyin</span><span class="sxs-lookup"><span data-stu-id="a75ed-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="a75ed-145">Barındırma hizmetleri için kullanılabilir konumları listelemek için kullanın **listesi\_konumları** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="a75ed-146">Bir bulut hizmeti veya depolama hizmeti oluşturduğunuzda, geçerli bir konum sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="a75ed-147">**Listesi\_konumları** yöntem her zaman şu anda kullanılabilir konumların güncel bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a75ed-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="a75ed-148">Bu makalenin yazıldığı sırada kullanılabilir konumlarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a75ed-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="a75ed-149">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="a75ed-149">West Europe</span></span>
* <span data-ttu-id="a75ed-150">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="a75ed-150">North Europe</span></span>
* <span data-ttu-id="a75ed-151">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="a75ed-151">Southeast Asia</span></span>
* <span data-ttu-id="a75ed-152">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="a75ed-152">East Asia</span></span>
* <span data-ttu-id="a75ed-153">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="a75ed-153">Central US</span></span>
* <span data-ttu-id="a75ed-154">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="a75ed-154">North Central US</span></span>
* <span data-ttu-id="a75ed-155">Orta Güney ABD</span><span class="sxs-lookup"><span data-stu-id="a75ed-155">South Central US</span></span>
* <span data-ttu-id="a75ed-156">Batı ABD</span><span class="sxs-lookup"><span data-stu-id="a75ed-156">West US</span></span>
* <span data-ttu-id="a75ed-157">Doğu ABD</span><span class="sxs-lookup"><span data-stu-id="a75ed-157">East US</span></span>
* <span data-ttu-id="a75ed-158">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="a75ed-158">Japan East</span></span>
* <span data-ttu-id="a75ed-159">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="a75ed-159">Japan West</span></span>
* <span data-ttu-id="a75ed-160">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="a75ed-160">Brazil South</span></span>
* <span data-ttu-id="a75ed-161">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="a75ed-161">Australia East</span></span>
* <span data-ttu-id="a75ed-162">Avustralya Güneydoğu</span><span class="sxs-lookup"><span data-stu-id="a75ed-162">Australia Southeast</span></span>

## <span data-ttu-id="a75ed-163"><a name="CreateCloudService"></a>Nasıl yapılır: bir bulut hizmeti oluştur</span><span class="sxs-lookup"><span data-stu-id="a75ed-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="a75ed-164">Bir uygulama oluşturduğunuzda ve Azure'da çalıştırmak, kod ve yapılandırma birlikte Azure adlandırılır [bulut hizmeti] [ cloud service] (olarak bilinen bir *barındırılan hizmetin* önceki Azure serbest bırakır).</span><span class="sxs-lookup"><span data-stu-id="a75ed-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="a75ed-165">**Oluşturma\_barındırılan\_hizmet** yöntemi (hangi Azure içinde benzersiz olması gerekir) bir barındırılan hizmet adı, (otomatik olarak base64 kodlanmış) bir etiket, açıklama, sağlayarak yeni bir barındırılan hizmet oluşturmanıza olanak sağlar ve konumu.</span><span class="sxs-lookup"><span data-stu-id="a75ed-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="a75ed-166">Barındırılan tüm hizmetleri aboneliğinizle için listeleyebilirsiniz **listesi\_barındırılan\_Hizmetleri** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="a75ed-167">Belirli bir barındırılan hizmet hakkında bilgi almak istiyorsanız, bunu barındırılan hizmet adını geçirerek yapabilirsiniz **almak\_barındırılan\_hizmet\_özellikleri** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="a75ed-168">Bir bulut hizmeti oluşturduktan sonra kodunuzu hizmetiyle dağıtabileceğiniz **oluşturma\_dağıtım** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="a75ed-169"><a name="DeleteCloudService"></a>Nasıl yapılır: bir bulut hizmetini silin</span><span class="sxs-lookup"><span data-stu-id="a75ed-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="a75ed-170">Bir bulut hizmeti için hizmet adı geçirerek silebilirsiniz **silmek\_barındırılan\_hizmet** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="a75ed-171">Bir hizmet silmeden önce tüm dağıtımlar için hizmet silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="a75ed-172">(Bkz [nasıl yapılır: bir dağıtımı silin](#DeleteDeployment) Ayrıntılar için.)</span><span class="sxs-lookup"><span data-stu-id="a75ed-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="a75ed-173"><a name="DeleteDeployment"></a>Nasıl yapılır: bir dağıtımı silin</span><span class="sxs-lookup"><span data-stu-id="a75ed-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="a75ed-174">Bir dağıtımı silmek için kullanın **silmek\_dağıtım** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="a75ed-175">Aşağıdaki örnekte nasıl adlı bir dağıtım silineceğini gösterir `v1`.</span><span class="sxs-lookup"><span data-stu-id="a75ed-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="a75ed-176"><a name="CreateStorageService"></a>Nasıl yapılır: bir depolama birimi hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="a75ed-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="a75ed-177">A [depolama birimi hizmeti](../storage/common/storage-create-storage-account.md) , Azure'a erişmenizi [BLOB'lar](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabloları](../cosmos-db/table-storage-how-to-use-python.md), ve [sıraları](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a75ed-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="a75ed-178">Bir depolama birimi hizmeti oluşturmak için bir ad hizmeti (3 ila 24 küçük harf karakter ve Azure içinde benzersiz), bir açıklama, etiket (en fazla 100 karakter otomatik olarak base64 kodlanmış) ve bir konum gerekir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="a75ed-179">Aşağıdaki örnek, bir konum belirterek bir depolama birimi hizmeti oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a75ed-179">The following example shows how to create a storage service by specifying a location.</span></span>

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

<span data-ttu-id="a75ed-180">Önceki örnekte Not, durumunu **oluşturma\_depolama\_hesap** işlemi tarafından döndürülen sonuç geçirerek alınabilir **oluşturma\_depolama\_hesap** için **almak\_işlemi\_durum** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="a75ed-181">Depolama hesaplarınızı ve özellikleri ile listeleyebilirsiniz **listesi\_depolama\_hesapları** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="a75ed-182"><a name="DeleteStorageService"></a>Nasıl yapılır: bir depolama birimi hizmeti Sil</span><span class="sxs-lookup"><span data-stu-id="a75ed-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="a75ed-183">Depolama hizmet adına geçirerek bir depolama birimi hizmeti silebilirsiniz **silmek\_depolama\_hesap** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="a75ed-184">Bir depolama birimi hizmeti silme (BLOB'lar, tablolar ve Kuyruklar) hizmetinde depolanan tüm verileri siler.</span><span class="sxs-lookup"><span data-stu-id="a75ed-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="a75ed-185"><a name="ListOperatingSystems"></a>Nasıl yapılır: listesinde kullanılabilir işletim sistemleri</span><span class="sxs-lookup"><span data-stu-id="a75ed-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="a75ed-186">Barındırma hizmetleri için kullanılabilen işletim sistemlerini listelemek için kullanın **listesi\_işletim\_sistemleri** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="a75ed-187">Alternatif olarak, kullanabileceğiniz **listesi\_işletim\_sistem\_aileleri** işletim sistemi ailesi tarafından grupları yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="a75ed-188"><a name="CreateVMImage"></a>Nasıl yapılır: bir işletim sistemi görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="a75ed-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="a75ed-189">Görüntü deposu için bir işletim sistemi görüntüsü eklemek için kullanın **ekleme\_os\_görüntü** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

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

<span data-ttu-id="a75ed-190">Kullanılabilir işletim sistemi görüntülerini listelemek için kullanın **listesi\_os\_görüntüleri** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a75ed-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="a75ed-191">Tüm platform görüntüleri ve kullanıcı görüntüleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a75ed-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="a75ed-192"><a name="DeleteVMImage"></a>Nasıl yapılır: bir işletim sistemi görüntüsünü silme</span><span class="sxs-lookup"><span data-stu-id="a75ed-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="a75ed-193">Bir kullanıcı görüntüsü silmek için kullanın **silmek\_os\_görüntü** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="a75ed-194"><a name="CreateVM"></a>Nasıl yapılır: bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="a75ed-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="a75ed-195">Bir sanal makine oluşturmak için önce oluşturmanız gerekir bir [bulut hizmeti](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="a75ed-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="a75ed-196">Dağıtım kullanarak sanal makineyi oluşturmak **oluşturma\_sanal\_makine\_dağıtım** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
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

## <span data-ttu-id="a75ed-197"><a name="DeleteVM"></a>Nasıl yapılır: bir sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="a75ed-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="a75ed-198">Bir sanal makineyi silmek için önce dağıtım kullanarak silmeniz **silmek\_dağıtım** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="a75ed-199">Bulut hizmeti kullanılarak sonra silinebilir **silmek\_barındırılan\_hizmet** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="a75ed-200">Nasıl yapılır: bir sanal makine yakalanan görüntüden sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="a75ed-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="a75ed-201">Bir VM görüntüsü yakalamak için ilk çağrı **yakalama\_vm\_görüntü** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a75ed-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
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

<span data-ttu-id="a75ed-202">Ardından, görüntüyü başarıyla yakaladıktan emin olmak için kullanın **listesi\_vm\_görüntüleri** API'sini ve görüntünüzü sonuçlarında görüntülenen emin olun:</span><span class="sxs-lookup"><span data-stu-id="a75ed-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="a75ed-203">Son olarak yakalanan görüntüyü kullanarak sanal makine oluşturmak için kullanın **oluşturma\_sanal\_makine\_dağıtım** önce ancak bu kez vm_image_name yerine geçirirken yöntemi</span><span class="sxs-lookup"><span data-stu-id="a75ed-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
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

<span data-ttu-id="a75ed-204">Linux sanal makine yakalama hakkında daha fazla bilgi için bkz: [Linux sanal makine yakalama.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a75ed-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="a75ed-205">Windows sanal makinesi yakalama hakkında daha fazla bilgi için bkz: [Windows sanal makinesi yakalama.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a75ed-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="a75ed-206"><a name="What's Next"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a75ed-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="a75ed-207">Hizmet Yönetimi öğrendiğinize göre erişebilirsiniz [tam API başvuru belgeleri Azure Python SDK'sı](http://azure-sdk-for-python.readthedocs.org/) ve python uygulamanızı kolayca yönetmek için karmaşık görevleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a75ed-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="a75ed-208">Daha fazla bilgi için bkz. [Python Geliştirici Merkezi](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="a75ed-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
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
