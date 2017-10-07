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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Azure yedekleme sunucusu v2 katılımsız yüklemesini çalıştırın

Bilgi nasıl toorun Azure yedekleme sunucusu v2 katılımsız yüklemesi. 

Azure yedekleme sunucusu v1 yüklüyorsanız, bu adımları uygulamayın.

## <a name="install-backup-server-v2"></a>Yedek sunucu v2 yükleyin

1. Azure yedekleme sunucusu v2 barındıran hello sunucusunda, bir metin dosyası oluşturun. (Merhaba dosyasını Not Defteri'nde veya başka bir metin düzenleyicisi oluşturabilirsiniz.) Merhaba dosyayı MABSSetup.ini kaydedin. 

2. Merhaba MABSSetup.ini dosyasındaki kodu aşağıdaki hello yapıştırın. Merhaba metni hello ayraç içinde Değiştir (\< \>), ortamınızdan değerlere sahip. metin aşağıdaki hello bir örnek verilmiştir:

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

3. Merhaba dosyasını kaydedin. Ardından, bir yükseltilmiş komut isteminde hello yükleme sunucusunda şu komutu girin:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Bu bayrakların hello yükleme için kullanabilirsiniz:</br>
**/f**: .ini dosya yolu</br>
**/l**: günlük dosyası yolu</br>
**/ı**: yükleme yolu</br>
**/x**: yol kaldırma</br>

## <a name="next-steps"></a>Sonraki adımlar
Yedekleme sunucusu yükledikten sonra bilgi nasıl tooprepare sunucunuz veya bir iş yükü korumaya başlamak.

- [Yedekleme sunucusu iş yükleri hazırlama](backup-azure-microsoft-azure-backup.md)
- [Bir VMware sunucusu yedekleme sunucusu tooback kullanın](backup-azure-backup-server-vmware.md)
- [SQL Server Yedekleme Sunucusu tooback kullanın](backup-azure-sql-mabs.md)
- [Modern yedekleme depolama tooBackup sunucu ekleme](backup-mabs-add-storage.md)
