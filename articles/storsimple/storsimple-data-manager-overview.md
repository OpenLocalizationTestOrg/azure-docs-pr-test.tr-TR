---
title: "Microsoft Azure StorSimple veri Yöneticisi'ne genel bakış | Microsoft Docs"
description: "StorSimple veri Yöneticisi hizmetini (özel olarak incelenmektedir) genel bir bakış sağlar"
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
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: aedb44610fe57055851538b9dbdb810e66e58d73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="72603-103">StorSimple Data Manager genel bakış (özel olarak incelenmektedir)</span><span class="sxs-lookup"><span data-stu-id="72603-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="72603-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="72603-104">Overview</span></span>

<span data-ttu-id="72603-105">Microsoft Azure StorSimple yaygın olarak dosya paylaşımları ile ilgili yapılandırılmamış veriler karmaşıklığını adresleri bir karma bulut depolama çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="72603-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses the complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="72603-106">StorSimple bulut depolama bulut depolama ve şirket içi depolama şirket içi çözüm ve otomatik olarak katmanları verilerinin bir uzantısı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="72603-106">StorSimple uses cloud storage as an extension of the on-premises solution and automatically tiers data across the on-premises storage and cloud storage.</span></span> <span data-ttu-id="72603-107">Veri koruma, yerel ile tümleşik ve bulut anlık görüntüleri, sprawling bir depolama altyapısını ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="72603-107">Integrated data protection, with local and cloud snapshots, eliminates the need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="72603-108">Arşiv ve olağanüstü durum kurtarma ayrıca bir site dışı konumu olarak işlev gören bulut ile sorunsuz olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="72603-108">Archival and disaster recovery is also seamless with the cloud acting as an offsite location.</span></span>

<span data-ttu-id="72603-109">Bu belgede, sunuyoruz veri dönüştürme hizmet sorunsuz bir şekilde bulutta StorSimple veri erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="72603-109">The data transformation service that we are introducing in this document, allows you to seamlessly access the StorSimple data in the cloud.</span></span> <span data-ttu-id="72603-110">Bu hizmet, StorSimple verileri ayıklamak ve bunu diğer Azure hizmetlerine biçimlerde, sunmak için API'ları kolayca kullanılabilecek sağlar.</span><span class="sxs-lookup"><span data-stu-id="72603-110">This service provides APIs to extract data from StorSimple and present it to other Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="72603-111">Bu Önizleme'de desteklenen biçimler şunlardır: Azure BLOB'ları ve Azure Media Services varlıklar.</span><span class="sxs-lookup"><span data-stu-id="72603-111">The formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="72603-112">Bu dönüşüm hizmetlerini Azure Media Services, Azure Hdınsight, Azure Machine Learning ve Azure Search verileri StorSimple 8000 serisi şirket içi cihazda çalışmaya gibi kolayca wire sağlar.</span><span class="sxs-lookup"><span data-stu-id="72603-112">This transformation enables you to easily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search to operate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="72603-113">Bu gösteren üst düzey blok diyagramını aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="72603-113">A high-level block diagram illustrating this is shown below.</span></span>

![Üst düzey diyagramı](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="72603-115">Bu belgede, bu hizmet için bir özel Önizleme ne kaydolabilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="72603-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="72603-116">Ayrıca, bulutta nasıl StorSimple veri kullanan uygulamaları yazmak için bu hizmet ve diğer Azure hizmetleriyle kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="72603-116">It also explains how you can use this service to write applications that use StorSimple data and other Azure services in the cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="72603-117">Veri Yöneticisi Önizleme için kaydolma</span><span class="sxs-lookup"><span data-stu-id="72603-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="72603-118">Veri Yöneticisi hizmeti için kaydolmadan önce aşağıdaki önkoşulları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="72603-118">Before you sign up for the Data Manager service, review the following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="72603-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="72603-119">Prerequisites</span></span>

<span data-ttu-id="72603-120">Bu alıştırmada, sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="72603-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="72603-121">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="72603-121">an active Azure subscription.</span></span>
* <span data-ttu-id="72603-122">kayıtlı bir StorSimple 8000 serisi aygıt erişim</span><span class="sxs-lookup"><span data-stu-id="72603-122">access to a registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="72603-123">StorSimple 8000 serisi cihaz ile ilişkili tüm anahtarları.</span><span class="sxs-lookup"><span data-stu-id="72603-123">all the keys associated with the StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="72603-124">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="72603-124">Sign up</span></span>

<span data-ttu-id="72603-125">StorSimple veri Yöneticisi'ni özel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="72603-125">The StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="72603-126">Bu hizmetin özel Önizleme için kaydolmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="72603-126">Perform the following steps to sign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="72603-127">StorSimple veri Yöneticisi uzantısına Azure portalıyla günlüğüne: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="72603-127">Log into the Azure portal with the StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="72603-128">Oturum açmak için Azure kimlik bilgilerinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="72603-128">Use your Azure credentials to log in.</span></span>

2.  <span data-ttu-id="72603-129">Tıklatın  **+**  bir hizmet oluşturmak için simge.</span><span class="sxs-lookup"><span data-stu-id="72603-129">Click the **+** icon to create a service.</span></span> <span data-ttu-id="72603-130">Tıklatın **depolama** ve ardından **bkz tüm** dikey penceresinde açılır.</span><span class="sxs-lookup"><span data-stu-id="72603-130">Click **Storage** and then click **See All** in the blade that opens up.</span></span>

    ![Arama StorSimple veri Yöneticisi simgesi](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="72603-132">StorSimple Data Manager simgesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="72603-132">You see the StorSimple Data Manager icon.</span></span>

    ![StorSimple veri Yöneticisi simgesini seçin](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="72603-134">StorSimple veri Yöneticisi simgesine tıklayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="72603-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="72603-135">Özel önizleme için etkinleştirin ve ardından istediğiniz aboneliği seçin **bana kaydolun!**</span><span class="sxs-lookup"><span data-stu-id="72603-135">Pick the subscription that you want to enable for the private preview and then click **Sign me up!**</span></span>

    ![Bana kaydolun](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="72603-137">Bu yerleşik bir isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="72603-137">This sends a request to onboard you.</span></span> <span data-ttu-id="72603-138">Biz yerleşik mümkün olan en kısa sürede çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="72603-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="72603-139">Aboneliğinizi etkinleştirildikten sonra StorSimple veri Yöneticisi hizmeti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72603-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="72603-140">Kolayca StorSimple veri Yöneticisi hizmetine erişim için Sık Kullanılanlara sabitlemek için yıldız simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="72603-140">To easily access the StorSimple Data Manager service, click the star icon to pin it to your favorites.</span></span>

    ![Erişim StorSimple veri yöneticileri](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="72603-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72603-142">Next steps</span></span>

<span data-ttu-id="72603-143">[StorSimple veri Yöneticisi'ni kullanın, verilerinizi dönüştürmek için kullanıcı Arabirimi](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="72603-143">[Use StorSimple Data Manager UI to transform your data](storsimple-data-manager-ui.md).</span></span>