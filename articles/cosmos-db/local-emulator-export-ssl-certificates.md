---
title: "aaaExport hello Azure Cosmos DB öykünücüsü sertifikaları | Microsoft Docs"
description: "Diller ve hello Windows sertifika deposunda kullanmayın çalışma zamanları geliştirirken hello SSL sertifikalarını yönetmenize ve tooexport gerekir. Bu post adım adım yönergeler sağlar."
services: cosmos-db
documentationcenter: 
keywords: "Azure Cosmos DB öykünücüsü"
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Java, Python ve Node.js ile kullanılmak üzere Hello Azure Cosmos DB öykünücüsü sertifikaları verme

[**Merhaba öykünücüsü indirin**](https://aka.ms/cosmosdb-emulator)

Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmeti SSL bağlantılarını kullanımı dahil olmak üzere Geliştirme amaçlı öykünen yerel bir ortam sağlar. Bu post nasıl diller ve hello kendi kullanan Java gibi Windows sertifika deposunda entegre değil çalışma zamanları kullanımda tooexport hello SSL sertifikalarını gösterir [sertifika deposu](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) ve kullananPython[yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html) ve kullandığı Node.js [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Daha fazla bilgiyi hello öykünücüsünde hakkında [geliştirme ve test etme için kullanım hello Azure Cosmos DB öykünücüsü](./local-emulator.md).

Bu öğretici hello aşağıdaki görevleri içerir:

> [!div class="checklist"]
> * Sertifikaları döndürme
> * SSL sertifikasını dışarı aktarma
> * Nasıl toouse hello Java, Python ve Node.js sertifikada öğrenme

## <a name="certification-rotation"></a>Sertifika döndürme

Hello Azure Cosmos DB yerel öykünücüsü olan sertifikalarda hello hello öykünücüsü ilk çalıştırıldığında oluşturulur. İki sertifika vardır. Biri toohello yerel öykünücüsü ve hello öykünücüsü içinde parolaları yönetmek için bir bağlanmak için kullanılır. tooexport istediğiniz hello hello kolay adı "DocumentDBEmulatorCertificate" Merhaba bağlantı sertifikasıyla sertifikasıdır.

Her iki sertifikanın tıklayarak üretilebilir **sıfırlama verileri** Azure Cosmos DB hello Windows Tepsisi çalıştıran öykücüsünden aşağıda gösterildiği gibi. Hello sertifikaları yeniden oluşturmak ve bunları hello Java sertifika deposuna yüklediyseniz veya başka bir yerde kullanılan tooupdate gerekir bunları, aksi takdirde, uygulamanızın artık bağlanan toohello yerel öykünücüsü.

![Verileri Azure Cosmos DB yerel öykünücüsünü sıfırlayın](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Nasıl tooexport hello Azure Cosmos DB SSL sertifikası

1. Certlm.msc çalıştırarak Hello Windows Sertifika Yöneticisi'ni başlatın ve gidin toohello kişisel -> sertifikaları klasörünü ve hello kolay ada sahip açık hello sertifika **DocumentDbEmulatorCertificate**.

    ![Azure Cosmos DB yerel öykünücüsü verme 1. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Tıklayın **ayrıntıları** sonra **Tamam**.

    ![Azure Cosmos DB yerel öykünücüsü verme 2. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Tıklatın **kopyalama tooFile...** .

    ![Azure Cosmos DB yerel öykünücüsü verme 3. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. **İleri**’ye tıklayın.

    ![Azure Cosmos DB yerel öykünücüsü verme 4. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Tıklatın **Hayır, özel anahtarı verme**, ardından **sonraki**.

    ![Azure Cosmos DB yerel öykünücüsü verme 5. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Tıklayın **Base-64 ile kodlanmış X.509 (. CER)** ve ardından **sonraki**.

    ![Azure Cosmos DB yerel öykünücüsü verme 6. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Merhaba sertifika bir ad verin. Bu durumda **documentdbemulatorcert** ve ardından **sonraki**.

    ![Azure Cosmos DB yerel öykünücüsü verme 7. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. **Son**'a tıklayın.

    ![Azure Cosmos DB yerel öykünücüsü 8. adımda dışarı aktarma](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Nasıl toouse hello Java sertifikada

Java uygulamalarını veya hello Java istemcisi kullanan MongoDB uygulamaları çalıştırırken daha kolay tooinstall hello sertifika hello Java varsayılan sertifika deposuna geçirme hello daha olan "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" bayrakları. Örneğin dahil hello [Java Demo uygulama](https://localhost:8081/_explorer/index.html) hello varsayılan sertifika deposuna bağlıdır.

Merhaba Hello yönergeleri izleyin [sertifika toohello Java CA deposuna sertifika ekleme](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 Sertifika hello varsayılan Java sertifika deposuna. İçinde kalmasını keytool çalıştırırken hello % JAVA_HOME % dizininde unutmayın çalışacaksınız.

Bir kez "CosmosDBEmulatorCertificate" SSL hello sertifika yüklü kullanım hello yerel Azure Cosmos DB öykünücüsü ve uygulamanızı mümkün tooconnect olması gerekir. Toohave sorun devam ederse toofollow hello isteyebilirsiniz [hata ayıklama SSL/TLS bağlantılarını](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) makalesi. Büyük olasılıkla hello %JAVA_HOME%/jre/lib/security/cacerts deposuna hello sertifika yüklü değil. Java uygulamanızı yüklü birden fazla sürümünü varsa örnek farklı cacerts deposu biri, güncelleştirilmiş hello daha kullanabilecek için.

## <a name="how-toouse-hello-certificate-in-python"></a>Nasıl toouse hello Python sertifikada

Varsayılan hello tarafından [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) Merhaba DocumentDB API değil deneyin ve toohello yerel öykünücüsü bağlanırken hello SSL sertifikası kullanın. Toouse SSL doğrulama istiyor ancak hello hello örneklerde takip edebilirsiniz, [Python yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html) belgeleri.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Nasıl toouse hello Node.js sertifikada

Varsayılan hello tarafından [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) Merhaba DocumentDB API değil deneyin ve toohello yerel öykünücüsü bağlanırken hello SSL sertifikası kullanın. Toouse SSL doğrulama istiyor ancak hello hello örneklerde takip edebilirsiniz, [Node.js belgelerine](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Döndürülen sertifikaları
> * Dışarı aktarılan hello SSL sertifikası
> * Nasıl toouse hello Java, Python ve Node.js sertifikada öğrendiniz

Şimdi toohello Cosmos DB hakkında daha fazla bilgi için kavramları bölümüne geçebilirsiniz.

> [!div class="nextstepaction"]
> [Genel dağıtım](distribute-data-globally.md) 
