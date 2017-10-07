---
title: "aaaAdd hello Oracle Veritabanı Bağlayıcısı Azure Logic Apps içinde | Microsoft Docs"
description: "Bir mantıksal uygulama Hello Oracle Veritabanı Bağlayıcısı kullanma"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="e84ec-103">Merhaba Oracle Veritabanı Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e84ec-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="e84ec-104">Merhaba Oracle Veritabanı Bağlayıcısı'nı kullanarak, varolan bir veritabanında veri kullanan kurumsal iş akışları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e84ec-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="e84ec-105">Bu bağlayıcı, şirket içi Oracle veritabanına veya Oracle veritabanı içeren bir Azure sanal makinesi yüklü tooan bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="e84ec-106">Bu bağlayıcı ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e84ec-106">With this connector, you can:</span></span>

* <span data-ttu-id="e84ec-107">Yeni bir müşteri tooa müşteriler veritabanı ekleyerek veya bir sırada siparişler veritabanını güncelleştirmek, iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e84ec-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="e84ec-108">Eylemler tooget bir veri satırı kullanın, yeni bir satır ekleyin ve hatta silin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="e84ec-109">Örneğin, bir kayıt Dynamics CRM Online içinde (tetikleyici) oluşturulduğunda, bir satır bir Oracle veritabanına (bir eylem) ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="e84ec-110">Bu konu nasıl toouse hello Oracle Veritabanı Bağlayıcısı bir mantıksal uygulama içinde gösterir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e84ec-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e84ec-111">Prerequisites</span></span>

* <span data-ttu-id="e84ec-112">Desteklenen Oracle sürümleri:</span><span class="sxs-lookup"><span data-stu-id="e84ec-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="e84ec-113">Oracle 9 ve sonraki sürümler</span><span class="sxs-lookup"><span data-stu-id="e84ec-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="e84ec-114">Oracle istemci yazılımı 8.1.7 ve sonraki sürümler</span><span class="sxs-lookup"><span data-stu-id="e84ec-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="e84ec-115">Merhaba şirket içi veri ağ geçidi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="e84ec-116">[Tooon içi veri mantığı uygulamalardan bağlanmak](../logic-apps/logic-apps-gateway-connection.md) hello adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="e84ec-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="e84ec-117">Merhaba, gerekli tooconnect tooan şirket içi Oracle veritabanına veya Oracle DB yüklü olan bir Azure VM geçididir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="e84ec-118">Merhaba şirket içi veri ağ geçidi köprü olarak davranır ve şirket içi verileri (Merhaba bulutta olmayan) ve logic apps arasında güvenli veri aktarımını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e84ec-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="e84ec-119">Merhaba, aynı ağ geçidi birden çok hizmet ve birden çok veri kaynağı ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="e84ec-120">Bu nedenle, yalnızca tooinstall hello ağ geçidi kez gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="e84ec-121">Merhaba Oracle istemcisi hello şirket içi veri ağ geçidinin yüklü olduğu hello makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="e84ec-122">Tooinstall Oracle .NET için 64-bit Oracle veri sağlayıcısı hello emin olun:</span><span class="sxs-lookup"><span data-stu-id="e84ec-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="e84ec-123">Windows x64 için 64-bit ODAC 12c sürüm 4 (12.1.0.2.4)</span><span class="sxs-lookup"><span data-stu-id="e84ec-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="e84ec-124">Merhaba Oracle istemcisi yüklü değilse, toocreate deneyin veya hello bağlantı kullandığınızda bir hata oluşur.</span><span class="sxs-lookup"><span data-stu-id="e84ec-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="e84ec-125">Bu konuda Hello yaygın hatalar görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e84ec-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="e84ec-126">Merhaba bağlayıcısını ekleyin</span><span class="sxs-lookup"><span data-stu-id="e84ec-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e84ec-127">Bu bağlayıcı hiçbir tetikleyici yok.</span><span class="sxs-lookup"><span data-stu-id="e84ec-127">This connector does not have any triggers.</span></span> <span data-ttu-id="e84ec-128">Yalnızca eylem yok.</span><span class="sxs-lookup"><span data-stu-id="e84ec-128">It has only actions.</span></span> <span data-ttu-id="e84ec-129">Mantıksal uygulamanızı oluşturduğunuzda, bu nedenle başka bir tetikleyici toostart mantıksal uygulamanızı gibi ekleyin **çizelgesi - yinelenme**, veya **istek / yanıt - yanıt**.</span><span class="sxs-lookup"><span data-stu-id="e84ec-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="e84ec-130">Merhaba, [Azure portal](https://portal.azure.com), boş mantıksal uygulama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e84ec-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="e84ec-131">Mantıksal uygulamanızı Hello başlangıcında hello seçin **istek / yanıt - istek** tetikleyici:</span><span class="sxs-lookup"><span data-stu-id="e84ec-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="e84ec-132">**Kaydet**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-132">Select **Save**.</span></span> <span data-ttu-id="e84ec-133">Kaydettiğinizde, bir istek URL'sini otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e84ec-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="e84ec-134">Seçin **yeni adım**seçip **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e84ec-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="e84ec-135">Yazın `oracle` toosee hello kullanılabilir eylemler:</span><span class="sxs-lookup"><span data-stu-id="e84ec-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="e84ec-136">Bu aynı zamanda hello hızlı şekilde toosee olup hello tetikleyiciler ve Eylemler herhangi bir bağlayıcı için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="e84ec-137">Merhaba bağlayıcı adı, bir parçası yazın `oracle`.</span><span class="sxs-lookup"><span data-stu-id="e84ec-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="e84ec-138">Merhaba Tasarımcısı hiçbir tetikleyici ve eylemleri listeler.</span><span class="sxs-lookup"><span data-stu-id="e84ec-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="e84ec-139">Merhaba eylemlerden birini gibi seçin **Oracle veritabanı - Get satır**.</span><span class="sxs-lookup"><span data-stu-id="e84ec-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="e84ec-140">Seçin **Connect şirket içi veri ağ geçidi üzerinden**.</span><span class="sxs-lookup"><span data-stu-id="e84ec-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="e84ec-141">Merhaba Oracle sunucu adını, kimlik doğrulama yöntemi, kullanıcı adı, parola ve select hello ağ geçidi girin:</span><span class="sxs-lookup"><span data-stu-id="e84ec-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="e84ec-142">Bağlantı kurulduktan sonra hello listesinden bir tablo seçin ve hello satır kimliği tooyour tablo girin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="e84ec-143">Tooknow hello tanımlayıcı toohello tablo gerekir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="e84ec-144">Bilmiyorsanız, Oracle DB yöneticinize başvurun ve hello çıktısını almak `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="e84ec-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="e84ec-145">Tooproceed gereksinim olarak tanımlanabilir bilgileri hello kazandırır.</span><span class="sxs-lookup"><span data-stu-id="e84ec-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="e84ec-146">Aşağıdaki örnek hello, İnsan Kaynakları veritabanından iş veri döndürülmüyor:</span><span class="sxs-lookup"><span data-stu-id="e84ec-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="e84ec-147">Bu sonraki adımda hello herhangi diğer bağlayıcıları toobuild kullanabilirsiniz, iş akışı.</span><span class="sxs-lookup"><span data-stu-id="e84ec-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="e84ec-148">Oracle tootest alma verileri istediğiniz sonra hello Oracle veri hello birini kullanarak kendiniz bir e-posta Gönder, e-posta bağlayıcıları, böyle bir Office 365 veya Gmail gönderin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="e84ec-149">Merhaba dinamik hello Oracle tablo toobuild hello belirteçlerinden kullanmak `Subject` ve `Body` e-postanızın:</span><span class="sxs-lookup"><span data-stu-id="e84ec-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="e84ec-150">**Kaydet** mantıksal uygulama ve ardından **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="e84ec-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="e84ec-151">Merhaba Tasarımcısını Kapat ve hello durumu için hello çalıştırır geçmişini bakın.</span><span class="sxs-lookup"><span data-stu-id="e84ec-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="e84ec-152">Başarısız olursa hello başarısız ileti satırını seçin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="e84ec-153">Merhaba Tasarımcısı açılır ve hangi adım başarısız gösterir ve ayrıca gösterir hata bilgilerini hello.</span><span class="sxs-lookup"><span data-stu-id="e84ec-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="e84ec-154">Başarılı olursa, eklediğiniz hello bilgi içeren bir e-posta almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="e84ec-155">İş akışı fikirleri</span><span class="sxs-lookup"><span data-stu-id="e84ec-155">Workflow ideas</span></span>

* <span data-ttu-id="e84ec-156">Toomonitor hello #oracle diyez istediğiniz ve bunlar sorgulanan ve diğer uygulamalar içinde kullanılan şekilde hello tweet'leri bir veritabanında yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="e84ec-157">Bir mantıksal uygulama hello eklemek `Twitter - When a new tweet is posted` tetikleyebilir ve hello girin **#oracle** diyez.</span><span class="sxs-lookup"><span data-stu-id="e84ec-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="e84ec-158">Ardından, hello ekleyin `Oracle Database - Insert row` eylemi ve tablonuzu seçin:</span><span class="sxs-lookup"><span data-stu-id="e84ec-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="e84ec-159">İletileri tooa Service Bus kuyruğuna gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="e84ec-160">Bu iletiler tooget istediğiniz ve onları bir veritabanında yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e84ec-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="e84ec-161">Bir mantıksal uygulama hello eklemek `Service Bus - when a message is received in a queue` tetikleyici ve select hello sırası.</span><span class="sxs-lookup"><span data-stu-id="e84ec-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="e84ec-162">Ardından, hello ekleyin `Oracle Database - Insert row` eylemi ve tablonuzu seçin:</span><span class="sxs-lookup"><span data-stu-id="e84ec-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="e84ec-163">Sık karşılaşılan hataları</span><span class="sxs-lookup"><span data-stu-id="e84ec-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="e84ec-164">**Hata**: hello ağ geçidi ulaşamıyor</span><span class="sxs-lookup"><span data-stu-id="e84ec-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="e84ec-165">**Neden**: hello şirket içi veri ağ geçidi mümkün tooconnect toohello bulut değil.</span><span class="sxs-lookup"><span data-stu-id="e84ec-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="e84ec-166">**Azaltma**: ağ geçidiniz burada yükler ve onun toohello bağlanabilir hello şirket içi makinede çalıştığından emin olun Internet.</span><span class="sxs-lookup"><span data-stu-id="e84ec-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="e84ec-167">Merhaba ağ geçidi, bir bilgisayar kapalı olabilir veya uyku yüklenmiyor öneririz.</span><span class="sxs-lookup"><span data-stu-id="e84ec-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="e84ec-168">Merhaba şirket içi veri Ağ Geçidi Hizmeti (PBIEgwService) de yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e84ec-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="e84ec-169">**Hata**: kullanılmakta olan hello sağlayıcısının kullanım dışıdır: ' System.Data.OracleClient gerektirir Oracle istemci yazılımı 8.1.7 veya daha büyük.'.</span><span class="sxs-lookup"><span data-stu-id="e84ec-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="e84ec-170">Lütfen şu adresi ziyaret [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello resmi sağlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e84ec-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="e84ec-171">**Neden**: hello Oracle istemci SDK'sı yüklü değil hello makinede hello burada şirket içi veri ağ geçidi çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="e84ec-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="e84ec-172">**Çözümleme**: hello Oracle istemci SDK'sı üzerinde hello yükleyip hello şirket içi veri ağ geçidi ile aynı bilgisayara.</span><span class="sxs-lookup"><span data-stu-id="e84ec-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="e84ec-173">**Hata**: '[Tablename]' tablosu tüm anahtar sütunlarını tanımlamak değil</span><span class="sxs-lookup"><span data-stu-id="e84ec-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="e84ec-174">**Neden**: hello tablo hiçbir birincil anahtar yok.</span><span class="sxs-lookup"><span data-stu-id="e84ec-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="e84ec-175">**Çözümleme**: hello Oracle veritabanı connector, birincil anahtar sütunu içeren bir tablo kullanılmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e84ec-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="e84ec-176">Şu anda desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="e84ec-176">Currently not supported</span></span>

* <span data-ttu-id="e84ec-177">Görünümleri ve saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="e84ec-177">Views and stored procedures</span></span> 
* <span data-ttu-id="e84ec-178">Bileşik anahtarlar ile herhangi bir tabloyu</span><span class="sxs-lookup"><span data-stu-id="e84ec-178">Any table with composite keys</span></span>
* <span data-ttu-id="e84ec-179">İç içe nesne türlerinin tablolardaki</span><span class="sxs-lookup"><span data-stu-id="e84ec-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="e84ec-180">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e84ec-180">Connector-specific details</span></span>

<span data-ttu-id="e84ec-181">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="e84ec-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="e84ec-182">Bazı Yardım alın</span><span class="sxs-lookup"><span data-stu-id="e84ec-182">Get some help</span></span>

<span data-ttu-id="e84ec-183">Merhaba [Azure Logic Apps Forumu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) mükemmel tooask sorular yerleştirin, soruları ve diğer Logic Apps kullanıcıların ne yaptıklarını bakın.</span><span class="sxs-lookup"><span data-stu-id="e84ec-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="e84ec-184">Logic Apps ve bağlayıcıları oylama ve fikirlerinizi adresindeki gönderme tarafından artırmaya yardımcı olabilir [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="e84ec-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="e84ec-185">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e84ec-185">Next steps</span></span>
<span data-ttu-id="e84ec-186">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md)ve hello kullanılabilir bağlayıcılar Logic Apps içinde keşfetme bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e84ec-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
