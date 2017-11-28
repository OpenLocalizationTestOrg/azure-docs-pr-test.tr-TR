---
title: "aaaInstall şirket içi veri ağ geçidi | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve bir şirket içi veri ağ geçidi yapılandırın."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="dd35b-103">Yükleme ve bir şirket içi veri ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="dd35b-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="dd35b-104">Bir veya daha fazla Azure Analysis Services sunucuları aynı hello olduğunda bir şirket içi veri ağ geçidi gereklidir bölge tooon içi veri kaynaklarına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="dd35b-105">toolearn hello ağ geçidi hakkında daha fazla bilgi görmek [şirket içi veri ağ geçidi](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="dd35b-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd35b-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dd35b-106">Prerequisites</span></span>
<span data-ttu-id="dd35b-107">**En düşük gereksinimler:**</span><span class="sxs-lookup"><span data-stu-id="dd35b-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="dd35b-108">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="dd35b-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="dd35b-109">64 bit sürümü Windows 7 / Windows Server 2008 R2 (veya üstü)</span><span class="sxs-lookup"><span data-stu-id="dd35b-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="dd35b-110">**Önerilen:**</span><span class="sxs-lookup"><span data-stu-id="dd35b-110">**Recommended:**</span></span>

* <span data-ttu-id="dd35b-111">8 çekirdekli CPU</span><span class="sxs-lookup"><span data-stu-id="dd35b-111">8 Core CPU</span></span>
* <span data-ttu-id="dd35b-112">8 GB bellek</span><span class="sxs-lookup"><span data-stu-id="dd35b-112">8 GB Memory</span></span>
* <span data-ttu-id="dd35b-113">64 bit sürümü Windows 2012 R2'in (veya üstü)</span><span class="sxs-lookup"><span data-stu-id="dd35b-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="dd35b-114">**Önemli noktalar:**</span><span class="sxs-lookup"><span data-stu-id="dd35b-114">**Important considerations:**</span></span>

* <span data-ttu-id="dd35b-115">Ağ geçidiniz Azure ile kaydedilirken Kurulum sırasında hello varsayılan bölge aboneliğiniz için seçilir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="dd35b-116">Farklı bir bölgeye seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd35b-116">You can choose a different region.</span></span> <span data-ttu-id="dd35b-117">Birden çok bölgede sunucularınız varsa, her bölge için bir ağ geçidi yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="dd35b-118">Merhaba ağ geçidi etki alanı denetleyicisine yüklenemez.</span><span class="sxs-lookup"><span data-stu-id="dd35b-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="dd35b-119">Yalnızca bir ağ geçidi tek bir bilgisayara yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="dd35b-120">Merhaba ağ geçidi üzerinde kalır ve toosleep geçmez bir bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="dd35b-121">Merhaba ağ geçidi, bir bilgisayar kablosuz olarak bağlı tooyour ağda yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="dd35b-122">Performans yayınladıklarını.</span><span class="sxs-lookup"><span data-stu-id="dd35b-122">Performance can be diminished.</span></span>


## <span data-ttu-id="dd35b-123"><a name="download"></a>İndirme</span><span class="sxs-lookup"><span data-stu-id="dd35b-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="dd35b-124">Merhaba ağ geçidini indirin</span><span class="sxs-lookup"><span data-stu-id="dd35b-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="dd35b-125"><a name="install"></a>Yükleme</span><span class="sxs-lookup"><span data-stu-id="dd35b-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="dd35b-126">Kur'u yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-126">Run setup.</span></span>

2. <span data-ttu-id="dd35b-127">Bir konum seçin, hello koşullarını kabul edin ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Konum ve Lisans Koşulları'nı yükleme](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="dd35b-129">Seçin **şirket içi veri ağ geçidi (önerilen)**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="dd35b-130">Azure Analysis Services kişisel modunu desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="dd35b-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Ağ geçidi türünü seçin](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="dd35b-132">Bir hesap toosign tooAzure girin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="dd35b-133">Merhaba hesabı kiracınıza ait Azure Active Directory'de olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="dd35b-134">Bu hesap hello Ağ Geçidi Yöneticisi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-134">This account is used for hello gateway administrator.</span></span> 

   ![Bir hesap toosign tooAzure içinde girin](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="dd35b-136">Bir etki alanı hesabıyla oturum açın, olacaktır Azure AD'de tooyour kuruluş hesabıyla eşlenir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="dd35b-137">Kuruluş hesabınızla hello hello Ağ Geçidi Yöneticisi olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="dd35b-138"><a name="register"></a>Kaydetme</span><span class="sxs-lookup"><span data-stu-id="dd35b-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="dd35b-139">Sipariş toocreate Azure bir ağ geçidi kaynağı'da, ağ geçidi bulut Hizmeti'ne hello ile yüklü hello yerel örneği kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="dd35b-140">Seçin **bu bilgisayarda yeni bir ağ geçidini kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-140">Select **Register a new gateway on this computer**.</span></span>

    ![Kaydolma](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="dd35b-142">Ağ geçidiniz için bir ad ve kurtarma anahtarı yazın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="dd35b-143">Varsayılan olarak, aboneliğiniz varsayılan bölge hello ağ geçidi kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="dd35b-144">Tooselect farklı bir bölgeye gereksinim duyarsanız, seçin **değişikliğin bölgesini**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![Kaydolma](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="dd35b-146"><a name="create-resource"></a>Bir Azure ağ geçidi kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd35b-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="dd35b-147">Yüklenen ve ağ geçidiniz kaydedilen sonra Azure aboneliğinizde toocreate bir ağ geçidi kaynağı gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="dd35b-148">TooAzure hello ile aynı oturum açma hello ağ geçidi kaydederken kullanılan hesap.</span><span class="sxs-lookup"><span data-stu-id="dd35b-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="dd35b-149">Azure portalında tıklatın **yeni bir hizmet Oluştur** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi**  >   **Oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Bir ağ geçidi kaynağı oluşturun](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="dd35b-151">İçinde **oluşturma bağlantı ağ geçidi**, bu ayarları girin:</span><span class="sxs-lookup"><span data-stu-id="dd35b-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="dd35b-152">**Ad**: ağ geçidi kaynağı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="dd35b-153">**Abonelik**: seçin, ağ geçidi kaynağı ile Azure aboneliği tooassociate hello.</span><span class="sxs-lookup"><span data-stu-id="dd35b-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="dd35b-154">Bu abonelik olmalıdır hello sunucularıdır içinde aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="dd35b-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="dd35b-155">Merhaba varsayılan abonelik hello toosign içinde kullanılan Azure hesabı temel alır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="dd35b-156">**Kaynak grubu**: Kaynak grubu oluşturun veya mevcut bir kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="dd35b-157">**Konum**: Select hello bölge, ağ geçidi kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="dd35b-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="dd35b-158">**Yükleme adı**: ağ geçidi yüklemenizi seçili değilse, select hello ağ geçidi kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="dd35b-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="dd35b-159">İşiniz bittiğinde tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="dd35b-160"><a name="connect-servers"></a>Sunucuları toohello ağ geçidi kaynağına bağlanma</span><span class="sxs-lookup"><span data-stu-id="dd35b-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="dd35b-161">Azure Analysis Services sunucusu genel bakışta tıklatın **şirket içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Sunucu toogateway Bağlan](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="dd35b-163">İçinde **bir şirket içi veri ağ geçidi tooconnect çekme**, ağ geçidi kaynağı seçin ve ardından **Bağlan seçilen ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Sunucu toogateway kaynak Bağlan](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="dd35b-165">Ağ geçidiniz hello listede görünmüyorsa, sunucusu olası değil hello hello ağ geçidi kaydedilirken belirtilen hello bölge ile aynı bölgeye.</span><span class="sxs-lookup"><span data-stu-id="dd35b-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="dd35b-166">Bu kadar.</span><span class="sxs-lookup"><span data-stu-id="dd35b-166">That's it.</span></span> <span data-ttu-id="dd35b-167">Tooopen bağlantı noktaları gerekir ya da sorun giderme yapın, çıkışı emin toocheck olması [şirket içi veri ağ geçidi](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="dd35b-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd35b-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd35b-168">Next steps</span></span>
* [<span data-ttu-id="dd35b-169">Çözümleme Hizmetleri yönetme</span><span class="sxs-lookup"><span data-stu-id="dd35b-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="dd35b-170">Azure Analysis Services Veri Al</span><span class="sxs-lookup"><span data-stu-id="dd35b-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
