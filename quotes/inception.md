## Inception Quotes

Next time someone asks “What is Programming like?” I’ll say something along these lines:

“Did you watch that movie “Inception”? Programming is similar, you build your own worlds, with your own rules (and worlds that can only exist in the abstract, sometimes very hard to explain in words), but now imagine that instead of dreaming in 4 levels (dreams inside dreams) you could be dreaming in about 12 levels down, but not only that, you could be having several dreams at once (each with several levels down), and most of the times some of these dreams have to share things with one another in order to make sense or they break.

So Programming is like Inception, but Deeper, In Parallel and Synchronized.”

## How programmers saw Inception

``` php
 function inception($idea) {  
     return enterDream($idea);  
 }  
   
 function enterDream($idea) {  
     try {  
         //Do Something...  
     } catch (SubjectRealizesWhatsGoingOnException e) {  
         return false;  
     }  
   
     if (IdeaHasTakenRoot) {  
         return true;  
     } else {  
         return enterDream($idea);  
     }  
 }  
```
