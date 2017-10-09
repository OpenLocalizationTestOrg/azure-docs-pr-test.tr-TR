


## <a name="using-vm-extensions"></a><span data-ttu-id="bd485-101">VM uzantıları kullanma</span><span class="sxs-lookup"><span data-stu-id="bd485-101">Using VM Extensions</span></span>
<span data-ttu-id="bd485-102">Azure VM uzantıları uygulamak davranışları veya ya da Azure Vm'lerde iş diğer programları yardımcı olan özellikleri (örneğin, hello **WebDeployForVSDevTest** uzantısı, Azure VM dağıtma çözümleri Visual Studio tooWeb sağlar) veya sağlayın başka bir davranışı, toointeract hello VM toosupport ile yeteneği hello (örneğin, PowerShell, hello Azure CLI ve REST istemcileri tooreset hello VM erişimi uzantılarını kullanıyorsanız veya uzaktan erişim değerleri, Azure VM'deki değiştirmek için).</span><span class="sxs-lookup"><span data-stu-id="bd485-102">Azure VM Extensions implement behaviors or features that either help other programs work on Azure VMs (for example, hello **WebDeployForVSDevTest** extension allows Visual Studio tooWeb Deploy solutions on your Azure VM) or provide hello ability for you toointeract with hello VM toosupport some other behavior (for example, you can use hello VM Access extensions from PowerShell, hello Azure CLI, and REST clients tooreset or modify remote access values on your Azure VM).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd485-103">Uzantılar destekledikleri hello özellikleri için tam bir listesi için bkz: [Azure VM uzantıları ve özellikleri](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd485-103">For a complete list of extensions by hello features they support, see [Azure VM Extensions and Features](../articles/virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="bd485-104">Her VM uzantısı belirli bir özelliği desteklediğinden, tam olarak ne yapıp uzantılı olamaz hello uzantısı bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="bd485-104">Because each VM extension supports a specific feature, exactly what you can and cannot do with an extension depends on hello extension.</span></span> <span data-ttu-id="bd485-105">Bu nedenle, VM değiştirmeden önce hello toouse istediğiniz VM uzantısı için hello belgelerini okuma emin olun.</span><span class="sxs-lookup"><span data-stu-id="bd485-105">Therefore, before modifying your VM, make sure you have read hello documentation for hello VM Extension you want toouse.</span></span> <span data-ttu-id="bd485-106">Bazı VM uzantıları kaldırma desteklenmiyor; diğer VM davranışı tüketicisinin değiştirmek ayarlanabilir özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bd485-106">Removing some VM Extensions is not supported; others have properties that can be set that change VM behavior radically.</span></span>
> 
> 

<span data-ttu-id="bd485-107">Merhaba en yaygın görevleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bd485-107">hello most common tasks are:</span></span>

1. <span data-ttu-id="bd485-108">Kullanılabilir uzantılar bulma</span><span class="sxs-lookup"><span data-stu-id="bd485-108">Finding Available Extensions</span></span>
2. <span data-ttu-id="bd485-109">Yüklenen uzantıları güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="bd485-109">Updating Loaded Extensions</span></span>
3. <span data-ttu-id="bd485-110">Uzantılar ekleme</span><span class="sxs-lookup"><span data-stu-id="bd485-110">Adding Extensions</span></span>
4. <span data-ttu-id="bd485-111">Uzantılarını kaldırma</span><span class="sxs-lookup"><span data-stu-id="bd485-111">Removing Extensions</span></span>

## <a name="find-available-extensions"></a><span data-ttu-id="bd485-112">Kullanılabilir uzantılar bulun</span><span class="sxs-lookup"><span data-stu-id="bd485-112">Find Available Extensions</span></span>
<span data-ttu-id="bd485-113">Uzantı ve genişletilmiş bilgileri kullanarak bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd485-113">You can locate extension and extended information using:</span></span>

* <span data-ttu-id="bd485-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd485-114">PowerShell</span></span>
* <span data-ttu-id="bd485-115">Azure platformlar arası komut satırı arabirimi (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="bd485-115">Azure Cross-Platform Command Line Interface (Azure CLI)</span></span>
* <span data-ttu-id="bd485-116">Hizmet Yönetimi REST API'si</span><span class="sxs-lookup"><span data-stu-id="bd485-116">Service Management REST API</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="bd485-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd485-117">Azure PowerShell</span></span>
<span data-ttu-id="bd485-118">Bazı uzantılar yapılandırmalarını Powershell'den daha kolay hale getirebilir belirli toothem olan PowerShell cmdlet'leri; yine de sahip istiyor musunuz? ancak hello aşağıdaki cmdlet'leri çalışması için tüm VM uzantıları.</span><span class="sxs-lookup"><span data-stu-id="bd485-118">Some extensions have PowerShell cmdlets that are specific toothem, which may make their configuration from PowerShell easier; but hello following cmdlets work for all VM extensions.</span></span>

<span data-ttu-id="bd485-119">Kullanılabilir uzantılar hakkında cmdlet'leri tooobtain bilgi aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd485-119">You can use hello following cmdlets tooobtain information about available extensions:</span></span>

* <span data-ttu-id="bd485-120">İçin örnek web rolleri veya çalışan rolleri, hello kullanabilirsiniz [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd485-120">For instances of web roles or worker roles, you can use hello [Get-AzureServiceAvailableExtension](https://msdn.microsoft.com/library/azure/dn722498.aspx) cmdlet.</span></span>
* <span data-ttu-id="bd485-121">İçin örnekleri sanal makinelerin hello kullanabilirsiniz [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd485-121">For instances of Virtual Machines, you can use hello [Get-AzureVMAvailableExtension](https://msdn.microsoft.com/library/azure/dn722480.aspx) cmdlet.</span></span>
  
   <span data-ttu-id="bd485-122">Örneğin, kod örnekteki nasıl aşağıdaki hello toolist hello bilgilerini **IaaSDiagnostics** PowerShell kullanarak uzantısı.</span><span class="sxs-lookup"><span data-stu-id="bd485-122">For example, hello following code example shows how toolist the information for hello **IaaSDiagnostics** extension using PowerShell.</span></span>
  
      PS C:\> Get-AzureVMAvailableExtension -ExtensionName IaaSDiagnostics
  
      Publisher                   : Microsoft.Azure.Diagnostics
      ExtensionName               : IaaSDiagnostics
      Version                     : 1.2
      Label                       : Microsoft Monitoring Agent Diagnostics
      Description                 : Microsoft Monitoring Agent Extension
      PublicConfigurationSchema   :
      PrivateConfigurationSchema  :
      IsInternalExtension         : False
      SampleConfig                :
      ReplicationCompleted        : True
      Eula                        :
      PrivacyUri                  :
      HomepageUri                 :
      IsJsonExtension             : True
      DisallowMajorVersionUpgrade : False
      SupportedOS                 :
      PublishedDate               :
      CompanyName                 :

### <a name="azure-command-line-interface-azure-cli"></a><span data-ttu-id="bd485-123">Azure komut satırı arabirimi (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="bd485-123">Azure Command Line Interface (Azure CLI)</span></span>
<span data-ttu-id="bd485-124">Belirli toothem olan Azure CLI komutlarının bazı uzantılı (Merhaba Docker VM uzantısı olan bir örnek) yapılandırmalarını daha kolay hale getirebilir; ancak tüm VM uzantıları için iş hello aşağıdaki komutları.</span><span class="sxs-lookup"><span data-stu-id="bd485-124">Some extensions have Azure CLI commands that are specific toothem (hello Docker VM Extension is one example), which may make their configuration easier; but hello following commands work for all VM extensions.</span></span>

<span data-ttu-id="bd485-125">Merhaba kullanabilirsiniz **azure vm uzantısı listesinde** komutu kullanılabilir uzantıları tooobtain bilgilerini ve hello kullan **–-json** bir veya daha fazla uzantıları hakkında tüm kullanılabilir bilgi toodisplay seçeneği.</span><span class="sxs-lookup"><span data-stu-id="bd485-125">You can use hello **azure vm extension list** command tooobtain information about available extensions, and use hello **–-json** option toodisplay all available information about one or more extensions.</span></span> <span data-ttu-id="bd485-126">Bir uzantı adı kullanmıyorsanız hello komut tüm kullanılabilir uzantıları JSON açıklamasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="bd485-126">If you do not use an extension name, hello command returns a JSON description of all available extensions.</span></span>

<span data-ttu-id="bd485-127">Örneğin, aşağıdaki kod örneğine hello nasıl toolist hello bilgi hello için gösterir **IaaSDiagnostics** uzantısını kullanarak hello Azure CLI **azure vm uzantısı listesinde** komut ve kullandığı hello **–-json** seçeneği tooreturn tam bilgi.</span><span class="sxs-lookup"><span data-stu-id="bd485-127">For example, hello following code example shows how toolist hello information for hello **IaaSDiagnostics** extension using hello Azure CLI **azure vm extension list** command and uses hello **–-json** option tooreturn complete information.</span></span>

    $ azure vm extension list -n IaaSDiagnostics --json
    [
      {
        "publisher": "Microsoft.Azure.Diagnostics",
        "name": "IaaSDiagnostics",
        "version": "1.2",
        "label": "Microsoft Monitoring Agent Diagnostics",
        "description": "Microsoft Monitoring Agent Extension",
        "replicationCompleted": true,
        "isJsonExtension": true
      }
    ]



### <a name="service-management-rest-apis"></a><span data-ttu-id="bd485-128">Hizmet Yönetimi REST API'leri</span><span class="sxs-lookup"><span data-stu-id="bd485-128">Service Management REST APIs</span></span>
<span data-ttu-id="bd485-129">Kullanılabilir uzantılar hakkında REST API'leri tooobtain bilgi aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd485-129">You can use hello following REST APIs tooobtain information about available extensions:</span></span>

* <span data-ttu-id="bd485-130">İçin örnek web rolleri veya çalışan rolleri, hello kullanabilirsiniz [listesi kullanılabilir uzantıları](https://msdn.microsoft.com/library/dn169559.aspx) işlemi.</span><span class="sxs-lookup"><span data-stu-id="bd485-130">For instances of web roles or worker roles, you can use hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span> <span data-ttu-id="bd485-131">kullanabileceğiniz hello sürümlerinde kullanılabilir uzantıları toolist, [listesi uzantısı sürümleri](https://msdn.microsoft.com/library/dn495437.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd485-131">toolist hello versions of available extensions, you can use [List Extension Versions](https://msdn.microsoft.com/library/dn495437.aspx).</span></span>
* <span data-ttu-id="bd485-132">İçin örnekleri sanal makinelerin hello kullanabilirsiniz [listesi kaynak uzantıları](https://msdn.microsoft.com/library/dn495441.aspx) işlemi.</span><span class="sxs-lookup"><span data-stu-id="bd485-132">For instances of Virtual Machines, you can use hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span> <span data-ttu-id="bd485-133">kullanabileceğiniz hello sürümlerinde kullanılabilir uzantıları toolist, [listesi kaynak uzantısı sürümleri](https://msdn.microsoft.com/library/dn495440.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd485-133">toolist hello versions of available extensions, you can use [List Resource Extension Versions](https://msdn.microsoft.com/library/dn495440.aspx).</span></span>

## <a name="add-update-or-disable-extensions"></a><span data-ttu-id="bd485-134">Ekleme, güncelleştirme ya da uzantılarını devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="bd485-134">Add, Update, or Disable Extensions</span></span>
<span data-ttu-id="bd485-135">Uzantıları örneği oluşturulduğunda veya örneğini çalıştıran tooa eklenebilir eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="bd485-135">Extensions can be added when an instance is created or they can be added tooa running instance.</span></span> <span data-ttu-id="bd485-136">Uzantıları güncelleştirildi, devre dışı veya kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bd485-136">Extensions can be updated, disabled, or removed.</span></span> <span data-ttu-id="bd485-137">Azure PowerShell cmdlet'lerini kullanarak veya hello Hizmet Yönetimi REST API işlemleri kullanarak bu eylemleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="bd485-137">You can perform these actions by using Azure PowerShell cmdlets or by using hello Service Management REST API operations.</span></span> <span data-ttu-id="bd485-138">Parametreler gerekli tooinstall ve bazı uzantıların ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bd485-138">Parameters are required tooinstall and set up some extensions.</span></span> <span data-ttu-id="bd485-139">Ortak ve özel parametreleri uzantılar için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bd485-139">Public and private parameters are supported for extensions.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="bd485-140">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd485-140">Azure PowerShell</span></span>
<span data-ttu-id="bd485-141">Azure PowerShell cmdlet'lerini kullanarak hello en kolay yolu tooadd ve güncelleştirme uzantıları değildir.</span><span class="sxs-lookup"><span data-stu-id="bd485-141">Using Azure PowerShell cmdlets is hello easiest way tooadd and update extensions.</span></span> <span data-ttu-id="bd485-142">Merhaba uzantısı cmdlet'leri kullandığınızda, hello uzantısının hello yapılandırmasının çoğu yapılır sizin için.</span><span class="sxs-lookup"><span data-stu-id="bd485-142">When you use hello extension cmdlets, most of hello configuration of hello extension is done for you.</span></span> <span data-ttu-id="bd485-143">Bazen gerekebilir tooprogrammatically uzantı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd485-143">At times, you may need tooprogrammatically add an extension.</span></span> <span data-ttu-id="bd485-144">Bu toodo gerektiğinde Merhaba uzantısı hello yapılandırmasını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd485-144">When you need toodo this, you must provide hello configuration of hello extension.</span></span>

<span data-ttu-id="bd485-145">Uzantı genel ve özel parametrelerinin yapılandırması sağlanıp sağlanmadığını cmdlet'leri tooknow aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd485-145">You can use hello following cmdlets tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="bd485-146">İçin örnek web rolleri veya çalışan rolleri, hello kullanabilirsiniz **Get-AzureServiceAvailableExtension** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd485-146">For instances of web roles or worker roles, you can use hello **Get-AzureServiceAvailableExtension** cmdlet.</span></span>
* <span data-ttu-id="bd485-147">İçin örnekleri sanal makinelerin hello kullanabilirsiniz **Get-AzureVMAvailableExtension** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bd485-147">For instances of Virtual Machines, you can use hello **Get-AzureVMAvailableExtension** cmdlet.</span></span>

### <a name="service-management-rest-apis"></a><span data-ttu-id="bd485-148">Hizmet Yönetimi REST API'leri</span><span class="sxs-lookup"><span data-stu-id="bd485-148">Service Management REST APIs</span></span>
<span data-ttu-id="bd485-149">Merhaba REST API'lerini kullanarak kullanılabilir uzantıları listesini almak için yapılandırılmış toobe hello uzantısı nasıl olduğu hakkında bilgi alıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="bd485-149">When you retrieve a listing of available extensions by using hello REST APIs, you receive information about how hello extension is toobe configured.</span></span> <span data-ttu-id="bd485-150">döndürülen hello bilgi ortak şema ve özel şema tarafından temsil edilen parametre bilgilerini gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="bd485-150">hello information that is returned might show parameter information represented by a public schema and private schema.</span></span> <span data-ttu-id="bd485-151">Ortak parametre değerlerini hello örnekleri hakkında sorgularda döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bd485-151">Public parameter values are returned in queries about hello instances.</span></span> <span data-ttu-id="bd485-152">Özel parametre değerlerini döndürülmez.</span><span class="sxs-lookup"><span data-stu-id="bd485-152">Private parameter values are not returned.</span></span>

<span data-ttu-id="bd485-153">Uzantı genel ve özel parametrelerinin yapılandırması sağlanıp sağlanmadığını REST API'leri tooknow aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bd485-153">You can use hello following REST APIs tooknow whether an extension requires a configuration of public and private parameters:</span></span>

* <span data-ttu-id="bd485-154">İçin web rolleri veya çalışan rolleri örneklerini hello **PublicConfigurationSchema** ve **PrivateConfigurationSchema** öğeleri içeren hello hello yanıttan hello bilgileri [listesi Kullanılabilir uzantılar](https://msdn.microsoft.com/library/dn169559.aspx) işlemi.</span><span class="sxs-lookup"><span data-stu-id="bd485-154">For instances of web roles or worker roles, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Available Extensions](https://msdn.microsoft.com/library/dn169559.aspx) operation.</span></span>
* <span data-ttu-id="bd485-155">İçin sanal makine örneklerini hello **PublicConfigurationSchema** ve **PrivateConfigurationSchema** öğeleri içeren hello hello yanıttan hello bilgileri [listesi Kaynak uzantıları](https://msdn.microsoft.com/library/dn495441.aspx) işlemi.</span><span class="sxs-lookup"><span data-stu-id="bd485-155">For instances of Virtual Machines, hello **PublicConfigurationSchema** and **PrivateConfigurationSchema** elements contain hello information in hello response from hello [List Resource Extensions](https://msdn.microsoft.com/library/dn495441.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="bd485-156">Uzantılar, JSON ile tanımlanan yapılandırmaları da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd485-156">Extensions can also use configurations that are defined with JSON.</span></span> <span data-ttu-id="bd485-157">Bu uzantı türlerini kullanıldığında, yalnızca hello **SampleConfig** öğe kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd485-157">When these types of extensions are used, only hello **SampleConfig** element is used.</span></span>
> 
> 

