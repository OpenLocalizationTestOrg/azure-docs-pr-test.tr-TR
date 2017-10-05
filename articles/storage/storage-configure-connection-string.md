---
title: "Azure Storage için bir bağlantı dizesi yapılandırma | Microsoft Docs"
description: "Bir Azure depolama hesabı için bir bağlantı dizesi yapılandırın. Bir bağlantı dizesi çalışma zamanında uygulamanızdan bir depolama hesabına erişimi kimlik doğrulaması yapmak için gereken bilgileri içerir."
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
ms.openlocfilehash: 01aa506e2b47fc29a70592e670a206a2b74248a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-azure-storage-connection-strings"></a><span data-ttu-id="ba12c-104">Azure Storage bağlantı dizelerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba12c-104">Configure Azure Storage connection strings</span></span>

<span data-ttu-id="ba12c-105">Bir bağlantı dizesi uygulamanız çalışma zamanında bir Azure depolama hesabındaki verilere erişmek için gereken kimlik doğrulama bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="ba12c-105">A connection string includes the authentication information required for your application to access data in an Azure Storage account at runtime.</span></span> <span data-ttu-id="ba12c-106">Bağlantı dizeleri için yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ba12c-106">You can configure connection strings to:</span></span>

* <span data-ttu-id="ba12c-107">Azure storage öykünücüsü bağlayın.</span><span class="sxs-lookup"><span data-stu-id="ba12c-107">Connect to the Azure storage emulator.</span></span>
* <span data-ttu-id="ba12c-108">Azure depolama hesabı erişim.</span><span class="sxs-lookup"><span data-stu-id="ba12c-108">Access a storage account in Azure.</span></span>
* <span data-ttu-id="ba12c-109">Paylaşılan erişim imzası (SAS) aracılığıyla Azure içinde belirtilen kaynaklara erişir.</span><span class="sxs-lookup"><span data-stu-id="ba12c-109">Access specified resources in Azure via a shared access signature (SAS).</span></span>

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a><span data-ttu-id="ba12c-110">Bağlantı dizenizi depolanması</span><span class="sxs-lookup"><span data-stu-id="ba12c-110">Storing your connection string</span></span>
<span data-ttu-id="ba12c-111">Azure depolama alanına yapılan istekleri kimlik doğrulaması için çalışma zamanında bağlantı dizesi erişmek uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba12c-111">Your application needs to access the connection string at runtime to authenticate requests made to Azure Storage.</span></span> <span data-ttu-id="ba12c-112">Bağlantı dizenizi depolamak için birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="ba12c-112">You have several options for storing your connection string:</span></span>

* <span data-ttu-id="ba12c-113">Masaüstünde veya bir cihazdaki uygulama çalıştıran bir bağlantı dizesinde depolayabilir bir **app.config** veya **web.config** dosya.</span><span class="sxs-lookup"><span data-stu-id="ba12c-113">An application running on the desktop or on a device can store the connection string in an **app.config** or **web.config** file.</span></span> <span data-ttu-id="ba12c-114">Bağlantı dizesine eklemek **AppSettings** bu dosyaları bölümünde.</span><span class="sxs-lookup"><span data-stu-id="ba12c-114">Add the connection string to the **AppSettings** section in these files.</span></span>
* <span data-ttu-id="ba12c-115">Bir Azure bulut hizmetindeki çalışan bir uygulamaya bağlantı dizesinde depolayabilir [Azure hizmet yapılandırma (.cscfg) şema dosyası](https://msdn.microsoft.com/library/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="ba12c-115">An application running in an Azure cloud service can store the connection string in the [Azure service configuration schema (.cscfg) file](https://msdn.microsoft.com/library/ee758710.aspx).</span></span> <span data-ttu-id="ba12c-116">Bağlantı dizesine eklemek **ConfigurationSettings** hizmet yapılandırma dosyasının.</span><span class="sxs-lookup"><span data-stu-id="ba12c-116">Add the connection string to the **ConfigurationSettings** section of the service configuration file.</span></span>
* <span data-ttu-id="ba12c-117">Bağlantı dizenizi doğrudan kodunuzda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba12c-117">You can use your connection string directly in your code.</span></span> <span data-ttu-id="ba12c-118">Ancak, çoğu senaryoda yapılandırma dosyasında bağlantı dizenizi depolamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="ba12c-118">However, we recommend that you store your connection string in a configuration file in most scenarios.</span></span>

<span data-ttu-id="ba12c-119">Bağlantı dizenizi bir yapılandırma dosyasında depolamak depolama öykünücüsünü ve buluttaki bir Azure depolama hesabını arasında geçiş yapmak için bağlantı dizesini güncellemeniz kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ba12c-119">Storing your connection string in a configuration file makes it easy to update the connection string to switch between the storage emulator and an Azure storage account in the cloud.</span></span> <span data-ttu-id="ba12c-120">Yalnızca hedef ortamınızı noktası için bağlantı dizesi düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba12c-120">You only need to edit the connection string to point to your target environment.</span></span>

<span data-ttu-id="ba12c-121">Kullanabileceğiniz [Microsoft Azure Yapılandırma Yöneticisi](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) , uygulamanızın nerede çalıştığına bakmaksızın çalışma zamanında bağlantı dizenizi erişmek için.</span><span class="sxs-lookup"><span data-stu-id="ba12c-121">You can use the [Microsoft Azure Configuration Manager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) to access your connection string at runtime regardless of where your application is running.</span></span>

## <a name="create-a-connection-string-for-the-storage-emulator"></a><span data-ttu-id="ba12c-122">Bir bağlantı dizesi oluşturmak için depolama öykünücüsü</span><span class="sxs-lookup"><span data-stu-id="ba12c-122">Create a connection string for the storage emulator</span></span>
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

<span data-ttu-id="ba12c-123">Depolama öykünücüsü hakkında daha fazla bilgi için bkz: [geliştirme ve sınama için Azure storage öykünücüsünü kullanma](storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ba12c-123">For more information about the storage emulator, see [Use the Azure storage emulator for development and testing](storage-use-emulator.md).</span></span>

## <a name="create-a-connection-string-for-an-azure-storage-account"></a><span data-ttu-id="ba12c-124">Bir Azure depolama hesabı için bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba12c-124">Create a connection string for an Azure storage account</span></span>
<span data-ttu-id="ba12c-125">Azure depolama hesabınız için bir bağlantı dizesi oluşturmak için aşağıdaki biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba12c-125">To create a connection string for your Azure storage account, use the following format.</span></span> <span data-ttu-id="ba12c-126">(Önerilen) HTTPS üzerinden depolama hesabı bağlanmak istediğiniz veya HTTP belirtmek, yerine `myAccountName` depolama hesabı ve Değiştir adıyla `myAccountKey` hesabının erişim anahtarı ile:</span><span class="sxs-lookup"><span data-stu-id="ba12c-126">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, and replace `myAccountKey` with your account access key:</span></span>

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

<span data-ttu-id="ba12c-127">Örneğin, bağlantı dizenizi benzer şekilde görünebilir:</span><span class="sxs-lookup"><span data-stu-id="ba12c-127">For example, your connection string might look similar to:</span></span>

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

<span data-ttu-id="ba12c-128">Azure Storage HTTP ve HTTPS bağlantı dizesinde desteklemesine rağmen *HTTPS tavsiye*.</span><span class="sxs-lookup"><span data-stu-id="ba12c-128">Although Azure Storage supports both HTTP and HTTPS in a connection string, *HTTPS is highly recommended*.</span></span>

> [!TIP]
> <span data-ttu-id="ba12c-129">Depolama hesabınızın bağlantı dizeleri bulabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba12c-129">You can find your storage account's connection strings in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ba12c-130">Gidin **ayarları** > **erişim anahtarları** bağlantı dizeleri için hem birincil ve ikincil erişim tuşlarını görmek için depolama hesabınızın menü dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="ba12c-130">Navigate to **SETTINGS** > **Access keys** in your storage account's menu blade to see connection strings for both primary and secondary access keys.</span></span>
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a><span data-ttu-id="ba12c-131">Paylaşılan erişim imzası kullanarak bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba12c-131">Create a connection string using a shared access signature</span></span>
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a><span data-ttu-id="ba12c-132">Bir açık depolama uç nokta için bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba12c-132">Create a connection string for an explicit storage endpoint</span></span>
<span data-ttu-id="ba12c-133">Varsayılan uç noktalar kullanmak yerine, bağlantı dizesinde açık hizmet uç noktaları belirtin.</span><span class="sxs-lookup"><span data-stu-id="ba12c-133">You can specify explicit service endpoints in your connection string instead of using the default endpoints.</span></span> <span data-ttu-id="ba12c-134">Açık bir uç nokta belirten bir bağlantı dizesi oluşturmak için aşağıdaki biçimde protokolü belirtimi (HTTPS (önerilen) veya HTTP) dahil olmak üzere her hizmet için tam Hizmeti uç noktası belirtin:</span><span class="sxs-lookup"><span data-stu-id="ba12c-134">To create a connection string that specifies an explicit endpoint, specify the complete service endpoint for each service, including the protocol specification (HTTPS (recommended) or HTTP), in the following format:</span></span>

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

<span data-ttu-id="ba12c-135">Blob storage uç noktanız eşlenen nerede istediğiniz açık bir uç nokta belirtmek için bir senaryo olduğunda bir [özel etki alanı](storage-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="ba12c-135">One scenario where you might wish to specify an explicit endpoint is when you've mapped your Blob storage endpoint to a [custom domain](storage-custom-domain-name.md).</span></span> <span data-ttu-id="ba12c-136">Bu durumda, bağlantı dizenizi Blob storage için özel uç noktanızı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba12c-136">In that case, you can specify your custom endpoint for Blob storage in your connection string.</span></span> <span data-ttu-id="ba12c-137">Uygulamanız bunları kullanıyorsa, isteğe bağlı olarak diğer hizmetler için varsayılan uç noktalar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba12c-137">You can optionally specify the default endpoints for the other services if your application uses them.</span></span>

<span data-ttu-id="ba12c-138">Burada, Blob hizmeti için açık bir uç nokta belirten bir bağlantı dizesi örneği verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ba12c-138">Here is an example of a connection string that specifies an explicit endpoint for the Blob service:</span></span>

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

<span data-ttu-id="ba12c-139">Bu örnek Blob hizmeti için özel bir etki alanı dahil olmak üzere tüm hizmetleri için açık uç nokta belirtir:</span><span class="sxs-lookup"><span data-stu-id="ba12c-139">This example specifies explicit endpoints for all services, including a custom domain for the Blob service:</span></span>

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

<span data-ttu-id="ba12c-140">Bir bağlantı dizesi uç nokta değerleri depolama hizmetleri için URI isteği oluşturun ve kodunuzu döndürülen URI'ler form dikte için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba12c-140">The endpoint values in a connection string are used to construct the request URIs to the storage services, and dictate the form of any URIs that are returned to your code.</span></span>

<span data-ttu-id="ba12c-141">Bir depolama uç noktası için özel bir etki alanı eşlenen ve bu uç bağlantı dizesinden atlarsanız, daha sonra kodunuzdan bu hizmetindeki verilere erişmek için bağlantı dizesini kullanmanız mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="ba12c-141">If you've mapped a storage endpoint to a custom domain and omit that endpoint from a connection string, then you will not be able to use that connection string to access data in that service from your code.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba12c-142">Hizmet uç noktası değerleri bağlantı dizelerinizi doğru biçimlendirilmiş olmalıdır URI'ler dahil olmak üzere, `https://` (önerilen) veya `http://`.</span><span class="sxs-lookup"><span data-stu-id="ba12c-142">Service endpoint values in your connection strings must be well-formed URIs, including `https://` (recommended) or `http://`.</span></span> <span data-ttu-id="ba12c-143">Azure Storage henüz HTTPS özel etki alanları için desteklemediğinden, *gerekir* belirtin `http://` için herhangi bir uç nokta için özel bir etki alanı gösteren URI.</span><span class="sxs-lookup"><span data-stu-id="ba12c-143">Because Azure Storage does not yet support HTTPS for custom domains, you *must* specify `http://` for any endpoint URI that points to a custom domain.</span></span>
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a><span data-ttu-id="ba12c-144">Bir uç nokta soneki ile bir bağlantı dizesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba12c-144">Create a connection string with an endpoint suffix</span></span>
<span data-ttu-id="ba12c-145">Azure Çin veya Azure kamu gibi bölgelerde veya farklı uç nokta sonekleri örnekleriyle depolama hizmeti için bir bağlantı dizesi oluşturmak için aşağıdaki bağlantı dizesi biçimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba12c-145">To create a connection string for a storage service in regions or instances with different endpoint suffixes, such as for Azure China or Azure Government, use the following connection string format.</span></span> <span data-ttu-id="ba12c-146">(Önerilen) HTTPS üzerinden depolama hesabı bağlanmak istediğiniz veya HTTP belirtmek, yerine `myAccountName` depolama hesabınızın adıyla değiştirin `myAccountKey` hesap erişim tuşu ve Değiştir ile `mySuffix` URI soneki:</span><span class="sxs-lookup"><span data-stu-id="ba12c-146">Indicate whether you want to connect to the storage account through HTTPS (recommended) or HTTP, replace `myAccountName` with the name of your storage account, replace `myAccountKey` with your account access key, and replace `mySuffix` with the URI suffix:</span></span>

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

<span data-ttu-id="ba12c-147">Bir örnek bağlantı dizesi Azure Çin'de depolama hizmetleri aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="ba12c-147">Here's an example connection string for storage services in Azure China:</span></span>

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a><span data-ttu-id="ba12c-148">Bir bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="ba12c-148">Parsing a connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a><span data-ttu-id="ba12c-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba12c-149">Next steps</span></span>
* [<span data-ttu-id="ba12c-150">Geliştirme ve sınama için Azure storage öykünücüsünü kullanma</span><span class="sxs-lookup"><span data-stu-id="ba12c-150">Use the Azure storage emulator for development and testing</span></span>](storage-use-emulator.md)
* [<span data-ttu-id="ba12c-151">Azure depolama gezginleri</span><span class="sxs-lookup"><span data-stu-id="ba12c-151">Azure Storage explorers</span></span>](storage-explorers.md)
* [<span data-ttu-id="ba12c-152">Paylaşılan erişim imzaları (SAS) kullanma</span><span class="sxs-lookup"><span data-stu-id="ba12c-152">Using Shared Access Signatures (SAS)</span></span>](storage-dotnet-shared-access-signature-part-1.md)

