## <u>Tasks </u>

Tasks are composed of multiple instructions that are processed by the CPU.

## <u>Cooperative-Multitasking-System </u>

The CPU receives multiple tasks , it follows a `yield` process. Basically, it jumps from one task into the other and goes back to the point it left/yield to recontinue the task execution.
In real experimentation, it gives us the feel that these multiple task are being executed in parallel, but what's actually happening , is the cpu is handling the tasks very fast, by jumping among their instructions.

**cons:** the task might claim the CPU resources for a long time , thus making the entire system unresponsive.

## <u>Preemptive-Multitasking-System </u>

OS manages the CPU resources and not the task itself. It will allocate CPU time slices to different tasks according to its own algorith scheduling.
Same as Coorperative , one task is being run at a given instance of time . However due to its rapidness, it will feel like multiple tasks are being executed at the same time

**pros:** Allows concurrent execution of multiple tasks and _guarantess_ system responsiveness.

**cons:** very complex , BUT they are abstracted out from us DEVELOPERS.

**ANDROID IS A PREEMPTIVE MULTITASKING SYSTEM, ANDROID OS DECIDES WHICH TASK IS GOING TO RUN AT ANY GIVEN INSTANCE OF TIME**
