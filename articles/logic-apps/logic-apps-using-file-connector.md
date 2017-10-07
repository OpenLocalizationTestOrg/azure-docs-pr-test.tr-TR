---
title: "aaaConnect tooon içi dosya Azure Logic Apps sistemlerden | Microsoft Docs"
description: "Mantıksal uygulama akışınızı hello şirket içi veri ağ geçidi ve dosya sistemi bağlayıcısı aracılığıyla tooon içi dosya sistemleri bağlayın"
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
ms.openlocfilehash: beb5565293def4aba81f63f19e77d7498aac38c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-file-systems-from-logic-apps-with-hello-file-system-connector"></a><span data-ttu-id="61381-104">Logic apps hello dosya sistemi bağlayıcı ile tooon içi dosya sistemleri bağlayın</span><span class="sxs-lookup"><span data-stu-id="61381-104">Connect tooon-premises file systems from logic apps with hello File System connector</span></span>

<span data-ttu-id="61381-105">Karma bulut bağlantı merkezi toologic uygulamaların, bunu toomanage verilerini ve güvenli bir şekilde erişim şirket içi kaynakları, mantıksal uygulamalarınızı hello şirket içi veri ağ geçidi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61381-105">Hybrid cloud connectivity is central toologic apps, so toomanage data and securely access on-premises resources, your logic apps can use hello on-premises data gateway.</span></span> <span data-ttu-id="61381-106">Bu makalede, nasıl tooconnect tooan dosya sistemi temel senaryo ile şirket içi gösteriyoruz: Bu karşıya yüklenen tooDropbox tooa dosya paylaşımı, sonra bir e-posta Gönder dosyasını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="61381-106">In this article, we show how tooconnect tooan on-premises file system with a basic scenario: copy a file that's uploaded tooDropbox tooa file share, then send an email.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61381-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="61381-107">Prerequisites</span></span>

- <span data-ttu-id="61381-108">Merhaba son yükleyip [şirket içi veri ağ geçidi](https://www.microsoft.com/download/details.aspx?id=53127).</span><span class="sxs-lookup"><span data-stu-id="61381-108">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127).</span></span>
- <span data-ttu-id="61381-109">Merhaba son şirket içi veri ağ geçidi, sürüm 1.15.6150.1 yüklemek veya üstü.</span><span class="sxs-lookup"><span data-stu-id="61381-109">Install hello latest on-premises data gateway, version 1.15.6150.1 or above.</span></span> <span data-ttu-id="61381-110">[Toohello şirket içi veri ağ geçidi bağlantı](http://aka.ms/logicapps-gateway) hello adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="61381-110">[Connect toohello on-premises data gateway](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="61381-111">Merhaba adımları hello kalanı ile devam etmeden önce bir şirket içi makinede hello ağ geçidi yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="61381-111">hello gateway must be installed on an on-premises machine before you can continue with hello rest of hello steps.</span></span>

## <a name="add-trigger-and-actions-for-connecting-tooyour-file-system"></a><span data-ttu-id="61381-112">Tetikleyici ve tooyour dosya sistemine bağlanmak için Eylemler ekleme</span><span class="sxs-lookup"><span data-stu-id="61381-112">Add trigger and actions for connecting tooyour file system</span></span>

1. <span data-ttu-id="61381-113">Bir mantıksal uygulama oluşturun ve bu Dropbox tetikleyici ekleyin: **bir dosya oluşturulduğunda**</span><span class="sxs-lookup"><span data-stu-id="61381-113">Create a logic app, and add this Dropbox trigger: **When a file is created**</span></span> 
2. <span data-ttu-id="61381-114">Merhaba tetikleyici altında seçin **sonraki adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="61381-114">Under hello trigger, choose **Next Step** > **Add an action**.</span></span> 
3. <span data-ttu-id="61381-115">Merhaba arama kutusuna `file system` hello dosya sistemi Bağlayıcısı için desteklenen tüm eylemler görmesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="61381-115">In hello search box, enter `file system` so you can view all supported actions for hello File System connector.</span></span>

   ![Dosya bağlayıcı arayın](media/logic-apps-using-file-connector/search-file-connector.png)

2. <span data-ttu-id="61381-117">Merhaba seçin **dosyası oluştur** eylemi ve bir bağlantı tooyour dosya sistemi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="61381-117">Choose hello **Create file** action, and create a connection tooyour file system.</span></span>

   <span data-ttu-id="61381-118">Varolan bir bağlantıyı yoksa, istendiğinde toocreate biri demektir.</span><span class="sxs-lookup"><span data-stu-id="61381-118">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="61381-119">Seçin **Connect şirket içi veri ağ geçidi üzerinden**.</span><span class="sxs-lookup"><span data-stu-id="61381-119">Choose **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="61381-120">Daha fazla özellik görünür.</span><span class="sxs-lookup"><span data-stu-id="61381-120">More properties appear.</span></span>
   2. <span data-ttu-id="61381-121">Dosya sistemi için kök klasör seçin.</span><span class="sxs-lookup"><span data-stu-id="61381-121">Select your root folder for your file system.</span></span>
      
       > [!NOTE]
       > <span data-ttu-id="61381-122">Tüm dosya ile ilgili eylemler için göreli yollar için kullanılan hello ana üst klasör Hello kök klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="61381-122">hello root folder is hello main parent folder, which is used for relative paths for all file-related actions.</span></span> <span data-ttu-id="61381-123">Burada hello şirket içi veri ağ geçidi yüklü değil veya hello klasör makine hello bir ağ paylaşımına erişmek için olabilir hello makinede yerel bir klasöre belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61381-123">You can specify a local folder on hello machine where hello on-premises data gateway is installed, or hello folder can be a network share that hello machine can access.</span></span>

   3. <span data-ttu-id="61381-124">Merhaba ağ geçidi için Hello kullanıcı adı ve parola girin.</span><span class="sxs-lookup"><span data-stu-id="61381-124">Enter hello username and password for hello gateway.</span></span>
   4. <span data-ttu-id="61381-125">Daha önce yüklediğiniz hello ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="61381-125">Select hello gateway that you previously installed.</span></span>

       ![Bağlantıyı yapılandırın](media/logic-apps-using-file-connector/create-file.png)

3. <span data-ttu-id="61381-127">Tüm hello ayrıntıları verdikten sonra Seç **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="61381-127">After you provide all hello details, choose **Create**.</span></span> 

   <span data-ttu-id="61381-128">Logic Apps yapılandırır ve hello bağlantı düzgün çalıştığından emin olmayı bağlantınızı test eder.</span><span class="sxs-lookup"><span data-stu-id="61381-128">Logic Apps configures and tests your connection, making sure that hello connection works properly.</span></span> 
   <span data-ttu-id="61381-129">Merhaba bağlantı düzgün şekilde ayarlanıp ayarlanmadığını seçenekler, daha önce seçtiğiniz hello eylemi için bkz.</span><span class="sxs-lookup"><span data-stu-id="61381-129">If hello connection is set up correctly, you see options for hello action that you previously selected.</span></span> 
   <span data-ttu-id="61381-130">Merhaba dosya sistemi bağlayıcı artık kullanıma hazırdır.</span><span class="sxs-lookup"><span data-stu-id="61381-130">hello file system connector is now ready for use.</span></span>

4. <span data-ttu-id="61381-131">Şirket içi dosya paylaşımı için Dropbox toohello kök klasörü toocopy dosyalarından istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="61381-131">Specify that you want toocopy files from Dropbox toohello root folder for your on-premises file share.</span></span>

   ![Dosya eylem oluşturun](media/logic-apps-using-file-connector/create-file-filled.png)

5. <span data-ttu-id="61381-133">Mantıksal uygulama kopyaları hello dosyanıza sonra ilgili kullanıcıların hello yeni dosya hakkında bilmesi bir e-posta gönderen bir Outlook eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="61381-133">After your logic app copies hello file, add an Outlook action that sends an email so relevant users know about hello new file.</span></span> <span data-ttu-id="61381-134">Merhaba alıcılar, başlık ve hello e-posta gövdesini girin.</span><span class="sxs-lookup"><span data-stu-id="61381-134">Enter hello recipients, title, and body of hello email.</span></span> 

   <span data-ttu-id="61381-135">Merhaba dinamik içerik Seçici'de, daha fazla ayrıntı toohello e-posta ekleyebilmek hello dosya Bağlayıcısı'ndan veri çıkışları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="61381-135">In hello dynamic content selector, you can choose data outputs from hello file connector so you can add more details toohello email.</span></span>

   ![E-posta eylemi Gönder](media/logic-apps-using-file-connector/send-email.png)

6. <span data-ttu-id="61381-137">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="61381-137">Save your logic app.</span></span> <span data-ttu-id="61381-138">Bir dosya tooDropbox karşıya yükleyerek uygulamanızı test edin.</span><span class="sxs-lookup"><span data-stu-id="61381-138">Test your app by uploading a file tooDropbox.</span></span> <span data-ttu-id="61381-139">Merhaba dosya kopyalanan toohello şirket içi dosya paylaşımı almanız gerekir ve hello işlemi hakkında bir e-posta almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="61381-139">hello file should get copied toohello on-premises file share, and you should receive an email about hello operation.</span></span>

   > [!TIP] 
   > <span data-ttu-id="61381-140">Nasıl çok öğrenin[mantıksal uygulamalarınızı izleme](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="61381-140">Learn how too[monitor your logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="61381-141">Tebrikler, artık tooyour şirket içi dosya sistemi bağlanabilmesi için bir çalışma mantıksal uygulama vardır.</span><span class="sxs-lookup"><span data-stu-id="61381-141">Congratulations, you now have a working logic app that can connect tooyour on-premises file system.</span></span> <span data-ttu-id="61381-142">Bağlayıcı sunar, örneğin hello diğer işlevleri keşfetme deneyin:</span><span class="sxs-lookup"><span data-stu-id="61381-142">Try exploring other functionalities that hello connector offers, for example:</span></span>

- <span data-ttu-id="61381-143">Dosya Oluştur</span><span class="sxs-lookup"><span data-stu-id="61381-143">Create file</span></span>
- <span data-ttu-id="61381-144">Klasördeki dosyaları listele</span><span class="sxs-lookup"><span data-stu-id="61381-144">List files in folder</span></span>
- <span data-ttu-id="61381-145">Dosya ekleme</span><span class="sxs-lookup"><span data-stu-id="61381-145">Append file</span></span>
- <span data-ttu-id="61381-146">Dosya Sil</span><span class="sxs-lookup"><span data-stu-id="61381-146">Delete file</span></span>
- <span data-ttu-id="61381-147">Dosya içeriğini alma</span><span class="sxs-lookup"><span data-stu-id="61381-147">Get file content</span></span>
- <span data-ttu-id="61381-148">Dosya yolunu kullanarak dosya içeriğini al</span><span class="sxs-lookup"><span data-stu-id="61381-148">Get file content using path</span></span>
- <span data-ttu-id="61381-149">Dosya meta verileri alma</span><span class="sxs-lookup"><span data-stu-id="61381-149">Get file metadata</span></span>
- <span data-ttu-id="61381-150">Dosya yolunu kullanarak dosya meta verilerini al</span><span class="sxs-lookup"><span data-stu-id="61381-150">Get file metadata using path</span></span>
- <span data-ttu-id="61381-151">Kök klasördeki dosyaları listele</span><span class="sxs-lookup"><span data-stu-id="61381-151">List files in root folder</span></span>
- <span data-ttu-id="61381-152">Güncelleştirme dosyası</span><span class="sxs-lookup"><span data-stu-id="61381-152">Update file</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="61381-153">Görünüm hello swagger</span><span class="sxs-lookup"><span data-stu-id="61381-153">View hello swagger</span></span>
<span data-ttu-id="61381-154">Merhaba bkz [ayrıntıları swagger](/connectors/fileconnector/).</span><span class="sxs-lookup"><span data-stu-id="61381-154">See hello [swagger details](/connectors/fileconnector/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="61381-155">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="61381-155">Get help</span></span>

<span data-ttu-id="61381-156">tooask sorular soruları ve hangi diğer Azure mantığı kullanıcılar gittiğini, uygulamaların ziyaret hello öğrenin [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="61381-156">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="61381-157">toohelp Azure mantıksal uygulamaları ve bağlayıcıların geliştirmek, oy veya hello fikir gönderme [Azure Logic Apps kullanıcı geri bildirim sitesi](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="61381-157">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="61381-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="61381-158">Next steps</span></span>

- <span data-ttu-id="61381-159">[Tooon içi veri bağlanmak](../logic-apps/logic-apps-gateway-connection.md) mantığı uygulamalardan</span><span class="sxs-lookup"><span data-stu-id="61381-159">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
- <span data-ttu-id="61381-160">Hakkında bilgi edinin [Kurumsal tümleştirme](../logic-apps/logic-apps-enterprise-integration-overview.md)</span><span class="sxs-lookup"><span data-stu-id="61381-160">Learn about [enterprise integration](../logic-apps/logic-apps-enterprise-integration-overview.md)</span></span>
