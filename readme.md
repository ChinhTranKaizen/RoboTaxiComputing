# Performance modeling of vehicular cloud based on RoboTaxi fleet
## Motivation
Robotaxis are equipped with wireless telecommunication capabilities, a sensor suite that contains diverse type of sensors and a powerful onboard computation unit. It will be a subject of interest when the robotaxis of a mobility service provider can interconnect and form a computing cluser and execute external computing jobs together while serving regular hailers. Clearly, this will provide additional values to the mobility service provider. However, there remains a few questions of this system that need to be answered:
1. What are the behaviors, which include the interarrival times of the requests to the taxi system and the duration of the ride, of the current hailers?

2. Since the main objective of the system is to first serve the hailers then, during robitaxi idle time, to execute the jobs, what will be the computation throughput of the system during rush/ off-peak hours?

3. How many robotaxis are required to fulfill a certain Quality of service of both the mobility service and the computing service?
This project is aimed to answer questions similarly to the above.
## Project description
The project is splitted into 2 parts: Hailers' behavior analysis and Performance analysis of robotaxi computing system
### Hailers' behavior analysis
This project applies data analysis, statistical modeling to the NYC Yellow Taxi dataset to answer the first question above. The procedures are as follow:

- Extract trip start time and end time for each trip.

- Apply feature engineering to remove illogical values based on [NYC TLC law on driver's fatique management](https://www1.nyc.gov/site/tlc/about/fatigued-driving-prevention-frequently-asked-questions.page)

- Apply computer engineering knowledge to enhance details of trip start time

- Derive trip duration from the trip end time and start time

- Derive hailers' request interarrival time from engineered trip start time

- Model the interarrival time distribution and residency time distribution as a [Phase-Type distribution](https://en.wikipedia.org/wiki/Phase-type_distribution), which is commonly done in analyzing service systems.

- The fitting of the Phase-type distribution is done using [Hyperstar](https://www.mi.fu-berlin.de/inf/groups/ag-tech/projects/HyperStar/index.html) tool, which is based on K-Means algorithm.

### Performance analysis of robotaxi computing system
Assuming that the hailers' request are prioritized to be execute comparing to computing request. Thus, when a hailers' request comes while all the taxis are busy executing either hailers' request or computing request, one computing job will be suspended to make place for the hailers' request. The job will be resumed with progress intact when a taxi is again become free.

Thus, we can analyse the sytem as a Ph/Ph/c/N priority queue with 2 priority levels: the hailers (prioritized) and computing jobs.

The distribution of number of hailers request in the system can be derived [here](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/papers/Ph_Ph_c_N_Queue_Performance%20Evaluation%20of%20Cloud%20Computing%20Centers%20with%20General%20Arrivals%20and%20Service.pdf), which is based on these papers: [paper1](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/papers/Reduced%20complexity%20in%20M_Ph_c_N%20queues.pdf), [paper2](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/papers/a%20recurrent%20solution%20of%20PH_M_C_N%20queue.pdf).

Then the distribution of the number of computing jobs in the system is shown [here](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/papers/Multi-server%20preemptive%20priority%20queue%20with%20general%20arrivals%20and%20service%20times.pdf)

## Summarized Findings
As a proof of concept and without loss of generality, we are going to look only at Monday morning from 6 to 10 am in May of 2019. The reason for this choice is that May is a neither a hot or cold month in NYC and Monday mornings are supposed to be rush hour time.
### Hailers' behavior analysis
#### Interarrival times
- The average of interarrival time of the hailers is 0.4 seconds
- The variance of interarrival time is 0.31 seconds
- The cdf of the interarrival time then can be graphed as shown below:
!['cdf interarrival'](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/May_2019/Monday_morning_cdf_hailers_request_interarrival_time.png?raw=true)
- Using the hyperstar tool, the Phase-type distribution parameters can be derived as:
!['fitting interarrival'](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/May_2019/Monday_morning_fitting_hailers_request_interarrival_time_screenshot.png?raw=true)
#### Trip duration
- The average of trip duration is 881 seconds
- The variance of trip duration is 619155 seconds
- The cdf of the trip duration then can be graphed as shown below:
!['cdf trip duration'](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/May_2019/Monday_morning_cdf_trip_duration.png?raw=true)
- Using the hyperstar tool, the Phase-type distribution parameters can be derived as:
!['fitting trip duration'](https://github.com/ChinhTranKaizen/RoboTaxiComputing/blob/main/May_2019/Monday_morning_fitting_trip_duration_screenshot.png?raw=true)
### Performance analysis of robotaxi computing system
**on-going progress**

