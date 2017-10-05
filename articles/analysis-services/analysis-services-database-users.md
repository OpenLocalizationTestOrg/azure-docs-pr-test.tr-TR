---
title: "Veritabanı rolleri ve Azure Analysis Services kullanıcıları yönetme | Microsoft Docs"
description: "Veritabanı rolleri ve kullanıcıların Azure Analysis Services sunucusunda yönetmeyi öğrenin."
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
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="13651-103">Veritabanı rolleri ve kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="13651-103">Manage database roles and users</span></span>

<span data-ttu-id="13651-104">Model veritabanı düzeyinde tüm kullanıcıların bir role ait olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="13651-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="13651-105">Rolleri model veritabanı için belirli izinlerine sahip olan kullanıcıların tanımlar.</span><span class="sxs-lookup"><span data-stu-id="13651-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="13651-106">Herhangi bir kullanıcı veya güvenlik grubu role eklenen bir hesap Azure AD kiracısı sunucu ile aynı abonelikte olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="13651-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="13651-107">Rolleri tanımlama nasıl kullandığınız aracı bağlı olarak farklı olan, ancak etkisi aynıdır.</span><span class="sxs-lookup"><span data-stu-id="13651-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="13651-108">Rol izinleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="13651-108">Role permissions include:</span></span>
*  <span data-ttu-id="13651-109">**Yönetici** -kullanıcınız veritabanı için tam izinleri.</span><span class="sxs-lookup"><span data-stu-id="13651-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="13651-110">Yönetici izinlerine sahip veritabanı rolleri, sunucu yöneticisinden farklıdır.</span><span class="sxs-lookup"><span data-stu-id="13651-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="13651-111">**İşlem** -kullanıcılar bağlanmak ve veritabanı üzerinde işlem işlemleri ve model veritabanı verileri analiz edin.</span><span class="sxs-lookup"><span data-stu-id="13651-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="13651-112">**Okuma** -bağlanmak ve model veritabanı verileri çözümlemek için bir istemci uygulaması kullanıcılar kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="13651-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="13651-113">Tablo modeli projesi oluştururken, roller oluşturabilir ve SSDT içinde rol Yöneticisi'ni kullanarak bu rollere kullanıcıları veya grupları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="13651-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="13651-114">Bir sunucuya dağıtıldığında, SSMS, kullandığınız [Analiz Hizmetleri PowerShell cmdlet'leri](https://msdn.microsoft.com/library/hh758425.aspx), veya [tablolu modeli komut dosyası dili](https://msdn.microsoft.com/library/mt614797.aspx) rolleri ve kullanıcı üye eklemek veya kaldırmak için (TMSL).</span><span class="sxs-lookup"><span data-stu-id="13651-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="13651-115">Eklemek veya roller ve SSDT kullanıcıları yönetmek için</span><span class="sxs-lookup"><span data-stu-id="13651-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="13651-116">Ssdt'de > **tablolu Model Gezgini**, sağ **rolleri**.</span><span class="sxs-lookup"><span data-stu-id="13651-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="13651-117">**Rol Yöneticisi**'nde **Yeni**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="13651-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="13651-118">Rolü için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="13651-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="13651-119">Varsayılan olarak, varsayılan rol adını artımlı olarak her yeni rol için numaralandırılır.</span><span class="sxs-lookup"><span data-stu-id="13651-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="13651-120">Üye türü, örneğin, finans yöneticileri veya İnsan Kaynakları uzmanlarıyla açıkça tanımlayan bir ad yazın önerilir.</span><span class="sxs-lookup"><span data-stu-id="13651-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="13651-121">Aşağıdaki izinlerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="13651-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="13651-122">İzin</span><span class="sxs-lookup"><span data-stu-id="13651-122">Permission</span></span>|<span data-ttu-id="13651-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="13651-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="13651-124">**Yok**</span><span class="sxs-lookup"><span data-stu-id="13651-124">**None**</span></span>|<span data-ttu-id="13651-125">Üyeleri olan model şeması değiştirilemez ve verileri sorgulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="13651-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="13651-126">**Okuma**</span><span class="sxs-lookup"><span data-stu-id="13651-126">**Read**</span></span>|<span data-ttu-id="13651-127">Üyeler (satır filtreleri bağlı olarak) verileri sorgulayabilir ancak model şeması değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="13651-128">**Okuma ve işlem**</span><span class="sxs-lookup"><span data-stu-id="13651-128">**Read and Process**</span></span>|<span data-ttu-id="13651-129">Üye verileri (temel alınarak satır düzeyi filtreleri) ve çalıştırma işlemi ve işlem tüm işlemleri sorgulama yapabilirsiniz ancak model şeması değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="13651-130">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="13651-130">**Process**</span></span>|<span data-ttu-id="13651-131">Üye işlemi ve işlem tüm işlemleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="13651-132">Model şeması değişiklik yapılamaz ve veri sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="13651-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="13651-133">**Yönetici**</span><span class="sxs-lookup"><span data-stu-id="13651-133">**Administrator**</span></span>|<span data-ttu-id="13651-134">Üyeleri olan model şeması değiştirmek ve tüm verileri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="13651-135">Rol kullanıyorsanız oluşturma okuma veya okuma ve işlem izni bir DAX formülü kullanarak satır filtrelerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="13651-136">Tıklatın **satır filtrelerini** sekmesinde, bir tablo seçin, sonra tıklatın **DAX filtre** alan ve bir DAX formülü girin.</span><span class="sxs-lookup"><span data-stu-id="13651-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="13651-137">Tıklatın **üyeleri** > **dış eklemek**.</span><span class="sxs-lookup"><span data-stu-id="13651-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="13651-138">İçinde **dış Üye Ekle**, kullanıcıları veya grupları, Azure AD kiracınızda tarafından e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="13651-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="13651-139">Tamam'ı tıklatın ve Rol Yöneticisi'ni kapatın rolleri ve Rol üyeleri tablolu Model Gezgini'nde görünür.</span><span class="sxs-lookup"><span data-stu-id="13651-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Rol ve kullanıcı tablolu Model Gezgini](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="13651-141">Azure Analysis Services sunucusuna dağıtır.</span><span class="sxs-lookup"><span data-stu-id="13651-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="13651-142">Eklemek veya roller ve SSMS kullanıcıları yönetmek için</span><span class="sxs-lookup"><span data-stu-id="13651-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="13651-143">Rol ve kullanıcı bir dağıtılan modeli veritabanına eklemek için Sunucu Yöneticisi veya yönetici izinlerine sahip bir veritabanı rolü zaten sunucusuna bağlı olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="13651-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="13651-144">Nesne Exporer içinde sağ **rolleri** > **yeni rol**.</span><span class="sxs-lookup"><span data-stu-id="13651-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="13651-145">İçinde **Rol Oluştur**, bir rol adı ve açıklama girin.</span><span class="sxs-lookup"><span data-stu-id="13651-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="13651-146">Bir izin seçin.</span><span class="sxs-lookup"><span data-stu-id="13651-146">Select a permission.</span></span>
   |<span data-ttu-id="13651-147">İzin</span><span class="sxs-lookup"><span data-stu-id="13651-147">Permission</span></span>|<span data-ttu-id="13651-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="13651-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="13651-149">**Tam Denetim (Yönetici)**</span><span class="sxs-lookup"><span data-stu-id="13651-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="13651-150">Üyeleri olan model şeması değiştirebilirsiniz işlemek ve tüm verileri sorgulayabilir.</span><span class="sxs-lookup"><span data-stu-id="13651-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="13651-151">**İşlem veritabanı**</span><span class="sxs-lookup"><span data-stu-id="13651-151">**Process database**</span></span>|<span data-ttu-id="13651-152">Üye işlemi ve işlem tüm işlemleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="13651-153">Model şeması değişiklik yapılamaz ve veri sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="13651-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="13651-154">**Okuma**</span><span class="sxs-lookup"><span data-stu-id="13651-154">**Read**</span></span>|<span data-ttu-id="13651-155">Üyeler (satır filtreleri bağlı olarak) verileri sorgulayabilir ancak model şeması değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="13651-156">Tıklatın **üyelik**, sonra bir kullanıcı veya grubu girin kiracınızda Azure AD tarafından e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="13651-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Kullanıcı ekle](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="13651-158">Oluşturmakta olduğunuz rol okuma iznine sahipse, bir DAX formülü kullanarak satır filtrelerini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="13651-159">Tıklatın **satır filtrelerini**, bir tablo seçin ve ardından bir DAX formülü yazın **DAX filtre** alan.</span><span class="sxs-lookup"><span data-stu-id="13651-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="13651-160">TMSL komut dosyası kullanarak rolleri ve kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="13651-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="13651-161">SSMS veya PowerShell kullanarak XMLA penceresinde TMSL komut dosyası çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="13651-162">Kullanım [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) komut ve [rolleri](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) nesnesi.</span><span class="sxs-lookup"><span data-stu-id="13651-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="13651-163">**Örnek TMSL komut dosyası**</span><span class="sxs-lookup"><span data-stu-id="13651-163">**Sample TMSL script**</span></span>

<span data-ttu-id="13651-164">Bu örnekte, B2B dış kullanıcı ve Grup SalesBI veritabanı için Okuma izinlerine sahip analist rol eklenir.</span><span class="sxs-lookup"><span data-stu-id="13651-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="13651-165">Dış kullanıcı ve Grup aynı Kiracı Azure AD olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="13651-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
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

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="13651-166">PowerShell kullanarak rolleri ve kullanıcılar ekleme</span><span class="sxs-lookup"><span data-stu-id="13651-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="13651-167">[SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) görev özgü veritabanı yönetimi cmdlet'leri ve tablo modeli komut dosyası dili (TMSL) sorgu veya betik kabul genel amaçlı Invoke-ASCmd cmdlet modülü sağlar.</span><span class="sxs-lookup"><span data-stu-id="13651-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="13651-168">Aşağıdaki cmdlet, veritabanı rolleri ve kullanıcıları yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="13651-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="13651-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="13651-169">Cmdlet</span></span>|<span data-ttu-id="13651-170">Açıklama</span><span class="sxs-lookup"><span data-stu-id="13651-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="13651-171">Ekleme RoleMember</span><span class="sxs-lookup"><span data-stu-id="13651-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="13651-172">Bir veritabanı rolüne üye ekleme.</span><span class="sxs-lookup"><span data-stu-id="13651-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="13651-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="13651-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="13651-174">Üye veritabanı rolden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="13651-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="13651-175">Çağırma ASCmd</span><span class="sxs-lookup"><span data-stu-id="13651-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="13651-176">TMSL betiğini yürütün.</span><span class="sxs-lookup"><span data-stu-id="13651-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="13651-177">Satır filtreleri</span><span class="sxs-lookup"><span data-stu-id="13651-177">Row filters</span></span>  
<span data-ttu-id="13651-178">Hangi satır bir tablodaki belirli bir rol üyeleri tarafından sorgulanabilir satır filtrelerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="13651-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="13651-179">Satır filtrelerini DAX formülleri kullanarak modeldeki her tablo için tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="13651-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="13651-180">Satır filtreleri, yalnızca rollerini okuma ve okuma için tanımlanabilir ve işlem izinleri.</span><span class="sxs-lookup"><span data-stu-id="13651-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="13651-181">Belirli bir tablo için bir satır filtresi tanımlı değilse, varsayılan olarak, başka bir tablodan çapraz filtreleme uygulanır sürece tablodaki tüm satırları üyeleri sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13651-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="13651-182">Satır filtrelerini bu belirli rolünün üyeleri tarafından sorgulanabilir satırları tanımlamak için bir TRUE/FALSE değeri değerlendirilmelidir bir DAX formülü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="13651-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="13651-183">DAX formülü dahil edilmeyen satırları sorgulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="13651-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="13651-184">Örneğin, aşağıdaki satırı Müşteriler tablosuyla ifadeyi filtreler *müşteriler [Country] = "ABD" =*, satış rolünün üyeleri yalnızca ABD'deki müşteriler bakın.</span><span class="sxs-lookup"><span data-stu-id="13651-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="13651-185">Belirtilen satırları ve ilişkili satırları satır filtreleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="13651-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="13651-186">Bir tabloda birden çok ilişki olduğunda, güvenlik etkin ilişki için filtre uygulayın.</span><span class="sxs-lookup"><span data-stu-id="13651-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="13651-187">Satır filtrelerini diğer satır filtreleri ilişkili tablolar için örneğin tanımlanmış kesiştiğinden:</span><span class="sxs-lookup"><span data-stu-id="13651-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="13651-188">Tablo</span><span class="sxs-lookup"><span data-stu-id="13651-188">Table</span></span>|<span data-ttu-id="13651-189">DAX ifadesi</span><span class="sxs-lookup"><span data-stu-id="13651-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="13651-190">Bölge</span><span class="sxs-lookup"><span data-stu-id="13651-190">Region</span></span>|<span data-ttu-id="13651-191">= Bölge [Country] = "Tr"</span><span class="sxs-lookup"><span data-stu-id="13651-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="13651-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="13651-192">ProductCategory</span></span>|<span data-ttu-id="13651-193">= ProductCategory [Name] "Bisiklet" =</span><span class="sxs-lookup"><span data-stu-id="13651-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="13651-194">İşlemler</span><span class="sxs-lookup"><span data-stu-id="13651-194">Transactions</span></span>|<span data-ttu-id="13651-195">= İşlemleri [yıl] 2016 =</span><span class="sxs-lookup"><span data-stu-id="13651-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="13651-196">Üyeleri burada müşteri ABD'de, ürün kategorisi bisiklet olduğu ve yıl 2016 veri satırı sorgulayabilirsiniz net etkisidir.</span><span class="sxs-lookup"><span data-stu-id="13651-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="13651-197">Kullanıcılar, bu izinler veren başka bir rolün üyesi olmadığı sürece olmayan bisiklet ya da işlemleri 2016'da değil işlemleri işlemleri ABD dışında sorgulayamıyor.</span><span class="sxs-lookup"><span data-stu-id="13651-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="13651-198">Filtre kullanabilirsiniz *=FALSE()*, tüm bir tabloyu tüm satırları erişimini.</span><span class="sxs-lookup"><span data-stu-id="13651-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13651-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13651-199">Next steps</span></span>
  <span data-ttu-id="13651-200">[Sunucu yöneticileri yönetin](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="13651-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="13651-201">Azure Analysis Services PowerShell ile yönetme</span><span class="sxs-lookup"><span data-stu-id="13651-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="13651-202">Tablo modeli komut dosyası dili (TMSL) başvurusu</span><span class="sxs-lookup"><span data-stu-id="13651-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

