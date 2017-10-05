---
title: "Azure Analysis Services öğreticisi 13. ders: Dağıtma | Microsoft Docs"
description: "Azure Analysis Services’a öğretici projesinin nasıl dağıtılacağını açıklar."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="fda62-103">13. Ders: Dağıtma</span><span class="sxs-lookup"><span data-stu-id="fda62-103">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="fda62-104">Bu derste, Azure Analysis Services sunucusunun model için bir ad belirtmesini sağlayarak dağıtım özelliklerini yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="fda62-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="fda62-105">Daha sonra modeli bu örneğe dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="fda62-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="fda62-106">Modeliniz dağıtıldıktan sonra kullanıcılar bir raporlama istemci uygulaması kullanarak modele bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fda62-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="fda62-107">Daha fazla bilgi için bkz. [Azure Analysis Services’a Dağıtma](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="fda62-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="fda62-108">Bu dersin tahmini tamamlanma süresi: **5 dakika**</span><span class="sxs-lookup"><span data-stu-id="fda62-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="fda62-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fda62-109">Prerequisites</span></span>  
<span data-ttu-id="fda62-110">Bu konu, sırayla tamamlanması gereken bir tablo modelleme öğreticisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="fda62-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="fda62-111">Bu dersteki görevleri gerçekleştirmeden önce, bir önceki dersi tamamlamış olmanız gerekir: [12. Ders: Excel’de çözümleme](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="fda62-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="fda62-112">Uzak Analysis Services sunucusunu dağıtmak için sunucu üzerinde [Yönetici izinlerine](../analysis-services-server-admins.md) sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fda62-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="fda62-113">AdventureWorksDW2014 örnek veritabanını şirket içi bir SQL Server’a yüklediyseniz ve modelinizi bir Azure Analysis Services sunucusuna dağıtacaksanız [Şirket içi veri ağ geçidi](../analysis-services-gateway.md) gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fda62-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="fda62-114">Modeli dağıtma</span><span class="sxs-lookup"><span data-stu-id="fda62-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="fda62-115">Dağıtım özelliklerini yapılandırmak için</span><span class="sxs-lookup"><span data-stu-id="fda62-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="fda62-116">**Çözüm Gezgini**’nde **AW İnternet Satışları** projesine sağ tıklayıp **Özellikler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda62-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="fda62-117">**AW İnternet Satışları Özellik Sayfaları** iletişim kutusundaki **Dağıtım Sunucusu** altında bulunan **Server** özelliğine tüm sunucuyu girin.</span><span class="sxs-lookup"><span data-stu-id="fda62-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="fda62-119">**Database** özelliğine **Adventure Works İnternet Satışları** yazın.</span><span class="sxs-lookup"><span data-stu-id="fda62-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="fda62-120">**Model Name** özelliğine **Adventure Works İnternet Satışları Modeli** yazın.</span><span class="sxs-lookup"><span data-stu-id="fda62-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="fda62-121">Seçimlerinizi doğrulayıp **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda62-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="fda62-122">Adventure Works İnternet Satışlarını dağıtmak için</span><span class="sxs-lookup"><span data-stu-id="fda62-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="fda62-123">**Çözüm Gezgini**’nde **AW İnternet Satışları** projesine sağ tıklayıp **Derleme**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda62-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="fda62-124">**AW İnternet Satışları** projesine sağ tıklayıp **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda62-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="fda62-125">Azure Analysis Services'a dağıtım yaparken hesabınızı girmeniz istenebilir.</span><span class="sxs-lookup"><span data-stu-id="fda62-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="fda62-126">Kuruluş hesabınızı ve parolanızı girin, örneğin nancy@adventureworks.com. Bu hesap, sunucudaki Yöneticiler grubuna üye olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fda62-126">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="fda62-127">Dağıtım iletişim kutusu görünür ve burada meta veriler ile modele dahil edilen her tablonun dağıtım durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fda62-127">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="fda62-129">Dağıtım başarıyla tamamlandığında devam edin ve **Kapat**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fda62-129">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="fda62-130">Sonuç</span><span class="sxs-lookup"><span data-stu-id="fda62-130">Conclusion</span></span>  
<span data-ttu-id="fda62-131">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="fda62-131">Congratulations!</span></span> <span data-ttu-id="fda62-132">İlk Analysis Services Tablo modelinizi yazma ve dağıtma işlemini tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="fda62-132">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="fda62-133">Bu öğretici, bir tablo modeli oluştururken en yaygın görevleri tamamlamanıza yardımcı olmuştur.</span><span class="sxs-lookup"><span data-stu-id="fda62-133">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="fda62-134">Adventure Works İnternet Satışları modeliniz artık dağıtıldığına göre SQL Server Management Studio’yu kullanarak modeli yönetebilir, işlem betikleri ve bir yedek plan oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fda62-134">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="fda62-135">Kullanıcılar artık ayrıca Microsoft Excel veya Power BI gibi bir raporlama istemci uygulaması kullanarak modele bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="fda62-135">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="fda62-137">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="fda62-137">What's next?</span></span>
<span data-ttu-id="fda62-138">[Power BI Desktop ile bağlanma](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="fda62-138">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="fda62-139">[Ek Ders - Dinamik güvenlik](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="fda62-139">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="fda62-140">[Ek Ders - Ayrıntı satırları](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="fda62-140">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="fda62-141">Ek Ders - Düzensiz hiyerarşiler</span><span class="sxs-lookup"><span data-stu-id="fda62-141">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
