---
title: "Azure SQL Azure otomasyonu kullanarak veritabanlarını aaaManage | Microsoft Docs"
description: "Hello Azure Otomasyon hizmetine ölçekte kullanılan toomanage Azure SQL veritabanı nasıl olabilir hakkında bilgi edinin."
services: sql-database, automation
documentationcenter: 
author: jodoglevy
manager: jhubbard
editor: monicar
ms.assetid: 77c262a1-9b93-456d-b3c7-b2f23bdfcd61
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: jhubbard
ms.openlocfilehash: d613cca32ba86e27b9c1b952c4e723ea7f07beb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="5fb56-103">Azure otomasyonu kullanarak Azure SQL veritabanlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="5fb56-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="5fb56-104">Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure SQL veritabanlarınızın kullanılan toosimplify yönetim nasıl çalıştırılabilir tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fb56-104">This guide will introduce you toohello Azure Automation service, and how it can be used toosimplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="5fb56-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="5fb56-105">What is Azure Automation?</span></span>
<span data-ttu-id="5fb56-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="5fb56-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="5fb56-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fb56-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated tooincrease reliability, efficiency, and time toovalue for your organization.</span></span>

<span data-ttu-id="5fb56-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi toomeet ölçeklendirilebilen bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fb56-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales toomeet your needs as your organization grows.</span></span> <span data-ttu-id="5fb56-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="5fb56-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="5fb56-110">İşletimsel ek yükü azaltmak ve boşaltmak BT / DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5fb56-110">Lower operational overhead and free up IT / DevOps staff toofocus on work that adds business value by moving your cloud management tasks toobe run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="5fb56-111">Azure Otomasyonu Azure SQL veritabanlarını yönetme nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="5fb56-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="5fb56-112">Azure SQL veritabanı yönetilebilir Azure Otomasyonu'nda hello kullanarak [Azure SQL Database PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) hello kullanılabilir [Azure PowerShell Araçları](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5fb56-112">Azure SQL Database can be managed in Azure Automation by using hello [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in hello [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="5fb56-113">Tüm SQL DB yönetim görevlerinizi hello hizmet içinde gerçekleştirebilmeniz azure Otomasyonu hello kutudan çıktığında, bu Azure SQL Database PowerShell cmdlet'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="5fb56-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of hello box, so that you can perform all of your SQL DB management tasks within hello service.</span></span> <span data-ttu-id="5fb56-114">Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fb56-114">You can also pair these cmdlets in Azure Automation with hello cmdlets for other Azure services, tooautomate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="5fb56-115">Azure Otomasyonu da hello özelliği toocommunicate SQL sunucuları ile doğrudan PowerShell kullanarak SQL komutları vererek sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5fb56-115">Azure Automation also has hello ability toocommunicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="5fb56-116">Merhaba [Azure Otomasyonu runbook Galerisi](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) Azure SQL veritabanları, diğer Azure Hizmetleri ve 3. taraf sistemi yönetimi otomatikleştirme başlatılan ürün ekibi ve topluluk runbook'lar tooget çeşitli içerir.</span><span class="sxs-lookup"><span data-stu-id="5fb56-116">hello [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks tooget started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="5fb56-117">Galeri runbook'ları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="5fb56-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="5fb56-118">Bir SQL Server veritabanında SQL sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="5fb56-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="5fb56-119">(Yukarı veya aşağı) dikey olarak ölçeklendirmek bir zamanlamaya göre bir Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="5fb56-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="5fb56-120">Veritabanı boyut üst sınırına yaklaşıyor varsa bir SQL tablosunu kesme</span><span class="sxs-lookup"><span data-stu-id="5fb56-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="5fb56-121">Yüksek oranda parçalanmış varsa bir Azure SQL veritabanı tablolarında dizin</span><span class="sxs-lookup"><span data-stu-id="5fb56-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="5fb56-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5fb56-122">Next steps</span></span>
<span data-ttu-id="5fb56-123">Azure Otomasyonu ve kullanılan toomanage Azure SQL veritabanı nasıl olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.</span><span class="sxs-lookup"><span data-stu-id="5fb56-123">Now that you've learned hello basics of Azure Automation and how it can be used toomanage Azure SQL databases, follow these links toolearn more about Azure Automation.</span></span>

* [<span data-ttu-id="5fb56-124">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="5fb56-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="5fb56-125">İlk runbook’um</span><span class="sxs-lookup"><span data-stu-id="5fb56-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="5fb56-126">Azure Otomasyonu öğrenme Haritası</span><span class="sxs-lookup"><span data-stu-id="5fb56-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="5fb56-127">Azure Otomasyonu: Hello bulut içinde SQL Agent</span><span class="sxs-lookup"><span data-stu-id="5fb56-127">Azure Automation: Your SQL Agent in hello Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

