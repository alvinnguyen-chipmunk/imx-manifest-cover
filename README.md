i.MX Repo Manifest README

This repo is used to download manifests for i.MX BSP releases.

Specific instructions will reside in READMEs in each branch.

The branch will be based on the release type Linux or Android with release manifests in each branch tied to the base releases.

For example for i.MX Linux Yocto Project releases the branches will be imx_linux_<Yocto Project release> so imx_linux_rocko with
all manifests tied to releases on rocko in this branch.

*************************************************************************************************************************
To use this manifest repo, the 'repo' tool must be installed first.
-------------------------------------------------------------------------------------------------------------------------

$: mkdir ~/bin
$: curl http://commondatastorage.googleapis.com/git-repo-downloads/repo  > ~/bin/repo
$: chmod a+x ~/bin/repo
$: PATH=${PATH}:~/bin


To excute 
$: mkdir <release>
$: cd <release>
$: repo init -u https://github.com/alvinnguyen-chipmunk/imx-manifest-cover.git -b <branch name> [ -m <release manifest>]

Each branch will have detailed READMEs describing exact syntax.

*************************************************************************************************************************
Examples
-------------------------------------------------------------------------------------------------------------------------

To download the 4.9.88-2.0.0 GA release
repo init -u https://github.com/alvinnguyen-chipmunk/imx-manifest-cover.git -b imx-linux-rocko -m imx-4.9.88-2.0.0_ga.xml

*************************************************************************************************************************
Setup the build folder for a BSP release:
-------------------------------------------------------------------------------------------------------------------------

First at all, read carefully i.MX_Yocto_Project_User's_Guide.pdf for more information. 

Note: The remaining instructions are for setting up a BSP release only. For setting
up a demo, please see imx-manifest/README-<demo> for further instructions.

$: [MACHINE=<machine>] [DISTRO=fsl-imx-<backend>] source ./fsl-setup-release.sh -b bld-<backend>

<machine> defaults to imx6qsabresd

<backend>   Graphics backend type
xwayland    Wayland with X11 support - default distro
wayland     Wayland
x11         X11  (not supported for mx8)
fb          Framebuffer (not supported for mx8)

Note if the poky community distro is used then build breaks will happen with some
components using our meta-fsl-bsp-release layer.

Examples:
- Setup for XWayland.
$: MACHINE=imx7ulpevk DISTRO=fsl-imx-xwayland source ./fsl-setup-release.sh -b bld-xwayland

*************************************************************************************************************************
Build an image:
-------------------------------------------------------------------------------------------------------------------------

bitbake <image recipe>

Some image recipes:
fsl-image-gui - full image with demos and tests used for testing with graphics, no QT.
fsl-image-qt5 - fsl-image-gui with QT 5.9.

