---
title: "apps_kscreen.json"
source: "https://gist.github.com/MrHighVoltage/78ca58218a569d253433fd4be883c6c3"
author:
  - "[[MrHighVoltage]]"
  - "[[VXsz]]"
published:
created: 2025-09-25
description: "GitHub Gist: instantly share code, notes, and snippets."
tags:
  - "clippings"
---
```
{
        
        
          

              "env": {
        
        
          

                  "PATH": "$(PATH):$(HOME)\/.local\/bin"
        
        
          

              },
        
        
          

              "apps": [
        
        
          

                  {
        
        
          

                      "name": "720p60 Desktop",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.1280x720@60 output.HDMI-A-1.hdr.disable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1080p60 Desktop",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.1920x1080@60 output.HDMI-A-1.hdr.disable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable ",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1080p120 Desktop",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.1920x1080@120 output.HDMI-A-1.hdr.disable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable ",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1080p120 HDR Desktop",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.1920x1080@120 output.HDMI-A-1.hdr.enable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable ",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "4k60 HDR Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.3840x2160@60 output.HDMI-A-1.hdr.enable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "4k120 HDR Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.3840x2160@120 output.HDMI-A-1.hdr.enable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1440p60 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "image-path": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctoroutput.HDMI-A-1.mode.2560x1440@60 output.HDMI-A-1.hdr.disable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable ",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1440p60 HDR Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "image-path": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctoroutput.HDMI-A-1.mode.2560x1440@60 output.HDMI-A-1.hdr.enable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable ",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1920x1200 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "kscreen-doctor output.HDMI-A-1.mode.1920x1200@60 output.HDMI-A-1.hdr.disable output.HDMI-A-1.enable output.DP-1.disable output.DP-2.disable",
        
        
          

                              "undo": "kscreen-doctor output.DP-1.enable output.DP-2.enable output.HDMI-A-1.disable"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  }
        
        
          

              ]
        
        
          

          }
```

```
{
        
        
          

              "env": {
        
        
          

                  "PATH": "$(PATH):$(HOME)\/.local\/bin"
        
        
          

              },
        
        
          

              "apps": [
        
        
          

                  {
        
        
          

                      "name": "FullHD Desktop",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 1920x1080 --rate 60 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "OP6 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --newmode 2264x1080_60.00  203.50  2264 2408 2648 3032  1080 1083 1093 1120 -hsync +vsync",
        
        
          

                              "undo": "xrandr --rmmode 2264x1080_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --addmode HDMI-A-0 2264x1080_60.00",
        
        
          

                              "undo": "xrandr --delmode HDMI-A-0 2264x1080_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 2264x1080_60.00 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "S23U Low native 120 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --newmode 1544x720_120.00  195.25  1544 1664 1824 2104  720 723 733 775 -hsync +vsync",
        
        
          

                              "undo": "xrandr --rmmode 1544x720_120.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --addmode HDMI-A-0 1544x720_120.00",
        
        
          

                              "undo": "xrandr --delmode HDMI-A-0 1544x720_120.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 1544x720_120.00 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "S23U mid native 60 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --newmode 2320x1080_60.00  208.50  2320 2472 2712 3104  1080 1083 1093 1120 -hsync +vsync",
        
        
          

                              "undo": "xrandr --rmmode 2320x1080_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --addmode HDMI-A-0 2320x1080_60.00",
        
        
          

                              "undo": "xrandr --delmode HDMI-A-0 2320x1080_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 2320x1080_60.00 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "4k60 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 3840x2160 --rate 60 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1440p60 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "image-path": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --newmode 2560x1440_60.00  312.25  2560 2752 3024 3488  1440 1443 1448 1493 -hsync +vsync",
        
        
          

                              "undo": "xrandr --rmmode 2560x1440_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --addmode HDMI-A-0 2560x1440_60.00",
        
        
          

                              "undo": "xrandr --delmode HDMI-A-0 2560x1440_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 2560x1440_60.00 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ]
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "iPad Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --newmode 2360x1640_60.00  328.50  2360 2536 2792 3224  1640 1643 1653 1700 -hsync +vsync",
        
        
          

                              "undo": "xrandr --rmmode 2360x1640_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --addmode HDMI-A-0 2360x1640_60.00",
        
        
          

                              "undo": "xrandr --delmode HDMI-A-0 2360x1640_60.00"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 2360x1640_60.00 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "4k120 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 3840x2160 --rate 120 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  },
        
        
          

                  {
        
        
          

                      "name": "1920x1200 Desktop",
        
        
          

                      "output": "",
        
        
          

                      "cmd": "",
        
        
          

                      "prep-cmd": [
        
        
          

                          {
        
        
          

                              "do": "bash \/home\/georg\/.config\/sunshine\/prepare_steam.sh",
        
        
          

                              "undo": "bash \/home\/georg\/.config\/sunshine\/finalize_steam.sh"
        
        
          

                          },
        
        
          

                          {
        
        
          

                              "do": "xrandr --output HDMI-A-0 --mode 1920x1200 --rate 60 --primary --output DisplayPort-0 --off --output DisplayPort-1 --off",
        
        
          

                              "undo": "xrandr --output HDMI-A-0 --off --output DisplayPort-0 --auto --primary --output DisplayPort-1 --auto --left-of DisplayPort-0"
        
        
          

                          }
        
        
          

                      ],
        
        
          

                      "image-path": ""
        
        
          

                  }
        
        
          

              ]
        
        
          

          }
```