
<span data-ttu-id="c7212-101">Microsoft Azure bulut hizmeti ile ilgili sorunları tanılama sorunları ortaya çıktığında sanal makinelerde hizmetin günlük dosyalarını toplama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c7212-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting the service’s log files on virtual machines as the issues occur.</span></span> <span data-ttu-id="c7212-102">Ağda tek seferlik günlükleri koleksiyona AzureLogCollector uzantısı isteğe bağlı bir veya daha fazla bulut hizmeti Vm'lerden (web rolleri ve çalışan rolleri) kullanın ve tüm açmadan uzaktan herhangi birini Azure depolama hesabı için – toplanan dosya aktarımı VM'ler.</span><span class="sxs-lookup"><span data-stu-id="c7212-102">You can use the AzureLogCollector extension on-demand to perfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer the collected files to an Azure storage account – all without remotely logging on to any of the VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="c7212-103">Günlüğe kaydedilen bilgileri çoğunu açıklamalarını http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c7212-103">Descriptions for most of the logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="c7212-104">Toplanacak dosyaları türlerinde bağımlı koleksiyon iki moddan vardır.</span><span class="sxs-lookup"><span data-stu-id="c7212-104">There are two modes of collection dependent on the types of files to be collected.</span></span>

* <span data-ttu-id="c7212-105">Azure Konuk Aracısı günlükleri yalnızca (GA).</span><span class="sxs-lookup"><span data-stu-id="c7212-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="c7212-106">Bu koleksiyon modu Azure Konuk aracıları ve diğer Azure bileşenleri ile ilgili tüm günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="c7212-106">This collection mode includes all the logs related to Azure guest agents and other Azure components.</span></span>
* <span data-ttu-id="c7212-107">Tüm günlükleri (tam).</span><span class="sxs-lookup"><span data-stu-id="c7212-107">All Logs (Full).</span></span> <span data-ttu-id="c7212-108">Bu koleksiyon modu artı GA modunda tüm dosyaları toplar:</span><span class="sxs-lookup"><span data-stu-id="c7212-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="c7212-109">Sistem ve uygulama olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="c7212-109">system and application event logs</span></span>
  * <span data-ttu-id="c7212-110">HTTP Hata günlüklerini</span><span class="sxs-lookup"><span data-stu-id="c7212-110">HTTP error logs</span></span>
  * <span data-ttu-id="c7212-111">IIS günlükleri</span><span class="sxs-lookup"><span data-stu-id="c7212-111">IIS Logs</span></span>
  * <span data-ttu-id="c7212-112">Kurulum günlükleri</span><span class="sxs-lookup"><span data-stu-id="c7212-112">Setup logs</span></span>
  * <span data-ttu-id="c7212-113">diğer sistem günlükleri</span><span class="sxs-lookup"><span data-stu-id="c7212-113">other system logs</span></span>

<span data-ttu-id="c7212-114">Her iki koleksiyon modlarında aşağıdaki yapısını koleksiyonunu kullanarak ek veri koleksiyon klasörleri belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="c7212-114">In both collection modes, additional data collection folders can be specified by using a collection of the following structure:</span></span>

* <span data-ttu-id="c7212-115">**Ad**: ZIP dosyasının içinde alt klasör adı olarak toplanacak kullanılacak koleksiyonun adını.</span><span class="sxs-lookup"><span data-stu-id="c7212-115">**Name**: The name of the collection, which will be used as the name of subfolder inside the zip file to be collected.</span></span>
* <span data-ttu-id="c7212-116">**Konum**: sanal makinede burada dosya toplanacak klasörün yolu.</span><span class="sxs-lookup"><span data-stu-id="c7212-116">**Location**: The path to the folder on the virtual machine where file will be collected.</span></span>
* <span data-ttu-id="c7212-117">**SearchPattern**: toplanacak dosyaların adlarını düzeni.</span><span class="sxs-lookup"><span data-stu-id="c7212-117">**SearchPattern**: The pattern of the names of files to be collected.</span></span> <span data-ttu-id="c7212-118">Varsayılan değer "*"</span><span class="sxs-lookup"><span data-stu-id="c7212-118">Default is “*”</span></span>
* <span data-ttu-id="c7212-119">**Özyinelemeli**: dosyaları klasörünün altında toplanan yinelemeli olacaksa.</span><span class="sxs-lookup"><span data-stu-id="c7212-119">**Recursive**: if the files will be collected recursively under the folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7212-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c7212-120">Prerequisites</span></span>
* <span data-ttu-id="c7212-121">Oluşturulan ZIP dosyaları kaydetmek uzantı için bir depolama hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c7212-121">You need to have a storage account for extension to save generated zip files.</span></span>
* <span data-ttu-id="c7212-122">Azure PowerShell cmdlet'leri V0.8.0 kullandığınızdan emin olmanız gerekir veya üstü.</span><span class="sxs-lookup"><span data-stu-id="c7212-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="c7212-123">Daha fazla bilgi için bkz: [Azure indirmeleri](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c7212-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-the-extension"></a><span data-ttu-id="c7212-124">Uzantısı Ekle</span><span class="sxs-lookup"><span data-stu-id="c7212-124">Add the extension</span></span>
<span data-ttu-id="c7212-125">Kullanabileceğiniz [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet'leri veya [Hizmet Yönetimi REST API'lerine](https://msdn.microsoft.com/library/ee460799.aspx) AzureLogCollector uzantısı eklemek için.</span><span class="sxs-lookup"><span data-stu-id="c7212-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) to add the AzureLogCollector extension.</span></span>

<span data-ttu-id="c7212-126">Bulut Hizmetleri, var olan Azure Powershell cmdlet'i için **kümesi AzureServiceExtension**, bulut hizmet rolü örneklerinin uzantısını etkinleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7212-126">For Cloud Services, the existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used to enable the extension on Cloud Service role instances.</span></span> <span data-ttu-id="c7212-127">Bu uzantı Bu cmdlet'i etkinleştirilmiş her zaman, günlük toplama seçili roller seçili rol örneklerini tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="c7212-127">Every time this extension is enabled through this cmdlet, log collection is triggered on the selected role instances of selected roles.</span></span>

<span data-ttu-id="c7212-128">Sanal makineler, mevcut Azure Powershell cmdlet'i için **kümesi AzureVMExtension**, sanal makinelerde uzantısını etkinleştirmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c7212-128">For Virtual Machines, the existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used to enable the extension on Virtual Machines.</span></span> <span data-ttu-id="c7212-129">Bu uzantı cmdlet'leri aracılığıyla etkinleştirilmiş her zaman, günlük toplama her örneğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="c7212-129">Every time this extension is enabled through the cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="c7212-130">Dahili olarak, bu uzantı JSON tabanlı PublicConfiguration ve PrivateConfiguration kullanır.</span><span class="sxs-lookup"><span data-stu-id="c7212-130">Internally, this extension uses the JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="c7212-131">Ortak ve özel yapılandırması için örnek JSON düzenini verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c7212-131">The following is the layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="c7212-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="c7212-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri to your storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a><span data-ttu-id="c7212-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="c7212-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="c7212-134">Bu uzantının gerekmez **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="c7212-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="c7212-135">İçin boş bir yapı sağlar **– PrivateConfiguration** bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="c7212-135">You can just provide an empty structure for the **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="c7212-136">Bir veya daha fazla örneğini bir bulut hizmeti veya koleksiyonları çalıştırmak ve toplanan dosyaları belirtilen Azure hesabına göndermek için her bir VM üzerinde tetikler sanal makine seçilen rollerin AzureLogCollector eklemek için iki aşağıdaki adımlardan birini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7212-136">You can follow one of the two following steps to add the AzureLogCollector to one or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers the collections on each VM to run and send the collected files to Azure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="c7212-137">Bir hizmeti uzantı olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="c7212-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="c7212-138">Azure PowerShell aboneliğinize bağlanmak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c7212-138">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>
2. <span data-ttu-id="c7212-139">Ekleme ve AzureLogCollector uzantısını etkinleştirmek istediğiniz hizmet adı, yuva, rolleri ve rol örnekleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="c7212-139">Specify the service name, slot, roles, and role instances to which you want to add and enable the AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify the slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified the roles on which the extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify the instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="c7212-140">Dosyaları toplanacak ek veri klasörü belirtin (Bu adım isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="c7212-140">Specify the additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="c7212-141">Belirteci kullanabilirsiniz `%roleroot%` bir sabit sürücü kullanmayan rol kök sürücüsünde belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="c7212-141">You can use token `%roleroot%` to specify the role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="c7212-142">Azure depolama hesabı adı ve toplanan dosyaları karşıya yüklenecek anahtarı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c7212-142">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="c7212-143">(Makalenin sonunda yer alan) SetAzureServiceLogCollector.ps1 AzureLogCollector uzantısı için bir bulut hizmeti etkinleştirmek için şu şekilde çağırın.</span><span class="sxs-lookup"><span data-stu-id="c7212-143">Call the SetAzureServiceLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="c7212-144">Yürütme tamamlandığında, yüklenen dosya altında bulabilirsiniz`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="c7212-144">Once the execution is completed, you can find the uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="c7212-145">Aşağıdaki komut dosyasına iletilen parametreler tanımıdır.</span><span class="sxs-lookup"><span data-stu-id="c7212-145">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="c7212-146">(Bu aşağıda da kopyalanır.)</span><span class="sxs-lookup"><span data-stu-id="c7212-146">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* <span data-ttu-id="c7212-147">*ServiceName*: Bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="c7212-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="c7212-148">*Rolleri*: "WebRole1" veya "WorkerRole1" gibi rollerinin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="c7212-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="c7212-149">*Örnekleri*:--virgülle ayırarak rol örneklerinin adlarının bir listesini bir joker karakter dizesi kullanın ("*") tüm rol örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="c7212-149">*Instances*: A list of the names of role instances separated by comma -- use the wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="c7212-150">*Yuva*: Yuva adı.</span><span class="sxs-lookup"><span data-stu-id="c7212-150">*Slot*: Slot name.</span></span> <span data-ttu-id="c7212-151">"Üretim" veya "Hazırlama".</span><span class="sxs-lookup"><span data-stu-id="c7212-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="c7212-152">*Mod*: Koleksiyon modu.</span><span class="sxs-lookup"><span data-stu-id="c7212-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="c7212-153">"Tam" veya "GA".</span><span class="sxs-lookup"><span data-stu-id="c7212-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="c7212-154">*StorageAccountName*: toplanan verileri depolamak için ad, Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="c7212-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="c7212-155">*StorageAccountKey*: ad, Azure depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="c7212-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="c7212-156">*AdditionalDataLocationList*: aşağıdaki yapısını listesi:</span><span class="sxs-lookup"><span data-stu-id="c7212-156">*AdditionalDataLocationList*: A list of the following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="c7212-157">Bir VM uzantısı olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="c7212-157">Adding as a VM Extension</span></span>
<span data-ttu-id="c7212-158">Azure PowerShell aboneliğinize bağlanmak için yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="c7212-158">Follow the instructions to connect Azure PowerShell to your subscription.</span></span>

1. <span data-ttu-id="c7212-159">Hizmet adı, VM ve koleksiyon modu belirtin.</span><span class="sxs-lookup"><span data-stu-id="c7212-159">Specify the service name, VM, and the collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify the VM name
        $VMName = "'YourVMName'"
   
        #Specify the collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify the additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="c7212-160">Azure depolama hesabı adı ve toplanan dosyaları karşıya yüklenecek anahtarı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c7212-160">Provide the Azure storage account name and key to which collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="c7212-161">(Makalenin sonunda yer alan) SetAzureVMLogCollector.ps1 AzureLogCollector uzantısı için bir bulut hizmeti etkinleştirmek için şu şekilde çağırın.</span><span class="sxs-lookup"><span data-stu-id="c7212-161">Call the SetAzureVMLogCollector.ps1 (included at the end of the article) as follows to enable the AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="c7212-162">Yürütme tamamlandığında, yüklenen dosya https://YouareStorageAccountName.blob.core.windows.net/vmlogs altında bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="c7212-162">Once the execution is completed, you can find the uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="c7212-163">Aşağıdaki komut dosyasına iletilen parametreler tanımıdır.</span><span class="sxs-lookup"><span data-stu-id="c7212-163">The following is the definition of the parameters passed to the script.</span></span> <span data-ttu-id="c7212-164">(Bu aşağıda da kopyalanır.)</span><span class="sxs-lookup"><span data-stu-id="c7212-164">(This is copied below as well.)</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* <span data-ttu-id="c7212-165">ServiceName: Bulut hizmeti adınız.</span><span class="sxs-lookup"><span data-stu-id="c7212-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="c7212-166">VMName VM adı.</span><span class="sxs-lookup"><span data-stu-id="c7212-166">VMName The name of the VM.</span></span>
* <span data-ttu-id="c7212-167">: Koleksiyon modu.</span><span class="sxs-lookup"><span data-stu-id="c7212-167">Mode: Collection mode.</span></span> <span data-ttu-id="c7212-168">"Tam" veya "GA".</span><span class="sxs-lookup"><span data-stu-id="c7212-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="c7212-169">StorageAccountName: toplanan verileri depolamak için Azure depolama hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="c7212-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="c7212-170">StorageAccountKey: Azure depolama hesabı anahtarı adı.</span><span class="sxs-lookup"><span data-stu-id="c7212-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="c7212-171">AdditionalDataLocationList: Aşağıdaki yapısını bir listesi:</span><span class="sxs-lookup"><span data-stu-id="c7212-171">AdditionalDataLocationList: A list of the following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="c7212-172">Uzantı PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="c7212-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="c7212-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="c7212-173">SetAzureServiceLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  The value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need to get the Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri to the container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "The container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="c7212-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="c7212-174">SetAzureVMLogCollector.ps1</span></span>

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need to get the Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData to collect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it to JSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check the VM status to find if operation by extension has been completed or not. The completion of the operation,either succeed or fail, can be indicated by
                #the presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation to complete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access to the file, we can generate a read-only SasUri directly to the file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "The uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove the extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, the extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, the extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="c7212-175">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="c7212-175">Next Steps</span></span>
<span data-ttu-id="c7212-176">Şimdi inceleyin veya çok basit bir konumdan günlüklerinizi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c7212-176">Now you can examine or copy your logs from one very simple location.</span></span>

