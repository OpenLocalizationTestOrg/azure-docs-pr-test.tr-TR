# <a name="securing-docker-containers-in-azure-container-service"></a>Azure Container Service’de Docker kapsayıcılarının güvenliğini sağlama

Bu makalede, Azure Container Service'de dağıtılan Docker kapsayıcılarının güvenliğini sağlamak için önemli bilgiler ve öneriler yer almaktadır. Bu noktalar çoğunu genellikle, Azure veya diğer ortamlara dağıtılmış tooDocker kapsayıcıları de geçerlidir. 

## <a name="image-security"></a>Görüntü güvenliği

Kapsayıcı, bir veya daha fazla depoda depolanan görüntülerden oluşturulur. Bu depoları toopublic veya özel kapsayıcı kayıt defterleri ait olabilir. [Docker Hub](https://hub.docker.com/) genel bir kayıt defteri örneğidir. Özel bir kayıt defteri hello örneğidir [Docker güvenilen kayıt defteri](https://docs.docker.com/datacenter/dtr/2.0/), şirket içi yüklü olabilen veya bir sanal özel bulutta. Ayrıca [Azure Container Registry](../articles/container-registry/container-registry-intro.md) gibi özel kapsayıcı bulut tabanlı kayıt defteri hizmetleri de vardır.

### <a name="public-and-private-images"></a>Genel ve özel görüntüler
Temelde, tüm genel olarak yayımlanan yazılım paketlerinde olduğu gibi genel kullanıma açık kapsayıcı görüntülerinde de güvenlik garanti edilemez. Her yazılım katmanında güvenlik açıkları olabilir ve kapsayıcı görüntüleri birden çok yazılım katmanından oluşur. Anahtar toounderstand hello kaynak hello kapsayıcı görüntüsünün olduğunda, oluşur yazılım katmanları dahil olmak üzere hello sahibi hello görüntüsünün (güvenilir bir kaynak veya yok olması durumunda toodetermine) hello ve yazılım sürümlerini hello. 

Toohello resmi giderseniz, örneğin, [nginx deposu](https://hub.docker.com/_/nginx/) Docker hub ve toohello gidin **etiketleri** sekmesinde, her görüntü ren kodlu güvenlik açıkları bakın. Her renk hello güvenlik açığı hello görüntüsünün yazılım katmanın gösterilmektedir. Docker Hub tarama güvenlik açığı hakkında daha fazla bilgi için bkz. [Docker Hub'daki resmi depoları anlama](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/).

![Docker Hub'daki Nginx görüntüleri](./media/container-service-security/docker-hub-nginx.png)

Kuruluşlar için son derece önemli güvenlik ve tooprotect hakkında kendilerini güvenlik saldırılara karşı depolamak ve görüntüleri Azure kapsayıcı kayıt defteri veya Docker güvenilen kayıt gibi özel bir kayıt defteri almak. Azure kapsayıcı kayıt defteri toplama tooproviding yönetilen özel kayıt defteri, destekler [hizmet asıl tabanlı kimlik doğrulaması](../articles/container-registry/container-registry-authentication.md) rol tabanlı erişim için de dahil olmak üzere, temel kimlik doğrulaması akışlar için Azure Active Directory üzerinden salt okunur, yazma ve sahibi izinleri.

### <a name="image-security-scanning"></a>Görüntü güvenliği tarama

Özel bir kayıt defteri kullanırken bile, ek güvenlik doğrulama çözümleri tarama bir fikir toouse görüntüsü olduğundan. Her yazılım kapsayıcı görüntüsündeki olası yatkın toovulnerabilities bağımsız olarak diğer katmanları hello kapsayıcı görüntüsündeki katmanıdır. Kapsayıcı teknolojilerini temel, üretim iş yüklerini dağıtma şirketler giderek başlangıç olarak görüntü tarama kuruluşlarına güvenlik tehditlerinden önemli tooensure önleme haline gelir. 

İzleme ve çözümleri gibi tarama güvenlik [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) ve [açık mavi güvenlik](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), diğerleriyle birlikte, özel bir kayıt defteri kapsayıcı görüntülerde kullanılan tooscan olması ve olası güvenlik açıklarını belirleme. Bu hello farklı çözümler tarama toounderstand hello derinliği sağlamak önemlidir. Örneğin, bazı çözümleri görüntü katmanlarını yalnızca bilinen güvenlik açıklarına karşı doğrulayabilir. Bu çözümlerin belirli bir paket Yöneticisi yazılımı yerleşik mümkün tooverify görüntü katmanına yazılım olmayabilir. Diğer çözümler daha ayrıntılı tarama tümleştirmesine sahiptir ve tüm paketlenmiş yazılımlarda güvenlik açıkları bulabilir.

### <a name="production-deployment-rules-and-audit"></a>Üretim dağıtım kuralları ve denetim
Bir uygulama üretimde dağıtıldığında, üretim ortamlarında görüntüleri kullanılan birkaç kuralları tooensure güvenli ve hiçbir güvenlik açıkları içeren temel tooset var.

* Bir kural olarak, güvenlik açıkları, hatta küçük görüntülerle toorun bir üretim ortamında izin verilmemelidir. Ayrıca, üretimde dağıtılan tüm görüntüleri ideal bir özel kayıt defteri erişilebilir tooa Seç az kaydedilmesi gerekir. Bu da önemli tookeep hello üretim görüntüleri küçük tooensure bunlar etkili bir şekilde yönetilebilir sayısıdır.

* Genel kullanıma açık kapsayıcı görüntüden yazılımların sabit toopinpoint hello kaynak olduğundan, kaynak tooensure bilgi hello kaynak hello katmanının iyi bir uygulama toobuild görüntülerden var. Bir güvenlik açığı yüzeyleri olduğunda otomatik olarak oluşturulan kapsayıcı görüntü müşterileri daha hızlı bir yolu tooa çözüm bulabilirsiniz. Bir ortak görüntüsüyle müşteriler toofind hello ortak görüntü toofix kökündeki gerekir bu veya başka bir güvenli resim hello yayımcıdan elde etmek.

* Üretimde dağıtılan baştan sona taranmış bir görüntüsünü toobe toodate yukarı Merhaba uygulaması hello ömrü boyunca garanti edilmez. Güvenlik açıklarını önceden bilinmeyen veya hello üretim dağıtımdan sonra sunulan Katmanlar hello görüntüsünün için bildirilebilir. Üretimde dağıtılan görüntülerin düzenli denetim güncel veya bir süre güncelleştirilmediği gerekli tooidentify resimleri boyutudur. Bir mavi yeşil dağıtım yöntemleri ve yükseltme mekanizmalarına tooupdate kapsayıcı görüntüleri kapalı kalma süresi olmadan çalışırken kullanabilirsiniz. Görüntü tarama hello önceki bölümde açıklanan araçları ile yapılabilir. 

* Sürekli Tümleştirme (CI) ardışık düzen toobuild görüntüleri ve tümleşik güvenlik tarama yardımcı güvenli kapsayıcı görüntülerle güvenli özel kayıt defterleri korumak. Merhaba hello CI çözüme yerleşik güvenlik açığı taraması tüm hello sınamaları geçmesi görüntüleri hangi üretimden iş yükleri dağıtılan toohello özel kayıt defteri gönderilen sağlar. CI ardışık düzen hatası savunmasız görüntüleri üretim iş yükü dağıtımları için kullanılan hello özel kayıt defterine gönderilen değil sağlar. Ayrıca, çok sayıda görüntü varsa görüntü güvenliği taramasını otomatikleştirir. Aksi durumda, görüntüleri güvenlik açıkları için el ile denetlemek çok zor olabileceği gibi hata riskini de artırır.

## <a name="host-level-container-isolation"></a>Konak düzeyinde kapsayıcı yalıtımı
Bir müşteri Azure kaynaklarına kapsayıcı uygulamaları dağıttığında, bu uygulamalar kaynak gruplarında abonelik düzeyinde dağıtılır ve çok kiracılı değildir. Bu bir müşteri başkalarıyla bir abonelik paylaşıyorsa olduğunu hello iki dağıtımlarda arasında aynı oluşturulabilir hiçbir sınırları anlamına gelir Abonelik. Bu nedenle, kapsayıcı düzeyi güvenliği garanti edilemez. 

Ayrıca, kritik toounderstand kapsayıcıları hello çekirdek ve (Azure kapsayıcı Hizmeti'nde bir kümedeki bir Azure VM olan) hello ana hello kaynakları paylaşmak unutulmamalıdır. Bu nedenle, üretimde çalışan kapsayıcılar ayrıcalıklı olmayan kullanıcı modunda çalıştırılmalıdır. Kök ayrıcalıkları olan bir kapsayıcı çalıştıran hello tüm ortamın tehlikeye atabilir. Bir kapsayıcıda kök düzeyinde erişime bir bilgisayar korsanının toohello tam kök ayrıcalıkları hello konaktaki erişebilir. Buna ek olarak, salt okunur dosya sistemleri ile önemli toorun kapsayıcıları olur. Bu dosya sistemi ve tooother dosyalara erişim erişim tehlikeye toohello kapsayıcı toowrite kötü amaçlı komut dosyalarını toohello sahip olan kişi önler. Benzer şekilde, bu tooa kapsayıcı ayrılan önemli toolimit hello kaynaklar (örneğin, bellek, CPU ve ağ bant genişliği) olur. Bu kaynaklar işgal etmesini ve kredi kartı sahtekarlık veya diğer kapsayıcıları hello konağı veya kümesi üzerinde çalışmasını önleyebilir bitcoin araştırma gibi yasadışı etkinlikler sürdürdüğünü bilgisayar korsanlarının önlemeye yardımcı olur.

## <a name="orchestrator-considerations"></a>Düzenleyicide dikkat edilmesi gerekenler

Azure Container Service'de kullanılabilir her düzenleyicinin kendi güvenlik öncelikleri vardır. Örneğin, kapsayıcı hizmeti doğrudan SSH erişim tooorchestrator düğümler sınırlamanız gerekir. Bunun yerine, her orchestrator'ın kullanıcı Arabirimi veya komut satırı araçları kullanmalısınız (gibi `kubectl` Kubernetes için) hello konaklarına erişim olmadan toomanage hello kapsayıcı ortamı. Daha fazla bilgi için bkz: [bir uzak bağlantı tooa Kubernetes, DC/OS veya Docker Swarm kümesi olun](../articles/container-service/kubernetes/container-service-connect.md).

Ek orchestrator özgü güvenlik bilgileri için kaynakları aşağıdaki hello bakın:

* **Kubernetes**: [Kubernetes Dağıtımı için En İyi Güvenlik Uygulamaları](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**: [Kümenizin Güvenliğini Sağlama](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**: [Docker Güvenliği](https://www.docker.com/docker-security)

## <a name="next-steps"></a>Sonraki adımlar

* Docker mimarisi ve kapsayıcı güvenliği hakkında daha fazla bilgi için bkz: [giriş tooContainer güvenlik](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf).

* Hello Azure platform güvenliği hakkında daha fazla bilgi için bkz: [Azure Güvenlik Merkezi](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure).
