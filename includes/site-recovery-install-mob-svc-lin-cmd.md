1. <span data-ttu-id="498f5-101">Merhaba yükleyici tooa sunucusundaki yerel klasör (örneğin, tmp) tooprotect istediğiniz hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="498f5-101">Copy hello installer tooa local folder (for example, /tmp) on hello server that you want tooprotect.</span></span> <span data-ttu-id="498f5-102">Bir terminale hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="498f5-102">In a terminal, run hello following commands:</span></span>
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. <span data-ttu-id="498f5-103">Mobility hizmeti tooinstall hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="498f5-103">tooinstall Mobility Service, run hello following command:</span></span>

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. <span data-ttu-id="498f5-104">Yükleme tamamlandıktan sonra hello Mobility hizmeti tooget kayıtlı toohello yapılandırma sunucusu gerekir.</span><span class="sxs-lookup"><span data-stu-id="498f5-104">Once installation is complete, hello Mobility Service needs tooget registered toohello configuration server.</span></span> <span data-ttu-id="498f5-105">Komut tooregister hello Mobility hizmetinin yapılandırma sunucusu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="498f5-105">Run hello following command tooregister hello Mobility Service with Configuration server.</span></span>

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a><span data-ttu-id="498f5-106">Mobility hizmeti yükleyicisinin komut satırı</span><span class="sxs-lookup"><span data-stu-id="498f5-106">Mobility Service installer command-line</span></span>

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|<span data-ttu-id="498f5-107">Parametre</span><span class="sxs-lookup"><span data-stu-id="498f5-107">Parameter</span></span>|<span data-ttu-id="498f5-108">Tür</span><span class="sxs-lookup"><span data-stu-id="498f5-108">Type</span></span>|<span data-ttu-id="498f5-109">Açıklama</span><span class="sxs-lookup"><span data-stu-id="498f5-109">Description</span></span>|<span data-ttu-id="498f5-110">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="498f5-110">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="498f5-111">-r</span><span class="sxs-lookup"><span data-stu-id="498f5-111">-r</span></span> |<span data-ttu-id="498f5-112">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="498f5-112">Mandatory</span></span>|<span data-ttu-id="498f5-113">Mobility hizmetinin (MS) yüklü olmalıdır veya MasterTarget(MT) yüklenmesi gerektiğini belirtir</span><span class="sxs-lookup"><span data-stu-id="498f5-113">Specifies whether Mobility Service (MS) should be installed or MasterTarget(MT) should be installed</span></span>|<span data-ttu-id="498f5-114">MS</span><span class="sxs-lookup"><span data-stu-id="498f5-114">MS</span></span> </br> <span data-ttu-id="498f5-115">MT</span><span class="sxs-lookup"><span data-stu-id="498f5-115">MT</span></span>|
|<span data-ttu-id="498f5-116">-d</span><span class="sxs-lookup"><span data-stu-id="498f5-116">-d</span></span> |<span data-ttu-id="498f5-117">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="498f5-117">Optional</span></span>|<span data-ttu-id="498f5-118">Mobility hizmetinin yükleneceği konum</span><span class="sxs-lookup"><span data-stu-id="498f5-118">Location where Mobility Service will be installed</span></span>|<span data-ttu-id="498f5-119">/usr/local/ASR</span><span class="sxs-lookup"><span data-stu-id="498f5-119">/usr/local/ASR</span></span>|
|<span data-ttu-id="498f5-120">-v</span><span class="sxs-lookup"><span data-stu-id="498f5-120">-v</span></span>|<span data-ttu-id="498f5-121">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="498f5-121">Mandatory</span></span>|<span data-ttu-id="498f5-122">Merhaba platformu üzerinde hangi hello mobilite hizmeti yüklü belirtir</span><span class="sxs-lookup"><span data-stu-id="498f5-122">Specifies hello platform on which hello Mobility Service is getting installed</span></span> </br> </br><span data-ttu-id="498f5-123">- **VMware** : mobility hizmeti üzerinde çalışan bir VM yüklüyorsanız bu değeri kullanın *VMware vSphere ESXi konakları*, *Hyper-V konakları* ve *Phsyical sunucuları*</span><span class="sxs-lookup"><span data-stu-id="498f5-123">- **VMware** : use this value if you are installing mobility service on a VM running on *VMware vSphere ESXi Hosts*, *Hyper-V Hosts* and *Phsyical Servers*</span></span> </br> <span data-ttu-id="498f5-124">- **Azure** : bir Azure Iaas VM aracısı yüklüyorsanız, bu değeri kullanın</span><span class="sxs-lookup"><span data-stu-id="498f5-124">- **Azure** : use this value if you are installing agent on a Azure IaaS VM</span></span>| <span data-ttu-id="498f5-125">VMware</span><span class="sxs-lookup"><span data-stu-id="498f5-125">VMware</span></span> </br> <span data-ttu-id="498f5-126">Azure</span><span class="sxs-lookup"><span data-stu-id="498f5-126">Azure</span></span>|
|<span data-ttu-id="498f5-127">-q</span><span class="sxs-lookup"><span data-stu-id="498f5-127">-q</span></span>|<span data-ttu-id="498f5-128">İsteğe bağlı</span><span class="sxs-lookup"><span data-stu-id="498f5-128">Optional</span></span>|<span data-ttu-id="498f5-129">Sessiz modda toorun yükleyici belirtir</span><span class="sxs-lookup"><span data-stu-id="498f5-129">Specifies toorun installer in silent mode</span></span>| <span data-ttu-id="498f5-130">Yok</span><span class="sxs-lookup"><span data-stu-id="498f5-130">N/A</span></span>|


#### <a name="mobility-service-configuration-command-line"></a><span data-ttu-id="498f5-131">Mobility hizmeti yapılandırma komut satırı</span><span class="sxs-lookup"><span data-stu-id="498f5-131">Mobility Service configuration command-line</span></span>

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|<span data-ttu-id="498f5-132">Parametre</span><span class="sxs-lookup"><span data-stu-id="498f5-132">Parameter</span></span>|<span data-ttu-id="498f5-133">Tür</span><span class="sxs-lookup"><span data-stu-id="498f5-133">Type</span></span>|<span data-ttu-id="498f5-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="498f5-134">Description</span></span>|<span data-ttu-id="498f5-135">Olası değerler</span><span class="sxs-lookup"><span data-stu-id="498f5-135">Possible values</span></span>|
|-|-|-|-|
|<span data-ttu-id="498f5-136">-i</span><span class="sxs-lookup"><span data-stu-id="498f5-136">-i</span></span> |<span data-ttu-id="498f5-137">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="498f5-137">Mandatory</span></span>|<span data-ttu-id="498f5-138">Merhaba yapılandırma sunucusu IP</span><span class="sxs-lookup"><span data-stu-id="498f5-138">IP of hello Configuration Server</span></span>|<span data-ttu-id="498f5-139">Herhangi bir geçerli IP adresi</span><span class="sxs-lookup"><span data-stu-id="498f5-139">Any valid IP Address</span></span>|
|<span data-ttu-id="498f5-140">-P</span><span class="sxs-lookup"><span data-stu-id="498f5-140">-P</span></span> |<span data-ttu-id="498f5-141">Zorunlu</span><span class="sxs-lookup"><span data-stu-id="498f5-141">Mandatory</span></span>|<span data-ttu-id="498f5-142">Merhaba bağlantı parola kaydedildiği tam yol hello dosyası</span><span class="sxs-lookup"><span data-stu-id="498f5-142">Full file path hello file where hello connection passphrase is saved</span></span>|<span data-ttu-id="498f5-143">Geçerli bir klasör</span><span class="sxs-lookup"><span data-stu-id="498f5-143">Any valid folder</span></span>|
