# Lab3 IPC in FreeRTOS part 1: QueuesS

## OBJECTIVES

- Students understand the interprocess communication in FreeRTOS
- Students can write simple program with multiple tasks and queue

## OVERVIEW

Laboratory work 3 is aimed at obtaining initial knowledge and skills in programming FreeRTOS. You will need this knowledge to successfully complete the following laboratory work.

## PREREQUISITES

1. UM1974 User manual STM32 Nucleo-144 boards https://www.st.com/resource/en/user_manual/dm00244518-stm32-nucleo144-

boards-stmicroelectronics.pdf

2. UM1722 User manual Developing applications on STM32Cube with RTOS https://www.st.com/resource/en/user_manual/dm00105262-developing-applications-

on-stm32cube-with-rtos-stmicroelectronics.pdf

3. FreeRTOS. Real-time operating system for microcontrollers. https://www.freertos.org

4. Mastering the FreeRTOS. Real Time Kernel. https://www.freertos.org/wp-

content/uploads/2018/07/161204_Mastering_the_FreeRTOS_Real_Time_KernelA_Hands-On_Tutorial_Guide.pdf 5. FreeRTOS V10.0.0 Reference Manual https://www.freertos.org/wp-

content/uploads/2018/07/FreeRTOS_Reference_Manual_V10.0.0.pdf

6. Git. https://git-scm.com/
7. David Harris, Sarah Harris, Digital Design and Computer Architecture 2nd Edition
8. Paul Horowitz, Winfield Hill, The Art of Electronics
9. Brian W. Kernighan, Dennis M. Ritchie, C Programming Language, 2nd Edition

## Task

1. Read the FreeRTOS documentation about queue management
2. Create a new project

3. Create two task

4. Create one queue

5. One of the tasks flashes briefly LED when receiving information from the queue.

6. The second task writes any number to the queue and delayed 1 sec.

7. Write a report (1 point)

8. Put the **entire project (src)** in GitHub, use .gitignore to avoid undesirable files (1 point)

9. **Read the FreeRTOS documentation and answer the questions (2 points per question) in Yandex Forms**

## Questions

1. List the models of computation that use queues.

   Task scheduling、message queue

2. Explain the difference between Task and Co-routine in FreeRTOS.

   Applications in FreeRTOS can use tasks, co-routines, or a mixture of the two. However, tasks and coroutines use different API functions, so data cannot be sent from the task to the co-routines via the queue (or semaphore), and vice versa. Co-routines are prepared for MCUs with few resources, and their overhead is very small.
   Co-routines are conceptually similar to tasks but have the following fundamental differences:
   1.Stack usage
   All the co-routines within an application share a single stack. This greatly reduces the amount of RAM required compared to a similar application written using tasks.
   2.Scheduling and priorities
   Co-routines use prioritised cooperative scheduling with respect to other co-routines, but can be included in an application that uses preemptive tasks.
   3.Macro implementation
   The co-routine implementation is provided through a set of macros.
   4.Restrictions on use
   The reduction in RAM usage comes at the cost of some stringent restrictions in how co-routines can be structured.

3. Explain the difference between xQueueSendToBack and xQueueSendToBackFromISR.

   First, xqueuesend and xquesendtoback are aliases for the same function. So the difference you are looking at is the difference between a non-fromisr function and a fromisr function. The major difference between them is that the non-ISR version give you the option to block the task for awhile for the operation to complete if needed, while the ISR versions do not (you DON’T want to delay an ISR execution) but instead give you a flag to let you decide if you need to run the scheduler. A second internal difference is the way critical sections are implemented. The non-ISR versions use slightly simpler code knowing they aren’t in an interrupt context.

4. Why do we need the xTicksToWait parameter in the xQueueReceive function?

   The maximum amount of time the task should block waiting for an item to receive should the queue be empty at the time of the call. Setting xTicksToWait to 0 will cause the function to return immediately if the queue is empty. The time is defined in tick periods so the constant portTICK_PERIOD_MS should be used to convert to real time if this is required.

   If INCLUDE_vTaskSuspendis set to ‘1’ then specifying the block time as portMAX_DELAY will cause the task to block indefinitely (without a timeout).