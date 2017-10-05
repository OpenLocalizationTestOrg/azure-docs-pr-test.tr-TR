---
title: "SSDT kullanarak Azure Analysis Services'e dağıtma | Microsoft Docs"
description: "SSDT kullanarak bir tablo modelini Azure Analysis Services sunucusuna dağıtma hakkında bilgi edinin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e9a3aedfb6e55696e1525e226fada1062fd5eda8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="4e884-103">SSDT’den model dağıtma</span><span class="sxs-lookup"><span data-stu-id="4e884-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="4e884-104">Azure aboneliğinizde bir sunucu oluşturduktan sonra, aboneliğinize bir tablo modeli dağıtmaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="4e884-104">Once you've created a server in your Azure subscription, you're ready to deploy a tabular model database to it.</span></span> <span data-ttu-id="4e884-105">Üzerinde çalışmakta olduğunuz bir tablo modeli projesini derleyip dağıtmak için SQL Server Veri Araçları’nı (SSDT) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e884-105">You can use SQL Server Data Tools (SSDT) to build and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4e884-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e884-106">Prerequisites</span></span>
<span data-ttu-id="4e884-107">Başlamak için gerekli olanlar:</span><span class="sxs-lookup"><span data-stu-id="4e884-107">To get started, you need:</span></span>

* <span data-ttu-id="4e884-108">Azure’da **Analysis Services sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="4e884-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="4e884-109">Daha fazla bilgi için bkz. [Azure Analysis Services sunucusu oluşturma](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="4e884-109">To learn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="4e884-110">SSDT’deki **tablosal model projesi** ya da 1200 veya üzeri uyumluluk düzeyine sahip mevcut bir tablosal model.</span><span class="sxs-lookup"><span data-stu-id="4e884-110">**Tabular model project** in SSDT or an existing tabular model at the 1200 or higher compatibility level.</span></span> <span data-ttu-id="4e884-111">Daha önce hiç oluşturmadınız mı?</span><span class="sxs-lookup"><span data-stu-id="4e884-111">Never created one?</span></span> <span data-ttu-id="4e884-112">[Adventure Works İnternet satışı tablosal modelleme öğreticisini](https://msdn.microsoft.com/library/hh231691.aspx) deneyin.</span><span class="sxs-lookup"><span data-stu-id="4e884-112">Try the [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="4e884-113">**Şirket içi ağ geçidi** - Bir veya daha fazla veri kaynağı kuruluşunuzun ağında şirket içi olarak bulunuyorsa bir [Şirket içi veri ağ geçidi](analysis-services-gateway.md) yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e884-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need to install an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="4e884-114">Ağ geçidi, buluttaki sunucunuzun modeldeki verileri işlemek ve yenilemek üzere şirket içi veri kaynaklarınıza bağlanması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4e884-114">The gateway is necessary for your server in the cloud connect to your on-premises data sources to process and refresh data in the model.</span></span>

> [!TIP]
> <span data-ttu-id="4e884-115">Dağıtmadan önce tablolarınızdaki verileri işleyebildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e884-115">Before you deploy, make sure you can process the data in your tables.</span></span> <span data-ttu-id="4e884-116">SSDT’de **Model** > **İşlem** > **Tümünü İşle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e884-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="4e884-117">İşleme başarısız olursa dağıtımı başarıyla yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="4e884-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="to-deploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="4e884-118">SSDT’den tablo modeli dağıtmak için</span><span class="sxs-lookup"><span data-stu-id="4e884-118">To deploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="4e884-119">Dağıtmadan önce sunucu adını almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e884-119">Before you deploy, you need to get the server name.</span></span> <span data-ttu-id="4e884-120">**Azure portalı** > sunucu > **Genel Bakış** > **Sunucu adı** menüsünde sunucu adını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4e884-120">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="4e884-122">SSDT > **Çözüm Gezgini** menüsünde projeye sağ tıklayın > **Özellikler**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e884-122">In SSDT > **Solution Explorer**, right-click the project > **Properties**.</span></span> <span data-ttu-id="4e884-123">Ardından **Dağıtım** > **Sunucu** alanına sunucu adını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="4e884-123">Then in **Deployment** > **Server** paste the server name.</span></span>   
   
    ![Sunucu adını dağıtım sunucusu özelliğine yapıştırma](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="4e884-125">**Çözüm Gezgini**’nde **Özellikler**’e sağ tıklayıp **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4e884-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="4e884-126">Azure'da oturum açmanız istenebilir.</span><span class="sxs-lookup"><span data-stu-id="4e884-126">You may be prompted to sign in to Azure.</span></span>
   
    ![Sunucuya dağıtma](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="4e884-128">Dağıtım durumu hem Çıktı penceresinde hem de Dağıt menüsünde görünür.</span><span class="sxs-lookup"><span data-stu-id="4e884-128">Deployment status appears in both the Output window and in Deploy.</span></span>
   
    ![Dağıtım durumu](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="4e884-130">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="4e884-130">That's all there is to it!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="4e884-131">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4e884-131">Troubleshooting</span></span>
<span data-ttu-id="4e884-132">Meta verileri dağıtırken dağıtım başarısız olursa, bunun nedeni SSDT’nin sunucunuza bağlanamaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e884-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect to your server.</span></span> <span data-ttu-id="4e884-133">SSMS kullanarak sunucunuza bağlanabildiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e884-133">Make sure you can connect to your server using SSMS.</span></span> <span data-ttu-id="4e884-134">Ardından projenin Deployment Server özelliğinin doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e884-134">Then make sure the Deployment Server property for the project is correct.</span></span>

<span data-ttu-id="4e884-135">Bir tabloda dağıtım başarısız olursa, bunun nedeni sunucunuzun bir veri kaynağına bağlanamaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e884-135">If deployment fails on a table, it's likely because your server couldn't connect to a data source.</span></span> <span data-ttu-id="4e884-136">Veri kaynağınız kuruluşunuzun ağında şirket içi olarak bulunuyorsa bir [Şirket içi veri ağ geçidi](analysis-services-gateway.md) yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e884-136">If your data source is on-premises in your organization's network, be sure to install an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e884-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e884-137">Next steps</span></span>
<span data-ttu-id="4e884-138">Tablo modelinizi sunucunuza dağıttığınıza göre bağlanmak için hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="4e884-138">Now that you have your tabular model deployed to your server, you're ready to connect to it.</span></span> <span data-ttu-id="4e884-139">[SSMS ile sunucunuza bağlanarak](analysis-services-manage.md) sunucuyu yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e884-139">You can [connect to it with SSMS](analysis-services-manage.md) to manage it.</span></span> <span data-ttu-id="4e884-140">Ayrıca, Power BI, Power BI Desktop veya Excel gibi [bir istemci araç kullanarak bağlanabilir](analysis-services-connect.md) ve rapor oluşturmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e884-140">And, you can [connect to it using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

