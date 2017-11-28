---
title: "aaaUse Azure Otomasyonu tootrigger bir işi | Microsoft Docs"
description: "Bilgi nasıl StorSimple Data Manager işleri (özel olarak incelenmektedir) tetiklemek toouse Azure Otomasyonu"
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
ms.openlocfilehash: 0d9d6e5e6d52ed27ca759ed7e949b5f5dfd319c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-automation-tootrigger-a-job-private-preview"></a><span data-ttu-id="ca880-103">Azure Otomasyonu tootrigger işi (özel olarak incelenmektedir) kullanın</span><span class="sxs-lookup"><span data-stu-id="ca880-103">Use Azure Automation tootrigger a job (Private Preview)</span></span>

<span data-ttu-id="ca880-104">Bu makalede açıklanır nasıl toouse Azure Otomasyonu tootrigger bir StorSimple veri Yöneticisi işi.</span><span class="sxs-lookup"><span data-stu-id="ca880-104">This articles describes how toouse Azure Automation tootrigger a StorSimple Data Manager job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca880-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ca880-105">Prerequisites</span></span>

<span data-ttu-id="ca880-106">Başlamadan önce şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="ca880-106">Before you begin, ensure that you have:</span></span>

*   <span data-ttu-id="ca880-107">Azure Powershell yüklü.</span><span class="sxs-lookup"><span data-stu-id="ca880-107">Azure Powershell installed.</span></span> <span data-ttu-id="ca880-108">[Azure Powershell indirme](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span><span class="sxs-lookup"><span data-stu-id="ca880-108">[Download Azure Powershell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).</span></span>
*   <span data-ttu-id="ca880-109">Yapılandırma ayarları tooinitialize hello veri dönüştürme işi (yönergeleri tooobtain bu ayarları buraya dahil).</span><span class="sxs-lookup"><span data-stu-id="ca880-109">Configuration settings tooinitialize hello Data Transformation job (instructions tooobtain these settings are included here).</span></span>
*   <span data-ttu-id="ca880-110">Bir kaynak grubu içinde karma veri kaynağındaki doğru şekilde yapılandırılmış bir iş tanımı.</span><span class="sxs-lookup"><span data-stu-id="ca880-110">A job definition that has been correctly configured in a Hybrid Data Resource within a resource group.</span></span>
*   <span data-ttu-id="ca880-111">Karşıdan `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) hello github deposunu dosyasından.</span><span class="sxs-lookup"><span data-stu-id="ca880-111">Download `DataTransformationApp.zip` [zip](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/raw/master/Azure%20Automation%20For%20Data%20Manager/DataTransformationApp.zip) file from hello github repository.</span></span>
*   <span data-ttu-id="ca880-112">Karşıdan `Get-ConfigurationParams.ps1` [betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) hello github'da depodan.</span><span class="sxs-lookup"><span data-stu-id="ca880-112">Download `Get-ConfigurationParams.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Get-ConfigurationParams.ps1) from hello github repository.</span></span>
*   <span data-ttu-id="ca880-113">Karşıdan `Trigger-DataTransformation-Job.ps1` [betik](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) hello github'da depodan.</span><span class="sxs-lookup"><span data-stu-id="ca880-113">Download `Trigger-DataTransformation-Job.ps1` [script](https://github.com/Azure-Samples/storsimple-dotnet-data-manager-get-started/blob/master/Azure%20Automation%20For%20Data%20Manager/Trigger-DataTransformation-Job.ps1) from hello github repository.</span></span>

## <a name="step-by-step"></a><span data-ttu-id="ca880-114">Adım adım</span><span class="sxs-lookup"><span data-stu-id="ca880-114">Step-by-step</span></span>

### <a name="get-azure-active-directory-permissions-for-hello-automation-job-toorun-hello-job-definition"></a><span data-ttu-id="ca880-115">Azure Active Directory izinlerini hello Otomasyon iş toorun hello iş tanımı Al</span><span class="sxs-lookup"><span data-stu-id="ca880-115">Get Azure Active Directory permissions for hello automation job toorun hello job definition</span></span>

1. <span data-ttu-id="ca880-116">Active Directory için tooretrieve hello yapılandırma parametreleri adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="ca880-116">tooretrieve hello configuration parameters for Active Directory, do hello following steps:</span></span>

    1. <span data-ttu-id="ca880-117">Windows PowerShell'i yerel makinenizde açın.</span><span class="sxs-lookup"><span data-stu-id="ca880-117">Open Windows PowerShell in your local machine.</span></span> <span data-ttu-id="ca880-118">Emin [Azure PowerShell](https://azure.microsoft.com/downloads/) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="ca880-118">Ensure that [Azure PowerShell](https://azure.microsoft.com/downloads/) is installed.</span></span>
    1. <span data-ttu-id="ca880-119">Merhaba çalıştırmak `Get-ConfigurationParams.ps1` komut dosyası (yukarıda indirdiğiniz hello klasörü).</span><span class="sxs-lookup"><span data-stu-id="ca880-119">Run hello `Get-ConfigurationParams.ps1` script (in hello folder you downloaded above).</span></span> <span data-ttu-id="ca880-120">Merhaba komutu hello PowerShell penceresinde aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="ca880-120">Type hello following command in hello PowerShell window:</span></span>

        ```
        .\Get-ConfigurationParams.ps1 -SubscriptionName "AzureSubscriptionName" -ActiveDirectoryKey "AnyRandomPassword" -AppName "ApplicationName"
         ```

        <span data-ttu-id="ca880-121">Merhaba ActiveDirectoryKey daha sonra kullandığınız paroladır.</span><span class="sxs-lookup"><span data-stu-id="ca880-121">hello ActiveDirectoryKey is a password that you use later.</span></span> <span data-ttu-id="ca880-122">Tercih ettiğiniz bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="ca880-122">Enter a password of your choice.</span></span> <span data-ttu-id="ca880-123">AppName herhangi bir dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="ca880-123">AppName can be any string.</span></span>

2. <span data-ttu-id="ca880-124">Bu komut dosyası hello Otomasyon runbook'u tetiklemek yüklenirken kullanılması gereken değerleri aşağıdaki hello çıkarır.</span><span class="sxs-lookup"><span data-stu-id="ca880-124">This script outputs hello following values that should be used while triggering hello automation runbook.</span></span> <span data-ttu-id="ca880-125">Bu değerleri not edin.</span><span class="sxs-lookup"><span data-stu-id="ca880-125">Make a note of these values.</span></span>

    - <span data-ttu-id="ca880-126">İstemci kimliği</span><span class="sxs-lookup"><span data-stu-id="ca880-126">Client ID</span></span>
    - <span data-ttu-id="ca880-127">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="ca880-127">Tenant ID</span></span>
    - <span data-ttu-id="ca880-128">Active Directory anahtar (bir Yukarıda girilen hello ile aynı)</span><span class="sxs-lookup"><span data-stu-id="ca880-128">Active Directory key (same as hello one entered above)</span></span>
    - <span data-ttu-id="ca880-129">Abonelik Kimliği</span><span class="sxs-lookup"><span data-stu-id="ca880-129">Subscription ID</span></span>

### <a name="set-up-hello-automation-account"></a><span data-ttu-id="ca880-130">Otomasyon hesabı Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ca880-130">Set up hello Automation Account</span></span>

1. <span data-ttu-id="ca880-131">TooAzure üzerinde oturum ve Automation hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="ca880-131">Log on tooAzure and open your Automation account.</span></span>
2. <span data-ttu-id="ca880-132">Tıklatın **varlıklar** döşeme tooopen hello varlıkların listesi.</span><span class="sxs-lookup"><span data-stu-id="ca880-132">Click **Assets** tile tooopen hello list of assets.</span></span>
3. <span data-ttu-id="ca880-133">Tıklatın **modülleri** döşeme tooopen hello modüller listesi.</span><span class="sxs-lookup"><span data-stu-id="ca880-133">Click **Modules** tile tooopen hello list of modules.</span></span>
4. <span data-ttu-id="ca880-134">Tıklatın **+ bir modül Ekle** düğmesi ve hello Ekle modülü dikey başlatıldığında.</span><span class="sxs-lookup"><span data-stu-id="ca880-134">Click **+ Add a module** button and hello Add module blade is launched.</span></span>

    ![Otomasyon hesabı ayarları](./media/storsimple-data-manager-job-using-automation/add-module1m.png)

5. <span data-ttu-id="ca880-136">Merhaba seçtikten sonra `DataTransformationApp.zip` dosya yerel bilgisayarınızdan, tıklatın **Tamam** tooimport hello modülü.</span><span class="sxs-lookup"><span data-stu-id="ca880-136">After you have selected hello `DataTransformationApp.zip` file from your local computer, click **OK** tooimport hello module.</span></span>

   <span data-ttu-id="ca880-137">Azure Otomasyonu modülü tooyour hesabı aldığında hello modülüyle ilgili meta verileri ayıklar.</span><span class="sxs-lookup"><span data-stu-id="ca880-137">When Azure Automation imports a module tooyour account, it extracts metadata about hello module.</span></span> <span data-ttu-id="ca880-138">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ca880-138">This operation may take a couple of minutes.</span></span>

   ![Otomasyon hesabı ayarları](./media/storsimple-data-manager-job-using-automation/add-module2m.png)

   

6. <span data-ttu-id="ca880-140">Bir bildirim bu hello modül dağıtılan ve hello işlemi tamamlandığında, başka bir bildirim.</span><span class="sxs-lookup"><span data-stu-id="ca880-140">You receive a notification that hello module is being deployed and another notification when hello process is complete.</span></span>  <span data-ttu-id="ca880-141">Merhaba durum ayrıca kontrol edebilirsiniz **modülleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ca880-141">You can also check hello status in **Modules** tile.</span></span>

### <a name="tooimport-hello-runbook-that-triggers-hello-job-definition"></a><span data-ttu-id="ca880-142">Merhaba iş tanımı tetikler tooimport hello runbook</span><span class="sxs-lookup"><span data-stu-id="ca880-142">tooimport hello runbook that triggers hello job definition</span></span>

1. <span data-ttu-id="ca880-143">Hello Azure portal, Automation hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="ca880-143">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="ca880-144">Tıklatın **Runbook'lar** döşeme tooopen hello listesini.</span><span class="sxs-lookup"><span data-stu-id="ca880-144">Click **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="ca880-145">Tıklatın **+ runbook Ekle** ve ardından **mevcut bir runbook'u içeri aktar**.</span><span class="sxs-lookup"><span data-stu-id="ca880-145">Click **+ Add a runbook** and then **Import an existing runbook**.</span></span>

   ![Mevcut bir runbook'u İçeri Aktar](./media/storsimple-data-manager-job-using-automation/import-a-runbook.png)

4. <span data-ttu-id="ca880-147">Tıklatın **Runbook dosyası** ve select hello dosya tooimport `Trigger-DataTransformation-Job.ps1`.</span><span class="sxs-lookup"><span data-stu-id="ca880-147">Click **Runbook file** and select hello file tooimport `Trigger-DataTransformation-Job.ps1`.</span></span>
5. <span data-ttu-id="ca880-148">Tıklatın **oluşturma** tooimport hello runbook.</span><span class="sxs-lookup"><span data-stu-id="ca880-148">Click **Create** tooimport hello runbook.</span></span> <span data-ttu-id="ca880-149">Merhaba yeni runbook hello Otomasyon hesabı için runbook'ların hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="ca880-149">hello new runbook appears in hello list of runbooks for hello Automation account.</span></span>
7. <span data-ttu-id="ca880-150">Tıklatın **tetikleyici DataTransformation iş** runbook ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="ca880-150">Click **Trigger-DataTransformation-Job** runbook and then click **Edit**.</span></span>
8. <span data-ttu-id="ca880-151">Tıklatın **Yayımla** ve ardından **Evet** onaylamanız istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="ca880-151">Click **Publish** and then **Yes** when prompted for confirmation.</span></span>


### <a name="toorun-hello-runbook"></a><span data-ttu-id="ca880-152">toorun hello runbook:</span><span class="sxs-lookup"><span data-stu-id="ca880-152">toorun hello runbook:</span></span>
1. <span data-ttu-id="ca880-153">Hello Azure portal, Automation hesabınızı açın.</span><span class="sxs-lookup"><span data-stu-id="ca880-153">In hello Azure portal, open your Automation account.</span></span>
2. <span data-ttu-id="ca880-154">Merhaba tıklatın **Runbook'lar** döşeme tooopen hello listesini.</span><span class="sxs-lookup"><span data-stu-id="ca880-154">Click hello **Runbooks** tile tooopen hello list of runbooks.</span></span>
3. <span data-ttu-id="ca880-155">Tıklatın **tetikleyici DataTransformation iş**.</span><span class="sxs-lookup"><span data-stu-id="ca880-155">Click **Trigger-DataTransformation-Job**.</span></span>
4. <span data-ttu-id="ca880-156">Tıklatın **Başlat** toostart hello runbook.</span><span class="sxs-lookup"><span data-stu-id="ca880-156">Click **Start** toostart hello runbook.</span></span>

   ![Runbook’u başlatma](./media/storsimple-data-manager-job-using-automation/run-runbook1m.png)

5. <span data-ttu-id="ca880-158">Merhaba, **Başlat runbook** dikey penceresinde tüm hello parametreleri girin.</span><span class="sxs-lookup"><span data-stu-id="ca880-158">In hello **Start runbook** blade, enter all hello parameters.</span></span> <span data-ttu-id="ca880-159">Tıklatın **Tamam** toosubmit hello veri dönüştürme işi.</span><span class="sxs-lookup"><span data-stu-id="ca880-159">Click **OK** toosubmit hello Data Transformation job.</span></span>

   ![Runbook’u başlatma](./media/storsimple-data-manager-job-using-automation/run-runbook2m.png)


## <a name="next-steps"></a><span data-ttu-id="ca880-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca880-161">Next steps</span></span>

<span data-ttu-id="ca880-162">[StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="ca880-162">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
