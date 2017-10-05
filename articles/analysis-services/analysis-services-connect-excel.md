---
title: "Azure Analysis Services Excel ile bağlanma | Microsoft Docs"
description: "Excel kullanarak bir Azure Analysis Services sunucusuna bağlanmak öğrenin."
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
ms.openlocfilehash: d51b6980120f1cf9bc8d053d463a73ac600b915f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-with-excel"></a><span data-ttu-id="c114c-103">Excel ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="c114c-103">Connect with Excel</span></span>

<span data-ttu-id="c114c-104">Azure üzerinde bir sunucu oluşturulur ve bir tablo modeline dağıtılmış sonra bağlanmak ve veri araştırmaya başlamak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="c114c-104">Once you've created a server in Azure, and deployed a tabular model to it, you're ready to connect and begin exploring data.</span></span>


## <a name="connect-in-excel"></a><span data-ttu-id="c114c-105">Excel'de Bağlan</span><span class="sxs-lookup"><span data-stu-id="c114c-105">Connect in Excel</span></span>

<span data-ttu-id="c114c-106">Excel'de sunucusuna bağlanan Excel 2016'da Veri Al kullanılarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c114c-106">Connecting to a server in Excel is supported by using Get Data in Excel 2016.</span></span> <span data-ttu-id="c114c-107">Power Pivot Tablo Alma Sihirbazı'nı kullanarak bağlanması desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="c114c-107">Connecting by using the Import Table Wizard in Power Pivot is not supported.</span></span> 

<span data-ttu-id="c114c-108">**Excel 2016'da bağlanmak için**</span><span class="sxs-lookup"><span data-stu-id="c114c-108">**To connect in Excel 2016**</span></span>

1. <span data-ttu-id="c114c-109">2016, üzerinde Excel **veri** Şerit, tıklatın **dış veri al** > **diğer kaynaklardan** > **Çözümleme Hizmetleri'nden** .</span><span class="sxs-lookup"><span data-stu-id="c114c-109">In Excel 2016, on the **Data** ribbon, click **Get External Data** > **From Other Sources** > **From Analysis Services**.</span></span>

2. <span data-ttu-id="c114c-110">Veri Bağlantı Sihirbazı ' nda içinde **sunucu adı**, protokol ve URI'sini de dahil olmak üzere sunucu adı girin.</span><span class="sxs-lookup"><span data-stu-id="c114c-110">In the Data Connection Wizard, in **Server name**, enter the server name including protocol and URI.</span></span> <span data-ttu-id="c114c-111">Ardından **oturum açma kimlik bilgileri**seçin **aşağıdaki kullanıcı adını ve parolayı kullan**ve kuruluş kullanıcı adı, örneğin yazın nancy@adventureworks.comve parola.</span><span class="sxs-lookup"><span data-stu-id="c114c-111">Then, in **Logon credentials**, select **Use the following User Name and Password**, and then type the organizational user name, for example nancy@adventureworks.com, and password.</span></span>

    ![Excel oturumu açma bağlanma](./media/analysis-services-connect-excel/aas-connect-excel-logon.png)

3. <span data-ttu-id="c114c-113">İçinde **veritabanı ve Tablo Seç**, veritabanı ve model veya perspektif seçin ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="c114c-113">In **Select Database and Table**, select the database and model or perspective, and then click **Finish**.</span></span>
   
    ![Excel select modelden Bağlan](./media/analysis-services-connect-excel/aas-connect-excel-select.png)


## <a name="see-also"></a><span data-ttu-id="c114c-115">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c114c-115">See also</span></span>
<span data-ttu-id="c114c-116">[İstemci kitaplıkları](analysis-services-data-providers.md) </span><span class="sxs-lookup"><span data-stu-id="c114c-116">[Client libraries](analysis-services-data-providers.md) </span></span>  
[<span data-ttu-id="c114c-117">Sunucunuzu Yönetin</span><span class="sxs-lookup"><span data-stu-id="c114c-117">Manage your server</span></span>](analysis-services-manage.md)     


