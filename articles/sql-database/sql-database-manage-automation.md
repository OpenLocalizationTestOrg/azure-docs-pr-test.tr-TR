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
# <a name="managing-azure-sql-databases-using-azure-automation"></a>Azure otomasyonu kullanarak Azure SQL veritabanlarını yönetme
Bu kılavuz toohello Azure Otomasyon hizmetine ve Azure SQL veritabanlarınızın kullanılan toosimplify yönetim nasıl çalıştırılabilir tanıtılacaktır.

## <a name="what-is-azure-automation"></a>Azure Otomasyonu Nedir?
[Azure Otomasyonu](https://azure.microsoft.com/services/automation/) işlem Otomasyonu aracılığıyla bulut yönetimi basitleştirmek için bir Azure hizmetidir. Azure otomasyonu kullanarak, uzun süre çalışan, el ile hatasız ve sık tekrarlanan görevleri otomatik tooincrease güvenilirlik, verimliliği ve kuruluşunuz için zaman toovalue olabilir.

Azure Otomasyonu, kuruluşunuz büyüdükçe gereksinimlerinizi toomeet ölçeklendirilebilen bir yüksek oranda güvenilir ve yüksek oranda kullanılabilir iş akışı yürütme altyapısı sağlar. Tam olarak gerekli görevleri ortaya böylece Azure Otomasyonu'nda işlemleri el ile 3. taraf sistemleri tarafından veya zamanlanan aralıklarla artırılabilir devre dışı.

İşletimsel ek yükü azaltmak ve boşaltmak BT / DevOps personel toofocus iş değeri, bulut yönetim görevleri toobe taşıyarak ekler iş Azure Automation'ın otomatik olarak çalıştırın.

## <a name="how-can-azure-automation-help-manage-azure-sql-databases"></a>Azure Otomasyonu Azure SQL veritabanlarını yönetme nasıl yardımcı olabilir?
Azure SQL veritabanı yönetilebilir Azure Otomasyonu'nda hello kullanarak [Azure SQL Database PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/servicemanagement/azure.sqldatabase/v1.6.1/azure.sqldatabase/) hello kullanılabilir [Azure PowerShell Araçları](/powershell/azure/overview). Tüm SQL DB yönetim görevlerinizi hello hizmet içinde gerçekleştirebilmeniz azure Otomasyonu hello kutudan çıktığında, bu Azure SQL Database PowerShell cmdlet'leri vardır. Azure Automation bu cmdlet'leri diğer Azure Hizmetleri, tooautomate karmaşık görevleri için hello cmdlet'leri ile Azure hizmeti ve 3. taraf sistemi arasında eşleştirin.

Azure Otomasyonu da hello özelliği toocommunicate SQL sunucuları ile doğrudan PowerShell kullanarak SQL komutları vererek sahiptir.

Merhaba [Azure Otomasyonu runbook Galerisi](https://azure.microsoft.com/blog/2014/10/07/introducing-the-azure-automation-runbook-gallery/) Azure SQL veritabanları, diğer Azure Hizmetleri ve 3. taraf sistemi yönetimi otomatikleştirme başlatılan ürün ekibi ve topluluk runbook'lar tooget çeşitli içerir. Galeri runbook'ları şunları içerir:

* [Bir SQL Server veritabanında SQL sorguları çalıştırma](https://gallery.technet.microsoft.com/scriptcenter/How-to-use-a-SQL-Command-be77f9d2)
* [(Yukarı veya aşağı) dikey olarak ölçeklendirmek bir zamanlamaya göre bir Azure SQL veritabanı](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-Database-e957354f)
* [Veritabanı boyut üst sınırına yaklaşıyor varsa bir SQL tablosunu kesme](https://gallery.technet.microsoft.com/scriptcenter/Azure-Automation-Your-SQL-30f8736b)
* [Yüksek oranda parçalanmış varsa bir Azure SQL veritabanı tablolarında dizin](https://gallery.technet.microsoft.com/scriptcenter/Indexes-tables-in-an-Azure-73a2a8ea)

## <a name="next-steps"></a>Sonraki adımlar
Azure Otomasyonu ve kullanılan toomanage Azure SQL veritabanı nasıl olabilir hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn Azure Otomasyonu hakkında daha fazla izleyin.

* [Azure Otomasyonu genel bakış](../automation/automation-intro.md)
* [İlk runbook’um](../automation/automation-first-runbook-graphical.md)
* [Azure Otomasyonu öğrenme Haritası](https://azure.microsoft.com/documentation/learning-paths/automation/)
* [Azure Otomasyonu: Hello bulut içinde SQL Agent](https://azure.microsoft.com/blog/2014/06/26/azure-automation-your-sql-agent-in-the-cloud/) 

