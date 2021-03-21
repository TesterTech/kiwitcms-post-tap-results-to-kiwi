# kiwitcms-post-tap-results-to-kiwi
Code for the YouTube video: https://youtu.be/d7kK5wuBeZU

- Install Python3 and PIP
```
sudo apt install python3
sudo apt install python3-pip
```

- Optional: ```~/.bash_aliases```
```
alias python=python3
alias py=python
alias pip=pip3
```

- Get the code with the example TAP report
```
git clone https://github.com/kiwitcms/tap-plugin.git
```

- Certificate stuff (note if you have your own certs then this is different for you).
```
wget --no-check-certificate https://localhost/static/ca.crt
openssl x509 -text -noout -in ca.crt 
sudo vim /etc/hosts
(add the host hash to 127.0.0.1 <hash code>)
export SSL_CERT_FILE=/home/demo/kiwi/tap-plugin/ca.crt 
sudo docker exec -it kiwi_web /Kiwi/manage.py set_domain <hash code>
```

- Minimal setup needed
```
vim ~/.tcms.conf
```
- Add this to the file, note the hash can be different here.
```
[tcms]
url = https://<hash code>/xml-rpc/
username = demo
password = demo
```

- Install the tap plugin program
```
pip install kiwitcms-tap-plugin
```
- 
```
export JOB_NAME="My Cool tesing job"
export TCMS_PRODUCT_VERSION="1"
export BUILD_NUMBER="1"
```
- Finally call it. 
```
tcms-tap-plugin tests/data/traceback.tap 
```
Now go to you kiwi instance and see the results.

## References
- https://kiwitcms.readthedocs.io/en/latest/installing_docker.html?highlight=ssl
- https://github.com/kiwitcms/
- https://www.youtube.com/watch?v=S7h4OG7aeFA
- https://kiwitcms.org/blog/atodorov/2018/11/05/test-runner-plugin-specification/
- https://tcms-api.readthedocs.io/en/latest/modules/tcms_api.html#module-tcms_api
- https://tcms-api.readthedocs.io/en/latest/modules/tcms_api.plugin_helpers.html
- https://stackoverflow.com/a/46337779
- https://www.electricmonk.nl/log/2018HTTPSConnection/06/02/ssl-tls-client-certificate-verification-with-python-v3-4-sslcontext/
