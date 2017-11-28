---
title: "aaaAzure işlevleri çalışma zamanı yükleme | Microsoft Docs"
description: "Nasıl tooInstall hello Azure işlevleri çalışma zamanı"
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
ms.openlocfilehash: 67c6d10b5c0ac43e880d29cff0ae7b099f82bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="1b7bf-103">Hello Azure işlevleri çalışma zamanı Önizleme yükleyin</span><span class="sxs-lookup"><span data-stu-id="1b7bf-103">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="1b7bf-104">Tooinstall hello Azure işlevleri çalışma zamanı Önizleme istiyorsanız şu adımları izlemelisiniz:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-104">If you would like tooinstall hello Azure Functions Runtime preview, you must follow these steps:</span></span>

1. <span data-ttu-id="1b7bf-105">Merhaba en düşük gereksinimler makinenizi geçirir emin olun</span><span class="sxs-lookup"><span data-stu-id="1b7bf-105">Ensure your machine passes hello minimum requirements</span></span>
1. <span data-ttu-id="1b7bf-106">Merhaba karşıdan [Azure işlevleri çalışma zamanı Önizleme yükleyici](https://aka.ms/azafr).</span><span class="sxs-lookup"><span data-stu-id="1b7bf-106">Download hello [Azure Functions Runtime Preview Installer](https://aka.ms/azafr).</span></span> 
1. <span data-ttu-id="1b7bf-107">Hello Azure işlevleri çalışma zamanı preview yükleyin</span><span class="sxs-lookup"><span data-stu-id="1b7bf-107">Install hello Azure Functions Runtime preview</span></span>
1. <span data-ttu-id="1b7bf-108">Hello Azure işlevleri çalışma zamanı Önizleme tam hello yapılandırması</span><span class="sxs-lookup"><span data-stu-id="1b7bf-108">Complete hello configuration of hello Azure Functions Runtime preview</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b7bf-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1b7bf-109">Prerequisites</span></span>

<span data-ttu-id="1b7bf-110">Hello Azure işlevleri çalışma zamanı Önizleme yüklemeden önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1b7bf-110">Before you install hello Azure Functions Runtime preview, you must have hello following:</span></span>

1. <span data-ttu-id="1b7bf-111">Microsoft Windows Server 2016 veya Microsoft Windows 10 oluşturucuları Update (Professional veya Enterprise Edition) çalıştıran bir makineye.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-111">A machine running Microsoft Windows Server 2016 or Microsoft Windows 10 Creators Update (Professional or Enterprise Edition).</span></span>
1. <span data-ttu-id="1b7bf-112">Ağınızın içinde çalışan bir SQL Server örneği.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-112">A SQL Server instance running within your network.</span></span>  <span data-ttu-id="1b7bf-113">En düşük sürümü SQL Server Express gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-113">Minimum edition requirement is SQL Server Express.</span></span>

## <a name="install-hello-azure-functions-runtime-preview"></a><span data-ttu-id="1b7bf-114">Hello Azure işlevleri çalışma zamanı Önizleme yükleyin</span><span class="sxs-lookup"><span data-stu-id="1b7bf-114">Install hello Azure Functions Runtime Preview</span></span>

<span data-ttu-id="1b7bf-115">Hello Azure işlevleri çalışma zamanı Önizleme yükleyici hello yüklemesi hello Azure işlevleri çalışma zamanı Önizleme yönetimi ve çalışan rolleri sırasında size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-115">hello Azure Functions Runtime preview installer guides you through hello installation of hello Azure Functions Runtime preview Management and Worker Roles.</span></span>  <span data-ttu-id="1b7bf-116">Olası tooinstall hello yönetimi ve hello üzerinde çalışan rolü olan aynı makine.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-116">It is possible tooinstall hello Management and Worker role on hello same machine.</span></span>  <span data-ttu-id="1b7bf-117">Ancak, daha fazla işlevler eklemek gibi ek makineleri toobe mümkün tooscale daha fazla çalışan rollerinde işlevlerinizi birden çok Worker üzerine dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-117">However, as you add more Functions, you must deploy more worker roles on additional machines toobe able tooscale your functions onto multiple workers.</span></span>

## <a name="install-hello-management-and-worker-role-on-hello-same-machine"></a><span data-ttu-id="1b7bf-118">Merhaba yönetimi ve çalışan rolü üzerinde hello yükleme aynı makine</span><span class="sxs-lookup"><span data-stu-id="1b7bf-118">Install hello Management and Worker Role on hello same machine</span></span>

1. <span data-ttu-id="1b7bf-119">Hello Azure işlevleri çalışma zamanı Önizleme yükleyici çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-119">Run hello Azure Functions Runtime Preview Installer.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici][1]

1. <span data-ttu-id="1b7bf-121">**İleri'yi** öncelikli hello yükleyici ilk aşamasında hello geçmiş</span><span class="sxs-lookup"><span data-stu-id="1b7bf-121">**Click Next** advance past hello first stage of hello installer</span></span>
1. <span data-ttu-id="1b7bf-122">Merhaba hello koşullarını okuduğunuzu sonra **EULA**, **hello kutuyu** tooaccept hello hüküm ve **İleri'yi tıklatın** tooadvance.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-122">Once you have read hello terms of hello **EULA**, **check hello box** tooaccept hello terms and **click Next** tooadvance.</span></span>
1. <span data-ttu-id="1b7bf-123">Rolleri seçin hello artık bu makinede tooinstall istediğiniz **işlevleri yönetim rolü** ve/veya **işlevleri çalışan rolü** ve **İleri'yi tıklatın**</span><span class="sxs-lookup"><span data-stu-id="1b7bf-123">Now select hello roles you want tooinstall on this machine **Functions Management Role** and/or **Functions Worker Role** and **Click Next**</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici - rolü seçimi][3]

    > [!NOTE]
    > <span data-ttu-id="1b7bf-125">Merhaba yükleyebilirsiniz **işlevleri çalışan rolü** diğer birçok makineler toodo bu nedenle, bu yönergeleri izleyin ve yalnızca seçin **işlevleri çalışan rolü** hello yükleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-125">You can install hello **Functions Worker Role** on many other machines toodo so, follow these instructions, and only select **Functions Worker Role** in hello installer.</span></span>

1. <span data-ttu-id="1b7bf-126">**İleri'yi** toohave hello **Azure işlevleri çalışma zamanı yükleyicisi** makinenize yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-126">**Click Next** toohave hello **Azure Functions Runtime Installer** install on your machine.</span></span>
1. <span data-ttu-id="1b7bf-127">Tam hello yükleyici hello başlatacak sonra **Azure işlevleri çalışma zamanı yapılandırma aracı**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-127">Once complete hello installer will launch hello **Azure Functions Runtime Configuration tool**.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yükleyici tamamlandı][5]

    > [!NOTE]
    > <span data-ttu-id="1b7bf-129">Üzerinde yüklüyorsanız **Windows 10** ve hello **kapsayıcı** özelliği daha önce etkinleştirilmemiş, hello **Azure işlevleri çalışma zamanı** yükleyici tooreboot ister Makine toocomplete hello yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-129">If you are installing on **Windows 10** and hello **Container** feature has not been previously enabled, hello **Azure Functions Runtime** Installer prompts you tooreboot your machine toocomplete hello install.</span></span>

## <a name="configure-hello-azure-functions-runtime"></a><span data-ttu-id="1b7bf-130">Hello Azure işlevleri çalışma zamanı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1b7bf-130">Configure hello Azure Functions Runtime</span></span>

<span data-ttu-id="1b7bf-131">toocomplete hello Azure işlevleri çalışma zamanı yükleme hello yapılandırmasını tamamlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-131">toocomplete hello Azure Functions Runtime installation you must complete hello configuration.</span></span>

1. <span data-ttu-id="1b7bf-132">Merhaba **Azure işlevleri çalışma zamanı yapılandırma aracı** hangi rollerin makinenize yüklü olan gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-132">hello **Azure Functions Runtime Configuration Tool** shows which roles are installed on your machine.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yapılandırma aracı][6]

1. <span data-ttu-id="1b7bf-134">Hello tıklatın **veritabanı** sekmesinde, hello girin **bağlantı ayrıntıları, SQL Server örneği için** ve **Uygula'yı**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-134">Click hello **Database** tab, enter hello **connection details for your SQL Server Instance** and **click Apply**.</span></span>  <span data-ttu-id="1b7bf-135">Bu sipariş toohello Azure işlevleri çalışma zamanı toocreate veritabanı toosupport hello çalışma zamanı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-135">This is required in order toohello Azure Functions Runtime toocreate a database toosupport hello Runtime.</span></span>
    
    ![Azure işlevleri çalışma zamanı Önizleme veritabanı yapılandırması][7]

1. <span data-ttu-id="1b7bf-137">Merhaba tıklatın **kimlik bilgileri** sekmesi.  Bu ekranda tüm Azure işlevleri barındırmak için iki yeni kimlik bilgileri kullanmak için bir dosya paylaşımı ile oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-137">Click hello **Credentials** tab.  On this screen you must create two new credentials for use with a FileShare for hosting all your Azure Functions.</span></span>  <span data-ttu-id="1b7bf-138">**Kullanıcı adı ve parola belirtin** hello için KOMBİNASYON **dosya paylaşımı sahibi** ve hello için **dosya paylaşımı kullanıcısı** tıklatıp **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-138">**Specify Username and Password** combinations for hello **File Share Owner** and for hello **File Share User** and click **Apply**.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme kimlik bilgileri][8]

1. <span data-ttu-id="1b7bf-140">Merhaba tıklatın **dosya paylaşımı** sekmesi.  Bu ekranda hello hello ayrıntılarını belirtmelisiniz **dosya paylaşım konumunu**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-140">Click hello **File Share** tab.  In this screen you must specify hello details of hello **File Share location**.</span></span>  <span data-ttu-id="1b7bf-141">Bu sizin için oluşturulabilir veya var olan bir dosya paylaşımı kullanabilir ve tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-141">This can be created for you or you can use an existing File Share and click **Apply**.</span></span>  <span data-ttu-id="1b7bf-142">Yeni bir dosya paylaşımı konumu seçerseniz, hello Azure işlevleri çalışma zamanı tarafından kullanım için bir dizin belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-142">If you select a new File Share location, you must specify a directory for use by hello Azure Functions Runtime.</span></span>
    
    ![Azure işlevleri çalışma zamanı Önizleme dosya paylaşımı][9]

1. <span data-ttu-id="1b7bf-144">Merhaba tıklatın **IIS** sekmesi.  Bu sekme, IIS Azure işlevleri çalışma zamanı yükleme oluşturacak bu hello hello Web siteleri hello ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-144">Click hello **IIS** tab.  This tab shows hello details of hello websites in IIS that hello Azure Functions Runtime Installation will create.</span></span>  <span data-ttu-id="1b7bf-145">**Uygula'yı** toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-145">**Click Apply** toocomplete.</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme IIS][10]

1. <span data-ttu-id="1b7bf-147">Merhaba tıklatın **Hizmetleri** sekmesi.  Bu sekme, Azure işlevleri çalışma zamanı yükleme hello hello hizmetlerinin durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b7bf-147">Click hello **Services** tab.  This tab shows hello status of hello services in your Azure Functions Runtime installation.</span></span>  <span data-ttu-id="1b7bf-148">Eğer ilk yapılandırma hello sonra **Azure işlevleri konak Etkinleştirme hizmeti** tıklatın çalışmıyor **Hizmeti'ni Başlat**</span><span class="sxs-lookup"><span data-stu-id="1b7bf-148">If after initial configuration hello **Azure Functions Host Activation Service** is not running click **Start Service**</span></span>

    ![Azure işlevleri çalışma zamanı Önizleme yapılandırma tamamlandı][11]

1. <span data-ttu-id="1b7bf-150">Son olarak toohello Gözat **Azure işlevleri çalışma zamanı Portal** olarak`https://<machinename>/`</span><span class="sxs-lookup"><span data-stu-id="1b7bf-150">Finally browse toohello **Azure Functions Runtime Portal** as `https://<machinename>/`</span></span>

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