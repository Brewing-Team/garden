---
title: "RIOT - The friendly Operating System for the Internet of Things"
source: "https://www.riot-os.org/"
author:
published:
created: 2025-09-21
description:
tags:
  - "clippings"
---
## RIOT

In a nutshell

RIOT powers the Internet of Things like Linux powers the Internet. RIOT is a [free, open source](https://www.riot-os.org/#license) operating system developed by a [grassroots community](https://www.riot-os.org/#community) gathering companies, academia, and hobbyists, [distributed all around the world](http://summit.riot-os.org/).

RIOT supports most low-power [IoT devices](https://www.riot-os.org/boards.html), [microcontroller architectures](https://www.riot-os.org/cpus.html) (32-bit, 16-bit, 8-bit), and [external devices](https://www.riot-os.org/drivers.html). RIOT aims to implement all relevant [open standards](https://www.riot-os.org/#features) supporting an Internet of Things that is connected, secure, durable & privacy-friendly.

## Out of the box usage

Features

##### Connectivity

###### RIOT breaks silos.

RIOT is modular to adapt to application needs. We aim to support all common network technologies and Internet standards. RIOT is open to new developments and often an early adaptor in networking.

##### Quality

###### RIOT is constantly tested.

The RIOT community cares about code quality. Therefore, we use established tools such as [embUnit - Unit Testing](https://sourceforge.net/projects/embunit/) and [Continuous Integration](https://ci.riot-os.org/), performing [Hardware in the Loop (HIL)](https://hil.riot-os.org/results/) testing on multiple boards nightly.

##### License

###### RIOT is free and open source.

Most of the software developed by the RIOT community is available under the terms of the GNU [LGPLv2.1](http://www.gnu.org/licenses/old-licenses/lgpl-2.1.en.html), published by the Free Software Foundation. This ensures an open Internet and allows for building blocks under different licenses.

## First steps

Get started#### [Get the code](https://github.com/RIOT-OS/RIOT)#### [Read the documentation](https://doc.riot-os.org/)#### [Ask questions](https://forum.riot-os.org/)

## 48445

Commits

## 290

Contributors

## 281

Boards

## 74

Supported CPUs

## Get in touch

On the shoulders of a grassroots community

---

#### Developers

You want to participate and contribute to the kernel development or integrate new MCU and platform support? You're welcome!

Read the [newcomer guide](https://github.com/RIOT-OS/RIOT/blob/master/CONTRIBUTING.md) and scan through our [community processes](https://github.com/RIOT-OS/RIOT/wiki/RIOT-Community-Processes). Subscribe to the [RIOT Forum](https://forum.riot-os.org/), which is the right place in case you have questions. For live discussions, join our [Matrix chat](https://matrix.to/#/#riot-os:matrix.org).

The [RIOT issue tracker](https://github.com/RIOT-OS/RIOT/issues?state=open) informs about bugs and enhancement requests. You could also subscribe to the [notifications mailing list](https://lists.stillroot.org/postorius/lists/notifications.lists.riot-os.org/) to get informed about new issues, comments, and pull requests. Take a look at our [coding conventions](https://github.com/RIOT-OS/RIOT/blob/master/CODING_CONVENTIONS.md).

#### Users

Whether you are looking for help with writing an application for RIOT, learn more about it, or just want to stay in the loop, you are invited to join the [RIOT Forum](https://forum.riot-os.org/). We are also available on [Stack Overflow](https://stackoverflow.com/questions/tagged/riot-os).

If you are looking for existing open source projects that are based on RIOT, you can check and [hackster.io](https://www.hackster.io/riot-os).

RIOTers meet face to face at the annual [RIOT Summit](https://www.riot-os.org/community.html#summit).

## RIOT in the wild

Users

[![Continental](https://www.riot-os.org/assets/img/companies/continental-logo.svg)](https://www.continental.com/en)

[![Lauterbach](https://www.riot-os.org/assets/img/companies/lauterbach.png)](https://www.lauterbach.com/)

[![Locha Mesh](https://www.riot-os.org/assets/img/companies/lochamesh-logo.svg)](https://locha.io/)

[![Sapienza University of Rome](https://www.riot-os.org/assets/img/companies/sapienza-university.jpg)](https://www.uniroma1.it/en/)

[![Savoir-faire Linux](https://www.riot-os.org/assets/img/companies/savoir-faire-linux-logo.svg)](https://savoirfairelinux.com/en)

[![SSV Embedded Software Systems](https://www.riot-os.org/assets/img/companies/ssv-logo.svg)](https://www.ssv-embedded.de/en/)

[![wolfSSL](https://www.riot-os.org/assets/img/companies/wolfssl-logo.jpg)](https://www.wolfssl.com/)

User stories

## F.A.Q

Frequently Asked Questions

- Under what license is RIOT code released?
	The license is currently LGPLv2.1
- Why LGPL?
	Studies such as [this one](https://www.gartner.com/en/newsroom/press-releases/2014-10-09-gartner-says-by-2017-50-percent-of-internet-of-things-solutions-will-originate-in-startups-that-are-less-than-three-years-old) show that small companies and start-ups are going to determine IoT. More than bigger companies, such small structures need to spread development and maintenance costs for the kernel and all the software that is not their core business. Our analysis is that this is more compatible with LGPL than with BSD/MIT.
	We are of the opinion that, compared to BSD/MIT, LGPL will improve final user experience, security and privacy, by hindering device lock-down, favoring up-to-date, and field-upgradable code. We think this a more solid base to provide a consistent, compatible, secure-by-default standard system which developers can build upon to create trustworthy IoT applications, while not hindering business models based on closed source linked with RIOT (see the [automated tools](https://github.com/RIOT-OS/RIOT/tree/master/examples/advanced/bindist) provided to help check LGPL compliance, and/or [this technical guide](https://github.com/RIOT-OS/RIOT/wiki/LGPL-compliancy-guide))
	Since solutions competing with RIOT are quasi-exclusively BSD/MIT, we gauge that LGPL is a way to stand out favorably, and is a characteristic backing positive comparisons of RIOT with Linux.
	Last but not least, we think that (L)GPL is a better base than BSD/MIT to keep the community united in the mid and long run.
	For the record: we have also considered MIT/BSD (see, e.g., [this thread](https://forum.riot-os.org/t/switch-to-bsd/612)), but there was not enthusiastic majority supporting such a switch.
	Compare [https://github.com/RIOT-OS/RIOT/issues/2128](https://github.com/RIOT-OS/RIOT/issues/2128)
- How is RIOT development organized?
	In short there are certain [Coding Conventions](https://github.com/RIOT-OS/RIOT/blob/master/CODING_CONVENTIONS.md) to follow and we are using [Github](https://github.com/) ’s pull requests for code review. So for new features and fixes create a fork of the [RIOT repository](https://github.com/RIOT-OS/RIOT) and open a pull request with a detailed description of your changes.
	For a more in depth description check out the dedicated document on [development procedures](https://github.com/RIOT-OS/RIOT/blob/master/CONTRIBUTING.md).
	Also, do check out the open [community processes](https://github.com/RIOT-OS/RIOT/wiki/RIOT-Community-Processes).
- What should be my first steps to get started?
	The [Starter Guide](https://github.com/RIOT-OS/RIOT/wiki/Creating-your-first-RIOT-project) might be just what you are looking for.
- I want to contribute. How should I proceed?
	First of all, welcome to the RIOT community! There is a dedicated README on [contributing](https://github.com/RIOT-OS/RIOT/blob/master/CONTRIBUTING.md) listing opportunities to interact with fellow RIOT enthusiasts and some suggestions how to get started.
- I have an issue with RIOT code I can't solve. How can I get help?
	**For critical vulnerabilities we would appreciate you to report them with a 90 day heads-up to [security@riot-os.org](https://www.riot-os.org/) first, before making them publicly available. You may use the GPG-Key [44C6AE441172F88D3423E81F5F7964D0F4239033](https://www.riot-os.org/assets/keys/security.asc) to encrypt your report.**
	It’s a very good idea to search our [forum](https://forum.riot-os.org/) first, maybe someone has already solved your issue! You can also create an account there, and post via the forum website, or via email to [help@riot-os.org](https://www.riot-os.org/) following [this guide](https://forum.riot-os.org/t/riot-forum-as-a-mailing-list/46). Another option is to log an [issue](https://github.com/RIOT-OS/RIOT/issues/new/choose) in GitHub.
	You’re also welcome to ask in the Matrix room [#riot-os at matrix.org](https://matrix.to/#/#riot-os:matrix.org), but don’t be disappointed if everyone there is busy.
- Does RIOT run as-is on my hardware?
	Check out this page on supported [hardware](https://www.riot-os.org/boards.html). If your hardware is not listed there, you’re welcome to provide a port for your hardware!
- How much memory (ROM/RAM) will it need?
	This depends on the board and on the application. When you compile an application for a board, the last thing printed gives each sections memory footprint and looks like this:
	```
	text       data     bss     dec     hex filename
	    77732     296   24272  102300    18f9c applications/sixlowapp/bin/iot-lab_M3/sixlowapp.elf
	```
	The required RAM is `data + bss`, ROM is `text + data`.
	**Please note:** Usually a big portion of RAM is consumed by the stack space for threads. Although RIOT maintainers try to optimize the default values, manual tweaking may be necessary to get the most efficient results. You can check the maximum stack usage at runtime with the shell command `ps` or the corresponding function `thread_print_all()` from the module `ps`.
- My terminal doesn't recognize newlines coming from RIOT over serial!
	See [this page](https://github.com/RIOT-OS/RIOT/wiki/Configure-terminal-programs-for-correct-display-of-newlines).
- Does RIOT support Raspberry Pi?
	RIOT does support the [Raspberry Pi Pico](https://doc.riot-os.org/group__boards__rpi__pico.html) and the [Raspberry Pi Pico W](https://doc.riot-os.org/group__boards__rpi__pico__w.html).
	The Linux-capable Raspberry Pi boards are not supported, though. From the RIOT point of view these boards are supercomputers. RIOT targets mostly systems that are too constrained to run Linux (less than 1MB of RAM, no MMU). However, it is supported to run [RIOT native](https://doc.riot-os.org/group__boards__native.html) ([or the 64 bit native variant](https://doc.riot-os.org/group__boards__native64.html)) on platforms like the Raspberry Pi, and other hardware supported by Linux.
	A good rule of thumb concerning RIOT support of a particular board is: can Linux support this board? If yes, then you should ask yourself *why* you really want to use RIOT (other than [native](https://doc.riot-os.org/group__boards__native.html)) on this board. If no, then RIOT support is probably desirable.
- What is the benefit of RIOT compared to bare metal programming?
	In short: Increased productivity.
	RIOT provides a number of features that make reusing code easier: In RIOT hardware is abstracted by vendor-agnostic driver APIs and multi-threading eases decoupling of the implementation of distinct features. Particularly helpful is RIOT’s module system, that also allows seamless integration of external modules.
	In addition RIOT already provides a lot of functionality that is ready for use, such as modules providing a network stack, network protocols, and large number of device drivers. This can cut down development time significantly compared to bare metal programming.
- How does RIOT compare to other operating systems for embedded or IoT devices?
	Developing an OS for embedded systems involves many trade-offs. Hence, there is not a single right choice for every application. In this comparison we try to give a balanced comparison of the high-level architectural trade-offs other operating systems took and how they compare to RIOT. Additionally, we compare the government of the project and the licensing.
	##### RIOT
	RIOT runs on many different CPU architectures by many different vendors, from [a tiny 8-bit MCU with 2 KiB RAM and 32 KiB flash](https://doc.riot-os.org/group__boards__arduino-nano.html) all the way up to high-performance [ARM Cortex M](https://doc.riot-os.org/group__boards__same54-xpro.html) and [RISC-V](https://doc.riot-os.org/group__boards__esp32c3__devkit.html) MCUs. Because RIOT abstracts the hardware differences by providing the same API for the same functionality across this large range of MCUs, projects building upon RIOT are highly portable and therefore resilient to changes in the supply chain.
	RIOT is designed to be a general-purpose OS with batteries included. It provides a large collection of in-tree modules and out-of-tree packages that seamlessly integrate in your application. This allows developers to pick the features they need from a large collection (as long as they can fit on the MCU).
	RIOT aims to be easy to learn by using sane defaults, by providing good documentation, and via its helpful community that happily answers questions [in the forum](https://forum.riot-os.org/) or in the [matrix chat](https://matrix.to/#/#riot-os:matrix.org). However, RIOT does not sacrifice advanced features, productivity or the ability to tinker with settings for more simplicity. This makes RIOT suitable for students in teaching, tinkerers in the DIY community, and professionals alike.
	RIOT is developed by a diverse, open, and [self-governed](https://doc.riot-os.org/community-processes.html) community. Members in the community mostly belong to one (or more) of the following groups: academia, industry, and makers/hobbyists.
	RIOT is distributed under a copyleft license and strongly prefers free and open source components over proprietary code and binary blobs. Still, RIOT does contain proprietary drivers (some even using binary blobs) where no free alternative is available, e.g. for the ESP WiFi chipset. See also [“Why LGPL?”](https://www.riot-os.org/#faq-why-lgpl)
	##### Vendor Specific SDKs
	Most MCU vendors provide an SDK that is tied to and only supports MCUs of that specific vendor. The advantage of the vendor SDKs is that they are developed in lock-step with the hardware and expose all features of the hardware early on. The RIOT community can only start working on drivers once the MCUs are generally available and more exotic features that are only relevant to niche use cases may never be supported in favor of a cleaner and more portable API in RIOT.
	From a governance point of view, RIOT is developed by a self-governed community, while the vendor SDKs are under tight control of the vendor. Because of that, the RIOT community has maintained many popular boards well after the vendors declared them obsolete, while vendor SDKs often phase out support for older MCUs sooner.
	Vendor specific SDKs typically do not have any copyleft clauses.
	##### Arduino
	Both RIOT and [Arduino](https://www.arduino.cc/) have a strong focus on a gentle learning curve and a low entry barrier. Arduino however goes a step further and sacrifices advanced features such as native multi-threading, a full-fledged and mature network stack, or a VFS subsystem for simplicity. This combined with a trimmed-down IDE results in a lower entry barrier for Arduino compared to RIOT.
	RIOT still allows new users to quickly get productive, but without limiting developers to specific design patterns, specific software architectures, and a strong tie to a specific IDE. As a nice treat for users that started with Arduino but ran into limitations, our [Arduino compatibility layer](https://doc.riot-os.org/group__sys__arduino.html) allows re-using sketches and libraries from the Arduino world.
	Arduino has a vast ecosystem of libraries developed independently by third parties. The number of modules and packages shipped with RIOT is smaller, but they are seamlessly integrated, provide a consistent API and combine well with each other. This results in easier reuse of code and higher productivity without having to worry about interoperability issues of components and “impedance matching” between misaligned APIs.
	The Arduino software is released under a copyleft license and hardware support can be extended greatly beyond the official Arduino boards by using third-party Arduino cores. The development of the ecosystem is sponsored and controlled by a single company that owns the registered trademark of Arduino, while with RIOT an [independent community](https://doc.riot-os.org/community-processes.html) is responsible for governance.
	##### Zephyr
	[Zephyr](https://www.zephyrproject.org/) has a larger and more complex code base, a very sophisticated configuration system, and unique tooling and is backed by a larger community than RIOT. This results in a larger feature set at the expense of a steeper learning curve.
	RIOT’s leaner code base makes the code easier to understand and results in a lower memory footprint. In addition, RIOT has been ported to 8-bit and 16-bit platforms, allowing its use on MCUs that are too resource constrained to run Zephyr.
	Zephyr’s larger code base and development community does give Zephyr an edge when it comes to the number of features supported. We do believe that RIOT has an edge over Zephyr when a gentle learning curve, memory consumption, or quick prototyping cycles are priorities.
	Zephyr uses a permissive license and is developed by the Linux Foundation. Its development is governed by a [technical steering committee](https://www.zephyrproject.org/wp-content/uploads/sites/38/2020/09/CLEAN-LF-Zephyr-Charter-20200624-effective-20200901.pdf) elected from (paying) members, whereas RIOT is steered by a [self-governed community](https://doc.riot-os.org/community-processes.html).
	##### FreeRTOS / FreeRTOS for AWS IoT
	[FreeRTOS](https://www.freertos.org/) focuses on the basic core-OS features such as a scheduler and a small set of libraries. This clear focus resulted in FreeRTOS being ported to more platforms than RIOT, despite its smaller development community.
	RIOT on the other hand packs a lot more features as seamlessly integrated as modules and packages. The ability to quickly enable and build upon these features reduces the development time needed for a certain application.
	[FreeRTOS for AWS IoT](https://www.freertos.org/iot-libraries.html) provides libraries that ease the use of cloud APIs offered by a certain service provider from microcontrollers. RIOT on the other hand is open minded about the network architecture and enables applications developers to choose freely: RIOT can communicate with centralized cloud services (without any preference on the service provider), use a centralized on-premise architecture, use decentralized machine-to-machine communication, or operate offline.
	FreeROTS and FreeRTOS for AWS IoT are both developed by Amazon Web Services, Inc. under a permissive license.
	##### Contiki-NG
	[Contiki-NG](https://www.contiki-ng.org/) has a smaller development community and a small and focused code base. It has a strong focus on research, whereas RIOT intents to be a general-purpose OS. A unique feature of Contiki-NG is the Cooja Network Simulator. RIOT provides similar simulation features with the [ZEP packet dispatcher](https://github.com/RIOT-OS/RIOT/tree/master/dist/tools/zep_dispatch), but clearly Cooja is a more tightly integrated and polished experience. Another aspect where Contiki-NG’s focus on research manifests is that Contiki-NG only supports a small number of boards, while having a quite sophisticated network stack.
	As a result of the larger and more active community, RIOT packs more features, has a faster development pace, supports more MCU families, and has been ported to far more boards. While Contiki-NG’s network simulator and small code base make it a strong competitor to RIOT in the domain of research, RIOT has a clear edge over Contiki-NG when it comes to the hardware support and the features required for many real world applications.
	Contiki-NG’s development is steered by a small group of (mostly) computer science researchers and it is distributed under a permissive license.
- I want to contribute to this website. How do I do that?
	This website is hosted using Jekyll, so you can add your contributions to the [GitHub repository for the website](https://github.com/RIOT-OS/riot-os.org).
- I want to cite RIOT. Which reference should I use?
	Please consider the following references for citation.
	- Emmanuel Baccelli, Cenk Gündoğan, Oliver Hahm, Peter Kietzmann, Martine Lenders, Hauke Petersen, Kaspar Schleiser, Thomas C. Schmidt, Matthias Wählisch, [RIOT: An Open Source Operating System for Low-End Embedded Devices in the IoT](https://www.riot-os.org/assets/pdfs/riot-ieeeiotjournal-2018.pdf), IEEE Internet of Things Journal, Vol. 5, No. 6, pp. 4428-4440, December 2018.