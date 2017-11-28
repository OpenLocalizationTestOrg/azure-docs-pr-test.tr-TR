---
title: "Azure Data Lake araçları: U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama | Microsoft Docs"
description: "Nasıl toouse Azure Data Lake araçları Visual Studio Code toolocal çalıştırma ve yerel için hata ayıklama öğrenin."
Keywords: "VScode, Azure Data Lake araçları, yerel çalıştırma, yerel hata ayıklama, yerel hata ayıklama, Önizleme depolama dosyası toostorage yolu karşıya yükle"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: DJ
editor: jejiang
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: fb152f07fe8c4b03dde8fb8e62c7475eccda0578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-local-run-and-local-debug-with-visual-studio-code"></a><span data-ttu-id="568ed-104">U-SQL yerel çalıştırma ve Visual Studio Code ile yerel hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="568ed-104">U-SQL local run and local debug with Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="568ed-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="568ed-105">Prerequisites</span></span>
<span data-ttu-id="568ed-106">Merhaba bu yordamlara başlamadan önce aşağıdaki önkoşulların yerinde olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="568ed-106">Make sure you have hello following prerequisites in place before you start these procedures:</span></span>
- <span data-ttu-id="568ed-107">Visual Studio Code için Azure Data Lake aracı.</span><span class="sxs-lookup"><span data-stu-id="568ed-107">Azure Data Lake Tool for Visual Studio Code.</span></span> <span data-ttu-id="568ed-108">Yönergeler için bkz: [kullanım Azure Data Lake araçları Visual Studio Code için](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="568ed-108">For instructions, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="568ed-109">C# Visual Studio (tooperform U-SQL yerel hata ayıklama istiyorsanız) kodu.</span><span class="sxs-lookup"><span data-stu-id="568ed-109">C# for Visual Studio Code (if you want tooperform a U-SQL local debug).</span></span>

   ![C# Data Lake araçları Visual Studio için yükleme kodu](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-install-ms-vscodecsharp.png)
   
   > [!NOTE]
   > <span data-ttu-id="568ed-111">U-SQL yerel çalıştırma hello ve hata ayıklama özelliklerini şu anda yalnızca Windows kullanıcıları destekler.</span><span class="sxs-lookup"><span data-stu-id="568ed-111">hello U-SQL local run and debug features currently only support Windows users.</span></span> 


## <a name="set-up-hello-u-sql-local-run-environment"></a><span data-ttu-id="568ed-112">Merhaba U-SQL yerel çalıştırma ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="568ed-112">Set up hello U-SQL local run environment</span></span>

1. <span data-ttu-id="568ed-113">Ctrl + Shift + P tooopen hello komutu palet seçin ve ardından girin **ADL: LocalRun bağımlılık indirme** toodownload hello paketler.</span><span class="sxs-lookup"><span data-stu-id="568ed-113">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Download LocalRun Dependency** toodownload hello packages.</span></span>  

   ![Merhaba ADL LocalRun bağımlılık paketlerini yükleyin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/DownloadLocalRun.png)

2. <span data-ttu-id="568ed-115">Merhaba bağımlılık paketlerini hello gösterilen hello yolundan bulun **çıkış** bölmesinde ve sonra BuildTools ve Win10SDK 10240 yükleyin.</span><span class="sxs-lookup"><span data-stu-id="568ed-115">Locate hello dependency packages from hello path shown in hello **Output** pane, and then install BuildTools and Win10SDK 10240.</span></span> <span data-ttu-id="568ed-116">Bir örnek yolu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="568ed-116">Here is an example path:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency
`  
  <span data-ttu-id="568ed-117">![Merhaba bağımlılık paketlerini bulun](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span><span class="sxs-lookup"><span data-stu-id="568ed-117">![Locate hello dependency packages](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/LocateDependencyPath.png)</span></span>

   <span data-ttu-id="568ed-118">a.</span><span class="sxs-lookup"><span data-stu-id="568ed-118">a.</span></span> <span data-ttu-id="568ed-119">tooinstall BuildTools, hello sihirbazdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="568ed-119">tooinstall BuildTools, follow hello wizard instructions.</span></span>   

  ![BuildTools yükleyin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallBuildTools.png)

   <span data-ttu-id="568ed-121">b.</span><span class="sxs-lookup"><span data-stu-id="568ed-121">b.</span></span> <span data-ttu-id="568ed-122">tooinstall Win10SDK 10240 hello sihirbazdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="568ed-122">tooinstall Win10SDK 10240, follow hello wizard instructions.</span></span>  

  ![Win10SDK yükleme 10240](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/InstallWin10SDK.png)

3. <span data-ttu-id="568ed-124">Merhaba ortam değişkeni ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="568ed-124">Set up hello environment variable.</span></span> <span data-ttu-id="568ed-125">Set hello **SCOPE_CPP_SDK** ortam değişkenine:</span><span class="sxs-lookup"><span data-stu-id="568ed-125">Set hello **SCOPE_CPP_SDK** environment variable to:</span></span>  
`C:\Users\xxx\.vscode\extensions\usqlextpublisher.usql-vscode-ext-x.x.x\LocalRunDependency\CppSDK_3rdparty
`  
4. <span data-ttu-id="568ed-126">Merhaba OS toomake hello ortam değişkeni ayarlarının etkili emin yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="568ed-126">Restart hello OS toomake sure that hello environment variable settings take effect.</span></span>  

   ![Merhaba SCOPE_CPP_SDK ortam değişkeni yüklendiğinden emin olun](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/ConfigScopeCppSDk.png)

## <a name="start-hello-local-run-service-and-submit-hello-u-sql-job-tooa-local-account"></a><span data-ttu-id="568ed-128">Merhaba yerel çalıştırma hizmetini başlatın ve hello U-SQL iş tooa yerel hesap gönderme</span><span class="sxs-lookup"><span data-stu-id="568ed-128">Start hello local run service and submit hello U-SQL job tooa local account</span></span> 
<span data-ttu-id="568ed-129">Merhaba ilk kez kullanıcı için olduğunuz istendiğinde toodownload hello ADL: LocalRun bağımlılık indirme paketler zaten yüklü değilse.</span><span class="sxs-lookup"><span data-stu-id="568ed-129">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
1. <span data-ttu-id="568ed-130">Ctrl + Shift + P tooopen hello komutu palet seçin ve ardından girin **ADL: yerel çalıştırma Hizmeti'ni Başlat**.</span><span class="sxs-lookup"><span data-stu-id="568ed-130">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span>
2. <span data-ttu-id="568ed-131">Seçin **kabul** tooaccept hello hello ilk kez için Microsoft Yazılımı Lisans koşulları.</span><span class="sxs-lookup"><span data-stu-id="568ed-131">Select **Accept** tooaccept hello Microsoft Software License Terms for hello first time.</span></span> 

   ![Merhaba Microsoft Yazılımı Lisans koşulları kabul edin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/AcceptEULA.png)   
3. <span data-ttu-id="568ed-133">Başlangıç cmd konsolu açılır.</span><span class="sxs-lookup"><span data-stu-id="568ed-133">hello cmd console opens.</span></span> <span data-ttu-id="568ed-134">İlk kez kullanıcılar için ihtiyacınız tooenter **3**ve verilerinizi giriş ve çıkış hello yerel klasör yolunu bulun.</span><span class="sxs-lookup"><span data-stu-id="568ed-134">For first-time users, you need tooenter **3**, and then locate hello local folder path for your data input and output.</span></span> <span data-ttu-id="568ed-135">Diğer seçenekler için hello varsayılan değerleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="568ed-135">For other options, you can use hello default values.</span></span> 

   ![Visual Studio Code yerel çalıştırma cmd için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-cmd.png)
4. <span data-ttu-id="568ed-137">Ctrl + Shift + P tooopen hello komutu palet seçip girin **ADL: işi Gönder**ve ardından **yerel** toosubmit hello iş tooyour yerel hesap.</span><span class="sxs-lookup"><span data-stu-id="568ed-137">Select Ctrl+Shift+P tooopen hello command palette, enter **ADL: Submit Job**, and then select **Local** toosubmit hello job tooyour local account.</span></span>

   ![Visual Studio Code için Data Lake araçları yerel seçin](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-select-local.png)
5. <span data-ttu-id="568ed-139">Merhaba işi gönderdikten sonra hello gönderme ayrıntıları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="568ed-139">After you submit hello job, you can view hello submission details.</span></span> <span data-ttu-id="568ed-140">tooview hello gönderimi Seç ayrıntıları **jobUrl** hello içinde **çıkış** penceresi.</span><span class="sxs-lookup"><span data-stu-id="568ed-140">tooview hello submission details select **jobUrl** in hello **Output** window.</span></span> <span data-ttu-id="568ed-141">Başlangıç cmd konsolundan hello iş gönderme durumunu da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="568ed-141">You can also view hello job submission status from hello cmd console.</span></span> <span data-ttu-id="568ed-142">Girin **7** tooknow istiyorsanız başlangıç cmd konsolunda daha fazla proje ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="568ed-142">Enter **7** in hello cmd console if you want tooknow more job details.</span></span>

   <span data-ttu-id="568ed-143">![Data Lake araçları için Visual Studio Code yerel çıkış çalıştırma](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
   ![Data Lake araçları Visual Studio Code yerel cmd durumunu çalıştırmak için](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span><span class="sxs-lookup"><span data-stu-id="568ed-143">![Data Lake Tools for Visual Studio Code local run output](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-run-result.png)
![Data Lake Tools for Visual Studio Code local run cmd status](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-localrun-cmd-status.png)</span></span> 


## <a name="start-a-local-debug-for-hello-u-sql-job"></a><span data-ttu-id="568ed-144">Yerel bir hata ayıklama hello U-SQL işi Başlat</span><span class="sxs-lookup"><span data-stu-id="568ed-144">Start a local debug for hello U-SQL job</span></span>  
<span data-ttu-id="568ed-145">Merhaba ilk kez kullanıcı için olduğunuz istendiğinde toodownload hello ADL: LocalRun bağımlılık indirme paketler zaten yüklü değilse.</span><span class="sxs-lookup"><span data-stu-id="568ed-145">For hello first-time user, you are prompted toodownload hello ADL: Download LocalRun Dependency packages if they are not already installed.</span></span>
  
1. <span data-ttu-id="568ed-146">Ctrl + Shift + P tooopen hello komutu palet seçin ve ardından girin **ADL: yerel çalıştırma Hizmeti'ni Başlat**.</span><span class="sxs-lookup"><span data-stu-id="568ed-146">Select Ctrl+Shift+P tooopen hello command palette, and then enter **ADL: Start Local Run Service**.</span></span> <span data-ttu-id="568ed-147">Başlangıç cmd konsolu açılır.</span><span class="sxs-lookup"><span data-stu-id="568ed-147">hello cmd console opens.</span></span> <span data-ttu-id="568ed-148">Bu hello emin olun **DataRoot** ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="568ed-148">Make sure that hello **DataRoot** is set.</span></span>
3. <span data-ttu-id="568ed-149">Bir kesme noktası, C# kod arkasında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="568ed-149">Set a breakpoint in your C# code-behind.</span></span>
4. <span data-ttu-id="568ed-150">Merhaba komut dosyası Düzenleyicisi'nde geri Ctrl + Shift + P tooopen hello komut konsolundan seçin ve ardından girin **yerel hata ayıklama** toostart yerel hata ayıklama hizmetinizi.</span><span class="sxs-lookup"><span data-stu-id="568ed-150">Back in hello script editor, select Ctrl+Shift+P tooopen hello command console, and then enter **Local Debug** toostart your local debug service.</span></span>

![Visual Studio Code yerel hata ayıklama sonuç için Data Lake araçları](./media/data-lake-analytics-data-lake-tools-for-vscode-local-run-and-debug/data-lake-tools-for-vscode-local-debug-result.png)


## <a name="next-steps"></a><span data-ttu-id="568ed-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="568ed-152">Next steps</span></span>
- <span data-ttu-id="568ed-153">Azure Data Lake araçları için Visual Studio Code kullanmak için bkz: [kullanım Azure Data Lake araçları Visual Studio Code için](data-lake-analytics-data-lake-tools-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="568ed-153">For using Azure Data Lake Tools for Visual Studio Code, see [Use Azure Data Lake Tools for Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md).</span></span>
- <span data-ttu-id="568ed-154">Data Lake Analytics başlatılan bilgi almak için bkz: [Öğreticisi: Azure Data Lake Analytics ile çalışmaya başlama](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="568ed-154">For getting started information on Data Lake Analytics, see [Tutorial: Get started with Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).</span></span>
- <span data-ttu-id="568ed-155">Visual Studio için Data Lake araçları hakkında bilgi için bkz: [öğretici: Visual Studio için Data Lake araçları kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="568ed-155">For information about Data Lake Tools for Visual Studio, see [Tutorial: Develop U-SQL scripts by using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
- <span data-ttu-id="568ed-156">Derlemeler geliştirme hello hakkında bilgi için bkz [Azure Data Lake Analytics işleri için U-SQL geliştirmek derlemeleri](data-lake-analytics-u-sql-develop-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="568ed-156">For hello information on developing assemblies, see [Develop U-SQL assemblies for Azure Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-assemblies.md).</span></span>
