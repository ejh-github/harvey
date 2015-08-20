# News & events

<a name="debugging-harvey-gdb"></a>
## Using gdb to debug Harvey
August 8, 2015

A page has been added to the wiki which describes how to debug Harvey using gdb.  See [Debugging Harvey in gdb](https://github.com/Harvey-OS/harvey/wiki/Debugging-Harvey-in-gdb) for details.

---

<a name="ape-is-ready"></a>
## APE is ready
August 6, 2015

APE (the [ANSI/POSIX Environment](http://plan9.bell-labs.com/sys/doc/ape.html)) has been finally given the green light:

>ANSI people, it's your time. Let's go, doors are opened. Ape is working.
>Improvements, suggestions are welcome. Ports can be done. Wiki is ready in github.

This means a whole host of ports can be on their way fueled by POSIX -sort of- compliance:

>  There are some aspects of required POSIX behavior that are impossible or very hard to simulate in Plan 9.
>  Experience has shown, however, that the simulation is adequate for the vast majority of programs.

A quick [getting started with APE](https://github.com/Harvey-OS/ape/wiki/Getting-Started) guide is being drafted in the wiki.

---

<a name="broken-scheduler"></a>
## Broken scheduler, working scheduler
August 1, 2015	

Despite the hot summer, Harvey has been progressing steadily during these months. So, a big THANK YOU to everyone involved, you all rock!

Obviously, it can't all be happy days: resident guru Aki Nyrhinen has just proved how things can easily fall into chaos by detecting a major defect in Harvey's core. Straight from the horse's mouth:

>it turns out that the scheduler in harvey is badly broken.
>it does not do time sharing at all, among other things.
>it also crashes instantly if squidboy is enabled (>1 core).
>the procs aren't really reusable at all, because the kernel structures are apparently infested with pointers to the procs when one does an exit.
>there's a lot to be fixed here.

Undeterred by the mess, and in a question of hours, the fire has been put out:

>Alright, after 4 hours of furious editing and undoing damage to the boot code, I've got harvey booting up with the ndnr() in squidboy commented out.

Some (thorough?) measurements after the fix:

>Boot faster.
>CPU at 13% as usual (we still have pending a new random).
>No weird behaviours.
>Nice job!

Hooray!

---

<a name="usenix-2015-materials"></a>
## USENIX presentation slides available 
July 20, 2015

Here are Harvey's [presentation slides](docs/Harvey-Usenix-2015-ATC-BOF-slides.pdf) at USENIX 2015 ATC BOF.

We will update this note when we can link to a video of the talk.

---

<a name="developers-wanted"></a>
## Looking for developers!
July 15, 2015

For the next couple of months, the project is looking for developers to step up and help get Harvey ready for prime time.

> "I think the big goal for the next two months, the single most important goal, is to move a needle: we want more people contributing"

There still exist areas for continued development, and YOU can make a difference. This experience can make for an ideal project for Operating System courses and the like. Please talk to us!

> "For new people: we have troubles with sdiahci.c, ahci driver. So we haven't local disk for now. It's not blocking at all, but other improvements depends on it. But, what would you like to do with Harvey meanwhile?"

---

<a name="usenix-2015"></a>
##Harvey at USENIX 2015
July 8, 2015


It's usenix and we have a BOF tomorrow night, so we have to get the
minicluster going. Five AMD Persimmon boards in a stack and 1 Minnow
MAX.

We had really high hopes for the minnow max but it is a bit of a
disappointment. Super neat size -- see the little blue box hanging
from an ethernet cable in the 5th picture? It was kind of exciting to
see so much in such a small box.

We've concluded that to make this board usable for Harvey we're going
to need to swap out UEFI for some other firmware. it took us 15
minutes just to walk through enough of the commands and dialogues to
realize we can only boot from a FAT-formatted SD card. FAT
formatted. 2015. What's wrong with this picture?

So then tried PXE boot. See John taking a movie of the TV? It's
because when UEFI pxeboot fails, it puts the failure frame up for 1/30
second and clears it. So John took a movie, and then we watched the
movie frame by frame to see the error. 

Then we hit the next problem: once we
got the special version of GRUB booting over the LAN, it told
us we wouldn't have a visible console. We need a console.

The AMD stack, with three coreboot nodes and two AMI BIOS nodes,
worked better. The only thing that went wrong is that the AMI BIOS
breaks pxelinux.0 -- it loads and gets to some point, and then instant
reset. We can still boot harvey on the AMI BIOS nodes, but only from a USB stick. 
We'll be reflashing these too. 

![mini cluster](img/usenix2015/mini-cluster.jpg)
Harvey mini-cluster ready to fire up (or catch fire)

![boffins to blame](img/usenix2015/boffins-to-blame.jpg)
John on the floor, trying to make the minnowmax boot
Harvey, Aki on the chair making Harvey build on a mac and boot off of one.

![video of error](img/usenix2015/video-of-error.jpg)
John decided taking a video of the boot sequence would
be the best way to capture the sub-second error message.