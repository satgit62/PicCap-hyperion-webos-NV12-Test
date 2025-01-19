# PicCap-hyperion-webos-NV12-Test

PicCap v0.5.0

In the new hyperion-webos the NV12 video format has been added to the backends, so that NV12/YUV can be passed to the Hyperion or HyperHDR instead of RGB.

I have added an NV12 selection field to the user interface and an option to save the selected NV12 setting in config.json.

![PicCap GUI](https://github.com/user-attachments/assets/85662db0-ec27-474e-a54a-961f1319f3ee)


See the pull request:https://github.com/TBSniller/piccap/pull/90 and https://github.com/satgit62/piccap/tree/NV12

However, bumping an action to build PicCap ends with an error building the flattcc-native. See:https://github.com/satgit62/piccap/actions/runs/12784714938/job/35638252198
This is the reason why it has not been merged so far.

The easiest solution for me was to compile PicCap UI and the current hyperion webos separately and merge them into one build and create a package IPK file v0.5.0 for TV installation. 


# PicCap Build in a Linux development needs, buildroot-nc4 toolchain and Node.js.

# Setup buildroot-nc4 
```
cd /desired/path
wget -O toolchain.tar.gz $TOOLCHAIN_URL_FROM_RELEASES
tar -xvzf toolchain.tar.gz
rm toolchain.tar.gz
arm-webos-linux-gnueabi_sdk-buildroot/relocate-sdk.sh
export CMAKE_TOOLCHAIN_FILE=/desired/path/arm-webos-linux-gnueabi_sdk-buildroot/share/buildroot/toolchainfile.cmake
```
----------------------------------------------------------------------------------------------------------------------------
# PicCap Build
```
git clone -b NV12 --recursive https://github.com/satgit62/piccap piccap-build
# Unzip the build.zip folder and add it to the freshly cloned piccap-build.
cd piccap-build
npm install
# Only run 'npm run-script package' and do not try to compile 'hyperion-webos' yourself. Otherwise, the build folder will be overwritten.
npm run-script package
```

After building all files can be found in ./build.

