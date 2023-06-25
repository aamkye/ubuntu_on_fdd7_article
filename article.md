# HomeLab: How DevOps manage information and maintain high availability of the home infrastructure

Get to know how DevOps compute, stores, preserves, presents, and plays with information and data but also maintains high availability of the home infrastructure using corporation-grade software and hardware

## Introduction (Tale)

Once upon a time, back in the Stone Age of my childhood, I possessed a PC that was considered the bee's knees, at least in those ancient times. It boasted a whopping 80 gigabytes of hard disk space, an almighty Intel Core 2 Duo, and a mind-blowing 2 gigabytes of RAM. Oh, the joy it brought me! I could frolic in the virtual realms of games, bask in the glow of movies, groove to my favorite tunes, and conquer the daunting realm of homework.

But alas, this blissful existence was not meant to last. After a few months, I stumbled upon the mystical realm of the Internet—P2P, Linux, and all that jazz. As fate would have it, my music library started multiplying faster than gremlins in a swimming pool. It dawned on me that I desperately needed more space. Ah, the dark ages of hard disk scarcity, when they cost a fortune! I was left with no choice but to embark on a ruthless mission of deletion.

Fast forward to the present day, where I now possess a bookshelf adorned with BluRays, a vast collection of CDs, an arsenal of PS2 games, and more books than a library. As a self-proclaimed DevOps maestro and "data enthusiast," I felt obligated to digitize and preserve all these treasures for future generations—especially my own spawn. I have a sneaking suspicion that my kids will go bonkers for those ancient PS2 games.

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

\- "Behold my Raspberry Pi army, united in a glorious cluster. But how do I bestow upon them the gift of storage?"

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

My journey began with a straightforward upgrade from a 250GB HDD to a WD MyBook 1TB hard drive. However, it quickly became apparent that the storage space was still insufficient. In search of a solution, I stumbled upon two valuable resources: r/DataHoarder and r/HomeLab. After immersing myself in countless articles and delving into the subreddits' Wiki pages, I gained the necessary knowledge.

My initial choice was the WD PR4100, a relatively straightforward option. I equipped it with four 4TB WD RED HDDs and configured it in a JBOD setup. However, my further research on those subreddits revealed that this setup lacked redundancy protections. To address this, I educated myself on RAID levels and the distinctions between hardware and software RAIDs. This led me to the ZFS project—a software RAID solution. Initially, it seemed impossible to install ZFS without modifying the hardware. To seek answers, I turned to the WD forums and discovered an alternative—installing a different OS than WD CloudOS. I opted for Ubuntu Server and, after a few days of working with Ansible and KVM, achieved success:

![](./pic/image7.png)

But the story didn't end there. Although I managed to install ZFS on Ubuntu Server, I couldn't use it as a boot drive. Consequently, I had to install it on a USB drive. Unfortunately, this decision proved to be a significant mistake as the USB drive became corrupted after a few months, rendering my NAS unbootable. Thankfully, I had automated the reinstallation process using Ansible.

Next, I explored the possibility of installing a lightweight variation of Kubernetes called K3s on my NAS. While the installation was successful, K3s immediately consumed a significant portion of the CPU time (80%) and RAM (90%). Considering the NAS had only 4GB of RAM, an Intel Pentium N3710 processor, and the OS running from a USB drive, I had to abandon this idea. However, my pursuit continued, and after further research, I came across the concept of a "small business NAS" from HPE — the HPE ProLiant MicroServer Gen10.

![](./pic/image9.png)

It proved to be an ideal solution for my requirements, offering four 3.5" HDD bays, one 2.5" SSD bay (sold separately), 8GB of RAM, and an AMD Opteron X3216 processor. I purchased it second-hand, installed Ubuntu Server, and began migrating my data from the WD PR4100 by gradually replacing the disks. The end result was this tower configuration:

![](./pic/image10.jpeg)

However, I soon realized that the 8GB of RAM was not sufficient to run any workloads on the Kubernetes (K8s) cluster, such as Prometheus, Grafana, and others. Therefore, an additional upgrade was necessary to meet my requirements.

![](./pic/image11.gif)

## My current HomeLab

Now without (reasonable) compromises.

![](./pic/image12.png)

## Hardware at my HomeLab

![](./pic/image13.jpeg)

![](./pic/image14.jpeg)

![](./pic/image15.jpeg)

![](./pic/image16.jpeg)

![](./pic/image17.png)

![](./pic/image18.jpeg)

![](./pic/image19.jpeg)

![](./pic/image20.jpeg)

![](./pic/image21.png)

![](./pic/image22.jpeg)

## Motives

![](./pic/image23.png)

## Documentation at my HomeLab

## Networking at my HomeLab

## Host Operating System at my HomeLab

## VM & K8s software at my HomeLab

## Monitoring at my HomeLab

## Weather at my HomeLab

## Costs at my HomeLab

## It's never enough
