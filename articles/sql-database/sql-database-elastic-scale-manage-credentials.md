---
title: "Merhaba esnek veritabanı istemci Kitaplığı'nda aaaManaging kimlik | Microsoft Docs"
description: "Nasıl tooset hello doğru düzeyde kimlik bilgileri, yönetici tooread esnek veritabanı uygulamaları için yalnızca,"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 72e0edaf-795e-4856-84a5-6594f735fb7e
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 218783ca2a07e3c0a4b089aa92634f32c41386e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="credentials-used-tooaccess-hello-elastic-database-client-library"></a>Kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci kitaplığı
Merhaba [esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/) kimlik bilgileri tooaccess hello üç farklı türde kullanan [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md). Hello gerek bağlı olarak hello kimlik bilgisi hello düşük düzeyde erişim olası ile kullanın.

* **Yönetim kimlik bilgilerini**: oluşturmak veya bir parça eşleme Yöneticisi düzenleme. (Merhaba bkz [sözlüğü](sql-database-elastic-scale-glossary.md).) 
* **Erişim kimlik bilgilerini**: tooaccess var olan bir parça parça Yöneticisi tooobtain bilgilerini eşleyin.
* **Bağlantı kimlik bilgilerini**: tooconnect tooshards. 

Ayrıca bkz. [veritabanları ve Azure SQL veritabanında oturumları yönetme](sql-database-manage-logins.md). 

## <a name="about-management-credentials"></a>Yönetim kimlik bilgileri ayrıntıları
Yönetim kimlik bilgileri olan kullanılan toocreate bir [ **ShardMapManager** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) nesne parça eşlemeleri işleyen uygulamalar için. (Örneğin, [esnek veritabanı araçlarını kullanarak bir parça ekleme](sql-database-elastic-scale-add-a-shard.md) ve [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md)) hello kullanıcı hello esnek ölçek istemci kitaplığının hello SQL kullanıcılar ve SQL oturumu oluşturur ve her emin olur verilen hello genel parça hello okuma/yazma izinleri veritabanını ve tüm parça veritabanlarını da eşleyin. Değişiklikleri toohello parça eşleme gerçekleştirilir, bu kimlik bilgileri kullanılan toomaintain hello genel parça eşleme ve hello yerel parça eşlemeleri ' dir. Örneği için hello yönetim kimlik bilgileri toocreate hello parça eşleme Yöneticisi nesnesi kullanın (kullanarak [ **GetSqlShardMapManager**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx): 

    // Obtain a shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmAdminConnectionString, 
            ShardMapManagerLoadPolicy.Lazy 
    ); 

Merhaba değişkeni **smmAdminConnectionString** hello yönetim kimlik bilgilerini içeren bir bağlantı dizesi. Merhaba kullanıcı kimliği ve parola okuma/yazma erişimi tooboth parça eşleme veritabanı ve tek tek parça sağlar. Merhaba yönetim bağlantı dizesi hello sunucu adını ve veritabanını, ad tooidentify, hello genel parça, harita veritabanını da içerir. Bu amaç için tipik bağlantı dizesi şöyledir:

     "Server=<yourserver>.database.windows.net;Database=<yourdatabase>;User ID=<yourmgmtusername>;Password=<yourmgmtpassword>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;” 

Değerleri hello biçiminde kullanmayın "username@server" — yalnızca hello "username" değerini kullanın.  Bu durum, kimlik bilgileri hello parça eşleme manager veritabanı ve farklı sunucularda olabilir tek tek parça karşı çalışmanız gerekir çünkü.

## <a name="access-credentials"></a>Erişim kimlik bilgileri
Bir parça parça eşlemeleri yönetme olmayan bir uygulamada harita Yöneticisi oluştururken, hello genel parça harita üzerinde salt okuma izinlerine sahip kimlik bilgileri kullanın. Merhaba bu kimlik bilgileri altında hello genel parça eşlemesinden alındı bilgileri için kullanılır [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) ve toopopulate hello parça hello istemci önbelleği eşleyin. Merhaba aynı düzeni çok çağrı hello kimlik bilgileri sağlanır**GetSqlShardMapManager** yukarıda gösterildiği gibi: 

    // Obtain shard map manager. 
    ShardMapManager shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager( 
            smmReadOnlyConnectionString, 
            ShardMapManagerLoadPolicy.Lazy
    );  

Not hello hello **smmReadOnlyConnectionString** adına bu erişim için farklı kimlik bilgileri tooreflect hello kullanımı **yönetici olmayan** kullanıcılar: Bu kimlik bilgileri yazma sağlamalıdır değil Merhaba genel parça eşleme izinleri. 

## <a name="connection-credentials"></a>Bağlantı kimlik bilgileri
Ek kimlik bilgileri gerekli hello kullanırken [ **OpenConnectionForKey** ](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) yöntemi tooaccess parçalama anahtar ile ilişkili bir parça. Bu kimlik bilgileri, salt okunur erişim toohello yerel parça eşleme tablolarının hello parça üzerinde bulunan tooprovide izinlerinizin olması gerekir. Veri bağımlı hello parça üzerinde yönlendirme için gerekli tooperform bağlantısı doğrulama budur. Bu kod parçacığını veri erişimini veri bağımlı yönlendirme hello bağlamında sağlar: 

    using (SqlConnection conn = rangeMap.OpenConnectionForKey<int>( 
    targetWarehouse, smmUserConnectionString, ConnectionOptions.Validate)) 

Bu örnekte, **smmUserConnectionString** hello bağlantı dizesi hello için kullanıcı kimlik bilgilerini tutar. Azure SQL DB için kullanıcı kimlik bilgileri için tipik bağlantı dizesini şöyledir: 

    "User ID=<yourusername>; Password=<youruserpassword>; Trusted_Connection=False; Encrypt=True; Connection Timeout=30;”  

Merhaba yönetici kimlik'de olduğu gibi olmayan değerleri hello biçiminde "username@server". Bunun yerine, yalnızca "username" kullanın.  Ayrıca hello bağlantı dizesi bir sunucu adı ve veritabanı adı içermediğini unutmayın. Çünkü hello **OpenConnectionForKey** çağrı otomatik olarak hello bağlantı toohello parça dayalı hello anahtarı doğru doğrudan. Bu nedenle, hello veritabanı adı ve sunucu adı sağlanmadı. 

## <a name="see-also"></a>Ayrıca bkz.
[Azure SQL Veritabanında veritabanlarını ve oturum açma bilgilerini yönetme](sql-database-manage-logins.md)

[SQL Veritabanınızı güvenli hale getirme](sql-database-security-overview.md)

[Esnek veritabanı işlerine Başlarken](sql-database-elastic-jobs-getting-started.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

