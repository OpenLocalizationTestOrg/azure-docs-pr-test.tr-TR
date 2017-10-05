---
title: "Azure işlevleri çalışma zamanı yükleme | Microsoft Docs"
description: "Azure işlevleri çalışma zamanı yükleme"
services: functions
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 05/08/2017
ms.author: anwestg
ms.openlocfilehash: 1e4188313a87d07f396e5f8edc8969dd5da2c436
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="669b9-103">Azure işlevleri çalışma zamanı Preview yükleyin</span><span class="sxs-lookup"><span data-stu-id="669b9-103">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="669b9-104">Azure işlevleri çalışma zamanı Önizleme yüklemek istiyorsanız, şu adımları izlemelisiniz:</span><span class="sxs-lookup"><span data-stu-id="669b9-104">If you would like to install the Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="669b9-105">En düşük gereksinimleri makinenizi geçirir emin olun</span><span class="sxs-lookup"><span data-stu-id="669b9-105">Ensure your machine passes the minimum requirements</span></span>
1. <span data-ttu-id="669b9-106">Karşıdan [Azure işlevleri çalışma zamanı Önizleme yükleyici](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="669b9-106">Download the [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="669b9-107">Azure işlevleri çalışma zamanı preview yükleyin</span><span class="sxs-lookup"><span data-stu-id="669b9-107">Install the Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="669b9-108">Azure işlevleri çalışma zamanı Önizleme yapılandırmasını tamamlama</span><span class="sxs-lookup"><span data-stu-id="669b9-108">Complete the configuration of the Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="669b9-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="669b9-109">Prerequisites</span></span>

<span data-ttu-id="669b9-110">Azure işlevleri çalışma zamanı Önizleme yüklemeden önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="669b9-110">Before you install the Azure Functions Runtime preview, you must have the following:</span></span>

1. <span data-ttu-id="669b9-111">Microsoft Windows Server 2016 veya Microsoft Windows 10 oluşturucuları Update (Professional veya Enterprise Edition) çalıştıran bir makineye.</span><span class="sxs-lookup"><span data-stu-id="669b9-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="669b9-112">Ağınızın içinde çalışan bir SQL Server örneği.</span><span class="sxs-lookup"><span data-stu-id="669b9-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="669b9-113">En düşük sürümü SQL Server Express gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="669b9-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-the-azure-functions-runtime-preview"></a><span data-ttu-id="669b9-114">Azure işlevleri çalışma zamanı Preview yükleyin</span><span class="sxs-lookup"><span data-stu-id="669b9-114">Install the Azure Functions Runtime Preview</span></span>

<span data-ttu-id="669b9-115">Azure işlevleri çalışma zamanı Önizleme yükleyici Azure işlevleri çalışma zamanı Önizleme yönetimi ve çalışan rolleri yüklenmesinde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="669b9-115">The Azure Functions Runtime preview installer guides you through the installation of the Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="669b9-116">Yönetim ve çalışan rolü aynı makinede yüklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="669b9-116">It is possible to install the Management and Worker role on the same machine.</span></span>  <span data-ttu-id="669b9-117">Ancak, daha fazla işlevler eklemek gibi birden çok Worker üzerine işlevlerinizi ölçeklendirme yapabilmek için ek makinelerde daha fazla çalışan rolleri dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="669b9-117">However, as you add more Functions, you must deploy more worker roles on additional machines to be able to scale your functions onto multiple workers.</span></span>

## <a name="install-the-management-and-worker-role-on-the-same-machine"></a><span data-ttu-id="669b9-118">Yönetim ve çalışan rolü aynı makineye yükleme</span><span class="sxs-lookup"><span data-stu-id="669b9-118">Install the Management and Worker Role on the same machine</span></span>

1. <span data-ttu-id="669b9-119">Azure işlevleri çalışma zamanı Önizleme yükleyiciyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="669b9-119">Run the Azure Functions Runtime Preview Installer.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici][1]

1. <span data-ttu-id="669b9-121">**İleri'yi** öncelikli yükleyici ilk aşamasında geçmiş</span><span class="sxs-lookup"><span data-stu-id="669b9-121">**Click Next** advance past the first stage of the installer</span></span>
1. <span data-ttu-id="669b9-122">Koşullarını okuduğunuzu sonra **EULA**, **onay kutusunu** hükümleri kabul etmek ve **İleri'yi tıklatın** ilerlemek için.</span><span class="sxs-lookup"><span data-stu-id="669b9-122">Once you have read the terms of the **EULA**, **check the box** to accept the terms and **click Next** to advance.</span></span>
1. <span data-ttu-id="669b9-123">Şimdi, bu makinede yüklemek istediğiniz rol seçin **işlevleri yönetim rolü** ve/veya **işlevleri çalışan rolü** ve **İleri'yi tıklatın**</span><span class="sxs-lookup"><span data-stu-id="669b9-123">Now select the roles you want to install on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici - rolü seçimi][3]

    > [!NOTE]
    > <span data-ttu-id="669b9-125">Yükleyebileceğiniz **işlevleri çalışan rolü** Bunu yapmak için birçok diğer makinelere, aşağıdaki yönergeleri izleyin ve yalnızca seçin **işlevleri çalışan rolü** yükleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="669b9-125">You can install the **Functions Worker Role** on many other machines to do so, follow these instructions, and only select **Functions Worker Role** in the installer.</span></span>

1. <span data-ttu-id="669b9-126">**İleri'yi** olmasını **Azure işlevleri çalışma zamanı yükleyicisi** makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="669b9-126">**Click Next** to have the **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="669b9-127">Tamamlandığında yükleyici başlatacak **Azure işlevleri çalışma zamanı yapılandırma aracı**.</span><span class="sxs-lookup"><span data-stu-id="669b9-127">Once complete the installer will launch the **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici tamamlandı][5]

    > [!NOTE]
    > <span data-ttu-id="669b9-129">Üzerinde yüklüyorsanız **Windows 10** ve **kapsayıcı** özelliği daha önce etkinleştirilmemiş, **Azure işlevleri çalışma zamanı** yükleyici yeniden başlatılmasını ister, yüklemeyi tamamlamak için makine.</span><span class="sxs-lookup"><span data-stu-id="669b9-129">If you are installing on **Windows 10** and the **Container** feature has not been previously enabled, the **Azure Functions Runtime** Installer prompts you to reboot your machine to complete the install.</span></span>

## <a name="configure-the-azure-functions-runtime"></a><span data-ttu-id="669b9-130">Azure işlevleri çalışma zamanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="669b9-130">Configure the Azure Functions Runtime</span></span>

<span data-ttu-id="669b9-131">Azure işlevleri çalışma zamanı yüklemenin tamamlanması için yapılandırmasını tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="669b9-131">To complete the Azure Functions Runtime installation you must complete the configuration.</span></span>

1. <span data-ttu-id="669b9-132">**Azure işlevleri çalışma zamanı yapılandırma aracı** hangi rollerin makinenize yüklü olan gösterir.</span><span class="sxs-lookup"><span data-stu-id="669b9-132">The **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yapılandırma aracı][6]

1. <span data-ttu-id="669b9-134">Tıklatın **veritabanı** sekmesinde, girin **bağlantı ayrıntıları, SQL Server örneği için** ve **Uygula'yı**.</span><span class="sxs-lookup"><span data-stu-id="669b9-134">Click the **Database** tab, enter the **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="669b9-135">Çalışma zamanı desteklemek için bu bir veritabanı oluşturmak için sırayla Azure işlevleri çalışma zamanı için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="669b9-135">This is required in order to the Azure Functions Runtime to create a database to support the Runtime.</span></span>
    
    ![Azure işlevleri çalışma zamanı Önizleme veritabanı yapılandırması][7]

1. <span data-ttu-id="669b9-137">Tıklatın **kimlik bilgileri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="669b9-137">Click the **Credentials** tab.</span></span>  <span data-ttu-id="669b9-138">Bu ekranda tüm Azure işlevleri barındırmak için iki yeni kimlik bilgileri kullanmak için bir dosya paylaşımı ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="669b9-138">On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="669b9-139">**Kullanıcı adı ve parola belirtin** için KOMBİNASYON **dosya paylaşımı sahibi** ve **dosya paylaşımı kullanıcısı** tıklatıp **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="669b9-139">**Specify Username and Password** combinations for the **File Share Owner** and for the **File Share User** and click **Apply**.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme kimlik bilgileri][8]

1. <span data-ttu-id="669b9-141">Tıklatın **dosya paylaşımı** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="669b9-141">Click the **File Share** tab.</span></span>  <span data-ttu-id="669b9-142">Bu ekranda ayrıntılarını belirtmelisiniz **dosya paylaşım konumunu**.</span><span class="sxs-lookup"><span data-stu-id="669b9-142">In this screen you must specify the details of the **File Share location**.</span></span>  <span data-ttu-id="669b9-143">Bu sizin için oluşturulabilir veya var olan bir dosya paylaşımı kullanabilir ve tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="669b9-143">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="669b9-144">Yeni bir dosya paylaşımı konumu seçerseniz Azure işlevleri çalışma zamanı tarafından kullanılmak üzere bir dizin belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="669b9-144">If you select a new File Share location, you must specify a directory for use by the Azure Functions Runtime.</span></span>
    
    ![Azure işlevleri çalışma zamanı Önizleme dosya paylaşımı][9]

1. <span data-ttu-id="669b9-146">Tıklatın **IIS** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="669b9-146">Click the **IIS** tab.</span></span>  <span data-ttu-id="669b9-147">Bu sekme, Azure işlevleri çalışma zamanı yükleme oluşturacak IIS'de Web siteleri ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="669b9-147">This tab shows the details of the websites in IIS that the Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="669b9-148">**Uygula'yı** tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="669b9-148">**Click Apply** to complete.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme IIS][10]

1. <span data-ttu-id="669b9-150">Tıklatın **Hizmetleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="669b9-150">Click the **Services** tab.</span></span>  <span data-ttu-id="669b9-151">Bu sekme, Azure işlevleri çalışma zamanı yüklemenizdeki hizmetlerinin durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="669b9-151">This tab shows the status of the services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="669b9-152">Eğer ilk yapılandırmadan sonra **Azure işlevleri konak Etkinleştirme hizmeti** tıklatın çalışmıyor **Hizmeti'ni Başlat**</span><span class="sxs-lookup"><span data-stu-id="669b9-152">If after initial configuration the **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yapılandırma tamamlandı][11]

1. <span data-ttu-id="669b9-154">Son olarak göz atın **Azure işlevleri çalışma zamanı Portal** olarak`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="669b9-154">Finally browse to the **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme portalı][12]


<!--Image references-->
[1]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer1.png
[2]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer2-EULA.png
[3]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer3-ChooseRoles.png
[4]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer4-Install.png
[5]: ./media/functions-runtime-install/AzureFunctionsRuntime_Installer5-InstallComplete.png
[6]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration1.png
[7]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration2_SQL.png
[8]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration3_Credentials.png
[9]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration4_Fileshare.png
[10]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration5_IIS.png
[11]: ./media/functions-runtime-install/AzureFunctionsRuntime_Configuration6_Services.png
[12]: ./media/functions-runtime-install/AzureFunctionsRuntime_Portal.png