---
title: aaaAccess raporlama - Azure RBAC | Microsoft Docs
description: "Tüm listeleri değiştiğine erişim tooyour rol tabanlı erişim denetimi hello üzerinden Azure abonelikleriyle Son 90 gün içinde bir rapor oluşturun."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Rol tabanlı erişim denetimi için bir access raporu oluşturma
Birisi erişim izni verilir veya erişim aboneliklerinizi içinde iptal eder dilediğiniz zaman hello değişiklikleri Azure olayları günlüğe. Son 90 gün hello için tüm değişiklikleri erişim değişiklik geçmişi raporları toosee oluşturabilirsiniz.

## <a name="create-a-report-with-azure-powershell"></a>Azure PowerShell ile bir rapor oluşturma
toocreate access değiştirmek PowerShell, kullanım hello geçmişi raporda [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) komutu.

Bu komut çağırdığınızda, hello aşağıdakileri de dahil olmak üzere listelenen istediğiniz hello atamaları hangi özelliğinin belirtebilirsiniz:

| Özellik | Açıklama |
| --- | --- |
| **Eylem** |Erişim izni veya iptal |
| **Arayan** |Merhaba sahibi hello erişim için sorumlu değiştirme |
| **Principalıd** | Merhaba hello kullanıcı, Grup veya hello rolü atandı uygulamanın benzersiz tanıtıcısı |
| **PrincipalName** |Merhaba kullanıcı, Grup veya uygulama Hello adı |
| **PrincipalType** |Merhaba atama bir kullanıcı, Grup veya uygulama için olup |
| **Roledefinitionıd** |Merhaba verilen veya iptal hello rolünün GUID |
| **Rol adı** |verilen veya iptal hello rolü |
| **Kapsam** | Merhaba abonelik, kaynak grubu veya atama hello kaynak benzersiz tanıtıcısı Hello çok uygular| 
| **ScopeName** |Merhaba abonelik, kaynak grubu veya kaynak Hello adı |
| **ScopeType** |Merhaba atama hello abonelik, kaynak grubu veya kaynak kapsamı olup |
| **Zaman damgası** |Başlangıç tarihi ve saati bu erişim değiştirildi. |

Bu örnek komut, son yedi gün hello için hello Abonelikteki tüm erişim değişiklikleri listeler:

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - ekran görüntüsü](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Azure CLI ile bir rapor oluşturun
toocreate hello Azure komut satırı arabirimi (CLI), bir erişim değişiklik geçmişi raporda kullanmak hello `azure role assignment changelog list` komutu.

## <a name="export-tooa-spreadsheet"></a>Tooa elektronik ver
toosave rapor hello veya hello verileri işlemek, bir .csv dosyasına dışarı aktarma hello erişim değiştirir. Ardından, gözden geçirme için elektronik tablodaki hello raporunu görüntüleyebilirsiniz.

![Değişim günlüğü görüntülenebilir elektronik tablo olarak - ekran görüntüsü](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Sonraki adımlar
* Çalışmak [Azure rbac'de özel roller](role-based-access-control-custom-roles.md)
* Bilgi nasıl toomanage [powershell ile Azure RBAC](role-based-access-control-manage-access-powershell.md)

