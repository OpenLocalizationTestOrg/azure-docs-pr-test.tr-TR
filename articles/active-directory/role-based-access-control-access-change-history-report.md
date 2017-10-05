---
title: "Erişim raporlama - Azure RBAC | Microsoft Docs"
description: "Tüm değişiklikleri, Azure aboneliklerinize Son 90 gün içinde rol tabanlı erişim denetimi ile erişimi listeleyen bir rapor oluşturur."
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
ms.openlocfilehash: 4e8028ab43ed02ef0c0a1374326b07f72f97d9d9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a><span data-ttu-id="8cc3e-103">Rol tabanlı erişim denetimi için bir access raporu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cc3e-103">Create an access report for Role-Based Access Control</span></span>
<span data-ttu-id="8cc3e-104">Birisi erişim izni verilir veya erişim aboneliklerinizi içinde iptal eder dilediğiniz zaman değişiklikleri Azure olayları günlüğe.</span><span class="sxs-lookup"><span data-stu-id="8cc3e-104">Any time someone grants or revokes access within your subscriptions, the changes get logged in Azure events.</span></span> <span data-ttu-id="8cc3e-105">Son 90 gün için tüm değişiklikleri görmek için erişim değişiklik geçmişi raporları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cc3e-105">You can create access change history reports to see all changes for the past 90 days.</span></span>

## <a name="create-a-report-with-azure-powershell"></a><span data-ttu-id="8cc3e-106">Azure PowerShell ile bir rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="8cc3e-106">Create a report with Azure PowerShell</span></span>
<span data-ttu-id="8cc3e-107">PowerShell'de erişim değişiklik geçmişi raporu oluşturmak için kullanın [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) komutu.</span><span class="sxs-lookup"><span data-stu-id="8cc3e-107">To create an access change history report in PowerShell, use the [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) command.</span></span>

<span data-ttu-id="8cc3e-108">Bu komut çağırdığınızda, aşağıdakiler de dahil olmak üzere listelenen istediğiniz atamaları hangi özelliğinin belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8cc3e-108">When you call this command, you can specify which property of the assignments you want listed, including the following:</span></span>

| <span data-ttu-id="8cc3e-109">Özellik</span><span class="sxs-lookup"><span data-stu-id="8cc3e-109">Property</span></span> | <span data-ttu-id="8cc3e-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cc3e-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8cc3e-111">**Eylem**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-111">**Action**</span></span> |<span data-ttu-id="8cc3e-112">Erişim izni veya iptal</span><span class="sxs-lookup"><span data-stu-id="8cc3e-112">Whether access was granted or revoked</span></span> |
| <span data-ttu-id="8cc3e-113">**Arayan**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-113">**Caller**</span></span> |<span data-ttu-id="8cc3e-114">Erişim değişiklik için sorumlu sahibi</span><span class="sxs-lookup"><span data-stu-id="8cc3e-114">The owner responsible for the access change</span></span> |
| <span data-ttu-id="8cc3e-115">**Principalıd**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-115">**PrincipalId**</span></span> | <span data-ttu-id="8cc3e-116">Kullanıcı, Grup veya rolü atandı uygulamanın benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="8cc3e-116">The unique identifier of the user, group, or application that was assigned the role</span></span> |
| <span data-ttu-id="8cc3e-117">**PrincipalName**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-117">**PrincipalName**</span></span> |<span data-ttu-id="8cc3e-118">Kullanıcı, Grup veya uygulama adı</span><span class="sxs-lookup"><span data-stu-id="8cc3e-118">The name of the user, group, or application</span></span> |
| <span data-ttu-id="8cc3e-119">**PrincipalType**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-119">**PrincipalType**</span></span> |<span data-ttu-id="8cc3e-120">Bir kullanıcı, Grup veya uygulama atama olup</span><span class="sxs-lookup"><span data-stu-id="8cc3e-120">Whether the assignment was for a user, group, or application</span></span> |
| <span data-ttu-id="8cc3e-121">**Roledefinitionıd**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-121">**RoleDefinitionId**</span></span> |<span data-ttu-id="8cc3e-122">Verilen veya iptal rolünün GUID</span><span class="sxs-lookup"><span data-stu-id="8cc3e-122">The GUID of the role that was granted or revoked</span></span> |
| <span data-ttu-id="8cc3e-123">**Rol adı**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-123">**RoleName**</span></span> |<span data-ttu-id="8cc3e-124">Verilen veya iptal rolü</span><span class="sxs-lookup"><span data-stu-id="8cc3e-124">The role that was granted or revoked</span></span> |
| <span data-ttu-id="8cc3e-125">**Kapsam**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-125">**Scope**</span></span> | <span data-ttu-id="8cc3e-126">Abonelik, kaynak grubu veya atama uygulandığı kaynak benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="8cc3e-126">The unique identifier of the subscription, resource group, or resource that the assignment applies to</span></span> | 
| <span data-ttu-id="8cc3e-127">**ScopeName**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-127">**ScopeName**</span></span> |<span data-ttu-id="8cc3e-128">Abonelik, kaynak grubu veya kaynak adı</span><span class="sxs-lookup"><span data-stu-id="8cc3e-128">The name of the subscription, resource group, or resource</span></span> |
| <span data-ttu-id="8cc3e-129">**ScopeType**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-129">**ScopeType**</span></span> |<span data-ttu-id="8cc3e-130">Atama abonelik, kaynak grubu veya kaynak kapsamı olmasına</span><span class="sxs-lookup"><span data-stu-id="8cc3e-130">Whether the assignment was at the subscription, resource group, or resource scope</span></span> |
| <span data-ttu-id="8cc3e-131">**Zaman damgası**</span><span class="sxs-lookup"><span data-stu-id="8cc3e-131">**Timestamp**</span></span> |<span data-ttu-id="8cc3e-132">Erişim değiştirildi saat ve tarihi</span><span class="sxs-lookup"><span data-stu-id="8cc3e-132">The date and time that access was changed</span></span> |

<span data-ttu-id="8cc3e-133">Bu örnek komut Abonelik son yedi gün için tüm erişim değişiklikleri listeler:</span><span class="sxs-lookup"><span data-stu-id="8cc3e-133">This example command lists all access changes in the subscription for the past seven days:</span></span>

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - ekran görüntüsü](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a><span data-ttu-id="8cc3e-135">Azure CLI ile bir rapor oluşturun</span><span class="sxs-lookup"><span data-stu-id="8cc3e-135">Create a report with Azure CLI</span></span>
<span data-ttu-id="8cc3e-136">Azure komut satırı arabirimi (CLI) içinde bir erişim değişiklik geçmişi raporu oluşturmak için kullanın `azure role assignment changelog list` komutu.</span><span class="sxs-lookup"><span data-stu-id="8cc3e-136">To create an access change history report in the Azure command-line interface (CLI), use the `azure role assignment changelog list` command.</span></span>

## <a name="export-to-a-spreadsheet"></a><span data-ttu-id="8cc3e-137">Bir elektronik tabloya dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="8cc3e-137">Export to a spreadsheet</span></span>
<span data-ttu-id="8cc3e-138">Raporu kaydedin veya verileri işlemek için erişim değişikliklerini bir .csv dosyasına dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="8cc3e-138">To save the report, or manipulate the data, export the access changes into a .csv file.</span></span> <span data-ttu-id="8cc3e-139">Ardından, gözden geçirme için elektronik tablodaki raporunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cc3e-139">You can then view the report in a spreadsheet for review.</span></span>

![Değişim günlüğü görüntülenebilir elektronik tablo olarak - ekran görüntüsü](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a><span data-ttu-id="8cc3e-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cc3e-141">Next steps</span></span>
* <span data-ttu-id="8cc3e-142">Çalışmak [Azure rbac'de özel roller](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="8cc3e-142">Work with [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>
* <span data-ttu-id="8cc3e-143">Nasıl yöneteceğinizi öğrenmek [powershell ile Azure RBAC](role-based-access-control-manage-access-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8cc3e-143">Learn how to manage [Azure RBAC with powershell](role-based-access-control-manage-access-powershell.md)</span></span>

