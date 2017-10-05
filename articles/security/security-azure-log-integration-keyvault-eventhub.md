---
title: "Azure anahtar kasası günlükleri Olay hub'ları kullanarak tümleştirme | Microsoft Docs"
description: "Anahtar kasası günlükleri için bir SIEM Azure günlük tümleştirmeyi kullanarak kullanılabilmesi için gerekli adımları sağlar Öğreticisi"
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
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="00192-103">Azure günlük tümleştirme Öğreticisi: olay hub'ları kullanarak işlem Azure anahtar kasası olayları</span><span class="sxs-lookup"><span data-stu-id="00192-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="00192-104">Günlüğe kaydedilen olayları almak ve güvenlik bilgileri ve Olay yönetimi (SIEM) sisteminiz için kullanılabilir duruma getirmek için Azure günlük tümleştirme özelliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00192-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="00192-105">Bu öğreticide Azure günlük tümleştirme aracılığıyla Azure Event Hubs alınan günlükleri işlemek için nasıl kullanılabileceği bir örnek gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="00192-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="00192-106">Azure günlük tümleştirme ve Event Hubs birlikte nasıl örnek adımları izleyerek ve her adım çözümü nasıl destekler? anlama çalışır ile tanıyalım için bu öğreticiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="00192-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="00192-107">Daha sonra buraya oluşturmak, şirketinizin benzersiz gereksinimlerini desteklemek için kendi adımları öğrendiklerinizi alabilir.</span><span class="sxs-lookup"><span data-stu-id="00192-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="00192-108">Adımları ve Bu öğreticide komutları kopyalanan ve yapıştırılan amaçlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="00192-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="00192-109">Bunlar yalnızca örnek demektir.</span><span class="sxs-lookup"><span data-stu-id="00192-109">They're examples only.</span></span> <span data-ttu-id="00192-110">"Olduğu gibi" PowerShell komutlarını Canlı ortamınızda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="00192-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="00192-111">Bunları benzersiz ortamınıza bağlı özelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00192-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="00192-112">Bu öğreticide, alma olay hub'ına oturum Azure anahtar kasası etkinliği ve JSON dosyaları olarak SIEM sisteminizi kullanıma işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="00192-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="00192-113">SIEM sisteminizi JSON dosyalarını işlemek için daha sonra yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00192-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="00192-114">Bu öğreticideki adımlardan çoğu anahtar kasalarını, depolama hesapları ve olay hub'ları yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="00192-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="00192-115">Belirli Azure günlük tümleştirme adımları Bu öğreticinin sonunda ' dir.</span><span class="sxs-lookup"><span data-stu-id="00192-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="00192-116">Bu adımları bir üretim ortamında gerçekleştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="00192-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="00192-117">Bunlar yalnızca bir laboratuvar ortamı için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="00192-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="00192-118">Üretimde kullanmadan önce adımları özelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00192-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="00192-119">Yol boyunca sağlanan bilgiler, her adım nedenler anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="00192-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="00192-120">Diğer makalelerinin bağlantıları belirli konular hakkında daha fazla ayrıntı sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="00192-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="00192-121">Bu öğretici değinmektedir hizmetleri hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="00192-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="00192-122">Azure Anahtar Kasası.</span><span class="sxs-lookup"><span data-stu-id="00192-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="00192-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="00192-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="00192-124">Azure günlük tümleştirme</span><span class="sxs-lookup"><span data-stu-id="00192-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="00192-125">İlk kurulumu</span><span class="sxs-lookup"><span data-stu-id="00192-125">Initial setup</span></span>

<span data-ttu-id="00192-126">Bu makaledeki adımları tamamlayabilmeniz için önce aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="00192-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="00192-127">Bir Azure aboneliği ve hesabı bu abonelikte yönetici haklarına sahip.</span><span class="sxs-lookup"><span data-stu-id="00192-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="00192-128">Bir aboneliğiniz yoksa oluşturabileceğiniz bir [ücretsiz bir hesap](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="00192-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="00192-129">Azure günlük tümleştirme yükleme gereksinimlerini karşılayan internet erişimi olan bir sistemi.</span><span class="sxs-lookup"><span data-stu-id="00192-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="00192-130">Sistem veya şirket içinde barındırılan bir bulut hizmetinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="00192-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="00192-131">[Azure günlük tümleştirme](https://www.microsoft.com/download/details.aspx?id=53324) yüklü.</span><span class="sxs-lookup"><span data-stu-id="00192-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="00192-132">Yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="00192-132">To install it:</span></span>

   <span data-ttu-id="00192-133">a.</span><span class="sxs-lookup"><span data-stu-id="00192-133">a.</span></span> <span data-ttu-id="00192-134">2. adımda bahsedilen sisteme bağlanmak için Uzak Masaüstü'nü kullanın.</span><span class="sxs-lookup"><span data-stu-id="00192-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="00192-135">b.</span><span class="sxs-lookup"><span data-stu-id="00192-135">b.</span></span> <span data-ttu-id="00192-136">Azure günlük tümleştirme yükleyici sisteme kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="00192-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="00192-137">Yapabilecekleriniz [yükleme dosyalarını indirmek](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="00192-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="00192-138">c.</span><span class="sxs-lookup"><span data-stu-id="00192-138">c.</span></span> <span data-ttu-id="00192-139">Yükleyiciyi başlatma ve Microsoft Yazılım Lisans Koşulları'nı kabul edin.</span><span class="sxs-lookup"><span data-stu-id="00192-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="00192-140">d.</span><span class="sxs-lookup"><span data-stu-id="00192-140">d.</span></span> <span data-ttu-id="00192-141">Telemetri bilgileri sağlarız, onay kutusunu seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="00192-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="00192-142">Bunun yerine kullanım bilgilerini Microsoft'a göndermek, onay kutusunu temizleyin.</span><span class="sxs-lookup"><span data-stu-id="00192-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="00192-143">Azure günlük tümleştirme ve nasıl yükleneceği hakkında daha fazla bilgi için bkz: [Azure tanılama günlüğünü ve Windows Olay iletme Azure günlük tümleştirme](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="00192-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="00192-144">En son PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="00192-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="00192-145">Windows Server 2016 sahip sonra en az PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="00192-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="00192-146">Herhangi bir Windows Server sürümünü kullanıyorsanız, PowerShell yüklü önceki bir sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="00192-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="00192-147">Sürüm girerek denetleyebilirsiniz ```get-host``` bir PowerShell penceresinde.</span><span class="sxs-lookup"><span data-stu-id="00192-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="00192-148">PowerShell 5.0 yüklü yoksa, şunları yapabilirsiniz [karşıdan](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="00192-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="00192-149">En az sonra PowerShell 5. 0'da, devam en son sürümünü yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="00192-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="00192-150">a.</span><span class="sxs-lookup"><span data-stu-id="00192-150">a.</span></span> <span data-ttu-id="00192-151">Bir PowerShell penceresinde girin ```Install-Module Azure``` komutu.</span><span class="sxs-lookup"><span data-stu-id="00192-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="00192-152">Yükleme adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="00192-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="00192-153">b.</span><span class="sxs-lookup"><span data-stu-id="00192-153">b.</span></span> <span data-ttu-id="00192-154">Girin ```Install-Module AzureRM``` komutu.</span><span class="sxs-lookup"><span data-stu-id="00192-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="00192-155">Yükleme adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="00192-155">Complete the installation steps.</span></span>

   <span data-ttu-id="00192-156">Daha fazla bilgi için bkz: [Azure PowerShell yükleme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="00192-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="00192-157">Destekleyen altyapı öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="00192-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="00192-158">Yükseltilmiş bir PowerShell penceresi açın ve gidin **C:\Program Files\Microsoft Azure günlük tümleştirme**.</span><span class="sxs-lookup"><span data-stu-id="00192-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="00192-159">AzLog cmdlet'leri LoadAzLogModule.ps1 komut dosyası çalıştırarak içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="00192-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="00192-160">Girin `.\LoadAzLogModule.ps1` komutu.</span><span class="sxs-lookup"><span data-stu-id="00192-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="00192-161">(Bildirim ". \" Bu komutta.) Şuna benzer bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="00192-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Yüklenen modüller listesi](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="00192-163">Girin `Login-AzureRmAccount` komutu.</span><span class="sxs-lookup"><span data-stu-id="00192-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="00192-164">Oturum açma penceresinde, Bu öğretici için kullanacağı aboneliği için kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="00192-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="00192-165">Bu, Azure'a bu makineden oturum açtığınızdan ilk kez kullanıyorsanız, PowerShell kullanım verilerini toplamak için Microsoft izin verme hakkında bir ileti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="00192-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="00192-166">Azure PowerShell geliştirmek için kullanılacak çünkü bu veri toplama etkinleştirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="00192-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="00192-167">Başarılı bir kimlik doğrulamasından sonra oturum açtınız ve aşağıdaki ekran görüntüsünde bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="00192-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="00192-168">Sonraki adımları tamamlamanız gerekir çünkü abonelik kimliği ve abonelik adını not edin.</span><span class="sxs-lookup"><span data-stu-id="00192-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![PowerShell penceresi](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="00192-170">Daha sonra kullanılacak değerlerini depolamak için değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00192-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="00192-171">Aşağıdaki PowerShell satırların her biri girin.</span><span class="sxs-lookup"><span data-stu-id="00192-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="00192-172">Ortamınıza uyum sağlaması için değerleri ayarlamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="00192-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="00192-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(Abonelik adınızı farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="00192-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="00192-174">Önceki komutunun çıktısını bir parçası olarak görebileceğiniz.)</span><span class="sxs-lookup"><span data-stu-id="00192-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="00192-175">```$location = 'West US'```(Bu değişken kaynakların nerede oluşturulacağını konumu geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="00192-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="00192-176">"Seçtiğiniz herhangi bir yerde olması için bu değişkeni değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="00192-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="00192-177">``` $name = 'azlogtest' + $random```(Ad, herhangi bir şey olabilir, ancak yalnızca küçük harf ve sayı içermelidir.)</span><span class="sxs-lookup"><span data-stu-id="00192-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="00192-178">``` $storageName = $name```(Depolama hesabı adı için bu değişkeni kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="00192-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="00192-179">```$rgname = $name ```(Kaynak grubu adı için bu değişkeni kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="00192-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="00192-180">``` $eventHubNameSpaceName = $name```(Bu olay hub'ı ad alanının adıdır.)</span><span class="sxs-lookup"><span data-stu-id="00192-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="00192-181">İle çalışacaksınız abonelik belirtin:</span><span class="sxs-lookup"><span data-stu-id="00192-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="00192-182">Kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="00192-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="00192-183">Girerseniz `$rg` bu noktada, bu ekran görüntüsüne benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="00192-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Çıktıdan sonra kaynak grubu oluşturma](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="00192-185">Durum bilgileri izlemek için kullanılan bir depolama hesabı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="00192-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="00192-186">Olay hub'ı ad alanını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="00192-186">Create the event hub namespace.</span></span> <span data-ttu-id="00192-187">Bu, bir olay hub'ı oluşturmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="00192-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="00192-188">Öngörüler sağlayıcı ile kullanılacak kural kimliği alın:</span><span class="sxs-lookup"><span data-stu-id="00192-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="00192-189">Tüm olası Azure konumlarını almak ve daha sonraki bir adımda kullanılabilir bir değişken adları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="00192-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="00192-190">a.</span><span class="sxs-lookup"><span data-stu-id="00192-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="00192-191">b.</span><span class="sxs-lookup"><span data-stu-id="00192-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="00192-192">Girerseniz `$locations` bu noktada, Get-AzureRmLocation tarafından döndürülen ek bilgiler olmadan konum adlarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="00192-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="00192-193">Bir Azure Resource Manager günlük profili oluşturun:</span><span class="sxs-lookup"><span data-stu-id="00192-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="00192-194">Azure günlük profili hakkında daha fazla bilgi için bkz: [Azure etkinlik günlüğü'ne genel bakış](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="00192-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="00192-195">Bir günlük profil oluşturmaya çalışırken bir hata iletisi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00192-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="00192-196">Get-AzureRmLogProfile ve Kaldır-AzureRmLogProfile belgelerine daha sonra gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00192-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="00192-197">Get-AzureRmLogProfile çalıştırırsanız, günlük profili hakkındaki bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00192-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="00192-198">Girerek mevcut günlük profili silebilirsiniz ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` komutu.</span><span class="sxs-lookup"><span data-stu-id="00192-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Resource Manager profili hatası](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="00192-200">Bir anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="00192-200">Create a key vault</span></span>

1. <span data-ttu-id="00192-201">Anahtar kasası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="00192-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="00192-202">Anahtar kasası için günlüğe kaydetmeyi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="00192-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="00192-203">Günlük etkinliği oluştur</span><span class="sxs-lookup"><span data-stu-id="00192-203">Generate log activity</span></span>

<span data-ttu-id="00192-204">İstekleri anahtar kasası için günlük etkinliği oluşturmak için gönderilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="00192-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="00192-205">Eylemler anahtar oluşturma, gizli saklamak ister veya gizli anahtar Kasası'nı okuma günlük girişi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="00192-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="00192-206">Geçerli depolama anahtarlarını görüntüle:</span><span class="sxs-lookup"><span data-stu-id="00192-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="00192-207">Yeni bir **key2**:</span><span class="sxs-lookup"><span data-stu-id="00192-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="00192-208">Anahtarları yeniden görüntülemek ve görüp **key2** farklı bir değer içerir:</span><span class="sxs-lookup"><span data-stu-id="00192-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="00192-209">Ayarlama ve ek günlük girişleri oluşturmak için bir gizlilik okuyun:</span><span class="sxs-lookup"><span data-stu-id="00192-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="00192-210">a.</span><span class="sxs-lookup"><span data-stu-id="00192-210">a.</span></span> <span data-ttu-id="00192-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="00192-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Gizli döndürdü](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="00192-213">Azure günlük tümleştirmesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="00192-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="00192-214">Olay hub'ına oturum anahtar kasası için gerekli olan tüm öğelerin yapılandırdığınıza göre Azure günlük tümleştirmeyi de yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="00192-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="00192-215">Her olay hub'ına yönelik AzLog komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="00192-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="00192-216">Bir dakika veya bunu son iki komutlarını çalıştırarak, sonra oluşturulan JSON dosyaları görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="00192-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="00192-217">Dizin izleyerek onaylayın **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="00192-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00192-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00192-218">Next steps</span></span>

- [<span data-ttu-id="00192-219">Azure günlük tümleştirme hakkında SSS</span><span class="sxs-lookup"><span data-stu-id="00192-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="00192-220">Azure günlük tümleştirme ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="00192-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="00192-221">Azure kaynaklarını günlüklerinden SIEM sistemlerinizi tümleştirme</span><span class="sxs-lookup"><span data-stu-id="00192-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
