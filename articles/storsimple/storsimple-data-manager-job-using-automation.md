---
title: "Bir iş tetiklemek için Azure Otomasyonu kullanın | Microsoft Docs"
description: "StorSimple veri Yöneticisi işleri (özel olarak incelenmektedir) tetiklemek için Azure Otomasyonu kullanmayı öğrenin"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 9691408bcd80afb6eba534f26749b76dd3bfe315
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-automation-to-trigger-a-job-private-preview"></a><span data-ttu-id="a053a-103">Azure Otomasyonu (özel Önizleme) bir iş tetiklemek için kullanın</span><span class="sxs-lookup"><span data-stu-id="a053a-103">Use Azure Automation to trigger a job (Private Preview)</span></span>

<span data-ttu-id="a053a-104">Bu makaleler Azure Automation StorSimple Data Manager iş tetiklemek için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="a053a-104">This articles describes how to use Azure Automation to trigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a053a-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a053a-105">Prerequisites</span></span>

<span data-ttu-id="a053a-106">Başlamadan önce şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="a053a-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="a053a-107">Azure Powershell yüklü.</span><span class="sxs-lookup"><span data-stu-id="a053a-107">Azure Powershell installed.</span></span> <span data-ttu-id="a053a-108">[Azure Powershell indirme](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="a053a-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="a053a-109">Veri dönüştürme işlemini başlatmak için yapılandırma ayarlarını (Bu ayarları almak için yönergeleri dahil burada).</span><span class="sxs-lookup"><span data-stu-id="a053a-109">Configuration settings to initialize the Data Transformation job (instructions to obtain these settings are included here).</span></span>
*   <span data-ttu-id="a053a-110">Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı.</span><span class="sxs-lookup"><span data-stu-id="a053a-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="a053a-111">Karşıdan `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) github deposuna dosyasından.</span><span class="sxs-lookup"><span data-stu-id="a053a-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from the github repository.</span></span>
*   <span data-ttu-id="a053a-112">Karşıdan `Get-ConfigurationParams.ps1` [betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) github'da depodan.</span><span class="sxs-lookup"><span data-stu-id="a053a-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from the github repository.</span></span>
*   <span data-ttu-id="a053a-113">Karşıdan `Trigger-DataTransformation-Job.ps1` [betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) github'da depodan.</span><span class="sxs-lookup"><span data-stu-id="a053a-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from the github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="a053a-114">Adım adım</span><span class="sxs-lookup"><span data-stu-id="a053a-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-the-automation-job-to-run-the-job-definition"></a><span data-ttu-id="a053a-115">Azure Active Directory izinlerini iş tanımı çalıştırmak Otomasyonu işini alın</span><span class="sxs-lookup"><span data-stu-id="a053a-115">Get Azure Active Directory permissions for the automation job to run the job definition</span></span>

1. <span data-ttu-id="a053a-116">Active Directory için yapılandırma parametreleri almak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="a053a-116">To retrieve the configuration parameters for Active Directory, do the following steps:</span></span>

    1. <span data-ttu-id="a053a-117">Windows PowerShell'i yerel makinenizde açın.</span><span class="sxs-lookup"><span data-stu-id="a053a-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="a053a-118">Emin [Azure PowerShell](https://azure.microsoft.com/downloads/) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a053a-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="a053a-119">Çalıştırma `Get-ConfigurationParams.ps1` komut dosyası (yukarıda indirdiğiniz klasörde).</span><span class="sxs-lookup"><span data-stu-id="a053a-119">Run the `Get-ConfigurationParams.ps1` script (in the folder you downloaded above).</span></span> <span data-ttu-id="a053a-120">PowerShell penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="a053a-120">Type the following command in the PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="a053a-121">ActiveDirectoryKey daha sonra kullandığınız paroladır.</span><span class="sxs-lookup"><span data-stu-id="a053a-121">The ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="a053a-122">Tercih ettiğiniz bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="a053a-122">Enter a password of your choice.</span></span> <span data-ttu-id="a053a-123">AppName herhangi bir dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="a053a-123">AppName can be any string.</span></span>

2. <span data-ttu-id="a053a-124">Bu komut dosyası Otomasyon runbook'u tetikleyen yüklenirken kullanılması gereken aşağıdaki değerleri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="a053a-124">This script outputs the following values that should be used while triggering the automation runbook.</span></span> <span data-ttu-id="a053a-125">Bu değerleri not edin.</span><span class="sxs-lookup"><span data-stu-id="a053a-125">Make a note of these values.</span></span>

    - <span data-ttu-id="a053a-126">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="a053a-126">Client ID</span></span>
    - <span data-ttu-id="a053a-127">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="a053a-127">Tenant ID</span></span>
    - <span data-ttu-id="a053a-128">Active Directory anahtar (aynı Yukarıda girilen)</span><span class="sxs-lookup"><span data-stu-id="a053a-128">Active Directory key (same as the one entered above)</span></span>
    - <span data-ttu-id="a053a-129">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="a053a-129">Subscription ID</span></span>

### <a name="set-up-the-automation-account"></a><span data-ttu-id="a053a-130">Otomasyon hesabı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a053a-130">Set up the Automation Account</span></span>

1. <span data-ttu-id="a053a-131">Azure'da oturum açın ve Automation hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="a053a-131">Log on to Azure and open your Automation account.</span></span>
2. <span data-ttu-id="a053a-132">Tıklatın **varlıklar** döşeme varlıklar listesini açın.</span><span class="sxs-lookup"><span data-stu-id="a053a-132">Click **Assets** tile to open the list of assets.</span></span>
3. <span data-ttu-id="a053a-133">Tıklatın **modülleri** modüllerin listesini açmak için kutucuğa.</span><span class="sxs-lookup"><span data-stu-id="a053a-133">Click **Modules** tile to open the list of modules.</span></span>
4. <span data-ttu-id="a053a-134">Tıklatın **+ bir modül Ekle** düğmesi ve Ekle modülü dikey başlatıldığında.</span><span class="sxs-lookup"><span data-stu-id="a053a-134">Click **+ Add a module** button and the Add module blade is launched.</span></span>

    ![Otomasyon hesabı ayarları](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="a053a-136">Seçtikten sonra `DataTransformationApp.zip` dosya yerel bilgisayarınızdan, tıklatın **Tamam** modülü içeri aktarmak için.</span><span class="sxs-lookup"><span data-stu-id="a053a-136">After you have selected the `DataTransformationApp.zip` file from your local computer, click **OK** to import the module.</span></span>

   <span data-ttu-id="a053a-137">Azure Automation hesabınız için bir modül aldığında modülüyle ilgili meta verileri ayıklar.</span><span class="sxs-lookup"><span data-stu-id="a053a-137">When Azure Automation imports a module to your account, it extracts metadata about the module.</span></span> <span data-ttu-id="a053a-138">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a053a-138">This operation may take a couple of minutes.</span></span>

   ![Otomasyon hesabı ayarları](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="a053a-140">İşlem tamamlandığında, modül dağıtıldığı bir bildirim ve başka bir bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a053a-140">You receive a notification that the module is being deployed and another notification when the process is complete.</span></span>  <span data-ttu-id="a053a-141">Durum ayrıca kontrol edebilirsiniz **modülleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="a053a-141">You can also check the status in **Modules** tile.</span></span>

### <a name="to-import-the-runbook-that-triggers-the-job-definition"></a><span data-ttu-id="a053a-142">İş tanımı tetikler runbook'u içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="a053a-142">To import the runbook that triggers the job definition</span></span>

1. <span data-ttu-id="a053a-143">Azure portalında, Otomasyon hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="a053a-143">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="a053a-144">Tıklatın **Runbook'lar** listesini açmak için döşeme.</span><span class="sxs-lookup"><span data-stu-id="a053a-144">Click **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="a053a-145">Tıklatın **+ runbook Ekle** ve ardından **mevcut bir runbook'u içeri aktar**.</span><span class="sxs-lookup"><span data-stu-id="a053a-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Mevcut bir runbook'u İçeri Aktar](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="a053a-147">Tıklatın **Runbook dosyası** ve alınacak dosya seçin `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="a053a-147">Click **Runbook file** and select the file to import `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="a053a-148">Tıklatın **oluşturma** runbook'u içeri aktarma.</span><span class="sxs-lookup"><span data-stu-id="a053a-148">Click **Create** to import the runbook.</span></span> <span data-ttu-id="a053a-149">Yeni runbook Otomasyon hesabı için runbook'ları listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a053a-149">The new runbook appears in the list of runbooks for the Automation account.</span></span>
7. <span data-ttu-id="a053a-150">Tıklatın **tetikleyici DataTransformation iş** runbook ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="a053a-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="a053a-151">Tıklatın **Yayımla** ve ardından **Evet** onaylamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="a053a-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="to-run-the-runbook"></a><span data-ttu-id="a053a-152">Runbook'u çalıştırmak için:</span><span class="sxs-lookup"><span data-stu-id="a053a-152">To run the runbook:</span></span>
1. <span data-ttu-id="a053a-153">Azure portalında, Otomasyon hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="a053a-153">In the Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="a053a-154">Runbook'ların listesini açmak için **Runbook'lar** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a053a-154">Click the **Runbooks** tile to open the list of runbooks.</span></span>
3. <span data-ttu-id="a053a-155">Tıklatın **tetikleyici DataTransformation iş**.</span><span class="sxs-lookup"><span data-stu-id="a053a-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="a053a-156">Runbook'u başlatmak için **Başlat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a053a-156">Click **Start** to start the runbook.</span></span>

   ![Runbook’u başlatma](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="a053a-158">İçinde **Başlat runbook** dikey penceresinde tüm parametreleri girin.</span><span class="sxs-lookup"><span data-stu-id="a053a-158">In the **Start runbook** blade, enter all the parameters.</span></span> <span data-ttu-id="a053a-159">Tıklatın **Tamam** veri dönüştürme işi göndermek için.</span><span class="sxs-lookup"><span data-stu-id="a053a-159">Click **OK** to submit the Data Transformation job.</span></span>

   ![Runbook’u başlatma](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="a053a-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a053a-161">Next steps</span></span>

<span data-ttu-id="a053a-162">[StorSimple veri Yöneticisi'ni kullanın, verilerinizi dönüştürmek için kullanıcı Arabirimi](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a053a-162">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>