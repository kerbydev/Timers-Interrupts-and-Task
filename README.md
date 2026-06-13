Laboratory Activity 1: Timers, Interrupts, and Task Scheduling  Course: BCA143 Firmware Programming  
Student: Kerby labor  
Date: 14/06/2026

14/06/2026

This project implements timer-based interrupts and a cyclic executive scheduler on the STM32F407ZGT6 microcontroller (RT-Thread RT-Spark board).  
Hardware  

•	RT-Thread RT-Spark Development Board (STM32F407ZGT6)  
•	LEDs: PF11 (Red), PF12 (Blue)  
•	User Button: PA0  
•	Debug Pin: PE0  

Features  
•	TIM2: 1 Hz periodic interrupt (high priority)  
•	TIM3: 2 Hz periodic interrupt (medium priority)  
•	External interrupt on button press  
•	Foreground/background system architecture  
•	Timing measurement and analysis  

Build Instructions  
1.	Open project in STM32CubeIDE  
2.	Build: Project → Build All  
3.	Connect RT-Spark via USB  
4.	Upload: Run → Debug or Run

Analysis  

1. What is the maximum latency for Task A in your system?  
- 	The delay for Task A is 21.006 ms. This was measured using the DWT cycle counter by getting the time difference between the start of the TIM2 callback and when task_adc_ready started in the main loop. The highest value recorded is 21.006 ms. 
 
2. If Task B is running when TIM2 interrupt occurs, how does it affect TLatency(Task A)?  
- 	If Task B is running, it will pause because TIM2 is more important (higher priority). The CPU will handle the TIM2 interrupt first before going back to Task B. Because of this, Task A can trigger faster, so its delay becomes shorter. 
 
3. Calculate worst-case TResponse for Task A if all other tasks are running  
- 	To compute the worst-case response time, just add the biggest delay of Task A and its run time. The biggest delay measured is 21.006 ms, and Task A needs 50 ms to finish. So, the worst-case response time is 71.006 ms. 
 
4. How would response time change with a preemptive scheduler?  
If you use a preemptive scheduler, Task A will have a faster response time, especially if it has a higher priority. When Task A is ready, it does not need to wait for other tasks to finish. It can just interrupt a lower-priority task and run right away. This makes the delay much shorter. 
