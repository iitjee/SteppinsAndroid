

Unlike other programming paradigms in which apps are launched with a main() method, the Android system initiates code in an Activity instance by invoking specific callback methods(lifecycle methods).
There is a sequence of callback methods that - start up an activity and - that tear down an activity.Below is the " A simplified illustration of the Activity lifecycle, expressed as a step pyramid. "


![alt text](https://developer.android.com/images/training/basics/basic-lifecycle.png "basic-lifecycle")

only three of these states can be static. (i.e The activity can exist in one of only three states for an extended period of time)<br/><br/>
__Resumed__: activity is in the foreground and the user can interact with it. (Aka "running" state.) <br/>
__Paused__: activity is partially obscured by another activity—the other activity that's in the foreground is semi-transparent or doesn't cover the entire screen. The paused activity does not receive user input and cannot execute any code. <br/>
__Stopped__: activity is completely hidden and not visible to the user; it is considered to be in the background. While stopped, the activity instance and all its state information such as member variables is retained, but it cannot execute any code. <br/>

The other states (Created and Started) are transient and the system quickly moves from them to the next state by calling the next lifecycle callback method. That is, after the system calls onCreate(), it quickly calls onStart(), which is quickly followed by onResume().Your activity never resides in the Created or Started states. 
This is the first half of teh pyramid.

__Destroy the Activity__ <br/>
While the activity's first lifecycle callback is onCreate(), its very last callback is onDestroy(). 
Most apps don't need to implement this method because local class references are destroyed with the activity and your activity should perform most cleanup during onPause() and onStop(). 
However, if your activity includes background threads that you created during onCreate() or other long-running resources that could potentially leak memory if not properly closed, you should kill them during onDestroy().
<br/>

__Note__: The system calls onDestroy() after it has already called onPause() and onStop() in all situations except one: when you call finish() from within the onCreate() method. In some cases, such as when your activity operates as a temporary decision maker to launch another activity, you might call finish() from within onCreate() to destroy the activity. In this case, the system immediately calls onDestroy() without calling any of the other lifecycle methods.

