Steps:

1.      RPI_REPO=~/raspberrypi2_krogoth 
        mkdir -p ${RPI_REPO}; cd ${RPI_REPO}

2. Repo init:-
        
         repo init  -m  https://github.com/sanandin/manifests.git  --manifest-branch=master --manifest-name=manifest.xml
  
3. To Do repo sync:-
          
         repo sync

4. Configure for the Raspberry PI Target:- 

          cd ${RPI_REPO}/raspberrypi2_base_dir
          MACHINE=raspberrypi2 source oe-init-build-env

   This will place you in the "raspberrypi2_base/build " directory.

5. Edit bblayers.conf File:-

         <path>/raspberrypi2_base_dir/meta-openembedded/meta-oe  \
         <path>/raspberrypi2_base_dir/meta-openembedded/meta-gnome  \
         <path>/raspberrypi2_base_dir/meta-raspberrypi \
         <path>/raspberrypi2_base_dir/meta-browser \
         <path>/raspberrypi2_base_dir/meta-ui \

   Where "path" is the absolute path to the raspberrypi2_base poky project.

7. run command:- 
         MACHINE=raspberrypi2 bitbake rpi-ui-image
        

Steps to run firefox browser and load the URL:-


On raspberrypi2:-

         firefox /usr/bin/videodemo/index.html &

 ## Instructions for Raspberry Pi2 client

### Get the source code to build

```shell
PRODUCT_NAME="rpi2_browser"
MACHINE_NAME="raspberrypi2"
LOCAL_REPO_ROOT=`pwd`"/${PRODUCT_NAME}_repo"
LOCAL_REPO="${LOCAL_REPO_ROOT}/${PRODUCT_NAME}"
REMOTE_REPO_ROOT="https://github.com/hemanth-krishna"
REMOTE_MANIFEST_REPONAME="manifests.git"
#REMOTE_MANIFEST_BRANCH="${PRODUCT_NAME}"
REMOTE_MANIFEST_BRANCH="master"
REMOTE_MANIFEST_NAME="${PRODUCT_NAME}.xml"


if [ -d "${LOCAL_REPO_ROOT}" ]; then
  echo "Directory ${LOCAL_REPO_ROOT} already exists. Quitting."
  exit -1
fi

mkdir ${LOCAL_REPO_ROOT}
cd ${LOCAL_REPO_ROOT}
repo init -u "${REMOTE_REPO_ROOT}/${REMOTE_MANIFEST_REPONAME}" \
          --manifest-branch="${REMOTE_MANIFEST_BRANCH}" \
          --manifest-name="${REMOTE_MANIFEST_NAME}"

repo sync
```

### Configure the build

```shell
cd ${LOCAL_REPO}
MACHINE=${MACHINE_NAME} source oe-init-build-env "build_${PRODUCT_NAME}"

# edit the bblayers.conf file to add on these yocto layers

echo \"         ${LOCAL_REPO}/meta-openembedded/meta-oe     \\ \"
echo \"         ${LOCAL_REPO}/meta-openembedded/meta-gnome  \\ \"
echo \"         ${LOCAL_REPO}/meta-raspberrypi              \\ \"
echo \"         ${LOCAL_REPO}/meta-browser                  \\ \"
echo \"         ${LOCAL_REPO}/meta-ui                       \\ \"
```

### Build using the bitbake command
```shell
MACHINE=${MACHINE_NAME} bitbake rpi-ui-image
```

### Launch the applciation on the target after flashing the image and booting up
```shell
firefox /usr/bin/videodemo/index.html &
```


