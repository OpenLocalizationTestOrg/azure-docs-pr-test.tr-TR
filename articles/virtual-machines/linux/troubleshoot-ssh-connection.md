---
title: "aaaTroubleshoot SSH bağlantı sorunlarını tooan Azure VM | Microsoft Docs"
description: "Nasıl tootroubleshoot 'SSH bağlantısı başarısız oldu' veya 'SSH bağlantı reddedildi' gibi bir Azure VM için Linux çalıştıran verir."
keywords: "SSH bağlantı reddedildi, ssh hatası, azure ssh, SSH bağlantısı başarısız oldu"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a>SSH bağlantı tooan, hatalar, başarısız olur veya reddedilir Azure Linux VM'de sorun giderme
Güvenli Kabuk (SSH), SSH bağlantı hataları hatalarla veya tooconnect tooa Linux sanal makine (VM) çalıştığınızda SSH reddetti çeşitli nedenleri vardır. Bu makalede, bulma ve doğru hello sorunları yardımcı olur. Linux tootroubleshoot için hello Azure portal, Azure CLI ya da VM erişim uzantısı kullanın ve bağlantı sorunlarını giderin.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](http://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](http://azure.microsoft.com/support/options/) seçip **alma desteği**. Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](http://azure.microsoft.com/support/faq/).

## <a name="quick-troubleshooting-steps"></a>Hızlı sorun giderme adımları
Sorun giderme her adımdan sonra toohello VM yeniden bağlanmayı deneyin.

1. Merhaba SSH yapılandırmasını sıfırlayın.
2. Merhaba hello kullanıcının kimlik bilgilerini sıfırlayın.
3. Merhaba doğrulayın [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) kuralları SSH trafiğine izin verir.
   * Bir ağ güvenlik grubu kural toopermit SSH trafiği (varsayılan olarak, TCP bağlantı noktası 22) bulunduğundan emin olun.
   * Bağlantı noktası yeniden yönlendirmesine kullanamazsınız / Azure yük dengeleyici kullanmadan eşleme.
4. Merhaba denetleyin [VM kaynak durumu](../../resource-health/resource-health-overview.md). 
   * Bu hello VM olun sağlıklı olarak rapor.
   * Önyükleme tanılaması etkin varsa, hello VM önyükleme hataları hello günlüklerine bildirmeyen doğrulayın.
5. Merhaba VM yeniden başlatın.
6. Merhaba VM yeniden dağıtın.

Daha ayrıntılı sorun giderme adımları ve açıklamalar için okuma devam edin.

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a>Kullanılabilir yöntemleri tootroubleshoot SSH bağlantı sorunları
Kimlik bilgileri veya yöntemler aşağıdaki hello birini kullanarak SSH yapılandırması sıfırlayabilirsiniz:

* [Azure portal](#use-the-azure-portal) - tooquickly gerekiyorsa mükemmel hello SSH yapılandırması veya SSH anahtarı sıfırlama ve, yok sahip hello Azure Araçları yüklü.
* [Azure CLI 2.0](#use-the-azure-cli-20) - zaten hello komut satırında hızla sıfırlama hello SSH yapılandırması veya kimlik bilgileri kullanıyorsanız. Merhaba de kullanabilirsiniz [Azure CLI 1.0](#use-the-azure-cli-10)
* [Azure VMAccessForLinux uzantısını](#use-the-vmaccess-extension) - oluşturmak ve json tanım dosyalarını tooreset hello SSH yapılandırması veya kullanıcı kimlik bilgilerini yeniden kullanabilir.

Sorun giderme her adımdan sonra tooyour VM yeniden bağlanmayı deneyin. Hala bağlanamıyorsanız, sonraki adıma hello deneyin.

## <a name="use-hello-azure-portal"></a>Hello Azure portalını kullanın
Hello Azure portal, yerel bilgisayarınızda herhangi bir aracı yüklemeden hızlı şekilde tooreset hello SSH yapılandırması veya kullanıcı kimlik bilgilerini sağlar.

VM hello Azure portal'ı seçin. Toohello aşağı **destek + sorun giderme** bölümünde ve seçin **parola sıfırlama** aşağıdaki örneğine hello olduğu gibi:

![SSH yapılandırması veya hello Azure portal kimlik bilgilerini sıfırlama](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a>Merhaba SSH yapılandırmasını sıfırlayın
İlk adım olarak, seçin `Reset configuration only` hello gelen **modu** açılır menü ekran, önceki hello gibi ardından hello **sıfırlama** düğmesi. Bu işlem tamamlandıktan sonra tooaccess VM'yi yeniden deneyin.

### <a name="reset-ssh-credentials-for-a-user"></a>Bir kullanıcının SSH kimlik bilgilerini sıfırlama
Mevcut bir kullanıcının tooreset hello kimlik bilgilerini seçin ya da `Reset SSH public key` veya `Reset password` hello gelen **modu** ekran görüntüsü önceki hello olduğu gibi açılır menü. Merhaba kullanıcı adı ve bir SSH anahtarı veya yeni bir parola belirtin ve ardından hello **sıfırlama** düğmesi.

Bu menüden hello VM sudo ayrıcalıklarına sahip bir kullanıcı da oluşturabilirsiniz. Yeni kullanıcı adı ve ilişkili parolayı veya SSH anahtarını girin ve hello ardından **sıfırlama** düğmesi.

## <a name="use-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanın
Henüz yapmadıysanız, hello son yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).

Oluşturulan ve özel Linux disk görüntü karşıya emin hello olun [Microsoft Azure Linux Aracısı](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) sürüm 2.0.5 veya üstü yüklü. Galeri görüntüleri kullanılarak oluşturulan VM'ler için bu erişim uzantısı zaten yüklenmiş ve sizin için yapılandırılmış.

### <a name="reset-ssh-configuration"></a>SSH yapılandırmasını sıfırlayın
Başlangıçta deneyin sıfırlama hello SSH yapılandırma toodefault değerlerini ve hello VM yeniden başlatılan hello SSH sunucuda kullanabilirsiniz. Bu hello kullanıcı hesabı adı, parola veya SSH anahtarları değiştirmez olduğunu unutmayın.
Merhaba aşağıdaki örnek kullanır [az vm kullanıcı sıfırlama-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH yapılandırması hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a>Bir kullanıcının SSH kimlik bilgilerini sıfırlama
Merhaba aşağıdaki örnek kullanır [az vm kullanıcı güncelleştirme](/cli/azure/vm/user#update) tooreset hello kimlik bilgileri için `myUsername` belirtilen toohello değer `myPassword`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

SSH anahtar kimlik doğrulaması kullanıyorsanız, belirli bir kullanıcı için hello SSH anahtarı sıfırlayabilirsiniz. Merhaba aşağıdaki örnek kullanır **az vm erişim kümesi linux kullanıcı** tooupdate hello SSH anahtarı depolanır `~/.ssh/id_rsa.pub` adlı hello kullanıcı için `myUsername`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a>Merhaba VMAccess uzantısını kullanın
Merhaba Linux VM erişim uzantısını Eylemler toocarry çıkışı tanımlayan bir json dosyası olarak okur. Bu eylemler SSHD sıfırlama, bir SSH anahtarı sıfırlanıyor veya bir kullanıcı ekleme içerir. Hala hello Azure CLI toocall hello VMAccess uzantısını kullanır ancak hello json dosyaları arasında birden çok VM isterseniz yeniden kullanabilirsiniz. Bu yaklaşım toocreate sonra için senaryoları çağrılabilir json dosyalarınızın bir havuz sağlar.

### <a name="reset-sshd"></a>SSHD Sıfırla
Adlı bir dosya oluşturun `settings.json` içeriği aşağıdaki hello ile:

```json
{  
    "reset_ssh":"True"
}
```

Hello Azure CLI kullanarak, ardından hello çağırırsınız `VMAccessForLinux` uzantısı tooreset json dosyanız belirterek SSHD bağlantınızı. Merhaba aşağıdaki örnek kullanır [az vm uzantısı kümesi](/cli/azure/vm/extension#set) tooreset SSHD hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a>Bir kullanıcının SSH kimlik bilgilerini sıfırlama
SSHD toofunction doğru görünüyorsa, hello kullanıcının kimlik bilgilerini bir tireyle sıfırlayabilirsiniz. tooreset hello bir kullanıcının parolasını adlı bir dosya oluşturun `settings.json`. Merhaba aşağıdaki örnek sıfırlar hello kimlik bilgilerini `myUsername` belirtilen toohello değer `myPassword`. Satırlara aşağıdaki hello girin, `settings.json` dosya, kendi değerlerini kullanarak:

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

Veya SSH anahtarı bir kullanıcı için Merhaba, ilk adlı bir dosya oluşturun tooreset `settings.json`. Merhaba aşağıdaki örnek sıfırlar hello kimlik bilgilerini `myUsername` belirtilen toohello değer `myPassword`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Satırlara aşağıdaki hello girin, `settings.json` dosya, kendi değerlerini kullanarak:

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

Json dosyanızı oluşturduktan sonra hello Azure CLI toocall hello kullan `VMAccessForLinux` SSH kullanıcı kimlik bilgileri json dosyanız belirterek uzantısı tooreset. Merhaba aşağıdaki örnek sıfırlar hello adlı VM kimlik bilgisi `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a>Hello Azure CLI 1.0 kullanın
Henüz yapmadıysanız [hello Azure CLI 1.0 yükleyin ve tooyour Azure aboneliğine bağlanma](../../cli-install-nodejs.md). Resource Manager moduna gibi kullandığınızdan emin olun:

```azurecli
azure config mode arm
```

Oluşturulan ve özel Linux disk görüntü karşıya emin hello olun [Microsoft Azure Linux Aracısı](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) sürüm 2.0.5 veya üstü yüklü. Galeri görüntüleri kullanılarak oluşturulan VM'ler için bu erişim uzantısı zaten yüklenmiş ve sizin için yapılandırılmış.

### <a name="reset-ssh-configuration"></a>SSH yapılandırmasını sıfırlayın
Merhaba SSHD yapılandırma kendisini yanlış veya hello hizmeti bir hatayla karşılaştı. SSHD toomake hello SSH yapılandırması kendisini geçerli olduğundan emin sıfırlayabilirsiniz. SSHD sıfırlama hello ilk sorun giderme adımı gerçekleştirmeniz gerekir.

Merhaba aşağıdaki örnek sıfırlar adlı VM üzerinde SSHD `myVM` adlı hello kaynak grubunda `myResourceGroup`. Kendi VM ve kaynak grubu adları şu şekilde kullanın:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a>Bir kullanıcının SSH kimlik bilgilerini sıfırlama
SSHD toofunction doğru görünüyorsa, tireyle kullanıcıya hello parolayı sıfırlayabilirsiniz. Merhaba aşağıdaki örnek sıfırlar hello kimlik bilgilerini `myUsername` belirtilen toohello değer `myPassword`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

SSH anahtar kimlik doğrulaması kullanıyorsanız, belirli bir kullanıcı için hello SSH anahtarı sıfırlayabilirsiniz. Şu örnek güncelleştirmeleri hello hello depolanan SSH anahtarı `~/.ssh/id_rsa.pub` adlı hello kullanıcı için `myUsername`, hello adlı VM üzerinde `myVM` içinde `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a>Bir VM’yi yeniden başlatma
Merhaba SSH yapılandırması ve kullanıcı kimlik bilgilerini sıfırlamak veya Bunun yapılması bir hatayla karşılaştı, temel alınan işlem sorunları hello VM tooaddress yeniden başlatmayı deneyebilirsiniz.

### <a name="azure-portal"></a>Azure portalına
kullanarak bir VM toorestart hello Azure portal, select tıklayın ve VM hello **yeniden** aşağıdaki örneğine hello olduğu gibi düğmesi:

![Bir VM hello Azure portalında yeniden başlatın](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Aşağıdaki örnek yeniden hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Merhaba aşağıdaki örnek kullanır [az vm yeniden başlatma](/cli/azure/vm#restart) toorestart hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a>Bir VM’yi yeniden dağıtma
Temel ağ sorunları düzeltebilir Azure VM tooanother düğümde yeniden dağıtabilirsiniz. Bir VM dağıtarak hakkında daha fazla bilgi için bkz: [dağıtmanız sanal makine toonew Azure düğümü](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Bu işlem tamamlandıktan sonra kısa ömürlü disk veriler kaybolur ve hello sanal makineyle ilişkili olan dinamik IP adreslerini güncelleştirilir.
> 
> 

### <a name="azure-portal"></a>Azure portalına
kullanarak bir VM tooredeploy hello Azure portal, select toohello aşağı kaydırın ve VM **destek + sorun giderme** bölümü. Hello tıklatın **dağıtmanız** aşağıdaki örneğine hello olduğu gibi düğmesi:

![VM hello Azure portal ile yeniden dağıtın](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a>Azure CLI 1.0
Aşağıdaki örnek yeniden dağıtır hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a>Azure CLI 2.0
Merhaba örnek kullanım [az vm dağıtın](/cli/azure/vm#redeploy) tooredeploy hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`. Kendi değerlerinizi aşağıdaki şekilde kullanın:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modeli kullanılarak oluşturulan sanal makineleri
Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş olan VM'ler için bu adımları tooresolve hello en sık karşılaşılan SSH bağlantı hataları deneyin. Her adımdan sonra toohello VM yeniden bağlanmayı deneyin.

* Uzaktan Erişim'hello sıfırlama [Azure portal](https://portal.azure.com). Üzerinde Azure portal Merhaba, VM'yi seçin ve hello tıklatın **uzaktan Sıfırla...**  düğmesi.
* Merhaba VM yeniden başlatın. Merhaba üzerinde [Azure portal](https://portal.azure.com), VM'yi seçin ve hello tıklatın **yeniden** düğmesi.
    
* Merhaba VM tooa yeni Azure düğümü yeniden dağıtın. Hakkında bilgi için tooredeploy bir VM bkz [dağıtmanız sanal makine toonew Azure düğümü](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
    Bu işlem tamamlandıktan sonra kısa ömürlü disk veriler kaybolur ve hello sanal makineyle ilişkili olan dinamik IP adreslerini güncelleştirilir.
* Merhaba yönergeleri izleyin [nasıl tooreset bir parola veya SSH Linux tabanlı sanal makineler için](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) için:
  
  * Merhaba parolayı veya SSH anahtarını sıfırlayın.
  * Oluşturma bir *sudo* kullanıcı hesabı.
  * Merhaba SSH yapılandırmasını sıfırlayın.
* Platform sorunları için Hello VM'nin kaynak sistem durumunu denetleyin.<br>
     VM seçin ve aşağı kaydırarak **ayarları** > **durum denetimi**.

## <a name="additional-resources"></a>Ek kaynaklar
* Aşağıdaki adımlar hello sonra hala tooSSH tooyour VM olup olmadığını görmek [sorun giderme adımlarını ayrıntılı](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview ek adımlar tooresolve sorununuzu.
* Uygulama erişimi sorunlarını giderme hakkında daha fazla bilgi için bkz: [bir Azure sanal makine üzerinde çalışan sorun giderme erişim tooan uygulama](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* Merhaba Klasik dağıtım modeli kullanılarak oluşturulan sanal makineler sorunlarını giderme hakkında daha fazla bilgi için bkz: [nasıl tooreset bir parola veya SSH Linux tabanlı sanal makineler için](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

