---
title: "bir HTTP kaynağı - Azure aaaMove verilerden | Microsoft Docs"
description: "Azure Data Factory kullanarak şirket içi veya Bulut HTTP toomove verileri nasıl kaynak hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="b532f-103">Azure Data Factory kullanarak bir HTTP kaynağından veri taşıma</span><span class="sxs-lookup"><span data-stu-id="b532f-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="b532f-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove bir şirket içi/bulut HTTP uç noktası tooa verilerden havuz veri deposu desteklenen özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b532f-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="b532f-105">Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale listesiyle kopyalama etkinliği ve hello kaynakları/havuzlarını desteklenen veri depoları veri taşıma genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="b532f-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="b532f-106">Veri Fabrikası şu anda yalnızca bir HTTP veri taşınmasını destekler tooother veri depolarına kaynağı, ancak verileri diğer veriler taşıma değil tooan HTTP hedef depolar.</span><span class="sxs-lookup"><span data-stu-id="b532f-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="b532f-107">Desteklenen senaryolar ve kimlik doğrulama türleri</span><span class="sxs-lookup"><span data-stu-id="b532f-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="b532f-108">Bu HTTP Bağlayıcısı tooretrieve verilerden kullanabilirsiniz **Bulut ve şirket içi HTTP/s uç nokta** HTTP kullanarak **almak** veya **POST** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b532f-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="b532f-109">şu kimlik doğrulama türlerini hello desteklenir: **anonim**, **temel**, **Özet**, **Windows**, ve  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="b532f-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="b532f-110">Not hello birbirinden bu bağlayıcı ve hello [Web tablo Bağlayıcısı](data-factory-web-table-connector.md) olduğu: hello ikinci tablodur kullanılan tooextract web HTML sayfasından içerik.</span><span class="sxs-lookup"><span data-stu-id="b532f-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="b532f-111">Bir şirket içi HTTP uç noktasından veri kopyalama işlemi sırasında veri yönetimi ağ geçidi hello şirket içi ortamına/Azure VM yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b532f-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="b532f-112">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale toolearn veri yönetimi ağ geçidi ve hello ağ geçidi kurun ayarlama hakkında adım adım yönergeleri hakkında.</span><span class="sxs-lookup"><span data-stu-id="b532f-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b532f-113">Başlarken</span><span class="sxs-lookup"><span data-stu-id="b532f-113">Getting started</span></span>
<span data-ttu-id="b532f-114">Farklı araçlar/API'lerini kullanarak bir HTTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b532f-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="b532f-115">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="b532f-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b532f-116">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="b532f-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="b532f-117">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="b532f-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b532f-118">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="b532f-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="b532f-119">HTTP kaynağı tooAzure Blob Storage toocopy verileri JSON örnekleri için bkz: [JSON örnekler](#json-examples) Bu makaleler bölümü.</span><span class="sxs-lookup"><span data-stu-id="b532f-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b532f-120">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="b532f-120">Linked service properties</span></span>
<span data-ttu-id="b532f-121">Aşağıdaki tablonun hello JSON öğeleri belirli tooHTTP bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="b532f-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="b532f-122">Özellik</span><span class="sxs-lookup"><span data-stu-id="b532f-122">Property</span></span> | <span data-ttu-id="b532f-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b532f-123">Description</span></span> | <span data-ttu-id="b532f-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b532f-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b532f-125">type</span><span class="sxs-lookup"><span data-stu-id="b532f-125">type</span></span> | <span data-ttu-id="b532f-126">Merhaba type özelliği ayarlanmalıdır: `Http`.</span><span class="sxs-lookup"><span data-stu-id="b532f-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="b532f-127">Evet</span><span class="sxs-lookup"><span data-stu-id="b532f-127">Yes</span></span> |
| <span data-ttu-id="b532f-128">URL</span><span class="sxs-lookup"><span data-stu-id="b532f-128">url</span></span> | <span data-ttu-id="b532f-129">Temel URL toohello Web sunucusu</span><span class="sxs-lookup"><span data-stu-id="b532f-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="b532f-130">Evet</span><span class="sxs-lookup"><span data-stu-id="b532f-130">Yes</span></span> |
| <span data-ttu-id="b532f-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="b532f-131">authenticationType</span></span> | <span data-ttu-id="b532f-132">Merhaba kimlik doğrulama türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="b532f-132">Specifies hello authentication type.</span></span> <span data-ttu-id="b532f-133">İzin verilen değerler: **anonim**, **temel**, **Özet**, **Windows**, **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="b532f-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="b532f-134">Daha fazla özellikleri ve JSON örnekleri bu tablonun altındaki toosections bu kimlik doğrulama türleri için sırasıyla bakın.</span><span class="sxs-lookup"><span data-stu-id="b532f-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="b532f-135">Evet</span><span class="sxs-lookup"><span data-stu-id="b532f-135">Yes</span></span> |
| <span data-ttu-id="b532f-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="b532f-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="b532f-137">Kaynak HTTPS Web sunucusu ise tooenable sunucu SSL sertifikası doğrulaması olup olmadığını belirtin</span><span class="sxs-lookup"><span data-stu-id="b532f-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="b532f-138">Hayır, varsayılan değer true şeklindedir</span><span class="sxs-lookup"><span data-stu-id="b532f-138">No, default is true</span></span> |
| <span data-ttu-id="b532f-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b532f-139">gatewayName</span></span> | <span data-ttu-id="b532f-140">Merhaba veri yönetimi ağ geçidi tooconnect tooan adını HTTP kaynağı şirket içi.</span><span class="sxs-lookup"><span data-stu-id="b532f-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="b532f-141">Bir şirket içi HTTP kaynaktan veri kopyalama, Evet.</span><span class="sxs-lookup"><span data-stu-id="b532f-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="b532f-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="b532f-142">encryptedCredential</span></span> | <span data-ttu-id="b532f-143">Şifrelenmiş kimlik bilgileri tooaccess hello HTTP uç noktası.</span><span class="sxs-lookup"><span data-stu-id="b532f-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="b532f-144">Otomatik olarak oluşturulan Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda hello kimlik doğrulama bilgilerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b532f-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="b532f-145">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b532f-145">No.</span></span> <span data-ttu-id="b532f-146">Yalnızca bir şirket içi HTTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b532f-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="b532f-147">Bkz: [şirket içi kaynakları ve veri yönetimi ağ geçidi ile Merhaba bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) şirket içi HTTP Bağlayıcısı veri kaynağı için kimlik bilgilerini ayarlama hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b532f-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="b532f-148">Temel, Özet veya Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="b532f-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="b532f-149">Ayarlama `authenticationType` olarak `Basic`, `Digest`, veya `Windows`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="b532f-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="b532f-150">Özellik</span><span class="sxs-lookup"><span data-stu-id="b532f-150">Property</span></span> | <span data-ttu-id="b532f-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b532f-151">Description</span></span> | <span data-ttu-id="b532f-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b532f-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b532f-153">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="b532f-153">username</span></span> | <span data-ttu-id="b532f-154">Kullanıcı adı tooaccess hello HTTP uç noktası.</span><span class="sxs-lookup"><span data-stu-id="b532f-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="b532f-155">Evet</span><span class="sxs-lookup"><span data-stu-id="b532f-155">Yes</span></span> |
| <span data-ttu-id="b532f-156">password</span><span class="sxs-lookup"><span data-stu-id="b532f-156">password</span></span> | <span data-ttu-id="b532f-157">Merhaba kullanıcının (kullanıcı adı) parolası.</span><span class="sxs-lookup"><span data-stu-id="b532f-157">Password for hello user (username).</span></span> | <span data-ttu-id="b532f-158">Evet</span><span class="sxs-lookup"><span data-stu-id="b532f-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="b532f-159">Örnek: Temel, Özet veya Windows kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="b532f-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="b532f-160">ClientCertificate kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="b532f-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="b532f-161">toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `ClientCertificate`ve bunun yanında, HTTP Bağlayıcısı genel olanları sunulan yukarıda hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="b532f-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="b532f-162">Özellik</span><span class="sxs-lookup"><span data-stu-id="b532f-162">Property</span></span> | <span data-ttu-id="b532f-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b532f-163">Description</span></span> | <span data-ttu-id="b532f-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b532f-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b532f-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="b532f-165">embeddedCertData</span></span> | <span data-ttu-id="b532f-166">Merhaba Base64 ile kodlanmış içeriğini ikili veri hello kişisel bilgi değişimi (PFX) dosyası.</span><span class="sxs-lookup"><span data-stu-id="b532f-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="b532f-167">Her iki hello belirtin `embeddedCertData` veya `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="b532f-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="b532f-168">Certthumbprınt</span><span class="sxs-lookup"><span data-stu-id="b532f-168">certThumbprint</span></span> | <span data-ttu-id="b532f-169">ağ geçidi makinenizin sertifika deposunda yüklü hello sertifikanın parmak izini hello.</span><span class="sxs-lookup"><span data-stu-id="b532f-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="b532f-170">Yalnızca bir şirket içi HTTP kaynaktan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="b532f-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="b532f-171">Her iki hello belirtin `embeddedCertData` veya `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="b532f-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="b532f-172">password</span><span class="sxs-lookup"><span data-stu-id="b532f-172">password</span></span> | <span data-ttu-id="b532f-173">Merhaba sertifikayla ilişkili parola.</span><span class="sxs-lookup"><span data-stu-id="b532f-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="b532f-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="b532f-174">No</span></span> |

<span data-ttu-id="b532f-175">Kullanırsanız `certThumbprint` kimlik doğrulaması ve hello sertifika hello kişisel hello yerel bilgisayar deposunda yüklü için toogrant hello okuma izni toohello ağ geçidi hizmeti gerekir:</span><span class="sxs-lookup"><span data-stu-id="b532f-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="b532f-176">Microsoft Yönetim Konsolu (MMC) başlatın.</span><span class="sxs-lookup"><span data-stu-id="b532f-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="b532f-177">Merhaba eklemek **sertifikaları** bu hedefleri hello eklentisi **yerel bilgisayar**.</span><span class="sxs-lookup"><span data-stu-id="b532f-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="b532f-178">Genişletme **sertifikaları**, **kişisel**, tıklatıp **Sertifikalar**.</span><span class="sxs-lookup"><span data-stu-id="b532f-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="b532f-179">Merhaba kişisel deposundan Hello sertifikayı sağ tıklatın ve seçin **tüm görevler**->**özel anahtarları Yönet...**</span><span class="sxs-lookup"><span data-stu-id="b532f-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="b532f-180">Merhaba üzerinde **güvenlik** sekmesinde, altında veri yönetimi ağ geçidi ana bilgisayar hizmeti çalıştığı hello okuma erişimi toohello sertifikasıyla hello kullanıcı hesabını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b532f-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="b532f-181">Örnek: istemci sertifikası kullanarak</span><span class="sxs-lookup"><span data-stu-id="b532f-181">Example: using client certificate</span></span>
<span data-ttu-id="b532f-182">Bu hizmet bağlantılar, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı.</span><span class="sxs-lookup"><span data-stu-id="b532f-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="b532f-183">Veri Yönetimi yüklü ağ geçidi ile Merhaba makinede yüklü bir istemci sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="b532f-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="b532f-184">Örnek: istemci sertifikası bir dosyada kullanma</span><span class="sxs-lookup"><span data-stu-id="b532f-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="b532f-185">Bu hizmet bağlantılar, veri fabrikası tooan şirket içi HTTP web sunucunuzun bağlı.</span><span class="sxs-lookup"><span data-stu-id="b532f-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="b532f-186">Veri Yönetimi yüklü ağ geçidi ile bir istemci sertifika dosyası hello makinede kullanır.</span><span class="sxs-lookup"><span data-stu-id="b532f-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="b532f-187">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="b532f-187">Dataset properties</span></span>
<span data-ttu-id="b532f-188">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b532f-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b532f-189">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri türleri (Azure SQL, Azure blob, Azure tablo, vs.) için benzer.</span><span class="sxs-lookup"><span data-stu-id="b532f-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="b532f-190">Merhaba **typeProperties** bölüm veri kümesi her tür için farklıdır ve hello veri deposundaki hello veri hello konumu hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="b532f-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b532f-191">Merhaba typeProperties bölüm türü veri kümesi için **Http** hello aşağıdaki özelliklere sahip</span><span class="sxs-lookup"><span data-stu-id="b532f-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="b532f-192">Özellik</span><span class="sxs-lookup"><span data-stu-id="b532f-192">Property</span></span> | <span data-ttu-id="b532f-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b532f-193">Description</span></span> | <span data-ttu-id="b532f-194">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b532f-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="b532f-195">type</span><span class="sxs-lookup"><span data-stu-id="b532f-195">type</span></span> | <span data-ttu-id="b532f-196">Merhaba dataset Hello türü belirttiniz.</span><span class="sxs-lookup"><span data-stu-id="b532f-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="b532f-197">çok ayarlanmalıdır`Http`.</span><span class="sxs-lookup"><span data-stu-id="b532f-197">must be set too`Http`.</span></span> | <span data-ttu-id="b532f-198">Evet</span><span class="sxs-lookup"><span data-stu-id="b532f-198">Yes</span></span> |
| <span data-ttu-id="b532f-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="b532f-199">relativeUrl</span></span> | <span data-ttu-id="b532f-200">Merhaba verileri içeren bir göreli URL toohello kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="b532f-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="b532f-201">Yol belirtilmediğinde hello bağlantılı hizmet tanımında belirtilen yalnızca hello URL'si kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b532f-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="b532f-202">kullanabileceğiniz tooconstruct dinamik URL [Data Factory işlevler ve sistem değişkenleri](data-factory-functions-variables.md), örneğin "relativeUrl": "$$Text.Format ('/ my/rapor? ay = {0:yyyy}-{0:MM} & fmt csv =', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="b532f-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="b532f-203">Hayır</span><span class="sxs-lookup"><span data-stu-id="b532f-203">No</span></span> |
| <span data-ttu-id="b532f-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="b532f-204">requestMethod</span></span> | <span data-ttu-id="b532f-205">HTTP yöntemi.</span><span class="sxs-lookup"><span data-stu-id="b532f-205">Http method.</span></span> <span data-ttu-id="b532f-206">İzin verilen değerler **almak** veya **POST**.</span><span class="sxs-lookup"><span data-stu-id="b532f-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="b532f-207">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b532f-207">No.</span></span> <span data-ttu-id="b532f-208">Varsayılan değer `GET`.</span><span class="sxs-lookup"><span data-stu-id="b532f-208">Default is `GET`.</span></span> |
| <span data-ttu-id="b532f-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="b532f-209">additionalHeaders</span></span> | <span data-ttu-id="b532f-210">Ek HTTP isteği üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="b532f-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="b532f-211">Hayır</span><span class="sxs-lookup"><span data-stu-id="b532f-211">No</span></span> |
| <span data-ttu-id="b532f-212">RequestBody</span><span class="sxs-lookup"><span data-stu-id="b532f-212">requestBody</span></span> | <span data-ttu-id="b532f-213">HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="b532f-213">Body for HTTP request.</span></span> | <span data-ttu-id="b532f-214">Hayır</span><span class="sxs-lookup"><span data-stu-id="b532f-214">No</span></span> |
| <span data-ttu-id="b532f-215">Biçimi</span><span class="sxs-lookup"><span data-stu-id="b532f-215">format</span></span> | <span data-ttu-id="b532f-216">Toosimply istiyorsanız **HTTP uç noktası olarak hello veri almak-olduğu** ayrıştırma olmadan, bu biçim ayarlarını atla.</span><span class="sxs-lookup"><span data-stu-id="b532f-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="b532f-217">Kopyalama sırasında tooparse hello HTTP yanıt içerik isterseniz şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="b532f-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b532f-218">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="b532f-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="b532f-219">Hayır</span><span class="sxs-lookup"><span data-stu-id="b532f-219">No</span></span> |
| <span data-ttu-id="b532f-220">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="b532f-220">compression</span></span> | <span data-ttu-id="b532f-221">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b532f-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="b532f-222">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="b532f-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b532f-223">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="b532f-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b532f-224">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="b532f-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b532f-225">Hayır</span><span class="sxs-lookup"><span data-stu-id="b532f-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="b532f-226">Örnek: hello (varsayılan) GET yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="b532f-226">Example: using hello GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-hello-post-method"></a><span data-ttu-id="b532f-227">Örnek: Merhaba POST yöntemini kullanma</span><span class="sxs-lookup"><span data-stu-id="b532f-227">Example: using hello POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="b532f-228">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="b532f-228">Copy activity properties</span></span>
<span data-ttu-id="b532f-229">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="b532f-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b532f-230">Ad, açıklama, giriş ve çıkış tabloları ve ilke gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b532f-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="b532f-231">Hello kullanılabilen özellikleri **typeProperties** bölüm diğer yandan hello hello faaliyete, her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="b532f-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="b532f-232">Kopya etkinliği için bunlar hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="b532f-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="b532f-233">Şu anda kopyalama etkinliği hello kaynağında olduğunda türü **HttpSource**, aşağıdaki özelliklere hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="b532f-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="b532f-234">Özellik</span><span class="sxs-lookup"><span data-stu-id="b532f-234">Property</span></span> | <span data-ttu-id="b532f-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b532f-235">Description</span></span> | <span data-ttu-id="b532f-236">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b532f-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="b532f-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="b532f-237">httpRequestTimeout</span></span> | <span data-ttu-id="b532f-238">Merhaba HTTP isteği tooget yanıt için zaman aşımı (TimeSpan) hello.</span><span class="sxs-lookup"><span data-stu-id="b532f-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="b532f-239">Merhaba zaman aşımı tooget bir yanıt hello zaman aşımı tooread yanıt verileri değil olur.</span><span class="sxs-lookup"><span data-stu-id="b532f-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="b532f-240">Hayır.</span><span class="sxs-lookup"><span data-stu-id="b532f-240">No.</span></span> <span data-ttu-id="b532f-241">Varsayılan değer: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="b532f-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="b532f-242">Desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="b532f-242">Supported file and compression formats</span></span>
<span data-ttu-id="b532f-243">Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="b532f-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="b532f-244">JSON örnekleri</span><span class="sxs-lookup"><span data-stu-id="b532f-244">JSON examples</span></span>
<span data-ttu-id="b532f-245">Aşağıdaki örneğine hello sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b532f-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b532f-246">Bunların nasıl tooAzure Blob Storage HTTP toocopy veri kaynağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="b532f-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="b532f-247">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="b532f-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="b532f-248">Örnek: HTTP kaynağı tooAzure Blob depolama alanından veri Kopyala</span><span class="sxs-lookup"><span data-stu-id="b532f-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="b532f-249">Bu örnek için veri fabrikası çözümü Hello Data Factory varlıklarını aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="b532f-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="b532f-250">Bağlı hizmet türü [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b532f-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="b532f-251">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b532f-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="b532f-252">Bir giriş [dataset](data-factory-create-datasets.md) türü [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b532f-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="b532f-253">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b532f-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="b532f-254">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [HttpSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b532f-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b532f-255">Merhaba örnek verileri saatte bir HTTP kaynağı tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="b532f-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="b532f-256">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b532f-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="b532f-257">Bağlantılı HTTP hizmeti</span><span class="sxs-lookup"><span data-stu-id="b532f-257">HTTP linked service</span></span>
<span data-ttu-id="b532f-258">HTTP kullanan hello Bu örnek anonim kimlik doğrulaması ile bağlı.</span><span class="sxs-lookup"><span data-stu-id="b532f-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="b532f-259">Bkz: [HTTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b532f-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="b532f-260">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="b532f-260">Azure Storage linked service</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

### <a name="http-input-dataset"></a><span data-ttu-id="b532f-261">HTTP girdi veri kümesi</span><span class="sxs-lookup"><span data-stu-id="b532f-261">HTTP input dataset</span></span>
<span data-ttu-id="b532f-262">Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="b532f-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="b532f-263">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="b532f-263">Azure Blob output dataset</span></span>

<span data-ttu-id="b532f-264">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="b532f-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="b532f-265">Kopyalama etkinliği ile kanalı</span><span class="sxs-lookup"><span data-stu-id="b532f-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="b532f-266">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="b532f-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="b532f-267">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**HttpSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b532f-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="b532f-268">Bkz: [HttpSource](#copy-activity-properties) HttpSource hello tarafından desteklenen özellikler hello listesi.</span><span class="sxs-lookup"><span data-stu-id="b532f-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source tooan Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```

> [!NOTE]
> <span data-ttu-id="b532f-269">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b532f-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b532f-270">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="b532f-270">Performance and Tuning</span></span>
<span data-ttu-id="b532f-271">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="b532f-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
