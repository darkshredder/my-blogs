---
layout: post
title: "Building Workspace Switcher for MX Master 3"
date: 2022-08-31 03:29:20 +05:30
categories: darkshredder blogs journey begins mx mx-master mx-master-3 workspace-switcher horizontal-scroll
---

# Building Workspace Switcher for MX Master 3

## The Idea

Basically, I was annoyed with switching different applications with TAB, Also have used Mac before so Working on different workspaces was easy to manage.

I already used Logitech Mx Master 3 and looked at it's horizontal scroll wheel so thought I would try to build a workspace switcher using horizontal scroll wheel.

## Let's Build It

I use ubuntu 22.04 with X11 as my window manager.

Quickly went to [libX11](https://www.x.org/releases/X11R7.6/doc/libX11/specs/libX11/libX11.html) to find out how to change workspace.

For getting events for horizontal scroll I used input_event for `input.h` header file.

```c
// event0 is input_event file
char fd = open("/dev/input/event0", O_RDONLY);
if((fd == -1) {
    perror("opening device");
    exit(EXIT_FAILURE);
  }

  int event_count = 0;

  while(read(fd, &ie, sizeof(struct input_event))) {
    // Read the event
  }

```

## The Code

<br>


`common.h` header file

```c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <assert.h>

#include <linux/input.h>
#include <fcntl.h>
#include <X11/X.h>
#include <X11/Xlib.h>
#include <X11/extensions/XInput2.h>

#define AnyPropertyType      0L	/* special Atom, passed to GetProperty */

#define WRAP(_var, _from, _to) do { \
    if (*_var == (_from)) {         \
        *_var = (_to);              \
        return;                     \
    }                               \
} while (0)

void map_init(Display *dpy);
void map(int *x, int *y);

```

<br>

`map_rectangular.c` file
    
```c
#include "common.h"

/* This file provides a map which assumes the entire
   rectangular display area is viewable. */

static int width, height;

void map_init(Display *dpy) {
    int screen = DefaultScreen(dpy);
    width  = DisplayWidth (dpy, screen);
    height = DisplayHeight(dpy, screen);
}


void map(int *x, int *y) {
    WRAP(x, 0, width-2);
    WRAP(x, width-1, 1);
    WRAP(y, 0, height-2);
    WRAP(y, height-1, 1);
}
```

<br>

`main.c` file

```c
int main(int argc, char *argv[])
{
  int fd;

  assert(argc==2);
  struct input_event ie;
  assert(strncmp(argv[1], "/dev/input/event", 16)==0);

  if((fd = open(argv[1], O_RDONLY)) == -1) {
    perror("opening device");
    exit(EXIT_FAILURE);
  }

  int event_count = 0;

  while(read(fd, &ie, sizeof(struct input_event))) {
    if (ie.type == EV_REL && (ie.code == REL_HWHEEL || ie.code == REL_HWHEEL_HI_RES)) {

      event_count++;

      if (event_count < 3) {
        continue;
      }

      event_count = 0;
        
      if (ie.code == REL_HWHEEL_HI_RES){

        Display *dpy = XOpenDisplay(NULL);
        if (dpy == NULL) {
            fprintf(stderr, "Cannot open display\n");
            exit(EXIT_FAILURE);
        }
        Window root = DefaultRootWindow(dpy);
        Atom atom = XInternAtom(dpy, "_NET_CURRENT_DESKTOP", False);
        Atom actual_type;
        int actual_format;
        unsigned long nitems, bytes_after;
        unsigned long *data = NULL;
        int status = XGetWindowProperty(dpy, root, atom, 0, 1, False, AnyPropertyType, &actual_type, &actual_format, &nitems, &bytes_after, (unsigned char **)&data);
        if (status != Success) {
            fprintf(stderr, "Cannot get _NET_CURRENT_DESKTOP property\n");
            exit(EXIT_FAILURE);
        }
        int current_desktop = data[0];

        XEvent xev;
        memset(&xev, 0, sizeof(xev));
        xev.type = ClientMessage;
        xev.xclient.window = root;
        xev.xclient.message_type = atom;
        xev.xclient.format = 32;

        if (ie.value > 0)
        {
            xev.xclient.data.l[0] = current_desktop - 1;
        }
        else
        {
            xev.xclient.data.l[0] = current_desktop + 1;
        }

        xev.xclient.data.l[1] = 0;

        XSendEvent(dpy, root, False, SubstructureNotifyMask, &xev);
        XFlush(dpy);
        XFree(data);
        XCloseDisplay(dpy);

        printf("Switching to desktop %ld from %d\n", xev.xclient.data.l[0], current_desktop);

      }
    }
  }

  return 0;
}
```


## Contributing

The code is open source and you can contribute to it by creating an issue or a pull request. The [Github repository](https://github.com/darkshredder/mx-master-workspace-switcher) is the place to go to.
