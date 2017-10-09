---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: "Bilgi nasıl toodeploy bir web uygulaması tooa sanal makine. Bu komut dosyası yoksa hello gerekli kaynakları Azure aboneliğinizde oluşturur."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="24618-104">Yayımlama WebApplicationVM (Windows PowerShell komut dosyası)</span><span class="sxs-lookup"><span data-stu-id="24618-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="24618-105">Bir web uygulaması tooa sanal makine dağıtır.</span><span class="sxs-lookup"><span data-stu-id="24618-105">Deploys a web application tooa virtual machine.</span></span> <span data-ttu-id="24618-106">yoksa hello komut dosyası Azure aboneliğinizde hello gerekli kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="24618-106">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a><span data-ttu-id="24618-107">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="24618-107">Configuration</span></span>
<span data-ttu-id="24618-108">Merhaba dağıtımın hello ayrıntılarını açıklayan hello yolu toohello JSON yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="24618-108">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="24618-109">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-109">Aliases</span></span> | <span data-ttu-id="24618-110">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-111">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-111">Required?</span></span> |<span data-ttu-id="24618-112">TRUE</span><span class="sxs-lookup"><span data-stu-id="24618-112">true</span></span> |
| <span data-ttu-id="24618-113">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-113">Position</span></span> |<span data-ttu-id="24618-114">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-114">named</span></span> |
| <span data-ttu-id="24618-115">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-115">Default value</span></span> |<span data-ttu-id="24618-116">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-116">none</span></span> |
| <span data-ttu-id="24618-117">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-117">Accept pipeline input?</span></span> |<span data-ttu-id="24618-118">False</span><span class="sxs-lookup"><span data-stu-id="24618-118">false</span></span> |
| <span data-ttu-id="24618-119">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-119">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-120">False</span><span class="sxs-lookup"><span data-stu-id="24618-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="24618-121">varlığıyla subscriptionName</span><span class="sxs-lookup"><span data-stu-id="24618-121">SubscriptionName</span></span>
<span data-ttu-id="24618-122">Merhaba adını hello toocreate hello sanal makine istediğiniz Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="24618-122">hello name of hello Azure subscription in which you want toocreate hello virtual machine.</span></span>

| <span data-ttu-id="24618-123">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-123">Aliases</span></span> | <span data-ttu-id="24618-124">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-125">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-125">Required?</span></span> |<span data-ttu-id="24618-126">False</span><span class="sxs-lookup"><span data-stu-id="24618-126">false</span></span> |
| <span data-ttu-id="24618-127">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-127">Position</span></span> |<span data-ttu-id="24618-128">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-128">named</span></span> |
| <span data-ttu-id="24618-129">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-129">Default value</span></span> |<span data-ttu-id="24618-130">Merhaba ilk abonelik hello abonelik dosyasındaki kullanır</span><span class="sxs-lookup"><span data-stu-id="24618-130">Uses hello first subscription in hello subscription file</span></span> |
| <span data-ttu-id="24618-131">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-131">Accept pipeline input?</span></span> |<span data-ttu-id="24618-132">False</span><span class="sxs-lookup"><span data-stu-id="24618-132">false</span></span> |
| <span data-ttu-id="24618-133">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-133">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-134">False</span><span class="sxs-lookup"><span data-stu-id="24618-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="24618-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="24618-135">WebDeployPackage</span></span>
<span data-ttu-id="24618-136">Merhaba yolu toohello web dağıtım paketi toopublish toohello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="24618-136">hello path toohello web deployment package toopublish toohello virtual machine.</span></span> <span data-ttu-id="24618-137">Visual Studio'da hello Web Yayımlama Sihirbazı'nı kullanarak bu paketi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24618-137">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="24618-138">Bkz: [nasıl yapılır: Visual Studio'da bir Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="24618-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="24618-139">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-139">Aliases</span></span> | <span data-ttu-id="24618-140">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-141">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-141">Required?</span></span> |<span data-ttu-id="24618-142">False</span><span class="sxs-lookup"><span data-stu-id="24618-142">false</span></span> |
| <span data-ttu-id="24618-143">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-143">Position</span></span> |<span data-ttu-id="24618-144">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-144">named</span></span> |
| <span data-ttu-id="24618-145">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-145">Default value</span></span> |<span data-ttu-id="24618-146">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-146">none</span></span> |
| <span data-ttu-id="24618-147">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-147">Accept pipeline input?</span></span> |<span data-ttu-id="24618-148">False</span><span class="sxs-lookup"><span data-stu-id="24618-148">false</span></span> |
| <span data-ttu-id="24618-149">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-149">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-150">False</span><span class="sxs-lookup"><span data-stu-id="24618-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="24618-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="24618-151">AllowUntrusted</span></span>
<span data-ttu-id="24618-152">TRUE ise, bir güvenilen kök yetkilisi tarafından imzalanmadığını sertifikaları hello kullanılmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="24618-152">If true, allow hello use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="24618-153">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-153">Aliases</span></span> | <span data-ttu-id="24618-154">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-155">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-155">Required?</span></span> |<span data-ttu-id="24618-156">False</span><span class="sxs-lookup"><span data-stu-id="24618-156">false</span></span> |
| <span data-ttu-id="24618-157">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-157">Position</span></span> |<span data-ttu-id="24618-158">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-158">named</span></span> |
| <span data-ttu-id="24618-159">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-159">Default value</span></span> |<span data-ttu-id="24618-160">False</span><span class="sxs-lookup"><span data-stu-id="24618-160">false</span></span> |
| <span data-ttu-id="24618-161">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-161">Accept pipeline input?</span></span> |<span data-ttu-id="24618-162">False</span><span class="sxs-lookup"><span data-stu-id="24618-162">false</span></span> |
| <span data-ttu-id="24618-163">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-163">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-164">False</span><span class="sxs-lookup"><span data-stu-id="24618-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="24618-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="24618-165">VMPassword</span></span>
<span data-ttu-id="24618-166">Hello hello sanal makine hesabı için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="24618-166">hello credentials for hello virtual machine account.</span></span> <span data-ttu-id="24618-167">Örnek: - VMPassword @{Name = "Yönetici"; Parola = "parola"}</span><span class="sxs-lookup"><span data-stu-id="24618-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="24618-168">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-168">Aliases</span></span> | <span data-ttu-id="24618-169">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-170">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-170">Required?</span></span> |<span data-ttu-id="24618-171">False</span><span class="sxs-lookup"><span data-stu-id="24618-171">false</span></span> |
| <span data-ttu-id="24618-172">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-172">Position</span></span> |<span data-ttu-id="24618-173">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-173">named</span></span> |
| <span data-ttu-id="24618-174">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-174">Default value</span></span> |<span data-ttu-id="24618-175">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-175">none</span></span> |
| <span data-ttu-id="24618-176">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-176">Accept pipeline input?</span></span> |<span data-ttu-id="24618-177">False</span><span class="sxs-lookup"><span data-stu-id="24618-177">false</span></span> |
| <span data-ttu-id="24618-178">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-178">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-179">False</span><span class="sxs-lookup"><span data-stu-id="24618-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="24618-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="24618-180">DatabaseServerPassword</span></span>
<span data-ttu-id="24618-181">Azure SQL veritabanı hello Hello kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="24618-181">hello credentials for hello SQL database in Azure.</span></span> <span data-ttu-id="24618-182">Örnek: - DatabaseServerPassword @{Name = "Yönetici"; Parola = "parola"}</span><span class="sxs-lookup"><span data-stu-id="24618-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="24618-183">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-183">Aliases</span></span> | <span data-ttu-id="24618-184">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-185">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-185">Required?</span></span> |<span data-ttu-id="24618-186">False</span><span class="sxs-lookup"><span data-stu-id="24618-186">false</span></span> |
| <span data-ttu-id="24618-187">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-187">Position</span></span> |<span data-ttu-id="24618-188">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-188">named</span></span> |
| <span data-ttu-id="24618-189">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-189">Default value</span></span> |<span data-ttu-id="24618-190">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-190">none</span></span> |
| <span data-ttu-id="24618-191">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-191">Accept pipeline input?</span></span> |<span data-ttu-id="24618-192">False</span><span class="sxs-lookup"><span data-stu-id="24618-192">false</span></span> |
| <span data-ttu-id="24618-193">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-193">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-194">False</span><span class="sxs-lookup"><span data-stu-id="24618-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="24618-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="24618-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="24618-196">TRUE ise, yazdırma iletilerden hello betik toohello akış çıkışı.</span><span class="sxs-lookup"><span data-stu-id="24618-196">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="24618-197">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="24618-197">Aliases</span></span> | <span data-ttu-id="24618-198">Yok</span><span class="sxs-lookup"><span data-stu-id="24618-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="24618-199">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="24618-199">Required?</span></span> |<span data-ttu-id="24618-200">False</span><span class="sxs-lookup"><span data-stu-id="24618-200">false</span></span> |
| <span data-ttu-id="24618-201">Konumu</span><span class="sxs-lookup"><span data-stu-id="24618-201">Position</span></span> |<span data-ttu-id="24618-202">Adlı</span><span class="sxs-lookup"><span data-stu-id="24618-202">named</span></span> |
| <span data-ttu-id="24618-203">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="24618-203">Default value</span></span> |<span data-ttu-id="24618-204">False</span><span class="sxs-lookup"><span data-stu-id="24618-204">false</span></span> |
| <span data-ttu-id="24618-205">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-205">Accept pipeline input?</span></span> |<span data-ttu-id="24618-206">False</span><span class="sxs-lookup"><span data-stu-id="24618-206">false</span></span> |
| <span data-ttu-id="24618-207">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="24618-207">Accept wildcard characters?</span></span> |<span data-ttu-id="24618-208">False</span><span class="sxs-lookup"><span data-stu-id="24618-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="24618-209">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="24618-209">Remarks</span></span>
<span data-ttu-id="24618-210">Nasıl toouse hello betik toocreate geliştirme ve Test ortamları için bkz. bir tam açıklama için [Windows PowerShell komut dosyalarını kullanarak tooPublish tooDev ve Test ortamları](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="24618-210">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="24618-211">Merhaba JSON yapılandırma dosyası dağıtılan toobe nedir hello ayrıntılarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="24618-211">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="24618-212">Merhaba adı, benzeşim grubu, VHD görüntüsü ve hello sanal makinesinin boyutu gibi hello proje oluşturduğunuzda, belirttiğiniz hello bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="24618-212">It includes hello information that you specified when you created hello project, such as hello name, affinity group, VHD image, and size of hello virtual machine.</span></span> <span data-ttu-id="24618-213">Ayrıca hello sanal makinedeki hello veritabanları tooprovision hello uç noktaları varsa ve dağıtım parametreleri web.</span><span class="sxs-lookup"><span data-stu-id="24618-213">It also includes hello endpoints on hello virtual machine, hello databases tooprovision, if any, and web deployment parameters.</span></span> <span data-ttu-id="24618-214">koddan hello örnek bir JSON yapılandırma dosyası gösterir:</span><span class="sxs-lookup"><span data-stu-id="24618-214">hello following code shows an example JSON configuration file:</span></span>

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="24618-215">Merhaba JSON yapılandırma dosyası toochange ne sağlandığında düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24618-215">You can edit hello JSON configuration file toochange what is provisioned.</span></span> <span data-ttu-id="24618-216">Bir sanal makine ve bulut hizmeti gerekiyor, ancak hello veritabanı bölümü isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="24618-216">A virtual machine and a cloud service are required, but hello database section is optional.</span></span>

