---
title: "bir Azure depolama hesabı Azure CDN ile aaaIntegrate | Microsoft Docs"
description: "Önbelleğe alma tarafından toouse hello Azure içerik teslim ağı (CDN) toodeliver yüksek bant genişliği içeriği Azure Storage'dan nasıl BLOB'öğrenin."
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
ms.openlocfilehash: e44716969d6a784265cc4b1da34f0d021a17b38d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-an-azure-storage-account-with-azure-cdn"></a><span data-ttu-id="43f08-103">Azure storage hesabı Azure CDN ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="43f08-103">Integrate an Azure storage account with Azure CDN</span></span>
<span data-ttu-id="43f08-104">CDN etkin toocache Azure depolama hesabınızdan içerik olabilir.</span><span class="sxs-lookup"><span data-stu-id="43f08-104">CDN can be enabled toocache content from your Azure storage.</span></span> <span data-ttu-id="43f08-105">Geliştiriciler BLOB'ları ve işlem örnekleri hello ABD, Avrupa, Asya, Avustralya ve Güney Amerika fiziksel düğümlerde, statik içeriği önbelleğe alarak yüksek bant genişliği içeriği teslimi için genel bir çözüm sunar.</span><span class="sxs-lookup"><span data-stu-id="43f08-105">It offers developers a global solution for delivering high-bandwidth content by caching blobs and static content of compute instances at physical nodes in hello United States, Europe, Asia, Australia and South America.</span></span>

## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="43f08-106">1. adım: depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="43f08-106">Step 1: Create a storage account</span></span>
<span data-ttu-id="43f08-107">Aşağıdaki yordam toocreate bir Azure aboneliği için yeni bir depolama hesabı hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="43f08-107">Use hello following procedure toocreate a new storage account for a Azure subscription.</span></span> <span data-ttu-id="43f08-108">Bir depolama hesabı için Azure storage hizmetlerine erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="43f08-108">A storage account gives access to Azure storage services.</span></span> <span data-ttu-id="43f08-109">Merhaba depolama hesabı hello ad'hello Azure depolama hizmeti bileşenlerinin her biri erişmek için en yüksek düzeyde hello temsil eder: Blob Hizmetleri, kuyruk Hizmetleri ve Tablo Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="43f08-109">hello storage account represents hello highest level of hello namespace for accessing each of hello Azure storage service components: Blob services, Queue services, and Table services.</span></span> <span data-ttu-id="43f08-110">Daha fazla bilgi için toohello başvuran [giriş tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="43f08-110">For more information, refer toohello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span>

<span data-ttu-id="43f08-111">toocreate bir depolama hesabı, hello Hizmet Yöneticisi veya bir ortak yönetici için ilişkili hello olmalıdır abonelik.</span><span class="sxs-lookup"><span data-stu-id="43f08-111">toocreate a storage account, you must be either hello service administrator or a co-administrator for hello associated subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="43f08-112">Toocreate hello Azure Portal ve Powershell dahil olmak üzere bir depolama hesabı kullanabileceğiniz çeşitli yöntemler vardır.</span><span class="sxs-lookup"><span data-stu-id="43f08-112">There are several methods you can use toocreate a storage account, including hello Azure Portal and Powershell.</span></span>  <span data-ttu-id="43f08-113">Bu öğreticide, biz hello Azure Portal kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="43f08-113">For this tutorial, we'll be using hello Azure Portal.</span></span>  
> 
> 

<span data-ttu-id="43f08-114">**toocreate bir Azure aboneliği için bir depolama hesabı**</span><span class="sxs-lookup"><span data-stu-id="43f08-114">**toocreate a storage account for an Azure subscription**</span></span>

1. <span data-ttu-id="43f08-115">İçinde toohello oturum [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="43f08-115">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="43f08-116">Merhaba sol üst köşedeki, seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="43f08-116">In hello upper left corner, select **New**.</span></span> <span data-ttu-id="43f08-117">Merhaba, **yeni** iletişim kutusunda **veri + depolama**, ardından **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="43f08-117">In hello **New** Dialog, select **Data  + Storage**, then click **Storage account**.</span></span>
    
    <span data-ttu-id="43f08-118">Merhaba **depolama hesabı oluşturma** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="43f08-118">hello **Create storage account** blade appears.</span></span>   

    ![Depolama hesabı oluşturma][create-new-storage-account]  

3. <span data-ttu-id="43f08-120">Merhaba, **adı** alanında, bir alt etki alanı adı yazın.</span><span class="sxs-lookup"><span data-stu-id="43f08-120">In hello **Name** field, type a subdomain name.</span></span> <span data-ttu-id="43f08-121">Bu giriş, 3-24 küçük harfler ve sayılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="43f08-121">This entry can contain 3-24 lowercase letters and numbers.</span></span>
   
    <span data-ttu-id="43f08-122">Bu değer hello hello hello aboneliği için Blob, kuyruk veya tablo kaynak adres için kullanılan URI içindeki konak adına dönüşür.</span><span class="sxs-lookup"><span data-stu-id="43f08-122">This value becomes hello host name within hello URI that is used to address Blob, Queue, or Table resources for hello subscription.</span></span> <span data-ttu-id="43f08-123">Hello Blob hizmeti kapsayıcı kaynak adres için bir URI biçimi, aşağıdaki hello kullanırsınız nerede  *&lt;StorageAccountLabel&gt;*  yazmış toohello değeri başvuruyor **birURLgirin**:</span><span class="sxs-lookup"><span data-stu-id="43f08-123">To address a container resource in hello Blob service, you would use a URI in hello following format, where *&lt;StorageAccountLabel&gt;* refers toohello value you typed in **Enter a URL**:</span></span>
   
    <span data-ttu-id="43f08-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span><span class="sxs-lookup"><span data-stu-id="43f08-124">http://*&lt;StorageAcountLabel&gt;*.blob.core.windows.net/*&lt;mycontainer&gt;*</span></span>
   
    <span data-ttu-id="43f08-125">**Önemli:** URL etiketi forms hello alt hello depolama hesabının URI hello ve azure'da barındırılan tüm hizmetler arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="43f08-125">**Important:** hello URL label forms hello subdomain of hello storage  account URI and must be unique among all hosted services in  Azure.</span></span>
   
    <span data-ttu-id="43f08-126">Bu değer, ayrıca bu hesabı program aracılığıyla erişirken hello Portalı'nda veya bu depolama hesabını hello adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43f08-126">This value is also used as hello name of this storage account in hello portal, or when accessing this account programmatically.</span></span>
4. <span data-ttu-id="43f08-127">Merhaba Varsayılanları bırakabilir **dağıtım modeli**, **tür hesap**, **performans**, ve **çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="43f08-127">Leave hello defaults for **Deployment model**, **Account kind**, **Performance**, and **Replication**.</span></span> 
5. <span data-ttu-id="43f08-128">Select hello **abonelik** hello depolama hesabı ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="43f08-128">Select hello **Subscription** that hello storage account will be used with.</span></span>
6. <span data-ttu-id="43f08-129">Bir **Kaynak Grubu** seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="43f08-129">Select or create a **Resource Group**.</span></span>  <span data-ttu-id="43f08-130">Kaynak Grupları hakkında daha fazla bilgi için bkz. [Azure Resource Manager’a genel bakış](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="43f08-130">For more information on Resource Groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
7. <span data-ttu-id="43f08-131">Depolama hesabınız için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="43f08-131">Select a location for your storage account.</span></span>
8. <span data-ttu-id="43f08-132">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43f08-132">Click **Create**.</span></span> <span data-ttu-id="43f08-133">Merhaba hello depolama hesabı oluşturma işlemi birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="43f08-133">hello process of creating hello storage account might take several minutes toocomplete.</span></span>

## <a name="step-2-enable-cdn-for-hello-storage-account"></a><span data-ttu-id="43f08-134">2. adım: Hello depolama hesabı için CDN etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="43f08-134">Step 2: Enable CDN for hello storage account</span></span>

<span data-ttu-id="43f08-135">Merhaba yeni tümleştirmesi ile artık CDN depolama hesabınız için depolama portal uzantınızı ayrılmadan etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43f08-135">With hello newest integration, you can now enable CDN for your storage account without leaving your storage portal extension.</span></span> 

1. <span data-ttu-id="43f08-136">Merhaba depolama hesabını seçin, aşağı "CDN" ya da kaydırma hello sol gezinti menüsünde arayın, ardından "Azure CDN"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="43f08-136">Select hello storage account, search "CDN" or scroll down from hello left navigation menu, then click "Azure CDN".</span></span>
    
    <span data-ttu-id="43f08-137">Merhaba **Azure CDN** dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="43f08-137">hello **Azure CDN** blade appears.</span></span>

    ![CDN etkinleştir gezinme][cdn-enable-navigation]
    
2. <span data-ttu-id="43f08-139">Merhaba gerekli bilgileri girerek yeni bir uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="43f08-139">Create a new endpoint by entering hello required information</span></span>
    - <span data-ttu-id="43f08-140">**CDN profili**: yeni oluşturun veya varolan bir profili kullanın.</span><span class="sxs-lookup"><span data-stu-id="43f08-140">**CDN Profile**: You can create a new or use an existing profile.</span></span>
    - <span data-ttu-id="43f08-141">**Fiyatlandırma katmanı**: yalnızca bir fiyatlandırma katmanı yeni bir CDN profili oluşturursanız, tooselect gerekir.</span><span class="sxs-lookup"><span data-stu-id="43f08-141">**Pricing tier**: You only need tooselect a pricing tier if you create a new CDN profile.</span></span>
    - <span data-ttu-id="43f08-142">**CDN uç nokta adı**: tercih ettiğiniz her bir uç nokta adı girin.</span><span class="sxs-lookup"><span data-stu-id="43f08-142">**CDN endpoint name**: Enter an endpoint name per your choice.</span></span>

    > [!TIP]
    > <span data-ttu-id="43f08-143">oluşturulan hello CDN uç noktası hello ana bilgisayar depolama hesabınızın adını varsayılan olarak kaynak kullanır.</span><span class="sxs-lookup"><span data-stu-id="43f08-143">hello created CDN endpoint uses hello hostname of your storage account as origin by default.</span></span>

    <span data-ttu-id="43f08-144">! [cdn yeni uç nokta oluşturma] [cdn yeni-endpoint-oluşturma]</span><span class="sxs-lookup"><span data-stu-id="43f08-144">![cdn new endpoint creation][cdn-new-endpoint-creation]</span></span>

3. <span data-ttu-id="43f08-145">Oluşturulduktan sonra hello yeni uç nokta yukarıdaki hello uç nokta listesinde görünecektir.</span><span class="sxs-lookup"><span data-stu-id="43f08-145">After creation, hello new endpoint will show up in hello endpoint list above.</span></span>

    ![CDN depolama yeni uç noktası][cdn-storage-new-endpoint]

> [!NOTE]
> <span data-ttu-id="43f08-147">TooAzure CDN uzantısı tooenable CDN de gidebilirsiniz. [Öğreticisi](#Tutorial-cdn-create-profile).</span><span class="sxs-lookup"><span data-stu-id="43f08-147">You can also go tooAzure CDN extension tooenable CDN.[Tutorial](#Tutorial-cdn-create-profile).</span></span>
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]  

## <a name="step-3-enable-additional-cdn-features"></a><span data-ttu-id="43f08-148">3. adım: ek CDN özellikleri etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="43f08-148">Step 3: Enable additional CDN features</span></span>

<span data-ttu-id="43f08-149">Depolama hesabı "Azure CDN" dikey penceresinden hello listesi tooopen CDN yapılandırma dikey penceresinden hello CDN uç'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="43f08-149">From storage account "Azure CDN" blade, click hello CDN endpoint from hello list tooopen CDN configuration blade.</span></span> <span data-ttu-id="43f08-150">Sıkıştırma ve sorgu dizesi gibi teslimat için ek CDN özellikleri etkinleştirebilirsiniz coğrafi filtreleme.</span><span class="sxs-lookup"><span data-stu-id="43f08-150">You can enable additional CDN features for your delivery, such as compression, query string, geo filtering.</span></span> <span data-ttu-id="43f08-151">Ayrıca, özel etki alanı eşleme tooyour CDN uç noktası ekleyin ve özel etki alanı HTTPS etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="43f08-151">You can also add custom domain mapping tooyour CDN endpoint and enable custom domain HTTPS.</span></span>
    
![CDN depolama cdn yapılandırması][cdn-storage-cdn-configuration]

## <a name="step-4-access-cdn-content"></a><span data-ttu-id="43f08-153">4. adım: Erişim CDN içerik</span><span class="sxs-lookup"><span data-stu-id="43f08-153">Step 4: Access CDN content</span></span>
<span data-ttu-id="43f08-154">tooaccess CDN Merhaba içeriğine önbelleğe alınmış, kullanım hello CDN URL'sine hello Portalı'nda sağlanan.</span><span class="sxs-lookup"><span data-stu-id="43f08-154">tooaccess cached content on hello CDN, use hello CDN URL provided in hello portal.</span></span> <span data-ttu-id="43f08-155">önbelleğe alınan bir blob için başlangıç adresi benzer toohello şu olacaktır:</span><span class="sxs-lookup"><span data-stu-id="43f08-155">hello address for a cached blob will be similar toohello following:</span></span>

<span data-ttu-id="43f08-156">http://<*EndpointName*\>.azureedge.net/ <*myPublicContainer*\>/<*BlobName*\></span><span class="sxs-lookup"><span data-stu-id="43f08-156">http://<*EndpointName*\>.azureedge.net/<*myPublicContainer*\>/<*BlobName*\></span></span>

> [!NOTE]
> <span data-ttu-id="43f08-157">CDN erişim tooa depolama hesabı için etkinleştirdiğinizde, genel olarak kullanılabilir tüm nesneler CDN uç önbelleğe alma için uygundur.</span><span class="sxs-lookup"><span data-stu-id="43f08-157">Once you enable CDN access tooa storage account, all publicly available objects are eligible for CDN edge caching.</span></span> <span data-ttu-id="43f08-158">Merhaba CDN şu anda önbelleğe alınmış nesneyi değiştirirseniz, önbelleğe alınmış hello içerik yaşam süresi süresi sona erdiğinde hello CDN içeriğini yeniler kadar hello yeni içerik CDN hello kullanılabilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="43f08-158">If you modify an object that is currently cached in hello CDN, hello new content will not be available via hello CDN until hello CDN refreshes its content when hello cached content time-to-live period expires.</span></span>
> 
> 

## <a name="step-5-remove-content-from-hello-cdn"></a><span data-ttu-id="43f08-159">5. adım: içerik CDN hello Kaldır</span><span class="sxs-lookup"><span data-stu-id="43f08-159">Step 5: Remove content from hello CDN</span></span>
<span data-ttu-id="43f08-160">Artık toocache bir nesne hello Azure içerik teslim ağı (CDN) isterseniz, aşağıdaki adımları hello birini gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="43f08-160">If you no longer wish toocache an object in hello Azure Content Delivery Network (CDN), you can take one of hello following steps:</span></span>

* <span data-ttu-id="43f08-161">Kapsayıcı özel ortak yerine hello yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43f08-161">You can make hello container private instead of public.</span></span> <span data-ttu-id="43f08-162">Bkz: [anonim okuma erişimini toocontainers ve BLOB'ları yönetmek](../storage/blobs/storage-manage-access-to-resources.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="43f08-162">See [Manage anonymous read access toocontainers and blobs](../storage/blobs/storage-manage-access-to-resources.md) for more information.</span></span>
* <span data-ttu-id="43f08-163">Devre dışı bırakmak veya hello CDN uç noktası hello yönetim portalını kullanarak silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43f08-163">You can disable or delete hello CDN endpoint using hello Management Portal.</span></span>
* <span data-ttu-id="43f08-164">Barındırılan hizmet toono uzun yanıt toorequests hello nesnesi için değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43f08-164">You can modify your hosted service toono longer respond toorequests for hello object.</span></span>

<span data-ttu-id="43f08-165">Zaten hello CDN önbelleğe alınmış nesneyi hello nesne için hello yaşam süresi süresi sona erene kadar veya hello endpoint temizlenir kadar önbelleğe alınmış olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="43f08-165">An object already cached in hello CDN will remain cached until hello time-to-live period for hello object expires or until hello endpoint is purged.</span></span> <span data-ttu-id="43f08-166">Merhaba yaşam süresi süresi sona erdiğinde, hello CDN hello CDN uç noktası hala geçerli olup olmadığını ve hello nesne hala anonim olarak erişilebilir toosee kontrol eder.</span><span class="sxs-lookup"><span data-stu-id="43f08-166">When hello time-to-live period expires, hello CDN will check toosee whether hello CDN endpoint is still valid and hello object still anonymously accessible.</span></span> <span data-ttu-id="43f08-167">Değilse, ardından hello nesne artık önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="43f08-167">If it is not, then hello object will no longer be cached.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="43f08-168">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="43f08-168">Additional resources</span></span>
* [<span data-ttu-id="43f08-169">Nasıl tooMap CDN içerik tooa özel etki alanı</span><span class="sxs-lookup"><span data-stu-id="43f08-169">How tooMap CDN Content tooa Custom Domain</span></span>](cdn-map-content-to-custom-domain.md)
* [<span data-ttu-id="43f08-170">Özel etki alanınız için HTTPS'yi etkinleştir</span><span class="sxs-lookup"><span data-stu-id="43f08-170">Enable HTTPS for your custom domain</span></span>](cdn-custom-ssl.md)

[create-new-storage-account]: ./media/cdn-create-a-storage-account-with-cdn/CDN_CreateNewStorageAcct.png
[cdn-enable-navigation]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-creation.png
[cdn-storage-new-endpoint]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-new-endpoint-list.png
[cdn-storage-cdn-configuration]: ./media/cdn-create-a-storage-account-with-cdn/cdn-storage-endpoint-configuration.png 
