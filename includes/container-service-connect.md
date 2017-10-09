# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>Bir uzak bağlantı tooa Kubernetes, DC/OS veya Docker Swarm kümesi olun
Azure kapsayıcı hizmeti kümesi oluşturduktan sonra tooconnect toohello küme toodeploy gerekir ve iş yükleri yönetin. Bu makalede nasıl tooconnect toohello ana hello VM küme uzak bir bilgisayardan açıklanmaktadır. 

Merhaba Kubernetes, DC/OS ve Docker Swarm kümeleri yerel olarak HTTP uç noktaları sağlar. Kubernetes için bu uç noktası güvenli bir şekilde üzerinde sunulan Internet hello ve hello çalıştırarak erişebilirsiniz `kubectl` internet'e bağlı herhangi makineden komut satırı aracı. 

DC/OS ve Docker Swarm için yerel bilgisayar toohello küme yönetim sisteminden bir güvenli Kabuk (SSH) tüneli oluşturmanızı öneririz. Merhaba tünel kurulduktan sonra hello HTTP uç noktaları ve görünüm hello orchestrator'ın web Arabirimi'ni (varsa) Yerel sisteminizden kullanacağınız komutları çalıştırabilirsiniz. 

## <a name="prerequisites"></a>Ön koşullar

* Bir Kubernetes, DC/OS veya Docker Swarm kümesi [Azure Container Service’e dağıtılır](../articles/container-service/dcos-swarm/container-service-deployment.md).
* Toohello ortak anahtar eklenen toohello Küme dağıtımı sırasında karşılık gelen SSH RSA özel anahtar dosyası. Bu komutlarda hello özel SSH anahtarı olan varsayılmaktadır `$HOME/.ssh/id_rsa` bilgisayarınızda. Daha fazla bilgi için [macOS ve Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) veya [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) ile ilgili şu yönergelere bakın. Merhaba SSH bağlantısı çalışmıyorsa, çok gerekebilir [SSH anahtarlarını sıfırlama](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).

## <a name="connect-tooa-kubernetes-cluster"></a>Tooa Kubernetes kümesine bağlanın

Bu adımları tooinstall izleyin ve yapılandırma `kubectl` bilgisayarınızda.

> [!NOTE] 
> Linux veya macOS, bu bölümde kullanarak toorun hello komutları gerekebilir `sudo`.
> 

### <a name="install-kubectl"></a>Kubectl yükleyin
Tek yönlü tooinstall toouse hello bu araçtır `az acs kubernetes install-cli` Azure CLI 2.0 komutu. Bu komut, emin olun toorun, [yüklü](/cli/azure/install-az-cli2) en son Azure CLI 2.0 hello ve tooan Azure hesabı günlüğe (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

Alternatif olarak, hello son indirebilirsiniz `kubectl` hello doğrudan istemciden [Kubernetes serbest sayfa](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md). Daha fazla bilgi için bkz. [kubectl yükleme ve ayarlama](https://kubernetes.io/docs/tasks/kubectl/install/).

### <a name="download-cluster-credentials"></a>Küme kimlik bilgilerini indirme
Bulduktan sonra `kubectl` yüklü toocopy hello küme kimlik bilgilerini tooyour makine gerekir. Tek yönlü toodo get hello kimlik bilgileri olan ile Merhaba `az acs kubernetes get-credentials` komutu. Merhaba hello kaynak grubunun adını ve hello kapsayıcı hizmeti kaynak hello adını geçirin:

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

Bu komut çok hello küme kimlik bilgileri indirmeleri`$HOME/.kube/config`, burada `kubectl` bulunan toobe bekliyor.

Alternatif olarak, kullanabileceğiniz `scp` hello dosya Kopyala toosecurely `$HOME/.kube/config` hello ana VM tooyour yerel makine üzerinde. Örneğin:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Windows üzerinde varsa, Bash Ubuntu Windows, hello PuTTy güvenli dosya kopya istemcisi veya benzer bir aracı kullanabilirsiniz.

### <a name="use-kubectl"></a>Kubectl kullanma

Bulduktan sonra `kubectl` yapılandırılmış, kümenizdeki düğümlerin hello listeleyerek hello bağlantıyı sınayın:

```bash
kubectl get nodes
```

Diğer `kubectl` komutlarını deneyebilirsiniz. Örneğin, hello Kubernetes Pano görüntüleyebilirsiniz. İlk olarak, bir proxy toohello Kubernetes API sunucunuz çalıştırın:

```bash
kubectl proxy
```

Merhaba Kubernetes UI artık şu adresten edinilebilir: `http://localhost:8001/ui`.

Daha fazla bilgi için bkz: Merhaba [Kubernetes Hızlı Başlangıç](http://kubernetes.io/docs/user-guide/quick-start/).

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Tooa DC/OS ya da Swarm kümesine bağlanın

toouse hello DC/OS ve Docker Swarm kümeleri Azure kapsayıcı hizmeti tarafından dağıtılan yerel Linux, macOS ya da Windows sisteminizi bu yönergeler toocreate bir SSH tüneli izleyin. 

> [!NOTE]
> Bu yönergeler, SSH üzerinden TCP trafiğini tünellemeye odaklanır. Aynı zamanda etkileşimli bir SSH oturumu hello iç küme yönetimi sistemlerinden birini başlatabilirsiniz, ancak bu önerilmemektedir. Bir iç sistem üzerinde doğrudan çalışma, yanlışlıkla yapılandırma değişikliği yapma riskini içerir.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Linux veya macOS’ta SSH tüneli oluşturma
Linux veya macOS üzerinde SSH tüneli oluşturduğunuzda, bunu hello ilk şey toolocate hello ortak DNS hello yük dengeli asıl adıdır. Şu adımları uygulayın:


1. Merhaba, [Azure portal](https://portal.azure.com), kapsayıcı hizmeti kümesini içeren toohello kaynak grubunu bulun. Böylece her bir kaynağın görüntülenen hello kaynak grubunu genişletin. 

2. Merhaba tıklatın **kapsayıcı hizmeti** kaynak'ı tıklayın ve **genel bakış**. Merhaba **ana FQDN** Merhaba küme altında görüntülenir. **Essentials**. Bu adı daha sonra kullanmak için kaydedin. 

    ![Genel DNS adı](./media/container-service-connect/pubdns.png)

    Alternatif olarak, Başlangıç'ı çalıştırmak `az acs show` kapsayıcı hizmeti komutu. Merhaba Ara **ana profil: fqdn** hello komut çıktısı bir özellik.

3. Şimdi bir Kabuğu'nu açın ve hello çalıştırın `ssh` değerleri aşağıdaki hello belirterek komutu: 

    **LOCAL_PORT** hello tünel tooconnect hello hizmet tarafındaki hello TCP bağlantı noktasıdır. Swarm için bu too2375 ayarlayın. DC/OS için bu too80 ayarlayın. 
    **REMOTE_PORT** tooexpose istediğiniz hello endpoint hello bağlantı noktasıdır. Swarm için 2375 bağlantı noktasını kullanın. DC/OS için, 80 numaralı bağlantı noktasını kullanın.  
    **Kullanıcı adı** hello kümeyi dağıttığınızda sağlanan hello kullanıcı adıdır.  
    **DNSPREFIX** hello kümeyi dağıttığınızda sağladığınız hello DNS önekidir.  
    **Bölge** kaynak grubunuzun bulunduğu hello bölgedir.  
    **Path_to_prıvate_key** [isteğe bağlı] olan hello küme oluştururken sağladığınız ortak anahtar toohello karşılık gelen hello yolu toohello özel anahtarı. Bu seçeneği ile Merhaba kullanın `-i` bayrağı.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > Merhaba SSH bağlantı noktası 2200'dür ve standart bağlantı noktası 22'hello değil. Birden fazla ana VM ile bir kümede bu hello bağlantı bağlantı noktası toohello ilk VM yöneticisidir.
  > 

  Merhaba komut çıktısı döndürür.

Merhaba örneklere bölümleri aşağıdaki hello DC/OS ve Swarm için bakın.    

### <a name="dcos-tunnel"></a>DC/OS tüneli
DC/OS uç noktaları için bir tünel tooopen hello aşağıdaki gibi bir komutu çalıştırın:

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> 80 numaralı bağlantı noktasına bağlanan başka bir yerel işleminizin olmadığından emin olun. Gerekirse, 8080 bağlantı noktası gibi 80 bağlantı noktasından farklı bir yerel bağlantı noktası belirtebilirsiniz. Ancak, bu bağlantı noktasını kullandığınızda bazı web kullanıcı arabirimi bağlantıları çalışmayabilir.
>

Aşağıdaki URL'lere (yerel bağlantı noktası 80 varsayılarak) hello aracılığıyla Yerel sisteminizden hello DC/OS uç noktaları artık erişebilirsiniz:

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

Benzer şekilde, bu Tünel üzerinden her uygulama için hello rest API'lerine ulaşabilirsiniz.

### <a name="swarm-tunnel"></a>Swarm tüneli
tooopen tünel toohello Swarm uç hello aşağıdaki gibi bir komutu çalıştırın:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> 2375 numaralı bağlantı noktasına bağlanan başka bir yerel işleminizin olmadığından emin olun. Örneğin, hello Docker arka plan programı yerel olarak çalıştırıyorsanız, varsayılan toouse bağlantı 2375 ayarlanır. Gerekirse, 2375 bağlantı noktasından farklı bir yerel bağlantı noktası belirtebilirsiniz.
>

Artık hello Docker Swarm kümesi yerel sisteminizde hello Docker komut satırı arabirimi (Docker CLI) kullanarak erişebilirsiniz. Yükleme yönergeleri için bkz. [Docker Yükleme](https://docs.docker.com/engine/installation/).

DOCKER_HOST ortam değişkeni toohello hello tünel için yapılandırılmış yerel bağlantı noktası ayarlayın. 

```bash
export DOCKER_HOST=:2375
```

Bu tünel toohello Docker Swarm kümesi Docker komutları çalıştırın. Örneğin:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Windows’da SSH tüneli oluşturma
Windows’da SSH tünelleri oluşturmak için birden çok seçenek vardır. Windows veya benzer bir aracı üzerinde Ubuntu Bash çalıştırıyorsanız, bu makalenin macOS ve Linux için gösterilen hello SSH tünel oluşturma yönergeleri izleyebilir. Windows alternatif olarak, bu bölümde açıklanmıştır nasıl toouse PuTTY toocreate hello tünel.

1. [PuTTY karşıdan](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows sistemi.

2. Merhaba uygulamayı çalıştırın.

3. Merhaba Küme Yöneticisi kullanıcı adı ve hello kümedeki ilk ana hello hello Genel DNS adından oluşan bir ana bilgisayar adı girin. Merhaba **ana bilgisayar adı** çok benzer`azureuser@PublicDNSName`. Merhaba 2200 girin **bağlantı noktası**.

    ![PuTTY yapılandırması 1](./media/container-service-connect/putty1.png)

4. **SSH > Yetkilendirme** öğesini seçin. Bir yol tooyour özel anahtar dosyası (.ppk biçimi) kimlik doğrulaması için ekleyin. Bir aracı gibi kullanabilir [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) bu dosya toogenerate hello SSH anahtar kullanılan toocreate hello küme.

    ![PuTTY yapılandırması 2](./media/container-service-connect/putty2.png)

5. Seçin **SSH > tüneller** ve iletilen bağlantı noktalarını hello aşağıdakileri yapılandırın:

    * **Kaynak Bağlantı Noktası:** DC/OS için 80 veya Swarm için 2375 kullanın.
    * **Hedef:** DC/OS için localhost:80 veya Swarm için 2375 kullanın.

    Aşağıdaki örneğine hello DC/OS için yapılandırılmıştır, ancak Docker Swarm için olan benzer olacaktır.

    > [!NOTE]
    > Bu tüneli oluştururken bağlantı noktası 80 kullanımda olmamalıdır.
    > 

    ![PuTTY yapılandırması 3](./media/container-service-connect/putty3.png)

6. İşiniz bittiğinde tıklatın **oturum > Kaydet** toosave hello bağlantı yapılandırması.

7. tooconnect toohello PuTTY oturumu,'ı tıklatın **açık**. Bağlandığınızda, başlangıç bağlantı noktası yapılandırmasını hello PuTTY olay günlüğünde görebilirsiniz.

    ![PuTTY olay günlüğü](./media/container-service-connect/putty4.png)

DC/OS için hello tünel yapılandırdıktan sonra erişebilirsiniz hello ilgili Uç noktalara:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Docker Swarm için hello tünel yapılandırdıktan sonra Windows ayarlarını tooconfigure adlı bir sistem ortam değişkeni açmak `DOCKER_HOST` değerini `:2375`. Daha sonra Docker CLI hello hello Swarm kümesine erişebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Kümenizde kapsayıcıları dağıtma ve yönetme:

* [Azure Container Service ve Kubernetes ile çalışma](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Azure Container Service ve DC/OS ile çalışma](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Hello Azure kapsayıcı hizmeti ve Docker Swarm ile çalışma](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

