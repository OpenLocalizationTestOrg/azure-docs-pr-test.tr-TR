---
title: "Yayımlama WebApplicationVM | Microsoft Docs"
description: "Bir sanal makine bir web uygulamasına dağıtmayı öğrenin. Bu komut dosyası yoksa gerekli kaynakları Azure aboneliğinizde oluşturur."
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
ms.openlocfilehash: 2738fc1dff50a177a227ae2c7719bd9a192d82ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a><span data-ttu-id="f3ce5-104">Yayımlama WebApplicationVM (Windows PowerShell komut dosyası)</span><span class="sxs-lookup"><span data-stu-id="f3ce5-104">Publish-WebApplicationVM (Windows PowerShell script)</span></span>
<span data-ttu-id="f3ce5-105">Bir sanal makine bir web uygulamasına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-105">Deploys a web application to a virtual machine.</span></span> <span data-ttu-id="f3ce5-106">Komut dosyası yoksa gerekli kaynakları Azure aboneliğinizde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-106">The script creates the required resources in your Azure subscription if they don't exist.</span></span>

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

### <a name="configuration"></a><span data-ttu-id="f3ce5-107">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f3ce5-107">Configuration</span></span>
<span data-ttu-id="f3ce5-108">Dağıtım ayrıntılarını açıklayan JSON yapılandırma dosyasının yolu.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-108">The path to the JSON configuration file that describes the details of the deployment.</span></span>

| <span data-ttu-id="f3ce5-109">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-109">Aliases</span></span> | <span data-ttu-id="f3ce5-110">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-110">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-111">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-111">Required?</span></span> |<span data-ttu-id="f3ce5-112">TRUE</span><span class="sxs-lookup"><span data-stu-id="f3ce5-112">true</span></span> |
| <span data-ttu-id="f3ce5-113">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-113">Position</span></span> |<span data-ttu-id="f3ce5-114">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-114">named</span></span> |
| <span data-ttu-id="f3ce5-115">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-115">Default value</span></span> |<span data-ttu-id="f3ce5-116">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-116">none</span></span> |
| <span data-ttu-id="f3ce5-117">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-117">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-118">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-118">false</span></span> |
| <span data-ttu-id="f3ce5-119">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-119">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-120">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-120">false</span></span> |

### <a name="subscriptionname"></a><span data-ttu-id="f3ce5-121">varlığıyla subscriptionName</span><span class="sxs-lookup"><span data-stu-id="f3ce5-121">SubscriptionName</span></span>
<span data-ttu-id="f3ce5-122">Sanal makineyi oluşturmak istediğiniz Azure aboneliği adı.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-122">The name of the Azure subscription in which you want to create the virtual machine.</span></span>

| <span data-ttu-id="f3ce5-123">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-123">Aliases</span></span> | <span data-ttu-id="f3ce5-124">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-124">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-125">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-125">Required?</span></span> |<span data-ttu-id="f3ce5-126">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-126">false</span></span> |
| <span data-ttu-id="f3ce5-127">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-127">Position</span></span> |<span data-ttu-id="f3ce5-128">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-128">named</span></span> |
| <span data-ttu-id="f3ce5-129">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-129">Default value</span></span> |<span data-ttu-id="f3ce5-130">İlk aboneliğe abonelik dosyasındaki kullanır</span><span class="sxs-lookup"><span data-stu-id="f3ce5-130">Uses the first subscription in the subscription file</span></span> |
| <span data-ttu-id="f3ce5-131">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-131">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-132">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-132">false</span></span> |
| <span data-ttu-id="f3ce5-133">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-133">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-134">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-134">false</span></span> |

### <a name="webdeploypackage"></a><span data-ttu-id="f3ce5-135">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="f3ce5-135">WebDeployPackage</span></span>
<span data-ttu-id="f3ce5-136">Sanal makineye yayımlamak için web dağıtım paketi yolu.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-136">The path to the web deployment package to publish to the virtual machine.</span></span> <span data-ttu-id="f3ce5-137">Visual Studio'da Web'i Yayımla Sihirbazı'nı kullanarak bu paketi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-137">You can create this package by using the Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="f3ce5-138">Bkz: [nasıl yapılır: Visual Studio'da bir Web dağıtım paketi oluşturma](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="f3ce5-138">See [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span>

| <span data-ttu-id="f3ce5-139">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-139">Aliases</span></span> | <span data-ttu-id="f3ce5-140">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-140">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-141">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-141">Required?</span></span> |<span data-ttu-id="f3ce5-142">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-142">false</span></span> |
| <span data-ttu-id="f3ce5-143">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-143">Position</span></span> |<span data-ttu-id="f3ce5-144">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-144">named</span></span> |
| <span data-ttu-id="f3ce5-145">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-145">Default value</span></span> |<span data-ttu-id="f3ce5-146">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-146">none</span></span> |
| <span data-ttu-id="f3ce5-147">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-147">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-148">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-148">false</span></span> |
| <span data-ttu-id="f3ce5-149">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-149">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-150">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-150">false</span></span> |

### <a name="allowuntrusted"></a><span data-ttu-id="f3ce5-151">AllowUntrusted</span><span class="sxs-lookup"><span data-stu-id="f3ce5-151">AllowUntrusted</span></span>
<span data-ttu-id="f3ce5-152">TRUE ise, bir güvenilen kök yetkilisi tarafından imzalanmadığını sertifikaların kullanılmasına izin verin.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-152">If true, allow the use of certificates that aren't signed by a trusted root authority.</span></span>

| <span data-ttu-id="f3ce5-153">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-153">Aliases</span></span> | <span data-ttu-id="f3ce5-154">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-154">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-155">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-155">Required?</span></span> |<span data-ttu-id="f3ce5-156">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-156">false</span></span> |
| <span data-ttu-id="f3ce5-157">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-157">Position</span></span> |<span data-ttu-id="f3ce5-158">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-158">named</span></span> |
| <span data-ttu-id="f3ce5-159">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-159">Default value</span></span> |<span data-ttu-id="f3ce5-160">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-160">false</span></span> |
| <span data-ttu-id="f3ce5-161">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-161">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-162">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-162">false</span></span> |
| <span data-ttu-id="f3ce5-163">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-163">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-164">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-164">false</span></span> |

### <a name="vmpassword"></a><span data-ttu-id="f3ce5-165">VMPassword</span><span class="sxs-lookup"><span data-stu-id="f3ce5-165">VMPassword</span></span>
<span data-ttu-id="f3ce5-166">Sanal makine hesabı için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-166">The credentials for the virtual machine account.</span></span> <span data-ttu-id="f3ce5-167">Örnek: - VMPassword @{Name = "Yönetici"; Parola = "parola"}</span><span class="sxs-lookup"><span data-stu-id="f3ce5-167">Example: -VMPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="f3ce5-168">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-168">Aliases</span></span> | <span data-ttu-id="f3ce5-169">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-169">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-170">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-170">Required?</span></span> |<span data-ttu-id="f3ce5-171">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-171">false</span></span> |
| <span data-ttu-id="f3ce5-172">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-172">Position</span></span> |<span data-ttu-id="f3ce5-173">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-173">named</span></span> |
| <span data-ttu-id="f3ce5-174">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-174">Default value</span></span> |<span data-ttu-id="f3ce5-175">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-175">none</span></span> |
| <span data-ttu-id="f3ce5-176">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-176">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-177">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-177">false</span></span> |
| <span data-ttu-id="f3ce5-178">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-178">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-179">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-179">false</span></span> |

### <a name="databaseserverpassword"></a><span data-ttu-id="f3ce5-180">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="f3ce5-180">DatabaseServerPassword</span></span>
<span data-ttu-id="f3ce5-181">Azure SQL veritabanı için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-181">The credentials for the SQL database in Azure.</span></span> <span data-ttu-id="f3ce5-182">Örnek: - DatabaseServerPassword @{Name = "Yönetici"; Parola = "parola"}</span><span class="sxs-lookup"><span data-stu-id="f3ce5-182">Example: -DatabaseServerPassword @{Name = "admin"; Password = "password"}</span></span>

| <span data-ttu-id="f3ce5-183">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-183">Aliases</span></span> | <span data-ttu-id="f3ce5-184">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-184">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-185">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-185">Required?</span></span> |<span data-ttu-id="f3ce5-186">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-186">false</span></span> |
| <span data-ttu-id="f3ce5-187">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-187">Position</span></span> |<span data-ttu-id="f3ce5-188">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-188">named</span></span> |
| <span data-ttu-id="f3ce5-189">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-189">Default value</span></span> |<span data-ttu-id="f3ce5-190">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-190">none</span></span> |
| <span data-ttu-id="f3ce5-191">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-191">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-192">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-192">false</span></span> |
| <span data-ttu-id="f3ce5-193">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-193">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-194">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-194">false</span></span> |

### <a name="sendhostmessagestooutput"></a><span data-ttu-id="f3ce5-195">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="f3ce5-195">SendHostMessagesToOutput</span></span>
<span data-ttu-id="f3ce5-196">TRUE ise, yazdırma betikten çıkış akışına iletileri.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-196">If true, print messages from the script to the output stream.</span></span>

| <span data-ttu-id="f3ce5-197">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-197">Aliases</span></span> | <span data-ttu-id="f3ce5-198">Yok</span><span class="sxs-lookup"><span data-stu-id="f3ce5-198">none</span></span> |
| --- | --- |
| <span data-ttu-id="f3ce5-199">Gerekli?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-199">Required?</span></span> |<span data-ttu-id="f3ce5-200">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-200">false</span></span> |
| <span data-ttu-id="f3ce5-201">Konumu</span><span class="sxs-lookup"><span data-stu-id="f3ce5-201">Position</span></span> |<span data-ttu-id="f3ce5-202">Adlı</span><span class="sxs-lookup"><span data-stu-id="f3ce5-202">named</span></span> |
| <span data-ttu-id="f3ce5-203">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="f3ce5-203">Default value</span></span> |<span data-ttu-id="f3ce5-204">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-204">false</span></span> |
| <span data-ttu-id="f3ce5-205">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-205">Accept pipeline input?</span></span> |<span data-ttu-id="f3ce5-206">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-206">false</span></span> |
| <span data-ttu-id="f3ce5-207">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="f3ce5-207">Accept wildcard characters?</span></span> |<span data-ttu-id="f3ce5-208">False</span><span class="sxs-lookup"><span data-stu-id="f3ce5-208">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="f3ce5-209">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="f3ce5-209">Remarks</span></span>
<span data-ttu-id="f3ce5-210">Geliştirme ve Test ortamları, komut dosyası oluşturmak için nasıl kullanılacağını tam bir açıklaması için bkz: [geliştirme ve Test ortamları için yayımlamak için Windows PowerShell betiklerini kullanarak](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="f3ce5-210">For a complete explanation of how to use the script to create Dev and Test environments, see [Using Windows PowerShell Scripts to Publish to Dev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="f3ce5-211">JSON yapılandırma dosyası dağıtılacak nedir ayrıntılarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-211">The JSON configuration file specifies the details of what is to be deployed.</span></span> <span data-ttu-id="f3ce5-212">Ad, benzeşim grubu, VHD görüntüsü ve boyutunu sanal makine gibi bir proje oluşturduğunuzda, belirttiğiniz bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-212">It includes the information that you specified when you created the project, such as the name, affinity group, VHD image, and size of the virtual machine.</span></span> <span data-ttu-id="f3ce5-213">Ayrıca sanal makinede sağlamak için veritabanlarını uç noktaları varsa ve dağıtım parametreleri web.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-213">It also includes the endpoints on the virtual machine, the databases to provision, if any, and web deployment parameters.</span></span> <span data-ttu-id="f3ce5-214">Aşağıdaki kod örnek bir JSON yapılandırma dosyası gösterir:</span><span class="sxs-lookup"><span data-stu-id="f3ce5-214">The following code shows an example JSON configuration file:</span></span>

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

<span data-ttu-id="f3ce5-215">Ne sağlandığında değiştirmek için JSON yapılandırma dosyasını düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-215">You can edit the JSON configuration file to change what is provisioned.</span></span> <span data-ttu-id="f3ce5-216">Bir sanal makine ve bulut hizmeti gerekiyor, ancak veritabanı bölümü isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f3ce5-216">A virtual machine and a cloud service are required, but the database section is optional.</span></span>

