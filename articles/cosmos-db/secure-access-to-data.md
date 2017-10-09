---
title: "aaaLearn nasıl toosecure erişim Azure Cosmos veritabanı toodata | Microsoft Docs"
description: "Azure Cosmos veritabanı ana anahtarları, salt okunur anahtarları, kullanıcılar ve izinler de dahil olmak üzere, erişim denetimi kavramları hakkında bilgi edinin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>Erişim tooAzure Cosmos DB verilerin güvenliğini sağlama
Bu makalede depolanan erişim toodata güvenli hale getirme genel bir bakış sağlar [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).

Azure Cosmos DB anahtarları tooauthenticate kullanıcılar iki tür kullanır ve tooits verilere erişmek ve kaynaklar sağlar. 

|Anahtar türü|Kaynaklar|
|---|---|
|[Ana anahtarları](#master-keys) |Yönetim kaynaklar için kullanılan: veritabanı hesapları, veritabanları, kullanıcılar ve izinler|
|[Kaynak belirteçleri](#resource-tokens)|Uygulama kaynakları için kullanılan: koleksiyonlar, belgeler, ekleri, saklı yordamlar, tetikleyiciler ve UDF'ler|

<a id="master-keys"></a>

## <a name="master-keys"></a>Ana anahtarları 

Ana anahtarları erişim toohello hello veritabanı hesabı için tüm hello yönetim kaynaklar sağlar. Ana anahtarları:  
- Erişim tooaccounts, veritabanları, kullanıcılar ve izinler sağlar. 
- Kullanılan tooprovide ayrıntılı erişim toocollections ve belgeleri olamaz.
- Bir hesap Hello oluşturma sırasında oluşturulur.
- Herhangi bir zamanda yeniden oluşturulacak.

Her hesap iki ana anahtarları oluşur: bir birincil anahtar ve ikincil anahtar. çift anahtarları hello amacı, böylelikle yeniden oluşturmak veya sürekli erişim tooyour hesabı ve verileri sağlayan, anahtarları alma. 

Toplama toohello iki ana anahtarları'hello Cosmos DB hesabı için iki salt okunur anahtar vardır. Bu salt okunur anahtarları yalnızca okuma işlemleri hello hesabındaki izin verir. Salt okunur anahtarları tooread izinleri kaynaklara erişim sağlamaz.

Birincil, ikincil, salt okunur ve okuma-yazma ana anahtarları alınabilir ve hello Azure portal kullanarak yeniden oluşturulacak. Yönergeler için bkz: [görüntüleme, kopyalama ve yeniden oluşturma erişim tuşları](manage-account.md#keys).

![Erişim denetimi (IAM) hello Azure portal - gösterilmesi NoSQL veritabanı güvenliği](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

Ana anahtarınızı döndürme hello basit işlemidir. İkincil anahtarınızı toohello Azure portal tooretrieve gidin ikincil anahtarınızı uygulamanızda birincil anahtarınızı değiştirin, sonra hello Azure portalında birincil anahtarda hello döndür.

![Merhaba NoSQL veritabanı güvenliği gösteren Azure portal - ana anahtar dönüşü](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Örnek toouse bir ana anahtar kodu

Merhaba aşağıdaki kod örneği nasıl toouse Cosmos DB uç noktası ve ana anahtar tooinstantiate bir DocumentClient hesap ve bir veritabanı oluşturmayı gösterir. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>Kaynak belirteçleri

Kaynak belirteçleri, bir veritabanı içinde toohello uygulama kaynaklarına erişim sağlamak. Kaynak belirteçleri:
- Erişim toospecific koleksiyonları, bölüm anahtarlarını, belgeler, ekleri, saklı yordamlar, tetikleyiciler ve UDF'ler sağlar.
- Ne zaman oluşturulan bir [kullanıcı](#users) verilir [izinleri](#permissions) tooa belirli kaynak.
- İzni kaynak bağlı POST, GET ve PUT çağrısı tarafından çalıştırıldığı zaman yeniden oluşturulur.
- Merhaba kullanıcı, kaynak ve izni için özel olarak oluşturulan bir karma kaynak belirteci kullanın.
- Özelleştirilebilir geçerlilik süresi ile ilişkili zamanı. Merhaba varsayılan geçerli timespan bir saattir. Belirteç ömrü, ancak açıkça, tooa en fazla beş saat belirtilebilir.
- Güvenli bir alternatif toogiving hello ana anahtar çıkışı sağlar. 
- İstemciler tooread, yazma ve silme kaynakları verilen toohello izinler göre hello Cosmos DB hesabındaki etkinleştirin.

Kaynak belirteci (Cosmos DB kullanıcılar ve izinler oluşturarak) kullanabileceğiniz tooa istemci tooprovide erişim tooresources Cosmos DB'de hesabı istediğinizde hello ana anahtar ile güvenilir olamaz.  

Cosmos DB kaynak belirteçleri istemciler tooread, yazma ve silme kaynakların verilen toohello izinler göre Cosmos DB hesabınızda ve her iki ana gerek kalmadan sağlayan güvenli bir alternatif sunar veya yalnızca anahtar okuyun.

Adlı kaynak belirteçleri istenen, oluşturulan ve tooclients teslim tipik tasarım deseni şöyledir:

1. Orta katman hizmet tooserve bir mobil uygulama tooshare kullanıcı fotoğrafı ayarlanır. 
2. Merhaba orta katman hizmet hello ana anahtarı hello Cosmos DB hesabı sahip olur.
3. Merhaba fotoğraf uygulaması son kullanıcı mobil cihazlarda yüklü. 
4. Oturum açma hello fotoğraf uygulaması hello hello Orta katmanda hizmeti ile Merhaba kullanıcının kimliğini oluşturur. Bu kimlik kuruluş tamamen toohello uygulamayı oluşturan mekanizmadır.
5. Merhaba kimlik kurulduktan sonra hello orta katman hizmet hello kimliğine göre izinleri ister.
6. Merhaba Orta katmanda hizmeti kaynak belirteci geri toohello telefon uygulaması gönderir.
7. Hello telefon uygulaması toouse hello kaynak belirteci toodirectly Cosmos DB erişimine hello kaynak belirteci tarafından ve hello kaynak belirteci tarafından izin verilen hello aralığı için tanımlanan hello izinlerle devam edebilirsiniz. 
8. Merhaba kaynak belirtecinin süresi dolduğunda, sonraki istekler bir 401 Yetkisiz özel alırsınız.  Bu noktada, hello telefon uygulaması hello kimliği yeniden oluşturur ve yeni bir kaynak belirteci ister.

    ![İş akışı Azure Cosmos DB kaynak belirteçleri](./media/secure-access-to-data/resourcekeyworkflow.png)

Kaynak belirteci oluşturma ve yönetim hello yerel Cosmos DB istemci kitaplıkları tarafından işlenir; Ancak, REST kullanırsanız hello istek/kimlik doğrulama üstbilgileri oluşturmalıdır. İçin REST kimlik doğrulama üstbilgileri oluşturma hakkında daha fazla bilgi için bkz: [Cosmos DB kaynaklarda erişim denetimi](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) veya hello [bizim SDK'ları için kaynak kodu](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Orta katman hizmet örneği toogenerate veya Aracısı kaynak belirteçleri kullanılan hello bakın [ResourceTokenBroker uygulama](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Kullanıcılar
Cosmos DB kullanıcılar Cosmos DB veritabanı ile ilişkilidir.  Her veritabanı sıfır veya daha fazla Cosmos DB kullanıcılar içerebilir.  kodun örnek gösterdiği nasıl aşağıdaki hello toocreate Cosmos DB kullanıcı kaynağı.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Her Cosmos DB kullanıcı kullanılan tooretrieve hello listesi olabilecek PermissionsLink özelliğine [izinleri](#permissions) hello kullanıcıyla ilişkili.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>İzinler
Cosmos DB izni kaynak Cosmos DB kullanıcıyla ilişkili değil.  Her bir kullanıcı, sıfır veya daha fazla Cosmos DB izinleri içerebilir.  Bir izin kaynak kullanıcı gereksinimlerini tooaccess çalışırken bir özel uygulama kaynağı hello erişim tooa güvenlik belirteci sağlar.
İzni kaynak tarafından sağlanan iki kullanılabilir erişim düzeyleri şunlardır:

* Tümü: hello kullanıcının hello kaynaktaki tam izinleri vardır.
* Şunu okuyun: hello kullanıcı hello kaynak Merhaba içeriğine yalnızca okuyabilir, ancak yazma, güncelleştirme veya silme işlemleri hello kaynakta gerçekleştiremez.

> [!NOTE]
> Sipariş toorun Cosmos DB saklı yordamlar hello kullanıcı hello hangi hello saklı yordam çalıştırılacak hello koleksiyonunda tüm izninizin olması gerekir.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Kod örnek toocreate izni

Merhaba aşağıdaki kod örneği nasıl toocreate okuma izni kaynak hello hello izni kaynağının kaynak belirteci ve hello izinleri hello ile ilişkilendirmek gösterir [kullanıcı](#users) yukarıda oluşturduğunuz.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

Koleksiyon, belge ve ek kaynaklar için sonra hello izni koleksiyonunuz için bir bölüm anahtarı de dahil etmelisiniz belirtilmişse ResourcePartitionKey toplama toohello ResourceLink hello.

### <a name="code-sample-tooread-permissions-for-user"></a>Örnek tooread kullanıcının izinlerini kod

belirli bir kullanıcı ile ilişkili tüm izni kaynakları tooeasily elde etmek için Cosmos DB kullanılabilir hale getirir izin her kullanıcı nesnesi için akış.  Hello aşağıdaki kod parçacığını nasıl tooretrieve hello izni, yukarıda oluşturduğunuz hello kullanıcıyla ilişkilendirilmiş izin listesini oluşturmak ve hello kullanıcı adına yeni bir DocumentClient örneği gösterir.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>Sonraki adımlar
* toolearn Cosmos DB veritabanı güvenliği hakkında daha fazla bilgi görmek [Cosmos DB: Veritabanı Güvenlik](database-security.md).
* ana ve salt okunur anahtarlarını yönetme hakkında toolearn bkz [nasıl toomanage bir Azure Cosmos DB hesap](manage-account.md#keys).
* tooconstruct Azure Cosmos DB yetkilendirme belirteçleri nasıl görürüm toolearn [Azure Cosmos DB kaynaklarda erişim denetimi](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
