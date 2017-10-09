---
title: "aaaLearn nasıl toouse hello logic apps FTP Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooFTP sunucu toomanage dosyalarınızı bağlayın. Karşıya yükleme gibi çeşitli eylemleri, güncelleştirme, almak ve FTP sunucusu dosyaları silin."
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
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a><span data-ttu-id="d2fd6-105">Merhaba FTP Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d2fd6-105">Get started with hello FTP connector</span></span>
<span data-ttu-id="d2fd6-106">Merhaba FTP Bağlayıcısı toomonitor kullanmak için yönetmek ve bir FTP sunucusu üzerinde dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-106">Use hello FTP connector toomonitor, manage and create files on an  FTP server.</span></span> 

<span data-ttu-id="d2fd6-107">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-107">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="d2fd6-108">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d2fd6-108">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooftp"></a><span data-ttu-id="d2fd6-109">TooFTP Bağlan</span><span class="sxs-lookup"><span data-stu-id="d2fd6-109">Connect tooFTP</span></span>
<span data-ttu-id="d2fd6-110">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-110">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="d2fd6-111">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-111">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-tooftp"></a><span data-ttu-id="d2fd6-112">Bir bağlantı tooFTP oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2fd6-112">Create a connection tooFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a><span data-ttu-id="d2fd6-113">FTP tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="d2fd6-113">Use a FTP trigger</span></span>
<span data-ttu-id="d2fd6-114">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="d2fd6-115">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d2fd6-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="d2fd6-116">Merhaba FTP Bağlayıcısı Internet hello erişilebilir olduğundan ve FTP sunucusuna toooperate Pasif modu ile yapılandırılmış gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-116">hello FTP connector requires an FTP server that  is accessible from hello Internet and is configured toooperate with PASSIVE mode.</span></span> <span data-ttu-id="d2fd6-117">Ayrıca, hello FTP Bağlayıcıdır **örtük FTPS (FTP SSL üzerinden) ile uyumlu değil**.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-117">Also, hello FTP connector is **not compatible with implicit FTPS (FTP over SSL)**.</span></span> <span data-ttu-id="d2fd6-118">Merhaba FTP Bağlayıcısı, yalnızca açık FTPS (FTP SSL üzerinden) destekler.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-118">hello FTP connector only supports explicit FTPS (FTP over SSL).</span></span>  
> 
> 

<span data-ttu-id="d2fd6-119">Bu örnekte, ı bunu nasıl yapacağınızı gösterir toouse hello **bir dosya eklendiğinde veya FTP -** bir dosya için eklendiğinde veya, bir FTP sunucusuna değiştirildiğinde tooinitiate mantığı uygulama iş akışı tetikler.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-119">In this example, I will show you how toouse hello **FTP - When a file is added or modified** trigger tooinitiate a logic app workflow when a file is added to, or modified on, an FTP server.</span></span> <span data-ttu-id="d2fd6-120">Bir kurumsal örnekte müşterilerden siparişleri temsil eden yeni dosyalar için Bu tetikleyici toomonitor FTP klasörü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-120">In an enterprise example, you could use this trigger toomonitor an FTP folder for new files that represent orders from customers.</span></span>  <span data-ttu-id="d2fd6-121">Bir FTP Bağlayıcısı eylem gibi sonra kullanabilir **dosya içeriğini almak** tooget hello içeriği başka bir işleme ve depolama siparişleri veritabanınızdaki hello düzeni.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-121">You could then use an FTP connector action such as **Get file content** tooget hello contents of hello order for further processing and storage in your orders database.</span></span>

1. <span data-ttu-id="d2fd6-122">Girin *ftp* hello arama kutusuna hello logic apps tasarımcısında hello seçip **bir dosya eklendiğinde veya FTP -** tetikleyici</span><span class="sxs-lookup"><span data-stu-id="d2fd6-122">Enter *ftp* in hello search box on hello logic apps designer then select hello **FTP - When a file is added or modified**  trigger</span></span>   
   <span data-ttu-id="d2fd6-123">![FTP tetikleyici görüntü 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-123">![FTP trigger image 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)</span></span>  
   <span data-ttu-id="d2fd6-124">Merhaba **ne zaman bir dosya eklenen veya değiştirilen** denetim açılır</span><span class="sxs-lookup"><span data-stu-id="d2fd6-124">hello **When a file is added or modified** control opens up</span></span>  
   <span data-ttu-id="d2fd6-125">![FTP tetikleyici görüntü 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-125">![FTP trigger image 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)</span></span>  
2. <span data-ttu-id="d2fd6-126">Select hello **...**  hello sağ tarafında hello denetim bulunur.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-126">Select hello **...** located on hello right side of hello control.</span></span> <span data-ttu-id="d2fd6-127">Bu hello Klasör Seçici denetim açar</span><span class="sxs-lookup"><span data-stu-id="d2fd6-127">This opens hello folder picker control</span></span>  
   <span data-ttu-id="d2fd6-128">![FTP tetikleyici görüntü 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-128">![FTP trigger image 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)</span></span>  
3. <span data-ttu-id="d2fd6-129">Select hello  **>**  (sağ ok) ve yeni veya değiştirilmiş dosyaları için toomonitor istediğiniz toofind hello klasöre göz atın.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-129">Select hello **>** (right arrow) and browse toofind hello folder that you want toomonitor for new or modified files.</span></span> <span data-ttu-id="d2fd6-130">Merhaba klasörü seçin ve başlangıç klasörü hello şimdi görüntülenen fark **klasörü** denetim.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-130">Select hello folder and notice hello folder is now displayed in hello **Folder** control.</span></span>  
   <span data-ttu-id="d2fd6-131">![FTP tetikleyici görüntü 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-131">![FTP trigger image 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)</span></span>   

<span data-ttu-id="d2fd6-132">Bu noktada, mantıksal uygulamanızı bir dosya değiştiren veya hello belirli FTP klasörde oluşturulan yükleyen hello yürütülmesi diğer tetikleyiciler ve Eylemler hello iş akışında başlayacak bir tetikleyici ile yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-132">At this point, your logic app has been configured with a trigger that will begin a run of hello other triggers and actions in hello workflow when a file is either modified or created in hello specific FTP folder.</span></span> 

> [!NOTE]
> <span data-ttu-id="d2fd6-133">Bir mantıksal uygulama toobe için işlev, en az bir tetikleyici ve bir eylem içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-133">For a logic app toobe functional, it must contain at least one trigger and one action.</span></span> <span data-ttu-id="d2fd6-134">Merhaba sonraki bölümde tooadd eylemin Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-134">Follow hello steps in hello next section tooadd an action.</span></span>  
> 
> 

## <a name="use-a-ftp-action"></a><span data-ttu-id="d2fd6-135">Bir FTP eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="d2fd6-135">Use a FTP action</span></span>
<span data-ttu-id="d2fd6-136">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d2fd6-137">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d2fd6-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="d2fd6-138">Bir tetikleyici eklediğiniz, bu adımları tooadd hello tetik tarafından bulunan hello yeni veya değiştirilmiş dosya hello içeriğini alacak bir eylem izleyin.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-138">Now that you have added a trigger, follow these steps tooadd an action that will get hello contents of hello new or modified file found by hello trigger.</span></span>    

1. <span data-ttu-id="d2fd6-139">Seçin **+ yeni adım** tooadd hello hello eylem tooget hello hello dosyasının içeriğini hello FTP sunucusunda</span><span class="sxs-lookup"><span data-stu-id="d2fd6-139">Select **+ New step** tooadd hello hello action tooget hello contents of hello file on hello FTP server</span></span>  
2. <span data-ttu-id="d2fd6-140">Select hello **Eylem Ekle** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-140">Select hello **Add an action** link.</span></span>  
   <span data-ttu-id="d2fd6-141">![FTP eylem görüntü 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-141">![FTP action image 1](./media/connectors-create-api-ftp/ftp-action-1.png)</span></span>  
3. <span data-ttu-id="d2fd6-142">Girin *FTP* toosearch tüm eylemler için ilgili tooFTP.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-142">Enter *FTP* toosearch for all actions related tooFTP.</span></span>
4. <span data-ttu-id="d2fd6-143">Seçin **FTP - Al dosya içeriğini** hello FTP klasöründe yeni veya değiştirilmiş bir dosya bulunduğunda eylem tootake hello gibi.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-143">Select **FTP - Get file content**  as hello action tootake when a new or modified file is found in hello FTP folder.</span></span>      
   <span data-ttu-id="d2fd6-144">![FTP eylem görüntü 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-144">![FTP action image 2](./media/connectors-create-api-ftp/ftp-action-2.png)</span></span>  
   <span data-ttu-id="d2fd6-145">Merhaba **alma dosya içeriği** kontrol açar.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-145">hello **Get file content** control opens.</span></span> <span data-ttu-id="d2fd6-146">**Not**:, istendiğinde tooauthorize FTP sunucunuza hesabını, daha önce yapmadıysanız, logic app tooaccess olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-146">**Note**: you will be prompted tooauthorize your logic app tooaccess your FTP server account if you have not done so previously.</span></span>  
   <span data-ttu-id="d2fd6-147">![FTP eylem görüntüsü 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-147">![FTP action image 3](./media/connectors-create-api-ftp/ftp-action-3.png)</span></span>   
5. <span data-ttu-id="d2fd6-148">Select hello **dosya** denetimi (Merhaba boşluk bulunan aşağıda **dosya***).</span><span class="sxs-lookup"><span data-stu-id="d2fd6-148">Select hello **File** control (hello white space located below **FILE***).</span></span> <span data-ttu-id="d2fd6-149">Burada, herhangi bir hello çeşitli özellikleri dosyasından hello FTP sunucusunda bulunan hello yeni veya değiştirilmiş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-149">Here, you can use any of hello various properties from hello new or modified file found on hello FTP server.</span></span>  
6. <span data-ttu-id="d2fd6-150">Select hello **dosya içeriği** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-150">Select hello **File content** option.</span></span>  
   <span data-ttu-id="d2fd6-151">![FTP eylem görüntüsü 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-151">![FTP action image 4](./media/connectors-create-api-ftp/ftp-action-4.png)</span></span>   
7. <span data-ttu-id="d2fd6-152">Merhaba denetim güncelleştirilir, o hello belirten **FTP - Al dosya içeriğini** eylemin hello alırsınız *dosya içeriği* hello yeni veya değiştirilmiş dosyasının hello FTP sunucusundaki.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-152">hello control is updated, indicating that hello **FTP - Get file content** action will get hello *file content* of hello new or modified file on hello FTP server.</span></span>      
   <span data-ttu-id="d2fd6-153">![FTP eylem görüntüsü 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span><span class="sxs-lookup"><span data-stu-id="d2fd6-153">![FTP action image 5](./media/connectors-create-api-ftp/ftp-action-5.png)</span></span>     
8. <span data-ttu-id="d2fd6-154">Çalışmanızı kaydedin, sonra iş akışınızı bir dosya toohello FTP klasörü tootest ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-154">Save your work then add a file toohello FTP folder tootest your workflow.</span></span>    

<span data-ttu-id="d2fd6-155">Bu noktada, hello mantıksal uygulama boyunca yeni bir dosya veya değiştirilmiş bir dosya hello FTP sunucusunda bulduğunda bir tetikleyici toomonitor ile bir klasör bir FTP sunucusu ve başlatma hello iş akışı yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-155">At this point, hello logic app has been configured with a trigger toomonitor a folder on an FTP server and initiate hello workflow when it finds either a new file or a modified file on hello FTP server.</span></span> 

<span data-ttu-id="d2fd6-156">Merhaba mantıksal uygulama aynı zamanda bir eylem tooget hello hello yeni veya değiştirilmiş dosyasının içeriğiyle yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-156">hello logic app also has been configured with an action tooget hello contents of hello new or modified file.</span></span>

<span data-ttu-id="d2fd6-157">Hello gibi başka bir eylem artık ekleyebilirsiniz [SQL Server - Satır Ekle](connectors-create-api-sqlazure.md) eylem tooinsert hello hello yeni veya değiştirilmiş dosyasına SQL veritabanı tablosunda içeriğini.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-157">You can now add another action such as hello [SQL Server - insert row](connectors-create-api-sqlazure.md) action tooinsert hello contents of hello new or modified file into a SQL database table.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="d2fd6-158">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d2fd6-158">Connector-specific details</span></span>

<span data-ttu-id="d2fd6-159">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/ftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="d2fd6-159">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/ftpconnector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d2fd6-160">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d2fd6-160">Next Steps</span></span>
[<span data-ttu-id="d2fd6-161">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2fd6-161">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

