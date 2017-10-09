---
title: "Azure depolama için bir bağlantı dizesi aaaConfigure | Microsoft Docs"
description: "Bir Azure depolama hesabı için bir bağlantı dizesi yapılandırın. Bir bağlantı dizesi tooauthenticate tooa depolama hesabı uygulamanızdan çalışma zamanında gereken erişim hello bilgiler içerir."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: ac1d7d9bf11fa6f44243cda0c40d8faee12e513b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="78845-104">Azure Storage bağlantı dizelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="78845-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="78845-105">Bir bağlantı dizesi uygulama tooaccess verilerinizi çalışma zamanında bir Azure depolama hesabı için gerekli hello kimlik doğrulama bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="78845-105">A connection string includes hello authentication information required for your application tooaccess data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="78845-106">Bağlantı dizeleri için yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="78845-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="78845-107">Toohello Azure storage öykünücüsü bağlayın.</span><span class="sxs-lookup"><span data-stu-id="78845-107">Connect toohello Azure storage emulator.</span></span>
* <span data-ttu-id="78845-108">Azure depolama hesabı erişim.</span><span class="sxs-lookup"><span data-stu-id="78845-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="78845-109">Paylaşılan erişim imzası (SAS) aracılığıyla Azure içinde belirtilen kaynaklara erişir.</span><span class="sxs-lookup"><span data-stu-id="78845-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="78845-110">Bağlantı dizenizi depolanması</span><span class="sxs-lookup"><span data-stu-id="78845-110">Storing your connection string</span></span>
<span data-ttu-id="78845-111">Uygulamanızı tooaccess hello bağlantı dizesi çalışma zamanı tooauthenticate yapılan istekleri tooAzure depolama konumunda gerekir.</span><span class="sxs-lookup"><span data-stu-id="78845-111">Your application needs tooaccess hello connection string at runtime tooauthenticate requests made tooAzure Storage.</span></span> <span data-ttu-id="78845-112">Bağlantı dizenizi depolamak için birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="78845-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="78845-113">Çalışan hello Masaüstü veya bir aygıtta bir uygulama hello bağlantı dizesinde depolayabilir bir **app.config** veya **web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="78845-113">An application running on hello desktop or on a device can store hello connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="78845-114">Merhaba bağlantı dizesi toohello ekleme **AppSettings** bu dosyaları bölümünde.</span><span class="sxs-lookup"><span data-stu-id="78845-114">Add hello connection string toohello **AppSettings** section in these files.</span></span>
* <span data-ttu-id="78845-115">Bir Azure bulut hizmetindeki çalışan bir uygulama hello bağlantı dizesi hello depolayabilir [Azure hizmet yapılandırma (.cscfg) şema dosyası](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="78845-115">An application running in an Azure cloud service can store hello connection string in hello [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="78845-116">Merhaba bağlantı dizesi toohello ekleme **ConfigurationSettings** hello hizmet yapılandırma dosyasının.</span><span class="sxs-lookup"><span data-stu-id="78845-116">Add hello connection string toohello **ConfigurationSettings** section of hello service configuration file.</span></span>
* <span data-ttu-id="78845-117">Bağlantı dizenizi doğrudan kodunuzda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78845-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="78845-118">Ancak, çoğu senaryoda yapılandırma dosyasında bağlantı dizenizi depolamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="78845-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="78845-119">Bağlantı dizenizi bir yapılandırma dosyasında depolanması, bu kolay tooupdate hello bağlantı dizesi tooswitch hello depolama öykünücüsü Azure storage hesabı arasındaki hello bulutta sağlar.</span><span class="sxs-lookup"><span data-stu-id="78845-119">Storing your connection string in a configuration file makes it easy tooupdate hello connection string tooswitch between hello storage emulator and an Azure storage account in hello cloud.</span></span> <span data-ttu-id="78845-120">Yalnızca tooedit hello bağlantı dizesi toopoint tooyour hedef ortam gerekir.</span><span class="sxs-lookup"><span data-stu-id="78845-120">You only need tooedit hello connection string toopoint tooyour target environment.</span></span>

<span data-ttu-id="78845-121">Merhaba kullanabilirsiniz [Microsoft Azure Yapılandırma Yöneticisi](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) , bağlantı dizesi, uygulamanızın nerede çalıştığına bakmaksızın çalışma zamanında tooaccess.</span><span class="sxs-lookup"><span data-stu-id="78845-121">You can use hello [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-hello-storage-emulator"></a><span data-ttu-id="78845-122">Merhaba depolama öykünücüsü için bağlantı dizesi oluştur</span><span class="sxs-lookup"><span data-stu-id="78845-122">Create a connection string for hello storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="78845-123">Merhaba depolama öykünücüsü hakkında daha fazla bilgi için bkz: [geliştirme ve test amacıyla hello Azure storage öykünücüsünü kullanma](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="78845-123">For more information about hello storage emulator, see [Use hello Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="78845-124">Bir Azure depolama hesabı için bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="78845-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="78845-125">Azure depolama hesabınız için bir bağlantı dizesi toocreate, kullanım hello aşağıdaki biçimi.</span><span class="sxs-lookup"><span data-stu-id="78845-125">toocreate a connection string for your Azure storage account, use hello following format.</span></span> <span data-ttu-id="78845-126">(Önerilen) HTTPS üzerinden tooconnect toohello depolama hesabı isteyip istemediğiniz veya HTTP belirtmek, yerine `myAccountName` hello adlı depolama hesabı ve Değiştir `myAccountKey` hesabının erişim anahtarı ile:</span><span class="sxs-lookup"><span data-stu-id="78845-126">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="78845-127">Örneğin, bağlantı dizenizi benzer şekilde görünebilir:</span><span class="sxs-lookup"><span data-stu-id="78845-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="78845-128">Azure Storage HTTP ve HTTPS bağlantı dizesinde desteklemesine rağmen *HTTPS tavsiye*.</span><span class="sxs-lookup"><span data-stu-id="78845-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="78845-129">Depolama hesabınızın bağlantı dizeleri hello bulabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78845-129">You can find your storage account's connection strings in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="78845-130">Çok gidin**ayarları** > **erişim anahtarları** depolama hesabınızın menü dikey toosee bağlantı dizelerinde her iki birincil ve ikincil erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="78845-130">Navigate too**SETTINGS** > **Access keys** in your storage account's menu blade toosee connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="78845-131">Paylaşılan erişim imzası kullanarak bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="78845-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="78845-132">Bir açık depolama uç nokta için bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="78845-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="78845-133">Merhaba varsayılan uç noktaları kullanmak yerine, bağlantı dizesinde açık hizmet uç noktaları belirtin.</span><span class="sxs-lookup"><span data-stu-id="78845-133">You can specify explicit service endpoints in your connection string instead of using hello default endpoints.</span></span> <span data-ttu-id="78845-134">toocreate açık bir uç nokta belirten bir bağlantı dizesi biçimi aşağıdaki hello hello protokolü belirtimi (HTTPS (önerilen) veya HTTP) dahil olmak üzere her hizmet için hello tüm hizmet uç noktası belirtin:</span><span class="sxs-lookup"><span data-stu-id="78845-134">toocreate a connection string that specifies an explicit endpoint, specify hello complete service endpoint for each service, including hello protocol specification (HTTPS (recommended) or HTTP), in hello following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="78845-135">Blob storage uç nokta tooa eşlenen nerede istediğiniz toospecify açık bir uç nokta bir senaryo olduğunda [özel etki alanı](../blobs/storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="78845-135">One scenario where you might wish toospecify an explicit endpoint is when you've mapped your Blob storage endpoint tooa [custom domain](../blobs/storage-custom-domain-name.md).</span></span> <span data-ttu-id="78845-136">Bu durumda, bağlantı dizenizi Blob storage için özel uç noktanızı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78845-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="78845-137">Uygulamanız bunları kullanıyorsa diğer hizmetler hello için hello varsayılan uç noktalar isteğe bağlı olarak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78845-137">You can optionally specify hello default endpoints for hello other services if your application uses them.</span></span>

<span data-ttu-id="78845-138">Burada, hello Blob hizmeti için açık bir uç nokta belirten bir bağlantı dizesi örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="78845-138">Here is an example of a connection string that specifies an explicit endpoint for hello Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="78845-139">Bu örnek hello Blob hizmeti için özel bir etki alanı dahil olmak üzere tüm hizmetleri için açık uç nokta belirtir:</span><span class="sxs-lookup"><span data-stu-id="78845-139">This example specifies explicit endpoints for all services, including a custom domain for hello Blob service:</span></span>

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="78845-140">Merhaba uç değerler bağlantı dizesinde kullanılan tooconstruct hello isteği URI'ler toohello depolama hizmetleri ve tooyour kodu döndürdü URI'ler hello biçiminde dikte.</span><span class="sxs-lookup"><span data-stu-id="78845-140">hello endpoint values in a connection string are used tooconstruct hello request URIs toohello storage services, and dictate hello form of any URIs that are returned tooyour code.</span></span>

<span data-ttu-id="78845-141">Depolama uç nokta tooa özel bir etki alanı eşlenen ve bu uç bağlantı dizesinden mümkün toouse olmaz atlayın Bu bağlantı o hizmet kodunuzdan tooaccess verileri dize.</span><span class="sxs-lookup"><span data-stu-id="78845-141">If you've mapped a storage endpoint tooa custom domain and omit that endpoint from a connection string, then you will not be able toouse that connection string tooaccess data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78845-142">Hizmet uç noktası değerleri bağlantı dizelerinizi doğru biçimlendirilmiş olmalıdır URI'ler dahil olmak üzere, `https://` (önerilen) veya `http://`.</span><span class="sxs-lookup"><span data-stu-id="78845-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="78845-143">Azure Storage henüz HTTPS özel etki alanları için desteklemediğinden, *gerekir* belirtin `http://` için herhangi bir uç nokta tooa özel etki alanı gösteren URI.</span><span class="sxs-lookup"><span data-stu-id="78845-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points tooa custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="78845-144">Bir uç nokta soneki ile bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="78845-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="78845-145">toocreate bir bağlantı dizesi için bölgeler ve farklı uç nokta sonekleri örnekleriyle depolama hizmetinde gibi Azure Çin veya Azure kamu, bağlantı dizesi biçimi aşağıdaki kullanım hello için.</span><span class="sxs-lookup"><span data-stu-id="78845-145">toocreate a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use hello following connection string format.</span></span> <span data-ttu-id="78845-146">(Önerilen) HTTPS üzerinden tooconnect toohello depolama hesabı isteyip istemediğiniz veya HTTP belirtmek, yerine `myAccountName` depolama hesabınız hello adıyla değiştirin `myAccountKey` hesap erişim tuşu ve Değiştir ile `mySuffix` hello URI ile soneki:</span><span class="sxs-lookup"><span data-stu-id="78845-146">Indicate whether you want tooconnect toohello storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with hello name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with hello URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="78845-147">Bir örnek bağlantı dizesi Azure Çin'de depolama hizmetleri aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="78845-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="78845-148">Bir bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="78845-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="78845-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78845-149">Next steps</span></span>
* [<span data-ttu-id="78845-150">Geliştirme ve test amacıyla Hello Azure storage öykünücüsünü kullanma</span><span class="sxs-lookup"><span data-stu-id="78845-150">Use hello Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="78845-151">Azure depolama gezginleri</span><span class="sxs-lookup"><span data-stu-id="78845-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="78845-152">Paylaşılan erişim imzaları (SAS) kullanma</span><span class="sxs-lookup"><span data-stu-id="78845-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

