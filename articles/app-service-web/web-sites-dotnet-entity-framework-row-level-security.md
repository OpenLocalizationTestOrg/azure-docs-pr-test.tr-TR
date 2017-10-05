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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Öğreticisi: Entity Framework ve satır düzeyi güvenlik kullanarak çok Kiracı veritabanı Web uygulaması
Bu öğretici ile çok kiracılı web uygulamasının nasıl oluşturulacağını gösterir bir "[paylaşılan veritabanı, paylaşılan şema](https://msdn.microsoft.com/library/aa479086.aspx)" Entity Framework kullanarak Kiracı modeli ve [satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131.aspx). Bu modelde, tek bir veritabanı için çok sayıda Kiracı verileri içeren ve her tablodaki her satır bir "Kiracı kimliği ile" ilişkilendirilir Satır düzeyi güvenlik (RLS), Azure SQL veritabanı için yeni bir özellik, kiracıların diğer kişilerin veri erişimini engellemek için kullanılır. Bu yalnızca bir tek, küçük bir değişiklik uygulama gerektirir. Veritabanının içindeki Kiracı erişim mantığı merkezileştirerek tarafından RLS uygulama kodu basitleştirir ve kiracılar arasında yanlışlıkla veri sızıntısı riskini azaltır.

Basit Contact Manager uygulamasından ile başlayalım [auth ve SQL DB ile bir ASP.NET MVP uygulama oluşturun ve Azure App Service'e dağıtma](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Sağ şimdi, tüm kullanıcıların tüm kişileri görmek için (kiracılar) uygulama verir:

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Böylece kullanıcılar yalnızca kendilerine ait olan kişileri görebilmek için birkaç küçük değişikliklerle çoklu kiracı için destek ekleyeceğiz.

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a>1. adım: SESSION_CONTEXT ayarlamak için uygulamada dinleyiciyi sınıfı ekleme
Bir uygulama değişikliği yapmak için ihtiyacımız var. Tüm uygulama kullanıcılarının aynı bağlantı dizesini (yani aynı SQL oturum açma) kullanarak veritabanına bağlanmak için da şu anda hangi kullanıcı için filtre öğrenmek bir RLS İlkesi yolu yoktur. Bu yaklaşım verimli bağlantı havuzu sağlar, ancak veritabanı içinde geçerli uygulama kullanıcıyı tanımlamak için bir başka yolu ihtiyacımız anlamına gelir web uygulamalarında çok yaygındır. Çözüm geçerli UserID için bir anahtar-değer çifti kümesi uygulama yapmaktır [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) hemen bağlantı açıldıktan sonra önce yürütülmeden tüm sorgular. Bir oturum kapsamlı anahtar-değer deposu SESSION_CONTEXT olduğu ve RLS ilkemizi depolanan UserID geçerli kullanıcıyı tanımlamak için kullanır.

Ekleyeceğiz bir [dinleyiciyi](https://msdn.microsoft.com/data/dn469464.aspx) (özellikle, bir [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), yeni bir özellik içinde Entity Framework (T-SQL yürüterek geçerli UserID SESSION_CONTEXT otomatik olarak ayarlamak için EF) 6, EF bağlantı açıldığında deyimi.

1. ContactManager projesini Visual Studio'da açın.
2. Çözüm Gezgini'nde modeller klasörü sağ tıklatın ve Ekle'yi seçin > sınıfı.
3. Yeni sınıf "SessionContextInterceptor.cs" ve Ekle'yi tıklatın.
4. SessionContextInterceptor.cs içeriğini aşağıdaki kodla değiştirin.

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

Yalnızca uygulama değişikliği gerekli olmasıdır. Şimdi, yapı ve uygulama yayımlama.

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a>2. adım: bir kullanıcı kimliği sütunu veritabanı şemasında ekleme
Ardından, biz (Kiracı) sahip bir kullanıcı her satır ilişkilendirilecek kişiler tabloya bir kullanıcı kimliği sütunu eklemeniz gerekir. Bu alan bizim EF verileri modele dahil edilecek yok böylece biz doğrudan veritabanında şema değiştirecek.

SQL Server Management Studio veya Visual Studio kullanarak veritabanına doğrudan bağlanın ve sonra aşağıdaki T-SQL yürütün:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Bu kullanıcı kimliği sütunu Kişiler tablosuna ekler. Nvarchar(128) veri türü AspNetUsers tablosunda depolanan kullanıcı kimliklerini eşleşecek şekilde kullanırız ve şu anda SESSION_CONTEXT içinde depolanan UserID olmasını UserID yeni eklenen satırlar için otomatik olarak ayarlayacak bir DEFAULT kısıtlaması oluşturuyoruz.

Şimdi tablo şöyle görünür:

![SSMS kişiler tablosu](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Yeni kişiler oluşturduğunuzda, otomatik olarak doğru UserID atanmaları. Tanıtım amacıyla, ancak şimdi bu var olan kişileri bazılarını mevcut bir kullanıcının atayın.

Uygulama zaten oluşturduktan birkaç kullanıcı (örneğin, yerel kullanarak, Google veya Facebook hesapları), AspNetUsers tablosunda görürsünüz. Aşağıdaki ekran görüntüsünde, yalnızca bir kullanıcı yok kadarki.

![SSMS AspNetUsers tablo](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Kopya Kimliği için user1@contoso.com, T-SQL deyiminde yapıştırın. Üç kişiler bu kullanıcı kimliği ile ilişkilendirmek için bu deyimini yürütün.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a>3. adım: veritabanında bir satır düzeyi güvenlik ilkesi oluşturma
Son adım UserID SESSION_CONTEXT içinde otomatik olarak sorgular tarafından döndürülen sonuçları filtrelemek için kullandığı bir güvenlik ilkesi oluşturmaktır.

Hala veritabanına bağlı olsa da, aşağıdaki T-SQL yürütün:

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

Bu kod üç şey yapar. İlk olarak, merkezileştirme ve RLS nesnelere erişimi sınırlamak için en iyi uygulama olarak yeni bir şema oluşturur. Ardından, bir satır UserID SESSION_CONTEXT UserID eşleştiğinde '1' döndürülecek koşul bir işlev oluşturur. Son olarak, kişiler tablosunda bir filtre ve blok koşul olarak bu işlevi ekler bir güvenlik ilkesi oluşturur. Filtre koşulu geçerli kullanıcıya ait satır döndürülecek sorguları neden olur ve her zamankinden yanlışlıkla yanlış kullanıcı için bir satır ekleme uygulamanın önlemek için koruyucu engelleme koşulunun görür.

Uygulamayı çalıştırın ve olarak oturum açın artık user1@contoso.com. Bu kullanıcı şimdi Biz bu UserID için daha önce atanan kişiler görür:

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

Bu daha fazla doğrulamak için yeni bir kullanıcı kaydetme deneyin. Hiçbiri kendilerine atanmış olduğundan hiçbir kişiler görürler. Yeni bir kişi oluşturmak istiyorsanız, bunları atanacak ve yalnızca görmek seçebilecekler.

## <a name="next-steps"></a>Sonraki adımlar
İşte bu kadar! Basit kişi yöneticisi web uygulaması bir çok kiracılı biri her bir kullanıcı kendi kişi listesi olduğu dönüştürüldü. Satır düzeyi güvenlik kullanarak, biz Kiracı erişim mantığı bizim uygulama kodundaki zorlamayı karmaşıklığını kaçınılması. Bu saydamlık elinizdeki gerçek iş sorununu üzerinde odaklanmak uygulama izin verir ve ayrıca kullanıcının uygulamayı codebase gibi yanlışlıkla veri sızıntıları riski azaltır büyür.

Bu öğretici yalnızca RLS ile mümkündür yüzeyine disk bozulmuş. Örneğin, daha gelişmiş bir mümkündür veya ayrıntılı erişim mantığı ve daha fazlasını geçerli UserID SESSION_CONTEXT depolanmasını mümkün. Ayrıca mümkün [RLS esnek veritabanı araçlarını istemci kitaplıkları ile tümleştirmek](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) çok kiracılı parça genişleme veri katmanındaki desteklemek için.

Bu olanakları de RLS bile daha iyi yapmak için çalışıyoruz. Herhangi bir sorunuz, fikirleri veya görmek istediğiniz şey varsa, lütfen açıklamaları bize bildirin. Geri bildiriminiz için teşekkür ederiz!

