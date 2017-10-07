---
title: "Azure yedekleme sunucusu v2 aaaSilent yüklemesi | Microsoft Docs"
description: "PowerShell komut dosyası toosilently Azure yedekleme sunucusu v2 yükleyin. Bu tür bir yükleme, katılımsız bir yükleme olarak da adlandırılır."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="20e8c-104">Azure yedekleme sunucusu v2 katılımsız yüklemesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="20e8c-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="20e8c-105">Bilgi nasıl toorun Azure yedekleme sunucusu v2 katılımsız yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="20e8c-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="20e8c-106">Azure yedekleme sunucusu v1 yüklüyorsanız, bu adımları uygulamayın.</span><span class="sxs-lookup"><span data-stu-id="20e8c-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="20e8c-107">Yedek sunucu v2 yükleyin</span><span class="sxs-lookup"><span data-stu-id="20e8c-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="20e8c-108">Azure yedekleme sunucusu v2 barındıran hello sunucusunda, bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="20e8c-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="20e8c-109">(Merhaba dosyasını Not Defteri'nde veya başka bir metin düzenleyicisi oluşturabilirsiniz.) Merhaba dosyayı MABSSetup.ini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="20e8c-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="20e8c-110">Merhaba MABSSetup.ini dosyasındaki kodu aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="20e8c-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="20e8c-111">Merhaba metni hello ayraç içinde Değiştir (\< \>), ortamınızdan değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="20e8c-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="20e8c-112">metin aşağıdaki hello bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="20e8c-112">hello following text is an example:</span></span>

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. <span data-ttu-id="20e8c-113">Merhaba dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="20e8c-113">Save hello file.</span></span> <span data-ttu-id="20e8c-114">Ardından, bir yükseltilmiş komut isteminde hello yükleme sunucusunda şu komutu girin:</span><span class="sxs-lookup"><span data-stu-id="20e8c-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="20e8c-115">Bu bayrakların hello yükleme için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="20e8c-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="20e8c-116">
**/f**: .ini dosya yolu</span><span class="sxs-lookup"><span data-stu-id="20e8c-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="20e8c-117">
**/l**: günlük dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="20e8c-117">
**/l**: Log path</span></span></br><span data-ttu-id="20e8c-118">
**/ı**: yükleme yolu</span><span class="sxs-lookup"><span data-stu-id="20e8c-118">
**/i**: Installation path</span></span></br><span data-ttu-id="20e8c-119">
**/x**: yol kaldırma</span><span class="sxs-lookup"><span data-stu-id="20e8c-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="20e8c-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20e8c-120">Next steps</span></span>
<span data-ttu-id="20e8c-121">Yedekleme sunucusu yükledikten sonra bilgi nasıl tooprepare sunucunuz veya bir iş yükü korumaya başlamak.</span><span class="sxs-lookup"><span data-stu-id="20e8c-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="20e8c-122">Yedekleme sunucusu iş yükleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="20e8c-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="20e8c-123">Bir VMware sunucusu yedekleme sunucusu tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="20e8c-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="20e8c-124">SQL Server Yedekleme Sunucusu tooback kullanın</span><span class="sxs-lookup"><span data-stu-id="20e8c-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="20e8c-125">Modern yedekleme depolama tooBackup sunucu ekleme</span><span class="sxs-lookup"><span data-stu-id="20e8c-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
