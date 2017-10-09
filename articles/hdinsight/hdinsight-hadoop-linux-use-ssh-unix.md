---
title: "aaaUse Hadoop - Azure Hdınsight ile SSH | Microsoft Docs"
description: "Secure Shell (SSH) kullanarak HDInsight'a erişebilirsiniz. Bu belge, tooHDInsight kullanarak hello ssh ve scp komutları Windows, Linux, Unix ya da macOS istemcilerden bağlanma hakkında bilgi sağlar."
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
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>SSH kullanarak tooHDInsight (Hadoop) bağlanma

Bilgi nasıl toouse [güvenli Kabuk (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely tooHadoop Azure hdınsight'ta bağlanın. 

Hdınsight Linux (Ubuntu) hello Hadoop küme içindeki düğümler hello işletim sistemi olarak kullanabilirsiniz. Merhaba aşağıdaki tabloda bir SSH istemcisi kullanarak tooLinux tabanlı Hdınsight bağlanırken gereken hello adresi ve bağlantı noktası bilgileri içerir:

| Adres | Bağlantı noktası | Bağlandığı yer... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Kenar düğümü (HDInsight üzerinde R Sunucusu) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Kenar düğümü (bir kenar düğümü varsa diğer küme türleri) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Birincil baş düğüm |
| `<clustername>-ssh.azurehdinsight.net` | 23 | İkincil baş düğüm |

> [!NOTE]
> Değiştir `<edgenodename>` hello kenar düğümüne hello adı.
>
> Değiştir `<clustername>` kümenizin hello ada sahip.
>
> Kümeniz bir kenar düğümüne içeriyorsa öneririz, __zaman toohello kenar düğümüne bağlanabilirsiniz__ SSH kullanarak. Merhaba baş düğümler Hadoop kritik toohello durumunu hizmetlerini barındırır. Merhaba kenar düğümüne yalnızca ne üzerinde yerleştirdiğiniz çalışır.
>
> Kenar düğümlerini kullanma hakkında daha fazla bilgi için bkz. [HDInsight’ta kenar düğümlerini kullanma](hdinsight-apps-use-edge-node.md#access-an-edge-node).

## <a name="ssh-clients"></a>SSH istemcileri

Linux ve UNIX macOS sistemleri sağlar hello `ssh` ve `scp` komutları. Merhaba `ssh` yaygın olarak kullanılan toocreate bir Linux veya UNIX tabanlı bir sistemi uzaktan komut satırı oturumla bir istemcidir. Merhaba `scp` istemcidir kullanılan toosecurely kopya dosyalarını, istemci ve hello uzak sistem arasında.

Microsoft Windows, varsayılan olarak SSH istemcisi sağlamaz. Merhaba `ssh` ve `scp` istemcileridir paketleri aşağıdaki hello ile Windows için kullanılabilir:

* [Azure bulut Kabuk](../cloud-shell/quickstart.md): hello bulut Kabuk tarayıcınızda Bash ortamı sağlar ve hello sağlar `ssh`, `scp`ve diğer ortak Linux komutlarını.

* [Windows 10 Ubuntu bash](https://msdn.microsoft.com/commandline/wsl/about): Merhaba `ssh` ve `scp` komutları Windows komut satırında hello Bash üzerinden kullanılabilir.

* [Git (https://git-scm.com/)](https://git-scm.com/): Merhaba `ssh` ve `scp` komutları hello Gitbash'i komut satırı kullanılabilir.

* [GitHub Masaüstü (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` ve `scp` komutları hello GitHub Kabuk komut satırı kullanılabilir. GitHub Masaüstü hello Git Kabuk komut satırı hello olarak yapılandırılmış toouse Bash, hello Windows komut istemi veya PowerShell olabilir.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello PowerShell takım OpenSSH tooWindows taşıma ve test sürümleri sağlar.

    > [!WARNING]
    > Merhaba OpenSSH paketi içerir hello SSH sunucu bileşeni, `sshd`. Bu bileşen SSH sunucusu diğerlerine izin veren sisteminizde başlatır tooconnect tooit. Bu bileşen yapılandırmazsanız veya sisteminizde toohost SSH sunucusu istemediğiniz sürece bağlantı noktası 22'ni açın. Hdınsight ile gerekli toocommunicate değil.

Ayrıca [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) ve [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/) gibi çeşitli grafiksel SSH istemcisi mevcuttur. Bu istemciler kullanılan tooconnect tooHDInsight olabilirler, ancak bağlanma hello hello kullanmaktan farklı işlemidir `ssh` yardımcı programı. Daha fazla bilgi için kullanmakta olduğunuz hello grafik istemcisinin hello belgelerine bakın.

## <a id="sshkey"></a>Kimlik doğrulaması: SSH Anahtarları

SSH anahtarları kullanmak [ortak anahtar şifrelemesini](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH oturumları. SSH anahtarları parolalara göre daha güvenli ve bir kolay bir yolu toosecure erişim tooyour Hadoop kümesi sağlayın.

Bir anahtar kullanarak SSH hesabınızı güvenli, hello istemci bağlandığınızda özel anahtarı eşleşen hello sağlamanız gerekir:

* Çoğu istemciler yapılandırılmış toouse olabilir bir __varsayılan anahtar__. Örneğin, hello `ssh` bir özel anahtar, istemci arar `~/.ssh/id_rsa` Linux ve UNIX ortamlarla.

* Merhaba belirtebilirsiniz __yolu tooa özel anahtarı__. Merhaba ile `ssh` istemcisi, hello `-i` kullanılan toospecify hello yol tooprivate anahtarını bir parametredir. Örneğin, `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Farklı sunucularla kullanılacak __birden fazla özel anahtarınız__ varsa [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) gibi bir yardımcı program kullanmayı deneyin. Merhaba `ssh-agent` yardımcı programı bir SSH oturumu oluşturulurken kullanılan tooautomatically select hello anahtar toouse olabilir.

> [!IMPORTANT]
>
> Özel anahtarınızı bir parola ile güvenli, başlangıç anahtarı kullanırken hello parola girmeniz gerekir. Yardımcı programlar gibi `ssh-agent` hello parola size kolaylık sağlamak için önbelleğe alabilir.

### <a name="create-an-ssh-key-pair"></a>SSH anahtar çifti oluşturma

Kullanım hello `ssh-keygen` toocreate ortak ve özel anahtar dosyaları komutu. Merhaba aşağıdaki komutu Hdınsight ile kullanılabilir 2048 bit RSA anahtar çifti oluşturur:

    ssh-keygen -t rsa -b 2048

Merhaba anahtar oluşturma işlemi sırasında bilgileri istenir. Örneğin, hello anahtarları depolandığı veya toouse bir parola. Merhaba işlemi tamamlandıktan sonra iki dosya oluşturulur; Ortak anahtar ve özel anahtarı.

* Merhaba __ortak anahtar__ kullanılan toocreate Hdınsight kümesi değil. Merhaba ortak anahtara sahip bir uzantısı olarak `.pub`.

* Merhaba __özel anahtarı__ istemci toohello Hdınsight kümenize kullanılan tooauthenticate değil.

> [!IMPORTANT]
> Anahtarlarınızın güvenliğini şifre ile sağlayabilirsiniz. Parola, aslında özel anahtarınız üzerindeki bir şifredir. Birisi özel anahtarınızı edinir olsa bile, bunlar hello parola toouse hello anahtarı olması gerekir.

### <a name="create-hdinsight-using-hello-public-key"></a>Merhaba ortak anahtarı kullanılarak Hdınsight oluşturma

| Oluşturma yöntemi | Nasıl toouse hello ortak anahtar |
| ------- | ------- |
| **Azure portal** | İşaretini __küme oturum açma aynı parolayı kullanın__ve ardından __ortak anahtar__ SSH kimlik doğrulama türü hello gibi. Son olarak, hello ortak anahtar dosyası seçin veya hello hello metin hello dosyasının içeriğini yapıştırın __SSH ortak anahtarını__ alan.</br>![HDInsight küme oluşturma işleminde SSH ortak anahtarı iletişim kutusu](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Kullanım hello `-SshPublicKey` hello parametresinin `New-AzureRmHdinsightCluster` hello ortak anahtarı bir dize olarak cmdlet'i ve geçişi hello içeriğini.|
| **Azure CLI 1.0** | Kullanım hello `--sshPublicKey` hello parametresinin `azure hdinsight cluster create` komut ve hello ortak anahtar Merhaba içeriğine bir dize olarak geçirin. |
| **Resource Manager Şablonu** | SSH anahtarlarını şablonla kullanma örneği için bkz. [HDInsight’ı SSH anahtarı ile Linux’a dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/). Merhaba `publicKeys` hello öğesinde [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) dosyasıdır kullanılan toopass hello anahtarları tooAzure hello kümesi oluştururken. |

## <a id="sshpassword"></a>Kimlik doğrulaması: Parola

SSH hesaplarının güvenliği bir parola kullanılarak sağlanabilir. SSH kullanarak tooHDInsight bağlandığınızda, istendiğinde tooenter hello parola olur.

> [!WARNING]
> SSH için parola kimlik doğrulamasının kullanılması önerilmez. Parolalar, tahmin edilebilir ve güvenlik açığı toobrute zorla saldırılar. Bunun yerine, [kimlik doğrulaması için SSH anahtarları](#sshkey) kullanmanız önerilir.

### <a name="create-hdinsight-using-a-password"></a>Parola kullanarak HDInsight oluşturma

| Oluşturma yöntemi | Nasıl toospecify hello parola |
| --------------- | ---------------- |
| **Azure portal** | Varsayılan olarak, hello hello SSH kullanıcı hesabı sahip hello küme oturum açma hesabı olarak aynı parola. toouse farklı bir parola işaretini __küme oturum açma aynı parolayı kullanın__ve hello parola hello enter __SSH parolası__ alan.</br>![HDInsight küme oluşturma işleminde SSH parolası iletişim kutusu](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Kullanım hello `--SshCredential` hello parametresinin `New-AzureRmHdinsightCluster` cmdlet'i ve geçirin bir `PSCredential` hello SSH kullanıcı hesabı adını ve parolayı içeren nesne. |
| **Azure CLI 1.0** | Kullanım hello `--sshPassword` hello parametresinin `azure hdinsight cluster create` komut ve hello parola değeri sağlayın. |
| **Resource Manager Şablonu** | Parolayı şablonla kullanma örneği için bkz. [HDInsight’ı SSH parolası ile Linux’a dağıtma](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). Merhaba `linuxOperatingSystemProfile` hello öğesinde [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) dosyasıdır adı ve parola kullanılan toopass hello SSH hesabı tooAzure hello kümesi oluştururken.|

### <a name="change-hello-ssh-password"></a>Merhaba SSH Parolayı Değiştir

Merhaba hello SSH kullanıcı hesabının parolasını değiştirme hakkında daha fazla bilgi için bkz __parolaları değiştirme__ hello bölümünü [yönetmek Hdınsight](hdinsight-administer-use-portal-linux.md#change-passwords) belge.

## <a id="domainjoined"></a>Kimlik doğrulama: Etki alanına katılmış HDInsight

Kullanıyorsanız bir __etki alanına katılmış Hdınsight kümesi__, hello kullanmalısınız `kinit` SSH ile bağlandıktan sonra komutu. Bu komutu bir etki alanı kullanıcısı ve parola isteyen ve hello kümesi ile ilişkili hello Azure Active Directory etki alanı ile oturumunuz doğrular.

Daha fazla bilgi için bkz. [Etki alanına katılmış HDInsight yapılandırma](hdinsight-domain-joined-configure.md).

## <a name="connect-toonodes"></a>Toonodes Bağlan

(varsa) baş düğümler ve kenar düğümüne hello hello erişilebilmesi için bağlantı noktası 22 ve 23 Internet'te.

* Toohello bağlanırken __baş düğümler__, bağlantı noktasını kullanacak __22__ tooconnect toohello birincil baş düğüm ve bağlantı noktası __23__ tooconnect toohello ikincil baş düğüm. Merhaba tam etki alanı adı toouse olan `clustername-ssh.azurehdinsight.net`, burada `clustername` hello kümenizin adıdır.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Zaman connectiung toohello __kenar düğümüne__, bağlantı noktası 22 kullanın. Merhaba tam etki alanı adıdır `edgenodename.clustername-ssh.azurehdinsight.net`, burada `edgenodename` ne zaman sağladığınız adı hello kenar düğümüne oluşturuyor. `clustername`Merhaba hello küme adıdır.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> Merhaba önceki örneklerde, parola kimlik doğrulaması kullanıyorsanız veya bu sertifika kimlik doğrulaması otomatik olarak ortaya çıkma varsayılmaktadır. Kimlik doğrulaması için bir SSH anahtar çiftini kullanırsanız ve hello sertifika otomatik olarak kullanılmaz, hello kullan `-i` parametre toospecify hello özel anahtarı. Örneğin, `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Bağlantı kurulduktan sonra hello istemi bağlı tooindicate hello SSH kullanıcı adı ve hello düğümü değiştirir. Örneğin, bağlıyken toohello birincil baş düğümü olarak `sshuser`, hello komut istemi `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Tooworker ve Zookeeper düğümleri Bağlan

çalışan düğümü hello ve Zookeeper düğümleri doğrudan erişilebilir olmayan hello Internet. Bunlar hello küme baş düğüm veya kenar düğümleri erişilebilir. Merhaba, hello genel adımlar tooconnect tooother düğümleri şunlardır:

1. SSH, tooconnect tooa head veya edge düğümünü kullanın:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Merhaba SSH bağlantı toohello head veya kenar düğümünü, hello kullan `ssh` komutu tooconnect tooa çalışan hello küme düğümünde:

        ssh sshuser@wn0-myhdi

    tooretrieve hello kümedeki hello düğümlerinin hello etki alanı adlarının bir listesini görmek hello [Ambari REST API kullanarak Hdınsight yönetmek hello](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) belge.

Merhaba SSH hesabı kullanarak güvenli bir __parola__, bağlanırken hello parolayı girin.

Merhaba SSH hesabı kullanarak sağlanmışsa __SSH anahtarları__, SSH iletme hello istemcide etkin olduğundan emin olun.

> [!NOTE]
> Toodirectly erişim hello kümedeki tüm düğümlerin başka bir Azure sanal ağı Hdınsight'a tooinstall yoludur. Ardından, uzak makine toohello katılabilirsiniz aynı sanal ağ ve hello kümedeki tüm düğümlere doğrudan erişebilirsiniz.
>
> Daha fazla bilgi için bkz. [HDInsight ile sanal ağ kullanma](hdinsight-extend-hadoop-virtual-network.md).

### <a name="configure-ssh-agent-forwarding"></a>SSH aracı iletmeyi yapılandırma

> [!IMPORTANT]
> Hello aşağıdaki adımları bir Linux veya UNIX tabanlı sistemi ve Windows 10 Bash ile çalışır. Bu adımlar, sisteminiz için işe yaramazsa, tooconsult hello belgeleri için SSH istemcinizi gerekebilir.

1. Bir metin düzenleyicisiyle `~/.ssh/config` dosyasını açın. Bu dosya yoksa, komut satırında `touch ~/.ssh/config` girerek oluşturabilirsiniz.

2. Metin toohello aşağıdaki hello eklemek `config` dosya.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Hello yerine __ana bilgisayar__ bilgi hello düğümü hello adresiyle toousing SSH bağlanın. Merhaba önceki örnek hello kenar düğümünü kullanır. Bu giriş, SSH aracı iletmeyi hello belirtilen düğümü için yapılandırır.

3. SSH aracı iletmeyi hello terminal komutu aşağıdaki hello kullanarak test edin:

        echo "$SSH_AUTH_SOCK"

    Bu komut, metin aşağıdaki bilgileri benzer toohello döndürür:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Hiçbir şeyin döndürülmemesi, `ssh-agent` özelliğinin çalışmadığını gösterir. Daha fazla bilgi için hello Aracısı başlatma komut dosyaları bilgilerine bakın [ssh ile ssh-aracı kullanma (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) veya SSH istemcisi belgelerinize başvurun.

4. Doğruladıktan sonra **ssh aracı** , tooadd aşağıdaki kullanım hello SSH özel anahtar toohello aracınızı çalışıyor:

        ssh-add ~/.ssh/id_rsa

    Özel anahtarınızı farklı bir dosyada saklanıyorsa, yerini `~/.ssh/id_rsa` hello yol toohello dosya ile.

5. Toohello küme kenar düğümüne veya baş düğümler SSH kullanarak bağlanın. Ardından hello SSH komutu tooconnect tooa çalışan veya zookeeper düğümünü kullanın. iletilen hello anahtarı kullanarak Hello bağlantı kurulur.

## <a name="copy-files"></a>Dosyaları kopyalama

Merhaba `scp` yardımcı programı, kullanılan toocopy dosyaları tooand tek tek düğümden hello küme de olabilir. Örneğin, komut kopyaları hello aşağıdaki hello `test.txt` hello yerel sistem toohello birincil baş düğümünden dizin:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Yol sonra hello belirtilmezse bu yana `:`, hello dosya hello yerleştirilir `sshuser` giriş dizini.

Örnek kopyaları hello Hello `test.txt` hello dosyasından `sshuser` hello birincil baş düğüm toohello yerel sistemde giriş dizini:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`yalnızca bireysel düğümleri hello kümedeki hello dosya sistemine erişebilir. Merhaba HDFS uyumlu depolama hello küme için kullanılan tooaccess verilerde olamaz.
>
> Kullanmak `scp` bir SSH oturumundan kullanmak için bir kaynak tooupload gerektiğinde. Örneğin, bir Python komut dosyasını karşıya yükleyin ve ardından bir SSH oturumunda hello betiği çalıştırın.
>
> Verileri HDFS uyumlu depolama hello doğrudan yükleme hakkında daha fazla bilgi için belgeleri aşağıdaki hello bakın:
>
> * [Azure Depolama kullanarak HDInsight](hdinsight-hadoop-use-blob-storage.md)
>
> * [Azure Data Lake Store kullanarak HDInsight](hdinsight-hadoop-use-data-lake-store.md)

## <a name="next-steps"></a>Sonraki adımlar

* [HDInsight ile SSH tüneli kullanma](hdinsight-linux-ambari-ssh-tunnel.md)
* [HDInsight ile sanal ağ kullanma](hdinsight-extend-hadoop-virtual-network.md)
* [HDInsight’ta kenar düğümlerini kullanma](hdinsight-apps-use-edge-node.md#access-an-edge-node)