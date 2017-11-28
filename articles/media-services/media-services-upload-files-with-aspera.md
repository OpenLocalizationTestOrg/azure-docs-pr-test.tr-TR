---
title: "Aspera kullanarak Azure Media Services hesabı aaaUpload dosyalarıyla | Microsoft Docs"
description: "Bu öğretici, hello kullanarak Media Services hesabı ile ilişkili bir depolama hesabı içine dosyaları karşıya hello adım adım anlatılmaktadır ** Aspera sunucu üzerinde isteğe bağlı ** Azure hizmeti."
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
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a><span data-ttu-id="d0126-103">Azure'da hello Aspera sunucu isteğe bağlı hizmet kullanarak bir Media Services hesabı içine dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d0126-103">Upload files into a Media Services account using hello Aspera Server On Demand service on Azure</span></span>

## <a name="overview"></a><span data-ttu-id="d0126-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d0126-104">Overview</span></span>

<span data-ttu-id="d0126-105">**Aspera** çok yüksek hızlı bir dosya aktarım yazılımıdır.</span><span class="sxs-lookup"><span data-stu-id="d0126-105">**Aspera** is a high-speed file transfer software.</span></span> <span data-ttu-id="d0126-106">Azure için **Aspera Server On Demand**, büyük dosyaların doğrudan Azure Blob nesne depolama alanına yüksek hızda yüklenmesini ve indirilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0126-106">**Aspera Server On Demand** for Azure enables high-speed upload and download of large files directly into Azure Blob object storage.</span></span> <span data-ttu-id="d0126-107">Hakkında bilgi için **isteğe bağlı Aspera**, hello bkz [Aspera bulut](http://cloud.asperasoft.com/) site.</span><span class="sxs-lookup"><span data-stu-id="d0126-107">For information about **Aspera On Demand**, see hello [Aspera Cloud](http://cloud.asperasoft.com/) site.</span></span> 
  
<span data-ttu-id="d0126-108">**İsteğe bağlı Aspera sunucu** hello satınalma için Azure kullanılabilir [Azure Market](https://azure.microsoft.com/en-us/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="d0126-108">**Aspera Server On Demand** for Azure is available for purchase from hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/).</span></span> <span data-ttu-id="d0126-109">İçinde bir satın toocomplete sipariş **Aspera sunucu isteğe bağlı** Azure için lütfen Azure Marketi Windows Live ID'niz ile oturum açın</span><span class="sxs-lookup"><span data-stu-id="d0126-109">In order toocomplete a purchase of **Aspera Server On Demand** for Azure, please log into Azure Marketplace with your Windows Live ID.</span></span>

<span data-ttu-id="d0126-110">Bu öğretici, hello kullanarak Media Services hesabı ile ilişkili bir depolama hesabı içine dosyaları karşıya hello adım adım anlatılmaktadır **Aspera sunucu isteğe bağlı** Azure üzerinde hizmet.</span><span class="sxs-lookup"><span data-stu-id="d0126-110">This tutorial walks you through hello steps of uploading files into a storage account that is associated with a Media Services account using hello **Aspera Server On Demand** service on Azure.</span></span> 

<span data-ttu-id="d0126-111">Toouse Azure Aspera ve Media Services ile nasıl çalıştığını gösteren bir örnek bulabilirsiniz [burada](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span><span class="sxs-lookup"><span data-stu-id="d0126-111">You can find an example that shows how toouse Azure functions with Aspera and Media Services [here](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).</span></span>

>[!NOTE]
><span data-ttu-id="d0126-112">Azure Media Services ile medya işlemcileri (Mp'leri) işlemek için desteklenen bir toohello en büyük dosya boyutu sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="d0126-112">There is a limit toohello maximum file size supported for processing with Azure Media Services media processors (MPs).</span></span> <span data-ttu-id="d0126-113">Lütfen bakın [bu](media-services-quotas-and-limitations.md) hello dosya boyutu sınırlaması hakkında ayrıntılı bilgi için konu.</span><span class="sxs-lookup"><span data-stu-id="d0126-113">Please see [this](media-services-quotas-and-limitations.md) topic for details about hello file size limitation.</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="d0126-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d0126-114">Prerequisites</span></span> 

<span data-ttu-id="d0126-115">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0126-115">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="d0126-116">Windows Live ID</span><span class="sxs-lookup"><span data-stu-id="d0126-116">A Windows Live ID</span></span>
* <span data-ttu-id="d0126-117">Bir [Azure hesabı](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="d0126-117">An [Azure account](https://azure.microsoft.com).</span></span> <span data-ttu-id="d0126-118">Ayrıntılar için bkz. [Azure Ücretsiz Deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0126-118">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
* <span data-ttu-id="d0126-119">Bir [Azure Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d0126-119">An [Azure Media Services account](media-services-portal-create-account.md).</span></span>

## <a name="purchase-aspera-on-demand-for-azure"></a><span data-ttu-id="d0126-120">Azure için İsteğe Bağlı Aspera yazılımını satın alın</span><span class="sxs-lookup"><span data-stu-id="d0126-120">Purchase Aspera On Demand for Azure</span></span>

<span data-ttu-id="d0126-121">Azure Market oturum açtıktan sonra bu temel adımları toocomplete Aspera istendiğinde Azure satın alma işleminiz izleyin.</span><span class="sxs-lookup"><span data-stu-id="d0126-121">Once you have logged into Azure Marketplace,  follow these basic steps toocomplete your purchase of Aspera On Demand for Azure.</span></span>

1. <span data-ttu-id="d0126-122">Aspera ifadesini arayın ve 'Server On Demand' öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="d0126-122">Search for Aspera and select 'Server On Demand'.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. <span data-ttu-id="d0126-124">Merhaba abonelik planları gözden geçirin ve ' oturum üzerinde ' düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="d0126-124">Review hello subscription plans and click on 'Sign Up'</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. <span data-ttu-id="d0126-126">İsteğe bağlı abonelik sunucunuzda hello ayrıntıları doldurun.</span><span class="sxs-lookup"><span data-stu-id="d0126-126">Fill in hello specifics for your Server on Demand subscription.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. <span data-ttu-id="d0126-128">Tıklatın hello üzerinde **fiyatlandırma katmanı** ve istenen aylık biriminiz hello alt panelinde seçin.</span><span class="sxs-lookup"><span data-stu-id="d0126-128">Click on hello **Pricing Tier** and select your desired monthly volume in hello sub panel.</span></span> <span data-ttu-id="d0126-129">Merhaba, **planlama ayrıntıları** paneli, select **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="d0126-129">In hello **Plan details** panel, select **OK**.</span></span> <span data-ttu-id="d0126-130">Ardından hello **fiyatlandırma Katmanınızı seçin** öğesine tıklayın **seçin**.</span><span class="sxs-lookup"><span data-stu-id="d0126-130">Then, in hello **Choose your Pricing Tier** panel, click **Select**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. <span data-ttu-id="d0126-132">Tıklayın **yasal koşulları** tooview ve hello alt panelinde hello yasal koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="d0126-132">Click on **Legal terms** tooview and accept hello legal terms in hello sub panel.</span></span> <span data-ttu-id="d0126-133">Merhaba yasal koşulları gözden geçirdikten sonra tıklayın **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="d0126-133">Once you have reviewed hello legal terms, click **Purchase**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. <span data-ttu-id="d0126-135">Tamamlamak hello satın alma tıklayarak **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="d0126-135">Complete hello purchase by clicking **Create**.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. <span data-ttu-id="d0126-137">Hello Azure Pano hello hizmet sağlama, Duyurusu.</span><span class="sxs-lookup"><span data-stu-id="d0126-137">hello Azure dashboard will announce that it is provisioning hello service.</span></span>  <span data-ttu-id="d0126-138">Sağlamada tamamlandıktan sonra hello yeni abonelik kaynaklarınız hello hizmetin hello adı için arayarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0126-138">Once it is completed with provisioning, you can find hello new subscription by searching in your resources for hello name of hello service.</span></span> <span data-ttu-id="d0126-139">Merhaba hizmeti, çift tıklayarak toolaunch hello Hizmet Yönetim Portalı bulduktan sonra.</span><span class="sxs-lookup"><span data-stu-id="d0126-139">Once you have found hello service, double click on it toolaunch hello service management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. <span data-ttu-id="d0126-141">Merhaba Aspera Yönetim Portalı'nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="d0126-141">Launch hello Aspera management portal.</span></span> <span data-ttu-id="d0126-142">Yeni Aspera hizmetinizi bulduktan sonra hello hizmette tıklayarak erişim toohello Yönetim Portalı, kaynaklara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="d0126-142">Once you have found your new Aspera service, you can gain access toohello management portal, by clicking on hello service.</span></span>  <span data-ttu-id="d0126-143">Yeni bir panel başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d0126-143">A new panel will be launched.</span></span> <span data-ttu-id="d0126-144">Bu yeni paneli, hello üzerinde tooclick gereken **kaynak adı** yeni hizmetinizin.</span><span class="sxs-lookup"><span data-stu-id="d0126-144">From within that new panel, you need tooclick on hello **Resource Name** of your new service.</span></span>  <span data-ttu-id="d0126-145">Aşağıdaki ekran görüntüsü hello 'AsperaTransferDemo' hello kaynak adıdır.</span><span class="sxs-lookup"><span data-stu-id="d0126-145">In hello following screenshot, hello resource name is 'AsperaTransferDemo'.</span></span> <span data-ttu-id="d0126-146">Merhaba kaynak adına tıkladığınızda, başka bir panel başlatılır.</span><span class="sxs-lookup"><span data-stu-id="d0126-146">Once you click on hello resource name, another panel is launched.</span></span> <span data-ttu-id="d0126-147">Yeni başlatılan bu panelde bir 'Yönet' bağlantısı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d0126-147">In that newly launched panel, you will see a 'Manage' link.</span></span> <span data-ttu-id="d0126-148">Merhaba üzerinde 'Yönet' bağlantı toolaunch hello Aspera Yönetim Portalı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d0126-148">Click on hello 'Manage' link toolaunch hello Aspera management portal.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. <span data-ttu-id="d0126-150">Merhaba üzerinde tıklatarak bağlantı yönetmek için gerekli toohello kayıt sayfası alırsınız tooaccess hello hizmet.</span><span class="sxs-lookup"><span data-stu-id="d0126-150">By clicking on hello manage link, you will get toohello registration page, which is required tooaccess hello service.</span></span>

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. <span data-ttu-id="d0126-152">Bu noktada, burada erişim tuşları oluşturma, Aspera istemcileri ve lisansları yükleyin, kullanım görüntüleyebilir ve API hello hakkında bilgi edinin erişim toohello Aspera Hizmet Yönetim Portalı, olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0126-152">At this point, you should have access toohello Aspera service management portal, where you can create access keys, download Aspera clients and licenses, view usage and learn about hello APIs.</span></span>

    <span data-ttu-id="d0126-153">Merhaba aşağıdaki ekran görüntüsü hello erişim oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0126-153">hello following screenshot shows hello access creation.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    <span data-ttu-id="d0126-155">Merhaba aşağıdaki ekran görüntüsünde hello portal arabirimlerde raporlama hello kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0126-155">hello following screenshot shows hello usage reporting interfaces in hello portal.</span></span> 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a><span data-ttu-id="d0126-157">Aspera ile dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="d0126-157">Upload files with Aspera</span></span>

1. <span data-ttu-id="d0126-158">Karşıdan yükle ve hello Aspera istemci yazılımı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="d0126-158">Download and install hello Aspera client software:</span></span>
    
    * [<span data-ttu-id="d0126-159">Tarayıcı eklentisi</span><span class="sxs-lookup"><span data-stu-id="d0126-159">Browser plugin</span></span>](http://downloads.asperasoft.com/connect2/)
    * [<span data-ttu-id="d0126-160">Zengin istemci</span><span class="sxs-lookup"><span data-stu-id="d0126-160">Rich client</span></span>](http://downloads.asperasoft.com/en/downloads/2)

2. <span data-ttu-id="d0126-161">İlk aktarımınızı yapın.</span><span class="sxs-lookup"><span data-stu-id="d0126-161">Make your first transfer.</span></span> <span data-ttu-id="d0126-162">Merhaba Aspera Aktarım Hizmeti ile sipariş toouse hello Aspera istemci tootransfer içinde toocomplete hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="d0126-162">In order toouse hello Aspera client tootransfer with hello Aspera transfer service, you need toocomplete hello following:</span></span> 

    1. <span data-ttu-id="d0126-163">Merhaba Aspera portalı kullanarak bir erişim anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0126-163">Create an access key, using hello Aspera portal.</span></span>  
    2. <span data-ttu-id="d0126-164">İndirme, yükleme ve lisans hello Aspera istemci (yazılım hello Aspera Portalı'nda bulunabilir).</span><span class="sxs-lookup"><span data-stu-id="d0126-164">Download, install, and license hello Aspera client (software can be found in hello Aspera portal).</span></span>  

    >[!NOTE]
    ><span data-ttu-id="d0126-165">Merhaba Aspera istemci Kılavuzu yapılandırma bilgileri okuyun.</span><span class="sxs-lookup"><span data-stu-id="d0126-165">Please read hello Aspera client guide for configuration information.</span></span>
    
    3. <span data-ttu-id="d0126-166">Azure Media hello kullanarak hesabınızla ilişkilendirilen depolama hesabınızın bazı bilgiler almak [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d0126-166">Retrieve some information of your storage account that is associated with your Azure Media Account using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d0126-167">Özellikle, adı ve anahtar ve hello depolama blob kapsayıcı adı toowhich içinde içeriğinizi tooplace istiyor.</span><span class="sxs-lookup"><span data-stu-id="d0126-167">Specifically, name and key, and hello storage blob container name in toowhich you want tooplace your content.</span></span> 

        * <span data-ttu-id="d0126-168">tooget hello depolama bilgisi hello portalından: depolama hesabınız, hello erişim tuşları ve hesabınızın kopyalama hello adı ve hello anahtar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d0126-168">tooget hello storage info from hello portal: find your storage account, click on hello Access keys and copy hello name and hello key of your account.</span></span>
        * <span data-ttu-id="d0126-169">tooget hello kapsayıcı adı: seçin, depolama hesabını bulmak **BLOB'lar**seçin hello kapsayıcısının içine tooupload hello içerik istediğiniz hello adı.</span><span class="sxs-lookup"><span data-stu-id="d0126-169">tooget hello container name: find your storage account, select **Blobs**, select hello name of hello container you want tooupload hello content into.</span></span> 

    <span data-ttu-id="d0126-170">Merhaba ekran görüntüsü hello Aspera istemci aşağıdadır **Bağlantı Yöneticisi** burada belirtmelisiniz hello blob kapsayıcısı yanı sıra hello 'Azure' depolama türünü ve kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d0126-170">Below is hello screenshot of hello Aspera client **Connection Manager** where you must specify hello 'Azure' storage type and credentials as well as hello blob container.</span></span>

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a><span data-ttu-id="d0126-172">Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d0126-172">Resources</span></span>

<span data-ttu-id="d0126-173">Merhaba kaynakları izleyerek, bu makalede bahsedilen.</span><span class="sxs-lookup"><span data-stu-id="d0126-173">hello following resources were mentioned in this article.</span></span> 

* [<span data-ttu-id="d0126-174">Connect Tarayıcı Eklentisi</span><span class="sxs-lookup"><span data-stu-id="d0126-174">Connect Browser Plugin</span></span>](http://downloads.asperasoft.com/connect2/)
* [<span data-ttu-id="d0126-175">Connect Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d0126-175">Connect Guide</span></span>](http://downloads.asperasoft.com/en/documentation/8)
* [<span data-ttu-id="d0126-176">Aspera İstemcisi</span><span class="sxs-lookup"><span data-stu-id="d0126-176">Aspera Client</span></span>](http://downloads.asperasoft.com/en/downloads/2)
* [<span data-ttu-id="d0126-177">İstemci Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d0126-177">Client Guide</span></span>](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a><span data-ttu-id="d0126-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0126-178">Next steps</span></span>

<span data-ttu-id="d0126-179">Artık, [bir depolama hesabından AMS hesabına blob kopyalayabilirsiniz](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span><span class="sxs-lookup"><span data-stu-id="d0126-179">You can now [copy blobs from a storage account into an AMS account ](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="d0126-180">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="d0126-180">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d0126-181">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="d0126-181">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

