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
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="8ad08-103">Rol tabanlı erişim denetimi için bir access raporu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ad08-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="8ad08-104">Birisi erişim izni verilir veya erişim aboneliklerinizi içinde iptal eder dilediğiniz zaman hello değişiklikleri Azure olayları günlüğe.</span><span class="sxs-lookup"><span data-stu-id="8ad08-104">Any time someone grants or revokes access within your subscriptions, hello changes get logged in Azure events.</span></span> <span data-ttu-id="8ad08-105">Son 90 gün hello için tüm değişiklikleri erişim değişiklik geçmişi raporları toosee oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ad08-105">You can create access change history reports toosee all changes for hello past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="8ad08-106">Azure PowerShell ile bir rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="8ad08-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="8ad08-107">toocreate access değiştirmek PowerShell, kullanım hello geçmişi raporda [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) komutu.</span><span class="sxs-lookup"><span data-stu-id="8ad08-107">toocreate an access change history report in PowerShell, use hello [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="8ad08-108">Bu komut çağırdığınızda, hello aşağıdakileri de dahil olmak üzere listelenen istediğiniz hello atamaları hangi özelliğinin belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ad08-108">When you call this command, you can specify which property of hello assignments you want listed, including hello following:</span></span>

| <span data-ttu-id="8ad08-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="8ad08-109">Property</span></span> | <span data-ttu-id="8ad08-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8ad08-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8ad08-111">**Eylem**</span><span class="sxs-lookup"><span data-stu-id="8ad08-111">**Action**</span></span> |<span data-ttu-id="8ad08-112">Erişim izni veya iptal</span><span class="sxs-lookup"><span data-stu-id="8ad08-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="8ad08-113">**Arayan**</span><span class="sxs-lookup"><span data-stu-id="8ad08-113">**Caller**</span></span> |<span data-ttu-id="8ad08-114">Merhaba sahibi hello erişim için sorumlu değiştirme</span><span class="sxs-lookup"><span data-stu-id="8ad08-114">hello owner responsible for hello access change</span></span> |
| <span data-ttu-id="8ad08-115">**Principalıd**</span><span class="sxs-lookup"><span data-stu-id="8ad08-115">**PrincipalId**</span></span> | <span data-ttu-id="8ad08-116">Merhaba hello kullanıcı, Grup veya hello rolü atandı uygulamanın benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="8ad08-116">hello unique identifier of hello user, group, or application that was assigned hello role</span></span> |
| <span data-ttu-id="8ad08-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="8ad08-117">**PrincipalName**</span></span> |<span data-ttu-id="8ad08-118">Merhaba kullanıcı, Grup veya uygulama Hello adı</span><span class="sxs-lookup"><span data-stu-id="8ad08-118">hello name of hello user, group, or application</span></span> |
| <span data-ttu-id="8ad08-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="8ad08-119">**PrincipalType**</span></span> |<span data-ttu-id="8ad08-120">Merhaba atama bir kullanıcı, Grup veya uygulama için olup</span><span class="sxs-lookup"><span data-stu-id="8ad08-120">Whether hello assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="8ad08-121">**Roledefinitionıd**</span><span class="sxs-lookup"><span data-stu-id="8ad08-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="8ad08-122">Merhaba verilen veya iptal hello rolünün GUID</span><span class="sxs-lookup"><span data-stu-id="8ad08-122">hello GUID of hello role that was granted or revoked</span></span> |
| <span data-ttu-id="8ad08-123">**Rol adı**</span><span class="sxs-lookup"><span data-stu-id="8ad08-123">**RoleName**</span></span> |<span data-ttu-id="8ad08-124">verilen veya iptal hello rolü</span><span class="sxs-lookup"><span data-stu-id="8ad08-124">hello role that was granted or revoked</span></span> |
| <span data-ttu-id="8ad08-125">**Kapsam**</span><span class="sxs-lookup"><span data-stu-id="8ad08-125">**Scope**</span></span> | <span data-ttu-id="8ad08-126">Merhaba abonelik, kaynak grubu veya atama hello kaynak benzersiz tanıtıcısı Hello çok uygular</span><span class="sxs-lookup"><span data-stu-id="8ad08-126">hello unique identifier of hello subscription, resource group, or resource that hello assignment applies too</span></span>| 
| <span data-ttu-id="8ad08-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="8ad08-127">**ScopeName**</span></span> |<span data-ttu-id="8ad08-128">Merhaba abonelik, kaynak grubu veya kaynak Hello adı</span><span class="sxs-lookup"><span data-stu-id="8ad08-128">hello name of hello subscription, resource group, or resource</span></span> |
| <span data-ttu-id="8ad08-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="8ad08-129">**ScopeType**</span></span> |<span data-ttu-id="8ad08-130">Merhaba atama hello abonelik, kaynak grubu veya kaynak kapsamı olup</span><span class="sxs-lookup"><span data-stu-id="8ad08-130">Whether hello assignment was at hello subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="8ad08-131">**Zaman damgası**</span><span class="sxs-lookup"><span data-stu-id="8ad08-131">**Timestamp**</span></span> |<span data-ttu-id="8ad08-132">Başlangıç tarihi ve saati bu erişim değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="8ad08-132">hello date and time that access was changed</span></span> |

<span data-ttu-id="8ad08-133">Bu örnek komut, son yedi gün hello için hello Abonelikteki tüm erişim değişiklikleri listeler:</span><span class="sxs-lookup"><span data-stu-id="8ad08-133">This example command lists all access changes in hello subscription for hello past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - ekran görüntüsü](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="8ad08-135">Azure CLI ile bir rapor oluşturun</span><span class="sxs-lookup"><span data-stu-id="8ad08-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="8ad08-136">toocreate hello Azure komut satırı arabirimi (CLI), bir erişim değişiklik geçmişi raporda kullanmak hello `azure role assignment changelog list` komutu.</span><span class="sxs-lookup"><span data-stu-id="8ad08-136">toocreate an access change history report in hello Azure command-line interface (CLI), use hello `azure role assignment changelog list` command.</span></span>

## <a name="export-tooa-spreadsheet"></a><span data-ttu-id="8ad08-137">Tooa elektronik ver</span><span class="sxs-lookup"><span data-stu-id="8ad08-137">Export tooa spreadsheet</span></span>
<span data-ttu-id="8ad08-138">toosave rapor hello veya hello verileri işlemek, bir .csv dosyasına dışarı aktarma hello erişim değiştirir.</span><span class="sxs-lookup"><span data-stu-id="8ad08-138">toosave hello report, or manipulate hello data, export hello access changes into a .csv file.</span></span> <span data-ttu-id="8ad08-139">Ardından, gözden geçirme için elektronik tablodaki hello raporunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ad08-139">You can then view hello report in a spreadsheet for review.</span></span>

![Değişim günlüğü görüntülenebilir elektronik tablo olarak - ekran görüntüsü](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="8ad08-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ad08-141">Next steps</span></span>
* <span data-ttu-id="8ad08-142">Çalışmak [Azure rbac'de özel roller](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="8ad08-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="8ad08-143">Bilgi nasıl toomanage [powershell ile Azure RBAC](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8ad08-143">Learn how toomanage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

