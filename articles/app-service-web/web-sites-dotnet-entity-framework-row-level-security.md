---
title: "Öğreticisi: Entity Framework ve satır düzeyi güvenlik kullanarak çok Kiracı veritabanı Web uygulaması"
description: "Nasıl toodevelop bir ASP.NET MVC 5 web uygulaması çok kiracılı SQL Entity Framework ve satır düzeyi güvenlik kullanarak veritabanını backent, ile bilgi edinin."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="6d5dc-103">Öğreticisi: Entity Framework ve satır düzeyi güvenlik kullanarak çok Kiracı veritabanı Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="6d5dc-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="6d5dc-104">Bu öğretici nasıl toobuild çok kiracılı web uygulamasıyla gösterir bir "[paylaşılan veritabanı, paylaşılan şema](https://msdn.microsoft.com/library/aa479086.aspx)" Entity Framework kullanarak Kiracı modeli ve [satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d5dc-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="6d5dc-105">Bu modelde, tek bir veritabanı için çok sayıda Kiracı verileri içeren ve her tablodaki her satır bir "Kiracı kimliği ile" ilişkilendirilir</span><span class="sxs-lookup"><span data-stu-id="6d5dc-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="6d5dc-106">Satır düzeyi güvenlik (RLS), Azure SQL veritabanı için yeni bir özellik birbirinin verilerine erişmesini kullanılan tooprevent kiracılar ' dir.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="6d5dc-107">Bu, yalnızca tek bir, küçük değişiklikler toohello uygulama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="6d5dc-108">Merkezileştirerek hello Kiracı erişim mantığı veritabanındaki hello kendisi tarafından RLS hello uygulama kodu basitleştirir ve hello kiracılar arasında yanlışlıkla veri sızıntısı riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="6d5dc-109">Merhaba basit Contact Manager uygulamasından ile başlayalım [ASP.NET MVP uygulama kimlik doğrulama ve SQL DB ile oluşturup tooAzure uygulama hizmeti](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="6d5dc-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="6d5dc-110">Sağ tüm kişileri Merhaba uygulaması artık, tüm kullanıcıların (kiracılar) toosee sağlar:</span><span class="sxs-lookup"><span data-stu-id="6d5dc-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="6d5dc-112">Böylece kullanıcılar toothem ait mümkün toosee yalnızca hello kişiler yalnızca birkaç küçük değişikliklerle çoklu kiracı için destek ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="6d5dc-113">1. adım: hello uygulama tooset hello SESSION_CONTEXT dinleyiciyi sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="6d5dc-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="6d5dc-114">Bir uygulama değişikliği toomake ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-114">There is one application change we need toomake.</span></span> <span data-ttu-id="6d5dc-115">Tüm uygulama kullanıcılarının bağlandığından toohello veritabanı kullanarak, aynı bağlantı dizesini (yani aynı SQL oturum açma) Merhaba, şu anda hangi kullanıcı onu filtre bir RLS İlkesi tooknow bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="6d5dc-116">Bu yaklaşım verimli bağlantı havuzu sağlar, ancak başka bir şekilde tooidentify hello geçerli uygulama kullanıcısı hello veritabanı içinde ihtiyacımız anlamına gelir web uygulamalarında çok yaygındır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="6d5dc-117">Merhaba toohave hello uygulama kümesi için bir anahtar-değer çifti çözümdür hello içinde geçerli UserID hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) hemen bağlantı açıldıktan sonra önce yürütülmeden tüm sorgular.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="6d5dc-118">SESSION_CONTEXT olan bir oturum kapsamlı anahtar-değer deposu ve RLS ilkemizi UserID içinde depolanan hello kullanacağı tooidentify hello geçerli kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="6d5dc-119">Ekleyeceğiz bir [dinleyiciyi](https://msdn.microsoft.com/data/dn469464.aspx) (özellikle, bir [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), yeni bir özellik içinde Entity Framework (EF) 6, tooautomatically kümesi yürüterek hello SESSION_CONTEXT içinde geçerli UserID hello bir EF bağlantı açıldığında T-SQL ifadesi.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="6d5dc-120">Merhaba ContactManager projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="6d5dc-121">Hello Çözüm Gezgini hello modelleri klasörüne sağ tıklayın ve Ekle'yi seçin > sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="6d5dc-122">"SessionContextInterceptor.cs" Merhaba yeni sınıf adını ve Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="6d5dc-123">Merhaba içeriğine SessionContextInterceptor.cs koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

<span data-ttu-id="6d5dc-124">Merhaba yalnızca uygulama değişikliği gerekli olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-124">That's hello only application change required.</span></span> <span data-ttu-id="6d5dc-125">Devam edin ve yapı ve hello uygulamayı yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="6d5dc-126">2. adım: bir kullanıcı kimliği sütunu toohello veritabanı şeması ekleme</span><span class="sxs-lookup"><span data-stu-id="6d5dc-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="6d5dc-127">Ardından, bir kullanıcıyla (Kiracı) her satır bir kullanıcı kimliği sütunu toohello kişiler tablo tooassociate tooadd ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="6d5dc-128">Böylece biz tooinclude EF veri modelimizi Bu alan yoksa biz hello şemada doğrudan hello veritabanı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="6d5dc-129">SQL Server Management Studio veya Visual Studio kullanarak toohello veritabanına doğrudan bağlanın ve aşağıdaki T-SQL hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="6d5dc-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="6d5dc-130">Bu, bir kullanıcı kimliği sütunu toohello kişiler tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="6d5dc-131">Kullanıcı kimliklerini hello AspNetUsers tablosunda depolanan hello nvarchar(128) veri türü toomatch hello kullanırız ve hello UserID yeni eklenen satırlar toobe hello şu anda SESSION_CONTEXT içinde depolanan UserID için otomatik olarak ayarlayacak bir DEFAULT kısıtlaması oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="6d5dc-132">Şimdi hello tablo şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="6d5dc-132">Now hello table looks like this:</span></span>

![SSMS kişiler tablosu](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="6d5dc-134">Yeni kişiler oluşturduğunuzda, otomatik olarak hello atanmaları UserID düzeltin.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="6d5dc-135">Tanıtım amacıyla, ancak şimdi birkaç kullanıcı var olan bu kişiler tooan atayın.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="6d5dc-136">Zaten hello uygulamada oluşturduğunuz birkaç kullanıcı (örneğin, yerel kullanarak, Google veya Facebook hesapları), hello AspNetUsers tabloda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="6d5dc-137">Merhaba ekran görüntüsünde, yalnızca bir kullanıcı yok kadarki.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-137">In hello screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers tablo](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="6d5dc-139">Kopya hello kimliği için user1@contoso.com, INTO hello T-SQL deyimi aşağıdaki yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="6d5dc-140">Bu kullanıcı kimliği ile Merhaba kişilerin bu deyimi tooassociate üç yürütün.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="6d5dc-141">3. adım: hello veritabanında bir satır düzeyi güvenlik ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6d5dc-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="6d5dc-142">Merhaba son toocreate sorgular tarafından döndürülen SESSION_CONTEXT tooautomatically filtre hello sonuçları hello UserID kullanan bir güvenlik ilkesi adımdır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="6d5dc-143">Hala bağlı toohello veritabanı sırasında T-SQL aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="6d5dc-143">While still connected toohello database, execute hello following T-SQL:</span></span>

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

<span data-ttu-id="6d5dc-144">Bu kod üç şey yapar.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-144">This code does three things.</span></span> <span data-ttu-id="6d5dc-145">İlk olarak, merkezileştirme ve erişim toohello RLS nesneleri sınırlamak için en iyi uygulama olarak yeni bir şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="6d5dc-146">Ardından, hello satır UserID hello SESSION_CONTEXT UserID eşleştiğinde '1' döndürülecek koşul bir işlev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="6d5dc-147">Son olarak, bu işlev hello kişiler tablosunda bir filtre ve blok koşul olarak ekler bir güvenlik ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="6d5dc-148">Merhaba filtre koşulu toohello geçerli kullanıcıya ait yalnızca satır sorguları tooreturn neden olur ve hello engelleme koşulu her zamankinden yanlışlıkla hello yanlış kullanıcı için bir satır ekleme bir koruma tooprevent hello uygulamanın gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="6d5dc-149">Merhaba uygulamayı çalıştırın ve olarak oturum açın artık user1@contoso.com. Bu kullanıcı şimdi biz toothis UserID daha önce atanan hello kişiler görür:</span><span class="sxs-lookup"><span data-stu-id="6d5dc-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="6d5dc-151">toovalidate Bu ayrıca, deneyin yeni bir kullanıcı kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="6d5dc-152">Hiçbiri toothem atanmış olduğundan hiçbir kişiler görürler.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="6d5dc-153">Yeni bir kişi oluşturun, toothem atanacak ve yalnızca mümkün toosee olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d5dc-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d5dc-154">Next steps</span></span>
<span data-ttu-id="6d5dc-155">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="6d5dc-155">That's it!</span></span> <span data-ttu-id="6d5dc-156">Merhaba basit kişi yöneticisi web uygulaması bir çok kiracılı biri her bir kullanıcı kendi kişi listesi olduğu dönüştürüldü.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="6d5dc-157">Satır düzeyi güvenlik kullanarak, biz Kiracı erişim mantığı bizim uygulama kodundaki zorlamayı hello karmaşıklığını kaçınılması.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="6d5dc-158">Bu saydamlık hello uygulama toofocus elinizdeki hello gerçek iş sorunu sağlar ve ayrıca kullanıcının Merhaba uygulaması codebase gibi yanlışlıkla veri sızıntıları hello riskini azaltır büyür.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="6d5dc-159">Bu öğretici yalnızca RLS ile mümkündür, çizilmiş hello yüzeyi vardır.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="6d5dc-160">Örneğin, olası toohave daha karmaşık olan veya ayrıntılı erişim mantığı ve onun olası toostore hello SESSION_CONTEXT içinde geçerli UserID daha fazlasını hello.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="6d5dc-161">Ayrıca çok mümkündür[RLS hello esnek veritabanı araçlarını istemci kitaplıkları ile tümleştirmek](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) bir genişleme veri katmanına toosupport çok kiracılı parça.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="6d5dc-162">Bu olanakları de toomake RLS daha da iyi çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="6d5dc-163">Herhangi bir sorunuz, fikirleri veya toosee istediğiniz şey varsa, lütfen hello açıklamaları bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="6d5dc-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="6d5dc-164">Geri bildiriminiz için teşekkür ederiz!</span><span class="sxs-lookup"><span data-stu-id="6d5dc-164">We appreciate your feedback!</span></span>

