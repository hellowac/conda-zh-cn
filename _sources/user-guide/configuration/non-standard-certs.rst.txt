===============================
使用非标准证书
===============================

Using non-standard certificates

.. tab:: 中文

    在防火墙后使用 conda 可能需要使用一组非标准的证书，这通常需要自定义设置。
    
    如果你使用的是一组非标准的证书，那么 `requests` 包需要设置 ``REQUESTS_CA_BUNDLE``。  
    如果你遇到自签名证书相关的错误，可以尝试取消设置 ``REQUESTS_CA_BUNDLE`` 以及 ``CURL_CA_BUNDLE``，  
    并参考 `禁用 SSL 验证 <https://conda.io/projects/conda/en/latest/user-guide/configuration/disable-ssl-verification.html>`_  
    以便通过 HTTP 创建 conda 环境。
    
    你可能还需要将 conda 的证书替换为公司提供的根证书。
    
    以下是在 macOS 上的一种解决流程：
    
    * 打开 Chrome，访问任意网站，点击网址左侧的锁形图标。  
      在下拉菜单中点击「证书」。弹出的窗口中会显示一个证书链，  
      最上方（即窗口中的顶层）是根证书（例如 Zscaler Root CA）。
    * 打开 macOS 钥匙串（Keychain Access），点击「证书」，  
      从多个证书中找到你刚识别出的根证书。将其导出到任意文件夹。
    * 使用 OpenSSL 转换该证书：  
      ``openssl x509 -inform der -in /path/to/your/certificate.cer -out /path/to/converted/certificate.pem``
    * 临时测试时，可在 shell 中设置环境变量：  
      ``export REQUESTS_CA_BUNDLE=/path/to/converted/certificate.pem``
    * 如需永久设置，请编辑你的 shell 配置文件（如 ``.bashrc`` 或 ``.zshrc``），添加以下行：  
      ``export REQUESTS_CA_BUNDLE=/path/to/converted/certificate.pem``  
      然后退出终端并重新打开，再次验证。

.. tab:: 英文

    Using conda behind a firewall may require using a non-standard
    set of certificates, which requires custom settings.
    
    If you are using a non-standard set of certificates, then the
    requests package requires the setting of ``REQUESTS_CA_BUNDLE``.
    If you receive an error with self-signed certifications, you may
    consider unsetting ``REQUESTS_CA_BUNDLE`` as well as ``CURL_CA_BUNDLE`` and `disabling SSL verification <https://conda.io/projects/conda/en/latest/user-guide/configuration/disable-ssl-verification.html>`_
    to create a conda environment over HTTP.
    
    You may need to set the conda environment to use the root certificate
    provided by your company rather than conda’s generic ones.
    
    One workflow to resolve this on macOS is:
    
    * Open Chrome, got to any website, click on the lock icon on the left
      of the URL. Click on «Certificate» on the dropdown. In the next window
      you see a stack of certificates. The uppermost (aka top line in window)
      is the root certificate (e.g. Zscaler Root CA).
    * Open macOS keychain, click on «Certificates» and choose among the
      many certificates the root certificate that you just identified.
      Export this to any folder of your choosing.
    * Convert this certificate with OpenSSL: ``openssl x509 -inform der -in /path/to/your/certificate.cer -out /path/to/converted/certificate.pem``
    * For a quick check, set your shell to acknowledge the certificate: ``export REQUESTS_CA_BUNDLE=/path/to/converted/certificate.pem``
    * To set this permanently, open your shell profile (e.g. ``.bashrc`` or ``.zshrc``) and add this line: ``export REQUESTS_CA_BUNDLE=/path/to/converted/certificate.pem.``
      Now exit your terminal/shell and reopen. Check again.
