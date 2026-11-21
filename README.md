# CrackerKernels

This repository builds the latest stable Linux Kernel for use with Firecracker using GitHub actions. It will compile two kernels with different kernel options:

- `vmlinux`: Kernel compiled with base Firecracker config
- `vmlinux-podman`: Kernel compiled with base Firecracker config + kernel options to support podman

After compilation is complete, the resulting kernels are published as a single release tagged to the latest stable kernel version.

Latest release:

[![Latest Release](https://img.shields.io/github/v/release/icyguider/CrackerKernels?display_name=tag)](https://github.com/icyguider/CrackerKernels/releases/latest) [![Release Date](https://img.shields.io/github/release-date/icyguider/CrackerKernels?display_date=published_at)](https://github.com/icyguider/CrackerKernels/releases/latest)

## Why???

Pre-built stable Linux kernels for Firecracker aren't readily available from official sources. The [official Firecracker S3 bucket](https://s3.amazonaws.com/spec.ccfc.min?list-type=2) only provides compiled LTS kernels with a base config. Sometimes using the stable kernel is preferable over LTS, and sometimes custom kernel options are required for specific use cases.

Additionally, building these kernels transparently via Github actions provides users with a trusted resource for obtaining pre-built stable kernels for Firecracker.

#### Podman kernel?

I wanted to use Podman + gVisor inside of Firecracker VMs, so a custom kernel was required. Is this a good idea? Idk... sounded good to me.

#### Need a custom kernel?

Need a kernel with specific options enabled? Open an issue describing what use case you need a kernel for. Also include whatever kernel options are required.

## Workflow

- Runs daily at 06:00 UTC or manually via `workflow_dispatch`.
- Downloads the latest stable kernel from kernel.org and the newest `microvm-kernel-ci-x86_64-*.config` from the Firecracker repository.
- Skips the build when the release for the current kernel version already contains both assets.
- Creates or updates the `v<kernel-version>-firecracker` release.

## Inspiration

```
                                          _/                          
                                      _,_/_                           
                                     (/ < \)                          
             FUCK YOU THAT'S MINE      _/|\_     NO FUCK YOU IT'S MINE
                                      (/ | \)                         
                       \                 \)                 /         
                         __ <`-,-,_,-,        ,-,_,-,-'7 __           
                         \_;>   ^  _<---'  `--->_  ^   <`_/           
                            )  _,-'              `-,_  (              
                           /  /                      \  \             
__                       ,'  /                        \  `,           
)_\                  _,-'   /                          \   \          
   \_   _,-_-,_  _,-'      /                _,-_-,_ _,-',   \         
     \_/\,_ `  `'          \               /\,_ `  '         \        
      /\,_ `               |             _/\,_ `              |       
      |\,_` )     ,        <          __/ |\,_` )    ,        <       
       \\_`/,_,_ _\,_  _/ _/         /_/   \\_`/,_,__\,_  _/ _/       
       |\_/\,_| `   )=| |=(                |\_/\,_|    )=| |=(        
      /\_/  \_|     \-| |-/               /\_/  \_|    \-| |-/        
      \ )   < )     < / \ >               \ )   < )    < / \ >        
       \\    \\      \| |/                 \\    \\     \| |/         
        \\_   \\_    /| |\_                 \\_   \\_   /| |\_        
        ),_\   )_\  /_(  )_\                ),_\   )_\ /_(  )_\ mic   
```
