---
title: "SSH’yi Hadoop - Azure HDInsight ile Kullanma | Microsoft Docs"
description: "Secure Shell (SSH) kullanarak HDInsight'a erişebilirsiniz. Bu belgede; Windows, Linux, Unix veya macOS istemcilerinden ssh ve scp komutlarını kullanarak HDInsight’a bağlanmaya ilişkin bilgi sağlanmıştır."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "linux’taki hadoop komutları,hadoop linux komutları,hadoop macos,ssh hadoop,ssh hadoop kümesi"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: df0feb51469333bac42c779d860192d46f24ac62
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-hdinsight-hadoop-using-ssh"></a><span data-ttu-id="bbf71-105">SSH kullanarak HDInsight’a (Hadoop) bağlanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-105">Connect to HDInsight (Hadoop) using SSH</span></span>

<span data-ttu-id="bbf71-106">[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) kullanarak Azure HDInsight’ta Hadoop’a güvenli bir şekilde bağlanma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-106">Learn how to use [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) to securely connect to Hadoop on Azure HDInsight.</span></span> 

<span data-ttu-id="bbf71-107">HDInsight, Hadoop kümesi içindeki düğümler için işletim sistemi olarak Linux’ı (Ubuntu) kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-107">HDInsight can use Linux (Ubuntu) as the operating system for nodes within the Hadoop cluster.</span></span> <span data-ttu-id="bbf71-108">Aşağıdaki tablo, SSH istemcisi kullanılarak Linux tabanlı HDInsight’a bağlanılırken gereken adres ve bağlantı noktası bilgilerini içerir:</span><span class="sxs-lookup"><span data-stu-id="bbf71-108">The following table contains the address and port information needed when connecting to Linux-based HDInsight using an SSH client:</span></span>

| <span data-ttu-id="bbf71-109">Adres</span><span class="sxs-lookup"><span data-stu-id="bbf71-109">Address</span></span> | <span data-ttu-id="bbf71-110">Bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="bbf71-110">Port</span></span> | <span data-ttu-id="bbf71-111">Bağlandığı yer...</span><span class="sxs-lookup"><span data-stu-id="bbf71-111">Connects to...</span></span> |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | <span data-ttu-id="bbf71-112">22</span><span class="sxs-lookup"><span data-stu-id="bbf71-112">22</span></span> | <span data-ttu-id="bbf71-113">Kenar düğümü (HDInsight üzerinde R Sunucusu)</span><span class="sxs-lookup"><span data-stu-id="bbf71-113">Edge node (R Server on HDInsight)</span></span> |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="bbf71-114">22</span><span class="sxs-lookup"><span data-stu-id="bbf71-114">22</span></span> | <span data-ttu-id="bbf71-115">Kenar düğümü (bir kenar düğümü varsa diğer küme türleri)</span><span class="sxs-lookup"><span data-stu-id="bbf71-115">Edge node (any other cluster type, if an edge node exists)</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="bbf71-116">22</span><span class="sxs-lookup"><span data-stu-id="bbf71-116">22</span></span> | <span data-ttu-id="bbf71-117">Birincil baş düğüm</span><span class="sxs-lookup"><span data-stu-id="bbf71-117">Primary headnode</span></span> |
| `<clustername>-ssh.azurehdinsight.net` | <span data-ttu-id="bbf71-118">23</span><span class="sxs-lookup"><span data-stu-id="bbf71-118">23</span></span> | <span data-ttu-id="bbf71-119">İkincil baş düğüm</span><span class="sxs-lookup"><span data-stu-id="bbf71-119">Secondary headnode</span></span> |

> [!NOTE]
> <span data-ttu-id="bbf71-120">`<edgenodename>` ifadesini kenar düğümünün adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-120">Replace `<edgenodename>` with the name of the edge node.</span></span>
>
> <span data-ttu-id="bbf71-121">`<clustername>` değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-121">Replace `<clustername>` with the name of your cluster.</span></span>
>
> <span data-ttu-id="bbf71-122">Kümeniz bir kenar düğümü içeriyorsa __kenar düğümüne her zaman SSH’yi kullanarak bağlanmanızı__ öneririz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-122">If your cluster contains an edge node, we recommend that you __always connect to the edge node__ using SSH.</span></span> <span data-ttu-id="bbf71-123">Baş düğümler, Hadoop’un sistem durumu için kritik öneme sahip olan hizmetleri barındırır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-123">The head nodes host services that are critical to the health of Hadoop.</span></span> <span data-ttu-id="bbf71-124">Kenar düğümü yalnızca üzerine yerleştirdiğiniz öğeleri çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-124">The edge node runs only what you put on it.</span></span>
>
> <span data-ttu-id="bbf71-125">Kenar düğümlerini kullanma hakkında daha fazla bilgi için bkz. [HDInsight’ta kenar düğümlerini kullanma](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span><span class="sxs-lookup"><span data-stu-id="bbf71-125">For more information on using edge nodes, see [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node).</span></span>

## <a name="ssh-clients"></a><span data-ttu-id="bbf71-126">SSH istemcileri</span><span class="sxs-lookup"><span data-stu-id="bbf71-126">SSH clients</span></span>

<span data-ttu-id="bbf71-127">Linux, Unix ve macOS sistemleri `ssh` ve `scp` komutlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbf71-127">Linux, Unix, and macOS systems provide the `ssh` and `scp` commands.</span></span> <span data-ttu-id="bbf71-128">`ssh` istemcisi, yaygın olarak Linux veya Unix tabanlı bir sistemle uzak komut satırı oturumu oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-128">The `ssh` client is commonly used to create a remote command-line session with a Linux or Unix-based system.</span></span> <span data-ttu-id="bbf71-129">`scp` istemcisi, dosyaları istemciniz ve uzak sistem arasında güvenli bir şekilde kopyalamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-129">The `scp` client is used to securely copy files between your client and the remote system.</span></span>

<span data-ttu-id="bbf71-130">Microsoft Windows, varsayılan olarak SSH istemcisi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-130">Microsoft Windows does not provide any SSH clients by default.</span></span> <span data-ttu-id="bbf71-131">`ssh` ve `scp` istemcileri, aşağıdaki paketler aracılığıyla Windows için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="bbf71-131">The `ssh` and `scp` clients are available for Windows through the following packages:</span></span>

* <span data-ttu-id="bbf71-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): Cloud Shell, tarayıcınızda bir Bash ortamı sunar. Ayrıca `ssh` ve `scp` komutu ile diğer sık kullanılan Linux komutlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbf71-132">[Azure Cloud Shell](../cloud-shell/quickstart.md): The Cloud Shell provides a Bash environment in your browser, and provides the `ssh`, `scp`, and other common Linux commands.</span></span>

* <span data-ttu-id="bbf71-133">[Windows 10 üzerinde Ubuntu’da Bash](https://msdn.microsoft.com/commandline/wsl/about): `ssh` ve `scp` komutları, Windows üzerinde Bash komut satırı ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-133">[Bash on Ubuntu on Windows 10](https://msdn.microsoft.com/commandline/wsl/about): The `ssh` and `scp` commands are available through the Bash on Windows command line.</span></span>

* <span data-ttu-id="bbf71-134">[Git (https://git-scm.com/)](https://git-scm.com/): `ssh` ve `scp` komutları, GitBash komut satırıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-134">[Git (https://git-scm.com/)](https://git-scm.com/): The `ssh` and `scp` commands are available through the GitBash command line.</span></span>

* <span data-ttu-id="bbf71-135">[GitHub Masaüstü (https://desktop.github.com/)](https://desktop.github.com/) `ssh` ve `scp` komutları, GitHub Kabuğu komut satırıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-135">[GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) The `ssh` and `scp` commands are available through the GitHub Shell command line.</span></span> <span data-ttu-id="bbf71-136">GitHub Masaüstü, Git Kabuğunun komut satırı olarak Bash, Windows Komut İstemi veya PowerShell kullanacak şekilde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-136">GitHub Desktop can be configured to use Bash, the Windows Command Prompt, or PowerShell as the command line for the Git Shell.</span></span>

* <span data-ttu-id="bbf71-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): PowerShell ekibi, OpenSSH’i Windows’a taşımakta ve test yayınları yapmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-137">[OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): The PowerShell team is porting OpenSSH to Windows, and provides test releases.</span></span>

    > [!WARNING]
    > <span data-ttu-id="bbf71-138">OpenSSH paketi, `sshd` adlı SSH sunucu bileşenini içerir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-138">The OpenSSH package includes the SSH server component, `sshd`.</span></span> <span data-ttu-id="bbf71-139">Bu bileşen, sisteminizde başkalarının bağlanmasına izin verilen bir SSH sunucusu başlatır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-139">This component starts an SSH server on your system, allowing others to connect to it.</span></span> <span data-ttu-id="bbf71-140">Sisteminizde bir SSH sunucusu barındırmak istemiyorsanız, bu bileşeni yapılandırmayın veya 22 numaralı bağlantı noktasını açmayın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-140">Do not configure this component or open port 22 unless you want to host an SSH server on your system.</span></span> <span data-ttu-id="bbf71-141">HDInsight ile iletişim kurulması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bbf71-141">It is not required to communicate with HDInsight.</span></span>

<span data-ttu-id="bbf71-142">Ayrıca [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) ve [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/) gibi çeşitli grafiksel SSH istemcisi mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="bbf71-142">There are also several graphical SSH clients, such as [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) and [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/).</span></span> <span data-ttu-id="bbf71-143">Bu istemciler HDInsight’a bağlanmak için kullanılabilse de bağlanma işlemi `ssh` yardımcı programını kullanmaktan farklıdır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-143">While these clients can be used to connect to HDInsight, the process of connecting is different than using the `ssh` utility.</span></span> <span data-ttu-id="bbf71-144">Daha fazla bilgi için, kullanmakta olduğunuz grafiksel istemcinin belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-144">For more information, see the documentation of the graphical client you are using.</span></span>

## <span data-ttu-id="bbf71-145"><a id="sshkey"></a>Kimlik doğrulaması: SSH Anahtarları</span><span class="sxs-lookup"><span data-stu-id="bbf71-145"><a id="sshkey"></a>Authentication: SSH Keys</span></span>

<span data-ttu-id="bbf71-146">SSH anahtarları, SSH oturumlarının kimliğini doğrulamak için [Ortak anahtar şifrelemesi](https://en.wikipedia.org/wiki/Public-key_cryptography) kullanır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-146">SSH keys use [Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) to authenticate SSH sessions.</span></span> <span data-ttu-id="bbf71-147">SSH anahtarları parolalara göre daha güvenlidir ve Hadoop kümenize erişimin güvenliğini sağlamak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbf71-147">SSH keys are more secure than passwords, and provide an easy way to secure access to your Hadoop cluster.</span></span>

<span data-ttu-id="bbf71-148">SSH hesabınızın güvenliği bir anahtar yardımıyla sağlanıyorsa, bağlantı kurduğunuzda istemci eşleşen özel anahtarı sağlamalıdır:</span><span class="sxs-lookup"><span data-stu-id="bbf71-148">If your SSH account is secured using a key, the client must provide the matching private key when you connect:</span></span>

* <span data-ttu-id="bbf71-149">Çoğu istemci, bir __varsayılan anahtar__ kullanmak üzere yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-149">Most clients can be configured to use a __default key__.</span></span> <span data-ttu-id="bbf71-150">Örneğin, `ssh` istemcisi Linux ve Unix ortamlarında `~/.ssh/id_rsa` üzerinde bir özel anahtar arar.</span><span class="sxs-lookup"><span data-stu-id="bbf71-150">For example, the `ssh` client looks for a private key at `~/.ssh/id_rsa` on Linux and Unix environments.</span></span>

* <span data-ttu-id="bbf71-151">__Özel anahtarın yolunu__ belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-151">You can specify the __path to a private key__.</span></span> <span data-ttu-id="bbf71-152">`ssh` istemcisi ile özel anahtarın yolunu belirtmek için `-i` parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-152">With the `ssh` client, the `-i` parameter is used to specify the path to private key.</span></span> <span data-ttu-id="bbf71-153">Örneğin, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="bbf71-153">For example, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.</span></span>

* <span data-ttu-id="bbf71-154">Farklı sunucularla kullanılacak __birden fazla özel anahtarınız__ varsa [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) gibi bir yardımcı program kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-154">If you have __multiple private keys__ for use with different servers, consider using a utility such as [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent).</span></span> <span data-ttu-id="bbf71-155">`ssh-agent` yardımcı programı, SSH oturumu oluşturulurken kullanılacak anahtarı otomatik olarak seçmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-155">The `ssh-agent` utility can be used to automatically select the key to use when establishing an SSH session.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="bbf71-156">Özel anahtarınızın güvenliğini şifre ile sağlıyorsanız, anahtarı kullanmak için şifreyi girmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-156">If you secure your private key with a passphrase, you must enter the passphrase when using the key.</span></span> <span data-ttu-id="bbf71-157">`ssh-agent` gibi yardımcı programlar, size kolaylık sağlamak için parolayı önbelleğe alabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-157">Utilities such as `ssh-agent` can cache the password for your convenience.</span></span>

### <a name="create-an-ssh-key-pair"></a><span data-ttu-id="bbf71-158">SSH anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbf71-158">Create an SSH key pair</span></span>

<span data-ttu-id="bbf71-159">Ortak ve özel anahtar dosyaları oluşturmak için `ssh-keygen` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-159">Use the `ssh-keygen` command to create public and private key files.</span></span> <span data-ttu-id="bbf71-160">Aşağıdaki komut, HDInsight ile kullanılabilecek bir 2048-bit RSA anahtar çifti oluşturur:</span><span class="sxs-lookup"><span data-stu-id="bbf71-160">The following command generates a 2048-bit RSA key pair that can be used with HDInsight:</span></span>

    ssh-keygen -t rsa -b 2048

<span data-ttu-id="bbf71-161">Anahtar oluşturma işlemi sırasında sizden bilgiler istenir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-161">You are prompted for information during the key creation process.</span></span> <span data-ttu-id="bbf71-162">Örneğin, anahtarların nerede depolanacağı veya şifre kullanılıp kullanılmayacağı.</span><span class="sxs-lookup"><span data-stu-id="bbf71-162">For example, where the keys are stored or whether to use a passphrase.</span></span> <span data-ttu-id="bbf71-163">İşlem tamamlandıktan sonra biri ortak anahtar, diğeri özel anahtar olmak üzere iki dosya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bbf71-163">After the process completes, two files are created; a public key and a private key.</span></span>

* <span data-ttu-id="bbf71-164">__Ortak anahtar__ bir HDInsight kümesi oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-164">The __public key__ is used to create an HDInsight cluster.</span></span> <span data-ttu-id="bbf71-165">Ortak anahtar `.pub` uzantısına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-165">The public key has an extension of `.pub`.</span></span>

* <span data-ttu-id="bbf71-166">__Özel anahtar__, HDInsight kümesinde istemcinizin kimliğini doğrulamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-166">The __private key__ is used to authenticate your client to the HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf71-167">Anahtarlarınızın güvenliğini şifre ile sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-167">You can secure your keys using a passphrase.</span></span> <span data-ttu-id="bbf71-168">Parola, aslında özel anahtarınız üzerindeki bir şifredir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-168">A passphrase is effectively a password on your private key.</span></span> <span data-ttu-id="bbf71-169">Özel anahtarınız başkası tarafından ele geçirilirse, anahtarın kullanılması için şifrenin girilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-169">Even if someone obtains your private key, they must have the passphrase to use the key.</span></span>

### <a name="create-hdinsight-using-the-public-key"></a><span data-ttu-id="bbf71-170">Ortak anahtar kullanarak HDInsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbf71-170">Create HDInsight using the public key</span></span>

| <span data-ttu-id="bbf71-171">Oluşturma yöntemi</span><span class="sxs-lookup"><span data-stu-id="bbf71-171">Creation method</span></span> | <span data-ttu-id="bbf71-172">Ortak anahtarı kullanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-172">How to use the public key</span></span> |
| ------- | ------- |
| <span data-ttu-id="bbf71-173">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="bbf71-173">**Azure portal**</span></span> | <span data-ttu-id="bbf71-174">__Küme oturumu açmak için kullanılan parolayı kullan__ seçeneğinin işaretini kaldırın ve ardından SSH kimlik doğrulama türü olarak __Ortak Anahtar__’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-174">Uncheck __Use same password as cluster login__, and then select __Public Key__ as the SSH authentication type.</span></span> <span data-ttu-id="bbf71-175">Son olarak, ortak anahtar dosyasını seçin veya dosyanın metin içeriğini __SSH ortak anahtarı__ alanına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-175">Finally, select the public key file or paste the text contents of the file in the __SSH public key__ field.</span></span></br><span data-ttu-id="bbf71-176">![HDInsight küme oluşturma işleminde SSH ortak anahtarı iletişim kutusu](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span><span class="sxs-lookup"><span data-stu-id="bbf71-176">![SSH public key dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png)</span></span> |
| <span data-ttu-id="bbf71-177">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="bbf71-177">**Azure PowerShell**</span></span> | <span data-ttu-id="bbf71-178">`New-AzureRmHdinsightCluster` cmdlet'inin `-SshPublicKey` parametresini kullanarak, ortak anahtarın içeriğini dize olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-178">Use the `-SshPublicKey` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass the contents of the public key as a string.</span></span>|
| <span data-ttu-id="bbf71-179">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="bbf71-179">**Azure CLI 1.0**</span></span> | <span data-ttu-id="bbf71-180">`azure hdinsight cluster create` komutunun `--sshPublicKey` parametresini kullanarak, ortak anahtarın içeriğini dize olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-180">Use the `--sshPublicKey` parameter of the `azure hdinsight cluster create` command and pass the contents of the public key as a string.</span></span> |
| <span data-ttu-id="bbf71-181">**Resource Manager Şablonu**</span><span class="sxs-lookup"><span data-stu-id="bbf71-181">**Resource Manager Template**</span></span> | <span data-ttu-id="bbf71-182">SSH anahtarlarını şablonla kullanma örneği için bkz. [HDInsight’ı SSH anahtarı ile Linux’a dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span><span class="sxs-lookup"><span data-stu-id="bbf71-182">For an example of using SSH keys with a template, see [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/).</span></span> <span data-ttu-id="bbf71-183">[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) dosyasında `publicKeys` öğesi, kümeyi oluştururken Azure’a anahtarları geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-183">The `publicKeys` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) file is used to pass the keys to Azure when creating the cluster.</span></span> |

## <span data-ttu-id="bbf71-184"><a id="sshpassword"></a>Kimlik doğrulaması: Parola</span><span class="sxs-lookup"><span data-stu-id="bbf71-184"><a id="sshpassword"></a>Authentication: Password</span></span>

<span data-ttu-id="bbf71-185">SSH hesaplarının güvenliği bir parola kullanılarak sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-185">SSH accounts can be secured using a password.</span></span> <span data-ttu-id="bbf71-186">SSH kullanarak HDInsight’a bağlandığınızda, parola girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-186">When you connect to HDInsight using SSH, you are prompted to enter the password.</span></span>

> [!WARNING]
> <span data-ttu-id="bbf71-187">SSH için parola kimlik doğrulamasının kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="bbf71-187">We do not recommend using password authentication for SSH.</span></span> <span data-ttu-id="bbf71-188">Parolalar tahmin edilebilir ve deneme yanılma saldırılarına karşı savunmasızdır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-188">Passwords can be guessed and are vulnerable to brute force attacks.</span></span> <span data-ttu-id="bbf71-189">Bunun yerine, [kimlik doğrulaması için SSH anahtarları](#sshkey) kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-189">Instead, we recommend that you use [SSH keys for authentication](#sshkey).</span></span>

### <a name="create-hdinsight-using-a-password"></a><span data-ttu-id="bbf71-190">Parola kullanarak HDInsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbf71-190">Create HDInsight using a password</span></span>

| <span data-ttu-id="bbf71-191">Oluşturma yöntemi</span><span class="sxs-lookup"><span data-stu-id="bbf71-191">Creation method</span></span> | <span data-ttu-id="bbf71-192">Parola belirtme</span><span class="sxs-lookup"><span data-stu-id="bbf71-192">How to specify the password</span></span> |
| --------------- | ---------------- |
| <span data-ttu-id="bbf71-193">**Azure portal**</span><span class="sxs-lookup"><span data-stu-id="bbf71-193">**Azure portal**</span></span> | <span data-ttu-id="bbf71-194">Varsayılan olarak, SSH kullanıcı hesabı ile küme oturum açma hesabı aynı parolaya sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-194">By default, the SSH user account has the same password as the cluster login account.</span></span> <span data-ttu-id="bbf71-195">Farklı bir parola kullanmak için __Küme oturumu açmak için kullanılan parolayı kullan__ seçeneğinin işaretini kaldırın ve __SSH parolası__ alanına parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-195">To use a different password, uncheck __Use same password as cluster login__, and then enter the password in the __SSH password__ field.</span></span></br><span data-ttu-id="bbf71-196">![HDInsight küme oluşturma işleminde SSH parolası iletişim kutusu](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span><span class="sxs-lookup"><span data-stu-id="bbf71-196">![SSH password dialog in HDInsight cluster creation](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)</span></span>|
| <span data-ttu-id="bbf71-197">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="bbf71-197">**Azure PowerShell**</span></span> | <span data-ttu-id="bbf71-198">`New-AzureRmHdinsightCluster` cmdlet’inin `--SshCredential` parametresini kullanın ve SSH kullanıcı hesabı adı ile parolasını içeren bir `PSCredential` nesnesi geçirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-198">Use the `--SshCredential` parameter of the `New-AzureRmHdinsightCluster` cmdlet and pass a `PSCredential` object that contains the SSH user account name and password.</span></span> |
| <span data-ttu-id="bbf71-199">**Azure CLI 1.0**</span><span class="sxs-lookup"><span data-stu-id="bbf71-199">**Azure CLI 1.0**</span></span> | <span data-ttu-id="bbf71-200">`azure hdinsight cluster create` komutunun `--sshPassword` parametresini kullanarak parola değerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-200">Use the `--sshPassword` parameter of the `azure hdinsight cluster create` command and provide the password value.</span></span> |
| <span data-ttu-id="bbf71-201">**Resource Manager Şablonu**</span><span class="sxs-lookup"><span data-stu-id="bbf71-201">**Resource Manager Template**</span></span> | <span data-ttu-id="bbf71-202">Parolayı şablonla kullanma örneği için bkz. [HDInsight’ı SSH parolası ile Linux’a dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span><span class="sxs-lookup"><span data-stu-id="bbf71-202">For an example of using a password with a template, see [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/).</span></span> <span data-ttu-id="bbf71-203">[azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) dosyasındaki `linuxOperatingSystemProfile` öğesi, kümeyi oluştururken SSH hesabı adı ile parolasını Azure’a geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-203">The `linuxOperatingSystemProfile` element in the [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) file is used to pass the SSH account name and password to Azure when creating the cluster.</span></span>|

### <a name="change-the-ssh-password"></a><span data-ttu-id="bbf71-204">SSH parolasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="bbf71-204">Change the SSH password</span></span>

<span data-ttu-id="bbf71-205">SSH kullanıcı hesabı parolasını değiştirme hakkında bilgi için, [HDInsight’ı Yönetme](hdinsight-administer-use-portal-linux.md#change-passwords) belgesinin __Parolaları değiştirme__ bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-205">For information on changing the SSH user account password, see the __Change passwords__ section of the [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) document.</span></span>

## <span data-ttu-id="bbf71-206"><a id="domainjoined"></a>Kimlik doğrulama: Etki alanına katılmış HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbf71-206"><a id="domainjoined"></a>Authentication: Domain-joined HDInsight</span></span>

<span data-ttu-id="bbf71-207">__Etki alanına katılmış HDInsight kümesi__ kullanıyorsanız, SSH ile bağlantı kurduktan sonra `kinit` komutunu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-207">If you are using a __domain-joined HDInsight cluster__, you must use the `kinit` command after connecting with SSH.</span></span> <span data-ttu-id="bbf71-208">Bu komut sizden bir etki alanı kullanıcı adı ile parolası ister ve kümenizle ilişkili Azure Active Directory etki alanını kullanarak oturumunuzun kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="bbf71-208">This command prompts you for a domain user and password, and authenticates your session with the Azure Active Directory domain associated with the cluster.</span></span>

<span data-ttu-id="bbf71-209">Daha fazla bilgi için bkz. [Etki alanına katılmış HDInsight yapılandırma](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bbf71-209">For more information, see [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md).</span></span>

## <a name="connect-to-nodes"></a><span data-ttu-id="bbf71-210">Düğümlere bağlanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-210">Connect to nodes</span></span>

<span data-ttu-id="bbf71-211">Baş düğümlere ve (varsa) kenar düğümüne İnternet üzerinden 22 ve 23 numaralı bağlantı noktalarıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-211">The head nodes and edge node (if there is one) can be accessed over the internet on ports 22 and 23.</span></span>

* <span data-ttu-id="bbf71-212">__Baş düğümlere__ bağlanırken, birincil baş düğüme bağlanmak için __22__, ikincil baş düğüme bağlanmak için __23__ numaralı bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-212">When connecting to the __head nodes__, use port __22__ to connect to the primary head node and port __23__ to connect to the secondary head node.</span></span> <span data-ttu-id="bbf71-213">Kullanılacak tam etki alanı adı `clustername-ssh.azurehdinsight.net`‘tir, burada `clustername` kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-213">The fully qualified domain name to use is `clustername-ssh.azurehdinsight.net`, where `clustername` is the name of your cluster.</span></span>

    ```bash
    # Connect to primary head node
    # port not specified since 22 is the default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect to secondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* <span data-ttu-id="bbf71-214">__Kenar düğümüne__ bağlanırken 22 numaralı bağlantı noktasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-214">When connectiung to the __edge node__, use port 22.</span></span> <span data-ttu-id="bbf71-215">Kullanılacak tam etki alanı adı `edgenodename.clustername-ssh.azurehdinsight.net`‘tir, burada `edgenodename` kenar düğümü oluştururken girdiğiniz addır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-215">The fully qualified domain name is `edgenodename.clustername-ssh.azurehdinsight.net`, where `edgenodename` is a name you provided when creating the edge node.</span></span> <span data-ttu-id="bbf71-216">`clustername`, kümenin adıdır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-216">`clustername` is the name of the cluster.</span></span>

    ```bash
    # Connect to edge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> <span data-ttu-id="bbf71-217">Önceki örneklerde, parola ile kimlik doğrulaması kullandığınız veya sertifika kimlik doğrulamasının otomatik olarak yapıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-217">The previous examples assume that you are using password authentication, or that certificate authentication is occuring automatically.</span></span> <span data-ttu-id="bbf71-218">Kimlik doğrulaması için bir SSH anahtar çifti kullanıyorsanız ve sertifika otomatik olarak kullanılmıyorsa, özel anahtarı belirtmek için `-i` parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-218">If you use an SSH key-pair for authentication, and the certificate is not used automatically, use the `-i` parameter to specify the private key.</span></span> <span data-ttu-id="bbf71-219">Örneğin, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="bbf71-219">For example, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.</span></span>

<span data-ttu-id="bbf71-220">Bağlantı kurulduktan sonra istem SSH kullanıcı adını ve bağlandığınız düğüm belirtecek şekilde değiştir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-220">Once connected, the prompt changes to indicate the SSH user name and the node you are connected to.</span></span> <span data-ttu-id="bbf71-221">Örneğin, `sshuser` olarak birincil baş düğüme bağlıyken komut istemi `sshuser@hn0-clustername:~$` değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-221">For example, when connected to the primary head node as `sshuser`, the prompt is `sshuser@hn0-clustername:~$`.</span></span>

### <a name="connect-to-worker-and-zookeeper-nodes"></a><span data-ttu-id="bbf71-222">Çalışan ve Zookeeper düğümlerine bağlanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-222">Connect to worker and Zookeeper nodes</span></span>

<span data-ttu-id="bbf71-223">Çalışan düğümlerine ve Zookeeper düğümlerine doğrudan internetten erişilemez.</span><span class="sxs-lookup"><span data-stu-id="bbf71-223">The worker nodes and Zookeeper nodes are not directly accessible from the internet.</span></span> <span data-ttu-id="bbf71-224">Bunlara, küme baş düğümleri veya kenar düğümlerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-224">They can be accessed from the cluster head nodes or edge nodes.</span></span> <span data-ttu-id="bbf71-225">Diğer düğümlere bağlanmak için uygulamanız gereken genel adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bbf71-225">The following are the general steps to connect to other nodes:</span></span>

1. <span data-ttu-id="bbf71-226">SSH kullanarak bir baş veya kenar düğümüne bağlanın:</span><span class="sxs-lookup"><span data-stu-id="bbf71-226">Use SSH to connect to a head or edge node:</span></span>

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. <span data-ttu-id="bbf71-227">Baş veya kenar düğümüne yaptığınız SSH bağlantısında `ssh` komutunu kullanarak kümedeki bir çalışan düğümüne bağlanın:</span><span class="sxs-lookup"><span data-stu-id="bbf71-227">From the SSH connection to the head or edge node, use the `ssh` command to connect to a worker node in the cluster:</span></span>

        ssh sshuser@wn0-myhdi

    <span data-ttu-id="bbf71-228">Kümedeki düğümlerin etki alanı adlarının listesini almak için [Ambari REST API’yi kullanarak HDInsight’ı yönetme](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) belgesine bakın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-228">To retrieve a list of the domain names of the nodes in the cluster, see the [Manage HDInsight by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.</span></span>

<span data-ttu-id="bbf71-229">SSH hesabının güvenliği bir __parola__ kullanılarak sağlanıyorsa bağlanırken parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-229">If the SSH account is secured using a __password__, enter the password when connecting.</span></span>

<span data-ttu-id="bbf71-230">SSH hesabının güvenliği __SSH anahtarları__ kullanılarak sağlanıyorsa istemciden SSH iletmenin etkinleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bbf71-230">If the SSH account is secured using __SSH keys__, make sure that SSH forwarding is enabled on the client.</span></span>

> [!NOTE]
> <span data-ttu-id="bbf71-231">Kümedeki tüm düğümlere doğrudan erişmenin başka bir yolu ise HDInsight’ın bir Azure Sanal Ağına bağlanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-231">Another way to directly access all nodes in the cluster is to install HDInsight into an Azure Virtual Network.</span></span> <span data-ttu-id="bbf71-232">Bundan sonra, uzak makinenizi aynı sanal ağa bağlayabilir ve kümedeki tüm düğümlere doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-232">Then, you can join your remote machine to the same virtual network and directly access all nodes in the cluster.</span></span>
>
> <span data-ttu-id="bbf71-233">Daha fazla bilgi için bkz. [HDInsight ile sanal ağ kullanma](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="bbf71-233">For more information, see [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md).</span></span>

### <a name="configure-ssh-agent-forwarding"></a><span data-ttu-id="bbf71-234">SSH aracı iletmeyi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bbf71-234">Configure SSH agent forwarding</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbf71-235">Aşağıdaki adımlar, Linux veya UNIX tabanlı bir sistem için geçerlidir ve Windows 10 üzerinde Bash ile birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-235">The following steps assume a Linux or UNIX-based system, and work with Bash on Windows 10.</span></span> <span data-ttu-id="bbf71-236">Bu adımlar sisteminizde çalışmazsa SSH istemcinizin belgelerine bakmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-236">If these steps do not work for your system, you may need to consult the documentation for your SSH client.</span></span>

1. <span data-ttu-id="bbf71-237">Bir metin düzenleyicisiyle `~/.ssh/config` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-237">Using a text editor, open `~/.ssh/config`.</span></span> <span data-ttu-id="bbf71-238">Bu dosya yoksa, komut satırında `touch ~/.ssh/config` girerek oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-238">If this file doesn't exist, you can create it by entering `touch ~/.ssh/config` at a command line.</span></span>

2. <span data-ttu-id="bbf71-239">Aşağıdakileri metni `config` dosyasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-239">Add the following text to the `config` file.</span></span>

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    <span data-ttu-id="bbf71-240">__Ana bilgisayar__ bilgisini, SSH kullanarak bağlandığınız düğümün adresiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-240">Replace the __Host__ information with the address of the node you connect to using SSH.</span></span> <span data-ttu-id="bbf71-241">Önceki örnekte kenar düğümü kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-241">The previous example uses the edge node.</span></span> <span data-ttu-id="bbf71-242">Bu giriş, belirtilen düğüm için SSH aracı iletmeyi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="bbf71-242">This entry configures SSH agent forwarding for the specified node.</span></span>

3. <span data-ttu-id="bbf71-243">Terminalde aşağıdaki komutu kullanarak, SSH aracı iletmeyi test edin:</span><span class="sxs-lookup"><span data-stu-id="bbf71-243">Test SSH agent forwarding by using the following command from the terminal:</span></span>

        echo "$SSH_AUTH_SOCK"

    <span data-ttu-id="bbf71-244">Bu komutun aşağıdaki metne benzer bilgiler döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="bbf71-244">This command returns information similar to the following text:</span></span>

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    <span data-ttu-id="bbf71-245">Hiçbir şeyin döndürülmemesi, `ssh-agent` özelliğinin çalışmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-245">If nothing is returned, then `ssh-agent` is not running.</span></span> <span data-ttu-id="bbf71-246">Daha fazla bilgi için [ssh ile ssh-agent kullanma (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) sayfasındaki aracı başlatma komut dosyası bilgilerine bakın veya SSH istemcinizin belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="bbf71-246">For more information, see the agent startup scripts information at [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) or consult your SSH client documentation.</span></span>

4. <span data-ttu-id="bbf71-247">**ssh aracı**nın çalıştığını doğruladıktan sonra, SSH özel anahtarınızı aracıya eklemek için aşağıdakini kullanın:</span><span class="sxs-lookup"><span data-stu-id="bbf71-247">Once you have verified that **ssh-agent** is running, use the following to add your SSH private key to the agent:</span></span>

        ssh-add ~/.ssh/id_rsa

    <span data-ttu-id="bbf71-248">Özel anahtarınızı farklı bir dosyada saklanıyorsa, `~/.ssh/id_rsa` ile dosyanın yolunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="bbf71-248">If your private key is stored in a different file, replace `~/.ssh/id_rsa` with the path to the file.</span></span>

5. <span data-ttu-id="bbf71-249">SSH kullanarak küme kenar düğümüne veya baş düğümlerine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-249">Connect to the cluster edge node or head nodes using SSH.</span></span> <span data-ttu-id="bbf71-250">Ardından, SSH komutunu kullanarak bir çalışan veya zookeeper düğümüne bağlanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-250">Then use the SSH command to connect to a worker or zookeeper node.</span></span> <span data-ttu-id="bbf71-251">İletilen anahtar kullanılarak bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="bbf71-251">The connection is established using the forwarded key.</span></span>

## <a name="copy-files"></a><span data-ttu-id="bbf71-252">Dosyaları kopyalama</span><span class="sxs-lookup"><span data-stu-id="bbf71-252">Copy files</span></span>

<span data-ttu-id="bbf71-253">`scp` yardımcı programı, kümedeki bireysel düğümlerde gelen ve giden dosyaları kopyalamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-253">The `scp` utility can be used to copy files to and from individual nodes in the cluster.</span></span> <span data-ttu-id="bbf71-254">Örneğin, aşağıdaki komut `test.txt` dizinini yerel sistemden birincil baş düğüme kopyalar.</span><span class="sxs-lookup"><span data-stu-id="bbf71-254">For example, the following command copies the `test.txt` directory from the local system to the primary head node:</span></span>

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

<span data-ttu-id="bbf71-255">`:` sonrasında yol sonra belirtilmezse dosya `sshuser` giriş dizinine yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-255">Since no path is specified after the `:`, the file is placed in the `sshuser` home directory.</span></span>

<span data-ttu-id="bbf71-256">Aşağıdaki örnekte birincil baş düğümdeki `sshuser` giriş dizininden `test.txt` dosyası yerel sisteme kopyalanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="bbf71-256">The following example copies the `test.txt` file from the `sshuser` home directory on the primary head node to the local system:</span></span>

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> <span data-ttu-id="bbf71-257">`scp`, yalnızca küme içindeki tek düğümlerin dosya sistemine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="bbf71-257">`scp` can only access the file system of individual nodes within the cluster.</span></span> <span data-ttu-id="bbf71-258">Küme için HDFS uyumlu depolama biriminde bulunan verilere erişmek için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="bbf71-258">It cannot be used to access data in the HDFS-compatible storage for the cluster.</span></span>
>
> <span data-ttu-id="bbf71-259">Bir kaynağı SSH oturumundan kullanmak için karşıya yüklemeniz gerektiğinde `scp` kullanın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-259">Use `scp` when you need to upload a resource for use from an SSH session.</span></span> <span data-ttu-id="bbf71-260">Örneğin, bir Python betiğini karşıya yükleyin ve bir SSH oturumundan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bbf71-260">For example, upload a Python script and then run the script from an SSH session.</span></span>
>
> <span data-ttu-id="bbf71-261">Verileri HDFS uyumlu depolama alanına doğrudan yükleme hakkında daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="bbf71-261">For information on directly loading data into the HDFS-compatible storage, see the following documents:</span></span>
>
> * <span data-ttu-id="bbf71-262">[Azure Depolama kullanarak HDInsight](hdinsight-hadoop-use-blob-storage.md)</span><span class="sxs-lookup"><span data-stu-id="bbf71-262">[HDInsight using Azure Storage](hdinsight-hadoop-use-blob-storage.md).</span></span>
>
> * <span data-ttu-id="bbf71-263">[Azure Data Lake Store kullanarak HDInsight](hdinsight-hadoop-use-data-lake-store.md)</span><span class="sxs-lookup"><span data-stu-id="bbf71-263">[HDInsight using Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbf71-264">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bbf71-264">Next steps</span></span>

* [<span data-ttu-id="bbf71-265">HDInsight ile SSH tüneli kullanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-265">Use SSH tunneling with HDInsight</span></span>](hdinsight-linux-ambari-ssh-tunnel.md)
* [<span data-ttu-id="bbf71-266">HDInsight ile sanal ağ kullanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-266">Use a virtual network with HDInsight</span></span>](hdinsight-extend-hadoop-virtual-network.md)
* [<span data-ttu-id="bbf71-267">HDInsight’ta kenar düğümlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="bbf71-267">Use edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md#access-an-edge-node)