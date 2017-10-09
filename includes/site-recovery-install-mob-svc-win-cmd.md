1. <span data-ttu-id="c1f0f-101">Merhaba yükleyici tooa yerel klasöre (örneğin, C:\Temp) tooprotect istediğiniz hello sunucusuna kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c1f0f-101">Copy hello installer tooa local folder (for example, C:\Temp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="c1f0f-102">Komutlar bir yönetici komut isteminde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c1f0f-102">Run hello following commands as an administrator at a command prompt:</span></span>

  ```
  cd C:\Temp
  ren Microsoft-ASR_UA*Windows*release.exe MobilityServiceInstaller.exe
  MobilityServiceInstaller.exe /q /x:C:\Temp\Extracted
  cd C:\Temp\Extracted.
  ```
2. <span data-ttu-id="c1f0f-103">Mobility hizmeti tooinstall hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c1f0f-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  UnifiedAgent.exe /Role "MS" /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
  ```
3. <span data-ttu-id="c1f0f-104">Şimdi hello aracının hello yapılandırma sunucusu ile kayıtlı toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="c1f0f-104">Now hello agent needs toobe registered with hello Configuration Server.</span></span>

  ```
  cd C:\Program Files (x86)\Microsoft Azure Site Recovery\agent
  UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
  ```

#### <a name="mobility-service-installer-command-line-arguments"></a><span data-ttu-id="c1f0f-105">Mobility Hizmeti Yükleyici komut satırı bağımsız değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c1f0f-105">Mobility Service installer command-line arguments</span></span>

```
Usage :
UnifiedAgent.exe /Role <MS|MT> /InstallLocation <Install Location> /Platform “VmWare” /Silent
```

| <span data-ttu-id="c1f0f-106">Parametre</span><span class="sxs-lookup"><span data-stu-id="c1f0f-106">Parameter</span></span>|<span data-ttu-id="c1f0f-107">Tür</span><span class="sxs-lookup"><span data-stu-id="c1f0f-107">Type</span></span>|<span data-ttu-id="c1f0f-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c1f0f-108">Description</span></span>|<span data-ttu-id="c1f0f-109">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="c1f0f-109">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="c1f0f-110">/ Rol</span><span class="sxs-lookup"><span data-stu-id="c1f0f-110">/Role</span></span>|<span data-ttu-id="c1f0f-111">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-111">Mandatory</span></span>|<span data-ttu-id="c1f0f-112">Mobility hizmetinin (MS) yüklü olmalıdır veya MasterTarget(MT) yüklenmesi gerektiğini belirtir</span><span class="sxs-lookup"><span data-stu-id="c1f0f-112">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="c1f0f-113">MS</span><span class="sxs-lookup"><span data-stu-id="c1f0f-113">MS</span></span> </br> <span data-ttu-id="c1f0f-114">MT</span><span class="sxs-lookup"><span data-stu-id="c1f0f-114">MT</span></span>|
|<span data-ttu-id="c1f0f-115">/InstallLocation</span><span class="sxs-lookup"><span data-stu-id="c1f0f-115">/InstallLocation</span></span>|<span data-ttu-id="c1f0f-116">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c1f0f-116">Optional</span></span>|<span data-ttu-id="c1f0f-117">Mobility Hizmeti'nin yüklendiği konumu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-117">Location where Mobility Service is installed</span></span>|<span data-ttu-id="c1f0f-118">Merhaba bilgisayarda herhangi bir klasör</span><span class="sxs-lookup"><span data-stu-id="c1f0f-118">Any folder on hello computer</span></span>|
|<span data-ttu-id="c1f0f-119">/ Platform</span><span class="sxs-lookup"><span data-stu-id="c1f0f-119">/Platform</span></span>|<span data-ttu-id="c1f0f-120">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-120">Mandatory</span></span>|<span data-ttu-id="c1f0f-121">Merhaba platformu üzerinde hangi hello mobilite hizmeti yüklü belirtir</span><span class="sxs-lookup"><span data-stu-id="c1f0f-121">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="c1f0f-122">- **VMware** : mobility hizmeti üzerinde çalışan bir VM yüklüyorsanız bu değeri kullanın *VMware vSphere ESXi konakları*, *Hyper-V konakları* ve *Phsyical sunucuları*</span><span class="sxs-lookup"><span data-stu-id="c1f0f-122">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="c1f0f-123">- **Azure** : bir Azure Iaas VM aracısı yüklüyorsanız, bu değeri kullanın</span><span class="sxs-lookup"><span data-stu-id="c1f0f-123">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="c1f0f-124">VMware</span><span class="sxs-lookup"><span data-stu-id="c1f0f-124">VMware</span></span> </br> <span data-ttu-id="c1f0f-125">Azure</span><span class="sxs-lookup"><span data-stu-id="c1f0f-125">Azure</span></span>|
|<span data-ttu-id="c1f0f-126">/ Sessiz</span><span class="sxs-lookup"><span data-stu-id="c1f0f-126">/Silent</span></span>|<span data-ttu-id="c1f0f-127">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="c1f0f-127">Optional</span></span>|<span data-ttu-id="c1f0f-128">Sessiz modda toorun hello yükleyici belirtir</span><span class="sxs-lookup"><span data-stu-id="c1f0f-128">Specifies toorun hello installer in silent mode</span></span>| <span data-ttu-id="c1f0f-129">NA</span><span class="sxs-lookup"><span data-stu-id="c1f0f-129">NA</span></span>|

>[!TIP]
> <span data-ttu-id="c1f0f-130">Merhaba Kurulum günlüklerini %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c1f0f-130">hello setup logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentInstaller.log</span></span>

#### <a name="mobility-service-registration-command-line-arguments"></a><span data-ttu-id="c1f0f-131">Mobility hizmeti kayıt komut satırı bağımsız değişkenleri</span><span class="sxs-lookup"><span data-stu-id="c1f0f-131">Mobility Service registration command-line arguments</span></span>

```
Usage :
UnifiedAgentConfigurator.exe”  /CSEndPoint <CSIP> /PassphraseFilePath <PassphraseFilePath>
```

  | <span data-ttu-id="c1f0f-132">Parametre</span><span class="sxs-lookup"><span data-stu-id="c1f0f-132">Parameter</span></span>|<span data-ttu-id="c1f0f-133">Tür</span><span class="sxs-lookup"><span data-stu-id="c1f0f-133">Type</span></span>|<span data-ttu-id="c1f0f-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c1f0f-134">Description</span></span>|<span data-ttu-id="c1f0f-135">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="c1f0f-135">Possible values</span></span>|
  |-|-|-|-|
  |<span data-ttu-id="c1f0f-136">/ CSEndPoint</span><span class="sxs-lookup"><span data-stu-id="c1f0f-136">/CSEndPoint</span></span> |<span data-ttu-id="c1f0f-137">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-137">Mandatory</span></span>|<span data-ttu-id="c1f0f-138">Merhaba yapılandırma sunucusu IP adresi</span><span class="sxs-lookup"><span data-stu-id="c1f0f-138">IP address of hello configuration server</span></span>| <span data-ttu-id="c1f0f-139">Geçerli bir IP adresi</span><span class="sxs-lookup"><span data-stu-id="c1f0f-139">Any valid IP address</span></span>|
  |<span data-ttu-id="c1f0f-140">/PassphraseFilePath</span><span class="sxs-lookup"><span data-stu-id="c1f0f-140">/PassphraseFilePath</span></span>|<span data-ttu-id="c1f0f-141">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-141">Mandatory</span></span>|<span data-ttu-id="c1f0f-142">Merhaba parola konumu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-142">Location of hello passphrase</span></span> |<span data-ttu-id="c1f0f-143">Herhangi bir geçerli UNC veya yerel dosya yolu</span><span class="sxs-lookup"><span data-stu-id="c1f0f-143">Any valid UNC or local file path</span></span>|


>[!TIP]
> <span data-ttu-id="c1f0f-144">Merhaba AgentConfiguration günlükleri %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="c1f0f-144">hello AgentConfiguration logs can be found under %ProgramData%\ASRSetupLogs\ASRUnifiedAgentConfigurator.log</span></span>
