---
title: "Azure mantıksal uygulamaları şirket içi dosya sistemlerine bağlanmak | Microsoft Docs"
description: "Şirket içi dosya sistemleri için mantığı uygulama akışınızı şirket içi veri ağ geçidi ve dosya sistemi bağlayıcısı aracılığıyla bağlayın"
keywords: Dosya sistemleri
services: logic-apps
author: derek1ee
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/27/2017
ms.author: LADocs; deli
ms.openlocfilehash: f33e7c58103c57e17e4e273caba1ab9b83f0cd2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-file-systems-from-logic-apps-with-the-file-system-connector"></a><span data-ttu-id="3e2bf-104">Logic apps dosya sistemi bağlayıcı ile şirket içi dosya sistemleri bağlayın</span><span class="sxs-lookup"><span data-stu-id="3e2bf-104">Connect to on-premises file systems from logic apps with the File System connector</span></span>

<span data-ttu-id="3e2bf-105">Karma bulut bağlantı mantıksal uygulamalar için merkezi olduğundan verileri yönetmek ve güvenli bir şekilde şirket içi kaynaklara erişmek için mantıksal uygulamalarınızı şirket içi veri ağ geçidi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-105">Hybrid cloud connectivity is central to logic apps, so to manage data and securely access on-premises resources, your logic apps can use the on-premises data gateway.</span></span> <span data-ttu-id="3e2bf-106">Bu makalede, temel senaryo ile şirket içi dosya sistemine bağlanmak nasıl gösteriyoruz: Dropbox'a dosya paylaşımına yüklendikten sonra bir e-posta Gönder dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-106">In this article, we show how to connect to an on-premises file system with a basic scenario: copy a file that's uploaded to Dropbox to a file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e2bf-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3e2bf-107">Prerequisites</span></span>

- <span data-ttu-id="3e2bf-108">Yükleme ve yapılandırma en son [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="3e2bf-108">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="3e2bf-109">En son şirket içi veri ağ geçidini, sürüm 1.15.6150.1 yükleyin veya üstü.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-109">Install the latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="3e2bf-110">[Şirket içi veri ağ geçidine bağlanmak](http://aka.ms/logicapps-gateway) adımlar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-110">[Connect to the on-premises data gateway](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="3e2bf-111">Ağ geçidi adımları geri kalanı ile devam etmeden önce bir şirket içi makineye yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-111">The gateway must be installed on an on-premises machine before you can continue with the rest of the steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-to-your-file-system"></a><span data-ttu-id="3e2bf-112">Tetikleyici ve dosya sistemine bağlanmak için Eylemler ekleme</span><span class="sxs-lookup"><span data-stu-id="3e2bf-112">Add trigger and actions for connecting to your file system</span></span>

1. <span data-ttu-id="3e2bf-113">Bir mantıksal uygulama oluşturun ve bu Dropbox tetikleyici ekleyin: **bir dosya oluşturulduğunda**</span><span class="sxs-lookup"><span data-stu-id="3e2bf-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="3e2bf-114">Tetikleyici altında seçin **sonraki adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-114">Under the trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="3e2bf-115">Arama kutusuna `file system` dosya sistemi Bağlayıcısı için desteklenen tüm eylemler görmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-115">In the search box, enter `file system` so you can view all supported actions for the File System connector.</span></span>

   ![Dosya bağlayıcı arayın](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="3e2bf-117">Seçin **dosyası oluştur** eylemi ve dosya sisteminizi bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-117">Choose the **Create file** action, and create a connection to your file system.</span></span>

   <span data-ttu-id="3e2bf-118">Varolan bir bağlantıyı sahip değilseniz, birini oluşturmanız istenir.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-118">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="3e2bf-119">Seçin **Connect şirket içi veri ağ geçidi üzerinden**.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="3e2bf-120">Daha fazla özellik görünür.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-120">More properties appear.</span></span>
   2. <span data-ttu-id="3e2bf-121">Dosya sistemi için kök klasör seçin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="3e2bf-122">Tüm dosya ile ilgili eylemler için göreli yollar için kullanılan ana üst klasörü kök klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-122">The root folder is the main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="3e2bf-123">Bir yerel klasör, şirket içi veri ağ geçidi yüklendi veya klasörü makinenin erişebildiği bir ağ paylaşımı olabilir makinede belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-123">You can specify a local folder on the machine where the on-premises data gateway is installed, or the folder can be a network share that the machine can access.</span></span>

   3. <span data-ttu-id="3e2bf-124">Ağ geçidi için kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-124">Enter the username and password for the gateway.</span></span>
   4. <span data-ttu-id="3e2bf-125">Daha önce yüklediğiniz ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-125">Select the gateway that you previously installed.</span></span>

       ![Bağlantıyı yapılandırın](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="3e2bf-127">Tüm Ayrıntılar verdikten sonra Seç **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-127">After you provide all the details, choose **Create**.</span></span> 

   <span data-ttu-id="3e2bf-128">Logic Apps yapılandırır ve bağlantı düzgün çalıştığından emin olmayı bağlantınızı test eder.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-128">Logic Apps configures and tests your connection, making sure that the connection works properly.</span></span> 
   <span data-ttu-id="3e2bf-129">Bağlantısı düzgün şekilde ayarlanıp ayarlanmadığını seçenekler, daha önce seçtiğiniz eylem için bkz.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-129">If the connection is set up correctly, you see options for the action that you previously selected.</span></span> 
   <span data-ttu-id="3e2bf-130">Dosya sistemi Bağlayıcısı'nı şimdi kullanıma hazırdır.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-130">The file system connector is now ready for use.</span></span>

4. <span data-ttu-id="3e2bf-131">Şirket içi dosya paylaşımı için kök klasör Dropbox'tan dosyalarını kopyalamak istediğiniz belirtin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-131">Specify that you want to copy files from Dropbox to the root folder for your on-premises file share.</span></span>

   ![Dosya eylem oluşturun](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="3e2bf-133">Mantıksal uygulamanızı dosyaları kopyaladıktan sonra ilgili kullanıcılar yeni dosya hakkında bilmesi bir e-posta gönderen bir Outlook eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-133">After your logic app copies the file, add an Outlook action that sends an email so relevant users know about the new file.</span></span> <span data-ttu-id="3e2bf-134">Alıcılar, başlık ve e-posta gövdesini girin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-134">Enter the recipients, title, and body of the email.</span></span> 

   <span data-ttu-id="3e2bf-135">Dinamik içerik Seçici içinde daha fazla ayrıntı için e-posta ekleyebilmek dosya Bağlayıcısı'ndan veri çıkışları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-135">In the dynamic content selector, you can choose data outputs from the file connector so you can add more details to the email.</span></span>

   ![E-posta eylemi Gönder](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="3e2bf-137">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-137">Save your logic app.</span></span> <span data-ttu-id="3e2bf-138">Dropbox için bir dosyayı karşıya yükleyerek uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-138">Test your app by uploading a file to Dropbox.</span></span> <span data-ttu-id="3e2bf-139">Dosya şirket içi dosya paylaşımına kopyalanmış ve işlemi hakkında bir e-posta almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-139">The file should get copied to the on-premises file share, and you should receive an email about the operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="3e2bf-140">Bilgi edinmek için nasıl [mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3e2bf-140">Learn how to [monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="3e2bf-141">Tebrikler, artık, şirket içi dosya sistemine bağlanmak bir çalışma mantıksal uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-141">Congratulations, you now have a working logic app that can connect to your on-premises file system.</span></span> <span data-ttu-id="3e2bf-142">Bağlayıcı sunar, örneğin diğer işlevleri keşfetme deneyin:</span><span class="sxs-lookup"><span data-stu-id="3e2bf-142">Try exploring other functionalities that the connector offers, for example:</span></span>

- <span data-ttu-id="3e2bf-143">Dosya Oluştur</span><span class="sxs-lookup"><span data-stu-id="3e2bf-143">Create file</span></span>
- <span data-ttu-id="3e2bf-144">Klasördeki dosyaları listele</span><span class="sxs-lookup"><span data-stu-id="3e2bf-144">List files in folder</span></span>
- <span data-ttu-id="3e2bf-145">Dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="3e2bf-145">Append file</span></span>
- <span data-ttu-id="3e2bf-146">Dosya Sil</span><span class="sxs-lookup"><span data-stu-id="3e2bf-146">Delete file</span></span>
- <span data-ttu-id="3e2bf-147">Dosya içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="3e2bf-147">Get file content</span></span>
- <span data-ttu-id="3e2bf-148">Dosya yolunu kullanarak dosya içeriğini al</span><span class="sxs-lookup"><span data-stu-id="3e2bf-148">Get file content using path</span></span>
- <span data-ttu-id="3e2bf-149">Dosya meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="3e2bf-149">Get file metadata</span></span>
- <span data-ttu-id="3e2bf-150">Dosya yolunu kullanarak dosya meta verilerini al</span><span class="sxs-lookup"><span data-stu-id="3e2bf-150">Get file metadata using path</span></span>
- <span data-ttu-id="3e2bf-151">Kök klasördeki dosyaları listele</span><span class="sxs-lookup"><span data-stu-id="3e2bf-151">List files in root folder</span></span>
- <span data-ttu-id="3e2bf-152">Güncelleştirme dosyası</span><span class="sxs-lookup"><span data-stu-id="3e2bf-152">Update file</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="3e2bf-153">Swagger görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="3e2bf-153">View the swagger</span></span>
<span data-ttu-id="3e2bf-154">Bkz: [ayrıntıları swagger](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="3e2bf-154">See the [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="3e2bf-155">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="3e2bf-155">Get help</span></span>

<span data-ttu-id="3e2bf-156">Sorular sormak, soruları yanıtlamak ve diğer Azure Logic Apps kullanıcılarının neler yaptığını öğrenmek için [Azure Logic Apps forumunu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-156">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="3e2bf-157">Azure Logic Apps ve bağlayıcıları geliştirmeye yardımcı olmak için, [Azure Logic Apps kullanıcı geri bildirim sitesinde](http://aka.ms/logicapps-wish) oy kullanın veya fikirlerinizi paylaşın.</span><span class="sxs-lookup"><span data-stu-id="3e2bf-157">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e2bf-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e2bf-158">Next steps</span></span>

- <span data-ttu-id="3e2bf-159">[Şirket içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan</span><span class="sxs-lookup"><span data-stu-id="3e2bf-159">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="3e2bf-160">Hakkında bilgi edinin [Kurumsal tümleştirme](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="3e2bf-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
