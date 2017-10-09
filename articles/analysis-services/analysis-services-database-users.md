---
title: "aaaManage veritabanı rolleri ve kullanıcıların Azure Analysis Services | Microsoft Docs"
description: "Toomanage nasıl veritabanı rolleri ve kullanıcıların Azure Analysis Services sunucusunda öğrenin."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="5b570-103">Veritabanı rolleri ve kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="5b570-103">Manage database roles and users</span></span>

<span data-ttu-id="5b570-104">Merhaba model veritabanı düzeyinde tüm kullanıcılar tooa rolüne ait olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b570-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="5b570-105">Rolleri hello model veritabanı için belirli izinlerine sahip olan kullanıcıların tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5b570-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="5b570-106">Herhangi bir kullanıcı veya güvenlik grubu tooa rol hello Azure AD kiracısında içinde bir hesap olmalıdır eklenen hello sunucusu olarak aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="5b570-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="5b570-107">Rolleri tanımlama nasıl kullandığınız hello aracını kullanarak farklı bağlı olarak olmakla birlikte, hello etkisi aynı hello olduğu.</span><span class="sxs-lookup"><span data-stu-id="5b570-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="5b570-108">Rol izinleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5b570-108">Role permissions include:</span></span>
*  <span data-ttu-id="5b570-109">**Yönetici** -kullanıcınız hello veritabanı için tam izinleri.</span><span class="sxs-lookup"><span data-stu-id="5b570-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="5b570-110">Yönetici izinlerine sahip veritabanı rolleri, sunucu yöneticisinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5b570-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="5b570-111">**İşlem** -kullanıcıların tooand bağlanabilir hello veritabanında işlem işlemleri gerçekleştirmek ve model veritabanı verileri analiz etmek.</span><span class="sxs-lookup"><span data-stu-id="5b570-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="5b570-112">**Okuma** -kullanıcılar, bir istemci kullanabilir uygulama tooconnect tooand model veritabanı verileri analiz edin.</span><span class="sxs-lookup"><span data-stu-id="5b570-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="5b570-113">Tablo modeli projesi oluştururken, rolleri oluşturun ve SSDT içinde rol Yöneticisi'ni kullanarak kullanıcıları veya grupları toothose roller ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b570-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="5b570-114">Dağıtılan tooa server kullandığınızda SSMS, [Analiz Hizmetleri PowerShell cmdlet'leri](https://msdn.microsoft.com/library/hh758425.aspx), veya [tablolu modeli komut dosyası dili](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd veya rollerini ve kullanıcı üyeleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5b570-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="5b570-115">tooadd veya roller ve SSDT kullanıcıları yönetin</span><span class="sxs-lookup"><span data-stu-id="5b570-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="5b570-116">Ssdt'de > **tablolu Model Gezgini**, sağ **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="5b570-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="5b570-117">**Rol Yöneticisi**'nde **Yeni**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5b570-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="5b570-118">Merhaba rol için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="5b570-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="5b570-119">Varsayılan olarak, hello hello varsayılan rol adını artımlı olarak her yeni rol için numaralandırılır.</span><span class="sxs-lookup"><span data-stu-id="5b570-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="5b570-120">Merhaba üye türü, örneğin, finans yöneticileri veya İnsan Kaynakları uzmanlarıyla açıkça tanımlayan bir ad yazın önerilir.</span><span class="sxs-lookup"><span data-stu-id="5b570-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="5b570-121">Aşağıdaki izinleri hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="5b570-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="5b570-122">İzin</span><span class="sxs-lookup"><span data-stu-id="5b570-122">Permission</span></span>|<span data-ttu-id="5b570-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5b570-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="5b570-124">**Yok**</span><span class="sxs-lookup"><span data-stu-id="5b570-124">**None**</span></span>|<span data-ttu-id="5b570-125">Üyeleri hello model şeması değişiklik yapılamaz ve veri sorgulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="5b570-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="5b570-126">**Okuma**</span><span class="sxs-lookup"><span data-stu-id="5b570-126">**Read**</span></span>|<span data-ttu-id="5b570-127">Üyeler (satır filtreleri bağlı olarak) verileri sorgulayabilir ancak hello model şeması değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="5b570-128">**Okuma ve işlem**</span><span class="sxs-lookup"><span data-stu-id="5b570-128">**Read and Process**</span></span>|<span data-ttu-id="5b570-129">Üye verileri (temel alınarak satır düzeyi filtreleri) ve çalıştırma işlemi ve işlem tüm işlemleri sorgulama yapabilirsiniz ancak hello model şeması değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="5b570-130">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="5b570-130">**Process**</span></span>|<span data-ttu-id="5b570-131">Üye işlemi ve işlem tüm işlemleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="5b570-132">Merhaba model şeması değişiklik yapılamaz ve veri sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="5b570-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="5b570-133">**Yönetici**</span><span class="sxs-lookup"><span data-stu-id="5b570-133">**Administrator**</span></span>|<span data-ttu-id="5b570-134">Üyeleri hello model şeması değiştirmek ve tüm verileri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="5b570-135">Merhaba rol kullanıyorsanız oluşturma okuma veya okuma ve işlem izni bir DAX formülü kullanarak satır filtrelerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="5b570-136">Merhaba tıklatın **satır filtrelerini** sekmesinde, bir tablo seçin, sonra hello tıklatın **DAX filtre** alan ve bir DAX formülü girin.</span><span class="sxs-lookup"><span data-stu-id="5b570-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="5b570-137">Tıklatın **üyeleri** > **dış eklemek**.</span><span class="sxs-lookup"><span data-stu-id="5b570-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="5b570-138">İçinde **dış Üye Ekle**, kullanıcıları veya grupları, Azure AD kiracınızda tarafından e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="5b570-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="5b570-139">Tamam'ı tıklatın ve Rol Yöneticisi'ni kapatın rolleri ve Rol üyeleri tablolu Model Gezgini'nde görünür.</span><span class="sxs-lookup"><span data-stu-id="5b570-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Rol ve kullanıcı tablolu Model Gezgini](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="5b570-141">Tooyour Azure Analysis Services sunucusuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5b570-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="5b570-142">tooadd veya roller ve SSMS kullanıcıları yönetin</span><span class="sxs-lookup"><span data-stu-id="5b570-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="5b570-143">tooadd rol ve kullanıcı tooa model veritabanı dağıtıldı, bağlı toohello server sunucu yöneticisi olarak veya zaten bir veritabanı rolü yönetici izinlerine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5b570-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="5b570-144">Nesne Exporer içinde sağ **rolleri** > **yeni rol**.</span><span class="sxs-lookup"><span data-stu-id="5b570-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="5b570-145">İçinde **Rol Oluştur**, bir rol adı ve açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="5b570-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="5b570-146">Bir izin seçin.</span><span class="sxs-lookup"><span data-stu-id="5b570-146">Select a permission.</span></span>
   |<span data-ttu-id="5b570-147">İzin</span><span class="sxs-lookup"><span data-stu-id="5b570-147">Permission</span></span>|<span data-ttu-id="5b570-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5b570-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="5b570-149">**Tam Denetim (Yönetici)**</span><span class="sxs-lookup"><span data-stu-id="5b570-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="5b570-150">Üyeleri hello model şeması değiştirebilirsiniz işlemek ve tüm verileri sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="5b570-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="5b570-151">**İşlem veritabanı**</span><span class="sxs-lookup"><span data-stu-id="5b570-151">**Process database**</span></span>|<span data-ttu-id="5b570-152">Üye işlemi ve işlem tüm işlemleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="5b570-153">Merhaba model şeması değişiklik yapılamaz ve veri sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="5b570-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="5b570-154">**Okuma**</span><span class="sxs-lookup"><span data-stu-id="5b570-154">**Read**</span></span>|<span data-ttu-id="5b570-155">Üyeler (satır filtreleri bağlı olarak) verileri sorgulayabilir ancak hello model şeması değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="5b570-156">Tıklatın **üyelik**, sonra bir kullanıcı veya grubu girin kiracınızda Azure AD tarafından e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="5b570-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Kullanıcı ekle](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="5b570-158">Oluşturmakta olduğunuz hello rol okuma iznine sahipse, bir DAX formülü kullanarak satır filtrelerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="5b570-159">Tıklatın **satır filtrelerini**, bir tablo seçin ve ardından bir DAX formülü hello yazın **DAX filtre** alan.</span><span class="sxs-lookup"><span data-stu-id="5b570-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="5b570-160">tooadd roller ve TMSL komut dosyası kullanarak kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="5b570-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="5b570-161">Bir TMSL komut penceresinde hello XMLA SSMS veya PowerShell kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="5b570-162">Kullanım hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) komut ve hello [rolleri](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5b570-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="5b570-163">**Örnek TMSL komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="5b570-163">**Sample TMSL script**</span></span>

<span data-ttu-id="5b570-164">Bu örnekte, B2B dış kullanıcı ve Grup hello SalesBI veritabanı için Okuma izinlerine sahip toohello analist rol eklenir.</span><span class="sxs-lookup"><span data-stu-id="5b570-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="5b570-165">Hem de dış kullanıcı hello ve Grup aynı Kiracı Azure AD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5b570-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="5b570-166">tooadd roller ve PowerShell kullanarak kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="5b570-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="5b570-167">Merhaba [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) modül tablolu modeli komut dosyası dili (TMSL) sorgu veya betik kabul görev özgü veritabanı yönetimi cmdlet'leri ve hello genel amaçlı Invoke-ASCmd cmdlet'i sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b570-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="5b570-168">cmdlet aşağıdaki hello veritabanı rolleri ve kullanıcıları yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5b570-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="5b570-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="5b570-169">Cmdlet</span></span>|<span data-ttu-id="5b570-170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5b570-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="5b570-171">Ekleme RoleMember</span><span class="sxs-lookup"><span data-stu-id="5b570-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="5b570-172">Üye tooa veritabanı rolü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5b570-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="5b570-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="5b570-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="5b570-174">Üye veritabanı rolden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5b570-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="5b570-175">Çağırma ASCmd</span><span class="sxs-lookup"><span data-stu-id="5b570-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="5b570-176">TMSL betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="5b570-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="5b570-177">Satır filtreleri</span><span class="sxs-lookup"><span data-stu-id="5b570-177">Row filters</span></span>  
<span data-ttu-id="5b570-178">Hangi satır bir tablodaki belirli bir rol üyeleri tarafından sorgulanabilir satır filtrelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="5b570-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="5b570-179">Satır filtrelerini DAX formülleri kullanarak modeldeki her tablo için tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="5b570-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="5b570-180">Satır filtreleri, yalnızca rollerini okuma ve okuma için tanımlanabilir ve işlem izinleri.</span><span class="sxs-lookup"><span data-stu-id="5b570-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="5b570-181">Belirli bir tablo için bir satır filtresi tanımlı değilse, varsayılan olarak, başka bir tablodan çapraz filtreleme uygulanır sürece hello tablodaki tüm satırları üyeleri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b570-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="5b570-182">Satır filtrelerini tooa TRUE/FALSE değeri, bu özel rolü üyeleri tarafından sorgulanan toodefine hello satırları değerlendirilmelidir bir DAX formülü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="5b570-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="5b570-183">Merhaba DAX formülü dahil edilmeyen satırları sorgulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="5b570-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="5b570-184">Örneğin, Müşteriler tablosu satır filtre ifadesi, aşağıdaki hello ile Merhaba *müşteriler [Country] = "ABD" =*, hello satış rolünün üyeleri yalnızca hello ABD müşteriler bakın.</span><span class="sxs-lookup"><span data-stu-id="5b570-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="5b570-185">Satır Filtreleri Uygula belirtilen toohello satırları ve ilişkili satırları.</span><span class="sxs-lookup"><span data-stu-id="5b570-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="5b570-186">Bir tabloda birden çok ilişki olduğunda, güvenlik etkin hello ilişki için filtre uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5b570-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="5b570-187">Satır filtrelerini diğer satır filtreleri ilişkili tablolar için örneğin tanımlanmış kesiştiğinden:</span><span class="sxs-lookup"><span data-stu-id="5b570-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="5b570-188">Tablo</span><span class="sxs-lookup"><span data-stu-id="5b570-188">Table</span></span>|<span data-ttu-id="5b570-189">DAX ifadesi</span><span class="sxs-lookup"><span data-stu-id="5b570-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="5b570-190">Bölge</span><span class="sxs-lookup"><span data-stu-id="5b570-190">Region</span></span>|<span data-ttu-id="5b570-191">= Bölge [Country] = "Tr"</span><span class="sxs-lookup"><span data-stu-id="5b570-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="5b570-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="5b570-192">ProductCategory</span></span>|<span data-ttu-id="5b570-193">= ProductCategory [Name] "Bisiklet" =</span><span class="sxs-lookup"><span data-stu-id="5b570-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="5b570-194">İşlemler</span><span class="sxs-lookup"><span data-stu-id="5b570-194">Transactions</span></span>|<span data-ttu-id="5b570-195">= İşlemleri [yıl] 2016 =</span><span class="sxs-lookup"><span data-stu-id="5b570-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="5b570-196">Merhaba net üyeleri burada hello müşteri hello ABD'de, bisiklet hello ürün kategorisi olan ve hello yıl 2016 veri satırı sorgulayabilirsiniz etkisidir.</span><span class="sxs-lookup"><span data-stu-id="5b570-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="5b570-197">Kullanıcılar, bu izinler veren başka bir rolün üyesi olmadığı sürece olmayan bisiklet ya da işlemleri 2016'da değil işlemleri işlemleri hello ABD dışında sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="5b570-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="5b570-198">Merhaba filtre kullanabilirsiniz *=FALSE()*, tüm bir tabloyu için toodeny erişim tooall sıralar.</span><span class="sxs-lookup"><span data-stu-id="5b570-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b570-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5b570-199">Next steps</span></span>
  <span data-ttu-id="5b570-200">[Sunucu yöneticileri yönetin](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="5b570-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="5b570-201">Azure Analysis Services PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="5b570-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="5b570-202">Tablo modeli komut dosyası dili (TMSL) başvurusu</span><span class="sxs-lookup"><span data-stu-id="5b570-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

