---
title: Azure Data Factory kullanarak SFTP sunucudan aaaMove veri | Microsoft Docs
description: "Hakkında bilgi edinin şirket içi veya Bulut SFTP sunucusunu Azure Data Factory kullanarak toomove verileri."
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
ms.date: 06/05/2017
ms.author: jingwang
ms.openlocfilehash: b976289e2c1b1899634bb5565b375499077fa554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-sftp-server-using-azure-data-factory"></a><span data-ttu-id="d4ed4-103">Azure Data Factory kullanarak bir SFTP sunucudan veri taşıma</span><span class="sxs-lookup"><span data-stu-id="d4ed4-103">Move data from an SFTP server using Azure Data Factory</span></span>
<span data-ttu-id="d4ed4-104">Bu makalede nasıl toouse hello kopya etkinliği Azure Data Factory toomove bir şirket içi/bulut SFTP sunucu tooa verilerden havuz veri deposu desteklenen özetlenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud SFTP server tooa supported sink data store.</span></span> <span data-ttu-id="d4ed4-105">Bu makale üzerinde hello derlemeler [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale listesiyle kopyalama etkinliği ve hello kaynakları/havuzlarını desteklenen veri depoları veri taşıma genel bir bakış sunar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="d4ed4-106">Veri Fabrikası şu anda destekleyen bir SFTP server tooother verilerden veri depolar, ancak taşıma yalnızca tooan SFTP sunucuda depolanan verileri diğer veriler taşıma için.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-106">Data factory currently supports only moving data from an SFTP server tooother data stores, but not for moving data from other data stores tooan SFTP server.</span></span> <span data-ttu-id="d4ed4-107">Her iki şirket içi destekler ve SFTP sunucuları bulut.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-107">It supports both on-premises and cloud SFTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ed4-108">Başarıyla kopyalanan toohello hedef tamamlandıktan sonra kopyalama etkinliği hello kaynak dosyayı silmez.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-108">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="d4ed4-109">Sonra başarılı bir kopyasını toodelete hello kaynak dosyası gerekiyorsa, bir özel etkinlik toodelete hello dosyası oluşturun ve hello ardışık düzeninde hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-109">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="d4ed4-110">Desteklenen senaryolar ve kimlik doğrulama türleri</span><span class="sxs-lookup"><span data-stu-id="d4ed4-110">Supported scenarios and authentication types</span></span>
<span data-ttu-id="d4ed4-111">Bu SFTP bağlayıcı toocopy verilerden kullanabilirsiniz **SFTP sunucuları ve şirket içi SFTP sunucuları hem de bulut**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-111">You can use this SFTP connector toocopy data from **both cloud SFTP servers and on-premises SFTP servers**.</span></span> <span data-ttu-id="d4ed4-112">**Temel** ve **SshPublicKey** toohello SFTP sunucusuna bağlanırken kimlik doğrulama türleri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-112">**Basic** and **SshPublicKey** authentication types are supported when connecting toohello SFTP server.</span></span>

<span data-ttu-id="d4ed4-113">Bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında veri yönetimi ağ geçidi hello şirket içi ortamına/Azure VM yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-113">When copying data from an on-premises SFTP server, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="d4ed4-114">Bkz: [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) hello ağ geçidi hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-114">See [Data Management Gateway](data-factory-data-management-gateway.md) for details on hello gateway.</span></span> <span data-ttu-id="d4ed4-115">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale hello ağ geçidi kurun ayarlama ve kullanmaya ilişkin adım adım yönergeler.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-115">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway and using it.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d4ed4-116">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d4ed4-116">Getting started</span></span>
<span data-ttu-id="d4ed4-117">Farklı araçlar/API'lerini kullanarak bir SFTP kaynaktan verileri taşır kopyalama etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-117">You can create a pipeline with a copy activity that moves data from an SFTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="d4ed4-118">Merhaba en kolay yolu toocreate bir ardışık düzen olduğu toouse hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d4ed4-119">Bkz: [öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma](data-factory-copy-data-wizard-tutorial.md) hello kopya veri Sihirbazı'nı kullanarak bir işlem hattı oluşturma Hızlı Kılavuz.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="d4ed4-120">Aşağıdaki araçlar toocreate bir ardışık düzen hello de kullanabilirsiniz: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager şablonu** , **.NET API**, ve **REST API**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d4ed4-121">Bkz: [kopyalama etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) adım adım yönergeler toocreate kopyalama etkinliği ile işlem hattı için.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="d4ed4-122">SFTP sunucu tooAzure Blob Storage toocopy verileri JSON örnekleri için bkz: [JSON örnek: SFTP sunucu tooAzure blobundan veri kopyalama](#json-example-copy-data-from-sftp-server-to-azure-blob) bu makalenin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-122">For JSON samples toocopy data from SFTP server tooAzure Blob Storage, see [JSON Example: Copy data from SFTP server tooAzure blob](#json-example-copy-data-from-sftp-server-to-azure-blob) section of this article.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="d4ed4-123">Bağlantılı hizmet özellikleri</span><span class="sxs-lookup"><span data-stu-id="d4ed4-123">Linked service properties</span></span>
<span data-ttu-id="d4ed4-124">Aşağıdaki tablonun hello JSON öğeleri belirli tooFTP bağlantılı hizmeti için bir açıklama sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-124">hello following table provides description for JSON elements specific tooFTP linked service.</span></span>

| <span data-ttu-id="d4ed4-125">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4ed4-125">Property</span></span> | <span data-ttu-id="d4ed4-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4ed4-126">Description</span></span> | <span data-ttu-id="d4ed4-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4ed4-127">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4ed4-128">type</span><span class="sxs-lookup"><span data-stu-id="d4ed4-128">type</span></span> | <span data-ttu-id="d4ed4-129">Merhaba type özelliği çok ayarlanmalıdır`Sftp`.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-129">hello type property must be set too`Sftp`.</span></span> |<span data-ttu-id="d4ed4-130">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-130">Yes</span></span> |
| <span data-ttu-id="d4ed4-131">ana bilgisayar</span><span class="sxs-lookup"><span data-stu-id="d4ed4-131">host</span></span> | <span data-ttu-id="d4ed4-132">Merhaba SFTP sunucu adı veya IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-132">Name or IP address of hello SFTP server.</span></span> |<span data-ttu-id="d4ed4-133">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-133">Yes</span></span> |
| <span data-ttu-id="d4ed4-134">port</span><span class="sxs-lookup"><span data-stu-id="d4ed4-134">port</span></span> |<span data-ttu-id="d4ed4-135">Hangi hello SFTP sunucusunun dinleme yaptığı bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-135">Port on which hello SFTP server is listening.</span></span> <span data-ttu-id="d4ed4-136">Merhaba varsayılan değer: 21</span><span class="sxs-lookup"><span data-stu-id="d4ed4-136">hello default value is: 21</span></span> |<span data-ttu-id="d4ed4-137">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-137">No</span></span> |
| <span data-ttu-id="d4ed4-138">authenticationType</span><span class="sxs-lookup"><span data-stu-id="d4ed4-138">authenticationType</span></span> |<span data-ttu-id="d4ed4-139">Kimlik doğrulama türü belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-139">Specify authentication type.</span></span> <span data-ttu-id="d4ed4-140">İzin verilen değerler: **temel**, **SshPublicKey**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-140">Allowed values: **Basic**, **SshPublicKey**.</span></span> <br><br> <span data-ttu-id="d4ed4-141">Çok başvuran[kullanarak temel kimlik doğrulaması](#using-basic-authentication) ve [kullanarak SSH ortak anahtar kimlik doğrulaması](#using-ssh-public-key-authentication) daha fazla özellikleri ve JSON örnekleri sırasıyla bölümler.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-141">Refer too[Using basic authentication](#using-basic-authentication) and [Using SSH public key authentication](#using-ssh-public-key-authentication) sections on more properties and JSON samples respectively.</span></span> |<span data-ttu-id="d4ed4-142">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-142">Yes</span></span> |
| <span data-ttu-id="d4ed4-143">skipHostKeyValidation</span><span class="sxs-lookup"><span data-stu-id="d4ed4-143">skipHostKeyValidation</span></span> | <span data-ttu-id="d4ed4-144">Tooskip anahtar doğrulama konak olup olmadığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-144">Specify whether tooskip host key validation.</span></span> | <span data-ttu-id="d4ed4-145">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-145">No.</span></span> <span data-ttu-id="d4ed4-146">Merhaba varsayılan değeri: false</span><span class="sxs-lookup"><span data-stu-id="d4ed4-146">hello default value: false</span></span> |
| <span data-ttu-id="d4ed4-147">hostKeyFingerprint</span><span class="sxs-lookup"><span data-stu-id="d4ed4-147">hostKeyFingerprint</span></span> | <span data-ttu-id="d4ed4-148">Merhaba parmak izi hello ana bilgisayar anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-148">Specify hello finger print of hello host key.</span></span> | <span data-ttu-id="d4ed4-149">Merhaba, Evet `skipHostKeyValidation` toofalse ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-149">Yes if hello `skipHostKeyValidation` is set toofalse.</span></span>  |
| <span data-ttu-id="d4ed4-150">gatewayName</span><span class="sxs-lookup"><span data-stu-id="d4ed4-150">gatewayName</span></span> |<span data-ttu-id="d4ed4-151">Merhaba veri yönetimi ağ geçidi tooconnect tooan adını SFTP sunucu şirket içi.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-151">Name of hello Data Management Gateway tooconnect tooan on-premises SFTP server.</span></span> | <span data-ttu-id="d4ed4-152">Bir şirket içi SFTP sunucusundan veri kopyalama, Evet.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-152">Yes if copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="d4ed4-153">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="d4ed4-153">encryptedCredential</span></span> | <span data-ttu-id="d4ed4-154">Şifrelenmiş kimlik bilgileri tooaccess hello SFTP sunucusu.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-154">Encrypted credential tooaccess hello SFTP server.</span></span> <span data-ttu-id="d4ed4-155">Otomatik olarak oluşturulan, temel kimlik doğrulaması (kullanıcı adı + parola) veya SshPublicKey kimlik (kullanıcı adı + özel anahtar yolu veya içerik) Kopyalama Sihirbazı'nı veya hello ClickOnce açılan iletişim kutusunda belirttiğiniz zaman.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-155">Auto-generated when you specify basic authentication (username + password) or SshPublicKey authentication (username + private key path or content) in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="d4ed4-156">Hayır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-156">No.</span></span> <span data-ttu-id="d4ed4-157">Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-157">Apply only when copying data from an on-premises SFTP server.</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="d4ed4-158">Temel kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="d4ed4-158">Using basic authentication</span></span>

<span data-ttu-id="d4ed4-159">toouse temel kimlik doğrulamasını ayarlamak `authenticationType` olarak `Basic`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-159">toouse basic authentication, set `authenticationType` as `Basic`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="d4ed4-160">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4ed4-160">Property</span></span> | <span data-ttu-id="d4ed4-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4ed4-161">Description</span></span> | <span data-ttu-id="d4ed4-162">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4ed4-162">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4ed4-163">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d4ed4-163">username</span></span> | <span data-ttu-id="d4ed4-164">Erişim toohello SFTP sunucusu olan kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-164">User who has access toohello SFTP server.</span></span> |<span data-ttu-id="d4ed4-165">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-165">Yes</span></span> |
| <span data-ttu-id="d4ed4-166">password</span><span class="sxs-lookup"><span data-stu-id="d4ed4-166">password</span></span> | <span data-ttu-id="d4ed4-167">Merhaba kullanıcının (kullanıcı adı) parolası.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-167">Password for hello user (username).</span></span> | <span data-ttu-id="d4ed4-168">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-168">Yes</span></span> |

#### <a name="example-basic-authentication"></a><span data-ttu-id="d4ed4-169">Örnek: Temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d4ed4-169">Example: Basic authentication</span></span>
```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a><span data-ttu-id="d4ed4-170">Örnek: Temel kimlik doğrulaması ile şifrelenmiş kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="d4ed4-170">Example: Basic authentication with encrypted credential</span></span>

```JSON
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
      }
}
```

### <a name="using-ssh-public-key-authentication"></a><span data-ttu-id="d4ed4-171">SSH ortak anahtar kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="d4ed4-171">Using SSH public key authentication</span></span>

<span data-ttu-id="d4ed4-172">toouse SSH ortak anahtar kimlik doğrulaması, ayarlamak `authenticationType` olarak `SshPublicKey`ve bunun yanında, SFTP bağlayıcı hello son bölümde sunulan genel olanları hello aşağıdaki özelliklere hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-172">toouse SSH public key authentication, set `authenticationType` as `SshPublicKey`, and specify hello following properties besides hello SFTP connector generic ones introduced in hello last section:</span></span>

| <span data-ttu-id="d4ed4-173">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4ed4-173">Property</span></span> | <span data-ttu-id="d4ed4-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4ed4-174">Description</span></span> | <span data-ttu-id="d4ed4-175">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4ed4-175">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d4ed4-176">kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d4ed4-176">username</span></span> |<span data-ttu-id="d4ed4-177">Erişim toohello SFTP sunucusu olan kullanıcı</span><span class="sxs-lookup"><span data-stu-id="d4ed4-177">User who has access toohello SFTP server</span></span> |<span data-ttu-id="d4ed4-178">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-178">Yes</span></span> |
| <span data-ttu-id="d4ed4-179">privateKeyPath</span><span class="sxs-lookup"><span data-stu-id="d4ed4-179">privateKeyPath</span></span> | <span data-ttu-id="d4ed4-180">Mutlak yol toohello belirtin özel anahtar dosyası bu ağ geçidi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-180">Specify absolute path toohello private key file that gateway can access.</span></span> | <span data-ttu-id="d4ed4-181">Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-181">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> <br><br> <span data-ttu-id="d4ed4-182">Yalnızca bir şirket içi SFTP sunucusundan veri kopyalama işlemi sırasında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-182">Apply only when copying data from an on-premises SFTP server.</span></span> |
| <span data-ttu-id="d4ed4-183">privateKeyContent</span><span class="sxs-lookup"><span data-stu-id="d4ed4-183">privateKeyContent</span></span> | <span data-ttu-id="d4ed4-184">Merhaba özel anahtar içeriğinin seri hale getirilmiş bir dize.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-184">A serialized string of hello private key content.</span></span> <span data-ttu-id="d4ed4-185">Merhaba Kopyalama Sihirbazı'nı hello özel anahtar dosyası okuma ve hello özel anahtar içeriği otomatik olarak ayıklar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-185">hello Copy Wizard can read hello private key file and extract hello private key content automatically.</span></span> <span data-ttu-id="d4ed4-186">Tüm diğer aracı/SDK kullanıyorsanız, bunun yerine hello privateKeyPath özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-186">If you are using any other tool/SDK, use hello privateKeyPath property instead.</span></span> | <span data-ttu-id="d4ed4-187">Her iki hello belirtin `privateKeyPath` veya `privateKeyContent`.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-187">Specify either hello `privateKeyPath` or `privateKeyContent`.</span></span> |
| <span data-ttu-id="d4ed4-188">Parola</span><span class="sxs-lookup"><span data-stu-id="d4ed4-188">passPhrase</span></span> | <span data-ttu-id="d4ed4-189">Merhaba anahtar dosyası bir parola deyimi tarafından korunuyorsa hello geçişi tümcecik/parola toodecrypt hello özel anahtarı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-189">Specify hello pass phrase/password toodecrypt hello private key if hello key file is protected by a pass phrase.</span></span> | <span data-ttu-id="d4ed4-190">Merhaba özel anahtar dosyası bir parola deyimi tarafından korunuyorsa, Evet.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-190">Yes if hello private key file is protected by a pass phrase.</span></span> |

> [!NOTE]
> <span data-ttu-id="d4ed4-191">SFTP Bağlayıcısı yalnızca OpenSSH anahtarını destekler.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-191">SFTP connector only support OpenSSH key.</span></span> <span data-ttu-id="d4ed4-192">Anahtar dosyanızı hello doğru biçimde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-192">Make sure your key file is in hello proper format.</span></span> <span data-ttu-id="d4ed4-193">Putty aracı tooconvert .ppk tooOpenSSH biçiminden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-193">You can use Putty tool tooconvert from .ppk tooOpenSSH format.</span></span>

#### <a name="example-sshpublickey-authentication-using-private-key-filepath"></a><span data-ttu-id="d4ed4-194">Örnek: özel anahtar filePath kullanarak SshPublicKey kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d4ed4-194">Example: SshPublicKey authentication using private key filePath</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "mygateway"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a><span data-ttu-id="d4ed4-195">Örnek: özel anahtar içeriği kullanarak SshPublicKey kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d4ed4-195">Example: SshPublicKey authentication using private key content</span></span>

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="d4ed4-196">Veri kümesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="d4ed4-196">Dataset properties</span></span>
<span data-ttu-id="d4ed4-197">Merhaba bölümleri & özellikleri veri kümeleri tanımlamak için kullanılabilir tam listesi için bkz [veri kümeleri oluşturma](data-factory-create-datasets.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-197">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d4ed4-198">Bölümler yapısı, kullanılabilirlik ve bir veri kümesi JSON İlkesi gibi tüm veri kümesi türleri için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-198">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="d4ed4-199">Merhaba **typeProperties** bölümü, her veri kümesi türü için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-199">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="d4ed4-200">Belirli toohello veri kümesi türü olan bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-200">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="d4ed4-201">Merhaba typeProperties bölüm türü veri kümesi için **FileShare** veri kümesine hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-201">hello typeProperties section for a dataset of type **FileShare** dataset has hello following properties:</span></span>

| <span data-ttu-id="d4ed4-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="d4ed4-202">Property</span></span> | <span data-ttu-id="d4ed4-203">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d4ed4-203">Description</span></span> | <span data-ttu-id="d4ed4-204">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d4ed4-204">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d4ed4-205">folderPath</span><span class="sxs-lookup"><span data-stu-id="d4ed4-205">folderPath</span></span> |<span data-ttu-id="d4ed4-206">Alt yolu toohello klasörü.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-206">Sub path toohello folder.</span></span> <span data-ttu-id="d4ed4-207">Kaçış karakteri kullanmak ' \ ' hello dize özel karakter.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-207">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="d4ed4-208">Bkz: [örnek bağlantılı hizmeti ve veri kümesi tanımları](#sample-linked-service-and-dataset-definitions) örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-208">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="d4ed4-209">Bu özellik ile birleştirebilirsiniz **partitionBy** toohave klasör yolları dilimine göre başlangıç/bitiş tarih saatleri.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-209">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="d4ed4-210">Evet</span><span class="sxs-lookup"><span data-stu-id="d4ed4-210">Yes</span></span> |
| <span data-ttu-id="d4ed4-211">fileName</span><span class="sxs-lookup"><span data-stu-id="d4ed4-211">fileName</span></span> |<span data-ttu-id="d4ed4-212">Hello Hello hello dosyasının adını belirtin **folderPath** hello tablo toorefer tooa belirli dosya hello klasöründeki istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-212">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="d4ed4-213">Bu özellik için herhangi bir değer belirtmezseniz, hello tablo hello klasöründeki tooall dosyaları işaret eder.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-213">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="d4ed4-214">FileName bir çıkış veri kümesi için belirtilmediğinde oluşturulan hello dosyasının hello adı Bu biçim aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-214">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="d4ed4-215">Veriler. <Guid>.txt (örnek: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="d4ed4-215">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="d4ed4-216">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-216">No</span></span> |
| <span data-ttu-id="d4ed4-217">fileFilter</span><span class="sxs-lookup"><span data-stu-id="d4ed4-217">fileFilter</span></span> |<span data-ttu-id="d4ed4-218">Tüm dosyalar yerine hello folderPath dosyaları kümesini filtre toobe tooselect kullanılan belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-218">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span><br/><br/><span data-ttu-id="d4ed4-219">İzin verilen değerler: `*` (birden çok karakter) ve `?` (tek bir karakter).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-219">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="d4ed4-220">Örnek 1:`"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="d4ed4-220">Examples 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="d4ed4-221">Örnek 2:`"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="d4ed4-221">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="d4ed4-222">fileFilter bir giriş FileShare veri kümesi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-222">fileFilter is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="d4ed4-223">Bu özellik ile HDFS desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-223">This property is not supported with HDFS.</span></span> |<span data-ttu-id="d4ed4-224">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-224">No</span></span> |
| <span data-ttu-id="d4ed4-225">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="d4ed4-225">partitionedBy</span></span> |<span data-ttu-id="d4ed4-226">partitionedBy kullanılan toospecify dinamik folderPath zaman serisi veri için dosya adı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-226">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="d4ed4-227">Örneğin, her veri saat için parametreli folderPath.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-227">For example, folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="d4ed4-228">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-228">No</span></span> |
| <span data-ttu-id="d4ed4-229">Biçimi</span><span class="sxs-lookup"><span data-stu-id="d4ed4-229">format</span></span> | <span data-ttu-id="d4ed4-230">şu biçimi türlerini hello desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-230">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="d4ed4-231">Set hello **türü** biçimi tooone şu değerlerden biri altında özellik.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-231">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="d4ed4-232">Daha fazla bilgi için bkz: [metin biçimi](data-factory-supported-file-and-compression-formats.md#text-format), [Json biçimine](data-factory-supported-file-and-compression-formats.md#json-format), [Avro biçimi](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc biçimi](data-factory-supported-file-and-compression-formats.md#orc-format), ve [Parquet biçimi](data-factory-supported-file-and-compression-formats.md#parquet-format) bölümler.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-232">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="d4ed4-233">Çok istiyorsanız**olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında hello Biçim bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-233">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="d4ed4-234">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-234">No</span></span> |
| <span data-ttu-id="d4ed4-235">Sıkıştırma</span><span class="sxs-lookup"><span data-stu-id="d4ed4-235">compression</span></span> | <span data-ttu-id="d4ed4-236">Merhaba türünü ve hello veri sıkıştırma düzeyini belirtin.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-236">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="d4ed4-237">Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-237">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="d4ed4-238">Desteklenen düzeyler: **Optimal** ve **en hızlı**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-238">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="d4ed4-239">Daha fazla bilgi için bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-239">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="d4ed4-240">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-240">No</span></span> |
| <span data-ttu-id="d4ed4-241">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="d4ed4-241">useBinaryTransfer</span></span> |<span data-ttu-id="d4ed4-242">Belirtin olup ikili aktarım modunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-242">Specify whether use Binary transfer mode.</span></span> <span data-ttu-id="d4ed4-243">İkili mod ve false ASCII için true.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-243">True for binary mode and false ASCII.</span></span> <span data-ttu-id="d4ed4-244">Varsayılan değer: True.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-244">Default value: True.</span></span> <span data-ttu-id="d4ed4-245">İlişkili bağlantılı hizmet türü türü olduğunda bu özellik yalnızca kullanılabilir: Ftp_sunucusu.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-245">This property can only be used when associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="d4ed4-246">Hayır</span><span class="sxs-lookup"><span data-stu-id="d4ed4-246">No</span></span> |

> [!NOTE]
> <span data-ttu-id="d4ed4-247">Dosya adı ve fileFilter aynı anda kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-247">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="d4ed4-248">PartionedBy özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="d4ed4-248">Using partionedBy property</span></span>
<span data-ttu-id="d4ed4-249">Merhaba önceki bölümünde belirtildiği gibi dinamik bir folderPath, zaman serisi veri partitionedBy ile dosya adını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-249">As mentioned in hello previous section, you can specify a dynamic folderPath, filename for time series data with partitionedBy.</span></span> <span data-ttu-id="d4ed4-250">Merhaba Data Factory makroları ve hello sistem değişkeni SliceStart, verilen veri dilimi için mantıksal süre hello belirtmek SliceEnd bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-250">You can do so with hello Data Factory macros and hello system variable SliceStart, SliceEnd that indicate hello logical time period for a given data slice.</span></span>

<span data-ttu-id="d4ed4-251">Zaman serisi veri kümeleri, zamanlama ve dilimleri hakkında toolearn bkz [veri kümeleri oluşturma](data-factory-create-datasets.md), [zamanlama ve yürütme](data-factory-scheduling-and-execution.md), ve [oluşturma ardışık düzen](data-factory-create-pipelines.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-251">toolearn about time series datasets, scheduling, and slices, See [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="d4ed4-252">Örnek 1:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-252">Sample 1:</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="d4ed4-253">Bu örnekte {dilim} belirtilen hello Data Factory sistem değişkenin değerini SliceStart hello biçiminde (YYYYMMDDHH) ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-253">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="d4ed4-254">Merhaba SliceStart hello dilim toostart süresini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-254">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="d4ed4-255">Merhaba folderPath her dilim için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-255">hello folderPath is different for each slice.</span></span> <span data-ttu-id="d4ed4-256">Örnek: wikidatagateway/wikisampledataout/2014100103 veya wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-256">Example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="d4ed4-257">Örnek 2:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-257">Sample 2:</span></span>

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
<span data-ttu-id="d4ed4-258">Bu örnekte, folderPath ve fileName özellikleri tarafından kullanılan ayrı değişkenleri içine yıl, ay, gün ve saat SliceStart ayıklanır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-258">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="d4ed4-259">Etkinlik özellikleri Kopyala</span><span class="sxs-lookup"><span data-stu-id="d4ed4-259">Copy activity properties</span></span>
<span data-ttu-id="d4ed4-260">Merhaba bölümleri & özellikleri etkinlikleri tanımlamak için kullanılabilir tam listesi için bkz [oluşturma ardışık düzen](data-factory-create-pipelines.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-260">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d4ed4-261">Ad, açıklama, giriş ve çıkış tabloları ve ilkeleri gibi özellikler etkinlikleri tüm türleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-261">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="d4ed4-262">Oysa Hello özellikler kullanılabilir hello etkinlik hello typeProperties bölümünde her etkinlik türü ile farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-262">Whereas, hello properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d4ed4-263">Kopya etkinliği için hello türü özellikleri hello türlerini kaynakları ve havuzlarını bağlı olarak farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-263">For Copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

[!INCLUDE [data-factory-file-system-source](../../includes/data-factory-file-system-source.md)]

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="d4ed4-264">Desteklenen dosya ve sıkıştırma biçimleri</span><span class="sxs-lookup"><span data-stu-id="d4ed4-264">Supported file and compression formats</span></span>
<span data-ttu-id="d4ed4-265">Bkz: [Azure Data Factory dosya ve sıkıştırma biçimlerde](data-factory-supported-file-and-compression-formats.md) makale ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-265">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-sftp-server-tooazure-blob"></a><span data-ttu-id="d4ed4-266">JSON örnek: Verilerini SFTP sunucu tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="d4ed4-266">JSON Example: Copy data from SFTP server tooAzure blob</span></span>
<span data-ttu-id="d4ed4-267">Merhaba aşağıdaki örnek örnek JSON tanımları sağlar, toocreate bir ardışık düzen kullanarak kullanabilirsiniz [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) veya [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) veya [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-267">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d4ed4-268">Bunların nasıl SFTP toocopy verileri tooAzure Blob Depolama kaynağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-268">They show how toocopy data from SFTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="d4ed4-269">Ancak, veriler kopyalanabilir **doğrudan** herhangi birinden belirtildiği hello havuzlarını, kaynakları tooany [burada](data-factory-data-movement-activities.md#supported-data-stores-and-formats) kullanarak Azure Data Factory kopyalama etkinliği hello.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-269">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4ed4-270">Bu örnek, JSON parçacıklarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-270">This sample provides JSON snippets.</span></span> <span data-ttu-id="d4ed4-271">Merhaba veri fabrikası oluşturma için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-271">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="d4ed4-272">Bkz: [Bulut ve şirket içi konumlara arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-272">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="d4ed4-273">Merhaba örnek data factory varlıklarını aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-273">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="d4ed4-274">Bağlı hizmet türü [sftp](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-274">A linked service of type [sftp](#linked-service-properties).</span></span>
* <span data-ttu-id="d4ed4-275">Bağlı hizmet türü [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-275">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="d4ed4-276">Bir giriş [dataset](data-factory-create-datasets.md) türü [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-276">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="d4ed4-277">Bir çıkış [dataset](data-factory-create-datasets.md) türü [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-277">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="d4ed4-278">A [ardışık düzen](data-factory-create-pipelines.md) kullanan kopyalama etkinliği ile [FileSystemSource](#copy-activity-properties) ve [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-278">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d4ed4-279">Merhaba örnek verileri saatte bir SFTP server tooan Azure blob kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-279">hello sample copies data from an SFTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="d4ed4-280">Bu örnekler kullanılan hello JSON özellikleri hello örnekleri aşağıdaki bölümlerde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-280">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d4ed4-281">**SFTP bağlı hizmet**</span><span class="sxs-lookup"><span data-stu-id="d4ed4-281">**SFTP linked service**</span></span>

<span data-ttu-id="d4ed4-282">Bu örnekte, kullanıcı adı ve parola düz metin hello temel kimlik doğrulaması kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-282">This example uses hello basic authentication with user name and password in plain text.</span></span> <span data-ttu-id="d4ed4-283">Aşağıdaki şekilde hello birini de kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-283">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="d4ed4-284">Şifrelenmiş kimlik bilgileri ile temel kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d4ed4-284">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="d4ed4-285">SSH ortak anahtar kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d4ed4-285">SSH public key authentication</span></span>

<span data-ttu-id="d4ed4-286">Bkz: [FTP bağlantılı hizmeti](#linked-service-properties) bölümü için farklı tür kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-286">See [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON

{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver",
            "port": 22,
            "authenticationType": "Basic",
            "username": "myuser",
            "password": "mypassword",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "mygateway"
        }
    }
}
```
<span data-ttu-id="d4ed4-287">**Azure Storage bağlı hizmeti**</span><span class="sxs-lookup"><span data-stu-id="d4ed4-287">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="d4ed4-288">**SFTP girdi veri kümesi**</span><span class="sxs-lookup"><span data-stu-id="d4ed4-288">**SFTP input dataset**</span></span>

<span data-ttu-id="d4ed4-289">Bu veri kümesi toohello SFTP klasörü işaret ediyor `mysharedfolder` ve dosya `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-289">This dataset refers toohello SFTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="d4ed4-290">Merhaba ardışık düzen hello dosya toohello hedef kopyalar.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-290">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="d4ed4-291">"Dış" ayarı: "true" bildirir hello Data Factory hizmetinin bu hello dataset dış toohello veri fabrikası olan ve hello veri fabrikasında bir etkinlik tarafından üretilen değil.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-291">Setting "external": "true" informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SFTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "SftpLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="d4ed4-292">**Azure Blob dataset çıktı**</span><span class="sxs-lookup"><span data-stu-id="d4ed4-292">**Azure Blob output dataset**</span></span>

<span data-ttu-id="d4ed4-293">Veri saatte tooa yeni blob yazılır (sıklığı: saat, aralığı: 1).</span><span class="sxs-lookup"><span data-stu-id="d4ed4-293">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d4ed4-294">hello blob Hello klasör yolu dinamik işlenmekte olan hello dilimin hello başlangıç zamanı temel alınarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-294">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d4ed4-295">Merhaba klasör yolu hello başlangıç zamanı yıl, ay, gün ve saat bölümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-295">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="d4ed4-296">**Kopyalama etkinliği ile kanalı**</span><span class="sxs-lookup"><span data-stu-id="d4ed4-296">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="d4ed4-297">Merhaba ardışık düzen içeren yapılandırılmış toouse olan kopyalama etkinliği girdi ve çıktı veri kümeleri hello ve zamanlanmış toorun her saatte birdir.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-297">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d4ed4-298">JSON tanımını Hello ardışık düzeninde, hello **kaynak** türü olarak ayarlanmış çok**FileSystemSource** ve **havuz** türü olarak ayarlanmış çok**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-298">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
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
        "start": "2017-02-20T18:00:00Z",
        "end": "2017-02-20T19:00:00Z"
    }
}
```

## <a name="performance-and-tuning"></a><span data-ttu-id="d4ed4-299">Performans ve ayarlama</span><span class="sxs-lookup"><span data-stu-id="d4ed4-299">Performance and Tuning</span></span>
<span data-ttu-id="d4ed4-300">Bkz: [kopya etkinliği performansının & ayarlama Kılavuzu](data-factory-copy-activity-performance.md) toolearn anahtarı hakkında Etkenler bu veri taşıma (kopyalama etkinliği) Azure Data Factory ve çeşitli yolları toooptimize etkisi performansını da.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-300">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4ed4-301">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d4ed4-301">Next Steps</span></span>
<span data-ttu-id="d4ed4-302">Aşağıdaki makaleleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="d4ed4-302">See hello following articles:</span></span>

* <span data-ttu-id="d4ed4-303">[Kopya etkinliği öğretici](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) kopyalama etkinliği ile işlem hattı oluşturmak için adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="d4ed4-303">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
