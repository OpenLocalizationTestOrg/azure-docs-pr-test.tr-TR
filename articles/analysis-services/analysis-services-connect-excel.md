---
title: aaaConnect tooAzure Analysis Services Excel ile | Microsoft Docs
description: "Nasıl tooconnect tooan Azure Analysis Services öğrenin Excel kullanarak sunucu."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 175b83e7d936716a626aa4b3bf22b5598bb983d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="21c3d-103">Excel ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="21c3d-103">Connect with Excel</span></span>

<span data-ttu-id="21c3d-104">Bir sunucu Azure içinde oluşturulan ve dağıtılan bir tablo modeli tooit sonra hazır tooconnect olduğunuz ve veri araştırmaya başlamak.</span><span class="sxs-lookup"><span data-stu-id="21c3d-104">Once you've created a server in Azure, and deployed a tabular model tooit, you're ready tooconnect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="21c3d-105">Excel'de Bağlan</span><span class="sxs-lookup"><span data-stu-id="21c3d-105">Connect in Excel</span></span>

<span data-ttu-id="21c3d-106">Excel'de tooa sunucusuyla bağlantı kuruluyor Excel 2016'da Veri Al kullanılarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="21c3d-106">Connecting tooa server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="21c3d-107">Power Pivot Hello alma Tablo Sihirbazı'nı kullanarak bağlanması desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="21c3d-107">Connecting by using hello Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="21c3d-108">**Excel 2016 tooconnect**</span><span class="sxs-lookup"><span data-stu-id="21c3d-108">**tooconnect in Excel 2016**</span></span>

1. <span data-ttu-id="21c3d-109">Excel 2016'da, hello içinde **veri** Şerit, tıklatın **dış veri al** > **diğer kaynaklardan** > **Çözümleme Hizmetleri'nden** .</span><span class="sxs-lookup"><span data-stu-id="21c3d-109">In Excel 2016, on hello **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="21c3d-110">İçinde veri Bağlantı Sihirbazı ' hello **sunucu adı**, protokol ve URI'sini de dahil olmak üzere hello sunucu adı girin.</span><span class="sxs-lookup"><span data-stu-id="21c3d-110">In hello Data Connection Wizard, in **Server name**, enter hello server name including protocol and URI.</span></span> <span data-ttu-id="21c3d-111">Ardından **oturum açma kimlik bilgileri**seçin **kullanıcı adı ve parola aşağıdaki kullanım hello**ve hello kuruluş kullanıcı adı, örneğin yazın nancy@adventureworks.comve parola.</span><span class="sxs-lookup"><span data-stu-id="21c3d-111">Then, in **Logon credentials**, select **Use hello following User Name and Password**, and then type hello organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Excel oturumu açma bağlanma](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="21c3d-113">İçinde **veritabanı ve Tablo Seç**hello veritabanı ve model veya perspektif seçin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="21c3d-113">In **Select Database and Table**, select hello database and model or perspective, and then click **Finish**.</span></span>
   
    ![Excel select modelden Bağlan](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="21c3d-115">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="21c3d-115">See also</span></span>
<span data-ttu-id="21c3d-116">[İstemci kitaplıkları](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="21c3d-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="21c3d-117">Sunucunuzu Yönetin</span><span class="sxs-lookup"><span data-stu-id="21c3d-117">Manage your server</span></span>](analysis-services-manage.md)     


