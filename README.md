Steps:

1.      RPI_REPO=~/raspberrypi2_krogoth 
        mkdir -p ${RPI_REPO}; cd ${RPI_REPO}

2. Repo init:-
        
         repo init  -m  https://github.com/sanandin/manifest.git  --manifest-branch=master --manifest-name=manifest.xml
  
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

 

