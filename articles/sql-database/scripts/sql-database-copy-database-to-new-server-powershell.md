---
title: "PowerShell örnek kopyası Azure SQL veritabanı yeni sunucu | Microsoft Docs"
description: "Yeni bir sunucuya SQL veritabanına kopyalamak için azure PowerShell örnek betiği"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a>Yeni bir sunucuya SQL veritabanına kopyalamak için PowerShell kullanın

Bu PowerShell komut dosyası örnek yeni bir sunucu varolan bir veritabanının bir kopyasını oluşturur. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a>Bir veritabanını yeni bir sunucuya kopyalayın

[!code-powershell[Ana](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "kopyalama veritabanını yeni sunucuya")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Komut dosyası örneği çalıştırdıktan sonra kaynak grubu ve onunla ilişkili tüm kaynakları kaldırmak için aşağıdaki komutu kullanılabilir.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmSqlServer yeni](/powershell/module/azurerm.sql/new-azurermsqlserver) | Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur. |
| [AzureRmSqlDatabaseCopy yeni](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | Anlık görüntü şu anda kullandığı bir veritabanının bir kopyasını oluşturur. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |
|||

## <a name="next-steps"></a>Sonraki adımlar

Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek SQL veritabanı PowerShell Betiği örnekleri bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).
