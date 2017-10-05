---
title: "Azure yedekleme sunucusu v2 sessiz yüklemesi | Microsoft Docs"
description: "Azure yedekleme sunucusu v2 sessizce yüklemek için bir PowerShell betiğini kullanın. Bu tür bir yükleme, katılımsız bir yükleme olarak da adlandırılır."
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="247ed-104">Azure yedekleme sunucusu v2 katılımsız yüklemesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="247ed-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="247ed-105">Azure yedekleme sunucusu v2 katılımsız yüklemesini çalıştırma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="247ed-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="247ed-106">Azure yedekleme sunucusu v1 yüklüyorsanız, bu adımları uygulamayın.</span><span class="sxs-lookup"><span data-stu-id="247ed-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="247ed-107">Yedek sunucu v2 yükleyin</span><span class="sxs-lookup"><span data-stu-id="247ed-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="247ed-108">Azure yedekleme sunucusu v2 barındıran sunucuda, bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="247ed-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="247ed-109">(Dosyasını Not Defteri'nde veya başka bir metin düzenleyicisinde oluşturabilirsiniz.) Dosyayı MABSSetup.ini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="247ed-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="247ed-110">Aşağıdaki kod MABSSetup.ini dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="247ed-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="247ed-111">Köşeli ayraçlar içindeki metni değiştirin (\< \>), ortamınızdan değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="247ed-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="247ed-112">Aşağıdaki metni bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="247ed-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="247ed-113">Dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="247ed-113">Save the file.</span></span> <span data-ttu-id="247ed-114">Ardından, bir yükseltilmiş komut isteminde yükleme sunucusunda şu komutu girin:</span><span class="sxs-lookup"><span data-stu-id="247ed-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="247ed-115">Bu bayrakların yükleme için kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="247ed-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="247ed-116">
**/f**: .ini dosya yolu</span><span class="sxs-lookup"><span data-stu-id="247ed-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="247ed-117">
**/l**: günlük dosyası yolu</span><span class="sxs-lookup"><span data-stu-id="247ed-117">
**/l**: Log path</span></span></br><span data-ttu-id="247ed-118">
**/ı**: yükleme yolu</span><span class="sxs-lookup"><span data-stu-id="247ed-118">
**/i**: Installation path</span></span></br><span data-ttu-id="247ed-119">
**/x**: yol kaldırma</span><span class="sxs-lookup"><span data-stu-id="247ed-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="247ed-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="247ed-120">Next steps</span></span>
<span data-ttu-id="247ed-121">Yedekleme sunucusu yükledikten sonra sunucunuzu hazırlama ya da bir iş yükü korumaya başlamak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="247ed-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="247ed-122">Yedekleme sunucusu iş yükleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="247ed-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="247ed-123">VMware sunucusunu yedeklemek için yedekleme sunucusu kullanın</span><span class="sxs-lookup"><span data-stu-id="247ed-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="247ed-124">SQL Server için yedekleme sunucusu kullanın</span><span class="sxs-lookup"><span data-stu-id="247ed-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="247ed-125">Modern yedekleme depolama yedekleme sunucusuna Ekle</span><span class="sxs-lookup"><span data-stu-id="247ed-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
