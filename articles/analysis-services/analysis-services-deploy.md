---
title: SSDT kullanarak aaaDeploy tooAzure Analysis Services | Microsoft Docs
description: "Nasıl toodeploy tablolu model tooan Azure Analysis Services öğrenin SSDT kullanarak sunucu."
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
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a><span data-ttu-id="48b01-103">SSDT’den model dağıtma</span><span class="sxs-lookup"><span data-stu-id="48b01-103">Deploy a model from SSDT</span></span>
<span data-ttu-id="48b01-104">Bir sunucu, Azure aboneliğinizde oluşturduktan sonra hazır toodeploy tablolu model veritabanı tooit demektir.</span><span class="sxs-lookup"><span data-stu-id="48b01-104">Once you've created a server in your Azure subscription, you're ready toodeploy a tabular model database tooit.</span></span> <span data-ttu-id="48b01-105">SQL Server veri Araçları (SSDT) toobuild kullanabilir ve üzerinde çalıştığınız bir tablo modeli projesi dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48b01-105">You can use SQL Server Data Tools (SSDT) toobuild and deploy a tabular model project you're working on.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="48b01-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="48b01-106">Prerequisites</span></span>
<span data-ttu-id="48b01-107">başlatılan tooget, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="48b01-107">tooget started, you need:</span></span>

* <span data-ttu-id="48b01-108">Azure’da **Analysis Services sunucusu**.</span><span class="sxs-lookup"><span data-stu-id="48b01-108">**Analysis Services server** in Azure.</span></span> <span data-ttu-id="48b01-109">toolearn daha, fazla [Azure Analysis Services sunucusu oluşturmak](analysis-services-create-server.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-109">toolearn more, see [Create an Azure Analysis Services server](analysis-services-create-server.md).</span></span>
* <span data-ttu-id="48b01-110">**Tablo modeli projesi** SSDT ya da var olan bir tablo modeli hello 1200 veya daha yüksek uyumluluk düzeyinde.</span><span class="sxs-lookup"><span data-stu-id="48b01-110">**Tabular model project** in SSDT or an existing tabular model at hello 1200 or higher compatibility level.</span></span> <span data-ttu-id="48b01-111">Daha önce hiç oluşturmadınız mı?</span><span class="sxs-lookup"><span data-stu-id="48b01-111">Never created one?</span></span> <span data-ttu-id="48b01-112">Merhaba deneyin [Adventure Works Internet satış tablo modelleme Öğreticisi](https://msdn.microsoft.com/library/hh231691.aspx).</span><span class="sxs-lookup"><span data-stu-id="48b01-112">Try hello [Adventure Works Internet sales tabular modeling tutorial](https://msdn.microsoft.com/library/hh231691.aspx).</span></span>
* <span data-ttu-id="48b01-113">**Şirket içi ağ geçidi** -şirket içi kuruluşunuzun ağındaki bir veya daha fazla veri kaynağı varsa tooinstall gereken bir [şirket içi veri ağ geçidi](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-113">**On-premises gateway** - If one or more data sources are on-premises in your organization's network, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span> <span data-ttu-id="48b01-114">Merhaba bulutta sunucunuz bağlantısı için tooyour şirket içi veri kaynakları tooprocess ve yenileme veri hello modelinde hello ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="48b01-114">hello gateway is necessary for your server in hello cloud connect tooyour on-premises data sources tooprocess and refresh data in hello model.</span></span>

> [!TIP]
> <span data-ttu-id="48b01-115">Dağıtmadan önce tabloları hello verileri işleyebildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="48b01-115">Before you deploy, make sure you can process hello data in your tables.</span></span> <span data-ttu-id="48b01-116">SSDT’de **Model** > **İşlem** > **Tümünü İşle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48b01-116">In SSDT, click **Model** > **Process** > **Process All**.</span></span> <span data-ttu-id="48b01-117">İşleme başarısız olursa dağıtımı başarıyla yapamazsınız.</span><span class="sxs-lookup"><span data-stu-id="48b01-117">If processing fails, you cannot successfully deploy.</span></span>
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a><span data-ttu-id="48b01-118">toodeploy SSDT tablolu bir modelden</span><span class="sxs-lookup"><span data-stu-id="48b01-118">toodeploy a tabular model from SSDT</span></span>

1. <span data-ttu-id="48b01-119">Dağıtmadan önce tooget hello sunucu adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="48b01-119">Before you deploy, you need tooget hello server name.</span></span> <span data-ttu-id="48b01-120">İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, kopya hello sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="48b01-120">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="48b01-122">Ssdt'de > **Çözüm Gezgini**, sağ hello Proje > **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="48b01-122">In SSDT > **Solution Explorer**, right-click hello project > **Properties**.</span></span> <span data-ttu-id="48b01-123">Ardından **dağıtım** > **Server** hello sunucu adı yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="48b01-123">Then in **Deployment** > **Server** paste hello server name.</span></span>   
   
    ![Sunucu adını dağıtım sunucusu özelliğine yapıştırma](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. <span data-ttu-id="48b01-125">**Çözüm Gezgini**’nde **Özellikler**’e sağ tıklayıp **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48b01-125">In **Solution Explorer**, right-click **Properties**, then click **Deploy**.</span></span> <span data-ttu-id="48b01-126">İstendiğinde toosign tooAzure de olabilir.</span><span class="sxs-lookup"><span data-stu-id="48b01-126">You may be prompted toosign in tooAzure.</span></span>
   
    ![Tooserver dağıtma](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    <span data-ttu-id="48b01-128">Dağıtım durumu hem hello çıktı penceresinde ve Dağıt görünür.</span><span class="sxs-lookup"><span data-stu-id="48b01-128">Deployment status appears in both hello Output window and in Deploy.</span></span>
   
    ![Dağıtım durumu](./media/analysis-services-deploy/aas-deploy-status.png)

<span data-ttu-id="48b01-130">Tüm olan tooit yok!</span><span class="sxs-lookup"><span data-stu-id="48b01-130">That's all there is tooit!</span></span>


## <a name="troubleshooting"></a><span data-ttu-id="48b01-131">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="48b01-131">Troubleshooting</span></span>
<span data-ttu-id="48b01-132">Meta veri dağıtırken dağıtım başarısız olursa SSDT tooyour sunucu bağlanamadığımız için büyük olasılıkla olur.</span><span class="sxs-lookup"><span data-stu-id="48b01-132">If deployment fails when deploying metadata, it's likely because SSDT couldn't connect tooyour server.</span></span> <span data-ttu-id="48b01-133">SSMS kullanarak tooyour sunucusuna bağlanabildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="48b01-133">Make sure you can connect tooyour server using SSMS.</span></span> <span data-ttu-id="48b01-134">Ardından hello hello proje için dağıtım sunucusu özelliği doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="48b01-134">Then make sure hello Deployment Server property for hello project is correct.</span></span>

<span data-ttu-id="48b01-135">Bir tablo üzerinde dağıtım başarısız olursa sunucunuz tooa veri kaynağı bağlanamadığımız için büyük olasılıkla olur.</span><span class="sxs-lookup"><span data-stu-id="48b01-135">If deployment fails on a table, it's likely because your server couldn't connect tooa data source.</span></span> <span data-ttu-id="48b01-136">Veri kaynağınızı şirket içi kuruluşunuzun ağındaki emin tooinstall olması bir [şirket içi veri ağ geçidi](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="48b01-136">If your data source is on-premises in your organization's network, be sure tooinstall an [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48b01-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48b01-137">Next steps</span></span>
<span data-ttu-id="48b01-138">Tablo modeli dağıtılan tooyour sunucunuz sahip olduğunuza göre hazır tooconnect tooit demektir.</span><span class="sxs-lookup"><span data-stu-id="48b01-138">Now that you have your tabular model deployed tooyour server, you're ready tooconnect tooit.</span></span> <span data-ttu-id="48b01-139">Yapabilecekleriniz [tooit SSMS ile bağlanma](analysis-services-manage.md) toomanage onu.</span><span class="sxs-lookup"><span data-stu-id="48b01-139">You can [connect tooit with SSMS](analysis-services-manage.md) toomanage it.</span></span> <span data-ttu-id="48b01-140">Ve yapabilecekleriniz [tooit bir istemci araç kullanarak bağlanmak](analysis-services-connect.md) Power BI, Power BI Desktop veya Excel ve raporları oluşturma başlangıç gibi.</span><span class="sxs-lookup"><span data-stu-id="48b01-140">And, you can [connect tooit using a client tool](analysis-services-connect.md) like Power BI, Power BI Desktop, or Excel, and start creating reports.</span></span>

