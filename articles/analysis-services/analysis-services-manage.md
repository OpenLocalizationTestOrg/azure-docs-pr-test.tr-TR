---
title: Azure Analysis Services aaaManage | Microsoft Docs
description: "Toomanage Analiz Hizmetleri nasıl öğrenin Azure sunucusu."
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
ms.openlocfilehash: b03bc440801a68162039e28cdb4f863da374014e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-analysis-services"></a><span data-ttu-id="6cadb-103">Çözümleme Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="6cadb-103">Manage Analysis Services</span></span>
<span data-ttu-id="6cadb-104">Azure'da bir Analysis Services sunucusuna oluşturduktan sonra bazı yönetim görevleri tooperform hemen gerekir ya da süre aşağı hello yol olabilir.</span><span class="sxs-lookup"><span data-stu-id="6cadb-104">Once you've created an Analysis Services server in Azure, there may be some administration and management tasks you need tooperform right away or sometime down hello road.</span></span> <span data-ttu-id="6cadb-105">Örneğin, toohello yenileme verileri, sunucunuzdaki hello modelleri erişebilir veya sunucunuzun sistem durumu izleme kimin işlemeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6cadb-105">For example, run processing toohello refresh data, control who can access hello models on your server, or monitor your server's health.</span></span> <span data-ttu-id="6cadb-106">Bazı yönetim görevleri, Azure portalında, diğerleri de SQL Server Management Studio (SSMS), yalnızca gerçekleştirilebilir ve bazı görevler ya da gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6cadb-106">Some management tasks can only be performed in Azure portal, others in SQL Server Management Studio (SSMS), and some tasks can be done in either.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="6cadb-107">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="6cadb-107">Azure portal</span></span>
<span data-ttu-id="6cadb-108">[Azure portal](http://portal.azure.com/) , oluşturmak ve sunucuları silin, sunucu kaynaklarını izlemek, boyutunu değiştirmek ve erişim tooyour sunucuları olanların yönetmek yerdir.</span><span class="sxs-lookup"><span data-stu-id="6cadb-108">[Azure portal](http://portal.azure.com/) is where you can create and delete servers, monitor server resources, change size, and manage who has access tooyour servers.</span></span>  <span data-ttu-id="6cadb-109">Bazı sorunlar yaşıyorsanız, ayrıca bir destek isteği gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cadb-109">If you're having some problems, you can also submit a support request.</span></span>

![Azure'da sunucu adını alma](./media/analysis-services-manage/aas-manage-portal.png)

## <a name="sql-server-management-studio"></a><span data-ttu-id="6cadb-111">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="6cadb-111">SQL Server Management Studio</span></span>
<span data-ttu-id="6cadb-112">Azure'da tooyour sunucusuyla bağlantı kuruluyor yalnızca tooa server örneği veya kendi kuruluşunuzdaki bağlanma gibi olur.</span><span class="sxs-lookup"><span data-stu-id="6cadb-112">Connecting tooyour server in Azure is just like connecting tooa server instance in your own organization.</span></span> <span data-ttu-id="6cadb-113">SSMS aynı işlem verileri gibi görevleri veya bir işleme betiği oluşturmak, rolleri yönetmek ve PowerShell kullanmak hello çoğunu gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cadb-113">From SSMS, you can perform many of hello same tasks such as process data or create a processing script, manage roles, and use PowerShell.</span></span>
  
![SQL Server Management Studio](./media/analysis-services-manage/aas-manage-ssms.png)

### <a name="download-and-install-ssms"></a><span data-ttu-id="6cadb-115">SSMS yükleyip</span><span class="sxs-lookup"><span data-stu-id="6cadb-115">Download and install SSMS</span></span>
<span data-ttu-id="6cadb-116">tooget tüm son özellikleri ve hello en yumuşak deneyimi tooyour Azure Analysis Services sunucusuna bağlanırken Merhaba, hello SSMS en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6cadb-116">tooget all hello latest features, and hello smoothest experience when connecting tooyour Azure Analysis Services server, be sure you're using hello latest version of SSMS.</span></span> 

<span data-ttu-id="6cadb-117">[SQL Server Management Studio'yu indirme](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="6cadb-117">[Download SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span>


### <a name="tooconnect-with-ssms"></a><span data-ttu-id="6cadb-118">SSMS ile tooconnect</span><span class="sxs-lookup"><span data-stu-id="6cadb-118">tooconnect with SSMS</span></span>
 <span data-ttu-id="6cadb-119">SSMS, bağlanan tooyour sunucu hello ilk kez önce kullanırken, kullanıcı adınızı hello Analysis Services Yöneticiler grubunda bulunduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="6cadb-119">When using SSMS, before connecting tooyour server hello first time, make sure your username is included in hello Analysis Services Admins group.</span></span> <span data-ttu-id="6cadb-120">toolearn daha, fazla [sunucu yöneticileri](#server-administrators) bu makalenin ilerisinde yer.</span><span class="sxs-lookup"><span data-stu-id="6cadb-120">toolearn more, see [Server administrators](#server-administrators) later in this article.</span></span>

1. <span data-ttu-id="6cadb-121">Bağlanmadan önce tooget hello sunucu adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6cadb-121">Before you connect, you need tooget hello server name.</span></span> <span data-ttu-id="6cadb-122">İçinde **Azure portal** > server > **genel bakış** > **sunucu adı**, kopya hello sunucu adı.</span><span class="sxs-lookup"><span data-stu-id="6cadb-122">In **Azure portal** > server > **Overview** > **Server name**, copy hello server name.</span></span>
   
    ![Azure'da sunucu adını alma](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. <span data-ttu-id="6cadb-124">SSMS içinde > **Object Explorer**, tıklatın **Bağlan** > **Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="6cadb-124">In SSMS > **Object Explorer**, click **Connect** > **Analysis Services**.</span></span>
3. <span data-ttu-id="6cadb-125">Merhaba, **tooServer bağlanmak** iletişim kutusu, Yapıştır hello sunucu adını, sonra da **kimlik doğrulaması**, şu kimlik doğrulama türlerini hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="6cadb-125">In hello **Connect tooServer** dialog box, paste in hello server name, then in **Authentication**, choose one of hello following authentication types:</span></span>
   
    <span data-ttu-id="6cadb-126">**Windows kimlik doğrulaması** toouse Windows etki alanı\kullanıcı adı ve parola bilgileriniz.</span><span class="sxs-lookup"><span data-stu-id="6cadb-126">**Windows Authentication** toouse your Windows domain\username and password credentials.</span></span>

    <span data-ttu-id="6cadb-127">**Active Directory parola kimlik doğrulaması** toouse bir kurumsal hesap.</span><span class="sxs-lookup"><span data-stu-id="6cadb-127">**Active Directory Password Authentication** toouse an organizational account.</span></span> <span data-ttu-id="6cadb-128">Örneğin, ne zaman bir etki bağlanma bilgisayar katıldı.</span><span class="sxs-lookup"><span data-stu-id="6cadb-128">For example, when connecting from a non-domain joined computer.</span></span>

    <span data-ttu-id="6cadb-129">**Active Directory Evrensel kimlik doğrulaması** toouse [etkileşimli olmayan veya çok faktörlü kimlik doğrulaması](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="6cadb-129">**Active Directory Universal Authentication** toouse [non-interactive or multi-factor authentication](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span> 
   
    ![SSMS bağlanma](./media/analysis-services-manage/aas-manage-connect-ssms.png)

## <a name="server-administrators-and-database-users"></a><span data-ttu-id="6cadb-131">Sunucu yöneticileri ve veritabanı kullanıcısı</span><span class="sxs-lookup"><span data-stu-id="6cadb-131">Server administrators and database users</span></span>
<span data-ttu-id="6cadb-132">Azure Analysis Services içinde kullanıcılar, Yöneticiler ve veritabanı kullanıcılarını iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="6cadb-132">In Azure Analysis Services, there are two types of users, server administrators and database users.</span></span> <span data-ttu-id="6cadb-133">Her iki tür kullanıcı Azure Active Directory'yi olmalıdır ve kurumsal e-posta adresi veya UPN ile belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="6cadb-133">Both types of users must be in your Azure Active Directory and must be specified by organizational email address or UPN.</span></span> <span data-ttu-id="6cadb-134">toolearn daha, fazla [kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="6cadb-134">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>


## <a name="troubleshooting-connection-problems"></a><span data-ttu-id="6cadb-135">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="6cadb-135">Troubleshooting connection problems</span></span>
<span data-ttu-id="6cadb-136">Sorunlarla karşılaşırsanız, SSMS, kullanarak bağlanırken, tooclear hello oturum açma önbellek gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="6cadb-136">When connecting using SSMS, if you run into problems, you may need tooclear hello login cache.</span></span> <span data-ttu-id="6cadb-137">Önbelleğe alınan toodisc doğrudur.</span><span class="sxs-lookup"><span data-stu-id="6cadb-137">Nothing is cached toodisc.</span></span> <span data-ttu-id="6cadb-138">tooclear hello önbellek, kapatın ve yeniden başlatma hello işlem bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6cadb-138">tooclear hello cache, close and restart hello connect process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6cadb-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6cadb-139">Next steps</span></span>
<span data-ttu-id="6cadb-140">Tablo modeli tooyour yeni bir sunucu zaten dağıttıysanız yapmadıysanız, iyi bir zamandır sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="6cadb-140">If you haven't already deployed a tabular model tooyour new server, now is a good time.</span></span> <span data-ttu-id="6cadb-141">toolearn daha, fazla [tooAzure Analysis Services dağıtma](analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6cadb-141">toolearn more, see [Deploy tooAzure Analysis Services](analysis-services-deploy.md).</span></span>

<span data-ttu-id="6cadb-142">Bir model tooyour sunucusu dağıttıktan sonra bir istemci veya tarayıcı kullanarak hazır tooconnect tooit demektir.</span><span class="sxs-lookup"><span data-stu-id="6cadb-142">If you've deployed a model tooyour server, you're ready tooconnect tooit using a client or browser.</span></span> <span data-ttu-id="6cadb-143">toolearn daha, fazla [veri Azure Analysis Services sunucusundan alma](analysis-services-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6cadb-143">toolearn more, see [Get data from Azure Analysis Services server](analysis-services-connect.md).</span></span>

