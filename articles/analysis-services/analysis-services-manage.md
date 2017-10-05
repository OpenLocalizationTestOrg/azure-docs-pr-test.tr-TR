---
title: "Azure Analysis Services yönetme | Microsoft Docs"
description: "Bir Analysis Services sunucusuna Azure yönetmeyi öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 79491d0b-b00d-4e02-9ca7-adc99bc02fdb
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: b897e81351ebee11c292e67ac76ba8202a6f0108
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="2bcff-103">Çözümleme Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="2bcff-103">Manage Analysis Services</span></span>
<span data-ttu-id="2bcff-104">Azure'da bir Analysis Services sunucusuna oluşturduktan sonra hemen veya süre yol gerçekleştirmeniz gereken bazı yönetim görevleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="2bcff-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need to perform right away or sometime down the road.</span></span> <span data-ttu-id="2bcff-105">Örneğin, sunucunuz modellerinde erişim veya sunucunuzun sistem durumu izleme kimin yenileme veri işlemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2bcff-105">For example, run processing to the refresh data, control who can access the models on your server, or monitor your server's health.</span></span> <span data-ttu-id="2bcff-106">Bazı yönetim görevleri, Azure portalında, diğerleri de SQL Server Management Studio (SSMS), yalnızca gerçekleştirilebilir ve bazı görevler ya da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2bcff-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="2bcff-107">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="2bcff-107">Azure portal</span></span>
<span data-ttu-id="2bcff-108">[Azure portal](http://portal.azure.com/) , oluşturmak ve sunucuları silin, sunucu kaynaklarını izlemek, boyutunu değiştirmek ve sunucularınızın kimlerin erişebileceğini yönetmek yerdir.</span><span class="sxs-lookup"><span data-stu-id="2bcff-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access to your servers.</span></span>  <span data-ttu-id="2bcff-109">Bazı sorunlar yaşıyorsanız, ayrıca bir destek isteği gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2bcff-109">If you're having some problems, you can also submit a support request.</span></span>

![Azure'da sunucu adını alma](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="2bcff-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="2bcff-111">SQL Server Management Studio</span></span>
<span data-ttu-id="2bcff-112">Azure'da sunucunuza bağlanma yalnızca bir sunucu örneği veya kendi kuruluşunuzdaki bağlanma gibi olur.</span><span class="sxs-lookup"><span data-stu-id="2bcff-112">Connecting to your server in Azure is just like connecting to a server instance in your own organization.</span></span> <span data-ttu-id="2bcff-113">SSMS verileri işlemek gibi gerçekleştirdiğiniz görevlerin çoğunu gerçekleştirmek veya bir işleme betiği oluşturmak, rolleri yönetebilir ve PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bcff-113">From SSMS, you can perform many of the same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="2bcff-115">SSMS yükleyip</span><span class="sxs-lookup"><span data-stu-id="2bcff-115">Download and install SSMS</span></span>
<span data-ttu-id="2bcff-116">Tüm almak için en son özellikleri ve Azure Analysis Services sunucusuna bağlanırken en yumuşak deneyimi SSMS en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2bcff-116">To get all the latest features, and the smoothest experience when connecting to your Azure Analysis Services server, be sure you're using the latest version of SSMS.</span></span> 

<span data-ttu-id="2bcff-117">[SQL Server Management Studio'yu indirme](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="2bcff-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="to-connect-with-ssms"></a><span data-ttu-id="2bcff-118">SSMS ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="2bcff-118">To connect with SSMS</span></span>
 <span data-ttu-id="2bcff-119">SSMS, sunucunuza ilk kez bağlanmadan önce kullanırken, kullanıcı adınızı Analysis Services Yöneticiler grubunda bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2bcff-119">When using SSMS, before connecting to your server the first time, make sure your username is included in the Analysis Services Admins group.</span></span> <span data-ttu-id="2bcff-120">Daha fazla bilgi için bkz: [sunucu yöneticileri](#server-administrators) bu makalenin ilerisinde yer.</span><span class="sxs-lookup"><span data-stu-id="2bcff-120">To learn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="2bcff-121">Bağlanmadan önce sunucu adını almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bcff-121">Before you connect, you need to get the server name.</span></span> <span data-ttu-id="2bcff-122">**Azure portalı** > sunucu > **Genel Bakış** > **Sunucu adı** menüsünde sunucu adını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="2bcff-122">In **Azure portal** > server > **Overview** > **Server name**, copy the server name.</span></span>
   
    ![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="2bcff-124">SSMS içinde > **Object Explorer**, tıklatın **Bağlan** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="2bcff-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="2bcff-125">İçinde **sunucuya Bağlan** iletişim kutusu, sunucu adının, sonra da Yapıştır **kimlik doğrulaması**, aşağıdaki kimlik doğrulama türlerinden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="2bcff-125">In the **Connect to Server** dialog box, paste in the server name, then in **Authentication**, choose one of the following authentication types:</span></span>
   
    <span data-ttu-id="2bcff-126">**Windows kimlik doğrulaması** Windows etki alanı\kullanıcı adı ve parola bilgileriniz kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="2bcff-126">**Windows Authentication** to use your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="2bcff-127">**Active Directory parola kimlik doğrulaması** kurumsal bir hesap kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="2bcff-127">**Active Directory Password Authentication** to use an organizational account.</span></span> <span data-ttu-id="2bcff-128">Örneğin, ne zaman bir etki bağlanma bilgisayar katıldı.</span><span class="sxs-lookup"><span data-stu-id="2bcff-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="2bcff-129">**Active Directory Evrensel kimlik doğrulaması** kullanmak için [etkileşimli olmayan veya çok faktörlü kimlik doğrulaması](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2bcff-129">**Active Directory Universal Authentication** to use [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![SSMS bağlanma](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="2bcff-131">Sunucu yöneticileri ve veritabanı kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="2bcff-131">Server administrators and database users</span></span>
<span data-ttu-id="2bcff-132">Azure Analysis Services içinde kullanıcılar, Yöneticiler ve veritabanı kullanıcılarını iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="2bcff-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="2bcff-133">Her iki tür kullanıcı Azure Active Directory'yi olmalıdır ve kurumsal e-posta adresi veya UPN ile belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="2bcff-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="2bcff-134">Daha fazla bilgi edinmek için bkz. [Kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="2bcff-134">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="2bcff-135">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2bcff-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="2bcff-136">Sorunlarla karşılaşırsanız, SSMS, kullanarak bağlanırken, oturum açma önbelleğini temizlemek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2bcff-136">When connecting using SSMS, if you run into problems, you may need to clear the login cache.</span></span> <span data-ttu-id="2bcff-137">Hiçbir şey önbelleğe diske. Önbelleği temizlemek için kapatın ve bağlanma işlemi başlatın.</span><span class="sxs-lookup"><span data-stu-id="2bcff-137">Nothing is cached to disc. To clear the cache, close and restart the connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2bcff-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2bcff-138">Next steps</span></span>
<span data-ttu-id="2bcff-139">Tablo modeli yeni sunucunuza zaten dağıttıysanız yapmadıysanız, iyi bir zamandır sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="2bcff-139">If you haven't already deployed a tabular model to your new server, now is a good time.</span></span> <span data-ttu-id="2bcff-140">Daha fazla bilgi için bkz. [Azure Analysis Services’a Dağıtma](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2bcff-140">To learn more, see [Deploy to Azure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="2bcff-141">Sunucunuza bir model dağıttıktan sonra bir istemci veya tarayıcı kullanarak bağlanmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="2bcff-141">If you've deployed a model to your server, you're ready to connect to it using a client or browser.</span></span> <span data-ttu-id="2bcff-142">Daha fazla bilgi için bkz: [veri Azure Analysis Services sunucusundan alma](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2bcff-142">To learn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

