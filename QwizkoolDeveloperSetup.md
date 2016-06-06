1. Install ember prerequisites

You will need the following things properly installed on your computer.  
Git  
Node.js v0.10.x and NPM v2.x. Please use the node/npm installer script to cleanly re-install https://gist.github.com/brock/5b1b70590e1171c4ab54. In the script, ensure that NODE_VERSION="0.10"  
Bower v1.7.x. npm install bower  
[ember-cli v.2.5.x] npm install -g ember-cli@0.1.2  

1. Create a workspace in your Ubuntu 14.04 machine
mkdir -p ~/work/qwizkool

1. Checkout the required projects  
```
cd ~/work/qwizkool  
git clone git@gitlab.com:qwizkool/qwizkool-client.git  
git clone git@gitlab.com:qwizkool/slim_api.git  
git clone git@gitlab.com:qwizkool/scripts.git  
```

1. Setup the client project  

```
cd ~/work/qwizkool/qwizkool-client  
npm install  
bower install  
```

1. Build and Deploy
cd ~/work/qwizkool/scripts  
./buildall.sh  

