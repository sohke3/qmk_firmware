# QMK 환경 설정하기

여러분의 키맵을 빌드할수 있게 되기 전에, 몇 가지 소프트웨어를 설치하고 빌드 환경을 설정해야 합니다. 얼마나 많은 키보드 펌웨어를 컴파일 하려는지는 모르지만, 이 과정은 단 한번만 하시면 됩니다.

## 1. 전제 조건

시작하려면 몇 가지 소프트웨어가 필요합니다.There are a few pieces of software you'll need to get started.

* [텍스트 에디터](newbs_learn_more_resources.md#text-editor-resources)
  * 일반 텍스트 파일을 수정하고 저장할 수 있는 프로그램이 필요합니다. 많은 OS에 딸려오는 기본 에디터는 일반 텍스트 파일을 저장하지 않기 때문에, 선택할때 어떤 에디터가 지원되는지 확인하십시오.
* [툴박스 (선택사항)](https://github.com/qmk/qmk_toolbox)
  * 윈도우와 맥에서 사용가능한 GUI 프로그램. 커스텀 키보드를 프로그램하고 디버그 할 수 있게 해줍니다.

?> Linux/Unix 커맨드라인으로 작업해보지 않았다면, 몇 가지 기본 개념과 명령어를 익히셔야 합니다. [이 리소스들](newbs_learn_more_resources.md#command-line-resources)은 QMK를 작업하기에 충분히 가르쳐줄 것입니다.

## 2. 빌드 환경을 준비하세요 :id=set-up-your-environment

우리는 QMK를 가능한 한 쉽게 설치할 수 있도록 노력해왔습니다. 여러분이 Linux/Unix 환경만 준비하시면, QMK가 나머지 것들을 설치할 것입니다.

<!-- tabs:start -->

### ** 윈도우 **

QMK는 CLI와 다른 필요한 플러그인과 같이, MSYS2와 관련된 것들을 관리하고 있습니다. 또한, 현재 환경에서 바로 띄울수 있는 'QMK MSYS' 터미널 숏컷이 제공됩니다.

#### 전제 조건

[QMK MSYS](https://msys.qmk.fm/)를 설치하셔야 합니다. 최신 버전은 [여기](https://github.com/qmk/qmk_distro_msys/releases/latest)에서 구하실 수 있습니다.

아니면, 수동으로 MSYS2를 설치하시고 싶다면, 다음 섹션의 절차를 따르십시오.

<details>
  <summary>수동 설치</summary>

?> 'QMK MSYS'를 사용하시면, 이 과정을 무시하십시오.

#### 전제 조건

MSYS2, Git, Python을 설치하셔야 합니다. https://www.msys2.org에서 설치 과정을 따르십시오.

MSYS2가 설치되면, 모든 열려있는 MSYS 터미널을 닫고, 새로운 MinGW 64비트 터미널을 여십시오.

!> **NOTE:** The MinGW 64-bit terminal is *not* the same as the MSYS terminal that opens when installation is completed. Your prompt should say "MINGW64" in purple text, rather than "MSYS". See [this page](https://www.msys2.org/wiki/MSYS2-introduction/#subsystems) for more information on the differences.

Then run the following command:

    pacman --needed --noconfirm --disable-download-timeout -S git mingw-w64-x86_64-toolchain mingw-w64-x86_64-python3-pip mingw-w64-x86_64-python-pillow

#### Installation

Install the QMK CLI by running:

    python3 -m pip install qmk

</details>

### ** macOS **

QMK maintains a Homebrew tap and formula which will automatically install the CLI and all necessary dependencies.

#### Prerequisites

You will need to install Homebrew. Follow the instructions on https://brew.sh.

#### Installation

Install the QMK CLI by running:

    brew install qmk/qmk/qmk

### ** Linux/WSL **

?> **Note for WSL users**: By default, the installation process will clone the QMK repository into your WSL home directory, but if you have cloned manually, ensure that it is located inside the WSL instance instead of the Windows filesystem (ie. not in `/mnt`), as accessing it is currently [extremely slow](https://github.com/microsoft/WSL/issues/4197).

#### Prerequisites

You will need to install Git and Python. It's very likely that you already have both, but if not, one of the following commands should install them:

* Debian / Ubuntu / Devuan: `sudo apt install -y git python3-pip`
* Fedora / Red Hat / CentOS: `sudo yum -y install git python3-pip`
* Arch / Manjaro: `sudo pacman --needed --noconfirm -S git python-pip libffi`
* Void: `sudo xbps-install -y git python3-pip`
* Solus: `sudo eopkg -y install git python3`
* Sabayon: `sudo equo install dev-vcs/git dev-python/pip`
* Gentoo: `sudo emerge dev-vcs/git dev-python/pip`

#### Installation

Install the QMK CLI by running:

    python3 -m pip install --user qmk

#### Community Packages

These packages are maintained by community members, so may not be up to date or completely functional. If you encounter problems, please report them to their respective maintainers.

On Arch-based distros you can install the CLI from the official repositories (NOTE: at the time of writing this package marks some dependencies as optional that should not be):

    sudo pacman -S qmk

You can also try the `qmk-git` package from AUR:

    yay -S qmk-git

###  ** FreeBSD **

#### Installation

Install the FreeBSD package for QMK CLI by running:

    pkg install -g "py*-qmk"

NOTE: remember to follow the instructions printed at the end of installation (use `pkg info -Dg "py*-qmk"` to show them again).

<!-- tabs:end -->

## 3. Run QMK Setup :id=set-up-qmk

<!-- tabs:start -->

### ** Windows **

After installing QMK you can set it up with this command:

    qmk setup

In most situations you will want to answer `y` to all of the prompts.

### ** macOS **

After installing QMK you can set it up with this command:

    qmk setup

In most situations you will want to answer `y` to all of the prompts.

### ** Linux/WSL **

After installing QMK you can set it up with this command:

    qmk setup

In most situations you will want to answer `y` to all of the prompts.

?>**Note on Debian, Ubuntu and their derivatives**:
It's possible, that you will get an error saying something like: `bash: qmk: command not found`.
This is due to a [bug](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=839155) Debian introduced with their Bash 4.4 release, which removed `$HOME/.local/bin` from the PATH. This bug was later fixed on Debian and Ubuntu.
Sadly, Ubuntu reintroduced this bug and is [yet to fix it](https://bugs.launchpad.net/ubuntu/+source/bash/+bug/1588562).
Luckily, the fix is easy. Run this as your user: `echo 'PATH="$HOME/.local/bin:$PATH"' >> $HOME/.bashrc && source $HOME/.bashrc`

###  ** FreeBSD **

After installing QMK you can set it up with this command:

    qmk setup

In most situations you will want to answer `y` to all of the prompts.

<!-- tabs:end -->

?> The qmk home folder can be specified at setup with `qmk setup -H <path>`, and modified afterwards using the [cli configuration](cli_configuration.md?id=single-key-example) and the variable `user.qmk_home`. For all available options run `qmk setup --help`.

?> If you already know how to use GitHub, [we recommend that you follow these instructions](getting_started_github.md) and use `qmk setup <github_username>/qmk_firmware` to clone your personal fork. If you don't know what that means you can safely ignore this message.

## 4. Test Your Build Environment

Now that your QMK build environment is set up, you can build a firmware for your keyboard. Start by trying to build the keyboard's default keymap. You should be able to do that with a command in this format:

    qmk compile -kb <keyboard> -km default

For example, to build a firmware for a Clueboard 66% you would use:

    qmk compile -kb clueboard/66/rev3 -km default

When it is done you should have a lot of output that ends similar to this:

```
Linking: .build/clueboard_66_rev3_default.elf                                                       [OK]
Creating load file for flashing: .build/clueboard_66_rev3_default.hex                               [OK]
Copying clueboard_66_rev3_default.hex to qmk_firmware folder                                        [OK]
Checking file size of clueboard_66_rev3_default.hex                                                 [OK]
 * The firmware size is fine - 26356/28672 (2316 bytes free)
```

# Creating Your Keymap

You are now ready to create your own personal keymap! Move on to [Building Your First Firmware](newbs_building_firmware.md) for that.
