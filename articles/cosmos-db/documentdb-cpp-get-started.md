---
title: "aaaC ++ Azure Cosmos DB Öğreticisi | Microsoft Docs"
description: "C++ için Azure Cosmos DB onaylı bir SDK’yı kullanarak bir C++ veritabanı ve konsol uygulaması oluşturan öğretici. Azure Cosmos DB, çok büyük ölçekli bir veritabanı hizmetidir."
services: cosmos-db
documentationcenter: cpp
author: asthana86
manager: jhubbard
editor: 
ms.assetid: b8756b60-8d41-4231-ba4f-6cfcfe3b4bab
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 12/25/2016
ms.author: aasthan
ms.openlocfilehash: 2d5eeff349b7753e39936b7eb77557ad30c5830a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-c-console-application-tutorial-for-hello-documentdb-api"></a>Azure Cosmos DB: Merhaba DocumentDB API C++ konsol uygulaması Öğreticisi
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB için Node.js](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 
 

Hoş Geldiniz toohello C++ öğretici hello Azure Cosmos DB DocumentDB API için C++ için SDK Destekli! Bu öğreticiden yararlandıktan sonra, bir C++ veritabanı dahil olmak üzere Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.

Şu konulara değineceğiz:

* Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma
* Uygulamanızı kurma
* C++ Azure Cosmos DB veritabanı oluşturma
* Koleksiyon oluşturma
* JSON belgeleri oluşturma
* Merhaba koleksiyonu sorgulama
* Bir belgeyi değiştirme
* Bir belgeyi silme
* Merhaba C++ Azure Cosmos DB veritabanı siliniyor

Zamanınız yok mu? Endişelenmeyin! Merhaba eksiksiz bir çözüm edinilebilir [GitHub](https://github.com/stalker314314/DocumentDBCpp). Bkz: [alma hello eksiksiz bir çözüm](#GetSolution) hızlı yönergeler için.

Merhaba C++ öğreticiyi tamamladıktan sonra lütfen hello kullan oylama hello bu sayfa toogive sonunda bize geri bildirim düğmeler. 

Bize istiyorsanız toocontact doğrudan düşündüğünüz ücretsiz tooinclude e-posta adresi, yorumlarınızı veya [toous burada ulaşmak](https://www.research.net/r/8BKRJ3Z). 

Şimdi başlayalım!

## <a name="prerequisites-for-hello-c-tutorial"></a>Merhaba C++ öğreticisi için Önkoşullar
Merhaba aşağıdaki sahip olduğunuzdan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [Ücretsiz Azure Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* [Visual Studio](https://www.visualstudio.com/downloads/), hello C++ dil bileşenlerinin yüklü ile.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1. Adım: Azure Cosmos DB hesabı oluşturma
Bir Azure Cosmos DB hesabı oluşturalım. Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[C++ uygulamanızı kurma](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupC++"></a>2. Adım: C++ uygulamanızı ayarlama
1. Visual Studio'yu açın ve ardından hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**. 
2. Merhaba, **yeni proje** penceresinde hello **yüklü** bölmesinde genişletin **Visual C++**, tıklatın **Win32**ve ardından  **Win32 konsol uygulaması**. Merhaba proje hellodocumentdb olarak adlandırın ve ardından **Tamam**. 
   
    ![Merhaba Yeni Proje Sihirbazı ekran görüntüsü](media/documentdb-cpp-get-started/hello.png)
3. Win32 Uygulama Sihirbazı'nı Hello başladığında tıklayın **son**.
4. Merhaba Proje oluşturulduktan sonra hello NuGet Paket Yöneticisi hello sağ tıklayarak açın **hellodocumentdb** proje **Çözüm Gezgini** tıklatıp **NuGet paketlerini Yönet**. 
   
    ![NuGet paketini Yönet hello Proje menüsünde gösteren ekran görüntüsü](media/documentdb-cpp-get-started/nuget.png)
5. Merhaba, **NuGet: hellodocumentdb** sekmesini tıklatın, **Gözat**, arayın ve sonra *documentdbcpp*. Merhaba sonuçlarında DocumentDbCPP, hello ekran aşağıdaki gösterildiği gibi seçin. Bu paketi başvuruları tooC ++ REST SDK hello DocumentDbCPP için bağımlılık olduğu yükler.  
   
    ![Vurgulanan gösteren ekran görüntüsü hello DocumentDbCpp paketi](media/documentdb-cpp-get-started/cpp.png)
   
    Merhaba paketleri tooyour proje eklendikten sonra tüm kümesi toostart biraz kod yazmaya duyuyoruz.   

## <a id="Config"></a>3. Adım: Azure Cosmos DB veritabanınıza yönelik bağlantı ayrıntılarını Azure portaldan kopyalama
Ortaya çıkarmak [Azure portal](https://portal.azure.com) ve çapraz oluşturduğunuz toohello Azure Cosmos DB veritabanı hesabı. Bizim C++ kod parçacığını biz hello URI ve hello sonraki adım tooestablish bağlantı Azure portalından hello birincil anahtar gerekir. 

![Azure Cosmos DB URI ve anahtarları'hello Azure portalı](media/documentdb-cpp-get-started/nosql-tutorial-keys.png)

## <a id="Connect"></a>4. adım: tooan Azure Cosmos DB hesap bağlanma
1. Üstbilgiler ve ad alanlarını tooyour kaynak kodu, sonra aşağıdaki hello eklemek `#include "stdafx.h"`.
   
        #include <cpprest/json.h>
        #include <documentdbcpp\DocumentClient.h>
        #include <documentdbcpp\exceptions.h>
        #include <documentdbcpp\TriggerOperation.h>
        #include <documentdbcpp\TriggerType.h>
        using namespace documentdb;
        using namespace std;
        using namespace web::json;
2. Sonraki hello aşağıdaki kod tooyour main işlevi ve hello hesabı yapılandırması birincil anahtar toomatch 3. adımındaki Azure Cosmos DB ayarlarınızı değiştirip ekleyin. 
   
        DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
        DocumentClient client (conf);
   
    Merhaba kod tooinitialize hello documentdb istemci sahip olduğunuza göre Azure Cosmos DB kaynaklarla çalışmak bir bakalım.

## <a id="CreateDBColl"></a>5. Adım: C++ veritabanı ve koleksiyonu oluşturma
Biz bu adımı gerçekleştirmeden önce nasıl bir veritabanı, koleksiyon ve belgeler için olanlar da yeni tooAzure Cosmos DB olan etkileşim üzerinden edelim. [Veritabanı](documentdb-resources.md#databases), koleksiyonlar genelinde bölümlenmiş belge depolama alanının mantıksal bir kapsayıcısıdır. A [koleksiyonu](documentdb-resources.md#collections) hello ilişkili JavaScript uygulama mantığının ve JSON belgelerinin bir kapsayıcıdır. Hello Azure Cosmos DB hiyerarşik kaynak modeli ve konuları hakkında daha fazla bilgi edinmek [Azure Cosmos DB hiyerarşik kaynak modeli ve kavramları](documentdb-resources.md).

Veritabanı bir toocreate ve karşılık gelen koleksiyon kod toohello ana işlevinizi sonuna aşağıdaki hello ekleyin. Bu, 'FamilyRegistry' ve 'hello önceki adımda bildirilen hello İstemci Yapılandırması'nı kullanarak FamilyCollection' adlı bir koleksiyon adı verilen bir veritabanı oluşturur.

    try {
      shared_ptr<Database> db = client.CreateDatabase(L"FamilyRegistry");
      shared_ptr<Collection> coll = db->CreateCollection(L"FamilyCollection");
    } catch (DocumentDBRuntimeException ex) {
      wcout << ex.message();
    }


## <a id="CreateDoc"></a>6. Adım: Belge oluşturma
[Belgeler](documentdb-resources.md#documents), kullanıcı tanımlı (rastgele) JSON içeriğidir. Artık Azure Cosmos DB'ye bir belge yerleştirebilirsiniz. Bir belge hello main işlevi hello sonuna koddan hello kopyalayarak oluşturabilirsiniz. 

    try {
      value document_family;
      document_family[L"id"] = value::string(L"AndersenFamily");
      document_family[L"FirstName"] = value::string(L"Thomas");
      document_family[L"LastName"] = value::string(L"Andersen");
      shared_ptr<Document> doc = coll->CreateDocumentAsync(document_family).get();

      document_family[L"id"] = value::string(L"WakefieldFamily");
      document_family[L"FirstName"] = value::string(L"Lucy");
      document_family[L"LastName"] = value::string(L"Wakefield");
      doc = coll->CreateDocumentAsync(document_family).get();
    } catch (ResourceAlreadyExistsException ex) {
      wcout << ex.message();
    }

toosummarize, bu kod bir Azure Cosmos DB veritabanı, koleksiyon ve belge Gezgini Azure portalında sorgulayabilirsiniz belgeler oluşturur. 

![C++ Öğreticisi - hello hello hesabı, hello veritabanı, hello koleksiyonu ve hello belgeler arasındaki hiyerarşik ilişkiyi gösteren diyagram](media/documentdb-cpp-get-started/docs.png)

## <a id="QueryDB"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama
Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler. Merhaba aşağıdaki örnek kod hello önceki adımda oluşturduğumuz hello belgeleri karşı çalıştırabilirsiniz SQL söz dizimi kullanılarak yapılan bir sorguyu gösterir.

benzersiz tanımlayıcı veya kaynak kimliği hello veritabanı ve hello belge istemci birlikte hello koleksiyonu için bağımsız değişkenler hello gibi hello işlevi alır. Bu kodu ana işlevden önce ekleyin.

    void executesimplequery(const DocumentClient &client,
                            const wstring dbresourceid,
                            const wstring collresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        wstring coll_name = coll->id();
        shared_ptr<DocumentIterator> iter =
            coll->QueryDocumentsAsync(wstring(L"SELECT * FROM " + coll_name)).get();
        wcout << "\n\nQuerying collection:";
        while (iter->HasMore()) {
          shared_ptr<Document> doc = iter->Next();
          wstring doc_name = doc->id();
          wcout << "\n\t" << doc_name << "\n";
          wcout << "\t"
                << "[{\"FirstName\":"
                << doc->payload().at(U("FirstName")).as_string()
                << ",\"LastName\":" << doc->payload().at(U("LastName")).as_string()
                << "}]";
        }
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Replace"></a>8. Adım: Bir belgeyi değiştirme
Azure Cosmos DB hello kod aşağıdaki gösterildiği gibi JSON belgelerini değiştirmeyi destekler. Merhaba executesimplequery işlevi sonra bu kodu ekleyin.

    void replacedocument(const DocumentClient &client, const wstring dbresourceid,
                         const wstring collresourceid,
                         const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        value newdoc;
        newdoc[L"id"] = value::string(L"WakefieldFamily");
        newdoc[L"FirstName"] = value::string(L"Lucy");
        newdoc[L"LastName"] = value::string(L"Smith Wakefield");
        coll->ReplaceDocument(docresourceid, newdoc);
      } catch (DocumentDBRuntimeException ex) {
        throw;
      }
    }

## <a id="Delete"></a>9. Adım: Bir belgeyi silme
JSON belgeleri silmeyi azure Cosmos DB destekler, kopyalama ve yapıştırma hello koddan sonra hello replacedocument işlevi tarafından bunu yapabilirsiniz. 

    void deletedocument(const DocumentClient &client, const wstring dbresourceid,
                        const wstring collresourceid, const wstring docresourceid) {
      try {
        client.GetDatabase(dbresourceid).get();
        shared_ptr<Database> db = client.GetDatabase(dbresourceid);
        shared_ptr<Collection> coll = db->GetCollection(collresourceid);
        coll->DeleteDocumentAsync(docresourceid).get();
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="DeleteDB"></a>10. Adım: Bir veritabanını silme
Oluşturulan hello veritabanı siliniyor hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.

Kod parçacığını (işlevi temizleme) hello deletedocument işlevi tooremove hello veritabanı ve tüm hello alt kaynakları sonra aşağıdaki hello kopyalayıp yeniden açın.

    void deletedb(const DocumentClient &client, const wstring dbresourceid) {
      try {
        client.DeleteDatabase(dbresourceid);
      } catch (DocumentDBRuntimeException ex) {
        wcout << ex.message();
      }
    }

## <a id="Run"></a>11. Adım: C++ uygulamanızı hep birlikte çalıştırın!
Biz kod toocreate artık eklemiş olduğunuz, sorgu, değiştirmek ve farklı Azure Cosmos DB kaynakları silin.  Bize şimdi bu yukarı bizim main işlevi hellodocumentdb.cpp bazı tanılama iletileri ile birlikte gelen çağrıları toothese farklı işlevler ekleyerek bağlayın.

Merhaba main işlevi, uygulamanızın koddan hello ile değiştirerek bunu yapabilirsiniz. Bu yazma hello account_configuration_uri ve 3. adımında, hello koda kopyaladığınız primary_key üzerinden şekilde kaydedin bu satırı ya da kopyalama hello değer yeniden hello portalından. 

    int main() {
        try {
            // Start by defining your account's configuration
            DocumentDBConfiguration conf (L"<account_configuration_uri>", L"<primary_key>");
            // Create your client
            DocumentClient client(conf);
            // Create a new database
            try {
                shared_ptr<Database> db = client.CreateDatabase(L"FamilyDB");
                wcout << "\nCreating database:\n" << db->id();
                // Create a collection inside database
                shared_ptr<Collection> coll = db->CreateCollection(L"FamilyColl");
                wcout << "\n\nCreating collection:\n" << coll->id();
                value document_family;
                document_family[L"id"] = value::string(L"AndersenFamily");
                document_family[L"FirstName"] = value::string(L"Thomas");
                document_family[L"LastName"] = value::string(L"Andersen");
                shared_ptr<Document> doc =
                    coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                document_family[L"id"] = value::string(L"WakefieldFamily");
                document_family[L"FirstName"] = value::string(L"Lucy");
                document_family[L"LastName"] = value::string(L"Wakefield");
                doc = coll->CreateDocumentAsync(document_family).get();
                wcout << "\n\nCreating document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                replacedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nReplaced document:\n" << doc->id();
                executesimplequery(client, db->resource_id(), coll->resource_id());
                deletedocument(client, db->resource_id(), coll->resource_id(),
                    doc->resource_id());
                wcout << "\n\nDeleted document:\n" << doc->id();
                deletedb(client, db->resource_id());
                wcout << "\n\nDeleted db:\n" << db->id();
                cin.get();
            }
            catch (ResourceAlreadyExistsException ex) {
                wcout << ex.message();
            }
        }
        catch (DocumentDBRuntimeException ex) {
            wcout << ex.message();
        }
        cin.get();
    }

Artık mümkün toobuild olması ve F5 tuşuna basarak Visual Studio'da kodunuzu çalıştırmak veya gerekir alternatif olarak hello uygulama bulma ve çalıştırarak terminal penceresinde hello yürütülebilir hello. 

Merhaba Başlarken uygulamanızın çıktısını görmeniz gerekir. Merhaba çıkış ekran aşağıdaki hello eşleşmelidir.

![Azure Cosmos DB C++ uygulama çıktısı](media/documentdb-cpp-get-started/console.png)

Tebrikler! Merhaba C++ öğreticisini tamamladınız ve İlk Azure Cosmos DB konsol uygulamanız sahip!

## <a id="GetSolution"></a>Merhaba tam C++ Öğreticisi çözümünü edinme
Bu makaledeki tüm hello örnekleri içeren toobuild hello GetStarted çözümünü hello aşağıdaki gerekir:

* [Azure Cosmos DB hesabı][create-account].
* Merhaba [GetStarted](https://github.com/stalker314314/DocumentDBCpp) çözüm Github'da kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).
* Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).
* Merhaba hello hello geliştirme bölümünde programlama modelleri hakkında daha fazla bilgi edinin [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account


