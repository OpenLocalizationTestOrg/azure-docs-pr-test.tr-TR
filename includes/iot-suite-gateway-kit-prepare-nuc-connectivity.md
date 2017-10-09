## <a name="prepare-your-intel-nuc"></a>Intel NUC hazırlama

toocomplete hello donanım Kurulum şunları yapmanız gerekir:

- Merhaba Seti'nde dahil, Intel NUC toohello güç kaynağı bağlayın.
- Ethernet kablosu kullanarak Intel NUC tooyour ağınıza bağlayın.

Intel NUC ağ geçidi cihazınız hello donanım Kurulumu tamamladınız.

### <a name="sign-in-and-access-hello-terminal"></a>Oturum açma ve hello terminal erişim

İki seçenek tooaccess, Intel NUC bir terminal ortamına sahip:

- Klavye varsa ve bağlı tooyour Intel NUC izlemek, hello Kabuğu doğrudan erişebilirsiniz. Merhaba varsayılan kimlik bilgileri olan kullanıcı adı **kök** ve parola **kök**.

- Masaüstü makinenizden SSH kullanarak, Intel NUC erişim hello Kabuğu.

#### <a name="sign-in-with-ssh"></a>Oturum SSH oturum

toosign SSH oturum Intel NUC başlangıç IP adresi gerekir. Klavye varsa ve bağlı tooyour Intel NUC izlemek, hello kullan `ifconfig` komut toofind başlangıç IP adresi. Alternatif olarak, ağınızdaki aygıtların tooyour yönlendirici toolist hello adreslerini bağlayın.

Kullanıcı adıyla oturum **kök** ve parola **kök**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>İsteğe bağlı: Intel NUC üzerinde bir klasör paylaşın

İsteğe bağlı olarak, masaüstü ortamınızı, Intel NUC tooshare bir klasör isteyebilirsiniz. Bir klasör paylaşımı, tercih edilen Masaüstü metin düzenleyici, toouse sağlar (gibi [Visual Studio Code](https://code.visualstudio.com/) veya [Sublime Text](http://www.sublimetext.com/)) kullanmak yerine, Intel NUC tooedit dosyalarda `nano` veya `vi`.

tooshare Windows, bir klasör, Intel NUC hello üzerinde Samba sunucusu yapılandırın. Alternatif olarak, Masaüstü makinenizde SFTP istemci ile Merhaba Intel NUC hello SFTP sunucusu kullanın.
