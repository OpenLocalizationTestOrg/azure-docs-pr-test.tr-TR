# <a name="container-service-frequently-asked-questions"></a>Kapsayıcı Hizmeti sık sorulan sorular

## <a name="orchestrators"></a>Düzenleyiciler

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Azure Container Service’te hangi kapsayıcı düzenleyicileri desteklenir? 

Açık kaynak DC/OS, Docker Swarm ve Kubernetes desteği mevcuttur. Daha fazla bilgi için bkz: Merhaba [genel bakış](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
 
### <a name="do-you-support-docker-swarm-mode"></a>Docker Swarm modu destekleniyor mu? 

Şu anda Swarm modu desteklenmiyor ancak hello hizmet Haritası üzerinde değil. 

### <a name="does-azure-container-service-support-windows-containers"></a>Azure Container Service, Windows kapsayıcılarını destekliyor mu?  

Şu anda Linux kapsayıcıları tüm düzenleyicilerle desteklenmektedir. Kubernetes ile Windows kapsayıcıları desteği önizleme aşamasındadır.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Azure Container Service için önerilen belirli bir düzenleyici var mı? 
Genellikle belirli bir düzenleyici önerilmemektedir. Desteklenen hello orchestrators biriyle deneyimi varsa, Azure kapsayıcı hizmeti bu deneyimi uygulayabilirsiniz. Ancak, veri eğilimleri DC/OS’nin Büyük Veri ve IoT iş yükleri için üretimde kanıtlandığını, Kubernetes’in bulut yerel iş yükleri için uygun olduğunu, Docker Swarm’ın ise Docker araçları ve kolay öğrenme eğrisi konusunda ünlü olduğunu ortaya koymaktadır.

Senaryonuza bağlı olarak, diğer Azure hizmetleriyle de özel kapsayıcı çözümleri oluşturup yönetebilirsiniz. Bu hizmetler [Sanal Makine](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) ve [Batch](../articles/batch/batch-technical-overview.md) hizmetleridir.  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Hello Azure kapsayıcı hizmeti ve ACS altyapısı arasındaki fark nedir? 
Azure kapsayıcı hizmeti bir SLA destekli Azure hello Azure portal, Azure komut satırı araçları ve Azure API'lerini özelliklerle hizmetidir. Merhaba, tooquickly uygulamak ve görece küçük bir yapılandırma seçeneklerinin sayıya standart kapsayıcı düzenleme araçları çalıştıran kümeler yönetmek hizmet sağlar. 

[ACS altyapısı](http://github.com/Azure/acs-engine) güç kullanıcılar toocustomize hello küme yapılandırması her düzeyde sağlayan bir açık kaynak projesidir. Bu özelliği tooalter hello yapılandırma altyapısı ve yazılım hiçbir SLA ACS altyapısı için sunuyoruz olduğunu anlamına gelir. Destek, github'da açık kaynaklı proje hello yerine resmi Microsoft kanallar aracılığıyla gerçekleştirilir. 

## <a name="cluster-management"></a>Küme yönetimi

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>Kümem için nasıl SSH anahtarları oluşturabilirim?

Standart Araçlar, işletim sistemi toocreate bir SSH RSA ortak ve özel anahtar çifti hello Linux sanal makinelere karşı kimlik doğrulaması için kümeniz için kullanabilirsiniz. Merhaba adımları için bkz [OS X ve Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) veya [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) Kılavuzu. 

Kullanırsanız [Azure CLI 2.0 komutları](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy bir kapsayıcı hizmeti kümesi, SSH anahtarları otomatik olarak kümeniz için oluşturulabilir.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Kubernetes kümem için nasıl hizmet sorumlusu oluşturabilirim?

Ayrıca bir Azure Active Directory hizmet asıl kimliği ve parola gerekli toocreate Azure kapsayıcı hizmeti Kubernetes kümede değildir. Daha fazla bilgi için bkz: [hello hizmet sorumlusu Kubernetes kümesi için hakkında](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md).

Kullanırsanız [Azure CLI 2.0 komutları](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy bir Kubernetes küme, hizmet asıl kimlik bilgileri, kümeniz için otomatik olarak da oluşturulabilir.

### <a name="how-large-a-cluster-can-i-create"></a>Ne kadar büyük bir küme oluşturabilirim?
1, 3 veya 5 ana düğüm içeren bir küme oluşturabilirsiniz. Too100 aracı düğümlerini seçebilirsiniz.

> [!IMPORTANT]
> Daha büyük kümeleri için ve hello düğümleri için seçtiğiniz VM boyutu bağlı olarak, aboneliğinizde tooincrease hello çekirdek kota gerekebilir. toorequest kota artışı, açık bir [çevrimiçi müşteri destek isteği](../articles/azure-supportability/how-to-create-azure-support-request.md) herhangi bir ücret alınmaz. [Ücretsiz Azure hesabı](https://azure.microsoft.com/free/) kullanıyorsanız, yalnızca sınırlı sayıda Azure işlem çekirdeği kullanabilirsiniz.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>Bir küme oluşturulduktan sonra nasıl yöneticileri hello sayısını artırmak? 
Merhaba Küme oluşturulduktan sonra ana sunucu sayısı hello sabittir ve değiştirilemez. Merhaba küme Hello oluşturma sırasında yüksek kullanılabilirlik için birden çok asıl ideal olarak seçmeniz gerekir.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>Bir küme oluşturulduktan sonra nasıl aracılarının hello sayısını artırmak? 
Hello Azure portal veya komut satırı araçlarını kullanarak hello kümede aracı hello sayısı ölçeklendirebilirsiniz. Bkz. [Azure Container Service kümesini ölçeklendirme](../articles/container-service/kubernetes/container-service-scale.md).

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>Merhaba URL'leri yöneticileri ve aracıları nelerdir? 
Azure kapsayıcı hizmeti kaynaklarında üzerinde hello dayalı küme Hello URL'lerini sağlayın ve hello dağıtım için seçtiğiniz Azure bölgesinde adını hello önek DNS adı. Örneğin, hello tam etki alanı adıdır (FQDN) hello ana düğümünün bu biçimi:

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Kümenizde hello Azure portal, Azure kaynak Gezgini hello veya diğer Azure Araçları için yaygın olarak kullanılan URL'leri bulabilirsiniz.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>Kümemde hangi orchestrator sürümünün çalıştığını nasıl öğrenirim?

* DC/OS: Hello bkz [Mesosphere belgelerine](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: `docker version` çalıştırın
* Kubernetes: `kubectl version` çalıştırın

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>Dağıtımdan sonra nasıl hello orchestrator yükseltme?

Şu anda, Azure kapsayıcı hizmeti araçları tooupgrade hello kümenizde dağıtılan hello orchestrator sürümünü sağlamaz. Kapsayıcı Hizmeti sonraki bir sürümü destekliyorsa, yeni bir küme dağıtabilirsiniz. Kullanılabilir tooupgrade bir kümeyi yerinde olmaları durumunda toouse orchestrator özel araçlar ise başka bir seçenektir. Örneğin, bkz. [DC/OS Yükseltme](https://dcos.io/docs/1.8/administration/upgrading/).
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Merhaba SSH bağlantı dizesi toomy küme nereden bulabilirim?

Merhaba bağlantı dizesi hello Azure portalında veya Azure komut satırı araçlarını kullanarak bulabilirsiniz. 

1. Merhaba Portalı'nda toohello kaynak grubu hello Küme dağıtımı için gidin.  

2. Tıklatın **genel bakış** ve hello bağlantısını tıklatın **dağıtımları** altında **Essentials**. 

3. Merhaba, **dağıtım geçmişi** dikey penceresinde ile başlayan bir ada sahip hello dağıtım tıklatın **microsoft acs** Dağıtım tarihi tarafından izlenen. Örnek: microsoft-acs-201701310000.  

4. Merhaba üzerinde **Özet** sayfasında **çıkışları**, birkaç küme bağlantılar verilmiştir. **SSHMaster0** bir SSH bağlantı dizesi toohello ilk ana kapsayıcı hizmeti kümesi sağlar. 

Daha önce belirtildiği gibi ayrıca Azure Araçları toofind hello hello ana FQDN'sini kullanabilirsiniz. Bir SSH bağlantısı hello hello ana ve hello kullanıcı adı hello küme oluştururken, belirtilen FQDN kullanarak toohello asıl olun. Örneğin:

```bash
ssh userName@masterFQDN –A –p 22 
```

Daha fazla bilgi için bkz: [Bağlan tooan Azure kapsayıcı hizmeti kümesi](../articles/container-service/kubernetes/container-service-connect.md).

## <a name="next-steps"></a>Sonraki adımlar

* Azure Container Service hakkında [daha fazla bilgi edinin](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
* Hello kullanarak bir kapsayıcı hizmeti kümesini dağıtma [portal](../articles/container-service/dcos-swarm/container-service-deployment.md) veya [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md).
