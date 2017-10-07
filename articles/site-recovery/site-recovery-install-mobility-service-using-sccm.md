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
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>Yazılım dağıtım araçları kullanarak mobilite hizmeti yükleme otomatikleştirme

>[!IMPORTANT]
Bu belge sürümü kullandığınız varsayılır **9.9.4510.1** ya da daha yüksek.

Bu makalede, System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility hizmeti, veri merkezinizde nasıl kullanabileceğinize bir örnek sağlar. Configuration Manager gibi yazılım dağıtım aracını kullanarak hello aşağıdaki avantajları vardır:
* Yazılım güncelleştirmeleri için planlanan bakım penceresi sırasında yeni yüklemeleri ve yükseltmeleri, dağıtımını planlama
* Dağıtım toohundreds sunucularının aynı anda ölçeklendirme


> [!NOTE]
> Bu makalede, System Center Configuration Manager 2012 R2 toodemonstrate hello dağıtım aktivitesi kullanır. Mobility hizmeti yükleme kullanarak da otomatikleştirmek [Azure Automation ve istenen durum Yapılandırması](site-recovery-automate-mobility-service-install.md).

## <a name="prerequisites"></a>Ön koşullar
1. Yazılım dağıtım aracı, yapılandırma, ortamınızda dağıtılmış Manager gibi.
  İki oluşturmak [cihaz koleksiyonları](https://technet.microsoft.com/library/gg682169.aspx), tüm için bir tane **Windows sunucuları**, tüm için başka bir **Linux sunucuları**, Site Recovery kullanarak tooprotect istiyor.
3. Site Recovery ile zaten kayıtlı bir yapılandırma sunucusu.
4. Merhaba Configuration Manager sunucusu tarafından erişilebilecek güvenli bir ağ dosya paylaşımına (sunucu ileti bloğu paylaşım).

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Mobility hizmetinin Windows çalıştıran bilgisayarlara dağıtma
> [!NOTE]
> Bu makalede hello yapılandırma sunucusu IP adresi hello 192.168.3.121 olacak ve bu hello güvenli ağ dosya paylaşımı varsayılmaktadır \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Adım 1: dağıtıma Hazırlan
1. Merhaba ağ paylaşımında bir klasör oluşturun ve adlandırın **MobSvcWindows**.
2. Tooyour yapılandırma sunucusunda oturum açın ve bir yönetici komut istemi açın.
3. Aşağıdaki komutları toogenerate parola dosya hello çalıştırın:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Kopya hello **MobSvc.passphrase** hello dosyasına **MobSvcWindows** klasör, ağ paylaşımında.
5. Merhaba yapılandırma sunucusu üzerindeki toohello yükleyici repository hello aşağıdaki komutu çalıştırarak göz atın:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Kopya hello  **Microsoft ASR\_UA\_*sürüm*\_Windows\_GA\_*tarih* \_ Release.exe** toohello **MobSvcWindows** klasör, ağ paylaşımında.
7. Hello aşağıdaki kodu kopyalayın ve olarak kaydedin **install.bat** hello içine **MobSvcWindows** klasör.

   > [!NOTE]
   > Bu komut dosyası Hello [CSIP] yer tutucuları hello gerçek başlangıç IP adresi yapılandırması sunucunuzun değerlerle değiştirin.

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

### <a name="step-2-create-a-package"></a>2. adım: bir paket oluşturun

1. Tooyour Configuration Manager konsolunda oturum açın.
2. Çok Gözat**yazılım Kitaplığı** > **Uygulama Yönetimi** > **paketleri**.
3. Sağ **paketleri**seçip **Paket Oluştur**.
4. Merhaba adı, açıklama, üreticisi, dil ve sürümü için değerler sağlayın.
5. Select hello **bu paket kaynak dosyalarını içeren** onay kutusu.
6. Tıklatın **Gözat**ve hello yükleyici depolandığı select hello ağ paylaşımı (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. Merhaba üzerinde **toocreate istediğiniz Seç hello program türü** sayfasında, **standart Program**, tıklatıp **sonraki**.

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Merhaba üzerinde **bu standart programla ilgili bilgiler belirt** sayfasında girişleri aşağıdaki hello sağlamak ve tıklayın **sonraki**. (Merhaba diğer girişleri varsayılan değerleri kullanabilirsiniz.)

  | **Parametre adı** | **Değer** |
  |--|--|
  | Ad | Microsoft Azure Mobility hizmetini (Windows) yükleme |
  | Komut satırı | install.bat |
  | Program çalışabilir | Bir kullanıcı olup olmadığına oturum |

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. Merhaba sonraki sayfada hello hedef işletim sistemlerini seçin. Mobility hizmeti, yalnızca Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008 R2 üzerinde yüklenebilir.

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. toocomplete hello Sihirbazı'nı tıklatın **sonraki** iki kez.


> [!NOTE]
> Merhaba betik her iki yeni yüklemeler Mobility hizmeti destekler ve yüklü olan tooagents güncelleştirir.

### <a name="step-3-deploy-hello-package"></a>Adım 3: hello paketini dağıtma
1. Merhaba Configuration Manager konsolunda, pakete sağ tıklayın ve seçin **içeriği Dağıt**.
  ![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Select hello  **[dağıtım noktaları](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich üzerinde hello paketleri kopyalanmalıdır.
3. Tam hello Sihirbazı. Merhaba paket sonra toohello çoğaltmaya başlar dağıtım noktaları belirtilmiş.
4. Merhaba paket dağıtımı yapıldıktan sonra hello paketini sağ tıklatın ve seçin **dağıtma**.
  ![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Merhaba dağıtımı için hedef koleksiyonu olarak hello önkoşullar bölümünde oluşturduğunuz hello Windows Server cihaz koleksiyonunu seçin.

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. Merhaba üzerinde **hello içerik hedefini belirtin** sayfasında, sizin **dağıtım noktaları**.
7. Merhaba üzerinde **bu yazılımın nasıl dağıtılacağını belirtin ayarları toocontrol** sayfasında, hello amacı olduğundan emin olun **gerekli**.

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Merhaba üzerinde **bu dağıtım için belirt hello zamanlamayı** sayfasında, bir zamanlama belirtin. Daha fazla bilgi için bkz: [paketleri zamanlama](https://technet.microsoft.com/library/gg682178.aspx).
9. Merhaba üzerinde **dağıtım noktaları** sayfasında, veri merkeziniz toohello gereksinimlerine göre hello özelliklerini yapılandırın. Başlangıç Sihirbazı'nı tamamlayın.

> [!TIP]
> tooavoid gereksiz yeniden başlatır, zamanlama hello paket yükleme sırasında aylık bakım penceresi veya yazılım güncelleştirmeleri penceresi.

Merhaba Configuration Manager konsolunu kullanarak hello dağıtımının ilerleme durumunu izleyebilirsiniz. Çok Git**izleme** > **dağıtımları** > *[paket adınız]*.

  ![Configuration Manager ekran seçeneği toomonitor dağıtımları](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Mobility hizmeti Linux çalıştıran bilgisayarlara dağıtma
> [!NOTE]
> Bu makalede hello yapılandırma sunucusu IP adresi hello 192.168.3.121 olacak ve bu hello güvenli ağ dosya paylaşımı varsayılmaktadır \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Adım 1: dağıtıma Hazırlan
1. Merhaba ağ paylaşımında bir klasör oluşturun ve olarak adlandırın **MobSvcLinux**.
2. Tooyour yapılandırma sunucusunda oturum açın ve bir yönetici komut istemi açın.
3. Aşağıdaki komutları toogenerate parola dosya hello çalıştırın:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Kopya hello **MobSvc.passphrase** hello dosyasına **MobSvcLinux** klasör, ağ paylaşımında.
5. Merhaba yapılandırma sunucusu üzerindeki toohello yükleyici repository hello komutu çalıştırarak göz atın:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Kopya hello aşağıdaki dosyaları toohello **MobSvcLinux** ağ paylaşımınızda klasörü:
   * Microsoft ASR\_UA\*RHEL6 64*release.tar.gz
   * Microsoft ASR\_UA\*RHEL7 64\*release.tar.gz
   * Microsoft ASR\_UA\*SLES11 SP3 64\*release.tar.gz
   * Microsoft ASR\_UA\*SLES11 SP4 64\*release.tar.gz
   * Microsoft ASR\_UA\*OL6 64\*release.tar.gz
   * Microsoft ASR\_UA\*UBUNTU 14.04 64\*release.tar.gz


7. Hello aşağıdaki kodu kopyalayın ve olarak kaydedin **install_linux.sh** hello içine **MobSvcLinux** klasör.
   > [!NOTE]
   > Bu komut dosyası Hello [CSIP] yer tutucuları hello gerçek başlangıç IP adresi yapılandırması sunucunuzun değerlerle değiştirin.

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

### <a name="step-2-create-a-package"></a>2. adım: bir paket oluşturun

1. Tooyour Configuration Manager konsolunda oturum açın.
2. Çok Gözat**yazılım Kitaplığı** > **Uygulama Yönetimi** > **paketleri**.
3. Sağ **paketleri**seçip **Paket Oluştur**.
4. Merhaba adı, açıklama, üreticisi, dil ve sürümü için değerler sağlayın.
5. Select hello **bu paket kaynak dosyalarını içeren** onay kutusu.
6. Tıklatın **Gözat**ve hello yükleyici depolandığı select hello ağ paylaşımı (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. Merhaba üzerinde **toocreate istediğiniz Seç hello program türü** sayfasında, **standart Program**, tıklatıp **sonraki**.

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Merhaba üzerinde **bu standart programla ilgili bilgiler belirt** sayfasında girişleri aşağıdaki hello sağlamak ve tıklayın **sonraki**. (Merhaba diğer girişleri varsayılan değerleri kullanabilirsiniz.)

    | **Parametre adı** | **Değer** |
  |--|--|
  | Ad | Microsoft Azure Mobility hizmetini (Linux) yükleme |
  | Komut satırı | ./install_linux.sh |
  | Program çalışabilir | Bir kullanıcı olup olmadığına oturum |

  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. Merhaba sonraki sayfada seçin **Bu program herhangi bir platformda çalışabilir**.
  ![Ekran görüntüsü, paket ve Program Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. toocomplete hello Sihirbazı'nı tıklatın **sonraki** iki kez.

> [!NOTE]
> Merhaba betik her iki yeni yüklemeler Mobility hizmeti destekler ve yüklü olan tooagents güncelleştirir.

### <a name="step-3-deploy-hello-package"></a>Adım 3: hello paketini dağıtma
1. Merhaba Configuration Manager konsolunda, pakete sağ tıklayın ve seçin **içeriği Dağıt**.
  ![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Select hello  **[dağıtım noktaları](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  toowhich üzerinde hello paketleri kopyalanmalıdır.
3. Tam hello Sihirbazı. Merhaba paket sonra toohello çoğaltmaya başlar dağıtım noktaları belirtilmiş.
4. Merhaba paket dağıtımı yapıldıktan sonra hello paketini sağ tıklatın ve seçin **dağıtma**.
  ![Ekran görüntüsü, Configuration Manager Konsolu](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Merhaba hello dağıtımı için hedef koleksiyonu olarak hello önkoşullar bölümünde oluşturduğunuz Linux sunucusu cihaz koleksiyonunu seçin.

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. Merhaba üzerinde **hello içerik hedefini belirtin** sayfasında, sizin **dağıtım noktaları**.
7. Merhaba üzerinde **bu yazılımın nasıl dağıtılacağını belirtin ayarları toocontrol** sayfasında, hello amacı olduğundan emin olun **gerekli**.

  ![Ekran görüntüsü, yazılımı Dağıt Sihirbazı](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Merhaba üzerinde **bu dağıtım için belirt hello zamanlamayı** sayfasında, bir zamanlama belirtin. Daha fazla bilgi için bkz: [paketleri zamanlama](https://technet.microsoft.com/library/gg682178.aspx).
9. Merhaba üzerinde **dağıtım noktaları** sayfasında, veri merkeziniz toohello gereksinimlerine göre hello özelliklerini yapılandırın. Başlangıç Sihirbazı'nı tamamlayın.

Mobility hizmeti yapılandırdığınız toohello zamanlamaya göre Linux Server Aygıt koleksiyonu hello üzerinde yüklü.

## <a name="other-methods-tooinstall-mobility-service"></a>Diğer yöntemleri tooinstall Mobility hizmeti
Mobility hizmetinin yüklenmesi için diğer bazı seçenekleri şunlardır:
* [GUI kullanarak el ile yükleme](http://aka.ms/mobsvcmanualinstall)
* [Komut satırı kullanarak el ile yükleme](http://aka.ms/mobsvcmanualinstallcli)
* [Yapılandırma sunucusu kullanarak yükleme](http://aka.ms/pushinstall)
* [Azure Otomasyonu & istenen durum Yapılandırması'nı kullanarak otomatik yükleme](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>Mobility hizmetini kaldırma
Configuration Manager paketlerini toouninstall Mobility hizmeti oluşturabilirsiniz. Komut dosyası toodo şekilde aşağıdaki hello kullan:

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

## <a name="next-steps"></a>Sonraki adımlar
Artık çok hazırsınız[korumayı etkinleştir](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) , sanal makineleriniz için.
