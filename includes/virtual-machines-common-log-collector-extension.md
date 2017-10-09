
<span data-ttu-id="dd0e6-101">Microsoft Azure bulut hizmeti ile ilgili sorunları tanılama hello sorunları ortaya çıktığında sanal makinelerde hello hizmetin günlük dosyalarını toplama gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-101">Diagnosing issues with an Microsoft Azure cloud service requires collecting hello service’s log files on virtual machines as hello issues occur.</span></span> <span data-ttu-id="dd0e6-102">Bir veya daha fazla bulut hizmeti Vm'lerden (web rolleri ve çalışan rolleri için) ve aktarım hello toplanan dosyaları tooan Azure depolama hesabı – tüm uzaktan oturum açma olmadan günlüklerinin hello AzureLogCollector uzantısı isteğe bağlı tooperfom tek seferlik koleksiyonunu kullanabilirsiniz Merhaba VM'ler tooany.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-102">You can use hello AzureLogCollector extension on-demand tooperfom one-time collection of logs from one or more Cloud Service VMs (from both web roles and worker roles) and transfer hello collected files tooan Azure storage account – all without remotely logging on tooany of hello VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="dd0e6-103">Oturum hello bilgilerin çoğunu açıklamalarını http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-103">Descriptions for most of hello logged information can be found at http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp.</span></span>
> 
> 

<span data-ttu-id="dd0e6-104">Toplanan dosyaları toobe hello türlerini bağımlı koleksiyon iki moddan vardır.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-104">There are two modes of collection dependent on hello types of files toobe collected.</span></span>

* <span data-ttu-id="dd0e6-105">Azure Konuk Aracısı günlükleri yalnızca (GA).</span><span class="sxs-lookup"><span data-stu-id="dd0e6-105">Azure Guest Agent Logs only (GA).</span></span> <span data-ttu-id="dd0e6-106">Bu koleksiyon modu tüm hello günlükleri ilgili tooAzure Konuk aracıları ve diğer Azure bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-106">This collection mode includes all hello logs related tooAzure guest agents and other Azure components.</span></span>
* <span data-ttu-id="dd0e6-107">Tüm günlükleri (tam).</span><span class="sxs-lookup"><span data-stu-id="dd0e6-107">All Logs (Full).</span></span> <span data-ttu-id="dd0e6-108">Bu koleksiyon modu artı GA modunda tüm dosyaları toplar:</span><span class="sxs-lookup"><span data-stu-id="dd0e6-108">This collection mode will collect all files in GA mode plus:</span></span>
  
  * <span data-ttu-id="dd0e6-109">Sistem ve uygulama olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="dd0e6-109">system and application event logs</span></span>
  * <span data-ttu-id="dd0e6-110">HTTP Hata günlüklerini</span><span class="sxs-lookup"><span data-stu-id="dd0e6-110">HTTP error logs</span></span>
  * <span data-ttu-id="dd0e6-111">IIS günlükleri</span><span class="sxs-lookup"><span data-stu-id="dd0e6-111">IIS Logs</span></span>
  * <span data-ttu-id="dd0e6-112">Kurulum günlükleri</span><span class="sxs-lookup"><span data-stu-id="dd0e6-112">Setup logs</span></span>
  * <span data-ttu-id="dd0e6-113">diğer sistem günlükleri</span><span class="sxs-lookup"><span data-stu-id="dd0e6-113">other system logs</span></span>

<span data-ttu-id="dd0e6-114">Her iki koleksiyon modlarında yapı izlenerek hello koleksiyonunu kullanarak ek veri koleksiyon klasörleri belirtilebilir:</span><span class="sxs-lookup"><span data-stu-id="dd0e6-114">In both collection modes, additional data collection folders can be specified by using a collection of hello following structure:</span></span>

* <span data-ttu-id="dd0e6-115">**Ad**: hello zip dosyası toobe içinde alt hello adı olarak kullanılacak hello koleksiyonunun hello adı toplanmadı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-115">**Name**: hello name of hello collection, which will be used as hello name of subfolder inside hello zip file toobe collected.</span></span>
* <span data-ttu-id="dd0e6-116">**Konum**: hello sanal makinedeki hello yol toohello klasörünü nereye dosya toplanacak.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-116">**Location**: hello path toohello folder on hello virtual machine where file will be collected.</span></span>
* <span data-ttu-id="dd0e6-117">**SearchPattern**: hello düzeni dosyaları toobe hello adlarının toplanır.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-117">**SearchPattern**: hello pattern of hello names of files toobe collected.</span></span> <span data-ttu-id="dd0e6-118">Varsayılan değer "*"</span><span class="sxs-lookup"><span data-stu-id="dd0e6-118">Default is “*”</span></span>
* <span data-ttu-id="dd0e6-119">**Özyinelemeli**: hello dosyaları hello klasörü altında toplanan yinelemeli olacaksa.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-119">**Recursive**: if hello files will be collected recursively under hello folder.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd0e6-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dd0e6-120">Prerequisites</span></span>
* <span data-ttu-id="dd0e6-121">Uzantı oluşturulan toosave ZIP dosyaları için toohave bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-121">You need toohave a storage account for extension toosave generated zip files.</span></span>
* <span data-ttu-id="dd0e6-122">Azure PowerShell cmdlet'leri V0.8.0 kullandığınızdan emin olmanız gerekir veya üstü.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-122">You must make sure that you are using Azure PowerShell Cmdlets V0.8.0 or above.</span></span> <span data-ttu-id="dd0e6-123">Daha fazla bilgi için bkz: [Azure indirmeleri](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="dd0e6-123">For more information, see [Azure Downloads](https://azure.microsoft.com/downloads/).</span></span>

## <a name="add-hello-extension"></a><span data-ttu-id="dd0e6-124">Merhaba uzantısı Ekle</span><span class="sxs-lookup"><span data-stu-id="dd0e6-124">Add hello extension</span></span>
<span data-ttu-id="dd0e6-125">Kullanabileceğiniz [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet'leri veya [Hizmet Yönetimi REST API'lerine](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector uzantısı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-125">You can use [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlets or [Service Management REST APIs](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector extension.</span></span>

<span data-ttu-id="dd0e6-126">Bulut Hizmetleri için var olan Azure Powershell cmdlet'ini hello **kümesi AzureServiceExtension**, bulut hizmet rolü örneklerinin üzerinde kullanılan tooenable hello uzantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-126">For Cloud Services, hello existing Azure Powershell cmdlet, **Set-AzureServiceExtension**, can be used tooenable hello extension on Cloud Service role instances.</span></span> <span data-ttu-id="dd0e6-127">Bu uzantı Bu cmdlet'i etkinleştirilmiş her zaman, günlük toplama seçili hello rol örneklerinde seçili roller tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-127">Every time this extension is enabled through this cmdlet, log collection is triggered on hello selected role instances of selected roles.</span></span>

<span data-ttu-id="dd0e6-128">Sanal makineler için mevcut Azure Powershell cmdlet'ini hello **kümesi AzureVMExtension**, sanal makinelerde kullanılan tooenable hello uzantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-128">For Virtual Machines, hello existing Azure Powershell cmdlet, **Set-AzureVMExtension**, can be used tooenable hello extension on Virtual Machines.</span></span> <span data-ttu-id="dd0e6-129">Bu uzantı hello cmdlet'leri aracılığıyla etkinleştirilmiş her zaman, günlük toplama her örneğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-129">Every time this extension is enabled through hello cmdlets, log collection is triggered on each instance.</span></span>

<span data-ttu-id="dd0e6-130">Dahili olarak, bu uzantı hello JSON tabanlı PublicConfiguration ve PrivateConfiguration kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-130">Internally, this extension uses hello JSON-based PublicConfiguration and PrivateConfiguration.</span></span> <span data-ttu-id="dd0e6-131">Merhaba, ortak ve özel yapılandırması için örnek JSON hello düzenini aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-131">hello following is hello layout of a sample JSON for public and private configuration.</span></span>

### <a name="publicconfiguration"></a><span data-ttu-id="dd0e6-132">PublicConfiguration</span><span class="sxs-lookup"><span data-stu-id="dd0e6-132">PublicConfiguration</span></span>
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
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

### <a name="privateconfiguration"></a><span data-ttu-id="dd0e6-133">PrivateConfiguration</span><span class="sxs-lookup"><span data-stu-id="dd0e6-133">PrivateConfiguration</span></span>
    {

    }

> [!NOTE]
> <span data-ttu-id="dd0e6-134">Bu uzantının gerekmez **privateConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-134">This extension doesn’t need **privateConfiguration**.</span></span> <span data-ttu-id="dd0e6-135">Merhaba yalnızca boş bir yapı sağlayabilir **– PrivateConfiguration** bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-135">You can just provide an empty structure for hello **–PrivateConfiguration** argument.</span></span>
> 
> 

<span data-ttu-id="dd0e6-136">Merhaba iki birini izleyin adımları tooadd hello AzureLogCollector tooone veya daha fazla örneğini bir bulut hizmeti veya sanal makineye hangi Tetikleyiciler hello her VM toorun koleksiyonunda ve tooAzure hesap hello toplanan dosya gönderme seçili roller Belirtilen.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-136">You can follow one of hello two following steps tooadd hello AzureLogCollector tooone or more instances of a Cloud Service or Virtual Machine of selected roles, which triggers hello collections on each VM toorun and send hello collected files tooAzure account specified.</span></span>

## <a name="adding-as-a-service-extension"></a><span data-ttu-id="dd0e6-137">Bir hizmeti uzantı olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="dd0e6-137">Adding as a Service Extension</span></span>
1. <span data-ttu-id="dd0e6-138">Merhaba yönergeleri tooconnect Azure PowerShell tooyour abonelik izleyin.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-138">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>
2. <span data-ttu-id="dd0e6-139">Merhaba hizmet adı, yuva, rolleri ve rol örnekleri toowhich tooadd istediğiniz ve hello AzureLogCollector uzantısını etkinleştirmek belirtin.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-139">Specify hello service name, slot, roles, and role instances toowhich you want tooadd and enable hello AzureLogCollector extension.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. <span data-ttu-id="dd0e6-140">Dosyaları toplanacak hello ek veri klasörü belirtin (Bu adım isteğe bağlıdır).</span><span class="sxs-lookup"><span data-stu-id="dd0e6-140">Specify hello additional data folder for which files will be collected (this step is optional).</span></span>
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > <span data-ttu-id="dd0e6-141">Belirteci kullanabilirsiniz `%roleroot%` bir sabit sürücü kullanmayan beri toospecify hello rol kök sürücüsünde.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-141">You can use token `%roleroot%` toospecify hello role root drive since it doesn’t use a fixed drive.</span></span>
   > 
   > 
4. <span data-ttu-id="dd0e6-142">Hello Azure depolama hesabı adı ve anahtar toowhich toplanan dosyaları karşıya yüklenebilir sağlayın.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-142">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. <span data-ttu-id="dd0e6-143">Merhaba SetAzureServiceLogCollector.ps1 (Merhaba hello makalenin sonunda yer alan) için bir bulut hizmeti aşağıdaki tooenable hello AzureLogCollector uzantısı olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-143">Call hello SetAzureServiceLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="dd0e6-144">Merhaba yürütme tamamlandığında, yüklenen hello dosyasını altında bulabilirsiniz`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span><span class="sxs-lookup"><span data-stu-id="dd0e6-144">Once hello execution is completed, you can find hello uploaded file under `https://YouareStorageAccountName.blob.core.windows.net/vmlogs`</span></span>
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

<span data-ttu-id="dd0e6-145">Merhaba, toohello komut iletilen hello parametrelerinin hello tanımı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-145">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="dd0e6-146">(Bu aşağıda da kopyalanır.)</span><span class="sxs-lookup"><span data-stu-id="dd0e6-146">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="dd0e6-147">*ServiceName*: Bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-147">*ServiceName*: Your cloud service name.</span></span>
* <span data-ttu-id="dd0e6-148">*Rolleri*: "WebRole1" veya "WorkerRole1" gibi rollerinin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-148">*Roles*: A list of roles, such as “WebRole1” or ”WorkerRole1”.</span></span>
* <span data-ttu-id="dd0e6-149">*Örnekleri*: rol örneklerinin hello adlarının bir listesini virgülle ayrılmış--hello joker karakter dizesi kullanın ("*") tüm rol örnekleri için.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-149">*Instances*: A list of hello names of role instances separated by comma -- use hello wildcard string (“*”) for all role instances.</span></span>
* <span data-ttu-id="dd0e6-150">*Yuva*: Yuva adı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-150">*Slot*: Slot name.</span></span> <span data-ttu-id="dd0e6-151">"Üretim" veya "Hazırlama".</span><span class="sxs-lookup"><span data-stu-id="dd0e6-151">“Production” or “Staging”.</span></span>
* <span data-ttu-id="dd0e6-152">*Mod*: Koleksiyon modu.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-152">*Mode*: Collection mode.</span></span> <span data-ttu-id="dd0e6-153">"Tam" veya "GA".</span><span class="sxs-lookup"><span data-stu-id="dd0e6-153">“Full” or “GA”.</span></span>
* <span data-ttu-id="dd0e6-154">*StorageAccountName*: toplanan verileri depolamak için ad, Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-154">*StorageAccountName*: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="dd0e6-155">*StorageAccountKey*: ad, Azure depolama hesabı anahtarı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-155">*StorageAccountKey*: Name of Azure storage account key.</span></span>
* <span data-ttu-id="dd0e6-156">*AdditionalDataLocationList*: Yapı izlenerek hello listesi:</span><span class="sxs-lookup"><span data-stu-id="dd0e6-156">*AdditionalDataLocationList*: A list of hello following structure:</span></span>
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a><span data-ttu-id="dd0e6-157">Bir VM uzantısı olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="dd0e6-157">Adding as a VM Extension</span></span>
<span data-ttu-id="dd0e6-158">Merhaba yönergeleri tooconnect Azure PowerShell tooyour abonelik izleyin.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-158">Follow hello instructions tooconnect Azure PowerShell tooyour subscription.</span></span>

1. <span data-ttu-id="dd0e6-159">Merhaba hizmet adı, VM ve hello koleksiyon modu belirtin.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-159">Specify hello service name, VM, and hello collection mode.</span></span>
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. <span data-ttu-id="dd0e6-160">Hello Azure depolama hesabı adı ve anahtar toowhich toplanan dosyaları karşıya yüklenebilir sağlayın.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-160">Provide hello Azure storage account name and key toowhich collected files will be uploaded.</span></span>
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. <span data-ttu-id="dd0e6-161">Merhaba SetAzureVMLogCollector.ps1 (Merhaba hello makalenin sonunda yer alan) için bir bulut hizmeti aşağıdaki tooenable hello AzureLogCollector uzantısı olarak çağırın.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-161">Call hello SetAzureVMLogCollector.ps1 (included at hello end of hello article) as follows tooenable hello AzureLogCollector extension for a Cloud Service.</span></span> <span data-ttu-id="dd0e6-162">Merhaba yürütme tamamlandığında, yüklenen hello dosyasını https://YouareStorageAccountName.blob.core.windows.net/vmlogs altında bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="dd0e6-162">Once hello execution is completed, you can find hello uploaded file under https://YouareStorageAccountName.blob.core.windows.net/vmlogs</span></span>

<span data-ttu-id="dd0e6-163">Merhaba, toohello komut iletilen hello parametrelerinin hello tanımı aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-163">hello following is hello definition of hello parameters passed toohello script.</span></span> <span data-ttu-id="dd0e6-164">(Bu aşağıda da kopyalanır.)</span><span class="sxs-lookup"><span data-stu-id="dd0e6-164">(This is copied below as well.)</span></span>

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

* <span data-ttu-id="dd0e6-165">ServiceName: Bulut hizmeti adınız.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-165">ServiceName: Your cloud service name.</span></span>
* <span data-ttu-id="dd0e6-166">Merhaba VM VMName hello adı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-166">VMName hello name of hello VM.</span></span>
* <span data-ttu-id="dd0e6-167">: Koleksiyon modu.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-167">Mode: Collection mode.</span></span> <span data-ttu-id="dd0e6-168">"Tam" veya "GA".</span><span class="sxs-lookup"><span data-stu-id="dd0e6-168">“Full” or “GA”.</span></span>
* <span data-ttu-id="dd0e6-169">StorageAccountName: toplanan verileri depolamak için Azure depolama hesabının adı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-169">StorageAccountName: Name of Azure storage account for storing collected data.</span></span>
* <span data-ttu-id="dd0e6-170">StorageAccountKey: Azure depolama hesabı anahtarı adı.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-170">StorageAccountKey: Name of Azure storage account key.</span></span>
* <span data-ttu-id="dd0e6-171">AdditionalDataLocationList: Listesini yapı izlenerek hello:</span><span class="sxs-lookup"><span data-stu-id="dd0e6-171">AdditionalDataLocationList: A list of hello following structure:</span></span>

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a><span data-ttu-id="dd0e6-172">Uzantı PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="dd0e6-172">Extention PowerShell Script files</span></span>
<span data-ttu-id="dd0e6-173">SetAzureServiceLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="dd0e6-173">SetAzureServiceLogCollector.ps1</span></span>

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
    else  #For all instances if not specified.  hello value should be a space or *
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
    #we need tooget hello Sasuri from StorageAccount and containers
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
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
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
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


<span data-ttu-id="dd0e6-174">SetAzureVMLogCollector.ps1</span><span class="sxs-lookup"><span data-stu-id="dd0e6-174">SetAzureVMLogCollector.ps1</span></span>

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
    #we need tooget hello Sasuri from StorageAccount and containers
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
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
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
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
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
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a><span data-ttu-id="dd0e6-175">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="dd0e6-175">Next Steps</span></span>
<span data-ttu-id="dd0e6-176">Şimdi inceleyin veya çok basit bir konumdan günlüklerinizi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="dd0e6-176">Now you can examine or copy your logs from one very simple location.</span></span>

