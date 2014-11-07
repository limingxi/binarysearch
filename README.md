#binary search summary

Recently I have read a great [post about Binary Search]. In this post, the author introduced us a 14 lines framework to write binary search. For the first time I read it, I did not quite understand the point. After a deep thinking on this, I think I get the point now and I would like to write it down for review :)  

First of all, binary search is not easy to write. The reason is that the target may or may not be in the given array. If we just want to look for the target and return -1 for not found, it's quite easy. But sometimes it's more complicated. For example, the question [search insertion position] requires us to look for the position we can insert target in. Target is maybe in the array and maybe not. This really makes me headache, there are so many boundary cases to consider. What if the target is smaller than the smallest element in array? What if the target is not in the array?  

As we can see, binary search varies a lot. If you deal with them by the original one from textbook, you are most likely going to the wrong answer. Now let's see where we can modify for binary search:  

1. 	When to stop: **left>right** or **left>=right**
2. 	How to choose mid: **left+(right-left)/2** or **right-(right-left)/2**
3. 	How to update left and right: **left=mid+1** or **left=mid** 
4. 	How to initialize the left and right: **right=n** or **right=n-1**? 

There are so many combinations there, which should we choose?  

Based on the post I mentioned above, we choose to:  

1. 	Keep looping for **right-left>1**
2. 	**mid=left+(right-left)/2**
3. 	Update left or right to mid. i.e. **left=mid** or **right=mid**
4. 	initialize: **left=-1** and **right=n**

Yes points 1, 3, 4 are weired. For point 1, why we want to keep looping for **right-left>1**? Actually this means we stop at **right-left==1**. It's tricky here, instead of giving us a single result, it gives us a pair(left,right). Remember we have invariant for our loop, and when loop ends, the invariant should remain true. So either we found the target or not, we know the target is in the range either (A[left],A[right]] or [A[left],A[right]). And this is depend on your choice (most likely you need to choose that based on your question).  

With the knowledge of invariant, point 3 and point 4 are easy to explain. For point 3, we don't use mid+1 or mid-1 because we don't want to kick the target out of the range. For example, we are looking for 8 and A[mid]=7 and A[mid+1]=9. Once we choose left=mid+1, then target&lt;A[left]. For point 4, the target maybe smaller than A[0] or larger then A[n-1]. We can assume A[-1]=INT_MIN and A[n]=INT_MAX which will guarantee the loop invariant in the first place.  

>Tip: one thing to mention here is that mid+1 or mid-1 can make sure you won't loop infinitely. So are we in danger for using **mid** to update left & right? The answer is no, because loop stops at **right-left==1**. Still get lost? Think about when we get an infinite loop: assume when right-left==1  
>**mid = left+(right-left)/2 = left+0 = left**  
>Then we assign mid to left, which means nothing changes here. However, our loop will be terminated when right-left==1 :)

Well, maybe you still think it's hard to remember the rules and apply them into real situation is even harder. OK then you just keep in mind one thing: **keep your "target" in A[left] and A[right]!** Sometimes you are finding a specific index, maybe sometimes you are just finding a **gap**, never skip the gap when you updating the left or right and you will be fine.



[post about Binary Search]:http://fihopzz.blogspot.com/2013/07/enter-post-title-here-binary-search-and.html
[search insertion position]:https://oj.leetcode.com/problems/search-insert-position/
