---
title: "Aspera kullanarak Azure Media Services hesabına dosya yükleme | Microsoft Docs"
description: "Bu öğreticide, bir Media Services hesabı kullanarak ilişkili bir depolama hesabı içine dosya karşıya yükleme adımları açıklanmaktadır ** Aspera sunucu üzerinde isteğe bağlı ** Azure hizmeti."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: e3090da9b2c5b8f99545a1f7f9601bfd8d5221f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="b72af-103">Azure üzerinde Aspera Server On Demand hizmetini kullanan bir Media Services hesabına dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="b72af-103">Upload files into a Media Services account using the Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="b72af-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b72af-104">Overview</span></span>

<span data-ttu-id="b72af-105">**Aspera** çok yüksek hızlı bir dosya aktarım yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="b72af-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="b72af-106">Azure için **Aspera Server On Demand**, büyük dosyaların doğrudan Azure Blob nesne depolama alanına yüksek hızda yüklenmesini ve indirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="b72af-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="b72af-107">**İsteğe Bağlı Aspera** hakkında bilgi için [Aspera Bulut](http://cloud.asperasoft.com/) sitesine bakın.</span><span class="sxs-lookup"><span data-stu-id="b72af-107">For information about **Aspera On Demand**, see the [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="b72af-108">Azure için **Aspera Server On Demand**, [Azure Market](https://azure.microsoft.com/en-us/marketplace/)’ten satın alınabilir.</span><span class="sxs-lookup"><span data-stu-id="b72af-108">**Aspera Server On Demand** for Azure is available for purchase from the [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="b72af-109">**Aspera Server On Demand** satın alma işlemini tamamlamak için lütfen Azure Market’te Windows Live ID’nizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b72af-109">In order to complete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="b72af-110">Bu öğreticide, Azure üzerinde **Aspera Server On Demand** hizmetini kullanarak bir Media Services hesabıyla ilişkili depolama hesabına dosya yükleme adımları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b72af-110">This tutorial walks you through the steps of uploading files into a storage account that is associated with a Media Services account using the **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="b72af-111">Azure işlevlerinin Aspera ve Media Services ile kullanımını gösteren bir örneği [burada](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest) bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72af-111">You can find an example that shows how to use Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="b72af-112">Azure Media Services medya işlemcileri (MP’ler) ile işleme için desteklenen dosya boyutlarına yönelik üst sınır uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b72af-112">There is a limit to the maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="b72af-113">Dosya boyutu sınırlaması hakkında ayrıntılı bilgi için lütfen [bu konu başlığını](media-services-quotas-and-limitations.md) inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b72af-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about the file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="b72af-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b72af-114">Prerequisites</span></span> 

<span data-ttu-id="b72af-115">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="b72af-115">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="b72af-116">Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="b72af-116">A Windows Live ID</span></span>
* <span data-ttu-id="b72af-117">Bir [Azure hesabı](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="b72af-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="b72af-118">Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b72af-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="b72af-119">Bir [Azure Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="b72af-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="b72af-120">Azure için İsteğe Bağlı Aspera yazılımını satın alın</span><span class="sxs-lookup"><span data-stu-id="b72af-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="b72af-121">Azure için İsteğe Bağlı Azure satın alma işlemini tamamlamak için Azure Market’te oturum açtıktan sonra aşağıdaki basit adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b72af-121">Once you have logged into Azure Marketplace,  follow these basic steps to complete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="b72af-122">Aspera ifadesini arayın ve 'Server On Demand' öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b72af-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="b72af-124">Abonelik planlarını gözden geçirin ve 'Kaydol' öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="b72af-124">Review the subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="b72af-126">İsteğe Bağlı Sunucu aboneliğinize ilişkin ayrıntıları doldurun.</span><span class="sxs-lookup"><span data-stu-id="b72af-126">Fill in the specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="b72af-128">**Fiyatlandırma Katmanı**’na tıklayın ve alt panelden istediğiniz aylık hacmi seçin.</span><span class="sxs-lookup"><span data-stu-id="b72af-128">Click on the **Pricing Tier** and select your desired monthly volume in the sub panel.</span></span> <span data-ttu-id="b72af-129">**Plan ayrıntıları** panelinde **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b72af-129">In the **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="b72af-130">Ardından **Fiyatlandırma Katmanınızı seçin** panelinde **Seç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b72af-130">Then, in the **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="b72af-132">Alt panelde yasal koşulları görüntüleyip kabul etmek için **Yasal koşullar** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b72af-132">Click on **Legal terms** to view and accept the legal terms in the sub panel.</span></span> <span data-ttu-id="b72af-133">Yasal koşulları gözden geçirdikten sonra **Satın al**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b72af-133">Once you have reviewed the legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="b72af-135">**Oluştur**’a tıklayarak satın alma işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b72af-135">Complete the purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="b72af-137">Azure panosu bu hizmeti sağladığını duyurur.</span><span class="sxs-lookup"><span data-stu-id="b72af-137">The Azure dashboard will announce that it is provisioning the service.</span></span>  <span data-ttu-id="b72af-138">Sağlama ile işlem tamamlandıktan sonra kaynaklarınızda hizmetin adını arayarak yeni aboneliği bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72af-138">Once it is completed with provisioning, you can find the new subscription by searching in your resources for the name of the service.</span></span> <span data-ttu-id="b72af-139">Hizmeti bulduktan sonra çift tıklayarak hizmet yönetim portalını başlatın.</span><span class="sxs-lookup"><span data-stu-id="b72af-139">Once you have found the service, double click on it to launch the service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="b72af-141">Aspera yönetim portalını başlatın.</span><span class="sxs-lookup"><span data-stu-id="b72af-141">Launch the Aspera management portal.</span></span> <span data-ttu-id="b72af-142">Yeni Aspera hizmetinizi bulduktan sonra hizmete tıklayarak yönetim portalına erişim elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72af-142">Once you have found your new Aspera service, you can gain access to the management portal, by clicking on the service.</span></span>  <span data-ttu-id="b72af-143">Yeni bir panel başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b72af-143">A new panel will be launched.</span></span> <span data-ttu-id="b72af-144">Bu yeni panelden yeni hizmetinizin **Kaynak Adı** seçeneğine tıklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b72af-144">From within that new panel, you need to click on the **Resource Name** of your new service.</span></span>  <span data-ttu-id="b72af-145">Aşağıdaki ekran görüntüsünde kaynak adı 'AsperaTransferDemo' şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="b72af-145">In the following screenshot, the resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="b72af-146">Kaynak adına tıkladığınızda başka bir panel başlatılır.</span><span class="sxs-lookup"><span data-stu-id="b72af-146">Once you click on the resource name, another panel is launched.</span></span> <span data-ttu-id="b72af-147">Yeni başlatılan bu panelde bir 'Yönet' bağlantısı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b72af-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="b72af-148">Aspera yönetim portalını başlatmak için 'Yönet' bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b72af-148">Click on the 'Manage' link to launch the Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="b72af-150">Yönet bağlantısına tıkladığınızda, hizmete erişmek için gerekli olan kayıt sayfasına ulaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="b72af-150">By clicking on the manage link, you will get to the registration page, which is required to access the service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="b72af-152">Bu noktada, erişim anahtarları oluşturabileceğiniz, Aspera istemci ve lisanslarını indirebileceğiniz, kullanımı görüntüleyebileceğiniz ve API’ler hakkında bilgi alabileceğiniz Aspera hizmet yönetim portalına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b72af-152">At this point, you should have access to the Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about the APIs.</span></span>

    <span data-ttu-id="b72af-153">Aşağıdaki ekran görüntüsünde erişim oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b72af-153">The following screenshot shows the access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="b72af-155">Aşağıdaki ekran görüntüsünde, portaldaki kullanım raporlama arabirimleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b72af-155">The following screenshot shows the usage reporting interfaces in the portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="b72af-157">Aspera ile dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="b72af-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="b72af-158">Aspera istemci yazılımını indirip yükleyin:</span><span class="sxs-lookup"><span data-stu-id="b72af-158">Download and install the Aspera client software:</span></span>
    
    * [<span data-ttu-id="b72af-159">Tarayıcı eklentisi</span><span class="sxs-lookup"><span data-stu-id="b72af-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="b72af-160">Zengin istemci</span><span class="sxs-lookup"><span data-stu-id="b72af-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="b72af-161">İlk aktarımınızı yapın.</span><span class="sxs-lookup"><span data-stu-id="b72af-161">Make your first transfer.</span></span> <span data-ttu-id="b72af-162">Aspera istemcisini kullanarak Aspera aktarım hizmetiyle aktarım yapmak için aşağıdaki işlemleri tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b72af-162">In order to use the Aspera client to transfer with the Aspera transfer service, you need to complete the following:</span></span> 

    1. <span data-ttu-id="b72af-163">Aspera portalını kullanarak bir erişim anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b72af-163">Create an access key, using the Aspera portal.</span></span>  
    2. <span data-ttu-id="b72af-164">Aspera istemcisini indirin, yükleyin ve lisans ekleyin (yazılım Aspera portalında bulunabilir).</span><span class="sxs-lookup"><span data-stu-id="b72af-164">Download, install, and license the Aspera client (software can be found in the Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="b72af-165">Yapılandırma bilgileri için lütfen Aspera istemci kılavuzunu okuyun.</span><span class="sxs-lookup"><span data-stu-id="b72af-165">Please read the Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="b72af-166">[Azure portalı](https://portal.azure.com/) kullanarak Azure Medya Hesabınız ile ilişkili depolama hesabınızın bazı bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="b72af-166">Retrieve some information of your storage account that is associated with your Azure Media Account using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="b72af-167">Almanız gereken bilgiler şunlardır: ad, anahtar ve içeriğinizi yerleştirmek istediğiniz depolama blobu kapsayıcısının adı.</span><span class="sxs-lookup"><span data-stu-id="b72af-167">Specifically, name and key, and the storage blob container name in to which you want to place your content.</span></span> 

        * <span data-ttu-id="b72af-168">Portaldan depolama bilgilerini almak için: Depolama hesabınızı bulun, Erişim anahtarları’na tıklayın ve hesabınızın adı ile anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b72af-168">To get the storage info from the portal: find your storage account, click on the Access keys and copy the name and the key of your account.</span></span>
        * <span data-ttu-id="b72af-169">Kapsayıcı adını almak için: Depolama hesabınızı bulun, **Bloblar**’ı ve sonra da içerik bilgisini yüklemek istediğiniz kapsayıcının adını seçin.</span><span class="sxs-lookup"><span data-stu-id="b72af-169">To get the container name: find your storage account, select **Blobs**, select the name of the container you want to upload the content into.</span></span> 

    <span data-ttu-id="b72af-170">Aşağıdaki ekran görüntüsünde, 'Azure' depolama türünü, kimlik bilgilerini ve blob kapsayıcısını belirtmeniz gereken Aspera istemcisi **Bağlantı Yöneticisi** gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b72af-170">Below is the screenshot of the Aspera client **Connection Manager** where you must specify the 'Azure' storage type and credentials as well as the blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="b72af-172">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="b72af-172">Resources</span></span>

<span data-ttu-id="b72af-173">Bu makalede aşağıdaki kaynaklardan bahsedilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b72af-173">The following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="b72af-174">Connect Tarayıcı Eklentisi</span><span class="sxs-lookup"><span data-stu-id="b72af-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="b72af-175">Connect Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="b72af-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="b72af-176">Aspera İstemcisi</span><span class="sxs-lookup"><span data-stu-id="b72af-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="b72af-177">İstemci Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="b72af-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="b72af-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b72af-178">Next steps</span></span>

<span data-ttu-id="b72af-179">Artık, [bir depolama hesabından AMS hesabına blob kopyalayabilirsiniz](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="b72af-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="b72af-180">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="b72af-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b72af-181">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="b72af-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

