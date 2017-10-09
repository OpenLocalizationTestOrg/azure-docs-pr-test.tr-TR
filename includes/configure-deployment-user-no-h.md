Dağıtım kimlik bilgileri ile Merhaba oluşturun [az webapp dağıtım kullanıcısı ayarlanmadı](/cli/azure/webapp/deployment/user#set) komutu.

Dağıtım kullanıcı FTP ve yerel Git dağıtım tooa web uygulaması için gereklidir. Merhaba kullanıcı adı ve parola hesap düzeyindedir. _Bunlar Azure aboneliği kimlik bilgilerinizden farklıdır._

Komut, aşağıdaki Hello yerine  *\<kullanıcı adı >* ve  *\<parola >* yeni bir kullanıcı adı ve parola ile. Merhaba kullanıcı adının benzersiz olması gerekir. Merhaba parola en az sekiz karakter uzunluğunda, iki üç öğeleri aşağıdaki hello olmalıdır: harf, sayı, simge. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Alırsanız bir ` 'Conflict'. Details: 409` hata, değişiklik hello kullanıcı adı. ` 'Bad Request'. Details: 400` hatası alırsanız daha güçlü bir parola kullanın.

Bu dağıtım kullanıcısını bir kez oluşturduktan sonra tüm Azure dağıtımlarınız için kullanabilirsiniz.

> [!NOTE]
> Kayıt hello kullanıcı adı ve parolası. Bunları toodeploy hello web uygulaması daha sonra ihtiyacınız var.
>
>