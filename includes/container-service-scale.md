# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Container Service kümesindeki aracı düğümlerini ölçekleme
Sonra [Azure kapsayıcı hizmeti kümesini dağıtma](../articles/container-service/dcos-swarm/container-service-deployment.md), toochange hello Aracısı düğüm sayısını gerekebilir. Örneğin, daha fazla kapsayıcı uygulaması veya örneği çalıştırmak için daha fazla aracı gerekebilir. 

Hello Azure portal kullanarak bir DC/OS, Docker Swarm veya Kubernetes kümesindeki Aracısı düğümler hello sayısını değiştirmek veya Azure CLI 2.0 hello. 

## <a name="scale-with-hello-azure-portal"></a>Azure portal ile Merhaba ölçeklendirme

1. Merhaba, [Azure portal](https://portal.azure.com), göz **kapsayıcı hizmetlerini**, toomodify istediğiniz hello kapsayıcı hizmeti'a tıklayın.
2. Merhaba, **kapsayıcı hizmeti** dikey penceresinde tıklatın **aracıları**.
3. İçinde **VM sayısını**, istenen hello aracıları düğüm sayısını girin.

    ![Merhaba portalı bir havuzda ölçeklendirme](./media/container-service-scale/container-service-scale-portal.png)

4. toosave hello yapılandırma tıklatın **kaydetmek**.

## <a name="scale-with-hello-azure-cli-20"></a>Azure CLI 2.0 Hello ile ölçeklendirin

Olduğundan emin olun, [yüklü](/cli/azure/install-az-cli2) en son Azure CLI 2.0 hello ve tooan içinde günlüğe azure hesabı (`az login`).

### <a name="see-hello-current-agent-count"></a>Merhaba geçerli aracı sayısı bakın
şu anda aracı toosee hello sayısı hello kümede çalışmasını hello `az acs show` komutu. Merhaba küme yapılandırmasını gösterir. Örneğin, komut gösterir hello adlı hello kapsayıcı hizmeti yapılandırmasını aşağıdaki hello `containerservice-myACSName` hello kaynak grubunda `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

Merhaba komut hello aracılarının hello sayısını döndürür `Count` altındaki `AgentPoolProfiles`.

### <a name="use-hello-az-acs-scale-command"></a>Kullanım az hello acs ölçek komutu
toochange hello hello çalıştırmak Aracısı düğümleri sayısı `az acs scale` komutunu ve sağlar hello **kaynak grubu**, **kapsayıcı hizmeti adı**ve istenen hello **yeni aracı sayısı**. Daha küçük veya daha büyük sayılar kullanarak sırasıyla yukarı veya aşağı ölçeklendirme yapabilirsiniz.

Örneğin, toochange hello hello önceki küme too10 aracıların sayısı hello aşağıdaki komutu yazın:

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

Hello Azure CLI 2.0 hello kapsayıcı hizmeti hello yeni aracı sayısı dahil olmak üzere, yeni yapılandırmasını hello temsil eden bir JSON dize döndürür.

Daha fazla komut seçeneği için `az acs scale --help` komutunu çalıştırın.

## <a name="scaling-considerations"></a>Ölçeklendirme konusunda dikkat edilmesi gerekenler

* Merhaba Aracısı düğüm sayısı 1 ile 100 (dahil) arasında olmalıdır. 

* Çekirdek kota hello bir küme içindeki aracı düğümlerin sayısını sınırlayabilirsiniz.

* Aracı düğümü ölçeklendirme hello Aracısı havuzunu içeren uygulanan tooan Azure sanal makine ölçek kümesi işlemleridir. Bir DC/OS kümesinde, bu makalede gösterilen hello işlemleri tarafından yalnızca Aracısı düğümlerine hello özel havuzunda ölçeklenir.

* Kümenizdeki dağıttığınız hello orchestrator bağlı olarak hello hello kümede çalışan bir kapsayıcı örnek sayısı ayrı olarak ölçeklendirebilirsiniz. Örneğin, bir DC/OS kümesinde hello kullan [Marathon kullanıcı Arabirimi](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello bir kapsayıcı uygulama örnek sayısı.

* Kapsayıcı hizmeti kümesindeki aracı düğümleri için otomatik ölçeklendirme şu anda desteklenmemektedir.

## <a name="next-steps"></a>Sonraki adımlar
* Azure Container Service ile Azure CLI 2.0 komutlarını kullanma hakkında [daha fazla örneğe](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) bakın.
* Azure Container Service’de [DC/OS aracı havuzları](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) hakkında daha fazla bilgi edinin.

