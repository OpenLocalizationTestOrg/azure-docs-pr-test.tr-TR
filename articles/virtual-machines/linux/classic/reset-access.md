---
title: "Linux VM parolası ve clı'dan SSH anahtarı sıfırlama | Microsoft Docs"
description: "Bir Linux VM parola veya SSH anahtarı sıfırlama, SSH yapılandırmasını düzeltmek ve disk tutarlılık denetimi için VMAccess uzantısını gelen Azure komut satırı arabirimi (CLI) kullanma"
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
ms.openlocfilehash: 74765877e7836d6878284b350a25d8355dc83d7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="7ac5f-103">Bir Linux VM parola veya SSH anahtarı sıfırlama, SSH yapılandırmasını düzeltmek ve VMAccess uzantısını kullanarak disk tutarlılık denetimi hakkında</span><span class="sxs-lookup"><span data-stu-id="7ac5f-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="7ac5f-104">Unutulmuş parola nedeniyle, yanlış bir güvenli Kabuk (SSH) anahtarını Azure Linux sanal makineye bağlanılamıyor veya SSH yapılandırması ile ilgili bir sorun VMAccessForLinux uzantısını Azure CLI ile parola veya SSH anahtarını sıfırlamak için kullanıyorsanız, SSH Düzelt Yapılandırma ve onay disk tutarlılık.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="7ac5f-105">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7ac5f-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7ac5f-106">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7ac5f-107">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7ac5f-108">[Bu adımları Resource Manager modeli kullanarak gerçekleştirmeyi](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="7ac5f-109">Azure CLI ile kullandığınız **azure vm uzantısı kümesi** komutlara erişmek için komut satırı arabiriminden (Bash, Terminal, komut istemi) komutu.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="7ac5f-110">Çalıştırma **azure Yardım vm uzantısı kümesi** ayrıntılı uzantısını kullanım için.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="7ac5f-111">Azure CLI ile bunu aşağıdaki görevleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7ac5f-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="7ac5f-112">Parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="7ac5f-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="7ac5f-113">SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="7ac5f-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="7ac5f-114">Parola ve SSH anahtarı sıfırlama</span><span class="sxs-lookup"><span data-stu-id="7ac5f-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="7ac5f-115">Yeni bir sudo kullanıcı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ac5f-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="7ac5f-116">SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="7ac5f-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="7ac5f-117">Kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="7ac5f-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="7ac5f-118">VMAccess uzantısını durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="7ac5f-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="7ac5f-119">Eklenen diskler tutarlılık denetimi</span><span class="sxs-lookup"><span data-stu-id="7ac5f-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="7ac5f-120">Linux VM eklenen disklerde onarın</span><span class="sxs-lookup"><span data-stu-id="7ac5f-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="7ac5f-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7ac5f-121">Prerequisites</span></span>
<span data-ttu-id="7ac5f-122">Aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7ac5f-122">You will need to do the following:</span></span>

* <span data-ttu-id="7ac5f-123">Etmeniz [Azure CLI yükleme](../../../cli-install-nodejs.md) ve [aboneliğinize bağlanma](../../../xplat-cli-connect.md) hesabınızla ilişkili Azure kaynaklarını kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="7ac5f-124">Komut isteminde aşağıdakini yazarak Klasik dağıtım modeli için doğru moda ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7ac5f-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="7ac5f-125">Bunlardan birini sıfırlamak istiyorsanız bir yeni bir parola veya SSH anahtarları kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="7ac5f-126">SSH yapılandırmasını sıfırlamak istiyorsanız, bu gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <span data-ttu-id="7ac5f-127"><a name="pwresetcli"></a>Parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="7ac5f-127"><a name="pwresetcli"></a>Reset the password</span></span>
1. <span data-ttu-id="7ac5f-128">Bu satırlar ile PrivateConf.json adlı yerel bilgisayarınızdaki bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="7ac5f-129">Değiştir **KullanıcıAdım** ve  **myP@ssW0rd**  kendi kullanıcı adı ve parola ile ve kendi sona erme tarihini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="7ac5f-130">Sanal makine için adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="7ac5f-131"><a name="sshkeyresetcli"></a>SSH anahtarını Sıfırla</span><span class="sxs-lookup"><span data-stu-id="7ac5f-131"><a name="sshkeyresetcli"></a>Reset the SSH key</span></span>
1. <span data-ttu-id="7ac5f-132">Bu içerikle PrivateConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="7ac5f-133">Değiştir **KullanıcıAdım** ve **mySSHKey** kendi bilgilerinizi değerlerle.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="7ac5f-134">Sanal makine için adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="7ac5f-135"><a name="resetbothcli"></a>Parola ve SSH anahtarı sıfırlama</span><span class="sxs-lookup"><span data-stu-id="7ac5f-135"><a name="resetbothcli"></a>Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="7ac5f-136">Bu içerikle PrivateConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="7ac5f-137">Değiştir **KullanıcıAdım**, **mySSHKey** ve  **myP@ssW0rd**  kendi bilgilerinizi değerlerle.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="7ac5f-138">Sanal makine için adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="7ac5f-139"><a name="createnewsudocli"></a>Yeni bir sudo kullanıcı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ac5f-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="7ac5f-140">Kullanıcı adınızı unutursanız, Vmaccess'in sudo yetkisine sahip yeni bir tane oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="7ac5f-141">Bu durumda, var olan kullanıcı adı ve parola değiştirilmeyecek.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="7ac5f-142">Parola erişimi ile yeni bir sudo kullanıcı oluşturmak için komut dosyasındaki kullanmak [parola sıfırlama](#pwresetcli) ve yeni bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="7ac5f-143">SSH anahtar erişimi ile yeni bir sudo kullanıcı oluşturmak için komut dosyasındaki kullanın [SSH anahtarı sıfırlama](#sshkeyresetcli) ve yeni bir kullanıcı adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="7ac5f-144">Aynı zamanda [parola ve SSH anahtarı sıfırlama](#resetbothcli) hem parola hem de SSH anahtar erişimi ile yeni bir kullanıcı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="7ac5f-145"><a name="sshconfigresetcli"></a>SSH yapılandırmasını sıfırlayın</span><span class="sxs-lookup"><span data-stu-id="7ac5f-145"><a name="sshconfigresetcli"></a>Reset the SSH configuration</span></span>
<span data-ttu-id="7ac5f-146">SSH yapılandırması istenmeyen bir durumda ise, erişim VM'ye kaybedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="7ac5f-147">Varsayılan durumuna getirmek yapılandırmasını sıfırlamak için VMAccess uzantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="7ac5f-148">Bunu yapmak için yalnızca "True" "reset_ssh" anahtarını ayarlamak yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="7ac5f-149">Uzantı SSH sunucuyu yeniden başlatın, VM'yi SSH bağlantı noktası açın ve SSH yapılandırmasını varsayılan değerlere sıfırla.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="7ac5f-150">Kullanıcı hesabı (adı, parola veya SSH anahtarları) değiştirilmez.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="7ac5f-151">Sıfırlama SSH yapılandırma dosyası /etc/ssh/sshd_config bulunur.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="7ac5f-152">Bu içerikle PrivateConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="7ac5f-153">Sanal makine için adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="7ac5f-154"><a name="deletecli"></a>Kullanıcı silme</span><span class="sxs-lookup"><span data-stu-id="7ac5f-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="7ac5f-155">Oturum açmayı VM doğrudan olmadan bir kullanıcı hesabı silmek istiyorsanız, bu komut dosyasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="7ac5f-156">İçin kaldırmak için kullanıcı adını değiştirerek bu içerikle PrivateConf.json adlı bir dosya oluşturun **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="7ac5f-157">Sanal makine için adını değiştirerek bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="7ac5f-158"><a name="statuscli"></a>VMAccess uzantısını durumunu görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="7ac5f-158"><a name="statuscli"></a>Display the status of the VMAccess extension</span></span>
<span data-ttu-id="7ac5f-159">VMAccess uzantısını durumunu görüntülemek için bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="7ac5f-160"><a name='checkdisk'></a>Eklenen diskler tutarlılık denetimi</span><span class="sxs-lookup"><span data-stu-id="7ac5f-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="7ac5f-161">Linux sanal makinedeki tüm disklerde fsck çalıştırmak için aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7ac5f-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="7ac5f-162">Bu içerikle PublicConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="7ac5f-163">Onay Disk veya sanal makinenize bağlı diskler denetlenip denetlenmeyeceğini için bir Boole değeri alır.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="7ac5f-164">Sanal makine için adını değiştirerek yürütmek için bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="7ac5f-165"><a name='repairdisk'></a>Onarım diskleri</span><span class="sxs-lookup"><span data-stu-id="7ac5f-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="7ac5f-166">Değil bağlanması veya takma yapılandırma hataları olan diskleri onarmak için Linux sanal makinenizde bağlama yapılandırmasını sıfırlamak için VMAccess uzantısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="7ac5f-167">İçin disk adınızı değiştirerek **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="7ac5f-168">Bu içerikle PublicConf.json adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="7ac5f-169">Sanal makine için adını değiştirerek yürütmek için bu komutu çalıştırmak **myVM**.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="7ac5f-170">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7ac5f-170">Next steps</span></span>
* <span data-ttu-id="7ac5f-171">Parola veya SSH anahtarını sıfırlamak için Azure PowerShell cmdlet'lerini veya Azure Resource Manager şablonları kullanmak istiyorsanız, SSH yapılandırması ve onay disk tutarlılık, bkz: düzeltme [VMAccess uzantısını belgelerine github'da](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="7ac5f-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="7ac5f-172">Aynı zamanda [Azure portal](https://portal.azure.com) parola veya SSH anahtarı bir Linux VM sıfırlamak için Klasik dağıtım modelinde dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="7ac5f-173">Şu anda portal do kullanamazsınız Resource Manager dağıtım modelinde dağıtılan bu bir Linux VM için.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="7ac5f-174">Bkz: [sanal makine uzantıları ve özellikleri hakkında](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure sanal makineler için VM uzantıları kullanma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="7ac5f-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

