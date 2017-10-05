---
title: "Öğreticisi: Entity Framework ve satır düzeyi güvenlik kullanarak çok Kiracı veritabanı Web uygulaması"
description: "Çoklu kiracı SQL Entity Framework ve satır düzeyi güvenlik kullanarak veritabanını backent, bir ASP.NET MVC 5 web uygulaması geliştirmeyi öğrenin."
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="b2eaf-103">Öğreticisi: Entity Framework ve satır düzeyi güvenlik kullanarak çok Kiracı veritabanı Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="b2eaf-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="b2eaf-104">Bu öğretici ile çok kiracılı web uygulamasının nasıl oluşturulacağını gösterir bir "[paylaşılan veritabanı, paylaşılan şema](https://msdn.microsoft.com/library/aa479086.aspx)" Entity Framework kullanarak Kiracı modeli ve [satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2eaf-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="b2eaf-105">Bu modelde, tek bir veritabanı için çok sayıda Kiracı verileri içeren ve her tablodaki her satır bir "Kiracı kimliği ile" ilişkilendirilir</span><span class="sxs-lookup"><span data-stu-id="b2eaf-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="b2eaf-106">Satır düzeyi güvenlik (RLS), Azure SQL veritabanı için yeni bir özellik, kiracıların diğer kişilerin veri erişimini engellemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="b2eaf-107">Bu yalnızca bir tek, küçük bir değişiklik uygulama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="b2eaf-108">Veritabanının içindeki Kiracı erişim mantığı merkezileştirerek tarafından RLS uygulama kodu basitleştirir ve kiracılar arasında yanlışlıkla veri sızıntısı riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="b2eaf-109">Basit Contact Manager uygulamasından ile başlayalım [auth ve SQL DB ile bir ASP.NET MVP uygulama oluşturun ve Azure App Service'e dağıtma](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b2eaf-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="b2eaf-110">Sağ şimdi, tüm kullanıcıların tüm kişileri görmek için (kiracılar) uygulama verir:</span><span class="sxs-lookup"><span data-stu-id="b2eaf-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="b2eaf-112">Böylece kullanıcılar yalnızca kendilerine ait olan kişileri görebilmek için birkaç küçük değişikliklerle çoklu kiracı için destek ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="b2eaf-113">1. adım: SESSION_CONTEXT ayarlamak için uygulamada dinleyiciyi sınıfı ekleme</span><span class="sxs-lookup"><span data-stu-id="b2eaf-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="b2eaf-114">Bir uygulama değişikliği yapmak için ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-114">There is one application change we need to make.</span></span> <span data-ttu-id="b2eaf-115">Tüm uygulama kullanıcılarının aynı bağlantı dizesini (yani aynı SQL oturum açma) kullanarak veritabanına bağlanmak için da şu anda hangi kullanıcı için filtre öğrenmek bir RLS İlkesi yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="b2eaf-116">Bu yaklaşım verimli bağlantı havuzu sağlar, ancak veritabanı içinde geçerli uygulama kullanıcıyı tanımlamak için bir başka yolu ihtiyacımız anlamına gelir web uygulamalarında çok yaygındır.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="b2eaf-117">Çözüm geçerli UserID için bir anahtar-değer çifti kümesi uygulama yapmaktır [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) hemen bağlantı açıldıktan sonra önce yürütülmeden tüm sorgular.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="b2eaf-118">Bir oturum kapsamlı anahtar-değer deposu SESSION_CONTEXT olduğu ve RLS ilkemizi depolanan UserID geçerli kullanıcıyı tanımlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="b2eaf-119">Ekleyeceğiz bir [dinleyiciyi](https://msdn.microsoft.com/data/dn469464.aspx) (özellikle, bir [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), yeni bir özellik içinde Entity Framework (T-SQL yürüterek geçerli UserID SESSION_CONTEXT otomatik olarak ayarlamak için EF) 6, EF bağlantı açıldığında deyimi.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="b2eaf-120">ContactManager projesini Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="b2eaf-121">Çözüm Gezgini'nde modeller klasörü sağ tıklatın ve Ekle'yi seçin > sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="b2eaf-122">Yeni sınıf "SessionContextInterceptor.cs" ve Ekle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="b2eaf-123">SessionContextInterceptor.cs içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

<span data-ttu-id="b2eaf-124">Yalnızca uygulama değişikliği gerekli olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-124">That's the only application change required.</span></span> <span data-ttu-id="b2eaf-125">Şimdi, yapı ve uygulama yayımlama.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="b2eaf-126">2. adım: bir kullanıcı kimliği sütunu veritabanı şemasında ekleme</span><span class="sxs-lookup"><span data-stu-id="b2eaf-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="b2eaf-127">Ardından, biz (Kiracı) sahip bir kullanıcı her satır ilişkilendirilecek kişiler tabloya bir kullanıcı kimliği sütunu eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="b2eaf-128">Bu alan bizim EF verileri modele dahil edilecek yok böylece biz doğrudan veritabanında şema değiştirecek.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="b2eaf-129">SQL Server Management Studio veya Visual Studio kullanarak veritabanına doğrudan bağlanın ve sonra aşağıdaki T-SQL yürütün:</span><span class="sxs-lookup"><span data-stu-id="b2eaf-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="b2eaf-130">Bu kullanıcı kimliği sütunu Kişiler tablosuna ekler.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="b2eaf-131">Nvarchar(128) veri türü AspNetUsers tablosunda depolanan kullanıcı kimliklerini eşleşecek şekilde kullanırız ve şu anda SESSION_CONTEXT içinde depolanan UserID olmasını UserID yeni eklenen satırlar için otomatik olarak ayarlayacak bir DEFAULT kısıtlaması oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="b2eaf-132">Şimdi tablo şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="b2eaf-132">Now the table looks like this:</span></span>

![SSMS kişiler tablosu](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="b2eaf-134">Yeni kişiler oluşturduğunuzda, otomatik olarak doğru UserID atanmaları.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="b2eaf-135">Tanıtım amacıyla, ancak şimdi bu var olan kişileri bazılarını mevcut bir kullanıcının atayın.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="b2eaf-136">Uygulama zaten oluşturduktan birkaç kullanıcı (örneğin, yerel kullanarak, Google veya Facebook hesapları), AspNetUsers tablosunda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="b2eaf-137">Aşağıdaki ekran görüntüsünde, yalnızca bir kullanıcı yok kadarki.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-137">In the screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers tablo](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="b2eaf-139">Kopya Kimliği için user1@contoso.com, T-SQL deyiminde yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="b2eaf-140">Üç kişiler bu kullanıcı kimliği ile ilişkilendirmek için bu deyimini yürütün.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="b2eaf-141">3. adım: veritabanında bir satır düzeyi güvenlik ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b2eaf-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="b2eaf-142">Son adım UserID SESSION_CONTEXT içinde otomatik olarak sorgular tarafından döndürülen sonuçları filtrelemek için kullandığı bir güvenlik ilkesi oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="b2eaf-143">Hala veritabanına bağlı olsa da, aşağıdaki T-SQL yürütün:</span><span class="sxs-lookup"><span data-stu-id="b2eaf-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="b2eaf-144">Bu kod üç şey yapar.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-144">This code does three things.</span></span> <span data-ttu-id="b2eaf-145">İlk olarak, merkezileştirme ve RLS nesnelere erişimi sınırlamak için en iyi uygulama olarak yeni bir şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="b2eaf-146">Ardından, bir satır UserID SESSION_CONTEXT UserID eşleştiğinde '1' döndürülecek koşul bir işlev oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="b2eaf-147">Son olarak, kişiler tablosunda bir filtre ve blok koşul olarak bu işlevi ekler bir güvenlik ilkesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="b2eaf-148">Filtre koşulu geçerli kullanıcıya ait satır döndürülecek sorguları neden olur ve her zamankinden yanlışlıkla yanlış kullanıcı için bir satır ekleme uygulamanın önlemek için koruyucu engelleme koşulunun görür.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="b2eaf-149">Uygulamayı çalıştırın ve olarak oturum açın artık user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="b2eaf-150">Bu kullanıcı şimdi Biz bu UserID için daha önce atanan kişiler görür:</span><span class="sxs-lookup"><span data-stu-id="b2eaf-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="b2eaf-152">Bu daha fazla doğrulamak için yeni bir kullanıcı kaydetme deneyin.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="b2eaf-153">Hiçbiri kendilerine atanmış olduğundan hiçbir kişiler görürler.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="b2eaf-154">Yeni bir kişi oluşturmak istiyorsanız, bunları atanacak ve yalnızca görmek seçebilecekler.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2eaf-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b2eaf-155">Next steps</span></span>
<span data-ttu-id="b2eaf-156">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="b2eaf-156">That's it!</span></span> <span data-ttu-id="b2eaf-157">Basit kişi yöneticisi web uygulaması bir çok kiracılı biri her bir kullanıcı kendi kişi listesi olduğu dönüştürüldü.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="b2eaf-158">Satır düzeyi güvenlik kullanarak, biz Kiracı erişim mantığı bizim uygulama kodundaki zorlamayı karmaşıklığını kaçınılması.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="b2eaf-159">Bu saydamlık elinizdeki gerçek iş sorununu üzerinde odaklanmak uygulama izin verir ve ayrıca kullanıcının uygulamayı codebase gibi yanlışlıkla veri sızıntıları riski azaltır büyür.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="b2eaf-160">Bu öğretici yalnızca RLS ile mümkündür yüzeyine disk bozulmuş.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="b2eaf-161">Örneğin, daha gelişmiş bir mümkündür veya ayrıntılı erişim mantığı ve daha fazlasını geçerli UserID SESSION_CONTEXT depolanmasını mümkün.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="b2eaf-162">Ayrıca mümkün [RLS esnek veritabanı araçlarını istemci kitaplıkları ile tümleştirmek](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) çok kiracılı parça genişleme veri katmanındaki desteklemek için.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="b2eaf-163">Bu olanakları de RLS bile daha iyi yapmak için çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="b2eaf-164">Herhangi bir sorunuz, fikirleri veya görmek istediğiniz şey varsa, lütfen açıklamaları bize bildirin.</span><span class="sxs-lookup"><span data-stu-id="b2eaf-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="b2eaf-165">Geri bildiriminiz için teşekkür ederiz!</span><span class="sxs-lookup"><span data-stu-id="b2eaf-165">We appreciate your feedback!</span></span>

