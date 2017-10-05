---
title: "Azure otomasyonu kullanarak Azure SQL veritabanlarını yönetme | Microsoft Docs"
description: "Nasıl Azure Otomasyon hizmetine ölçekte Azure SQL veritabanını yönetmek için kullanılabilir hakkında bilgi edinin."
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
ms.openlocfilehash: 7f45b8b654691063823c13bee61e9bb874a6a13a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-sql-databases-using-azure-automation"></a><span data-ttu-id="e5b66-103">Azure otomasyonu kullanarak Azure SQL veritabanlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="e5b66-103">Managing Azure SQL Databases using Azure Automation</span></span>
<span data-ttu-id="e5b66-104">Bu kılavuz Azure Otomasyon hizmetine ve nasıl Azure SQL veritabanlarınızın yönetimini basitleştirmek için kullanılabilmesi için tanıtılacaktır.</span><span class="sxs-lookup"><span data-stu-id="e5b66-104">This guide will introduce you to the Azure Automation service, and how it can be used to simplify management of your Azure SQL databases.</span></span>

## <a name="what-is-azure-automation"></a><span data-ttu-id="e5b66-105">Azure Otomasyonu Nedir?</span><span class="sxs-lookup"><span data-stu-id="e5b66-105">What is Azure Automation?</span></span>
<span data-ttu-id="e5b66-106">[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="e5b66-106">[Azure Automation](https://azure.microsoft.com/services/automation/) is an Azure service for simplifying cloud management through process automation.</span></span> <span data-ttu-id="e5b66-107">Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri güvenilirlik, verimliliği ve kuruluşunuz için değer süre artırmak için otomatik olarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="e5b66-107">Using Azure Automation, long-running, manual, error-prone, and frequently repeated tasks can be automated to increase reliability, efficiency, and time to value for your organization.</span></span>

<span data-ttu-id="e5b66-108">Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi karşılayacak şekilde ölçekler bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5b66-108">Azure Automation provides a highly-reliable and highly-available workflow execution engine that scales to meet your needs as your organization grows.</span></span> <span data-ttu-id="e5b66-109">Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.</span><span class="sxs-lookup"><span data-stu-id="e5b66-109">In Azure Automation, processes can be kicked off manually, by 3rd-party systems, or at scheduled intervals so that tasks happen exactly when needed.</span></span>

<span data-ttu-id="e5b66-110">İşletimsel ek yükü azaltmak ve boşaltmak BT / iş ekler çalışmaları odaklanmaya DevOps personel değer Azure Automation'ın otomatik olarak çalıştırılmak üzere bulut yönetim görevlerinizi taşıyarak.</span><span class="sxs-lookup"><span data-stu-id="e5b66-110">Lower operational overhead and free up IT / DevOps staff to focus on work that adds business value by moving your cloud management tasks to be run automatically by Azure Automation.</span></span>

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a><span data-ttu-id="e5b66-111">Azure Otomasyonu Azure SQL veritabanlarını yönetme nasıl yardımcı olabilir?</span><span class="sxs-lookup"><span data-stu-id="e5b66-111">How can Azure Automation help manage Azure SQL databases?</span></span>
<span data-ttu-id="e5b66-112">Azure SQL veritabanı yönetilebilir Azure Otomasyonu'nda kullanarak [Azure SQL Database PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) kullanılabilir olan [Azure PowerShell Araçları](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5b66-112">Azure SQL Database can be managed in Azure Automation by using the [Azure SQL Database PowerShell cmdlets](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) that are available in the [Azure PowerShell tools](/powershell/azure/overview).</span></span> <span data-ttu-id="e5b66-113">Tüm SQL DB yönetim görevlerinizi hizmet içinde gerçekleştirebilmeniz azure Otomasyonu kutudan çıktığında, bu Azure SQL Database PowerShell cmdlet'leri vardır.</span><span class="sxs-lookup"><span data-stu-id="e5b66-113">Azure Automation has these Azure SQL Database PowerShell cmdlets available out of the box, so that you can perform all of your SQL DB management tasks within the service.</span></span> <span data-ttu-id="e5b66-114">Ayrıca Azure Automation bu cmdlet'leri Azure hizmeti ve 3. taraf sistemi arasında karmaşık görevleri otomatikleştirmek için diğer Azure Hizmetleri için cmdlet'leri ile eşleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5b66-114">You can also pair these cmdlets in Azure Automation with the cmdlets for other Azure services, to automate complex tasks across Azure services and 3rd party systems.</span></span>

<span data-ttu-id="e5b66-115">Azure Otomasyonu, ayrıca PowerShell kullanarak SQL komutları vererek SQL sunucuları ile doğrudan iletişim kurmak için özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e5b66-115">Azure Automation also has the ability to communicate with SQL servers directly, by issuing SQL commands using PowerShell.</span></span>

<span data-ttu-id="e5b66-116">[Azure Otomasyonu runbook Galerisi](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) Azure SQL veritabanları, diğer Azure Hizmetleri ve 3. taraf sistemi yönetimi otomatikleştirme başlamak için ürün ekibi ve topluluk runbook'lar çeşitli içerir.</span><span class="sxs-lookup"><span data-stu-id="e5b66-116">The [Azure Automation runbook gallery](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) contains a variety of product team and community runbooks to get started automating management of Azure SQL Databases, other Azure services, and 3rd party systems.</span></span> <span data-ttu-id="e5b66-117">Galeri runbook'ları şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="e5b66-117">Gallery runbooks include:</span></span>

* [<span data-ttu-id="e5b66-118">Bir SQL Server veritabanında SQL sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e5b66-118">Run SQL queries against a SQL Server database</span></span>](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [<span data-ttu-id="e5b66-119">(Yukarı veya aşağı) dikey olarak ölçeklendirmek bir zamanlamaya göre bir Azure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="e5b66-119">Vertically scale (up or down) an Azure SQL Database on a schedule</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [<span data-ttu-id="e5b66-120">Veritabanı boyut üst sınırına yaklaşıyor varsa bir SQL tablosunu kesme</span><span class="sxs-lookup"><span data-stu-id="e5b66-120">Truncate a SQL table if its database approaches its maximum size</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [<span data-ttu-id="e5b66-121">Yüksek oranda parçalanmış varsa bir Azure SQL veritabanı tablolarında dizin</span><span class="sxs-lookup"><span data-stu-id="e5b66-121">Index tables in an Azure SQL Database if they are highly fragmented</span></span>](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a><span data-ttu-id="e5b66-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5b66-122">Next steps</span></span>
<span data-ttu-id="e5b66-123">Azure Otomasyonu ve nasıl Azure SQL veritabanlarını yönetmek için kullanılmadan öğrendiğinize göre Azure Otomasyonu hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e5b66-123">Now that you've learned the basics of Azure Automation and how it can be used to manage Azure SQL databases, follow these links to learn more about Azure Automation.</span></span>

* [<span data-ttu-id="e5b66-124">Azure Otomasyonu genel bakış</span><span class="sxs-lookup"><span data-stu-id="e5b66-124">Azure Automation Overview</span></span>](../automation/automation-intro.md)
* [<span data-ttu-id="e5b66-125">İlk runbook’um</span><span class="sxs-lookup"><span data-stu-id="e5b66-125">My first runbook</span></span>](../automation/automation-first-runbook-graphical.md)
* [<span data-ttu-id="e5b66-126">Azure Otomasyonu öğrenme Haritası</span><span class="sxs-lookup"><span data-stu-id="e5b66-126">Azure Automation learning map</span></span>](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [<span data-ttu-id="e5b66-127">Azure Otomasyonu: SQL aracınızı bulutta</span><span class="sxs-lookup"><span data-stu-id="e5b66-127">Azure Automation: Your SQL Agent in the Cloud</span></span>](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

