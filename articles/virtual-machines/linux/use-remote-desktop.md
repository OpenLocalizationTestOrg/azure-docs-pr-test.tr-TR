---
title: "aaaUse Uzak Masaüstü tooa Azure Linux VM'de | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Azure'da grafik araçları kullanarak Uzak Masaüstü'nü (xrdp) tooconnect tooa Linux VM yapılandırın"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a>Yükleme ve Uzak Masaüstü tooconnect tooa Linux VM Azure'da yapılandırma
Azure'daki Linux sanal makineleri (VM'ler) genellikle hello bir güvenli Kabuk (SSH) bağlantısı kullanarak komut satırından yönetilir. Zaman yeni tooLinux veya hızlı sorun giderme senaryoları için Uzak Masaüstü hello kullanımını daha kolay olabilir. Bu makale ayrıntıları nasıl tooinstall ve bir masaüstü ortamını yapılandırma ([xfce](https://www.xfce.org)) ve Uzak Masaüstü'nü ([xrdp](http://www.xrdp.org)) hello Resource Manager dağıtım modeli kullanarak, Linux VM için.


## <a name="prerequisites"></a>Ön koşullar
Bu makalede, azure'da var olan bir Linux VM gerektirir. Toocreate VM gerekiyorsa, yöntemler aşağıdaki hello birini kullanın:

- Merhaba [Azure CLI 2.0](quick-create-cli.md)
- Merhaba [Azure portalı](quick-create-portal.md)


## <a name="install-a-desktop-environment-on-your-linux-vm"></a>Bir masaüstü ortamı, Linux VM olanağına yükle
Çoğu Linux VM'ler için Azure'da varsayılan olarak yüklenen bir masaüstü ortamı yok. Linux VM'ler genellikle bir masaüstü ortamı yerine SSH bağlantısını kullanılarak yönetilir. Seçebileceğiniz Linux çeşitli masaüstü ortamlarında vardır. Tercih ettiğiniz Masaüstü ortamının bağlı olarak, bunu bir too2 GB disk alanı kullanabilir ve 5 too10 dakika tooinstall alın ve tüm gerekli hello paketler yapılandırın.

Merhaba aşağıdaki örnek yükler hello basit [xfce4](https://www.xfce.org/) bir Ubuntu VM Masaüstü ortamı. Komutları, diğer dağıtımlar biraz farklılık gösterir (kullanmak `yum` tooinstall Red Hat Enterprise Linux üzerinde ve uygun yapılandırma `selinux` kuralları ya da kullanım `zypper` örneğin SUSE üzerinde tooinstall).

İlk olarak, SSH tooyour VM. Merhaba aşağıdaki örnek bağlayan toohello adlı VM *myvm.westus.cloudapp.azure.com* hello kullanıcı adı ile *azureuser*:

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Windows kullanıyorsanız ve SSH kullanma hakkında daha fazla bilgi için bkz: [nasıl ile Windows toouse SSH anahtarları](ssh-from-windows.md).

Ardından, xfce kullanarak yükleyin `apt` gibi:

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a>Uzak Masaüstü sunucusu yükleme ve yapılandırma
Yüklü bir masaüstü ortamı sahip olduğunuza göre bir Uzak Masaüstü hizmet toolisten gelen bağlantıları için yapılandırın. [xrdp](http://xrdp.org) çoğu Linux dağıtımları hakkında kullanılabilir ve çalışır iyi xfce ile bir açık kaynak Uzak Masaüstü Protokolü (RDP) sunucusudur. Xrdp Ubuntu VM üzerinde aşağıdaki gibi yükleyin:

```bash
sudo apt-get install xrdp
```

Oturumunuz başlattığınızda xrdp hangi masaüstü ortamında toouse söyleyin. Xrdp toouse xfce masaüstü ortamınızı aşağıdaki gibi yapılandırın:

```bash
echo xfce4-session >~/.xsession
```

Merhaba xrdp hizmeti hello değişiklikleri tootake etkisi için aşağıdaki gibi yeniden başlatın:

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a>Bir yerel kullanıcı hesabı parolasını ayarlama
VM'nizi oluşturduğunuzda kullanıcı hesabınız için bir parola oluşturduysanız, bu adımı atlayın. Yalnızca SSH anahtar kimlik doğrulaması kullanmak ve yok bir yerel hesap parola ayarlayın, xrdp toolog tooyour VM kullanmadan önce bir parola belirtmek istiyorsanız. xrdp kimlik doğrulaması için SSH anahtarları kabul edemez. Merhaba aşağıdaki örnekte bir hello kullanıcı hesabının parolasını belirtir *azureuser*:

```bash
sudo passwd azureuser
```

> [!NOTE]
> Şu anda mevcut değilse parola belirterek SSHD yapılandırma toopermit parolalı oturum açma güncelleştirmez. Güvenlik açısından bakıldığında, tooxrdp bağlanmak ve anahtar tabanlı kimlik doğrulaması kullanarak SSH tüneli ile tooconnect tooyour VM istiyor olabilirsiniz. Bu durumda, bir ağ güvenlik grubu kural tooallow Uzak Masaüstü trafiği oluşturma ile ilgili adımı takip hello atlayın.


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a>Uzak Masaüstü trafiği için ağ güvenlik grubu kural oluşturma
tooallow Uzak Masaüstü trafiği tooreach Linux VM, bir ağ güvenlik grubu kural oluşturulan toobe izin veren TCP bağlantı noktası 3389 tooreach üzerinde VM gerekir. Ağ güvenlik grubu kuralları hakkında daha fazla bilgi için bkz: [bir ağ güvenlik grubu nedir?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Ayrıca [kullanım hello Azure portal toocreate bir ağ güvenlik grubu kural](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Merhaba aşağıdaki örnekleri oluşturma sahip bir ağ güvenlik grubu kural [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) adlı *myNetworkSecurityGroupRule* çok*izin* trafiğinde*tcp* bağlantı noktası *3389*.

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a>Linux VM ile bir Uzak Masaüstü İstemcisi Bağlan
Yerel, Uzak Masaüstü İstemcisi'ni açın ve toohello IP adresi veya DNS adı Linux VM bağlayın. Merhaba kullanıcı adı ve parola hello kullanıcı hesabı için VM üzerinde şu şekilde girin:

![Uzak Masaüstü İstemcisi'ni kullanarak tooxrdp Bağlan](./media/use-remote-desktop/remote-desktop-client.png)

Kimlik doğrulandıktan sonra hello xfce masaüstü ortamını yükleyin ve aşağıdaki örneğine benzer toohello bakın:

![xrdp aracılığıyla xfce Masaüstü ortamı](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a>Sorun giderme
Tooyour bir Uzak Masaüstü istemcisi kullanarak Linux VM bağlanamıyorsanız kullanmak `netstat` , VM için RDP bağlantıları gibi dinliyor, Linux VM tooverify üzerinde:

```bash
sudo netstat -plnt | grep rdp
```

Aşağıdaki örnekte gösterildiği hello beklendiği gibi 3389 numaralı TCP bağlantı noktasında dinleme VM hello:

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

Merhaba xrdp hizmet dinleme yapmıyorsanız bir Ubuntu VM üzerinde aşağıdaki gibi hello hizmetini yeniden başlatın:

```bash
sudo service xrdp restart
```

Gözden geçirme oturum açtığında */var/log*Thug toowhy hello hizmet olarak göstergeleri için Ubuntu VM üzerinde yanıt. Uzak Masaüstü bağlantı denemesi tooview sırasında hataları hello syslog da izleyebilirsiniz:

```bash
tail -f /var/log/syslog
```

Red Hat Enterprise Linux ve SUSE gibi diğer Linux dağıtımları farklı şekillerde toorestart Hizmetleri ve diğer günlük dosyası konumları tooreview olabilir.

Herhangi bir yanıt, Uzak Masaüstü İstemcisi almaz ve hello sistem günlüğündeki tüm olayları görmüyorsanız, Uzak Masaüstü trafik hello VM ulaşamıyor Bu davranış gösterir. Bir kural toopermit TCP bağlantı noktası 3389 sahip, ağ güvenlik grubu kuralları tooensure gözden geçirin. Daha fazla bilgi için bkz: [uygulama bağlantı sorunlarını giderme](../windows/troubleshoot-app-connection.md).


## <a name="next-steps"></a>Sonraki adımlar
Oluşturma ve Linux VM'ler ile SSH anahtarları kullanma hakkında daha fazla bilgi için bkz: [oluşturma SSH anahtarları Azure Linux VM'ler için](mac-create-ssh-keys.md).

Windows SSH kullanma hakkında daha fazla bilgi için bkz: [nasıl ile Windows toouse SSH anahtarları](ssh-from-windows.md).

