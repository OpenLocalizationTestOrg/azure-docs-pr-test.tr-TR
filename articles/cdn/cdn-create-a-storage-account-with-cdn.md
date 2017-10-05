---
title: "Azure storage hesabı Azure CDN ile tümleştirme | Microsoft Docs"
description: "Azure Storage bloblarından önbelleğe alarak yüksek bant genişliği içerik ulaştırmak için Azure içerik teslim ağı (CDN) kullanmayı öğrenin."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: cbc2ff98-916d-4339-8959-622823c5b772
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 511076935d06ed0908341044e37069e74530be49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="28b80-103">Azure storage hesabı Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="28b80-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="28b80-104">CDN önbellek içeriği Azure depolama hesabınızdan etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="28b80-104">CDN can be enabled to cache content from your Azure storage.</span></span> <span data-ttu-id="28b80-105">Geliştiriciler BLOB'ları ve işlem örnekleri ABD, Avrupa, Asya, Avustralya ve Güney Amerika fiziksel düğümlerde, statik içeriği önbelleğe alarak yüksek bant genişliği içeriği teslimi için genel bir çözüm sunar.</span><span class="sxs-lookup"><span data-stu-id="28b80-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in the United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="28b80-106">1. adım: depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="28b80-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="28b80-107">Bir Azure aboneliği için yeni bir depolama hesabı oluşturmak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="28b80-107">Use the following procedure to create a new storage account for a Azure subscription.</span></span> <span data-ttu-id="28b80-108">Bir depolama hesabı için Azure storage hizmetlerine erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="28b80-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="28b80-109">Depolama hesabı Azure depolama hizmeti bileşenlerinin her biri erişmek için ad alanı en yüksek düzeyde temsil eder: Blob Hizmetleri, kuyruk Hizmetleri ve Tablo Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="28b80-109">The storage account represents the highest level of the namespace for accessing each of the Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="28b80-110">Daha fazla bilgi için bkz [Microsoft Azure Storage'a giriş](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28b80-110">For more information, refer to the [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="28b80-111">Bir depolama hesabı oluşturmak için Hizmet Yöneticisi veya ilişkili abonelik için bir ortak yönetici olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="28b80-111">To create a storage account, you must be either the service administrator or a co-administrator for the associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="28b80-112">Azure Portal ve Powershell dahil olmak üzere bir depolama hesabı oluşturmak için kullanabileceğiniz çeşitli yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="28b80-112">There are several methods you can use to create a storage account, including the Azure Portal and Powershell.</span></span>  <span data-ttu-id="28b80-113">Bu öğretici için size Azure portalını kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="28b80-113">For this tutorial, we'll be using the Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="28b80-114">**Bir Azure aboneliği için bir depolama hesabı oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="28b80-114">**To create a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="28b80-115">[Azure Portal](https://portal.azure.com)'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="28b80-115">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="28b80-116">Sol üst köşedeki seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="28b80-116">In the upper left corner, select **New**.</span></span> <span data-ttu-id="28b80-117">İçinde **yeni** iletişim kutusunda **veri + depolama**, ardından **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="28b80-117">In the **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="28b80-118">**Depolama hesabı oluşturma** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="28b80-118">The **Create storage account** blade appears.</span></span>   

    ![Depolama hesabı oluşturma][create-new-storage-account]  

3. <span data-ttu-id="28b80-120">İçinde **adı** alanında, bir alt etki alanı adı yazın.</span><span class="sxs-lookup"><span data-stu-id="28b80-120">In the **Name** field, type a subdomain name.</span></span> <span data-ttu-id="28b80-121">Bu giriş, 3-24 küçük harfler ve sayılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="28b80-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="28b80-122">Bu değer aboneliği için Blob, kuyruk veya tablo kaynak adres için kullanılan URI içindeki konak adına dönüşür.</span><span class="sxs-lookup"><span data-stu-id="28b80-122">This value becomes the host name within the URI that is used to address Blob, Queue, or Table resources for the subscription.</span></span> <span data-ttu-id="28b80-123">Blob hizmetinde kapsayıcı kaynak adres için aşağıdaki biçimde bir URI kullanırsınız. burada  *&lt;StorageAccountLabel&gt;*  , yazdığınız değer başvurduğu **birURLgirin**:</span><span class="sxs-lookup"><span data-stu-id="28b80-123">To address a container resource in the Blob service, you would use a URI in the following format, where *&lt;StorageAccountLabel&gt;* refers to the value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="28b80-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="28b80-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="28b80-125">**Önemli:** URL depolama hesabının URI alt etki alanı forms etiket ve azure'da barındırılan tüm hizmetler arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="28b80-125">**Important:** The URL label forms the subdomain of the storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="28b80-126">Bu değer, aynı zamanda bu hesabı program aracılığıyla erişirken Portalı'nda veya bu depolama hesabı adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="28b80-126">This value is also used as the name of this storage account in the portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="28b80-127">Varsayılan değerleri bırakın **dağıtım modeli**, **tür hesap**, **performans**, ve **çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="28b80-127">Leave the defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="28b80-128">Seçin **abonelik** depolama hesabı ile kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="28b80-128">Select the **Subscription** that the storage account will be used with.</span></span>
6. <span data-ttu-id="28b80-129">Bir **Kaynak Grubu** seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="28b80-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="28b80-130">Kaynak Grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="28b80-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="28b80-131">Depolama hesabınız için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="28b80-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="28b80-132">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28b80-132">Click **Create**.</span></span> <span data-ttu-id="28b80-133">Depolama hesabı oluşturma işleminin tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="28b80-133">The process of creating the storage account might take several minutes to complete.</span></span>

## <a name="step-2-enable-cdn-for-the-storage-account"></a><span data-ttu-id="28b80-134">2. adım: Depolama hesabı için CDN etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="28b80-134">Step 2: Enable CDN for the storage account</span></span>

<span data-ttu-id="28b80-135">En yeni tümleştirmesi ile artık CDN depolama hesabınız için depolama portal uzantınızı ayrılmadan etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28b80-135">With the newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="28b80-136">Depolama hesabını seçin, "CDN" ya da aşağı sol gezinti menüsünde arayın, ardından "Azure CDN"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="28b80-136">Select the storage account, search "CDN" or scroll down from the left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="28b80-137">**Azure CDN** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="28b80-137">The **Azure CDN** blade appears.</span></span>

    ![CDN etkinleştir gezinme][cdn-enable-navigation]
    
2. <span data-ttu-id="28b80-139">Gerekli bilgileri girerek yeni bir uç noktası oluşturun</span><span class="sxs-lookup"><span data-stu-id="28b80-139">Create a new endpoint by entering the required information</span></span>
    - <span data-ttu-id="28b80-140">**CDN profili**: yeni oluşturun veya varolan bir profili kullanın.</span><span class="sxs-lookup"><span data-stu-id="28b80-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="28b80-141">**Fiyatlandırma katmanı**: yeni bir CDN profili oluşturursanız, bir fiyatlandırma katmanı seçmek yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="28b80-141">**Pricing tier**: You only need to select a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="28b80-142">**CDN uç nokta adı**: tercih ettiğiniz her bir uç nokta adı girin.</span><span class="sxs-lookup"><span data-stu-id="28b80-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="28b80-143">Oluşturulan CDN uç noktası ana bilgisayar depolama hesabınızın adını varsayılan olarak kaynak kullanır.</span><span class="sxs-lookup"><span data-stu-id="28b80-143">The created CDN endpoint uses the hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="28b80-144">! [cdn yeni uç nokta oluşturma] [cdn yeni-endpoint-oluşturma]</span><span class="sxs-lookup"><span data-stu-id="28b80-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="28b80-145">Oluşturulduktan sonra yeni uç nokta yukarıdaki uç nokta listesinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="28b80-145">After creation, the new endpoint will show up in the endpoint list above.</span></span>

    ![CDN depolama yeni uç noktası][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="28b80-147">CDN etkinleştirmek için Azure CDN uzantısı de gidebilirsiniz. [Öğreticisi](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="28b80-147">You can also go to Azure CDN extension to enable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="28b80-148">3. adım: ek CDN özellikleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="28b80-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="28b80-149">Depolama hesabı "Azure CDN" dikey penceresinden CDN yapılandırma dikey penceresini açmak için listeden CDN uç noktası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="28b80-149">From storage account "Azure CDN" blade, click the CDN endpoint from the list to open CDN configuration blade.</span></span> <span data-ttu-id="28b80-150">Sıkıştırma ve sorgu dizesi gibi teslimat için ek CDN özellikleri etkinleştirebilirsiniz coğrafi filtreleme.</span><span class="sxs-lookup"><span data-stu-id="28b80-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="28b80-151">Ayrıca, özel etki alanı eşleme CDN uç noktanızı eklemeyi ve özel etki alanı HTTPS etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="28b80-151">You can also add custom domain mapping to your CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN depolama cdn yapılandırması][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="28b80-153">4. adım: Erişim CDN içerik</span><span class="sxs-lookup"><span data-stu-id="28b80-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="28b80-154">CDN önbelleğe alınmış içeriğe erişmek için CDN Portal'da sağlanan URL'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="28b80-154">To access cached content on the CDN, use the CDN URL provided in the portal.</span></span> <span data-ttu-id="28b80-155">Önbelleğe alınan bir blob adresi aşağıdakine benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="28b80-155">The address for a cached blob will be similar to the following:</span></span>

<span data-ttu-id="28b80-156">http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="28b80-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="28b80-157">Bir depolama hesabı için CDN erişimi etkinleştirdiğinizde, genel olarak kullanılabilir tüm nesneler CDN uç önbelleğe alma için uygundur.</span><span class="sxs-lookup"><span data-stu-id="28b80-157">Once you enable CDN access to a storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="28b80-158">CDN şu anda önbelleğe alınmış nesneyi değiştirirseniz, yaşam süresi önbelleğe alınan içerik süresi sona erdiğinde, CDN içeriğini yeniler kadar yeni içerik CDN kullanılabilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="28b80-158">If you modify an object that is currently cached in the CDN, the new content will not be available via the CDN until the CDN refreshes its content when the cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-the-cdn"></a><span data-ttu-id="28b80-159">5. adım: içerik CDN Kaldır</span><span class="sxs-lookup"><span data-stu-id="28b80-159">Step 5: Remove content from the CDN</span></span>
<span data-ttu-id="28b80-160">Artık bir nesne içinde Azure içerik teslim ağı (CDN) önbelleğe almak istiyorsanız, aşağıdaki adımlardan birini gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="28b80-160">If you no longer wish to cache an object in the Azure Content Delivery Network (CDN), you can take one of the following steps:</span></span>

* <span data-ttu-id="28b80-161">Kapsayıcı yapabileceğiniz ortak yerine özel.</span><span class="sxs-lookup"><span data-stu-id="28b80-161">You can make the container private instead of public.</span></span> <span data-ttu-id="28b80-162">Daha fazla bilgi için bkz.: [Kapsayıcılar ve bloblar için anonim okuma erişimini yönetme](../storage/blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="28b80-162">See [Manage anonymous read access to containers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="28b80-163">Yönetim Portalı'nı kullanarak CDN uç noktasını silmek ya da devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="28b80-163">You can disable or delete the CDN endpoint using the Management Portal.</span></span>
* <span data-ttu-id="28b80-164">Barındırılan hizmet artık nesne için isteklere yanıt verecek şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28b80-164">You can modify your hosted service to no longer respond to requests for the object.</span></span>

<span data-ttu-id="28b80-165">Bir nesne zaten CDN önbelleğe nesne yaşam süresi boyunca sona erene kadar veya uç nokta temizlenir kadar önbelleğe alınmış olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="28b80-165">An object already cached in the CDN will remain cached until the time-to-live period for the object expires or until the endpoint is purged.</span></span> <span data-ttu-id="28b80-166">Yaşam süresi süresi sona erdiğinde, CDN CDN uç noktası hala geçerli olup olmadığını ve hala anonim olarak erişilebilir nesne görmek için kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="28b80-166">When the time-to-live period expires, the CDN will check to see whether the CDN endpoint is still valid and the object still anonymously accessible.</span></span> <span data-ttu-id="28b80-167">Değilse, ardından nesne artık önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="28b80-167">If it is not, then the object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28b80-168">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="28b80-168">Additional resources</span></span>
* [<span data-ttu-id="28b80-169">CDN İçeriğini Özel Etki Alanı ile Eşleme</span><span class="sxs-lookup"><span data-stu-id="28b80-169">How to Map CDN Content to a Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="28b80-170">Özel etki alanınız için HTTPS'yi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="28b80-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
