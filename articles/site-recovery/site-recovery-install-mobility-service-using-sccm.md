---
title: "yazılım dağıtım araçları kullanarak mobilite hizmeti yükleme Azure Site kurtarma aaaAutomate | Microsoft Docs"
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
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="cee10-103">Yazılım dağıtım araçları kullanarak mobilite hizmeti yükleme otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="cee10-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="cee10-104">Bu belge sürümü kullandığınız varsayılır **9.9.4510.1** ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="cee10-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="cee10-105">Bu makalede, System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility hizmeti, veri merkezinizde nasıl kullanabileceğinize bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="cee10-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="cee10-106">Configuration Manager gibi yazılım dağıtım aracını kullanarak hello aşağıdaki avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="cee10-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="cee10-107">Yazılım güncelleştirmeleri için planlanan bakım penceresi sırasında yeni yüklemeleri ve yükseltmeleri, dağıtımını planlama</span><span class="sxs-lookup"><span data-stu-id="cee10-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="cee10-108">Dağıtım toohundreds sunucularının aynı anda ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="cee10-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="cee10-109">Bu makalede, System Center Configuration Manager 2012 R2 toodemonstrate hello dağıtım aktivitesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="cee10-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="cee10-110">Mobility hizmeti yükleme kullanarak da otomatikleştirmek [Azure Automation ve istenen durum Yapılandırması](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="cee10-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cee10-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cee10-111">Prerequisites</span></span>
1. <span data-ttu-id="cee10-112">Yazılım dağıtım aracı, yapılandırma, ortamınızda dağıtılmış Manager gibi.</span><span class="sxs-lookup"><span data-stu-id="cee10-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="cee10-113">İki oluşturmak [cihaz koleksiyonları](https://technet.microsoft.com/library/gg682169.aspx), tüm için bir tane **Windows sunucuları**, tüm için başka bir **Linux sunucuları**, Site Recovery kullanarak tooprotect istiyor.</span><span class="sxs-lookup"><span data-stu-id="cee10-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="cee10-114">Site Recovery ile zaten kayıtlı bir yapılandırma sunucusu.</span><span class="sxs-lookup"><span data-stu-id="cee10-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="cee10-115">Merhaba Configuration Manager sunucusu tarafından erişilebilecek güvenli bir ağ dosya paylaşımına (sunucu ileti bloğu paylaşım).</span><span class="sxs-lookup"><span data-stu-id="cee10-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="cee10-116">Mobility hizmetinin Windows çalıştıran bilgisayarlara dağıtma</span><span class="sxs-lookup"><span data-stu-id="cee10-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="cee10-117">Bu makalede hello yapılandırma sunucusu IP adresi hello 192.168.3.121 olacak ve bu hello güvenli ağ dosya paylaşımı varsayılmaktadır \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="cee10-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="cee10-118">Adım 1: dağıtıma Hazırlan</span><span class="sxs-lookup"><span data-stu-id="cee10-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="cee10-119">Merhaba ağ paylaşımında bir klasör oluşturun ve adlandırın **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="cee10-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="cee10-120">Tooyour yapılandırma sunucusunda oturum açın ve bir yönetici komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="cee10-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="cee10-121">Aşağıdaki komutları toogenerate parola dosya hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cee10-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="cee10-122">Kopya hello **MobSvc.passphrase** hello dosyasına **MobSvcWindows** klasör, ağ paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="cee10-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="cee10-123">Merhaba yapılandırma sunucusu üzerindeki toohello yükleyici repository hello aşağıdaki komutu çalıştırarak göz atın:</span><span class="sxs-lookup"><span data-stu-id="cee10-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="cee10-124">Kopya hello  **Microsoft ASR\_UA\_*sürüm*\_Windows\_GA\_*tarih* \_ Release.exe** toohello **MobSvcWindows** klasör, ağ paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="cee10-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="cee10-125">Hello aşağıdaki kodu kopyalayın ve olarak kaydedin **install.bat** hello içine **MobSvcWindows** klasör.</span><span class="sxs-lookup"><span data-stu-id="cee10-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cee10-126">Bu komut dosyası Hello [CSIP] yer tutucuları hello gerçek başlangıç IP adresi yapılandırması sunucunuzun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cee10-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="cee10-127">2. adım: bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="cee10-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="cee10-128">Tooyour Configuration Manager konsolunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cee10-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="cee10-129">Çok Gözat**yazılım Kitaplığı** > **Uygulama Yönetimi** > **paketleri**.</span><span class="sxs-lookup"><span data-stu-id="cee10-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="cee10-130">Sağ **paketleri**seçip **Paket Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="cee10-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="cee10-131">Merhaba adı, açıklama, üreticisi, dil ve sürümü için değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cee10-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="cee10-132">Select hello **bu paket kaynak dosyalarını içeren** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="cee10-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="cee10-133">Tıklatın **Gözat**ve hello yükleyici depolandığı select hello ağ paylaşımı (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="cee10-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="cee10-135">Merhaba üzerinde **toocreate istediğiniz Seç hello program türü** sayfasında, **standart Program**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cee10-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="cee10-137">Merhaba üzerinde **bu standart programla ilgili bilgiler belirt** sayfasında girişleri aşağıdaki hello sağlamak ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cee10-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="cee10-138">(Merhaba diğer girişleri varsayılan değerleri kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="cee10-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="cee10-139">**Parametre adı**</span><span class="sxs-lookup"><span data-stu-id="cee10-139">**Parameter name**</span></span> | <span data-ttu-id="cee10-140">**Değer**</span><span class="sxs-lookup"><span data-stu-id="cee10-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="cee10-141">Ad</span><span class="sxs-lookup"><span data-stu-id="cee10-141">Name</span></span> | <span data-ttu-id="cee10-142">Microsoft Azure Mobility hizmetini (Windows) yükleme</span><span class="sxs-lookup"><span data-stu-id="cee10-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="cee10-143">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="cee10-143">Command line</span></span> | <span data-ttu-id="cee10-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="cee10-144">install.bat</span></span> |
  | <span data-ttu-id="cee10-145">Program çalışabilir</span><span class="sxs-lookup"><span data-stu-id="cee10-145">Program can run</span></span> | <span data-ttu-id="cee10-146">Bir kullanıcı olup olmadığına oturum</span><span class="sxs-lookup"><span data-stu-id="cee10-146">Whether or not a user is logged on</span></span> |

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="cee10-148">Merhaba sonraki sayfada hello hedef işletim sistemlerini seçin.</span><span class="sxs-lookup"><span data-stu-id="cee10-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="cee10-149">Mobility hizmeti, yalnızca Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008 R2 üzerinde yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="cee10-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="cee10-151">toocomplete hello Sihirbazı'nı tıklatın **sonraki** iki kez.</span><span class="sxs-lookup"><span data-stu-id="cee10-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="cee10-152">Merhaba betik her iki yeni yüklemeler Mobility hizmeti destekler ve yüklü olan tooagents güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="cee10-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="cee10-153">Adım 3: hello paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="cee10-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="cee10-154">Merhaba Configuration Manager konsolunda, pakete sağ tıklayın ve seçin **içeriği Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="cee10-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="cee10-155">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="cee10-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="cee10-156">Select hello  **[dağıtım noktaları](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich üzerinde hello paketleri kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cee10-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="cee10-157">Tam hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="cee10-157">Complete hello wizard.</span></span> <span data-ttu-id="cee10-158">Merhaba paket sonra toohello çoğaltmaya başlar dağıtım noktaları belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="cee10-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="cee10-159">Merhaba paket dağıtımı yapıldıktan sonra hello paketini sağ tıklatın ve seçin **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="cee10-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="cee10-160">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="cee10-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="cee10-161">Merhaba dağıtımı için hedef koleksiyonu olarak hello önkoşullar bölümünde oluşturduğunuz hello Windows Server cihaz koleksiyonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="cee10-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="cee10-163">Merhaba üzerinde **hello içerik hedefini belirtin** sayfasında, sizin **dağıtım noktaları**.</span><span class="sxs-lookup"><span data-stu-id="cee10-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="cee10-164">Merhaba üzerinde **bu yazılımın nasıl dağıtılacağını belirtin ayarları toocontrol** sayfasında, hello amacı olduğundan emin olun **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="cee10-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="cee10-166">Merhaba üzerinde **bu dağıtım için belirt hello zamanlamayı** sayfasında, bir zamanlama belirtin.</span><span class="sxs-lookup"><span data-stu-id="cee10-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="cee10-167">Daha fazla bilgi için bkz: [paketleri zamanlama](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="cee10-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="cee10-168">Merhaba üzerinde **dağıtım noktaları** sayfasında, veri merkeziniz toohello gereksinimlerine göre hello özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cee10-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="cee10-169">Başlangıç Sihirbazı'nı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="cee10-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="cee10-170">tooavoid gereksiz yeniden başlatır, zamanlama hello paket yükleme sırasında aylık bakım penceresi veya yazılım güncelleştirmeleri penceresi.</span><span class="sxs-lookup"><span data-stu-id="cee10-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="cee10-171">Merhaba Configuration Manager konsolunu kullanarak hello dağıtımının ilerleme durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cee10-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="cee10-172">Çok Git**izleme** > **dağıtımları** > *[paket adınız]*.</span><span class="sxs-lookup"><span data-stu-id="cee10-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Configuration Manager ekran seçeneği toomonitor dağıtımları](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="cee10-174">Mobility hizmeti Linux çalıştıran bilgisayarlara dağıtma</span><span class="sxs-lookup"><span data-stu-id="cee10-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="cee10-175">Bu makalede hello yapılandırma sunucusu IP adresi hello 192.168.3.121 olacak ve bu hello güvenli ağ dosya paylaşımı varsayılmaktadır \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="cee10-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="cee10-176">Adım 1: dağıtıma Hazırlan</span><span class="sxs-lookup"><span data-stu-id="cee10-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="cee10-177">Merhaba ağ paylaşımında bir klasör oluşturun ve olarak adlandırın **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="cee10-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="cee10-178">Tooyour yapılandırma sunucusunda oturum açın ve bir yönetici komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="cee10-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="cee10-179">Aşağıdaki komutları toogenerate parola dosya hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cee10-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="cee10-180">Kopya hello **MobSvc.passphrase** hello dosyasına **MobSvcLinux** klasör, ağ paylaşımında.</span><span class="sxs-lookup"><span data-stu-id="cee10-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="cee10-181">Merhaba yapılandırma sunucusu üzerindeki toohello yükleyici repository hello komutu çalıştırarak göz atın:</span><span class="sxs-lookup"><span data-stu-id="cee10-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="cee10-182">Kopya hello aşağıdaki dosyaları toohello **MobSvcLinux** ağ paylaşımınızda klasörü:</span><span class="sxs-lookup"><span data-stu-id="cee10-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="cee10-183">Microsoft ASR\_UA\*RHEL6 64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cee10-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="cee10-184">Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cee10-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cee10-185">Microsoft ASR\_UA\*SLES11 SP3 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cee10-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cee10-186">Microsoft ASR\_UA\*SLES11 SP4 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cee10-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cee10-187">Microsoft ASR\_UA\*OL6 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cee10-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="cee10-188">Microsoft ASR\_UA\*UBUNTU 14.04 64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="cee10-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="cee10-189">Hello aşağıdaki kodu kopyalayın ve olarak kaydedin **install_linux.sh** hello içine **MobSvcLinux** klasör.</span><span class="sxs-lookup"><span data-stu-id="cee10-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="cee10-190">Bu komut dosyası Hello [CSIP] yer tutucuları hello gerçek başlangıç IP adresi yapılandırması sunucunuzun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cee10-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="cee10-191">2. adım: bir paket oluşturun</span><span class="sxs-lookup"><span data-stu-id="cee10-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="cee10-192">Tooyour Configuration Manager konsolunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cee10-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="cee10-193">Çok Gözat**yazılım Kitaplığı** > **Uygulama Yönetimi** > **paketleri**.</span><span class="sxs-lookup"><span data-stu-id="cee10-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="cee10-194">Sağ **paketleri**seçip **Paket Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="cee10-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="cee10-195">Merhaba adı, açıklama, üreticisi, dil ve sürümü için değerler sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cee10-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="cee10-196">Select hello **bu paket kaynak dosyalarını içeren** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="cee10-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="cee10-197">Tıklatın **Gözat**ve hello yükleyici depolandığı select hello ağ paylaşımı (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="cee10-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="cee10-199">Merhaba üzerinde **toocreate istediğiniz Seç hello program türü** sayfasında, **standart Program**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cee10-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="cee10-201">Merhaba üzerinde **bu standart programla ilgili bilgiler belirt** sayfasında girişleri aşağıdaki hello sağlamak ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cee10-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="cee10-202">(Merhaba diğer girişleri varsayılan değerleri kullanabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="cee10-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="cee10-203">**Parametre adı**</span><span class="sxs-lookup"><span data-stu-id="cee10-203">**Parameter name**</span></span> | <span data-ttu-id="cee10-204">**Değer**</span><span class="sxs-lookup"><span data-stu-id="cee10-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="cee10-205">Ad</span><span class="sxs-lookup"><span data-stu-id="cee10-205">Name</span></span> | <span data-ttu-id="cee10-206">Microsoft Azure Mobility hizmetini (Linux) yükleme</span><span class="sxs-lookup"><span data-stu-id="cee10-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="cee10-207">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="cee10-207">Command line</span></span> | <span data-ttu-id="cee10-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="cee10-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="cee10-209">Program çalışabilir</span><span class="sxs-lookup"><span data-stu-id="cee10-209">Program can run</span></span> | <span data-ttu-id="cee10-210">Bir kullanıcı olup olmadığına oturum</span><span class="sxs-lookup"><span data-stu-id="cee10-210">Whether or not a user is logged on</span></span> |

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="cee10-212">Merhaba sonraki sayfada seçin **Bu program herhangi bir platformda çalışabilir**.</span><span class="sxs-lookup"><span data-stu-id="cee10-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="cee10-213">![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="cee10-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="cee10-214">toocomplete hello Sihirbazı'nı tıklatın **sonraki** iki kez.</span><span class="sxs-lookup"><span data-stu-id="cee10-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="cee10-215">Merhaba betik her iki yeni yüklemeler Mobility hizmeti destekler ve yüklü olan tooagents güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="cee10-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="cee10-216">Adım 3: hello paketini dağıtma</span><span class="sxs-lookup"><span data-stu-id="cee10-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="cee10-217">Merhaba Configuration Manager konsolunda, pakete sağ tıklayın ve seçin **içeriği Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="cee10-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="cee10-218">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="cee10-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="cee10-219">Select hello  **[dağıtım noktaları](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich üzerinde hello paketleri kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cee10-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="cee10-220">Tam hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="cee10-220">Complete hello wizard.</span></span> <span data-ttu-id="cee10-221">Merhaba paket sonra toohello çoğaltmaya başlar dağıtım noktaları belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="cee10-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="cee10-222">Merhaba paket dağıtımı yapıldıktan sonra hello paketini sağ tıklatın ve seçin **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="cee10-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="cee10-223">![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="cee10-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="cee10-224">Merhaba hello dağıtımı için hedef koleksiyonu olarak hello önkoşullar bölümünde oluşturduğunuz Linux sunucusu cihaz koleksiyonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="cee10-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="cee10-226">Merhaba üzerinde **hello içerik hedefini belirtin** sayfasında, sizin **dağıtım noktaları**.</span><span class="sxs-lookup"><span data-stu-id="cee10-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="cee10-227">Merhaba üzerinde **bu yazılımın nasıl dağıtılacağını belirtin ayarları toocontrol** sayfasında, hello amacı olduğundan emin olun **gerekli**.</span><span class="sxs-lookup"><span data-stu-id="cee10-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="cee10-229">Merhaba üzerinde **bu dağıtım için belirt hello zamanlamayı** sayfasında, bir zamanlama belirtin.</span><span class="sxs-lookup"><span data-stu-id="cee10-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="cee10-230">Daha fazla bilgi için bkz: [paketleri zamanlama](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="cee10-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="cee10-231">Merhaba üzerinde **dağıtım noktaları** sayfasında, veri merkeziniz toohello gereksinimlerine göre hello özelliklerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="cee10-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="cee10-232">Başlangıç Sihirbazı'nı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="cee10-232">Then complete hello wizard.</span></span>

<span data-ttu-id="cee10-233">Mobility hizmeti yapılandırdığınız toohello zamanlamaya göre Linux Server Aygıt koleksiyonu hello üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="cee10-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="cee10-234">Diğer yöntemleri tooinstall Mobility hizmeti</span><span class="sxs-lookup"><span data-stu-id="cee10-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="cee10-235">Mobility hizmetinin yüklenmesi için diğer bazı seçenekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="cee10-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="cee10-236">GUI kullanarak el ile yükleme</span><span class="sxs-lookup"><span data-stu-id="cee10-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="cee10-237">Komut satırı kullanarak el ile yükleme</span><span class="sxs-lookup"><span data-stu-id="cee10-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="cee10-238">Yapılandırma sunucusu kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="cee10-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="cee10-239">Azure Otomasyonu & istenen durum Yapılandırması'nı kullanarak otomatik yükleme</span><span class="sxs-lookup"><span data-stu-id="cee10-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="cee10-240">Mobility hizmetini kaldırma</span><span class="sxs-lookup"><span data-stu-id="cee10-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="cee10-241">Configuration Manager paketlerini toouninstall Mobility hizmeti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cee10-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="cee10-242">Komut dosyası toodo şekilde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="cee10-242">Use hello following script toodo so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cee10-243">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cee10-243">Next steps</span></span>
<span data-ttu-id="cee10-244">Artık çok hazırsınız[korumayı etkinleştir](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) , sanal makineleriniz için.</span><span class="sxs-lookup"><span data-stu-id="cee10-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
