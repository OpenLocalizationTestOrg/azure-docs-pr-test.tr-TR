1. <span data-ttu-id="66928-101">Yükleyici, korumak istediğiniz sunucuda yerel bir klasöre (örneğin, C:\Temp) kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="66928-101">Copy the installer to a local folder (for example, C:\Temp) on the server that you want to protect.</span></span> <span data-ttu-id="66928-102">Bir yönetici komut isteminde aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="66928-102">Run the following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="66928-103">Mobilite hizmetinin yüklenmesi için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="66928-103">To install Mobility Service, run the following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="66928-104">Şimdi aracı yapılandırma sunucusuna kayıtlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="66928-104">Now the agent needs to be registered with the Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="66928-105">Mobility Hizmeti Yükleyici komut satırı bağımsız değişkenleri</span><span class="sxs-lookup"><span data-stu-id="66928-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="66928-106">Parametre</span><span class="sxs-lookup"><span data-stu-id="66928-106">Parameter</span></span>|<span data-ttu-id="66928-107">Tür</span><span class="sxs-lookup"><span data-stu-id="66928-107">Type</span></span>|<span data-ttu-id="66928-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66928-108">Description</span></span>|<span data-ttu-id="66928-109">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="66928-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="66928-110">/ Rol</span><span class="sxs-lookup"><span data-stu-id="66928-110">/Role</span></span>|<span data-ttu-id="66928-111">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="66928-111">Mandatory</span></span>|<span data-ttu-id="66928-112">Mobility hizmetinin (MS) yüklü olmalıdır veya MasterTarget(MT) yüklenmesi gerektiğini belirtir</span><span class="sxs-lookup"><span data-stu-id="66928-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="66928-113">MS</span><span class="sxs-lookup"><span data-stu-id="66928-113">MS</span></span> </br> <span data-ttu-id="66928-114">MT</span><span class="sxs-lookup"><span data-stu-id="66928-114">MT</span></span>|
|<span data-ttu-id="66928-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="66928-115">/InstallLocation</span></span>|<span data-ttu-id="66928-116">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="66928-116">Optional</span></span>|<span data-ttu-id="66928-117">Mobility Hizmeti'nin yüklendiği konumu</span><span class="sxs-lookup"><span data-stu-id="66928-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="66928-118">Bilgisayardaki herhangi bir klasör</span><span class="sxs-lookup"><span data-stu-id="66928-118">Any folder on the computer</span></span>|
|<span data-ttu-id="66928-119">/ Platform</span><span class="sxs-lookup"><span data-stu-id="66928-119">/Platform</span></span>|<span data-ttu-id="66928-120">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="66928-120">Mandatory</span></span>|<span data-ttu-id="66928-121">Mobility hizmetinin yüklendiği platformu belirtir</span><span class="sxs-lookup"><span data-stu-id="66928-121">Specifies the platform on which the Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="66928-122">- **VMware** : mobility hizmeti üzerinde çalışan bir VM yüklüyorsanız bu değeri kullanın *VMware vSphere ESXi konakları*, *Hyper-V konakları* ve *Phsyical sunucuları*</span><span class="sxs-lookup"><span data-stu-id="66928-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="66928-123">- **Azure** : bir Azure Iaas VM aracısı yüklüyorsanız, bu değeri kullanın</span><span class="sxs-lookup"><span data-stu-id="66928-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="66928-124">VMware</span><span class="sxs-lookup"><span data-stu-id="66928-124">VMware</span></span> </br> <span data-ttu-id="66928-125">Azure</span><span class="sxs-lookup"><span data-stu-id="66928-125">Azure</span></span>|
|<span data-ttu-id="66928-126">/ Sessiz</span><span class="sxs-lookup"><span data-stu-id="66928-126">/Silent</span></span>|<span data-ttu-id="66928-127">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="66928-127">Optional</span></span>|<span data-ttu-id="66928-128">Yükleyici sessiz modda çalıştırmak için belirtir</span><span class="sxs-lookup"><span data-stu-id="66928-128">Specifies to run the installer in silent mode</span></span>| <span data-ttu-id="66928-129">NA</span><span class="sxs-lookup"><span data-stu-id="66928-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="66928-130">Kurulum günlüklerini %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="66928-130">The setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="66928-131">Mobility hizmeti kayıt komut satırı bağımsız değişkenleri</span><span class="sxs-lookup"><span data-stu-id="66928-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="66928-132">Parametre</span><span class="sxs-lookup"><span data-stu-id="66928-132">Parameter</span></span>|<span data-ttu-id="66928-133">Tür</span><span class="sxs-lookup"><span data-stu-id="66928-133">Type</span></span>|<span data-ttu-id="66928-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="66928-134">Description</span></span>|<span data-ttu-id="66928-135">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="66928-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="66928-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="66928-136">/CSEndPoint</span></span> |<span data-ttu-id="66928-137">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="66928-137">Mandatory</span></span>|<span data-ttu-id="66928-138">Yapılandırma sunucusu IP adresi</span><span class="sxs-lookup"><span data-stu-id="66928-138">IP address of the configuration server</span></span>| <span data-ttu-id="66928-139">Geçerli bir IP adresi</span><span class="sxs-lookup"><span data-stu-id="66928-139">Any valid IP address</span></span>|
  |<span data-ttu-id="66928-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="66928-140">/PassphraseFilePath</span></span>|<span data-ttu-id="66928-141">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="66928-141">Mandatory</span></span>|<span data-ttu-id="66928-142">Parola konumu</span><span class="sxs-lookup"><span data-stu-id="66928-142">Location of the passphrase</span></span> |<span data-ttu-id="66928-143">Herhangi bir geçerli UNC veya yerel dosya yolu</span><span class="sxs-lookup"><span data-stu-id="66928-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="66928-144">AgentConfiguration günlükleri %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="66928-144">The AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
