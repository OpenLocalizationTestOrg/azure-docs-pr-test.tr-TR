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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="5e7e2-105">Java, Python ve Node.js ile kullanılmak üzere Hello Azure Cosmos DB öykünücüsü sertifikaları verme</span><span class="sxs-lookup"><span data-stu-id="5e7e2-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="5e7e2-106">**Merhaba öykünücüsü indirin**</span><span class="sxs-lookup"><span data-stu-id="5e7e2-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="5e7e2-107">Hello Azure Cosmos DB öykünücüsü hello Azure Cosmos DB hizmeti SSL bağlantılarını kullanımı dahil olmak üzere Geliştirme amaçlı öykünen yerel bir ortam sağlar.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="5e7e2-108">Bu post nasıl diller ve hello kendi kullanan Java gibi Windows sertifika deposunda entegre değil çalışma zamanları kullanımda tooexport hello SSL sertifikalarını gösterir [sertifika deposu](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) ve kullananPython[yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html) ve kullandığı Node.js [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="5e7e2-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="5e7e2-109">Daha fazla bilgiyi hello öykünücüsünde hakkında [geliştirme ve test etme için kullanım hello Azure Cosmos DB öykünücüsü](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="5e7e2-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="5e7e2-110">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="5e7e2-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e7e2-111">Sertifikaları döndürme</span><span class="sxs-lookup"><span data-stu-id="5e7e2-111">Rotating certificates</span></span>
> * <span data-ttu-id="5e7e2-112">SSL sertifikasını dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="5e7e2-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="5e7e2-113">Nasıl toouse hello Java, Python ve Node.js sertifikada öğrenme</span><span class="sxs-lookup"><span data-stu-id="5e7e2-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="5e7e2-114">Sertifika döndürme</span><span class="sxs-lookup"><span data-stu-id="5e7e2-114">Certification rotation</span></span>

<span data-ttu-id="5e7e2-115">Hello Azure Cosmos DB yerel öykünücüsü olan sertifikalarda hello hello öykünücüsü ilk çalıştırıldığında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="5e7e2-116">İki sertifika vardır.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-116">There are two certificates.</span></span> <span data-ttu-id="5e7e2-117">Biri toohello yerel öykünücüsü ve hello öykünücüsü içinde parolaları yönetmek için bir bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="5e7e2-118">tooexport istediğiniz hello hello kolay adı "DocumentDBEmulatorCertificate" Merhaba bağlantı sertifikasıyla sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="5e7e2-119">Her iki sertifikanın tıklayarak üretilebilir **sıfırlama verileri** Azure Cosmos DB hello Windows Tepsisi çalıştıran öykücüsünden aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="5e7e2-120">Hello sertifikaları yeniden oluşturmak ve bunları hello Java sertifika deposuna yüklediyseniz veya başka bir yerde kullanılan tooupdate gerekir bunları, aksi takdirde, uygulamanızın artık bağlanan toohello yerel öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Verileri Azure Cosmos DB yerel öykünücüsünü sıfırlayın](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="5e7e2-122">Nasıl tooexport hello Azure Cosmos DB SSL sertifikası</span><span class="sxs-lookup"><span data-stu-id="5e7e2-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="5e7e2-123">Certlm.msc çalıştırarak Hello Windows Sertifika Yöneticisi'ni başlatın ve gidin toohello kişisel -> sertifikaları klasörünü ve hello kolay ada sahip açık hello sertifika **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 1. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="5e7e2-125">Tıklayın **ayrıntıları** sonra **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-125">Click on **Details** then **OK**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 2. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="5e7e2-127">Tıklatın **kopyalama tooFile...** .</span><span class="sxs-lookup"><span data-stu-id="5e7e2-127">Click **Copy tooFile...**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 3. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="5e7e2-129">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-129">Click **Next**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 4. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="5e7e2-131">Tıklatın **Hayır, özel anahtarı verme**, ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 5. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="5e7e2-133">Tıklayın **Base-64 ile kodlanmış X.509 (. CER)** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 6. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="5e7e2-135">Merhaba sertifika bir ad verin.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-135">Give hello certificate a name.</span></span> <span data-ttu-id="5e7e2-136">Bu durumda **documentdbemulatorcert** ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü verme 7. adım](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="5e7e2-138">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-138">Click **Finish**.</span></span>

    ![Azure Cosmos DB yerel öykünücüsü 8. adımda dışarı aktarma](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="5e7e2-140">Nasıl toouse hello Java sertifikada</span><span class="sxs-lookup"><span data-stu-id="5e7e2-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="5e7e2-141">Java uygulamalarını veya hello Java istemcisi kullanan MongoDB uygulamaları çalıştırırken daha kolay tooinstall hello sertifika hello Java varsayılan sertifika deposuna geçirme hello daha olan "-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= "<password>" bayrakları.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="5e7e2-142">Örneğin dahil hello [Java Demo uygulama](https://localhost:8081/_explorer/index.html) hello varsayılan sertifika deposuna bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="5e7e2-143">Merhaba Hello yönergeleri izleyin [sertifika toohello Java CA deposuna sertifika ekleme](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 Sertifika hello varsayılan Java sertifika deposuna.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="5e7e2-144">İçinde kalmasını keytool çalıştırırken hello % JAVA_HOME % dizininde unutmayın çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="5e7e2-145">Bir kez "CosmosDBEmulatorCertificate" SSL hello sertifika yüklü kullanım hello yerel Azure Cosmos DB öykünücüsü ve uygulamanızı mümkün tooconnect olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="5e7e2-146">Toohave sorun devam ederse toofollow hello isteyebilirsiniz [hata ayıklama SSL/TLS bağlantılarını](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) makalesi.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="5e7e2-147">Büyük olasılıkla hello %JAVA_HOME%/jre/lib/security/cacerts deposuna hello sertifika yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="5e7e2-148">Java uygulamanızı yüklü birden fazla sürümünü varsa örnek farklı cacerts deposu biri, güncelleştirilmiş hello daha kullanabilecek için.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="5e7e2-149">Nasıl toouse hello Python sertifikada</span><span class="sxs-lookup"><span data-stu-id="5e7e2-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="5e7e2-150">Varsayılan hello tarafından [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) Merhaba DocumentDB API değil deneyin ve toohello yerel öykünücüsü bağlanırken hello SSL sertifikası kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="5e7e2-151">Toouse SSL doğrulama istiyor ancak hello hello örneklerde takip edebilirsiniz, [Python yuva sarmalayıcıları](https://docs.python.org/2/library/ssl.html) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="5e7e2-152">Nasıl toouse hello Node.js sertifikada</span><span class="sxs-lookup"><span data-stu-id="5e7e2-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="5e7e2-153">Varsayılan hello tarafından [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) Merhaba DocumentDB API değil deneyin ve toohello yerel öykünücüsü bağlanırken hello SSL sertifikası kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="5e7e2-154">Toouse SSL doğrulama istiyor ancak hello hello örneklerde takip edebilirsiniz, [Node.js belgelerine](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="5e7e2-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e7e2-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e7e2-155">Next steps</span></span>

<span data-ttu-id="5e7e2-156">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="5e7e2-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e7e2-157">Döndürülen sertifikaları</span><span class="sxs-lookup"><span data-stu-id="5e7e2-157">Rotated certificates</span></span>
> * <span data-ttu-id="5e7e2-158">Dışarı aktarılan hello SSL sertifikası</span><span class="sxs-lookup"><span data-stu-id="5e7e2-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="5e7e2-159">Nasıl toouse hello Java, Python ve Node.js sertifikada öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="5e7e2-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="5e7e2-160">Şimdi toohello Cosmos DB hakkında daha fazla bilgi için kavramları bölümüne geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e7e2-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e7e2-161">Genel dağıtım</span><span class="sxs-lookup"><span data-stu-id="5e7e2-161">Global distribution</span></span>](distribute-data-globally.md) 
