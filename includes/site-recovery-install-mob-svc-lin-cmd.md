1. Merhaba yükleyici tooa sunucusundaki yerel klasör (örneğin, tmp) tooprotect istediğiniz hello kopyalayın. Bir terminale hello aşağıdaki komutları çalıştırın:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. Mobility hizmeti tooinstall hello aşağıdaki komutu çalıştırın:

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. Yükleme tamamlandıktan sonra hello Mobility hizmeti tooget kayıtlı toohello yapılandırma sunucusu gerekir. Komut tooregister hello Mobility hizmetinin yapılandırma sunucusu aşağıdaki hello çalıştırın.

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>Mobility hizmeti yükleyicisinin komut satırı

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|Parametre|Tür|Açıklama|Olası değerler|
|-|-|-|-|
|-r |Zorunlu|Mobility hizmetinin (MS) yüklü olmalıdır veya MasterTarget(MT) yüklenmesi gerektiğini belirtir|MS </br> MT|
|-d |İsteğe bağlı|Mobility hizmetinin yükleneceği konum|/usr/local/ASR|
|-v|Zorunlu|Merhaba platformu üzerinde hangi hello mobilite hizmeti yüklü belirtir </br> </br>- **VMware** : mobility hizmeti üzerinde çalışan bir VM yüklüyorsanız bu değeri kullanın *VMware vSphere ESXi konakları*, *Hyper-V konakları* ve *Phsyical sunucuları* </br> - **Azure** : bir Azure Iaas VM aracısı yüklüyorsanız, bu değeri kullanın| VMware </br> Azure|
|-q|İsteğe bağlı|Sessiz modda toorun yükleyici belirtir| Yok|


#### <a name="mobility-service-configuration-command-line"></a>Mobility hizmeti yapılandırma komut satırı

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|Parametre|Tür|Açıklama|Olası değerler|
|-|-|-|-|
|-i |Zorunlu|Merhaba yapılandırma sunucusu IP|Herhangi bir geçerli IP adresi|
|-P |Zorunlu|Merhaba bağlantı parola kaydedildiği tam yol hello dosyası|Geçerli bir klasör|
