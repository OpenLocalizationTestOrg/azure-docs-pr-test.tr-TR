---
title: "Olay hub'ları kullanarak Azure anahtar kasası günlükleri aaaIntegrate | Microsoft Docs"
description: "Merhaba gerekli adımları toomake anahtar kasası sağlar Öğreticisi, Azure günlük tümleştirmeyi kullanarak kullanılabilir tooa SIEM günlüğe kaydeder"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="44eb3-103">Azure günlük tümleştirme Öğreticisi: olay hub'ları kullanarak işlem Azure anahtar kasası olayları</span><span class="sxs-lookup"><span data-stu-id="44eb3-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="44eb3-104">Azure günlük tümleştirme oturum tooretrieve olayları kullanın ve bunları kullanılabilir tooyour güvenlik bilgileri ve Olay yönetimi (SIEM) sistemi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="44eb3-105">Bu öğreticide Azure günlük tümleştirme aracılığıyla Azure Event Hubs alınan kullanılan tooprocess günlüklerini nasıl olabilir bir örnek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="44eb3-106">Bu öğretici tooget nasıl birlikte izleyerek Azure günlük tümleştirme ve Event Hubs iş hello ile örnek adımlar TechNet'in ve her adımın hello çözümü nasıl destekler? anlama kullanın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="44eb3-107">Neler yapabileceğiniz sonra kendi adımları toosupport toocreate burada öğrendiniz, şirketinizin benzersiz gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="44eb3-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="44eb3-108">Merhaba adımları ve Bu öğreticide komutları kopyalanır ve yapıştırılan hedeflenen toobe değildir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="44eb3-109">Bunlar yalnızca örnek demektir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-109">They're examples only.</span></span> <span data-ttu-id="44eb3-110">"Olduğu gibi" Merhaba PowerShell komutlarını Canlı ortamınızda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="44eb3-111">Bunları benzersiz ortamınıza bağlı özelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="44eb3-112">Bu öğreticide, Azure anahtar kasası etkinlik oturum tooan olay hub'ı almak ve JSON dosyaları tooyour SIEM sistem olarak kullanılabilir hale getirme hello işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="44eb3-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="44eb3-113">Ardından, SIEM sistem tooprocess hello JSON dosyalarınızın yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="44eb3-114">Bu öğreticideki adımlardan hello çoğu anahtar kasalarını, depolama hesapları ve olay hub'ları yapılandırma içerir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="44eb3-115">Merhaba belirli Azure günlük tümleştirme hello Bu öğreticinin sonunda adımlardır.</span><span class="sxs-lookup"><span data-stu-id="44eb3-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="44eb3-116">Bu adımları bir üretim ortamında gerçekleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="44eb3-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="44eb3-117">Bunlar yalnızca bir laboratuvar ortamı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="44eb3-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="44eb3-118">Üretimde kullanmadan önce hello adımları özelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="44eb3-119">Her adım hello nedenler anlamak hello şekilde yardımcı olur bilgiler sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="44eb3-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="44eb3-120">Bağlantılar tooother makaleleri belirli konular hakkında daha fazla ayrıntı sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="44eb3-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="44eb3-121">Bu öğretici değinmektedir hello hizmetleri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="44eb3-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="44eb3-122">Azure Anahtar Kasası.</span><span class="sxs-lookup"><span data-stu-id="44eb3-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="44eb3-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="44eb3-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="44eb3-124">Azure günlük tümleştirme</span><span class="sxs-lookup"><span data-stu-id="44eb3-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="44eb3-125">İlk kurulumu</span><span class="sxs-lookup"><span data-stu-id="44eb3-125">Initial setup</span></span>

<span data-ttu-id="44eb3-126">Bu makalede hello adımları tamamlayabilmeniz için önce hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="44eb3-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="44eb3-127">Bir Azure aboneliği ve hesabı bu abonelikte yönetici haklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="44eb3-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="44eb3-128">Bir aboneliğiniz yoksa oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="44eb3-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="44eb3-129">Erişim toohello sistemiyle Azure günlük tümleştirme yüklemek için hello gereksinimleri karşılayan Internet.</span><span class="sxs-lookup"><span data-stu-id="44eb3-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="44eb3-130">Merhaba sistem veya şirket içinde barındırılan bir bulut hizmetinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="44eb3-131">[Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324) yüklü.</span><span class="sxs-lookup"><span data-stu-id="44eb3-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="44eb3-132">tooinstall onu:</span><span class="sxs-lookup"><span data-stu-id="44eb3-132">tooinstall it:</span></span>

   <span data-ttu-id="44eb3-133">a.</span><span class="sxs-lookup"><span data-stu-id="44eb3-133">a.</span></span> <span data-ttu-id="44eb3-134">2. adımda bahsedilen Uzak Masaüstü tooconnect toohello sistemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="44eb3-135">b.</span><span class="sxs-lookup"><span data-stu-id="44eb3-135">b.</span></span> <span data-ttu-id="44eb3-136">Hello Azure günlük tümleştirme yükleyici toohello sistem kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="44eb3-137">Yapabilecekleriniz [hello yükleme dosyalarını indirmek](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="44eb3-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="44eb3-138">c.</span><span class="sxs-lookup"><span data-stu-id="44eb3-138">c.</span></span> <span data-ttu-id="44eb3-139">Merhaba Yükleyicisi'ni başlatın ve hello Microsoft Yazılımı Lisans koşulları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="44eb3-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="44eb3-140">d.</span><span class="sxs-lookup"><span data-stu-id="44eb3-140">d.</span></span> <span data-ttu-id="44eb3-141">Telemetri bilgileri sağlayacaksa hello onay kutusunu seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="44eb3-142">Bunun yerine kullanım bilgileri tooMicrosoft göndermek hello onay kutusunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="44eb3-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="44eb3-143">Azure günlük tümleştirmesi hakkında daha fazla bilgi için ve nasıl tooinstall, bkz: [Azure tanılama günlüğünü ve Windows Olay iletme Azure günlük tümleştirme](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="44eb3-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="44eb3-144">Merhaba son PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="44eb3-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="44eb3-145">Windows Server 2016 sahip sonra en az PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="44eb3-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="44eb3-146">Herhangi bir Windows Server sürümünü kullanıyorsanız, PowerShell yüklü önceki bir sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="44eb3-147">Girerek hello sürüm denetleyebilirsiniz ```get-host``` bir PowerShell penceresinde.</span><span class="sxs-lookup"><span data-stu-id="44eb3-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="44eb3-148">PowerShell 5.0 yüklü yoksa, şunları yapabilirsiniz [karşıdan](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="44eb3-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="44eb3-149">En az sonra PowerShell 5. 0'da, tooinstall hello en son sürümünü devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44eb3-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="44eb3-150">a.</span><span class="sxs-lookup"><span data-stu-id="44eb3-150">a.</span></span> <span data-ttu-id="44eb3-151">Bir PowerShell penceresinde hello girin ```Install-Module Azure``` komutu.</span><span class="sxs-lookup"><span data-stu-id="44eb3-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="44eb3-152">Merhaba yükleme adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="44eb3-153">b.</span><span class="sxs-lookup"><span data-stu-id="44eb3-153">b.</span></span> <span data-ttu-id="44eb3-154">Merhaba girin ```Install-Module AzureRM``` komutu.</span><span class="sxs-lookup"><span data-stu-id="44eb3-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="44eb3-155">Merhaba yükleme adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="44eb3-156">Daha fazla bilgi için bkz: [Azure PowerShell yükleme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="44eb3-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="44eb3-157">Destekleyen altyapı öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="44eb3-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="44eb3-158">Yükseltilmiş bir PowerShell penceresi açın ve çok**C:\Program Files\Microsoft Azure günlük tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="44eb3-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="44eb3-159">Merhaba AzLog cmdlet'leri hello betik LoadAzLogModule.ps1 çalıştırarak içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="44eb3-160">Merhaba girin `.\LoadAzLogModule.ps1` komutu.</span><span class="sxs-lookup"><span data-stu-id="44eb3-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="44eb3-161">(Bildirim hello ". \" Bu komutta.) Şuna benzer bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="44eb3-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Yüklenen modüller listesi](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="44eb3-163">Merhaba girin `Login-AzureRmAccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="44eb3-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="44eb3-164">Merhaba oturum açma penceresinde hello Bu öğretici için kullanacağınız hello abonelik için kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="44eb3-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="44eb3-165">Bu hello tooAzure bu makineden oturum açtığınızdan ilk kez ise, Microsoft toocollect PowerShell kullanım verilerini izin verme hakkında bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="44eb3-166">Kullanılan tooimprove Azure PowerShell olacağından, bu veri toplama etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="44eb3-167">Başarılı bir kimlik doğrulamasından sonra oturum açtınız ve ekran aşağıdaki hello hello bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="44eb3-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="44eb3-168">Merhaba abonelik kimliği ve abonelik adını not edin, bunları gerekir çünkü toocomplete sonraki adımlar.</span><span class="sxs-lookup"><span data-stu-id="44eb3-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![PowerShell penceresi](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="44eb3-170">Değişkenleri daha sonra kullanılacak toostore değerleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44eb3-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="44eb3-171">Her PowerShell satırlardan hello girin.</span><span class="sxs-lookup"><span data-stu-id="44eb3-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="44eb3-172">Ortamınızı tooadjust hello değerleri toomatch gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="44eb3-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(Abonelik adınızı farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="44eb3-174">Merhaba hello önceki komutunun çıktısını bir parçası olarak görebileceğiniz.)</span><span class="sxs-lookup"><span data-stu-id="44eb3-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="44eb3-175">```$location = 'West US'```(Bu değişken, kaynaklar nerede oluşturulacağını kullanılan toopass hello konum olacaktır.</span><span class="sxs-lookup"><span data-stu-id="44eb3-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="44eb3-176">"Bu değişken toobe seçtiğiniz herhangi bir konuma değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="44eb3-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="44eb3-177">``` $name = 'azlogtest' + $random```(Merhaba adı herhangi bir şey olabilir, ancak yalnızca küçük harf ve sayı içermelidir.)</span><span class="sxs-lookup"><span data-stu-id="44eb3-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="44eb3-178">``` $storageName = $name```(Bu değişken hello depolama hesabı adı için kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="44eb3-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="44eb3-179">```$rgname = $name ```(Bu değişken hello kaynak grubu adı için kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="44eb3-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="44eb3-180">``` $eventHubNameSpaceName = $name```(Bu hello hello olay hub'ı ad alanının adıdır.)</span><span class="sxs-lookup"><span data-stu-id="44eb3-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="44eb3-181">İle çalışacaksınız hello abonelik belirtin:</span><span class="sxs-lookup"><span data-stu-id="44eb3-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="44eb3-182">Kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="44eb3-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="44eb3-183">Girerseniz `$rg` bu noktada, çıktı benzer toothis ekran görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="44eb3-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Çıktıdan sonra kaynak grubu oluşturma](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="44eb3-185">Durum bilgilerini kullanılan tookeep izini olacak bir depolama hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="44eb3-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="44eb3-186">Merhaba olay hub'ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="44eb3-186">Create hello event hub namespace.</span></span> <span data-ttu-id="44eb3-187">Gerekli toocreate bir event hub budur.</span><span class="sxs-lookup"><span data-stu-id="44eb3-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="44eb3-188">Merhaba Öngörüler sağlayıcı ile kullanılacak hello kural kimliği alın:</span><span class="sxs-lookup"><span data-stu-id="44eb3-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="44eb3-189">Tüm olası Azure konumlarını almak ve daha sonraki bir adımda kullanılabilir hello adları tooa değişkeni ekleyin:</span><span class="sxs-lookup"><span data-stu-id="44eb3-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="44eb3-190">a.</span><span class="sxs-lookup"><span data-stu-id="44eb3-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="44eb3-191">b.</span><span class="sxs-lookup"><span data-stu-id="44eb3-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="44eb3-192">Girerseniz `$locations` bu noktada, Get-AzureRmLocation tarafından döndürülen hello ek bilgileri olmadan hello konum adları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="44eb3-193">Bir Azure Resource Manager günlük profili oluşturun:</span><span class="sxs-lookup"><span data-stu-id="44eb3-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="44eb3-194">Hello Azure günlük profili hakkında daha fazla bilgi için bkz: [hello Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="44eb3-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="44eb3-195">Toocreate günlük profili çalıştığınızda bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="44eb3-196">Get-AzureRmLogProfile ve Kaldır-AzureRmLogProfile hello belgelerine daha sonra gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="44eb3-197">Get-AzureRmLogProfile çalıştırırsanız, hello günlük profili hakkındaki bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44eb3-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="44eb3-198">Merhaba girerek hello profil günlük silebilirsiniz ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` komutu.</span><span class="sxs-lookup"><span data-stu-id="44eb3-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Resource Manager profili hatası](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="44eb3-200">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="44eb3-200">Create a key vault</span></span>

1. <span data-ttu-id="44eb3-201">Merhaba anahtar kasası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="44eb3-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="44eb3-202">Merhaba anahtar kasası için günlüğe kaydetmeyi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="44eb3-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="44eb3-203">Günlük etkinliği oluştur</span><span class="sxs-lookup"><span data-stu-id="44eb3-203">Generate log activity</span></span>

<span data-ttu-id="44eb3-204">İstekleri tooKey kasa toogenerate günlük etkinliği gönderilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="44eb3-205">Eylemler anahtar oluşturma, gizli saklamak ister veya gizli anahtar Kasası'nı okuma günlük girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="44eb3-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="44eb3-206">Merhaba geçerli depolama anahtarlarını görüntüle:</span><span class="sxs-lookup"><span data-stu-id="44eb3-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="44eb3-207">Yeni bir **key2**:</span><span class="sxs-lookup"><span data-stu-id="44eb3-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="44eb3-208">Merhaba anahtarlarını görüntülemek yeniden ve, görmek **key2** farklı bir değer içerir:</span><span class="sxs-lookup"><span data-stu-id="44eb3-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="44eb3-209">Ayarlama ve ek günlük girişlerini gizli toogenerate okuyun:</span><span class="sxs-lookup"><span data-stu-id="44eb3-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="44eb3-210">a.</span><span class="sxs-lookup"><span data-stu-id="44eb3-210">a.</span></span> <span data-ttu-id="44eb3-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="44eb3-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Gizli döndürdü](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="44eb3-213">Azure günlük tümleştirmesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="44eb3-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="44eb3-214">Tüm hello gerekli öğeler toohave anahtar kasası günlüğü tooan olay hub'ı yapılandırdınız, tooconfigure Azure günlük tümleştirme gerekir:</span><span class="sxs-lookup"><span data-stu-id="44eb3-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="44eb3-215">Her olay hub'ına yönelik Hello AzLog komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="44eb3-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="44eb3-216">Bir dakika veya bunu hello son iki komutlarını çalıştırarak, sonra oluşturulan JSON dosyaları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="44eb3-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="44eb3-217">Hello dizin izleyerek onaylayın **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="44eb3-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44eb3-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44eb3-218">Next steps</span></span>

- [<span data-ttu-id="44eb3-219">Azure günlük tümleştirme hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="44eb3-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="44eb3-220">Azure günlük tümleştirme ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="44eb3-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="44eb3-221">Azure kaynaklarını günlüklerinden SIEM sistemlerinizi tümleştirme</span><span class="sxs-lookup"><span data-stu-id="44eb3-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
