# HomeLab: How DevOps manage information and maintain high availability of the home infrastructure

Get to know how DevOps compute, stores, preserves, presents, and plays with information and data but also maintains high availability of the home infrastructure using corporation-grade software and hardware

## Introduction (Tale)

Once upon a time, back in the Stone Age of my childhood, I possessed a PC that was considered the bee's knees, at least in those ancient times. It boasted a whopping 80 gigabytes of hard disk space, an almighty Intel Core 2 Duo, and a mind-blowing 2 gigabytes of RAM. Oh, the joy it brought me! I could frolic in the virtual realms of games, bask in the glow of movies, groove to my favorite tunes, and conquer the daunting realm of homework.

But alas, this blissful existence was not meant to last. After a few months, I stumbled upon the mystical realm of the Internet—P2P, Linux, and all that jazz. As fate would have it, my music library started multiplying faster than gremlins in a swimming pool. It dawned on me that I desperately needed more space. Ah, the dark ages of hard disk scarcity, when they cost a fortune! I was left with no choice but to embark on a ruthless mission of deletion.

Fast forward to the present day, where I now possess a bookshelf adorned with BluRays, a vast collection of CDs, an arsenal of PS2 games, and more books than a library. As a self-proclaimed DevOps maestro and "data enthusiast, " I felt obligated to digitize and preserve all these treasures for future generations — especially my own spawn. I have a sneaking suspicion that my kids will go bonkers for those ancient PS2 games.

And lo and behold, after two decades of technological advancement, I no longer suffer from the "not enough space" syndrome. Behold, my private HomeLab/NAS/Archive.org hybrid, lovingly crafted to house my hoard of goodies. It may not be the size of a small planet, but its humble 96 terabytes of raw space (considered puny by today's standards) somehow manages to accommodate my vast collection.

But enough reminiscing, let us venture back to where it all began, where my tale unfolds like a nostalgic Windows 95 screensaver.

## Tales of HomeLabs and the Adventures of their Owners (as I see it)

### The First Step of the Journey

Every self-proclaimed "data enthusiast" embarks on their grand adventure with a humble image and a relatable comment:

![](./pic/image1.png)

\- "Look at this chaos! External disks are scattered everywhere. I must gather all this storage into one central haven."

### The Second Start of Progress

For those who venture further into the realm of HomeLabs, especially the tech-savvy bunch, their journey takes a different turn:

![](./pic/image2.jpeg)

\- "Behold my Raspberry Pi-like army, united in a glorious cluster. But how do I bestow upon them the gift of storage?"

### The "JBOA - Just Bunch of Everything" Interlude

Merge the previous images, and witness the birth of a typical Reddit-esque HomeLab, providing solutions to 90% of their troubles:

![](./pic/image3.png)

\- "See here! Raspberry Pi, NAS devices, external disks, old PCs, and old laptops, all are linked together by the almighty TrueNAS-ish software. My storage now thrives under a unified SMB share. It's a triumph!"

### "The Dawn of the Small Rack"

Yet, in this tale, a crucial question arises: "Is this enough for me?" Alas, the answer tends to be a resounding "no." Thus begins the true HomeLab, where enthusiasts acquire old (and sometimes new) server relics, and wield their magical powers:

![](./pic/image4.jpeg)

\- "This shall suffice! Let the enchantment begin!"

### The Era of the Grand Rack (The Final HomeLab Stage)

However, as time marches on, their HomeLab transforms into a behemoth, and desperate pleas echo through the halls of Reddit:

![](./pic/image5.jpg)

\- "How do I escape this labyrinth? My HomeLab has consumed all available space. I must find a larger abode!"

## History of my HomeLabs

For now, end of the tale. Let's face facts and real examples of history.

My journey began with a straightforward upgrade from a 250GB HDD to a WD MyBook 1 TB hard drive. However, it quickly became apparent that the storage space was still insufficient. In search of a solution, I stumbled upon two valuable resources: r/DataHoarder and r/HomeLab. After immersing myself in countless articles and delving into the subreddits' Wiki pages, I gained the necessary knowledge.

My initial choice was the WD PR4100, a relatively straightforward option. I equipped it with four 4 TB WD RED HDDs and configured it in a JBOD setup. However, my further research on those subreddits revealed that this setup lacked redundancy protections. To address this, I educated myself on RAID levels and the distinctions between hardware and software RAIDs. This led me to the ZFS project—a software RAID solution. Initially, it seemed impossible to install ZFS without modifying the hardware. To seek answers, I turned to the WD forums and discovered an alternative—installing a different OS than WD CloudOS. I opted for Ubuntu Server and, after a few days of working with Ansible and KVM, achieved success:

![](./pic/image7.jpeg)

But the story didn't end there. Although I managed to install ZFS on Ubuntu Server, I couldn't use it as a boot drive. Consequently, I had to install it on a USB drive. Unfortunately, this decision proved to be a significant mistake as the USB drive became corrupted after a few months, rendering my NAS unbootable. Thankfully, I had automated the reinstallation process using Ansible.

Next, I explored the possibility of installing a lightweight variation of Kubernetes called K3s on my NAS. While the installation was successful, K3s immediately consumed a significant portion of the CPU time (80%) and RAM (90%). Considering the NAS had only 4GB of RAM, an Intel Pentium N3710 processor, and the OS running from a USB drive, I had to abandon this idea. However, my pursuit continued, and after further research, I came across the concept of a "small business NAS" from HPE — the HPE ProLiant MicroServer Gen10.

![](./pic/image9.jpeg)

It proved to be an ideal solution for my requirements, offering four 3.5" HDD bays, one 2.5" SSD bay (sold separately), 8GB of RAM, and an AMD Opteron X3216 processor. I purchased it second-hand, installed Ubuntu Server, and began migrating my data from the WD PR4100 by gradually replacing the disks. The end result was this tower configuration:

![](./pic/image10.jpeg)

However, I soon realized that the 8GB of RAM was not sufficient to run any workloads on the Kubernetes (K8s) cluster, such as Prometheus, Grafana, and others. Therefore, an additional upgrade was necessary to meet my requirements.

![](./pic/image11.gif)

## My current HomeLab

Now without (reasonable) compromises.

After months of research, comparing hardware, counting my savings, and taking a small inspiration from [here](https://www.youtube.com/watch?v=FAy9N1vX76o), I've finally decided to build this monster:

![](./pic/image12.png)

## Hardware at my HomeLab

Fractal Design Define 7 XL is a big case, and a big case means lots of space, and a lot of space needs a lot of pressure to move air through so my choice here was 8x 120mm and 1x 140mm Be Quiet! Silent Wings Pro 4 PWM fans:

![](./pic/image13.jpeg)

Such a big case allows the installation of a big motherboard, so I've chosen Asus X99-E WS. And a powerful motherboard requires a powerful CPU, here with a whooping 44t - Intel Xeon E5-2699v4. And not to stand out the CPU, the RAM banks have been filled with 8x32GB (256GB) DDR4 ECC RAM:

![](./pic/image15.jpeg)

A powerful CPU requires powerful cooling, so I've chosen BeQuiet DarkRock Pro 4. And for additional codecs workloads - Radeon WX 7100:

![](./pic/image16.jpeg)

A lot of desired storage requires a lot of SATA ports, so I've chosen LSI 9400-16i HBA card with 4x SFF-8643 ports:

![](./pic/image17.png)

And a lot of SATA ports require a lot of cables, so I've chosen 4x SFF-8643 to SATA3 cables

![](./pic/image18.jpeg)

This storage needs to be mounted somewhere, so I've chosen 16x Fractal Design HDD trays. And finally storage itself: 4x WD Red 4TB and 4x WD Ultrastar HC550 16TB HDDs:

![](./pic/image20.jpeg)

But HDDs are slow on their own, I had to speed them up with 2x QNAP QM2-4P-384 M.2 NVMe SSD PCIe cards and 8x WD SN700 4TB NVMe SSDs:

![](./pic/image22.jpeg)

And finally, all this hardware requires a lot of power, so I've chosen BeQuiet Dark Power Pro 12 1500W PSU.

We add all together, do some cable management, and _voilà_.

## Motives

Size:

```
zpool list
NAME       SIZE  ALLOC   FREE  CKPOINT  EXPANDSZ   FRAG    CAP  DEDUP    HEALTH
cheetah   7.27T   825G  6.46T        -         -     0%    11%  1.00x    ONLINE
elephant  58.2T  14.6T  43.6T        -         -     0%    25%  1.00x    ONLINE
tortoise  14.5T   855G  13.7T        -         -    14%     5%  1.00x    ONLINE
```

Reliability:

```
zpool status
  pool: cheetah
 state: ONLINE
config:

        NAME                                       STATE     READ WRITE CKSUM
        cheetah                                    ONLINE       0     0     0
          raidz1-0                                 ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800274  ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800291  ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800133  ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800267  ONLINE       0     0     0

errors: No known data errors

  pool: elephant
 state: ONLINE
config:

        NAME                                       STATE     READ WRITE CKSUM
        elephant                                   ONLINE       0     0     0
          raidz1-0                                 ONLINE       0     0     0
            scsi-SATA_WDC_WUH721816AL_2BKW62BT     ONLINE       0     0     0
            scsi-SATA_WDC_WUH721816AL_2BKZBNDT     ONLINE       0     0     0
            scsi-SATA_WDC_WUH721816AL_2PJ0LDMT     ONLINE       0     0     0
            scsi-SATA_WDC_WUH721816AL_4YGA3LWH     ONLINE       0     0     0
        logs
          mirror-1                                 ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800200  ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800835  ONLINE       0     0     0

errors: No known data errors

  pool: tortoise
 state: ONLINE
config:

        NAME                                       STATE     READ WRITE CKSUM
        tortoise                                   ONLINE       0     0     0
          raidz1-0                                 ONLINE       0     0     0
            scsi-SATA_WDC_WD4003FFBX-6_V1J8JJBG    ONLINE       0     0     0
            scsi-SATA_WDC_WD4003FFBX-6_V1JAPH9G    ONLINE       0     0     0
            scsi-SATA_WDC_WD4003FFBX-6_V1JASWGG    ONLINE       0     0     0
            scsi-SATA_WDC_WD4003FFBX-6_VBGJN8SF    ONLINE       0     0     0
        logs
          mirror-1                                 ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800705  ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800272  ONLINE       0     0     0

errors: No known data errors
```

Speed:

```
...
PS2/Games/Age Of Empires 2.iso
    634,811,856 100% 321.85MB/s     0:00:01 (xfr#33, ir-chk-2720/2780)
PS2/Games/Crash Nitro Kart.iso
  3,164,798,976 100% 468.01MB/s     0:00:06 (fr#34, ir-chk-2719/2780)
PS2/Games/Deus Ex - The Conspiracy.iso
  1,383,399,424 100% 357.15MB/s     0:00:03 (×fr#35, ir-chk-2718/2780)
PS2/Games/Devil May Cry 2 Dante. iso
  4,698,767,360 100% 471.99MB/s     0:00:09 (xfr#36, ir-chk=2717/2780)
PS2/Games/Devil May Cry 2 Lucia.iso
  4,698,767,360 100% 482.67MB/s     0:00:09 (xfr#37, ir-chk=2716/2780)
PS2/Games/Devil May Cry 3 Special Edition.iso
  4,499,308,544 100% 427.42MB/s     0:00:10 (xfr#38, ir-chk-2715/2780)
PS2/Games/Devil May Cry.iso
  1,246,822,400  26% 594.83MB/s     0:00:05
...
```

Benchmark results:

```
# Small, medium, and large files (4k/1m/32m) on sequential and random read/write
> fio \
  --direct=1 \
  --rw=[write|read|randwrite|randread] \
  --bs=[4k|1m|32m] \
  --iodepth=1 \
  --runtime=120 \
  --numjobs=1 \
  --time_based \
  --group_reporting \
  --name=iops-speed-test-job \
  --size=1g
```

| ZFS Pool Name | Test Type   | BS    | Speed (avg)     | IOPS (avg)  |
| ------------- | ----------- | ----- | --------------- | ----------- |
| Cheetah       | write       | 4k    | 358.90 MiB/s    | 89.72K      |
| Cheetah       | write       | 1m    | 3.65 GiB/s      | 3655        |
| Cheetah       | write       | 32m   | 2.75 GiB/s      | 85          |
| Cheetah       | randwrite   | 4k    | 350.21 MiB/s    | 58.54K      |
| Cheetah       | randwrite   | 1m    | 3.62 GiB/s      | 3626        |
| Cheetah       | randwrite   | 32m   | 2.85 GiB/s      | 89          |
| Cheetah       | read        | 4k    | 734.14 MiB/s    | 183.53K     |
| Cheetah       | read        | 1m    | 5.46 GiB/s      | 5.46K       |
| Cheetah       | read        | 32m   | 4.54 GiB/s      | 142         |
| Cheetah       | randread    | 4k    | 592.61 MiB/s    | 148.15K     |
| Cheetah       | randread    | 1m    | 5.18 GiB/s      | 5.18K       |
| Cheetah       | randread    | 32m   | 4.57 GiB/s      | 143         |
| ------------- | ----------- | ----- | --------------- | ----------- |
| Elephant      | write       | 4k    | 335.33 MiB/s    | 83.83K      |
| Elephant      | write       | 1m    | 754.25 MiB/s    | 736         |
| Elephant      | write       | 32m   | 671.65 MiB/s    | 20          |
| Elephant      | randwrite   | 4k    | 302.10 MiB/s    | 75.52K      |
| Elephant      | randwrite   | 1m    | 571.56 MiB/s    | 558         |
| Elephant      | randwrite   | 32m   | 745.84 MiB/s    | 22          |
| Elephant      | read        | 4k    | 718.03 MiB/s    | 179.50K     |
| Elephant      | read        | 1m    | 5.40 GiB/s      | 5400        |
| Elephant      | read        | 32m   | 4.56 GiB/s      | 142         |
| Elephant      | randread    | 4k    | 596.53 MiB/s    | 149.13K     |
| Elephant      | randread    | 1m    | 5.13 GiB/s      | 5133        |
| Elephant      | randread    | 32m   | 4.47 GiB/s      | 139         |
| ------------- | ----------- | ----- | --------------- | ----------- |
| Tortoise      | write       | 4k    | 243.74 MiB/s    | 60.93K      |
| Tortoise      | write       | 1m    | 452.69 MiB/s    | 442         |
| Tortoise      | write       | 32m   | 509.24 MiB/s    | 15          |
| Tortoise      | randwrite   | 4k    | 224.53 MiB/s    | 56.13K      |
| Tortoise      | randwrite   | 1m    | 475.20 MiB/s    | 464         |
| Tortoise      | randwrite   | 32m   | 581.77 MiB/s    | 17          |
| Tortoise      | read        | 4k    | 731.10 MiB/s    | 182.77K     |
| Tortoise      | read        | 1m    | 5.15 GiB/s      | 5151        |
| Tortoise      | read        | 32m   | 4.53 GiB/s      | 141         |
| Tortoise      | randread    | 4k    | 570.39 MiB/s    | 142.59K     |
| Tortoise      | randread    | 1m    | 5.14 GiB/s      | 5145        |
| Tortoise      | randread    | 32m   | 4.56 GiB/s      | 142         |

_Two more things:_

ZFS LOG Cache on write (pay attention to the `w=...` values):

```
> fio \
  --direct=1 \
  --rw=write \
  --bs=32m \
  --iodepth=1 \
  --runtime=120 \
  --numjobs=1 \
  --time_based \
  --group_reporting \
  --name=iops-speed-test-job \
  --size=1g \
  --eta-newline=5

iops-speed-test-job: (g=0): rw=write, bs=(R) 32.0MiB-32.0MiB, (W) 32.0MiB-32.0MiB, (T) 32.0MiB-32.0MiB, ioengine=psync, iodepth=1
fio-3.33
Starting 1 process
Jobs: 1 (f=1): [W(1)][6.6%][w=2430MiB/s][w=75 IOPS][eta 01m:53s]
Jobs: 1 (f=1): [W(1)][11.6%][w=2723MiB/s][w=85 IOPS][eta 01m:47s]
Jobs: 1 (f=1): [W(1)][16.5%][w=256MiB/s][w=8 IOPS][eta 01m:41s]
Jobs: 1 (f=1): [W(1)][21.5%][w=96.0MiB/s][w=3 IOPS][eta 01m:35s]
Jobs: 1 (f=1): [W(1)][26.7%][w=64.0MiB/s][w=2 IOPS][eta 01m:28s]
Jobs: 1 (f=1): [W(1)][31.4%][w=32.0MiB/s][w=1 IOPS][eta 01m:23s]
Jobs: 1 (f=1): [W(1)][36.4%][w=32.0MiB/s][w=1 IOPS][eta 01m:17s]
Jobs: 1 (f=1): [W(1)][41.3%][w=512MiB/s][w=16 IOPS][eta 01m:11s]
Jobs: 1 (f=1): [W(1)][46.3%][w=256MiB/s][w=8 IOPS][eta 01m:05s]
Jobs: 1 (f=1): [W(1)][51.2%][w=96.1MiB/s][w=3 IOPS][eta 00m:59s]
Jobs: 1 (f=1): [W(1)][56.2%][w=64.1MiB/s][w=2 IOPS][eta 00m:53s]
Jobs: 1 (f=1): [W(1)][61.2%][w=833MiB/s][w=26 IOPS][eta 00m:47s]
Jobs: 1 (f=1): [W(1)][66.1%][w=160MiB/s][w=5 IOPS][eta 00m:41s]
Jobs: 1 (f=1): [W(1)][71.1%][w=64.0MiB/s][w=2 IOPS][eta 00m:35s]
Jobs: 1 (f=1): [W(1)][76.0%][w=128MiB/s][w=4 IOPS][eta 00m:29s]
Jobs: 1 (f=1): [W(1)][81.0%][w=64.1MiB/s][w=2 IOPS][eta 00m:23s]
Jobs: 1 (f=1): [W(1)][86.0%][w=32.0MiB/s][w=1 IOPS][eta 00m:17s]
Jobs: 1 (f=1): [W(1)][90.9%][w=2208MiB/s][w=69 IOPS][eta 00m:11s]
Jobs: 1 (f=1): [W(1)][95.9%][w=1568MiB/s][w=49 IOPS][eta 00m:05s]
Jobs: 1 (f=1): [W(1)][100.0%][w=2498MiB/s][w=78 IOPS][eta 00m:00s]
iops-speed-test-job: (groupid=0, jobs=1): err= 0: pid=933058:
  write: IOPS=13, BW=439MiB/s (461MB/s)(51.5GiB/120002msec); 0 zone resets
    clat (msec): min=8, max=2301, avg=71.66, stdev=162.35
     lat (msec): min=9, max=2303, avg=72.85, stdev=162.40
    clat percentiles (msec):
     |  1.00th=[    9],  5.00th=[    9], 10.00th=[   10], 20.00th=[   10],
     | 30.00th=[   11], 40.00th=[   11], 50.00th=[   16], 60.00th=[   21],
     | 70.00th=[   56], 80.00th=[   80], 90.00th=[  155], 95.00th=[  330],
     | 99.00th=[  793], 99.50th=[ 1099], 99.90th=[ 1938], 99.95th=[ 2299],
     | 99.99th=[ 2299]
   bw (  KiB/s): min=65536, max=3276800, per=100.00%, avg=509240.77, stdev=757052.72, samples=208
   iops        : min=    2, max=  100, avg=15.53, stdev=23.09, samples=208
  lat (msec)   : 10=27.44%, 20=32.54%, 50=6.80%, 100=18.34%, 250=7.95%
  lat (msec)   : 500=4.37%, 750=1.46%, 1000=0.43%, 2000=0.61%, >=2000=0.06%
  cpu          : usr=1.77%, sys=17.57%, ctx=164430, majf=0, minf=10
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1647,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
  WRITE: bw=439MiB/s (461MB/s), 439MiB/s-439MiB/s (461MB/s-461MB/s), io=51.5GiB (55.3GB), run=120002-120002msec
```

ZFS ARC Cache on read (pay attention to the `r=...` values):

```
# Large file (128m) on random read
> fio \
  --direct=1 \
  --rw=randread \
  --bs=128m \
  --iodepth=1 \
  --runtime=120 \
  --numjobs=8 \
  --time_based \
  --group_reporting \
  --name=iops-speed-test-job \
  --size=1g \
  --eta-newline=5

iops-speed-test-job: (g=0): rw=randread, bs=(R) 128MiB-128MiB, (W) 128MiB-128MiB, (T) 128MiB-128MiB, ioengine=psync, iodepth=1
...
fio-3.33
Starting 8 processes
Jobs: 8 (f=8): [r(8)][5.8%][r=9728MiB/s][r=76 IOPS][eta 01m:54s]
Jobs: 8 (f=8): [r(8)][10.7%][r=9984MiB/s][r=78 IOPS][eta 01m:48s]
Jobs: 8 (f=8): [r(8)][15.7%][r=5766MiB/s][r=45 IOPS][eta 01m:42s]
Jobs: 8 (f=8): [r(8)][20.7%][r=6278MiB/s][r=49 IOPS][eta 01m:36s]
Jobs: 8 (f=8): [r(8)][25.6%][r=6278MiB/s][r=49 IOPS][eta 01m:30s]
Jobs: 8 (f=8): [r(8)][30.6%][r=6144MiB/s][r=48 IOPS][eta 01m:24s]
Jobs: 8 (f=8): [r(8)][35.5%][r=6663MiB/s][r=52 IOPS][eta 01m:18s]
Jobs: 8 (f=8): [r(8)][40.5%][r=6663MiB/s][r=52 IOPS][eta 01m:12s]
Jobs: 8 (f=8): [r(8)][45.5%][r=7560MiB/s][r=59 IOPS][eta 01m:06s]
Jobs: 8 (f=8): [r(8)][50.4%][r=9344MiB/s][r=73 IOPS][eta 01m:00s]
Jobs: 8 (f=8): [r(8)][55.8%][r=8832MiB/s][r=69 IOPS][eta 00m:53s]
Jobs: 8 (f=8): [r(8)][60.3%][r=9472MiB/s][r=74 IOPS][eta 00m:48s]
Jobs: 8 (f=8): [r(8)][65.3%][r=9600MiB/s][r=75 IOPS][eta 00m:42s]
Jobs: 8 (f=8): [r(8)][70.2%][r=9610MiB/s][r=75 IOPS][eta 00m:36s]
Jobs: 8 (f=8): [r(8)][75.2%][r=9481MiB/s][r=74 IOPS][eta 00m:30s]
Jobs: 8 (f=8): [r(8)][80.2%][r=9738MiB/s][r=76 IOPS][eta 00m:24s]
Jobs: 8 (f=8): [r(8)][85.1%][r=9856MiB/s][r=77 IOPS][eta 00m:18s]
Jobs: 8 (f=8): [r(8)][90.1%][r=10.0GiB/s][r=80 IOPS][eta 00m:12s]
Jobs: 8 (f=8): [r(8)][95.0%][r=10.3GiB/s][r=82 IOPS][eta 00m:06s]
Jobs: 8 (f=8): [r(8)][100.0%][r=10.0GiB/s][r=80 IOPS][eta 00m:00s]
iops-speed-test-job: (groupid=0, jobs=8): err= 0: pid=1182625: Mon Jun 26 13:44:18 2023
  read: IOPS=67, BW=8658MiB/s (9078MB/s)(1015GiB/120082msec)
    clat (msec): min=30, max=7698, avg=118.25, stdev=581.24
     lat (msec): min=30, max=7698, avg=118.25, stdev=581.24
    clat percentiles (msec):
     |  1.00th=[   32],  5.00th=[   33], 10.00th=[   36], 20.00th=[   41],
     | 30.00th=[   46], 40.00th=[   55], 50.00th=[   75], 60.00th=[   80],
     | 70.00th=[   83], 80.00th=[   87], 90.00th=[  100], 95.00th=[  102],
     | 99.00th=[  107], 99.50th=[ 6544], 99.90th=[ 6745], 99.95th=[ 7215],
     | 99.99th=[ 7684]
   bw (  MiB/s): min= 2048, max=21504, per=100.00%, avg=14738.69, stdev=642.94, samples=1122
   iops        : min=   16, max=  168, avg=114.65, stdev= 5.08, samples=1122
  lat (msec)   : 50=36.70%, 100=55.75%, 250=6.70%, 500=0.04%, 750=0.01%
  lat (msec)   : >=2000=0.80%
  cpu          : usr=0.02%, sys=99.28%, ctx=14764, majf=0, minf=262217
  IO depths    : 1=100.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=8122,0,0,0 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
   READ: bw=8658MiB/s (9078MB/s), 8658MiB/s-8658MiB/s (9078MB/s-9078MB/s), io=1015GiB (1090GB), run=120082-120082msec
```

Observability:

Being well-informed about the state of your system is critical to maintaining its health. So any information that can be gleaned from the system is valuable. The more observability you have, the better.

![](./pic/image27.jpeg)

Sustainability:

Imagine you're the captain of the Data Defender spaceship, soaring through the digital galaxy. Your crew of heroic disks stands united, ready to face any peril that comes their way. But alas! Amid your interstellar journey, disaster strikes! One of your loyal disks malfunctions and cries out, "Houston, we have a problem!"

Fear not, intrepid captain! The Data Defender is equipped with the legendary RAIDZ1, a shield of redundancy that will keep your data safe and sound. It's like having a team of cosmic superheroes at your command.

As soon as the distress signal is detected, your trusty crew leaps into action. They diligently diagnose the issue, like brilliant space engineers on a mission. Once they identify the culprit, it's time to bring in the reinforcements.

With the faulty disk replaced by a shiny new recruit, the resilvering process commences. It's like a cosmic restoration as if the universe itself is working its magic. Bit by bit, byte by byte, the missing data is reconstructed and woven back into the fabric of your digital universe.

The Data Defender crew works tirelessly, their laser-like focus ensuring that every precious fragment of information finds its rightful place. It's a celestial ballet of data, a symphony of technological wizardry.

And lo and behold, in the blink of an eye, your data is resurrected! It returns to its former glory, ready to continue its cosmic adventure. The crew celebrates this triumph, high-fiving and exchanging virtual fist bumps in zero gravity.

So, brave captain, fear not the cosmic glitches and digital hiccups. With RAIDZ1 guarding your data, even the mightiest of failures won't thwart your mission. The resilvering process is the elixir of restoration, bringing your precious information back from the brink.

Remember, in the vast expanse of the digital universe, RAIDZ1 shines as a beacon of resilience, ensuring that your data journey never comes to a premature end. Onward, intrepid explorer, with RAIDZ1 as your loyal companion!

```
> zpool status tortoise
  pool: tortoise
 state: DEGRADED
status: One or more devices is currently being resilvered. The pool will
        continue to function, possibly in a degraded state.
action: Wait for the resilver to complete.
  scan: resilver in progress since Sat May 6 08:42:29 2023
        7.51G scanned at 135M/s, 2.42G issued at 43.5M/s, 5.11T total
        598M resilvered, 0.05% done, 1 days 10:12:37 to go
config:
        NAME                                       STATE     READ WRITE CKSUM
        tortoise                                   DEGRADED     0     0     0
          raidz1-0                                 DEGRADED   498   572     0
            SCSi-SATA_NDC_ND4003FFBX-6_V138JJBG    DEGRADED   383   233     0
            Scsi-SATA_WDC_WD4003FFBX-6_V1JAPH9G    ONLINE     385   415     0
            SCSi-SATA_WDC_WD4003FFBX-6_V1JASWGG    ONLINE     472   271     0
            scsi-SATA_WDC_WD4003FFBX-6_VBGJN8SF    ONLINE     412   342     0
        logs
          mirror-1                                 ONLINE       0     0     0
            nume-WD_Red_SN700_2000GB_23024R800705  ONLINE       0     0     0
            nvme-WD_Red_SN700_2000GB_23024R800272  ONLINE       0     0     0
```

## Documentation at my HomeLab

In the context of this project, it is imperative to possess graphical documentation. Therefore, I have opted for the utilization of [draw.io](https://draw.io/) for this purpose.

![](./pic/image28.png)

Commencing from the selection of the provider, outbound connections, the establishment of a legend, depiction of data flows, network segregation, the configuration of the mesh, software functionalities, identification of unoccupied RJ45 slots, consideration of future software requirements, and specification of network hardware.

![](./pic/image29.png)

Additionally, it involves the creation of a connection diagram, representation of the docking station, specification of the server, specification of virtual machines (VMs) and Kubernetes (K8s) deployments, as well as the ZFS diagram illustrating the disk architecture.

These measures are crucial to ensure future reference and to prevent any confusion or loss of information.

## Networking at my HomeLab

Here, without a surprise, OpenWRT - maximum flexibility and control, minimum requirements.

![](./pic/image30.png)

AdBlock? Pfft, so yesterday! PiHole? Meh, too basic! AdGuard? Yawn, too mainstream! But network-wide ad blocking with OpenWRT? Oh heck yeah, sign me up for some Wi-Fi wizardry and ad annihilation!


The underlying principles are elegantly straightforward: maintain local DNS resolution while redirecting all non-local DNS queries to an external DNS resolver such as [NextDNS](https://nextdns.io). By employing this method, you can leverage your local DNS resolver while simultaneously reaping the benefits of network-wide ad blocking.

![](./pic/image31.png)

The conundrum of multiple Wi-Fi networks and signal dropout is a nuisance nobody relishes. To mitigate this predicament, I opted for a TP-Link mesh system featuring a unified SSID for both the 2.4GHz and 5GHz networks across three mesh devices. Consequently, I can freely wander throughout my abode without encountering any connectivity hindrances.

Now, as you might already spotted on the docs, here's the dealio, folks. The key to maintaining peace and harmony in the technological realm is to have not one, but two Wi-Fi networks. Oh yeah, we're living the high life now! The first one is exclusively for all those fancy-schmancy IoT devices, because, you know, they've got a party of their own going on. They're out there sharing cat memes and discussing the latest smart home gossip, while I'm just chilling on the sidelines.

But hold your horses, folks! We can't forget about the second network, designed especially for my dear wife. Why, you ask? Well, let me spill the beans. You see, I have a particular talent for accidentally breaking stuff. It's like my superpower or something. But fear not! With this second Wi-Fi network in place, my wife can still surf the web, browse her favorite websites, and watch adorable puppy videos, all while I'm over here causing havoc like a clumsy ninja.

In the end, my friends, it's all about preserving domestic tranquility in the face of technological mishaps. So, let's raise a glass to the two Wi-Fi networks because they're the real MVPs of our connected household. Cheers to endless internet for everyone, even when I'm on a rampage of destruction!

![](./pic/image32.png)

Ah, my personal favorite — VPN. Have you ever experienced the peculiar scenario of toiling away at a company for X years, while the esteemed security department assumes you're diligently working from country Y, only to be abruptly confronted with a malfunctioning VPN server that "teleports" you back to your original country, Z? The inevitable phone call from said security department ensues, bewildered by your sudden appearance in country Z. If you answered in the affirmative, rest assured, you're doing it right!

Every single device within my network must traverse the router, which boasts a meticulously configured VPN client. This meticulous setup guarantees that all my device traffic remains enciphered, safeguarding against any data leakage to the vast expanse of the Internet (well, at least until it reaches the VPN server, but that's a whole other story.)

![](./pic/image33.png)

## Host Operating System at my HomeLab

![](./pic/image35.png)

Once again, enter the stage with a drumroll — Proxmox! No surprises here, as this robust virtualization platform reigns supreme.

![](./pic/image36.png)

Ah, but hold your breath for the delightful surprise! In this setup, all the disks and GPU are magnificently passed through to the main VM, ushering in a virtualization extravaganza like no other. The power and potential of Proxmox coupled with this remarkable feature truly take the virtualization game to new heights!

![](./pic/image37.jpeg)

What is also worth mentioning - [cloudymax/pxeless](https://github.com/cloudymax/pxeless) - the automation tool for the ISO images to skillfully recraft them with a "pre-generated" seed file, housing essential information about virtual machines (VMs). This ingenious approach enables a seamless, automated installation process, rendering it entirely unattended.

## VM & K8s software at my HomeLab

Prepare yourself for an impressive ensemble of software that graces my HomeLab:

- [Ansible](https://github.com/ansible/ansible)
- [Cert-manager](https://github.com/cert-manager/cert-manager)
- [Deluge](https://github.com/deluge-torrent/deluge)
- [Grafana](https://github.com/grafana/grafana)
- [Helm](https://github.com/helm/helm)
- [Jellyfin](https://github.com/jellyfin/jellyfin)
- [K3s](https://github.com/k3s-io/k3s)
- [Kubernetes (K8s)](https://github.com/kubernetes/kubernetes)
- [Longhorn](https://github.com/longhorn/longhorn)
- [OpenZFS](https://github.com/openzfs/zfs)
- [Prometheus](https://github.com/prometheus/prometheus)
- [TimeMachine server](https://github.com/mbentley/docker-timemachine)
- [Ubuntu Server](https://ubuntu.com/)

## Monitoring at my HomeLab

As I already said: _"The more observability you have, the better"_.

Centralized hardware monitoring:

![](./pic/image51.png)

Centralized S.M.A.R.T. monitoring:

![](./pic/image52.png)

Centralized ZFS-usage monitoring:

![](./pic/image53.png)

## Weather at my HomeLab

Hold on to your socks, because I'm about to blow your mind! You know how we can keep an eye on our CPU temperature, right? Well, guess what? It turns out we can also tap into the mystical powers of weather monitoring! That's right, folks, I've got a full-fledged weather station right here in my HomeLab. I can predict rain, wind, and even the occasional sneeze from Mother Nature herself, all from the comfort of my high-tech haven. I've officially become the geeky weatherman of my own little tech kingdom!

![](./pic/image54.jpeg)

## Costs at my HomeLab

Ah, now let's delve into some vital details for all you tech-savvy individuals yearning to embark on a similar HomeLab endeavor - costs.

| Name                                | q.  | per ea.   | Cost PLN    | Cost USD  |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Stage1 (ok):                      |     |           | PLN 10.800  | $2.615    |
| Fractal DD7 XL                      | 1   | PLN 800   | PLN 800     | $194      |
| Asus X99-E WS                       | 1   | PLN 2.200 | PLN 2.200   | $533      |
| Xeon E5-2699v4                      | 1   | PLN 1.250 | PLN 1.250   | $303      |
| Radeon PRO WX7100                   | 1   | PLN 900   | PLN 900     | $218      |
| BeQuiet Dark Power Pro 12 1500W     | 1   | PLN 1.700 | PLN 1.700   | $412      |
| Hynix 32GB RDDIM DDR4               | 8   | PLN 275   | PLN 2.200   | $533      |
| BeQuiet Dark Rock Pro 4             | 1   | PLN 400   | PLN 400     | $97       |
| BeQuiet Silent Wings Pro 4 140MM    | 1   | PLN 150   | PLN 150     | $36       |
| BeQuiet Silent Wings Pro 4 120MM    | 8   | PLN 150   | PLN 1.200   | $291      |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Stage2 (ok):                      |     |           | PLN 4.600   | $1.114    |
| HBA LSI 9400-16i                    | 1   | PLN 2.400 | PLN 2.400   | $581      |
| Fractal FD-A-TRAY-002               | 16  | PLN 88    | PLN 1.400   | $339      |
| Fractal FD-A-CAGE-001               | 2   | PLN 400   | PLN 800     | $194      |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Stage3.1 (ok):                    |     |           | PLN 6.325   | $1.532    |
| QM2-4P-384                          | 1   | PLN 683   | PLN 683     | $165      |
| WD RED SN700 2TB                    | 4   | PLN 764   | PLN 3.057   | $740      |
| WD Ultrastar 16TB                   | 2   | PLN 1.293 | PLN 2.585   | $626      |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Stage3.2 (ok):                    |     |           | PLN 6.325   | $1.532    |
| QM2-4P-384                          | 1   | PLN 683   | PLN 683     | $165      |
| WD RED SN700 2 TB                    | 4   | PLN 764   | PLN 3.057   | $740      |
| WD Ultrastar 16 TB                   | 2   | PLN 1.293 | PLN 2.585   | $626      |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Stage4.0 (in-progress)            |     |           | PLN 10.341  | $2.504    |
| WD Ultrastar 16 TB                   | 8   | PLN 1.293 | PLN 10.341  | $2.504    |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Perfs (ok):                       |     |           | PLN 578     | $140      |
| Thermal Paste                       | 1   | PLN 100   | PLN 100     | $24       |
| PWM cable extenders                 | 4   | PLN 23    | PLN 90      | $22       |
| Sata power 1-to-2 extender          | 4   | PLN 30    | PLN 120     | $29       |
| RJ45 CAT6a                          | 1   | PLN 88    | PLN 88      | $21       |
| SFF-8643 to 4xSata                  | 4   | PLN 45    | PLN 180     | $44       |
| ----------------------------------- | --- | --------- | ----------- | --------- |
|   Total total (w/o Stage4.0)        |     |           | PLN 28.628  | $6.932    |

Ah, indeed, we cannot overlook the power consumption of such a magnificent beast!

![](./pic/image57.png)

## It's never enough...

However, to be perfectly honest, the achievements I have accomplished are truly remarkable, and the knowledge I have acquired throughout this process is commendable. I take immense pride in my accomplishments thus far. Nonetheless, I am cognizant of the fact that there is always room for improvement and continuous growth. Consequently, I have already begun contemplating the subsequent phases or endeavors that lie ahead, as I perpetually strive to expand my horizons and advance further in my journey.

![](./pic/image58.png)
