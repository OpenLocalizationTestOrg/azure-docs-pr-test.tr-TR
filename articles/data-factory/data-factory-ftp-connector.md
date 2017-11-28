---
title: Azure Data Factory kullanarak bir FTP sunucusu aaaMove verilerden | Microsoft Docs
description: "Hakkında bilgi edinin Azure Data Factory kullanarak bir FTP sunucusunu toomove verileri."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="50835-103">Azure Data Factory kullanarak bir FTP sunucusundan veri taşıma</span><span class="sxs-lookup"><span data-stu-id="50835-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="50835-104">Bu makalede nasıl toouse hello kopyalama etkinliği Azure Data Factory toomove verileri bir FTP sunucusundan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="50835-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="50835-105">Üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makalenin hello kopyalama etkinliği ile veri taşıma için genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="50835-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="50835-106">Bir FTP sunucusu desteklenen tooany havuz veri deposundan verileri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50835-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="50835-107">Verileri bir listesi için desteklenen depoları hello kopyalama etkinliği tarafından havuzlarını hello görür [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="50835-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="50835-108">Veri Fabrikası şu anda yalnızca bir FTP sunucusu tooother verilerden veri taşımayı depolar, ancak verileri diğer veriler taşıma değil tooan FTP sunucusu depolar destekler.</span><span class="sxs-lookup"><span data-stu-id="50835-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="50835-109">Her iki şirket içi destekler ve FTP sunucuları bulut.</span><span class="sxs-lookup"><span data-stu-id="50835-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="50835-110">başarıyla kopyalanan toohello hedef sonra hello kopyalama etkinliği hello kaynak dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="50835-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="50835-111">Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="50835-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="50835-112">Bağlantıyı etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="50835-112">Enable connectivity</span></span>
<span data-ttu-id="50835-113">Veri geçiş yapıyorsanız, bir **şirket içi** FTP sunucusu tooa bulut veri deposu (örneğin, tooAzure Blob Depolama), yükleme ve veri yönetimi ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="50835-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="50835-114">Merhaba veri yönetimi ağ geçidi, şirket içi makinenizde yüklü bir istemci aracısıdır ve bulut Hizmetleri tooconnect tooan şirket içi kaynak sağlar.</span><span class="sxs-lookup"><span data-stu-id="50835-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="50835-115">Ayrıntılar için bkz [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="50835-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="50835-116">Merhaba ağ geçidi kurun ayarlama ve kullanılarak adım adım yönergeler için bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="50835-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="50835-117">Merhaba sunucu üzerinde bir Azure altyapı (ıaas) sanal makine (VM) olarak olsa bile, hello ağ geçidi tooconnect tooan FTP sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="50835-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="50835-118">Olası tooinstall hello ağ geçidi olduğu hello üzerinde aynı makine ya da Iaas VM FTP sunucusu hello gibi şirket içi.</span><span class="sxs-lookup"><span data-stu-id="50835-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="50835-119">Ancak, ayrı makinede veya Iaas VM tooavoid kaynak çekişmesini ve daha iyi performans için hello ağ geçidi yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="50835-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="50835-120">Merhaba ağ geçidi ayrı bir makineye yüklediğinizde hello makine mümkün tooaccess hello FTP sunucusu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="50835-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="50835-121">başlarken</span><span class="sxs-lookup"><span data-stu-id="50835-121">Get started</span></span>
<span data-ttu-id="50835-122">Farklı araçlar veya API'lerini kullanarak bir FTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="50835-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="50835-123">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Data Factory Kopyalama Sihirbazı**.</span><span class="sxs-lookup"><span data-stu-id="50835-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="50835-124">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hızlı kılavuz.</span><span class="sxs-lookup"><span data-stu-id="50835-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="50835-125">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="50835-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="50835-126">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="50835-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="50835-127">Merhaba araçları veya API'lerle de kullansanız adımları toocreate veri kaynağına veri dosyaları tooa havuz veri deposunu taşır ardışık aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="50835-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="50835-128">Oluşturma **bağlantılı Hizmetleri** toolink girdi ve çıktı veri depoları tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="50835-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="50835-129">Oluşturma **veri kümeleri** giriş ve çıkış toorepresent hello için veri kopyalama işlemi.</span><span class="sxs-lookup"><span data-stu-id="50835-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="50835-130">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="50835-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="50835-131">Başlangıç Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve hello ardışık düzeni) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="50835-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="50835-132">Araçları veya API'ler (dışında .NET API'si) kullandığınızda, bu Data Factory varlıklarını hello JSON biçimini kullanarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="50835-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="50835-133">Merhaba bir FTP veri deposundaki kullanılan toocopy verileri Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz [JSON örnek: FTP sunucusu tooAzure blobundan veri kopyalama](#json-example-copy-data-from-ftp-server-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="50835-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="50835-134">Desteklenen dosya ve sıkıştırma biçimleri toouse hakkında daha fazla ayrıntı için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="50835-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="50835-135">Aşağıdaki bölümlerde hello kullanılan toodefine Data Factory varlıkları belirli tooFTP olan JSON özellikleri hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="50835-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="50835-136">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="50835-136">Linked service properties</span></span>
<span data-ttu-id="50835-137">Aşağıdaki tablonun hello JSON öğeleri belirli tooan bağlı FTP hizmeti açıklar.</span><span class="sxs-lookup"><span data-stu-id="50835-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="50835-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="50835-138">Property</span></span> | <span data-ttu-id="50835-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50835-139">Description</span></span> | <span data-ttu-id="50835-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="50835-140">Required</span></span> | <span data-ttu-id="50835-141">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="50835-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50835-142">type</span><span class="sxs-lookup"><span data-stu-id="50835-142">type</span></span> |<span data-ttu-id="50835-143">Bu tooFtpServer ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="50835-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="50835-144">Evet</span><span class="sxs-lookup"><span data-stu-id="50835-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="50835-145">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="50835-145">host</span></span> |<span data-ttu-id="50835-146">Merhaba adını veya hello FTP sunucusunun IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="50835-147">Evet</span><span class="sxs-lookup"><span data-stu-id="50835-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="50835-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="50835-148">authenticationType</span></span> |<span data-ttu-id="50835-149">Merhaba kimlik doğrulama türü belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-149">Specify hello authentication type.</span></span> |<span data-ttu-id="50835-150">Evet</span><span class="sxs-lookup"><span data-stu-id="50835-150">Yes</span></span> |<span data-ttu-id="50835-151">Temel, anonim</span><span class="sxs-lookup"><span data-stu-id="50835-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="50835-152">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="50835-152">username</span></span> |<span data-ttu-id="50835-153">Erişim toohello FTP sunucusu olan hello kullanıcı belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="50835-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-154">No</span></span> |&nbsp; |
| <span data-ttu-id="50835-155">password</span><span class="sxs-lookup"><span data-stu-id="50835-155">password</span></span> |<span data-ttu-id="50835-156">Merhaba kullanıcının (kullanıcı adı) Hello parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="50835-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-157">No</span></span> |&nbsp; |
| <span data-ttu-id="50835-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="50835-158">encryptedCredential</span></span> |<span data-ttu-id="50835-159">Şifrelenmiş hello kimlik bilgisi tooaccess hello FTP sunucusunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="50835-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-160">No</span></span> |&nbsp; |
| <span data-ttu-id="50835-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="50835-161">gatewayName</span></span> |<span data-ttu-id="50835-162">Veri Yönetimi ağ geçidi tooconnect tooan şirket içi FTP sunucusunda hello ağ geçidinin Hello adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="50835-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-163">No</span></span> |&nbsp; |
| <span data-ttu-id="50835-164">port</span><span class="sxs-lookup"><span data-stu-id="50835-164">port</span></span> |<span data-ttu-id="50835-165">Hangi hello FTP sunucusunun dinleme hello bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="50835-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-166">No</span></span> |<span data-ttu-id="50835-167">21</span><span class="sxs-lookup"><span data-stu-id="50835-167">21</span></span> |
| <span data-ttu-id="50835-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="50835-168">enableSsl</span></span> |<span data-ttu-id="50835-169">Toouse SSL/TLS kanalı üzerinden FTP olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="50835-170">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-170">No</span></span> |<span data-ttu-id="50835-171">TRUE</span><span class="sxs-lookup"><span data-stu-id="50835-171">true</span></span> |
| <span data-ttu-id="50835-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="50835-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="50835-173">FTP SSL/TLS kanalı üzerinden kullanırken tooenable sunucu SSL sertifikası doğrulaması olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="50835-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-174">No</span></span> |<span data-ttu-id="50835-175">TRUE</span><span class="sxs-lookup"><span data-stu-id="50835-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="50835-176">Anonim kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="50835-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="50835-177">Kullanıcı adı ve parola düz metin olarak temel kimlik doğrulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="50835-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="50835-178">Bağlantı noktası, enableSsl, enableServerCertificateValidation kullanın</span><span class="sxs-lookup"><span data-stu-id="50835-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="50835-179">Kimlik doğrulama ve ağ geçidi için encryptedCredential kullanın</span><span class="sxs-lookup"><span data-stu-id="50835-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="50835-180">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="50835-180">Dataset properties</span></span>
<span data-ttu-id="50835-181">Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="50835-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="50835-182">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="50835-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="50835-183">Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="50835-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="50835-184">Belirli toohello veri kümesi türü olan bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="50835-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="50835-185">Merhaba **typeProperties** bir veri kümesi için bir bölüm türü **FileShare** hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="50835-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="50835-186">Özellik</span><span class="sxs-lookup"><span data-stu-id="50835-186">Property</span></span> | <span data-ttu-id="50835-187">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50835-187">Description</span></span> | <span data-ttu-id="50835-188">Gerekli</span><span class="sxs-lookup"><span data-stu-id="50835-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="50835-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="50835-189">folderPath</span></span> |<span data-ttu-id="50835-190">Alt toohello klasör.</span><span class="sxs-lookup"><span data-stu-id="50835-190">Subpath toohello folder.</span></span> <span data-ttu-id="50835-191">Kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="50835-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="50835-192">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="50835-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="50835-193">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç ve bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="50835-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="50835-194">Evet</span><span class="sxs-lookup"><span data-stu-id="50835-194">Yes</span></span> |
| <span data-ttu-id="50835-195">fileName</span><span class="sxs-lookup"><span data-stu-id="50835-195">fileName</span></span> |<span data-ttu-id="50835-196">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="50835-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="50835-197">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="50835-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="50835-198">Zaman **fileName** belirtilmemiş bir çıkış veri kümesi için oluşturulan hello dosyasının hello adı biçimini izleyen hello:</span><span class="sxs-lookup"><span data-stu-id="50835-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="50835-199">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="50835-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="50835-200">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-200">No</span></span> |
| <span data-ttu-id="50835-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="50835-201">fileFilter</span></span> |<span data-ttu-id="50835-202">Bir filtre kullanılan toobe tooselect dosya alt kümesine hello belirtin **folderPath**, tüm dosyalar yerine.</span><span class="sxs-lookup"><span data-stu-id="50835-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="50835-203">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="50835-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="50835-204">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="50835-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="50835-205">Örnek 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="50835-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="50835-206">**fileFilter** bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="50835-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="50835-207">Bu özellik, Hadoop dağıtılmış dosya sistemi (HDFS ile) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="50835-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="50835-208">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-208">No</span></span> |
| <span data-ttu-id="50835-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="50835-209">partitionedBy</span></span> |<span data-ttu-id="50835-210">Toospecify dinamik kullanılan **folderPath** ve **fileName** zaman serisi veriler için.</span><span class="sxs-lookup"><span data-stu-id="50835-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="50835-211">Örneğin, belirleyebileceğiniz bir **folderPath** için verileri saatte parametreli.</span><span class="sxs-lookup"><span data-stu-id="50835-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="50835-212">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-212">No</span></span> |
| <span data-ttu-id="50835-213">Biçimi</span><span class="sxs-lookup"><span data-stu-id="50835-213">format</span></span> | <span data-ttu-id="50835-214">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="50835-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="50835-215">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="50835-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="50835-216">Merhaba daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi ](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="50835-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="50835-217">Depoları arasında (ikili kopya), dosya tabanlı oldukları gibi toocopy dosyaları istiyorsanız, her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="50835-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="50835-218">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-218">No</span></span> |
| <span data-ttu-id="50835-219">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="50835-219">compression</span></span> | <span data-ttu-id="50835-220">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="50835-221">Desteklenen türler **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**, ve desteklenen düzeyler **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="50835-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="50835-222">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="50835-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="50835-223">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-223">No</span></span> |
| <span data-ttu-id="50835-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="50835-224">useBinaryTransfer</span></span> |<span data-ttu-id="50835-225">Toouse hello ikili aktarım modu olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="50835-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="50835-226">Merhaba değerleri (Bu, hello varsayılan değer) ikili mod için true ve false ASCII için.</span><span class="sxs-lookup"><span data-stu-id="50835-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="50835-227">Merhaba ilişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="50835-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="50835-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="50835-229">**Dosya adı** ve **fileFilter** eşzamanlı olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="50835-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="50835-230">Merhaba partionedBy özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="50835-230">Use hello partionedBy property</span></span>
<span data-ttu-id="50835-231">Merhaba önceki bölümünde belirtildiği gibi bir dinamik belirtebilirsiniz **folderPath** ve **fileName** zaman serisi veri hello ile **partitionedBy** özelliği.</span><span class="sxs-lookup"><span data-stu-id="50835-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="50835-232">Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında toolearn bkz [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="50835-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="50835-233">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="50835-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="50835-234">Bu örnekte, {dilim} hello Data Factory sistem değişkeni SliceStart değeriyle değiştirilir, belirtilen (YYYYMMDDHH) hello biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="50835-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="50835-235">Merhaba SliceStart hello dilim toostart süresini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="50835-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="50835-236">Merhaba klasör yolu, her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="50835-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="50835-237">(Örneğin, wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="50835-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="50835-238">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="50835-238">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="50835-239">Bu örnekte, hello tarafından kullanılan ayrı değişkenleri içine ayıklanır hello yıl, ay, gün ve saat SliceStart **folderPath** ve **fileName** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="50835-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="50835-240">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="50835-240">Copy activity properties</span></span>
<span data-ttu-id="50835-241">Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="50835-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="50835-242">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="50835-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="50835-243">Hello kullanılabilen özellikleri **typeProperties** bölümünü diğer yandan faaliyete hello Merhaba, her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="50835-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="50835-244">Merhaba kopya etkinliği için hello türü özellikleri hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="50835-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="50835-245">Kopyalama etkinliğinde hello kaynak türü olduğunda **FileSystemSource**, özellik aşağıdaki hello sağlanmıştır **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="50835-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="50835-246">Özellik</span><span class="sxs-lookup"><span data-stu-id="50835-246">Property</span></span> | <span data-ttu-id="50835-247">Açıklama</span><span class="sxs-lookup"><span data-stu-id="50835-247">Description</span></span> | <span data-ttu-id="50835-248">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="50835-248">Allowed values</span></span> | <span data-ttu-id="50835-249">Gerekli</span><span class="sxs-lookup"><span data-stu-id="50835-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="50835-250">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="50835-250">recursive</span></span> |<span data-ttu-id="50835-251">Merhaba klasörlerdeki ya da yalnızca klasöründen hello belirtilen Hello veri yinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="50835-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="50835-252">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="50835-252">True, False (default)</span></span> |<span data-ttu-id="50835-253">Hayır</span><span class="sxs-lookup"><span data-stu-id="50835-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="50835-254">JSON örnek: FTP sunucusu tooAzure Blob veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="50835-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="50835-255">Bu örnek göstermektedir nasıl bir FTP sunucusu tooAzure Blob Depolama toocopy verileri.</span><span class="sxs-lookup"><span data-stu-id="50835-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="50835-256">İçinde belirtilen hello hello tooany havuzlarını doğrudan veri ancak kopyalanabilir [desteklenen veri depoları ve biçimleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats), veri fabrikasında hello kopyalama etkinliği kullanarak.</span><span class="sxs-lookup"><span data-stu-id="50835-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="50835-257">Merhaba aşağıdaki örneklerde sağlayan örnek JSON tanımları toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="50835-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="50835-258">Bağlı hizmet türü [Ftp_sunucusu](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="50835-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="50835-259">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="50835-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="50835-260">Bir giriş [dataset](data-factory-create-datasets.md) türü [dosya paylaşımı](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="50835-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="50835-261">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="50835-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="50835-262">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="50835-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="50835-263">Merhaba örnek verileri saatte bir FTP sunucusu tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="50835-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="50835-264">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="50835-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="50835-265">Bağlı FTP hizmeti</span><span class="sxs-lookup"><span data-stu-id="50835-265">FTP linked service</span></span>

<span data-ttu-id="50835-266">Bu örnek, hello kullanıcı adı ve parola düz metin ile temel kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="50835-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="50835-267">Aşağıdaki şekilde hello birini de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="50835-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="50835-268">Anonim kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="50835-268">Anonymous authentication</span></span>
* <span data-ttu-id="50835-269">Şifrelenmiş kimlik bilgileri ile temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="50835-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="50835-270">SSL/TLS (FTPS) üzerinden FTP</span><span class="sxs-lookup"><span data-stu-id="50835-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="50835-271">Merhaba bkz [FTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50835-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="50835-272">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="50835-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="50835-273">FTP giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="50835-273">FTP input dataset</span></span>

<span data-ttu-id="50835-274">Bu veri kümesi toohello FTP klasörü işaret ediyor `mysharedfolder` ve dosya `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="50835-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="50835-275">Merhaba ardışık düzen hello dosya toohello hedef kopyalar.</span><span class="sxs-lookup"><span data-stu-id="50835-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="50835-276">Ayarı **dış** çok**true** hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="50835-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="50835-277">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="50835-277">Azure Blob output dataset</span></span>

<span data-ttu-id="50835-278">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="50835-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="50835-279">Merhaba klasör yolu hello blob için dinamik olarak değerlendirilen işleniyor hello dilimin hello başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="50835-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="50835-280">Merhaba klasör yolu hello yıl, ay, gün ve saat bölümlerini hello başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="50835-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="50835-281">Dosya sistemi kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="50835-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="50835-282">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="50835-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="50835-283">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource**ve hello **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="50835-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="50835-284">Kaynak veri kümesi toocolumns havuz kümesinden toomap sütunlarından bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="50835-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="50835-285">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="50835-285">Next steps</span></span>
<span data-ttu-id="50835-286">Aşağıdaki makaleleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="50835-286">See hello following articles:</span></span>

* <span data-ttu-id="50835-287">anahtarı hakkında toolearn Etkenler etkisi performans veri fabrikasında (kopyalama etkinliği) veri hareketlerini ve çeşitli yolları toooptimize, hello bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="50835-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="50835-288">Kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için bkz: Merhaba [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="50835-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
