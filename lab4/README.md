# Lab4 IPC in FreeRTOS part 2: Binary Semaphores, Counting Semaphores, Mutexes

## OBJECTIVES

- Students can install FreeRTOS
- Students study the customization of FreeRTOS
- Students understand the structure of the FreeRTOS
- Students can write simple program with multiple tasks, queue, semaphores and mutexes

## OVERVIEW

Laboratory work 4 is aimed at obtaining initial knowledge and skills of using semaphores and mutexes for process synchronization in FreeRTOS.

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

1. Read the FreeRTOS documentation about semaphores and mutexes
2. Create a new project

3. Do the task according your variant. The variant can be calculated using the last digit of your ID. For example, if your ID is 192050183 your variant will be 3. If your ID is 192050180 your variant will be 10.

4. Write a report (1 point).

5. Put the **entire project** (src) in GitHub, use .gitignore if it necessary (1 point)

6. **Read the FreeRTOS documentation and answer on the questions (2 points per question) in Yandex Forms** 

## Questions

1. Why do I need semaphores?


Binary Semaphores – A binary semaphore used for synchronization does not need to be ‘given’ back after it has been successfully ‘taken’ (obtained). Task synchronization is implemented by having one task or interrupt ‘give’ the semaphore, and another task ‘take’ the semaphore.

Binary semaphores the better choice for implementing synchronization (between tasks or between an interrupt and a task), and mutexes the better choice for implementing simple mutual exclusion.

2. What problems do programmers face when using semaphores？

- The library uses multiple semaphores, which increases its RAM footprint.

- Semaphores cannot be used until they have been created, so a library that uses semaphores cannot be used until it has been explicitly initialized.

- Semaphores are generic objects that are applicable to a wide range of use cases; they include logic to allow any number of tasks to wait in the Blocked state for the semaphore to become available, and to select (in a deterministic manner) which task to remove from the Blocked state when the semaphore does become available. Executing that logic takes a finite time, and that processing overhead is unnecessary in the scenario shown is Listing 154, in which there cannot be more than one task waiting for the semaphore at any given time.

3. Why is it dangerous to use shared memory for multiple processes？

   This can be dangerous because on many platforms, if two threads write to a memory location at the same time, it may be possible for the memory location to end up holding a value that is some arbitrary and meaningless combination of the bits representing the values that each thread was attempting to write; this could result in memory corruption if the resulting value is one that neither thread attempted to write. Similarly, if one thread reads from a location while another thread is writing to it, it may be possible for the read to return a value that is some arbitrary and meaningless combination of the bits representing the value that the memory location held before the write, and of the bits representing the value being written.

4.  Explain the difference between semaphores and mutexes in FreeRTOS？

   Binary semaphores and mutexes are very similar, but do have some subtle differences. Mutexes include a priority inheritance mechanism, binary semaphores do not. This makes binary semaphores the better choice for implementing synchronization (between tasks or between an interrupt and a task), and mutexes the better choice for implementing simple mutual exclusion.

