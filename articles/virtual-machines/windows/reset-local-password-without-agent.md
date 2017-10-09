---
title: "aaaReset Azure Aracısı olmadan yerel Windows parola | Microsoft Docs"
description: "Nasıl tooreset hello yerel Windows kullanıcı hesabının parolasını hello Azure Konuk aracısı yüklü olan veya bir VM üzerinde çalışan olmadığında"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Nasıl Azure VM için yerel Windows parola tooreset
Bir VM hello kullanarak azure'da hello yerel Windows parolasını sıfırlayabilir [Azure portalında veya Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure Konuk aracısı yüklü sağlanan. Bu yöntem hello birincil yolu tooreset bir Azure VM için bir parola kullanılır. Yanıt vermiyor veya özel bir görüntü dosyalarını karşıya yükledikten sonra tooinstall başarısız hello Azure Konuk Aracısı ile sorunlarla karşılaşırsanız, el ile Windows parolanızı sıfırlayabilirsiniz. Bu makalede nasıl tooreset ekleyerek bir yerel hesap parolası hello kaynak işletim sistemi sanal disk tooanother VM ayrıntıları verilmektedir. 

> [!WARNING]
> Yalnızca bu işlemi son çare olarak kullanın. Her zaman tooreset hello kullanarak bir parola deneyin [Azure portalında veya Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ilk.
> 
> 

## <a name="overview-of-hello-process"></a>Merhaba işlemine genel bakış
erişim toohello Azure Konuk Aracısı olduğunda sıfırlama Azure Windows VM için yerel bir parolası gerçekleştirmek için hello çekirdek adımlar aşağıdaki gibidir:

* Merhaba kaynak VM silin. Merhaba sanal diskler korunur.
* Merhaba kaynak sanal makinenin işletim sistemi disk tooanother VM hello ekleme, Azure aboneliğinizin aynı konumdaki. Bu VM VM sorun giderme başvurulan tooas hello ' dir.
* VM sorun giderme hello kullanarak, bazı yapılandırma dosyalarını hello kaynak sanal makinenin işletim sistemi diski oluşturun.
* VM sorun giderme hello Hello VM'ın işletim sistemi diski kullanımdan çıkarın.
* Resource Manager şablonu toocreate hello özgün sanal diski kullanarak VM, kullanın.
* Merhaba yeni VM önyüklemesinde, Merhaba, yapılandırma dosyaları gerekli hello kullanıcının hello parola güncelleştirme oluşturun.

## <a name="detailed-steps"></a>Ayrıntılı adımlar
Her zaman tooreset hello kullanarak bir parola deneyin [Azure portalında veya Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) aşağıdaki adımları hello denemeden önce. Başlamadan önce VM yedeği olduğundan emin olun. 

1. Silme hello Azure Portalı'nda VM etkilenen. Silme hello VM yalnızca hello meta verileri, hello Azure içinde VM hello başvurusu siler. Merhaba VM silindiğinde hello sanal diskler korunur:
   
   * Select hello VM hello Azure portal'ı tıklatın *silmek*:
     
     ![Var olan VM silme](./media/reset-local-password-without-agent/delete_vm.png)
2. VM sorun giderme hello kaynak sanal makinenin işletim sistemi disk toohello ekleyin. VM sorun giderme hello hello olmalıdır hello kaynak sanal makinenin işletim sistemi diski ile aynı bölgeye (gibi `West US`):
   
   * VM hello Azure portal sorunlarını giderme hello seçin. Tıklatın *diskleri* | *Attach varolan*:
     
     ![Varolan bir diski kullanıma açın](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Seçin *VHD dosyasını* ve kaynağınız VM içeriyorsa hello depolama hesabı seçin:
     
     ![Depolama hesabı seçme](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Merhaba kaynak kapsayıcısı seçin. Merhaba kaynak kapsayıcıdır genellikle *VHD'ler*:
     
     ![Depolama kapsayıcısı seçin](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Merhaba OS vhd tooattach seçin. Tıklatın *seçin* toocomplete hello işlemi:
     
     ![Kaynak sanal disk seçin](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. VM Uzak Masaüstü kullanarak sorun giderme toohello bağlanabilir ve hello kaynak sanal makinenin işletim sistemi diski görünür olduğundan emin olun.
   
   * VM hello Azure portal sorunlarını giderme hello tıklatıp *Bağlan*.
   * Yüklemeleri hello RDP dosyasını açın. Merhaba kullanıcı VM sorun giderme hello adını ve parolasını girin.
   * Dosya Gezgini'nde, bağlı hello veri diski için bakın. Merhaba VM'in VHD'nin olduğundan kaynak hello veriler yalnızca bağlı disk toohello VM sorun giderme hello F: sürücü olması:
     
     ![Bağlı veri diski görüntüleme](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Oluşturma `gpt.ini` içinde `\Windows\System32\GroupPolicy` hello kaynak VM'in sürücüde (toogpt.ini.bak yeniden adlandırın gpt.ini varsa):
   
   > [!WARNING]
   > Yanlışlıkla C:\Windows dosyalarında aşağıdaki hello oluşturmak işletim sistemi sürücüsü hello VM sorun giderme için hello emin olun. Aşağıdaki veri diski olarak bağlı olduğu VM kaynağınız için hello işletim sistemi sürücüsündeki dosyaları hello oluşturun.
   > 
   > 
   
   * Merhaba satırlardan hello eklemek `gpt.ini` oluşturduğunuz dosyası:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![GPT.ini oluşturma](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Oluşturma `scripts.ini` içinde `\Windows\System32\GroupPolicy\Machine\Scripts`. Gizli klasörlere gösterilen emin olun. Gerekirse, hello oluşturma `Machine` veya `Scripts` klasörler.
   
   * Aşağıdaki satırları hello hello eklemek `scripts.ini` oluşturduğunuz dosyası:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Scripts.ini oluşturma](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Oluşturma `FixAzureVM.cmd` içinde `\Windows\System32` içeriği izleyerek, değiştirme hello ile `<username>` ve `<newpassword>` kendi değerlerinizi ile:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![FixAzureVM.cmd oluşturma](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    Merhaba yeni parola tanımlarken, VM için yapılandırılmış hello parola karmaşıklığı gereksinimlerini karşılamalıdır.
7. Azure Portalı'nda VM sorun giderme hello hello diski kullanımdan çıkarın:
   
   * VM hello Azure portal sorunlarını giderme hello seçin, *diskleri*.
   * Select hello veri diski 2. adımda eklenen, tıklatın *ayırma*:
     
     ![Disk ayırma](./media/reset-local-password-without-agent/detach_disk.png)
8. Bir VM oluşturmadan önce hello URI tooyour kaynak işletim sistemi diski alın:
   
   * Select hello depolama hesabında hello Azure portal'ı tıklatın *BLOB'lar*.
   * Merhaba kapsayıcısı seçin. Merhaba kaynak kapsayıcıdır genellikle *VHD'ler*:
     
     ![Depolama hesabı blob seçin](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Kaynağınız VM OS VHD seçin ve hello tıklatın *kopya* düğmesine bir sonraki toohello *URL* adı:
     
     ![Kopya disk URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Bir VM hello kaynak sanal makinenin işletim sistemi diski oluşturun:
   
   * Kullanım [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate özel bir VHD VM'den. Merhaba tıklatın `Deploy tooAzure` düğmesini tooopen hello Azure portalıyla hello şablonlu ayrıntılarını sizin için doldurulur.
   * Merhaba VM için tüm hello önceki ayarlarını tooretain istiyorsanız seçin *Düzen şablonu* tooprovide var olan sanal ağ, alt ağ, ağ bağdaştırıcısı veya genel IP.
   * Merhaba, `OSDISKVHDURI` parametresi metin kutusu, VHD Kaynak URI elde adım önceki hello Yapıştır hello:
     
     ![Bir VM şablonu oluşturma](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. Yeni VM çalıştıran hello sonra toohello VM hello yeni parolayla hello belirttiğiniz Uzak Masaüstü kullanarak bağlanmak `FixAzureVM.cmd` komut dosyası.
11. Uzak oturum toohello yeni VM, aşağıdaki Kaldır hello hello çevresi tooclean dosyalar:
    
    * %Windir%\System32
      * FixAzureVM.cmd Kaldır
    * %Windir%\System32\GroupPolicy\Machine\
      * scripts.ini Kaldır
    * %Windir%\System32\GroupPolicy
      * (önce gpt.ini var ve toogpt.ini.bak, yeniden adlandırma hello .bak dosya geri toogpt.ini yeniden adlandırılmış varsa) GPT.ini Kaldır

## <a name="next-steps"></a>Sonraki adımlar
Uzak Masaüstü kullanarak hala bağlanamazsa, hello bkz [RDP sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Merhaba [sorun giderme kılavuzu RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) belirli adımları yerine yöntemleri sorun giderme sırasında arar. Ayrıca [Azure destek isteği açma](https://azure.microsoft.com/support/options/) uygulamalı Yardım için.

