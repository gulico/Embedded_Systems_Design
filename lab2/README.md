# Lab2 Developing tasks in FreeRTOS

## OBJECTIVES

- Students can install FreeRTOS

- Students can understand the FreeRTOS organization

- Students learn the ways of the customization of FreeRTOS
- Students can write simple programs with multiple tasks for FreeRTOS

## OVERVIEW

Laboratory work 2 is aimed at obtaining initial knowledge and skills in programming FreeRTOS tasks. You will need this knowledge to successfully complete the following laboratory work.

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

1. Read the FreeRTOS and Git documentation
2. Install FreeRTOS using Stm32CubeIDE
3. Create a project
4. Create two tasks
5. From each task, control the LEDs at different frequencies
6. **Put the source code of the project on GitHub (2 points)**. You can use for this git, SourceTree, plugin for Eclipse, etc...
7. **Read the FreeRTOS documentation and answer the questions in the end of this document (2 points per question)**

## Questions

1. What features of FreeRTOS do you remember?

   - Pre-emptive or co-operative operation 
   - Very flexible task priority assignment 
   - Flexible, fast and light weight task notification mechanism 
   - Queues 
   - Binary semaphores 
   - Counting semaphores 
   - Mutexes 
   - Recursive Mutexes 
   - Software timers 
   - Event groups 
   - Tick hook functions 
   - Idle hook functions 
   - Stack overflow checking 
   - Trace recording 
   - Task run-time statistics gathering
   - Optional commercial licensing and support 
   - Full interrupt nesting model (for some architectures) 
   - A tick-less capability for extreme low power applications 
   - Software managed interrupt stack when appropriate (this can help save RAM)

2. What are the differences between FreeRTOS, OpenRTOS and SafeRTOS?

   - The **FreeRTOS** open source license is designed to ensure:

     1. FreeRTOS can be used in commercial applications.
     2. FreeRTOS itself remains freely available to everybody.
     3. FreeRTOS users retain ownership of their intellectual property.
   - **OpenRTOS** is a commercially licensed version of FreeRTOS provided under license from Real Time Engineers Ltd. by a third party.
   - **SafeRTOS** shares the same usage model as FreeRTOS, but has been developed in accordance with the practices, procedures, and processes necessary to claim compliance with various internationally recognized safety related standards.

3. Why do we need the vTaskStartScheduler() function?

   Starts the FreeRTOS scheduler running.

   Typically, before the scheduler has been started, main() (or a function called by main()) will be executing. After the scheduler has been started, only tasks and interrupts will ever execute.

   Starting the scheduler causes the highest priority task that was created while the scheduler was in the Initialization state to enter the Running state.

4. Why do we need the xTaskCreate() function?

   Creates a new instance of a task.

   Each task requires RAM that is used to hold the task state (the task control block, or TCB), and used by the task as its stack. If a task is created using xTaskCreate() then the required RAM is automatically allocated from the FreeRTOS heap. If a task is created using xTaskCreateStatic() then the RAM is provided by the application writer, which results in two additional function parameters, but allows the RAM to be statically allocated at compile time.

   Newly created tasks are initially placed in the Ready state, but will immediately become the Running state task if there are no higher priority tasks that are able to run.

   Tasks can be created both before and after the scheduler has been started.