---
title: "Linux VM parola aaaReset ve SSH anahtarı CLI hello | Microsoft Docs"
description: "Nasıl toouse hello VMAccess uzantısını hello Azure komut satırı arabirimi (CLI) tooreset bir Linux VM parola veya SSH anahtarı hello SSH yapılandırmasını düzeltmek ve disk tutarlılık denetimi"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="41121-103">Nasıl tooreset bir Linux VM parola veya SSH anahtarı hello SSH yapılandırmasını düzeltmek ve hello VMAccess uzantısını kullanarak disk tutarlılık denetimi</span><span class="sxs-lookup"><span data-stu-id="41121-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="41121-104">Unutulan parolayı, yanlış bir güvenli Kabuk (SSH) anahtarının veya hello SSH yapılandırması ile ilgili bir sorun nedeniyle Azure tooa Linux sanal makineye bağlanamıyorsanız, hello VMAccessForLinux uzantısını hello Azure CLI tooreset hello parola veya SSH anahtarı ile birlikte kullanmak için düzeltme SSH yapılandırması hello ve disk tutarlılık denetimi.</span><span class="sxs-lookup"><span data-stu-id="41121-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="41121-105">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="41121-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="41121-106">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="41121-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="41121-107">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="41121-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="41121-108">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="41121-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="41121-109">Hello Azure CLI ile kullandığınız hello **azure vm uzantısı kümesi** komut satırı arabirimi (Bash, Terminal, komut istemi) tooaccess komutlarının komutu.</span><span class="sxs-lookup"><span data-stu-id="41121-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="41121-110">Çalıştırma **azure Yardım vm uzantısı kümesi** ayrıntılı uzantısını kullanım için.</span><span class="sxs-lookup"><span data-stu-id="41121-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="41121-111">Hello Azure CLI ile yapabileceğiniz hello görevler:</span><span class="sxs-lookup"><span data-stu-id="41121-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="41121-112">Merhaba parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="41121-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="41121-113">Merhaba SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="41121-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="41121-114">Merhaba parola ve hello SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="41121-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="41121-115">Yeni bir sudo kullanıcı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41121-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="41121-116">Merhaba SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="41121-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="41121-117">Kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="41121-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="41121-118">Merhaba VMAccess uzantısını Hello durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="41121-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="41121-119">Eklenen diskler tutarlılık denetimi</span><span class="sxs-lookup"><span data-stu-id="41121-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="41121-120">Linux VM eklenen disklerde onarın</span><span class="sxs-lookup"><span data-stu-id="41121-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="41121-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="41121-121">Prerequisites</span></span>
<span data-ttu-id="41121-122">Toodo hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="41121-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="41121-123">Çok gerekir[hello Azure CLI yükleme](../../../cli-install-nodejs.md) ve [tooyour abonelik bağlanmak](../../../xplat-cli-connect.md) toouse Azure hesabınızla ilişkili kaynakları.</span><span class="sxs-lookup"><span data-stu-id="41121-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="41121-124">Merhaba Klasik dağıtım modeli için doğru moda Hello hello komut isteminde hello aşağıdakileri yazarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="41121-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="41121-125">Tooreset herhangi birini isterseniz yeni bir parola veya SSH anahtarlarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="41121-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="41121-126">Tooreset hello SSH yapılandırması istiyorsanız bu gerekmez.</span><span class="sxs-lookup"><span data-stu-id="41121-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="41121-127"><a name="pwresetcli"></a>Merhaba parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="41121-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="41121-128">Bu satırlar ile PrivateConf.json adlı yerel bilgisayarınızdaki bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41121-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="41121-129">Değiştir **KullanıcıAdım** ve  **myP@ssW0rd**  kendi kullanıcı adı ve parola ile ve kendi sona erme tarihini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="41121-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="41121-130">Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="41121-131"><a name="sshkeyresetcli"></a>Merhaba SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="41121-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="41121-132">Bu içerikle PrivateConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41121-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="41121-133">Hello yerine **KullanıcıAdım** ve **mySSHKey** kendi bilgilerinizi değerlerle.</span><span class="sxs-lookup"><span data-stu-id="41121-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="41121-134">Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="41121-135"><a name="resetbothcli"></a>Merhaba parola ve hello SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="41121-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="41121-136">Bu içerikle PrivateConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41121-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="41121-137">Hello yerine **KullanıcıAdım**, **mySSHKey** ve  **myP@ssW0rd**  kendi bilgilerinizi değerlerle.</span><span class="sxs-lookup"><span data-stu-id="41121-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="41121-138">Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="41121-139"><a name="createnewsudocli"></a>Yeni bir sudo kullanıcı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="41121-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="41121-140">Kullanıcı adınızı unutursanız, Vmaccess'in toocreate hello sudo yetkisine sahip yeni bir tane kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41121-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="41121-141">Bu durumda, hello olan bir kullanıcı adı ve parola değiştirilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="41121-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="41121-142">komut dosyası kullan hello parola erişimine sahip yeni bir sudo kullanıcı toocreate [hello parola sıfırlama](#pwresetcli) ve hello yeni bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="41121-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="41121-143">SSH anahtar erişimi, komut dosyası kullan hello sahip yeni bir sudo kullanıcı toocreate [sıfırlama hello SSH anahtarı](#sshkeyresetcli) ve hello yeni bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="41121-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="41121-144">Aynı zamanda [hello parola ve hello SSH anahtarını Sıfırla](#resetbothcli) toocreate hem parola hem de SSH anahtar erişimi olan yeni bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="41121-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="41121-145"><a name="sshconfigresetcli"></a>Merhaba SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="41121-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="41121-146">Merhaba SSH yapılandırması istenmeyen bir durumda ise, erişim toohello VM de kaybedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41121-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="41121-147">Merhaba VMAccess uzantısını tooreset hello yapılandırma tooits varsayılan durumu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41121-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="41121-148">toodo, tooset hello "reset_ssh" anahtar çok "True" yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="41121-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="41121-149">Merhaba uzantısı hello SSH sunucuyu yeniden başlatın, VM'yi hello SSH bağlantı noktası açın ve hello SSH yapılandırma toodefault değerlerini sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="41121-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="41121-150">Merhaba kullanıcı hesabı (adı, parola veya SSH anahtarları) değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="41121-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="41121-151">sıfırlama hello SSH yapılandırma dosyası /etc/ssh/sshd_config bulunur.</span><span class="sxs-lookup"><span data-stu-id="41121-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="41121-152">Bu içerikle PrivateConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41121-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="41121-153">Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="41121-154"><a name="deletecli"></a>Kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="41121-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="41121-155">Toodelete doğrudan oturum açmayı toohello VM olmadan bir kullanıcı hesabı istiyorsanız, bu komut dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41121-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="41121-156">Merhaba kullanıcı adı tooremove değiştirerek bu içerikle PrivateConf.json adlı bir dosya oluşturun **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="41121-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="41121-157">Sanal makine için Hello adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="41121-158"><a name="statuscli"></a>Merhaba VMAccess uzantısını Hello durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="41121-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="41121-159">Merhaba VMAccess uzantısını toodisplay hello durumu bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="41121-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="41121-160"><a name='checkdisk'></a>Eklenen diskler tutarlılık denetimi</span><span class="sxs-lookup"><span data-stu-id="41121-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="41121-161">toorun fsck Linux sanal makinedeki tüm disklerde toodo hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="41121-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="41121-162">Bu içerikle PublicConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41121-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="41121-163">Onay Disk olup olmadığını toocheck diskleri tooyour sanal makine veya bağlı için bir Boole değeri alır.</span><span class="sxs-lookup"><span data-stu-id="41121-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="41121-164">Sanal makine için Hello adını değiştirerek bu komut tooexecute çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="41121-165"><a name='repairdisk'></a>Onarım diskleri</span><span class="sxs-lookup"><span data-stu-id="41121-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="41121-166">bağlama yapılandırma hataları, değil bağlanması veya toorepair diskler Linux sanal makinenizde hello VMAccess uzantısını tooreset hello bağlama yapılandırması kullanın.</span><span class="sxs-lookup"><span data-stu-id="41121-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="41121-167">Merhaba adını değiştirerek diskiniz için **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="41121-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="41121-168">Bu içerikle PublicConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41121-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="41121-169">Sanal makine için Hello adını değiştirerek bu komut tooexecute çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="41121-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="41121-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41121-170">Next steps</span></span>
* <span data-ttu-id="41121-171">Toouse Azure PowerShell cmdlet'lerini veya Azure Resource Manager şablonları tooreset hello parola veya SSH anahtarı istiyorsanız, hello SSH yapılandırmasını düzeltmek ve disk tutarlılık denetimi, hello bkz [VMAccess uzantısını belgelerine github'da](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="41121-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="41121-172">Merhaba de kullanabilirsiniz [Azure portal](https://portal.azure.com) tooreset hello parola veya SSH anahtarı bir Linux VM dağıtılan hello Klasik dağıtım modelinde.</span><span class="sxs-lookup"><span data-stu-id="41121-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="41121-173">Bir Linux VM hello Resource Manager dağıtım modelinde dağıtılan hello portal toothis şu anda kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="41121-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="41121-174">Bkz: [sanal makine uzantıları ve özellikleri hakkında](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure sanal makineler için VM uzantıları kullanma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="41121-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

