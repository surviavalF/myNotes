
问题

npm ERR! code CERT_HAS_EXPIRED
npm ERR! errno CERT_HAS_EXPIRED
npm ERR! request to https://registry.npm.taobao.org/vue-loader-v16/download/vue-loader-v16-16.0.0-beta.5.4.tgz failed, reason: certificate has expired

解决
关闭证书验证
npm config set strict-ssl false