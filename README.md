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
1.	Answer: The biggest delay for Task A is 21.006 ms. We measured this using the DWT cycle counter. We just checked the time when the TIM2 callback starts, and the time when the task_adc_ready part starts in the main loop. The difference between the two times is the delay, and the highest recorded was 21.006 ms. 
 
2.	The biggest delay for Task A is 21.006 ms. We measured this using the DWT cycle counter. We just checked the time when the TIM2 callback starts, and the time when the task_adc_ready part starts in the main loop. The difference between the two times is the delay, and the highest recorded was 21.006 ms. 
 
3.	To compute the worst-case response time when all tasks are running, just add the biggest delay of Task A and the time it takes to run. The max delay is 21.006 ms, and Task A needs 50 ms to finish. So, the worst-case response time is 71.006 ms. 
 
4.	If you use a preemptive scheduler, the response time of Task A will be faster, especially if it has a high priority. Once Task A is ready, it does not need to wait for the current task to finish. It can just interrupt a lower-priority task and run right away. This makes the delay much shorter and improves the response time. 
 
