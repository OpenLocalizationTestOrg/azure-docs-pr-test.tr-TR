---
title: "Azure Active Directory denetim günlükleri ile günlük tümleştirme aaaAzure | Microsoft Docs"
description: "Nasıl tooinstall Azure günlük tümleştirme hizmeti hello ve Azure denetim günlükleri günlüklerinden tümleştirmek öğrenin"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="1655c-103">Azure Active Directory denetim günlüklerini tümleştirme</span><span class="sxs-lookup"><span data-stu-id="1655c-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="1655c-104">Azure Active Directory (Azure AD) denetim olayları Azure Active Directory'de oluştu ayrıcalıklı Eylemler belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1655c-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="1655c-105">Merhaba türlerini gözden geçirerek izleyebilirsiniz olayların görebilirsiniz [Azure Active Directory Denetim Raporu olayları](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span><span class="sxs-lookup"><span data-stu-id="1655c-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1655c-106">Bu makaledeki adımları hello çalışmadan önce hello gözden geçirmeniz gerekir [başlama](security-azure-log-integration-get-started.md) makalesi ve hello adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1655c-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="1655c-107">Adımları toointegrate Azure Active directory denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="1655c-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="1655c-108">Merhaba komut istemi açın ve şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1655c-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="1655c-109">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1655c-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="1655c-110">Bu komut için Azure oturum açma bilgilerinizi ister.</span><span class="sxs-lookup"><span data-stu-id="1655c-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="1655c-111">Merhaba komut sonra bir Azure Active Directory hizmet asıl hello Azure AD kiracılar oluşturur barındıran hello Azure abonelikleri hangi hello oturum açma kullanıcı olan bir yönetici, bir ortak yönetici veya bir sahip.</span><span class="sxs-lookup"><span data-stu-id="1655c-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="1655c-112">Merhaba oturum açmış kullanıcının yalnızca bir Konuk kullanıcı hello Azure AD kiracısında ise hello komut başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1655c-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="1655c-113">Kimlik doğrulama tooAzure Azure AD üzerinden yapılır.</span><span class="sxs-lookup"><span data-stu-id="1655c-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="1655c-114">Azure günlük tümleştirmesi için bir hizmet sorumlusu oluşturma hello erişim tooread Azure aboneliklerinden verilir Azure AD kimlik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1655c-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="1655c-115">Çalışma hello aşağıdaki tooprovide Kiracı kimliğinizi komutu.</span><span class="sxs-lookup"><span data-stu-id="1655c-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="1655c-116">Merhaba Kiracı Yönetici rolü toorun hello komutunu toobe üyesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1655c-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="1655c-117">Örnek:</span><span class="sxs-lookup"><span data-stu-id="1655c-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="1655c-118">Azure Active Directory denetim günlüğü JSON dosyalarını hello klasörleri tooconfirm aşağıdaki hello bunları oluşturulan denetleyin:</span><span class="sxs-lookup"><span data-stu-id="1655c-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="1655c-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="1655c-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="1655c-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="1655c-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="1655c-121">Merhaba aşağıdaki video bu makalede ele alınan hello adımları gösterir:</span><span class="sxs-lookup"><span data-stu-id="1655c-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="1655c-122">Merhaba bilgi hello JSON dosyalarında güvenlik bilgileri ve Olay yönetimi (SIEM) sistemi hale getirme ile ilgili ayrıntılı yönergeler için SIEM satıcınıza başvurun.</span><span class="sxs-lookup"><span data-stu-id="1655c-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="1655c-123">Topluluk Yardım hello kullanılabilir [Azure günlük tümleştirme MSDN Forumu](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span><span class="sxs-lookup"><span data-stu-id="1655c-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="1655c-124">Bu forumda kişilerin hello Azure günlük tümleştirme topluluk toosupport içinde birbirlerine sorular, yanıtlar, ipuçları ve püf noktaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="1655c-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="1655c-125">Ayrıca, hello Azure günlük tümleştirme takım Bu forumda izler ve mümkün olduğunca yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1655c-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="1655c-126">Ayrıca açabilirsiniz bir [destek isteği](../azure-supportability/how-to-create-azure-support-request.md).</span><span class="sxs-lookup"><span data-stu-id="1655c-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="1655c-127">Seçin **günlük tümleştirme** destek isteyen hello hizmet olarak.</span><span class="sxs-lookup"><span data-stu-id="1655c-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1655c-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1655c-128">Next steps</span></span>
<span data-ttu-id="1655c-129">Azure günlük tümleştirme hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="1655c-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="1655c-130">[Microsoft Azure günlük tümleştirme Azure günlükleri için](https://www.microsoft.com/download/details.aspx?id=53324): Bu Yükleme Merkezi sayfası ayrıntıları, sistem gereksinimleri ve yükleme yönergeleri için Azure günlük tümleştirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="1655c-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="1655c-131">[Giriş tooAzure günlük tümleştirme](security-azure-log-integration-overview.md): Bu makalede tooAzure günlük tümleştirme, önemli işlevleri ve nasıl çalıştığı tanıtılır.</span><span class="sxs-lookup"><span data-stu-id="1655c-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="1655c-132">[Ortak yapılandırma adımları](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): Bu blog gönderisine nasıl tooconfigure Azure günlük tümleştirme toowork ile iş ortağı çözümleri Splunk, HP ArcSight ve IBM QRadar gösterir.</span><span class="sxs-lookup"><span data-stu-id="1655c-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="1655c-133">[Azure günlük tümleştirme SSS](security-azure-log-integration-faq.md): Bu makalede Azure günlük tümleştirmesi hakkında sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1655c-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="1655c-134">[Güvenlik Merkezi uyarılarını Azure günlük tümleştirme ile tümleştirme](../security-center/security-center-integrating-alerts-with-log-integration.md): Bu makale size nasıl toosync Güvenlik Merkezi, sanal makine güvenlik olaylarını Azure tanılama ve günlük analizi ile Azure denetim günlükleri tarafından toplanan birlikte uyarıları gösterir veya SIEM çözümü.</span><span class="sxs-lookup"><span data-stu-id="1655c-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="1655c-135">[Azure tanılama ve Azure için yeni özellikler denetim günlüklerini](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): Bu blog gönderisine tooAzure denetim günlüklerini tanıtır ve yardımcı diğer özellikleri Azure kaynaklarınızı hello işlemlerini alın.</span><span class="sxs-lookup"><span data-stu-id="1655c-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
