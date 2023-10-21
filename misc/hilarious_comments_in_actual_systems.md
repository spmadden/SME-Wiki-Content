---
title: hilarious_comments_in_actual_systems
description: 
published: 1
date: 2023-10-21T13:50:53.421Z
tags: 
editor: markdown
dateCreated: 2023-09-11T01:28:59.005Z
---

## Hilarious Comments in ACTUAL systems

-   [Comments found in the Kernel Source](/misc/comments_in_linux_kernel)
-   [Temporary, I HOPE HOPE HOPE - Apollo AGC](https://github.com/chrislgarry/Apollo-11/blob/f1f0e58e2a46751b1c3b006f1ba2dc76f25dfb54/Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc#L179)

``` c++
// Not an ACK - message handler has failed us :(
```

``` c++
// These should be throwing exceptions...
```

``` c++
 //MIKE: i hate this
 and a few lines below this...
 //MIKE: see above comment
```

``` c++
 // I love this header file - [user1]
 //Me too - [user2]
```

``` c++
 //TODO: Not this.. never this!
 exit(1);
```

``` c++
 //TDA
 //This code never gets hit (at least app side)... lovely... why? because this is called too early. 
 //but i don't want to change it now.
```

``` c++
 (Not a comment, but actual code...)
 ASSERT(false);
 (^^ FOR THE LOVE OF GOD WHY???^^)
```

``` c++
 //ATTEMPT TO STOP TIME
 (a few lines below)
 //OH GOD WHY DID IT FAIL??
```

``` c++
 #define BOOL int //TODO:  Fix this.
```

``` c++
 // This condition pretty much never happens, but anyways...
 log_error(...
 // But if it does happen, you are screwed.
 exit(1);
```

``` c++
 // Note to the ghost of whoever wrote this before
 // NEVER EVER EVER EVER EVER CLICK YOURSELF.
 // Focus issues are hard enough as is. Just do the right MFC thing.
 // Love, -AD
```

``` javascript
    // Hate for safari
    if (document.title.substr(document.title.length - 2, 1) == "|") {
        document.title = $("title").text()+" "+owner.username+"-"+ticket.t_id;
    }
```

``` perl
1; ##### aargh.  (yes, virginia, this is necessary)
```

``` java
    /**
     * HAPPY FUCKING DUPLICATION YEAH!
     *
     * @see java.lang.Object#clone()
     * @return I Shall call him... Mini-me!
     */
    public CurriculumYearImpl clone() {
```

``` c++
LOG(ERROR) << "Time only flows one way - cannot start before told (my TARDIS is broken)";

```

``` c++
// semi-major axis of earth, change if intergalactic conquest.
const double SEMIMAJOR = 6378137.0;
// semi-minor axis of earth, change if intergalactic conquest.
const double SEMIMINOR = 6356752.314245;
```

``` c++
// <Windows is dumb>
#ifdef ERROR
#undef ERROR
#endif
// </Windows is dumb>
```

``` c++
// fuck me sideways with a type system
```

``` c
        if(length > memorySize){
                // Old mac donald had a farm...
                return -EIO;
        }
```

``` java
  //If we die, that isn't exactly revocable!
  //!!!
```
