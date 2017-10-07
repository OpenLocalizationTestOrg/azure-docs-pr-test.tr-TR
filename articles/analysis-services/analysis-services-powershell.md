---
title: aaaManage PowerShell ile Azure Analysis Services | Microsoft Docs
description: "PowerShell ile Azure Analysis Services yönetimi."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Azure Analysis Services PowerShell ile yönetme

Bu makalede PowerShell cmdlet'lerini kullanılan tooperform Azure Analysis Services sunucusu ve veritabanı yönetim görevleri açıklar. 

Sunucu yönetimi görevlerini oluşturma veya bir sunucu silme, askıya almak veya sunucu işlemlerini sürdürme veya hello hizmet düzeyi (katman) değiştirme gibi Azure Resource Manager (AzureRM) cmdlet'lerini kullanın. SQL Server Analysis Services olarak aynı SqlServer modülü gibi ekleme veya Rol üyeleri kaldırma, işleme veya kullanım cmdlet'leri bölümleme dahil veritabanlarını yönetmeyle ilgili diğer görevler hello.

## <a name="permissions"></a>İzinler
Çoğu PowerShell görevleri yönettiğiniz hello Analysis Services sunucusunda yönetici ayrıcalıkları gerektirir. Zamanlanmış PowerShell görevleri katılımsız işlemleridir. Merhaba Zamanlayıcısı'nı çalıştıran hello hesabının hello Çözümleme Hizmetleri sunucusunda yönetici ayrıcalıkları olmalıdır. 

AzureRm cmdlet'lerini kullanarak sunucu işlemleri için hesabınızı ya da Zamanlayıcı çalıştıran hello hesabının da hello kaynak için toohello sahip rolünü ait olmalıdır [Azure rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Sunucu işlemleri 
Azure Analysis Services cmdlet'lerini hello dahil [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) Bileşen Modülü. tooinstall AzureRM cmdlet modülleri bkz [Azure Resource Manager cmdlet'lerini](/powershell/azure/overview) hello PowerShell Galerisi içinde.

|Cmdlet|Açıklama| 
|------------|-----------------| 
|[Dışarı aktarma AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Dışarı aktarma toofile oturum açın.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Bir sunucu örneği ayrıntılarını alır.|  
|[AzureRmAnalysisServicesServer yeni](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Bir sunucu örneği oluşturur.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Bir sunucu örneğini kaldırır.|  
|[Askıya alma AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Bir sunucu örneği askıya alır.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Bir sunucuyu sürdürür.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Bir sunucu örneği değiştirir.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Bir sunucu örneğinin testleri hello varlığı.| 

## <a name="database-operations"></a>Veritabanı işlemleri

Azure Analysis Services veritabanı işlemlerini kullanmak hello aynı [SqlServer](https://www.powershellgallery.com/packages/SqlServer) modülü SQL Server Analysis Services olarak. Ancak, tüm cmdlet'leri Azure Analysis Services için desteklenir. 

Merhaba SqlServer modülü iyi bir tablolu Model komut dosyası dili (TMSL) kabul hello genel amaçlı Invoke-ASCmd cmdlet'ini olarak sorgu veya komut dosyası gibi görev özgü veritabanı yönetimi cmdlet'leri sağlar. Merhaba hello SqlServer modülünde aşağıdaki cmdlet'leri Azure Analysis Services için desteklenir.

  
|Cmdlet|Açıklama|
|------------|-----------------| 
|[Ekleme RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Üye tooa veritabanı rolü ekleyin.| 
|[Yedekleme ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Bir Analysis Services veritabanını yedekleyin.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Üye veritabanı rolden kaldırır.|   
|[Çağırma ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|TMSL betiğini yürütün.|
|[Çağırma ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Bir veritabanı işlemi.|  
|[Çağırma ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Bir bölüm işleme.| 
|[Çağırma ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Tablo işlem.|  
|[Bölüm birleştirme](https://msdn.microsoft.com/library/hh479576.aspx)|Bir bölümü birleştirin.|  
|[Geri yükleme ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Bir Analysis Services veritabanını geri yükleyin.| 
  

## <a name="related-information"></a>İlgili bilgiler

* [SQL Server PowerShell modülünü indirin](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [SSMS indirin](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [PowerShell galerisinde SqlServer Modülü](https://www.powershellgallery.com/packages/SqlServer)    
* [Tablo programlama modeli uyumluluk düzeyi 1200 ve daha yüksek](https://msdn.microsoft.com/library/mt712541.aspx)
