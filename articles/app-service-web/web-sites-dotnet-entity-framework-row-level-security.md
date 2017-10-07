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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Öğreticisi: Entity Framework ve satır düzeyi güvenlik kullanarak çok Kiracı veritabanı Web uygulaması
Bu öğretici nasıl toobuild çok kiracılı web uygulamasıyla gösterir bir "[paylaşılan veritabanı, paylaşılan şema](https://msdn.microsoft.com/library/aa479086.aspx)" Entity Framework kullanarak Kiracı modeli ve [satır düzeyi güvenlik](https://msdn.microsoft.com/library/dn765131.aspx). Bu modelde, tek bir veritabanı için çok sayıda Kiracı verileri içeren ve her tablodaki her satır bir "Kiracı kimliği ile" ilişkilendirilir Satır düzeyi güvenlik (RLS), Azure SQL veritabanı için yeni bir özellik birbirinin verilerine erişmesini kullanılan tooprevent kiracılar ' dir. Bu, yalnızca tek bir, küçük değişiklikler toohello uygulama gerektirir. Merkezileştirerek hello Kiracı erişim mantığı veritabanındaki hello kendisi tarafından RLS hello uygulama kodu basitleştirir ve hello kiracılar arasında yanlışlıkla veri sızıntısı riskini azaltır.

Merhaba basit Contact Manager uygulamasından ile başlayalım [ASP.NET MVP uygulama kimlik doğrulama ve SQL DB ile oluşturup tooAzure uygulama hizmeti](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Sağ tüm kişileri Merhaba uygulaması artık, tüm kullanıcıların (kiracılar) toosee sağlar:

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Böylece kullanıcılar toothem ait mümkün toosee yalnızca hello kişiler yalnızca birkaç küçük değişikliklerle çoklu kiracı için destek ekleyeceğiz.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>1. adım: hello uygulama tooset hello SESSION_CONTEXT dinleyiciyi sınıfı ekleme
Bir uygulama değişikliği toomake ihtiyacımız var. Tüm uygulama kullanıcılarının bağlandığından toohello veritabanı kullanarak, aynı bağlantı dizesini (yani aynı SQL oturum açma) Merhaba, şu anda hangi kullanıcı onu filtre bir RLS İlkesi tooknow bir yolu yoktur. Bu yaklaşım verimli bağlantı havuzu sağlar, ancak başka bir şekilde tooidentify hello geçerli uygulama kullanıcısı hello veritabanı içinde ihtiyacımız anlamına gelir web uygulamalarında çok yaygındır. Merhaba toohave hello uygulama kümesi için bir anahtar-değer çifti çözümdür hello içinde geçerli UserID hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) hemen bağlantı açıldıktan sonra önce yürütülmeden tüm sorgular. SESSION_CONTEXT olan bir oturum kapsamlı anahtar-değer deposu ve RLS ilkemizi UserID içinde depolanan hello kullanacağı tooidentify hello geçerli kullanıcı.

Ekleyeceğiz bir [dinleyiciyi](https://msdn.microsoft.com/data/dn469464.aspx) (özellikle, bir [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), yeni bir özellik içinde Entity Framework (EF) 6, tooautomatically kümesi yürüterek hello SESSION_CONTEXT içinde geçerli UserID hello bir EF bağlantı açıldığında T-SQL ifadesi.

1. Merhaba ContactManager projesini Visual Studio'da açın.
2. Hello Çözüm Gezgini hello modelleri klasörüne sağ tıklayın ve Ekle'yi seçin > sınıfı.
3. "SessionContextInterceptor.cs" Merhaba yeni sınıf adını ve Ekle'yi tıklatın.
4. Merhaba içeriğine SessionContextInterceptor.cs koddan hello ile değiştirin.

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

Merhaba yalnızca uygulama değişikliği gerekli olmasıdır. Devam edin ve yapı ve hello uygulamayı yayımlayın.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>2. adım: bir kullanıcı kimliği sütunu toohello veritabanı şeması ekleme
Ardından, bir kullanıcıyla (Kiracı) her satır bir kullanıcı kimliği sütunu toohello kişiler tablo tooassociate tooadd ihtiyacımız var. Böylece biz tooinclude EF veri modelimizi Bu alan yoksa biz hello şemada doğrudan hello veritabanı değiştirir.

SQL Server Management Studio veya Visual Studio kullanarak toohello veritabanına doğrudan bağlanın ve aşağıdaki T-SQL hello yürütün:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Bu, bir kullanıcı kimliği sütunu toohello kişiler tablo ekler. Kullanıcı kimliklerini hello AspNetUsers tablosunda depolanan hello nvarchar(128) veri türü toomatch hello kullanırız ve hello UserID yeni eklenen satırlar toobe hello şu anda SESSION_CONTEXT içinde depolanan UserID için otomatik olarak ayarlayacak bir DEFAULT kısıtlaması oluşturuyoruz.

Şimdi hello tablo şöyle görünür:

![SSMS kişiler tablosu](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Yeni kişiler oluşturduğunuzda, otomatik olarak hello atanmaları UserID düzeltin. Tanıtım amacıyla, ancak şimdi birkaç kullanıcı var olan bu kişiler tooan atayın.

Zaten hello uygulamada oluşturduğunuz birkaç kullanıcı (örneğin, yerel kullanarak, Google veya Facebook hesapları), hello AspNetUsers tabloda görürsünüz. Merhaba ekran görüntüsünde, yalnızca bir kullanıcı yok kadarki.

![SSMS AspNetUsers tablo](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Kopya hello kimliği için user1@contoso.com, INTO hello T-SQL deyimi aşağıdaki yapıştırın. Bu kullanıcı kimliği ile Merhaba kişilerin bu deyimi tooassociate üç yürütün.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>3. adım: hello veritabanında bir satır düzeyi güvenlik ilkesi oluşturma
Merhaba son toocreate sorgular tarafından döndürülen SESSION_CONTEXT tooautomatically filtre hello sonuçları hello UserID kullanan bir güvenlik ilkesi adımdır.

Hala bağlı toohello veritabanı sırasında T-SQL aşağıdaki hello yürütün:

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

Bu kod üç şey yapar. İlk olarak, merkezileştirme ve erişim toohello RLS nesneleri sınırlamak için en iyi uygulama olarak yeni bir şema oluşturur. Ardından, hello satır UserID hello SESSION_CONTEXT UserID eşleştiğinde '1' döndürülecek koşul bir işlev oluşturur. Son olarak, bu işlev hello kişiler tablosunda bir filtre ve blok koşul olarak ekler bir güvenlik ilkesi oluşturur. Merhaba filtre koşulu toohello geçerli kullanıcıya ait yalnızca satır sorguları tooreturn neden olur ve hello engelleme koşulu her zamankinden yanlışlıkla hello yanlış kullanıcı için bir satır ekleme bir koruma tooprevent hello uygulamanın gibi davranır.

Merhaba uygulamayı çalıştırın ve olarak oturum açın artık user1@contoso.com. Bu kullanıcı şimdi biz toothis UserID daha önce atanan hello kişiler görür:

![RLS etkinleştirmeden önce Yöneticisi uygulaması başvurun](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate Bu ayrıca, deneyin yeni bir kullanıcı kaydediliyor. Hiçbiri toothem atanmış olduğundan hiçbir kişiler görürler. Yeni bir kişi oluşturun, toothem atanacak ve yalnızca mümkün toosee olacaktır.

## <a name="next-steps"></a>Sonraki adımlar
İşte bu kadar! Merhaba basit kişi yöneticisi web uygulaması bir çok kiracılı biri her bir kullanıcı kendi kişi listesi olduğu dönüştürüldü. Satır düzeyi güvenlik kullanarak, biz Kiracı erişim mantığı bizim uygulama kodundaki zorlamayı hello karmaşıklığını kaçınılması. Bu saydamlık hello uygulama toofocus elinizdeki hello gerçek iş sorunu sağlar ve ayrıca kullanıcının Merhaba uygulaması codebase gibi yanlışlıkla veri sızıntıları hello riskini azaltır büyür.

Bu öğretici yalnızca RLS ile mümkündür, çizilmiş hello yüzeyi vardır. Örneğin, olası toohave daha karmaşık olan veya ayrıntılı erişim mantığı ve onun olası toostore hello SESSION_CONTEXT içinde geçerli UserID daha fazlasını hello. Ayrıca çok mümkündür[RLS hello esnek veritabanı araçlarını istemci kitaplıkları ile tümleştirmek](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) bir genişleme veri katmanına toosupport çok kiracılı parça.

Bu olanakları de toomake RLS daha da iyi çalışıyoruz. Herhangi bir sorunuz, fikirleri veya toosee istediğiniz şey varsa, lütfen hello açıklamaları bize bildirin. Geri bildiriminiz için teşekkür ederiz!

