---
title: "Yazılım dağıtım araçları kullanarak Azure Site Recovery Mobility hizmeti yüklemesi otomatikleştirmek | Microsoft Docs"
description: "Bu makalede, System Center Configuration Manager gibi yazılım dağıtım araçları kullanarak Mobility hizmetinin yüklenmesini otomatikleştirmek yardımcı olur."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="63465-103">Yazılım dağıtım araçları kullanarak mobilite hizmeti yükleme otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="63465-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="63465-104">Bu belge sürümü kullandığınız varsayılır **9.9.4510.1** ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="63465-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="63465-105">Bu makalede, Azure Site Recovery Mobility hizmeti, veri merkezinizde dağıtmak için System Center Configuration Manager nasıl kullanabileceğinize bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="63465-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="63465-106">Configuration Manager'ı aşağıdaki avantajlara sahip gibi bir yazılım dağıtım aracını kullanma:</span><span class="sxs-lookup"><span data-stu-id="63465-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="63465-107">Yazılım güncelleştirmeleri için planlanan bakım penceresi sırasında yeni yüklemeleri ve yükseltmeleri, dağıtımını planlama</span><span class="sxs-lookup"><span data-stu-id="63465-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="63465-108">Yüzlerce dağıtımına aynı anda ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="63465-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="63465-109">Bu makalede, bir dağıtım etkinliğiyle göstermek için System Center Configuration Manager 2012 R2 kullanır.</span><span class="sxs-lookup"><span data-stu-id="63465-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="63465-110">Mobility hizmeti yükleme kullanarak da otomatikleştirmek [Azure Automation ve istenen durum Yapılandırması](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="63465-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63465-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="63465-111">Prerequisites</span></span>
1. <span data-ttu-id="63465-112">Yazılım dağıtım aracı, yapılandırma, ortamınızda dağıtılmış Manager gibi.</span><span class="sxs-lookup"><span data-stu-id="63465-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="63465-113">İki oluşturmak [cihaz koleksiyonları](https://technet.microsoft.com/library/gg682169.aspx), tüm için bir tane **Windows sunucuları**, diğeri tüm **Linux sunucuları**, Site Recovery kullanarak korumak istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="63465-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="63465-114">Site Recovery ile zaten kayıtlı bir yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="63465-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="63465-115">Configuration Manager sunucusu tarafından erişilebilecek güvenli bir ağ dosya paylaşımına (sunucu ileti bloğu paylaşım).</span><span class="sxs-lookup"><span data-stu-id="63465-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="63465-116">Mobility hizmetinin Windows çalıştıran bilgisayarlara dağıtma</span><span class="sxs-lookup"><span data-stu-id="63465-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="63465-117">Bu makalede yapılandırma sunucusu IP adresini 192.168.3.121 olduğunu ve güvenli bir ağ dosya paylaşımına olduğunu varsayar \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="63465-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="63465-118">Adım 1: dağıtıma Hazırlan</span><span class="sxs-lookup"><span data-stu-id="63465-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="63465-119">Ağ paylaşımında bir klasör oluşturun ve adlandırın **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="63465-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="63465-120">Yapılandırma sunucunuza oturum açın ve bir yönetici komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="63465-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="63465-121">Bir parola dosyası oluşturmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="63465-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="63465-122">Kopya **MobSvc.passphrase** içine dosya **MobSvcWindows** klasör, ağ paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="63465-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="63465-123">Yapılandırma sunucusundaki yükleyici deposu için aşağıdaki komutu çalıştırarak göz atın:</span><span class="sxs-lookup"><span data-stu-id="63465-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="63465-124">Kopya  **Microsoft ASR\_UA\_*sürüm*\_Windows\_GA\_*tarih* \_İçin Release.exe** **MobSvcWindows** klasör, ağ paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="63465-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="63465-125">Aşağıdaki kodu kopyalayın ve kaydedileceği **install.bat** içine **MobSvcWindows** klasör.</span><span class="sxs-lookup"><span data-stu-id="63465-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="63465-126">Bu komut dosyasındaki [CSIP] yer tutucuları yapılandırma sunucunuzun IP adresini gerçek değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="63465-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a><span data-ttu-id="63465-127">2. adım: bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="63465-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="63465-128">Configuration Manager konsolunuza oturum açın.</span><span class="sxs-lookup"><span data-stu-id="63465-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="63465-129">Gözat **yazılım Kitaplığı** > **Uygulama Yönetimi** > **paketleri**.</span><span class="sxs-lookup"><span data-stu-id="63465-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="63465-130">Sağ **paketleri**seçip **Paket Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="63465-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="63465-131">Ad, açıklama, üreticisi, dil ve sürüm için değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="63465-132">Seçin **bu paket kaynak dosyalarını içeren** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="63465-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="63465-133">Tıklatın **Gözat**, yükleyici depolandığı ağ paylaşımı seçin (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="63465-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="63465-135">Üzerinde **oluşturmak istediğiniz program türünü seçin** sayfasında, **standart Program**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="63465-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="63465-137">Üzerinde **bu standart programla ilgili bilgiler belirt** sayfasında, aşağıdaki girişleri yapın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="63465-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="63465-138">(Diğer girişleri varsayılan değerleri kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="63465-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="63465-139">**Parametre adı**</span><span class="sxs-lookup"><span data-stu-id="63465-139">**Parameter name**</span></span> | <span data-ttu-id="63465-140">**Değer**</span><span class="sxs-lookup"><span data-stu-id="63465-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="63465-141">Ad</span><span class="sxs-lookup"><span data-stu-id="63465-141">Name</span></span> | <span data-ttu-id="63465-142">Microsoft Azure Mobility hizmetini (Windows) yükleme</span><span class="sxs-lookup"><span data-stu-id="63465-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="63465-143">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="63465-143">Command line</span></span> | <span data-ttu-id="63465-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="63465-144">install.bat</span></span> |
  | <span data-ttu-id="63465-145">Program çalışabilir</span><span class="sxs-lookup"><span data-stu-id="63465-145">Program can run</span></span> | <span data-ttu-id="63465-146">Bir kullanıcı olup olmadığına oturum</span><span class="sxs-lookup"><span data-stu-id="63465-146">Whether or not a user is logged on</span></span> |

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="63465-148">Sonraki sayfada, hedef işletim sistemlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="63465-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="63465-149">Mobility hizmeti, yalnızca Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008 R2 üzerinde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="63465-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="63465-151">Sihirbazı tamamlamak için tıklatın **sonraki** iki kez.</span><span class="sxs-lookup"><span data-stu-id="63465-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="63465-152">Komut dosyası Mobility hizmeti aracısı ve yüklü olan aracıları güncelleştirmeleri hem yeni yüklemeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="63465-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="63465-153">Adım 3: Paket dağıtma</span><span class="sxs-lookup"><span data-stu-id="63465-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="63465-154">Configuration Manager konsolunda, pakete sağ tıklayın ve seçin **içeriği Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="63465-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="63465-155">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="63465-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="63465-156">Seçin  **[dağıtım noktaları](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  paketleri kopyalanmalıdır açın.</span><span class="sxs-lookup"><span data-stu-id="63465-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="63465-157">Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-157">Complete the wizard.</span></span> <span data-ttu-id="63465-158">Paket sonra belirtilen dağıtım noktalarına çoğaltmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="63465-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="63465-159">Paket dağıtımı yapıldıktan sonra pakete sağ tıklayın ve seçin **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="63465-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="63465-160">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="63465-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="63465-161">Dağıtımı için hedef koleksiyonu olarak önkoşullar bölümünde oluşturduğunuz Windows Server cihaz koleksiyonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="63465-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="63465-163">Üzerinde **içerik hedefini belirt** sayfasında, sizin **dağıtım noktaları**.</span><span class="sxs-lookup"><span data-stu-id="63465-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="63465-164">Üzerinde **bu yazılımın nasıl dağıtılacağını denetlemek için ayarları belirtin** sayfasında, amacı olduğundan emin olun **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="63465-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="63465-166">Üzerinde **bu dağıtım için zamanlamayı belirtin** sayfasında, bir zamanlama belirtin.</span><span class="sxs-lookup"><span data-stu-id="63465-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="63465-167">Daha fazla bilgi için bkz: [paketleri zamanlama](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="63465-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="63465-168">Üzerinde **dağıtım noktaları** sayfasında, veri merkeziniz gereksinimlerine göre özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="63465-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="63465-169">Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="63465-170">Gereksiz yeniden başlatmalardan önlemek için paket yükleme aylık bakım penceresi veya yazılım güncelleştirmeleri penceresi sırasında zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="63465-171">Configuration Manager konsolunu kullanarak dağıtımının ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63465-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="63465-172">Git **izleme** > **dağıtımları** > *[paket adınız]*.</span><span class="sxs-lookup"><span data-stu-id="63465-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Dağıtımlarını izlemek için Configuration Manager ekran seçeneği](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="63465-174">Mobility hizmeti Linux çalıştıran bilgisayarlara dağıtma</span><span class="sxs-lookup"><span data-stu-id="63465-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="63465-175">Bu makalede yapılandırma sunucusu IP adresini 192.168.3.121 olduğunu ve güvenli bir ağ dosya paylaşımına olduğunu varsayar \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="63465-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="63465-176">Adım 1: dağıtıma Hazırlan</span><span class="sxs-lookup"><span data-stu-id="63465-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="63465-177">Ağ paylaşımında bir klasör oluşturun ve olarak adlandırın **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="63465-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="63465-178">Yapılandırma sunucunuza oturum açın ve bir yönetici komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="63465-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="63465-179">Bir parola dosyası oluşturmak için aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="63465-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="63465-180">Kopya **MobSvc.passphrase** içine dosya **MobSvcLinux** klasör, ağ paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="63465-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="63465-181">Yapılandırma sunucusundaki yükleyici deponuza komutunu çalıştırarak göz atın:</span><span class="sxs-lookup"><span data-stu-id="63465-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="63465-182">Aşağıdaki dosyaları kopyalayın **MobSvcLinux** ağ paylaşımınızda klasörü:</span><span class="sxs-lookup"><span data-stu-id="63465-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="63465-183">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="63465-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="63465-184">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="63465-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="63465-185">Microsoft ASR\_UA\*SLES11 SP3 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="63465-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="63465-186">Microsoft ASR\_UA\*SLES11 SP4 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="63465-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="63465-187">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="63465-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="63465-188">Microsoft ASR\_UA\*UBUNTU 14.04 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="63465-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="63465-189">Aşağıdaki kodu kopyalayın ve kaydedileceği **install_linux.sh** içine **MobSvcLinux** klasör.</span><span class="sxs-lookup"><span data-stu-id="63465-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="63465-190">Bu komut dosyasındaki [CSIP] yer tutucuları yapılandırma sunucunuzun IP adresini gerçek değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="63465-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="63465-191">2. adım: bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="63465-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="63465-192">Configuration Manager konsolunuza oturum açın.</span><span class="sxs-lookup"><span data-stu-id="63465-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="63465-193">Gözat **yazılım Kitaplığı** > **Uygulama Yönetimi** > **paketleri**.</span><span class="sxs-lookup"><span data-stu-id="63465-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="63465-194">Sağ **paketleri**seçip **Paket Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="63465-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="63465-195">Ad, açıklama, üreticisi, dil ve sürüm için değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="63465-196">Seçin **bu paket kaynak dosyalarını içeren** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="63465-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="63465-197">Tıklatın **Gözat**, yükleyici depolandığı ağ paylaşımı seçin (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="63465-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="63465-199">Üzerinde **oluşturmak istediğiniz program türünü seçin** sayfasında, **standart Program**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="63465-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="63465-201">Üzerinde **bu standart programla ilgili bilgiler belirt** sayfasında, aşağıdaki girişleri yapın ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="63465-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="63465-202">(Diğer girişleri varsayılan değerleri kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="63465-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="63465-203">**Parametre adı**</span><span class="sxs-lookup"><span data-stu-id="63465-203">**Parameter name**</span></span> | <span data-ttu-id="63465-204">**Değer**</span><span class="sxs-lookup"><span data-stu-id="63465-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="63465-205">Ad</span><span class="sxs-lookup"><span data-stu-id="63465-205">Name</span></span> | <span data-ttu-id="63465-206">Microsoft Azure Mobility hizmetini (Linux) yükleme</span><span class="sxs-lookup"><span data-stu-id="63465-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="63465-207">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="63465-207">Command line</span></span> | <span data-ttu-id="63465-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="63465-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="63465-209">Program çalışabilir</span><span class="sxs-lookup"><span data-stu-id="63465-209">Program can run</span></span> | <span data-ttu-id="63465-210">Bir kullanıcı olup olmadığına oturum</span><span class="sxs-lookup"><span data-stu-id="63465-210">Whether or not a user is logged on</span></span> |

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="63465-212">Sonraki sayfada seçin **Bu program herhangi bir platformda çalışabilir**.</span><span class="sxs-lookup"><span data-stu-id="63465-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="63465-213">![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="63465-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="63465-214">Sihirbazı tamamlamak için tıklatın **sonraki** iki kez.</span><span class="sxs-lookup"><span data-stu-id="63465-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="63465-215">Komut dosyası Mobility hizmeti aracısı ve yüklü olan aracıları güncelleştirmeleri hem yeni yüklemeleri destekler.</span><span class="sxs-lookup"><span data-stu-id="63465-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="63465-216">Adım 3: Paket dağıtma</span><span class="sxs-lookup"><span data-stu-id="63465-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="63465-217">Configuration Manager konsolunda, pakete sağ tıklayın ve seçin **içeriği Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="63465-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="63465-218">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="63465-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="63465-219">Seçin  **[dağıtım noktaları](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  paketleri kopyalanmalıdır açın.</span><span class="sxs-lookup"><span data-stu-id="63465-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="63465-220">Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-220">Complete the wizard.</span></span> <span data-ttu-id="63465-221">Paket sonra belirtilen dağıtım noktalarına çoğaltmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="63465-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="63465-222">Paket dağıtımı yapıldıktan sonra pakete sağ tıklayın ve seçin **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="63465-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="63465-223">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="63465-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="63465-224">Dağıtımı için hedef koleksiyonu olarak önkoşullar bölümünde oluşturduğunuz Linux sunucusu cihaz koleksiyonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="63465-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="63465-226">Üzerinde **içerik hedefini belirt** sayfasında, sizin **dağıtım noktaları**.</span><span class="sxs-lookup"><span data-stu-id="63465-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="63465-227">Üzerinde **bu yazılımın nasıl dağıtılacağını denetlemek için ayarları belirtin** sayfasında, amacı olduğundan emin olun **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="63465-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="63465-229">Üzerinde **bu dağıtım için zamanlamayı belirtin** sayfasında, bir zamanlama belirtin.</span><span class="sxs-lookup"><span data-stu-id="63465-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="63465-230">Daha fazla bilgi için bkz: [paketleri zamanlama](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="63465-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="63465-231">Üzerinde **dağıtım noktaları** sayfasında, veri merkeziniz gereksinimlerine göre özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="63465-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="63465-232">Sihirbazı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="63465-232">Then complete the wizard.</span></span>

<span data-ttu-id="63465-233">Mobility hizmeti Linux sunucusu cihaz koleksiyonunda, yapılandırdığınız zamanlamaya göre yüklü.</span><span class="sxs-lookup"><span data-stu-id="63465-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="63465-234">Mobilite hizmetinin yüklenmesi için diğer yöntemleri</span><span class="sxs-lookup"><span data-stu-id="63465-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="63465-235">Mobility hizmetinin yüklenmesi için diğer bazı seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="63465-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="63465-236">GUI kullanarak el ile yükleme</span><span class="sxs-lookup"><span data-stu-id="63465-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="63465-237">Komut satırı kullanarak el ile yükleme</span><span class="sxs-lookup"><span data-stu-id="63465-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="63465-238">Yapılandırma sunucusu kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="63465-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="63465-239">Azure Otomasyonu & istenen durum Yapılandırması'nı kullanarak otomatik yükleme</span><span class="sxs-lookup"><span data-stu-id="63465-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="63465-240">Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="63465-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="63465-241">Mobility hizmetini kaldırmak için Configuration Manager paketler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63465-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="63465-242">Bunu yapmak için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="63465-242">Use the following script to do so:</span></span>

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a><span data-ttu-id="63465-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63465-243">Next steps</span></span>
<span data-ttu-id="63465-244">Artık hazırsınız [korumayı etkinleştir](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) , sanal makineleriniz için.</span><span class="sxs-lookup"><span data-stu-id="63465-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
