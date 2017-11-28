---
title: "aaaPublish WebApplicationWebSite (Windows PowerShell komut dosyası) | Microsoft Docs"
description: "Nasıl toopublish bir web projesi tooan Azure Web sitesi öğrenin. Bu komut dosyası yoksa hello gerekli kaynakları Azure aboneliğinizde oluşturur."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a><span data-ttu-id="155f0-104">Yayımlama WebApplicationWebSite (Windows PowerShell komut dosyası)</span><span class="sxs-lookup"><span data-stu-id="155f0-104">Publish-WebApplicationWebSite (Windows PowerShell script)</span></span>
## <a name="syntax"></a><span data-ttu-id="155f0-105">Sözdizimi</span><span class="sxs-lookup"><span data-stu-id="155f0-105">Syntax</span></span>
<span data-ttu-id="155f0-106">Bir web projesi tooan Azure Web sitesi yayımlar.</span><span class="sxs-lookup"><span data-stu-id="155f0-106">Publishes a web project tooan Azure website.</span></span> <span data-ttu-id="155f0-107">yoksa hello komut dosyası Azure aboneliğinizde hello gerekli kaynakları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="155f0-107">hello script creates hello required resources in your Azure subscription if they don't exist.</span></span>

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a><span data-ttu-id="155f0-108">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="155f0-108">Configuration</span></span>
<span data-ttu-id="155f0-109">Merhaba dağıtımın hello ayrıntılarını açıklayan hello yolu toohello JSON yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="155f0-109">hello path toohello JSON configuration file that describes hello details of hello deployment.</span></span>

| <span data-ttu-id="155f0-110">Parametre</span><span class="sxs-lookup"><span data-stu-id="155f0-110">Parameter</span></span> | <span data-ttu-id="155f0-111">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-111">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="155f0-112">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="155f0-112">Aliases</span></span> |<span data-ttu-id="155f0-113">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-113">none</span></span> |
| <span data-ttu-id="155f0-114">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-114">Required?</span></span> |<span data-ttu-id="155f0-115">TRUE</span><span class="sxs-lookup"><span data-stu-id="155f0-115">true</span></span> |
| <span data-ttu-id="155f0-116">Konumu</span><span class="sxs-lookup"><span data-stu-id="155f0-116">Position</span></span> |<span data-ttu-id="155f0-117">Adlı</span><span class="sxs-lookup"><span data-stu-id="155f0-117">named</span></span> |
| <span data-ttu-id="155f0-118">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-118">Default value</span></span> |<span data-ttu-id="155f0-119">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-119">none</span></span> |
| <span data-ttu-id="155f0-120">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-120">Accept pipeline input?</span></span> |<span data-ttu-id="155f0-121">False</span><span class="sxs-lookup"><span data-stu-id="155f0-121">false</span></span> |
| <span data-ttu-id="155f0-122">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-122">Accept wildcard characters?</span></span> |<span data-ttu-id="155f0-123">False</span><span class="sxs-lookup"><span data-stu-id="155f0-123">false</span></span> |

## <a name="subscriptionname"></a><span data-ttu-id="155f0-124">varlığıyla subscriptionName</span><span class="sxs-lookup"><span data-stu-id="155f0-124">SubscriptionName</span></span>
<span data-ttu-id="155f0-125">Merhaba toocreate hello Web sitesi istediğiniz Azure aboneliği Hello adı.</span><span class="sxs-lookup"><span data-stu-id="155f0-125">hello name of hello Azure subscription that you want toocreate hello website in.</span></span>

| <span data-ttu-id="155f0-126">Parametre</span><span class="sxs-lookup"><span data-stu-id="155f0-126">Parameter</span></span> | <span data-ttu-id="155f0-127">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-127">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="155f0-128">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="155f0-128">Aliases</span></span> |<span data-ttu-id="155f0-129">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-129">none</span></span> |
| <span data-ttu-id="155f0-130">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-130">Required?</span></span> |<span data-ttu-id="155f0-131">False</span><span class="sxs-lookup"><span data-stu-id="155f0-131">false</span></span> |
| <span data-ttu-id="155f0-132">Konumu</span><span class="sxs-lookup"><span data-stu-id="155f0-132">Position</span></span> |<span data-ttu-id="155f0-133">Adlı</span><span class="sxs-lookup"><span data-stu-id="155f0-133">named</span></span> |
| <span data-ttu-id="155f0-134">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-134">Default value</span></span> |<span data-ttu-id="155f0-135">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-135">none</span></span> |
| <span data-ttu-id="155f0-136">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-136">Accept pipeline input?</span></span> |<span data-ttu-id="155f0-137">False</span><span class="sxs-lookup"><span data-stu-id="155f0-137">false</span></span> |
| <span data-ttu-id="155f0-138">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-138">Accept wildcard characters?</span></span> |<span data-ttu-id="155f0-139">False</span><span class="sxs-lookup"><span data-stu-id="155f0-139">false</span></span> |

## <a name="webdeploypackage"></a><span data-ttu-id="155f0-140">WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="155f0-140">WebDeployPackage</span></span>
<span data-ttu-id="155f0-141">Merhaba yolu toohello web dağıtım paketi toopublish toohello Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="155f0-141">hello path toohello web deployment package toopublish toohello website.</span></span> <span data-ttu-id="155f0-142">Visual Studio'da hello Web Yayımlama Sihirbazı'nı kullanarak bu paketi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="155f0-142">You can create this package by using hello Publish Web wizard in Visual Studio.</span></span> <span data-ttu-id="155f0-143">Daha fazla bilgi için bkz: [Azure Cloud Services ve ASP.NET kullanmaya başlama](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span><span class="sxs-lookup"><span data-stu-id="155f0-143">For more information, see [Get started with Azure Cloud Services and ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).</span></span>

| <span data-ttu-id="155f0-144">Parametre</span><span class="sxs-lookup"><span data-stu-id="155f0-144">Parameter</span></span> | <span data-ttu-id="155f0-145">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-145">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="155f0-146">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="155f0-146">Aliases</span></span> |<span data-ttu-id="155f0-147">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-147">none</span></span> |
| <span data-ttu-id="155f0-148">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-148">Required?</span></span> |<span data-ttu-id="155f0-149">False</span><span class="sxs-lookup"><span data-stu-id="155f0-149">false</span></span> |
| <span data-ttu-id="155f0-150">Konumu</span><span class="sxs-lookup"><span data-stu-id="155f0-150">Position</span></span> |<span data-ttu-id="155f0-151">Adlı</span><span class="sxs-lookup"><span data-stu-id="155f0-151">named</span></span> |
| <span data-ttu-id="155f0-152">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-152">Default value</span></span> |<span data-ttu-id="155f0-153">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-153">none</span></span> |
| <span data-ttu-id="155f0-154">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-154">Accept pipeline input?</span></span> |<span data-ttu-id="155f0-155">False</span><span class="sxs-lookup"><span data-stu-id="155f0-155">false</span></span> |
| <span data-ttu-id="155f0-156">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-156">Accept wildcard characters?</span></span> |<span data-ttu-id="155f0-157">False</span><span class="sxs-lookup"><span data-stu-id="155f0-157">false</span></span> |

## <a name="databaseserverpassword"></a><span data-ttu-id="155f0-158">DatabaseServerPassword</span><span class="sxs-lookup"><span data-stu-id="155f0-158">DatabaseServerPassword</span></span>
<span data-ttu-id="155f0-159">Merhaba kullanıcı adı ve parola hello Azure SQL veritabanı için.</span><span class="sxs-lookup"><span data-stu-id="155f0-159">hello username and password for hello SQL database in Azure.</span></span>

| <span data-ttu-id="155f0-160">Parametre</span><span class="sxs-lookup"><span data-stu-id="155f0-160">Parameter</span></span> | <span data-ttu-id="155f0-161">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-161">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="155f0-162">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="155f0-162">Aliases</span></span> |<span data-ttu-id="155f0-163">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-163">none</span></span> |
| <span data-ttu-id="155f0-164">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-164">Required?</span></span> |<span data-ttu-id="155f0-165">False</span><span class="sxs-lookup"><span data-stu-id="155f0-165">false</span></span> |
| <span data-ttu-id="155f0-166">Konumu</span><span class="sxs-lookup"><span data-stu-id="155f0-166">Position</span></span> |<span data-ttu-id="155f0-167">Adlı</span><span class="sxs-lookup"><span data-stu-id="155f0-167">named</span></span> |
| <span data-ttu-id="155f0-168">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-168">Default value</span></span> |<span data-ttu-id="155f0-169">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-169">none</span></span> |
| <span data-ttu-id="155f0-170">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-170">Accept pipeline input?</span></span> |<span data-ttu-id="155f0-171">False</span><span class="sxs-lookup"><span data-stu-id="155f0-171">false</span></span> |
| <span data-ttu-id="155f0-172">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-172">Accept wildcard characters?</span></span> |<span data-ttu-id="155f0-173">False</span><span class="sxs-lookup"><span data-stu-id="155f0-173">false</span></span> |

## <a name="sendhostmessagestooutput"></a><span data-ttu-id="155f0-174">SendHostMessagesToOutput</span><span class="sxs-lookup"><span data-stu-id="155f0-174">SendHostMessagesToOutput</span></span>
<span data-ttu-id="155f0-175">TRUE ise, yazdırma iletilerden hello betik toohello akış çıkışı.</span><span class="sxs-lookup"><span data-stu-id="155f0-175">If true, print messages from hello script toohello output stream.</span></span>

| <span data-ttu-id="155f0-176">Parametre</span><span class="sxs-lookup"><span data-stu-id="155f0-176">Parameter</span></span> | <span data-ttu-id="155f0-177">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-177">Default value</span></span> |
| --- | --- |
| <span data-ttu-id="155f0-178">Diğer adlar</span><span class="sxs-lookup"><span data-stu-id="155f0-178">Aliases</span></span> |<span data-ttu-id="155f0-179">Yok</span><span class="sxs-lookup"><span data-stu-id="155f0-179">none</span></span> |
| <span data-ttu-id="155f0-180">Gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-180">Required?</span></span> |<span data-ttu-id="155f0-181">False</span><span class="sxs-lookup"><span data-stu-id="155f0-181">false</span></span> |
| <span data-ttu-id="155f0-182">Konumu</span><span class="sxs-lookup"><span data-stu-id="155f0-182">Position</span></span> |<span data-ttu-id="155f0-183">Adlı</span><span class="sxs-lookup"><span data-stu-id="155f0-183">named</span></span> |
| <span data-ttu-id="155f0-184">Varsayılan değer</span><span class="sxs-lookup"><span data-stu-id="155f0-184">Default value</span></span> |<span data-ttu-id="155f0-185">False</span><span class="sxs-lookup"><span data-stu-id="155f0-185">false</span></span> |
| <span data-ttu-id="155f0-186">Ardışık Düzen giriş kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-186">Accept pipeline input?</span></span> |<span data-ttu-id="155f0-187">False</span><span class="sxs-lookup"><span data-stu-id="155f0-187">false</span></span> |
| <span data-ttu-id="155f0-188">Joker karakterler kabul edilsin mi?</span><span class="sxs-lookup"><span data-stu-id="155f0-188">Accept wildcard characters?</span></span> |<span data-ttu-id="155f0-189">False</span><span class="sxs-lookup"><span data-stu-id="155f0-189">false</span></span> |

## <a name="remarks"></a><span data-ttu-id="155f0-190">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="155f0-190">Remarks</span></span>
<span data-ttu-id="155f0-191">Nasıl toouse hello betik toocreate geliştirme ve Test ortamları için bkz. bir tam açıklama için [Windows PowerShell komut dosyalarını kullanarak tooPublish tooDev ve Test ortamları](vs-azure-tools-publishing-using-powershell-scripts.md).</span><span class="sxs-lookup"><span data-stu-id="155f0-191">For a complete explanation of how toouse hello script toocreate Dev and Test environments, see [Using Windows PowerShell Scripts tooPublish tooDev and Test Environments](vs-azure-tools-publishing-using-powershell-scripts.md).</span></span>

<span data-ttu-id="155f0-192">Merhaba JSON yapılandırma dosyası dağıtılan toobe nedir hello ayrıntılarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="155f0-192">hello JSON configuration file specifies hello details of what is toobe deployed.</span></span> <span data-ttu-id="155f0-193">Merhaba adı ve hello Web sitesi için kullanıcı adı gibi hello proje oluşturduğunuzda, belirttiğiniz hello bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="155f0-193">It includes hello information that you specified when you created hello project, such as hello name and username for hello website.</span></span> <span data-ttu-id="155f0-194">Ayrıca hello veritabanı tooprovision varsa içerir.</span><span class="sxs-lookup"><span data-stu-id="155f0-194">It also includes hello database tooprovision, if any.</span></span> <span data-ttu-id="155f0-195">koddan hello örnek bir JSON yapılandırma dosyası gösterir:</span><span class="sxs-lookup"><span data-stu-id="155f0-195">hello following code shows an example JSON configuration file:</span></span>

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

<span data-ttu-id="155f0-196">Ne dağıtılan hello JSON yapılandırma dosyası toochange düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="155f0-196">You can edit hello JSON configuration file toochange what is deployed.</span></span> <span data-ttu-id="155f0-197">Bir Web Bölümü gereklidir, ancak hello veritabanı bölümü isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="155f0-197">A webSite section is required, but hello database section is optional.</span></span>

## <a name="next-steps"></a><span data-ttu-id="155f0-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="155f0-198">Next steps</span></span>
<span data-ttu-id="155f0-199">Daha fazla bilgi için bkz: [Yayımla-WebApplicationVM (Windows PowerShell komut dosyası)](vs-azure-tools-publish-webapplicationvm.md)</span><span class="sxs-lookup"><span data-stu-id="155f0-199">For more information, see [Publish-WebApplicationVM (Windows PowerShell script)](vs-azure-tools-publish-webapplicationvm.md)</span></span>

