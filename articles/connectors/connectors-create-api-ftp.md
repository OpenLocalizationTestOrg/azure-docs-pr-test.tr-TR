---
title: "Logic apps içinde FTP Bağlayıcısı'nı kullanmayı öğrenin | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. Dosyalarınızı yönetmek için FTP sunucusuna bağlanın. Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve FTP sunucusu dosyaları silin."
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 61bfbedfd4f1e84b6976099323a32f3a720634c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-ftp-connector"></a><span data-ttu-id="05e95-105">FTP Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="05e95-105">Get started with the FTP connector</span></span>
<span data-ttu-id="05e95-106">İzleme, yönetme ve FTP sunucusunda bulunan dosyaları oluşturmak için FTP Bağlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="05e95-106">Use the FTP connector to monitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="05e95-107">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="05e95-107">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="05e95-108">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="05e95-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-ftp"></a><span data-ttu-id="05e95-109">FTP Bağlan</span><span class="sxs-lookup"><span data-stu-id="05e95-109">Connect to FTP</span></span>
<span data-ttu-id="05e95-110">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk önce oluşturmanız gerekir bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="05e95-110">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="05e95-111">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="05e95-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-ftp"></a><span data-ttu-id="05e95-112">FTP bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05e95-112">Create a connection to FTP</span></span>
> [!INCLUDE [Steps to create a connection to FTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="05e95-113">FTP tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="05e95-113">Use a FTP trigger</span></span>
<span data-ttu-id="05e95-114">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="05e95-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="05e95-115">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="05e95-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="05e95-116">Internet'ten erişilebilen ve Pasif modu ile çalışmak için yapılandırılmış bir FTP sunucusu FTP Bağlayıcısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="05e95-116">The FTP connector requires an FTP server that  is accessible from the Internet and is configured to operate with PASSIVE mode.</span></span> <span data-ttu-id="05e95-117">Ayrıca, FTP Bağlayıcıdır **örtük FTPS (FTP SSL üzerinden) ile uyumlu değil**.</span><span class="sxs-lookup"><span data-stu-id="05e95-117">Also, the FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="05e95-118">FTP Bağlayıcısı, yalnızca açık FTPS (FTP SSL üzerinden) destekler.</span><span class="sxs-lookup"><span data-stu-id="05e95-118">The FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="05e95-119">Bu örnekte, ı size nasıl kullanılacağını gösterir **bir dosya eklendiğinde veya FTP -** bir dosya için eklendiğinde veya, bir FTP sunucusuna değiştiren bir mantık uygulama iş akışını başlatmak için tetikler.</span><span class="sxs-lookup"><span data-stu-id="05e95-119">In this example, I will show you how to use the **FTP - When a file is added or modified** trigger to initiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="05e95-120">Bir kurumsal örnekte, bu tetikleyici müşterilerden siparişleri temsil eden yeni dosyalar için bir FTP klasörü izlemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05e95-120">In an enterprise example, you could use this trigger to monitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="05e95-121">Bir FTP Bağlayıcısı eylem gibi sonra kullanabilir **alma dosya içeriğini** siparişleri veritabanınızda başka bir işleme ve depolama düzeni içeriğini almak için.</span><span class="sxs-lookup"><span data-stu-id="05e95-121">You could then use an FTP connector action such as **Get file content** to get the contents of the order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="05e95-122">Girin *ftp* arama kutusuna logic apps tasarımcısında seçip **bir dosya eklendiğinde veya FTP -** tetikleyici</span><span class="sxs-lookup"><span data-stu-id="05e95-122">Enter *ftp* in the search box on the logic apps designer then select the **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="05e95-123">![FTP tetikleyici görüntü 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="05e95-124">**Ne zaman bir dosya eklenen veya değiştirilen** denetim açılır</span><span class="sxs-lookup"><span data-stu-id="05e95-124">The **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="05e95-125">![FTP tetikleyici görüntü 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="05e95-126">Seçin **...**  denetimi sağ tarafta bulunur.</span><span class="sxs-lookup"><span data-stu-id="05e95-126">Select the **...** located on the right side of the control.</span></span> <span data-ttu-id="05e95-127">Bu Klasör Seçici denetim açar</span><span class="sxs-lookup"><span data-stu-id="05e95-127">This opens the folder picker control</span></span>  
   <span data-ttu-id="05e95-128">![FTP tetikleyici görüntü 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="05e95-129">Seçin  **>**  (sağ ok) için yeni veya değiştirilmiş dosyaları izlemek istediğiniz klasörü bulmak üzere göz atın.</span><span class="sxs-lookup"><span data-stu-id="05e95-129">Select the **>** (right arrow) and browse to find the folder that you want to monitor for new or modified files.</span></span> <span data-ttu-id="05e95-130">Klasör ve klasör gösterilen artık bildirim seçin **klasörü** denetim.</span><span class="sxs-lookup"><span data-stu-id="05e95-130">Select the folder and notice the folder is now displayed in the **Folder** control.</span></span>  
   <span data-ttu-id="05e95-131">![FTP tetikleyici görüntü 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="05e95-132">Bu noktada, mantıksal uygulamanızı bir dosya değiştiren veya belirli FTP klasörde oluşturulan diğer tetikleyiciler ve Eylemler iş akışı bir farklı çalıştır başlayacak bir tetikleyici ile yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="05e95-132">At this point, your logic app has been configured with a trigger that will begin a run of the other triggers and actions in the workflow when a file is either modified or created in the specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="05e95-133">Bir mantıksal uygulama işlevsel olması en az bir tetikleyici ve bir eylem içermelidir.</span><span class="sxs-lookup"><span data-stu-id="05e95-133">For a logic app to be functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="05e95-134">Bir eylem eklemek için sonraki bölümdeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="05e95-134">Follow the steps in the next section to add an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="05e95-135">Bir FTP eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="05e95-135">Use a FTP action</span></span>
<span data-ttu-id="05e95-136">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="05e95-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="05e95-137">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="05e95-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="05e95-138">Eklediğiniz bir tetikleyici, tetikleyici tarafından bulunan yeni veya değiştirilmiş dosya içeriğini alacak bir eylem eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="05e95-138">Now that you have added a trigger, follow these steps to add an action that will get the contents of the new or modified file found by the trigger.</span></span>    

1. <span data-ttu-id="05e95-139">Seçin **+ yeni adım** eklemek için FTP sunucusunda dosyasının içeriğini almak için eylem</span><span class="sxs-lookup"><span data-stu-id="05e95-139">Select **+ New step** to add the the action to get the contents of the file on the FTP server</span></span>  
2. <span data-ttu-id="05e95-140">Seçin **Eylem Ekle** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="05e95-140">Select the **Add an action** link.</span></span>  
   <span data-ttu-id="05e95-141">![FTP eylem görüntü 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="05e95-142">Girin *FTP* FTP ilgili tüm eylemleri arayın.</span><span class="sxs-lookup"><span data-stu-id="05e95-142">Enter *FTP* to search for all actions related to FTP.</span></span>
4. <span data-ttu-id="05e95-143">Seçin **FTP - Al dosya içeriğini** ne zaman gerçekleştirilecek eylemi yeni veya değiştirilmiş bir dosya FTP klasöründe bulunur.</span><span class="sxs-lookup"><span data-stu-id="05e95-143">Select **FTP - Get file content**  as the action to take when a new or modified file is found in the FTP folder.</span></span>      
   <span data-ttu-id="05e95-144">![FTP eylem görüntü 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="05e95-145">**Alma dosya içeriği** kontrol açar.</span><span class="sxs-lookup"><span data-stu-id="05e95-145">The **Get file content** control opens.</span></span> <span data-ttu-id="05e95-146">**Not**: mantıksal uygulamanızı, bunu daha önceden yapmadıysanız, FTP sunucusu hesabınıza erişmeniz için yetkilendirmek istenir.</span><span class="sxs-lookup"><span data-stu-id="05e95-146">**Note**: you will be prompted to authorize your logic app to access your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="05e95-147">![FTP eylem görüntüsü 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="05e95-148">Seçin **dosya** denetimi (boşluk bulunan aşağıda **dosya***).</span><span class="sxs-lookup"><span data-stu-id="05e95-148">Select the **File** control (the white space located below **FILE***).</span></span> <span data-ttu-id="05e95-149">Burada FTP sunucusunda bulunan yeni veya değiştirilmiş dosyasından çeşitli özelliklerinden herhangi birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05e95-149">Here, you can use any of the various properties from the new or modified file found on the FTP server.</span></span>  
6. <span data-ttu-id="05e95-150">Seçin **dosya içeriği** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="05e95-150">Select the **File content** option.</span></span>  
   <span data-ttu-id="05e95-151">![FTP eylem görüntüsü 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="05e95-152">Gösteren denetimi güncelleştirilir **FTP - Al dosya içeriğini** eylem alırsınız *dosya içeriği* FTP sunucusunda yeni veya değiştirilmiş dosyasının.</span><span class="sxs-lookup"><span data-stu-id="05e95-152">The control is updated, indicating that the **FTP - Get file content** action will get the *file content* of the new or modified file on the FTP server.</span></span>      
   <span data-ttu-id="05e95-153">![FTP eylem görüntüsü 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="05e95-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="05e95-154">Çalışmanızı kaydedin, sonra iş akışınızı test etmek için FTP klasörüne bir dosya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="05e95-154">Save your work then add a file to the FTP folder to test your workflow.</span></span>    

<span data-ttu-id="05e95-155">Bu noktada, mantıksal uygulama, bir FTP sunucusundaki bir klasöre izlemek ve yeni bir dosya veya FTP sunucusunda değiştirilmiş bir dosya bulduğunda, iş akışını başlatmak için bir tetikleyici ile yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="05e95-155">At this point, the logic app has been configured with a trigger to monitor a folder on an FTP server and initiate the workflow when it finds either a new file or a modified file on the FTP server.</span></span> 

<span data-ttu-id="05e95-156">Mantıksal uygulama de yeni veya değiştirilmiş dosyasının içeriğini almak için bir eylem ile yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="05e95-156">The logic app also has been configured with an action to get the contents of the new or modified file.</span></span>

<span data-ttu-id="05e95-157">Başka bir eylem gibi şimdi eklemek [SQL Server - Satır Ekle](connectors-create-api-sqlazure.md) yeni veya değiştirilmiş dosya içeriğini bir SQL veritabanı tablosuna eklemek için eylem.</span><span class="sxs-lookup"><span data-stu-id="05e95-157">You can now add another action such as the [SQL Server - insert row](connectors-create-api-sqlazure.md) action to insert the contents of the new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="05e95-158">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="05e95-158">Connector-specific details</span></span>

<span data-ttu-id="05e95-159">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="05e95-159">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="05e95-160">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="05e95-160">Next Steps</span></span>
[<span data-ttu-id="05e95-161">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="05e95-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

