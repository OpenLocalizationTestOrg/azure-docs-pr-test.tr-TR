---
title: "Azure Data Factory kullanarak bir FTP sunucusundan veri taşıma | Microsoft Docs"
description: "Azure Data Factory kullanarak bir FTP sunucusundan veri taşıma hakkında bilgi edinin."
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="253f6-103">Azure Data Factory kullanarak bir FTP sunucusundan veri taşıma</span><span class="sxs-lookup"><span data-stu-id="253f6-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="253f6-104">Bu makalede kopya etkinliği Azure Data Factory'de bir FTP sunucusundan veri taşımak için nasıl kullanılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="253f6-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="253f6-105">Derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) kopyalama etkinliği ile veri taşıma için genel bir bakış sunar makalesi.</span><span class="sxs-lookup"><span data-stu-id="253f6-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="253f6-106">Bir FTP sunucusundan veri tüm desteklenen havuz veri deposuna kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="253f6-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="253f6-107">Veri depoları havuzlarını kopyalama etkinliği tarafından desteklenen bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tablo.</span><span class="sxs-lookup"><span data-stu-id="253f6-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="253f6-108">Veri Fabrikası şu anda yalnızca taşıma verilerden bir FTP sunucusu diğer veri depolarına destekler, ancak FTP sunucusuna verileri diğer veriler taşıma değil depolar.</span><span class="sxs-lookup"><span data-stu-id="253f6-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="253f6-109">Her iki şirket içi destekler ve FTP sunucuları bulut.</span><span class="sxs-lookup"><span data-stu-id="253f6-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="253f6-110">Hedefe başarıyla kopyalandıktan sonra kopyalama etkinliği kaynak dosyasını silmez.</span><span class="sxs-lookup"><span data-stu-id="253f6-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="253f6-111">Sonra başarılı bir kopyasını kaynak dosyasını silmeniz gerekirse, dosyayı silmek için özel bir etkinlik oluşturmak ve ardışık düzeninde etkinlik kullanın.</span><span class="sxs-lookup"><span data-stu-id="253f6-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="253f6-112">Bağlantıyı etkinleştirmek</span><span class="sxs-lookup"><span data-stu-id="253f6-112">Enable connectivity</span></span>
<span data-ttu-id="253f6-113">Verileri taşıyorsanız, bir **şirket içi** FTP sunucusuna Bulutu veri depolamak (örneğin,. Azure Blob depolama alanına) yükleyin ve veri yönetimi ağ geçidi kullanın.</span><span class="sxs-lookup"><span data-stu-id="253f6-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="253f6-114">Veri Yönetimi ağ geçidi, şirket içi makinenizde yüklü bir istemci aracısıdır ve bir şirket içi kaynağa bağlanmak bulut hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="253f6-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="253f6-115">Ayrıntılar için bkz [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="253f6-116">Adım adım yönergeler ayarı yukarı ağ geçidi ve, bkz [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="253f6-117">Sunucu üzerinde bir Azure altyapı (ıaas) sanal makine (VM) olarak olsa bile, bir FTP sunucusuna bağlanmak için ağ geçidi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="253f6-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="253f6-118">Aynı şirket içi makinede veya FTP sunucusu olarak Iaas VM ağ geçidi yüklemek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="253f6-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="253f6-119">Ancak, ayrı makinede veya Iaas kaynak çekişmesini önlemek için VM ve daha iyi performans için ağ geçidi yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="253f6-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="253f6-120">Ağ geçidi ayrı bir makineye yüklediğinizde, makine FTP sunucusunun erişebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="253f6-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="253f6-121">başlarken</span><span class="sxs-lookup"><span data-stu-id="253f6-121">Get started</span></span>
<span data-ttu-id="253f6-122">Farklı araçlar veya API'lerini kullanarak bir FTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="253f6-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="253f6-123">Bir işlem hattı oluşturmak için en kolay yolu kullanmaktır **Data Factory Kopyalama Sihirbazı**.</span><span class="sxs-lookup"><span data-stu-id="253f6-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="253f6-124">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hızlı kılavuz.</span><span class="sxs-lookup"><span data-stu-id="253f6-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="253f6-125">Bir işlem hattı oluşturmak için aşağıdaki araçları kullanabilirsiniz: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager şablonu**, **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="253f6-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="253f6-126">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="253f6-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="253f6-127">Araçlar ya da API'leri kullanıp bir havuz veri deposu için bir kaynak veri deposundan verileri taşır bir ardışık düzen oluşturmak için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="253f6-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="253f6-128">Oluşturma **bağlantılı Hizmetleri** girdi ve çıktı verilerini bağlamak için veri fabrikanıza depolar.</span><span class="sxs-lookup"><span data-stu-id="253f6-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="253f6-129">Oluşturma **veri kümeleri** kopyalama işlemi için girdi ve çıktı verilerini temsil etmek için.</span><span class="sxs-lookup"><span data-stu-id="253f6-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="253f6-130">Oluşturma bir **ardışık düzen** bir giriş olarak bir veri kümesi ve bir veri kümesini çıktı olarak alan kopyalama etkinliği ile.</span><span class="sxs-lookup"><span data-stu-id="253f6-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="253f6-131">Sihirbazı'nı kullandığınızda, bu Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) için JSON tanımları sizin için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="253f6-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="253f6-132">Araçları veya API'ler (dışında .NET API'si) kullandığınızda, JSON biçimini kullanarak bu Data Factory varlıklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="253f6-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="253f6-133">Bir FTP veri deposundan verileri kopyalamak için kullanılan Data Factory varlıkları için JSON tanımları içeren bir örnek için bkz: [JSON örnek: veri kopyalama FTP sunucusundan Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="253f6-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="253f6-134">Kullanmak için desteklenen dosya ve sıkıştırma biçimleri hakkında daha fazla ayrıntı için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="253f6-135">Aşağıdaki bölümler, Data Factory varlıklarını belirli FTP tanımlamak için kullanılan JSON özellikleri hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="253f6-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="253f6-136">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="253f6-136">Linked service properties</span></span>
<span data-ttu-id="253f6-137">Aşağıdaki tabloda bir FTP bağlantılı hizmete özgü JSON öğelerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="253f6-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="253f6-138">Özellik</span><span class="sxs-lookup"><span data-stu-id="253f6-138">Property</span></span> | <span data-ttu-id="253f6-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="253f6-139">Description</span></span> | <span data-ttu-id="253f6-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="253f6-140">Required</span></span> | <span data-ttu-id="253f6-141">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="253f6-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="253f6-142">type</span><span class="sxs-lookup"><span data-stu-id="253f6-142">type</span></span> |<span data-ttu-id="253f6-143">Bu Ftp_sunucusu için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="253f6-143">Set this to FtpServer.</span></span> |<span data-ttu-id="253f6-144">Evet</span><span class="sxs-lookup"><span data-stu-id="253f6-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="253f6-145">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="253f6-145">host</span></span> |<span data-ttu-id="253f6-146">Adını veya FTP sunucusunun IP adresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="253f6-147">Evet</span><span class="sxs-lookup"><span data-stu-id="253f6-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="253f6-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="253f6-148">authenticationType</span></span> |<span data-ttu-id="253f6-149">Kimlik doğrulama türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-149">Specify the authentication type.</span></span> |<span data-ttu-id="253f6-150">Evet</span><span class="sxs-lookup"><span data-stu-id="253f6-150">Yes</span></span> |<span data-ttu-id="253f6-151">Temel, anonim</span><span class="sxs-lookup"><span data-stu-id="253f6-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="253f6-152">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="253f6-152">username</span></span> |<span data-ttu-id="253f6-153">FTP sunucusuna erişimi olan kullanıcı belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="253f6-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-154">No</span></span> |&nbsp; |
| <span data-ttu-id="253f6-155">password</span><span class="sxs-lookup"><span data-stu-id="253f6-155">password</span></span> |<span data-ttu-id="253f6-156">(Kullanıcı adı) kullanıcının parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="253f6-157">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-157">No</span></span> |&nbsp; |
| <span data-ttu-id="253f6-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="253f6-158">encryptedCredential</span></span> |<span data-ttu-id="253f6-159">FTP sunucusuna erişmek için şifreli kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="253f6-160">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-160">No</span></span> |&nbsp; |
| <span data-ttu-id="253f6-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="253f6-161">gatewayName</span></span> |<span data-ttu-id="253f6-162">Veri Yönetimi ağ geçidi şirket içi FTP sunucusuna bağlanmak için ağ geçidi adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="253f6-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-163">No</span></span> |&nbsp; |
| <span data-ttu-id="253f6-164">port</span><span class="sxs-lookup"><span data-stu-id="253f6-164">port</span></span> |<span data-ttu-id="253f6-165">FTP sunucusunun dinlediği bağlantı noktasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="253f6-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-166">No</span></span> |<span data-ttu-id="253f6-167">21</span><span class="sxs-lookup"><span data-stu-id="253f6-167">21</span></span> |
| <span data-ttu-id="253f6-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="253f6-168">enableSsl</span></span> |<span data-ttu-id="253f6-169">FTP SSL/TLS kanalı üzerinden kullanılıp kullanılmayacağını belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="253f6-170">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-170">No</span></span> |<span data-ttu-id="253f6-171">TRUE</span><span class="sxs-lookup"><span data-stu-id="253f6-171">true</span></span> |
| <span data-ttu-id="253f6-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="253f6-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="253f6-173">FTP SSL/TLS kanalı üzerinden kullanırken sunucu SSL sertifika doğrulamasını etkinleştirmek bu seçeneği belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="253f6-174">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-174">No</span></span> |<span data-ttu-id="253f6-175">TRUE</span><span class="sxs-lookup"><span data-stu-id="253f6-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="253f6-176">Anonim kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="253f6-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="253f6-177">Kullanıcı adı ve parola düz metin olarak temel kimlik doğrulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="253f6-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="253f6-178">Bağlantı noktası, enableSsl, enableServerCertificateValidation kullanın</span><span class="sxs-lookup"><span data-stu-id="253f6-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="253f6-179">Kimlik doğrulama ve ağ geçidi için encryptedCredential kullanın</span><span class="sxs-lookup"><span data-stu-id="253f6-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="253f6-180">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="253f6-180">Dataset properties</span></span>
<span data-ttu-id="253f6-181">Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [veri kümeleri oluşturma](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="253f6-182">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="253f6-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="253f6-183">**TypeProperties** bölümü, her veri kümesi türü için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="253f6-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="253f6-184">Veri kümesi türüne özgü bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="253f6-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="253f6-185">**TypeProperties** bir veri kümesi için bir bölüm türü **FileShare** aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="253f6-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="253f6-186">Özellik</span><span class="sxs-lookup"><span data-stu-id="253f6-186">Property</span></span> | <span data-ttu-id="253f6-187">Açıklama</span><span class="sxs-lookup"><span data-stu-id="253f6-187">Description</span></span> | <span data-ttu-id="253f6-188">Gerekli</span><span class="sxs-lookup"><span data-stu-id="253f6-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="253f6-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="253f6-189">folderPath</span></span> |<span data-ttu-id="253f6-190">Alt klasöre.</span><span class="sxs-lookup"><span data-stu-id="253f6-190">Subpath to the folder.</span></span> <span data-ttu-id="253f6-191">Kaçış karakteri kullanmak ' \ ' dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="253f6-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="253f6-192">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="253f6-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="253f6-193">Bu özellik ile birleştirebilirsiniz **partitionBy** dilim başlangıç bağlı klasör yoluna sahip ve bitiş tarihi saatlerini.</span><span class="sxs-lookup"><span data-stu-id="253f6-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="253f6-194">Evet</span><span class="sxs-lookup"><span data-stu-id="253f6-194">Yes</span></span> |
| <span data-ttu-id="253f6-195">fileName</span><span class="sxs-lookup"><span data-stu-id="253f6-195">fileName</span></span> |<span data-ttu-id="253f6-196">Dosya adını belirtin **folderPath** klasöründeki belirli bir dosya belirtmek için tablo istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="253f6-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="253f6-197">Bu özellik için herhangi bir değer belirtmezseniz, tablonun klasördeki tüm dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="253f6-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="253f6-198">Zaman **fileName** belirtilmemiş bir çıkış veri kümesi için oluşturulan dosya adı şu biçimde:</span><span class="sxs-lookup"><span data-stu-id="253f6-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="253f6-199">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="253f6-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="253f6-200">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-200">No</span></span> |
| <span data-ttu-id="253f6-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="253f6-201">fileFilter</span></span> |<span data-ttu-id="253f6-202">Bir alt kümesini dosyalarında seçmek için kullanılacak bir filtre belirtin **folderPath**, tüm dosyalar yerine.</span><span class="sxs-lookup"><span data-stu-id="253f6-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="253f6-203">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="253f6-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="253f6-204">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="253f6-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="253f6-205">Örnek 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="253f6-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="253f6-206">**fileFilter** bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="253f6-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="253f6-207">Bu özellik, Hadoop dağıtılmış dosya sistemi (HDFS ile) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="253f6-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="253f6-208">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-208">No</span></span> |
| <span data-ttu-id="253f6-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="253f6-209">partitionedBy</span></span> |<span data-ttu-id="253f6-210">Dinamik belirtmek için kullanılan **folderPath** ve **fileName** zaman serisi veriler için.</span><span class="sxs-lookup"><span data-stu-id="253f6-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="253f6-211">Örneğin, belirleyebileceğiniz bir **folderPath** için verileri saatte parametreli.</span><span class="sxs-lookup"><span data-stu-id="253f6-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="253f6-212">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-212">No</span></span> |
| <span data-ttu-id="253f6-213">Biçimi</span><span class="sxs-lookup"><span data-stu-id="253f6-213">format</span></span> | <span data-ttu-id="253f6-214">Şu biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="253f6-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="253f6-215">Ayarlama **türü** şu değerlerden biri biçimine altında özellik.</span><span class="sxs-lookup"><span data-stu-id="253f6-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="253f6-216">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="253f6-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="253f6-217">Depoları arasında (ikili kopya), dosya tabanlı olarak dosyaları kopyalamak istiyorsanız, her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="253f6-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="253f6-218">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-218">No</span></span> |
| <span data-ttu-id="253f6-219">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="253f6-219">compression</span></span> | <span data-ttu-id="253f6-220">Veri sıkıştırma düzeyini ve türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="253f6-221">Desteklenen türler **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**, ve desteklenen düzeyler **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="253f6-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="253f6-222">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="253f6-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="253f6-223">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-223">No</span></span> |
| <span data-ttu-id="253f6-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="253f6-224">useBinaryTransfer</span></span> |<span data-ttu-id="253f6-225">İkili aktarım modunu kullanıp kullanmayacağınızı belirtin.</span><span class="sxs-lookup"><span data-stu-id="253f6-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="253f6-226">Değerleri (Bu değer varsayılan değer) ikili mod için doğru olduğundan ve ASCII için false.</span><span class="sxs-lookup"><span data-stu-id="253f6-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="253f6-227">İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="253f6-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="253f6-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="253f6-229">**Dosya adı** ve **fileFilter** eşzamanlı olarak kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="253f6-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="253f6-230">PartionedBy özelliğini kullanın</span><span class="sxs-lookup"><span data-stu-id="253f6-230">Use the partionedBy property</span></span>
<span data-ttu-id="253f6-231">Önceki bölümde belirtildiği gibi bir dinamik belirtebilirsiniz **folderPath** ve **fileName** zaman serisi verilerle için **partitionedBy** özelliği.</span><span class="sxs-lookup"><span data-stu-id="253f6-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="253f6-232">Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında bilgi edinmek için [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="253f6-233">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="253f6-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="253f6-234">Bu örnekte, {dilim} değişkeninin değeri veri fabrikası sistem SliceStart, belirtilen biçimde (YYYYMMDDHH) ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="253f6-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="253f6-235">Dilimin başlangıç SliceStart başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="253f6-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="253f6-236">Klasör yolu, her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="253f6-236">The folder path is different for each slice.</span></span> <span data-ttu-id="253f6-237">(Örneğin, wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="253f6-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="253f6-238">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="253f6-238">Sample 2</span></span>

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
<span data-ttu-id="253f6-239">Bu örnekte, tarafından kullanılan ayrı değişkenleri içine ayıklanır yıl, ay, gün ve saati SliceStart, **folderPath** ve **fileName** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="253f6-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="253f6-240">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="253f6-240">Copy activity properties</span></span>
<span data-ttu-id="253f6-241">Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen oluşturma](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="253f6-242">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="253f6-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="253f6-243">Kullanılabilir özellikler **typeProperties** etkinlik bölümünü Öte yandan, her etkinlik türü ile değişir.</span><span class="sxs-lookup"><span data-stu-id="253f6-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="253f6-244">Kopya etkinliği için tür özellikleri türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="253f6-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="253f6-245">Kopyalama etkinliğinde kaynak türü olduğunda **FileSystemSource**, aşağıdaki özellikler kullanılabilir **typeProperties** bölümü:</span><span class="sxs-lookup"><span data-stu-id="253f6-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="253f6-246">Özellik</span><span class="sxs-lookup"><span data-stu-id="253f6-246">Property</span></span> | <span data-ttu-id="253f6-247">Açıklama</span><span class="sxs-lookup"><span data-stu-id="253f6-247">Description</span></span> | <span data-ttu-id="253f6-248">İzin verilen değerler</span><span class="sxs-lookup"><span data-stu-id="253f6-248">Allowed values</span></span> | <span data-ttu-id="253f6-249">Gerekli</span><span class="sxs-lookup"><span data-stu-id="253f6-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="253f6-250">Özyinelemeli</span><span class="sxs-lookup"><span data-stu-id="253f6-250">recursive</span></span> |<span data-ttu-id="253f6-251">Alt klasörleri veya yalnızca belirtilen klasöre verileri özyinelemeli olarak okunur olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="253f6-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="253f6-252">TRUE, False (varsayılan)</span><span class="sxs-lookup"><span data-stu-id="253f6-252">True, False (default)</span></span> |<span data-ttu-id="253f6-253">Hayır</span><span class="sxs-lookup"><span data-stu-id="253f6-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="253f6-254">JSON örnek: veri kopyalama FTP sunucusundan Azure Blob</span><span class="sxs-lookup"><span data-stu-id="253f6-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="253f6-255">Bu örnek, bir FTP sunucusundan Azure Blob depolama alanına veri kopyalama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="253f6-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="253f6-256">Ancak, verileri doğrudan belirtilen havuzlarını hiçbirini kopyalanabilir [desteklenen veri depoları ve biçimleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats), Data Factory kopyalama etkinliği kullanarak.</span><span class="sxs-lookup"><span data-stu-id="253f6-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="253f6-257">Aşağıdaki örnekleri kullanarak bir işlem hattı oluşturmak için kullanabileceğiniz örnek JSON tanımları sağlar [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), veya [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="253f6-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="253f6-258">Bağlı hizmet türü [Ftp_sunucusu](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="253f6-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="253f6-259">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="253f6-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="253f6-260">Bir giriş [dataset](data-factory-create-datasets.md) türü [dosya paylaşımı](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="253f6-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="253f6-261">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="253f6-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="253f6-262">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="253f6-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="253f6-263">Örnek verileri saatte bir Azure blob bir FTP sunucusundan kopyalar.</span><span class="sxs-lookup"><span data-stu-id="253f6-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="253f6-264">Bu örnekler kullanılan JSON özellikleri örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="253f6-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="253f6-265">Bağlı FTP hizmeti</span><span class="sxs-lookup"><span data-stu-id="253f6-265">FTP linked service</span></span>

<span data-ttu-id="253f6-266">Bu örnek temel kimlik doğrulaması, kullanıcı adı ve parola düz metin kullanır.</span><span class="sxs-lookup"><span data-stu-id="253f6-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="253f6-267">Aşağıdaki yöntemlerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="253f6-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="253f6-268">Anonim kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="253f6-268">Anonymous authentication</span></span>
* <span data-ttu-id="253f6-269">Şifrelenmiş kimlik bilgileri ile temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="253f6-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="253f6-270">SSL/TLS (FTPS) üzerinden FTP</span><span class="sxs-lookup"><span data-stu-id="253f6-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="253f6-271">Bkz: [FTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="253f6-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="253f6-272">Azure Storage bağlı hizmeti</span><span class="sxs-lookup"><span data-stu-id="253f6-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="253f6-273">FTP giriş veri kümesi</span><span class="sxs-lookup"><span data-stu-id="253f6-273">FTP input dataset</span></span>

<span data-ttu-id="253f6-274">Bu veri kümesi FTP klasöre başvuruyor `mysharedfolder` ve dosya `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="253f6-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="253f6-275">Ardışık Düzen dosya hedefe kopyalar.</span><span class="sxs-lookup"><span data-stu-id="253f6-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="253f6-276">Ayarı **dış** için **true** Data Factory hizmetinin veri kümesi data factory dış ve veri fabrikasında bir etkinlik tarafından üretilen değil bildirir.</span><span class="sxs-lookup"><span data-stu-id="253f6-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="253f6-277">Azure Blob çıktı veri kümesi</span><span class="sxs-lookup"><span data-stu-id="253f6-277">Azure Blob output dataset</span></span>

<span data-ttu-id="253f6-278">Veri her saat yeni bir bloba yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="253f6-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="253f6-279">Klasör yolu blob'a dinamik olarak hesaplanan işleniyor dilim başlangıç zamanı temel alınarak.</span><span class="sxs-lookup"><span data-stu-id="253f6-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="253f6-280">Klasör yolu yıl, ay, gün ve saatleri bölümlerini başlangıç saatini kullanır.</span><span class="sxs-lookup"><span data-stu-id="253f6-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="253f6-281">Dosya sistemi kaynak ve blob havuz sahip işlem hattı kopyalama etkinliği</span><span class="sxs-lookup"><span data-stu-id="253f6-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="253f6-282">Ardışık Düzen giriş ve çıkış veri kümeleri kullanmak üzere yapılandırıldığı ve saatte çalışacak şekilde zamanlanır kopyalama etkinliği içerir.</span><span class="sxs-lookup"><span data-stu-id="253f6-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="253f6-283">JSON tanımını düzenindeki **kaynak** türü ayarlanmış **FileSystemSource**ve **havuz** türü ayarlanmış **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="253f6-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="253f6-284">Kaynak veri kümesi sütunlarından havuz kümesinden sütunlara eşlemek için bkz [Azure Data Factory veri kümesi sütunlarında eşleme](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="253f6-285">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="253f6-285">Next steps</span></span>
<span data-ttu-id="253f6-286">Aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="253f6-286">See the following articles:</span></span>

* <span data-ttu-id="253f6-287">Bu veri fabrikası ve onu en iyi duruma getirmek için çeşitli yollar veri taşıma (kopyalama etkinliği) etkisi performansını anahtar Etkenler hakkında bilgi için bkz [kopyalama etkinliği performans ve ayarlama Kılavuzu](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="253f6-288">Kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için bkz: [kopyalama etkinliği Öğreticisi](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="253f6-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
