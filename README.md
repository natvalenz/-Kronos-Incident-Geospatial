# The Kronos Incident: Geospatial-Temporal Patterns of Life Analysis

## Table of contents
- [Challenge Instructions](#challenge-instructions)
- [Project Objective](#project-objective)
- [Data Description](#data-description)
- [Data Preparation](#data-preparation)
- [Project Analysis](#project-analysis)
- [Project Discussion](#project-discussion)
- [Contributors](#contributors)

## Challenge Instructions
[(Back to top)](#table-of-contents)
<br>
Describe common daily routines for GASTech employees and identify up to twelve unusual events or patterns in the data.
In order to use this data, you will require skills in geospatial-temporal analysis, along with the ability to combine various types of data in sensible ways. The GPS data was extracted from the cars for the two weeks period prior to the kidnapping, but not including the kidnapping day itself. GASTech also issued company debit/credit cards that could be used for personal spending, and many employees had loyalty cards for restaurants and shops around Abila city. Analyzing the combined data sources could reveal clues about the kidnapping and the GASTech employees who may have participated in this activity. You need to be aware that some GPS readings may be skewed for some vehicles. In addition, particular locations may exhibit deviations in the times at which they post their card transactions. Similarly, in some cases, the transactions were logged in batches once per day; in some locations transactions may be delayed, creating the appearance of individuals shopping in the middle of the night.

Focus your work on identifying regular patterns. For example, credit card data may contain typical charges like GASTech employees preferring to use their debit and loyalty cards at coffee houses. Deviations from these patterns might indicate suspicious activities or just non-conforming patterns by individuals. Hypotheses about suspicious activities need to be supported by evidence and/or reasoning from data. Look for anomalies such as a credit card charge occurring for an employee while the GPS track indicates a different location for their assigned vehicle.

Map data, including shape files of Abila city streets and a visitor’s map of the city sites and shops, are provided to you as an additional support to understand patterns of life. For example, even though employees’ home addresses were not provided, patterns of life analysis may reveal where they spent their evening hours, typically indicating their home address. Regular gatherings at what appeared to be residences, but not corresponding to any employee’s home address could suggest different hypotheses.
<br>

## Project Objective
[(Back to top)](#table-of-contents)
<br>
GAStech has been breaking news headlines for being a prestigious company in the energy sector and has recently gained recognition after their initial public offering and successful business model. Now they are breaking news headlines for a different reason. Employees are devastated to find out that some of their coworkers have been kidnapped in an unfortunate turn of events. Two data scientists have been hired to help law enforcement discover unusual patterns of behavior to assist in their investigation of trying to identify what happened during what people are calling ‘The Kronos Incident.’ 

The data scientist researchers were provided with some background information on the employees. GAStech employees had the opportunity to have company cars that they could use for both business and personal occasions. The company cars provided employees an opportunity to have a car that they otherwise may not have been able to afford. The employees who were not assigned a car still had the opportunity to check out company trucks for business use, but the trucks could not be used for personal occasions. GAStech did not trust employees with the vehicles, so the company cars and trucks had geospatial tracking devices that periodically collected data when the vehicles were moving. Employees were unaware of these devices. Employees also had credit cards and loyalty cards which could be used for both personal and business transactions. Loyalty cards were cards where employees could gain rewards and discounts at their favorite local businesses.


## Data Description - *[Download](https://github.com/emmanueliarussi/DataScienceCapstone/tree/master/7_FinalProjects/TheKronosIncidentGeospatial/data/task2.zip)*
[(Back to top)](#table-of-contents)
<br>
To help the investigation, the researchers were given four main files of information. One file contained employee information including car assignment id, employee name and id, department, and title. Two files contained all the card data, one for the credit cards and another for the loyalty cards. Within the card data, the data fields included name, location, price, and the timestamp. The last file included geospatial data that had the car id, timestamp, latitude, and longitude coordinates. Geospatial ESRI shapefiles were provided with images of both Kronos and Abila, Kronos’ capital where the employees resided. Lastly, a tourist map with business locations and areas of interest was also supplied to the data scientists. 

## DATA PREPARATION 
[(Back to top)](#table-of-contents)
<br>
Data preparation came with a myriad of challenges. The first task was to align the GPS data with the shapefiles and the map with identified points of interest. The data was organized in an interactive map, where researchers could filter the name of the employee, what route they took, the time of day, and if the employee made any stops along their route. However, it was noted that GPS data points were sometimes missing or did not provide the full picture of the locations. For example, GPS data for Axel Calzas often showed spotty locations like in the image below. 
![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture1.png)
Figure 1: GPS data partially missing during the morning of 1/10/2014. The time frames were close together, so it can be assumed that the car continued to work after stopping at the coffee shop. 

The GPS data did not include employee names or location names, so both were deduced by the car assignments file along with comparing locations to credit cards and the tourist map. Additionally, the geospatial files did not have the location names. GPS points really did not have meaning without the context of the tourist locations. The employees who were not assigned a company vehicle were difficult to track. Truck drivers sometimes used the same company car on different days or even the same day. There were null car ids for truck drivers, so identifying who drove the truck on which days was tedious but doable with the help of the card data. 

Credit card and loyalty transaction data sets were also merged by each person, data, and cents amount on the price to identify patterns of use and corroborate the GPS location of the employee’s car route more easily. The credit card data was similar to the loyalty card except for the price and timestamp (for the loyalty data, the transactions only had the day but not the hour and minute granularity). There were some cases where employees only used one card or received cashback that left dollar amounts that do not match up. 

The credit card and loyalty card data usually matched the GPS data. In general, people would make a stop at a location and then make a purchase. However, when looking through the data, inconsistencies were identified. Some card transactions had missing timestamps. Sometimes, there were duplicate transactions. Furthermore, when the credit card and loyalty card data was compared to the GPS data, there were more problems. Some transactions had a timestamp at a time that was not necessarily the time the employee was at the business. Kronos Mart, for example, often had charges that did not show up until the following day. These conflicting data challenges were not completely overcome during the analysis and should be noted when law enforcement follows up on their investigation.

## ANALYSIS
[(Back to top)](#table-of-contents)
<br>
#### 1.  Describe common daily routines for GAStech employees. What does a day in the life of a typical GAStech employee look like? 
After filtering and processing the data, patterns started to emerge in the daily life of employees. Most of the employees lived in four to five different neighboring areas along Rist Way. All these locations are northeast, following the outline of the golf course. Employees start their day at home. It was common to see employees stop by the local coffee shop near them on their way to work, go out to eat at local restaurants during lunch, and run errands or go out to eat again at dinner. For example, Hideki Cocinaro lives by Sannon Park. A typical day for her was waking up and stopping by Hallowed Grounds on her way to work, stopping at Abila Zacharo (or another local restaurant) for lunch, and going out to Guy’s Gyros for dinner after work. On the weekends, employees went out later for lunch, shopping, and dinner, or enjoyed other activities such as going to the museum or playing golf. 

![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture2.png)

Figure 2: A typical GPS route of a GAStech employee with stop locations marked with asterisks and color coordinated by time of the day. 

Several patterns emerged with the local businesses as well. Katerina’s Kafe, Hippokampos, and Guy’s Gyros were by far the most popular restaurants. Brew’ve Been Served was the most popular coffee shop, followed by Hallowed Grounds.
![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture3.png)

Figure 3: Local business count of credit and loyalty card transactions. 

Employees from within the same department had similar routines as one another but had slightly different routines than those from other departments. For example, the truck drivers often frequented different shops and industries (such as going to the airport) than the other employees. All the executives seemed to enjoy playing golf more often than the other departments.

## UNUSUAL PATTERN RESULTS
[(Back to top)](#table-of-contents)
<br>
#### 2. Identify up to twelve unusual events or patterns that you see in the data. If you identify more than twelve patterns during your analysis, focus your answer on the patterns you consider to be most important for further investigation to help find the missing staff members. 
Although most employees followed a ‘typical day’ routine, there were several anomalies detected in the data sets. 

Pattern 1
Looking at both the credit card and loyalty card transactions, there were two outliers that warranted further investigation. Outliers are significant because they can show something unique about a situation. The first was a credit card charge at Frydo’s Autosupply shop for $10,000 at 2014-01-13 19:20:00 by Lucas Alcazar, and the second was a charge at Chostus Hotel for $600 at 2014-01-18 12:03:00 by the CEO Sten Sanjorge Junior. For the first transaction, Lucas’ GPS locations were examined for that day, and it was noted that he was nowhere near Frydo’s Autosupply shop when the charge happened. 

![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture4.png) 
Figure 4: Lucas’ GPS locations during the day of the Frydo’s Autosupply $10,000 transaction.

The GPS data and the card data did not match. Researchers also noted that Lucas only used his loyalty card from January 13th to January 15th, which is after the transaction at Frydo’s Autosupply. He did not use his credit card again until the 16th. There could be varied reasons for this. Lucas’ car GPS location is wrong, or he walked to the location. His card could have gotten stolen, or he gave the card to another coworker. Given the mismatch of GPS location and extremely high credit card charge, it is important to follow up and determine who else was in this location during this time of day. Looking through other employees’ locations during the same time, it was noted that Minke Mies was the only person at Frydo’s Autosupply at 7:20pm on January 13th, and thus, this makes him a suspect for the card transaction. The level of confidence for this pattern was average. There could be several explanations for the mismatching transaction and GPS data, so this event would be a suitable place for law enforcement agencies to start.

![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture5.png)

Figure 5: Minke’s GPS locations during the day of the Frydo’s Autosupply $10,000 transaction. He was the only person at Frydo’s Autosupply during the time of the credit card purchase.

Pattern 2
The other card outlier was the purchase at Chostus Hotel by the CEO. After reviewing the GPS coordinates of the CEO’s whereabouts, it appeared that the CEO was at the Chostus Hotel during the transaction time. There is not a lot of GPS information for the CEO, but with the GPS patterns that were there, the patterns indicate that he enjoyed playing golf and going to the hotel on the weekends, so this transaction does not seem as suspicious. The level of confidence about this pattern was average. The transaction was significant because it was an outlier, but company executives typically have a higher budget to make financial decisions. 

Pattern 3
One of the most puzzling patterns to understand was the card transactions that did not align with the GPS locations. There were several purchases, like Lucas’ $10,000 transaction at Frydo’s Autosupply, that also did not match the driving locations of other employee’s cars. For example, on January 7th, Axel Calzas had a charge at Hippokampus at 8:00pm but was never there on the GPS location. On January 8th, Felix Resumir had a charge of $30.85 at Abila Zacharo, but the GPS data does not reflect the same. On January 17th, Linnea Bergen’s loyalty and credit card were charged $140.78 at Kalami Kafenion, but she does not have GPS data to back it up. On January 19th, Bertrand Ovan had a charge of $72.25 at Katerina’s café, but he had no GPS data for that day. It is important to note that unlike Lucas’ $10,000 transaction at Frydo’s Autosupply, these other card transactions did not have GPS data that showed other employees were present at these locations during the time of the transaction, and in addition, these transactions were not outliers. However, it was important to note the inconsistency within part of the data. The level of confidence with this pattern was low since there were several times that the card data did not match with the GPS locations.


Pattern 4
After detecting outliers in the card transactions, GPS locations were used to identify suspicious activity. There were several people who drove around during lunch hours and seemed to stop at various meeting places to take a long lunch break. Hennie Osvaldo, Inga Ferro, Minke Mies, and Loreto Bodrogi were all noticed driving around during lunch and making several stops in addition to their lunch destination. Most of these stops were spread out across town. Just south of Frank’s Fuels, next to the Port of Abila, north of Abila Scrap, and to the west of Guy’s Gyros were all common locations of these random stops during lunch. Sometimes the employees went alone, and sometimes it seemed like they went with one another. For example, Inga and Loreta both stopped near Abila Scrap on January 17th. Minke and Hennie both stopped near Frank’s Fuels on January 16th, but Loreto went near the Frank’s Fuels location alone on January 11th. These locations were all next to and not at any of the major businesses, so it was suspicious that these people were taking long lunches and sneaking around to various locations. All these employees worked in the same department of security, and they seemed to have secret meetings during lunch. The level of confidence for this pattern was high since it happens on multiple days for every mentioned person in the past two weeks. All these employees should be questioned and asked about their whereabouts. 

![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture6.png) 
Figure 6: Hennie stops next to the Port of Abila during an extra-long lunch hour. She stops at 11:10am and leaves at 12:22pm.

Pattern 5 
Other surprising patterns in the GPS locations were night movements. These movements were significant because most shops or businesses were closed at night, and employees usually slept at night. There should not be much movement going on at 3:00am, so seeing a pattern of movement during this time should be further investigated. It is also interesting to note that most of the same people involved in the previous pattern (stopping for extra-long lunch breaks in odd locations) were also the ones involved in driving around at night. Hennie Osvaldo, Minke Mies, and Loreto Bodrogi were all involved in suspicious driving and stopping at various locations during lunch, and these three were also involved in suspicious driving and stopping during the middle of the night. Loreto stops at Spetson Park on January 7th and then Taxiarchon Park on January 9th around 3:30am and then leaves around 7:00am to go to the local coffee shop. Hennie stops near Ahaggo museum around 3:30am and leaves around 11am on January 11th, and she goes to the same location around 11:00pm on January 13th and leaves around 3:00am. Hennie also starts her morning and ends her evening in two separate locations throughout the two weeks making it difficult to track where she lives. She stays near Frydo’s Autosupply on most nights, but on January 8th, 11th, 12th, 15th, and 18th, she stays the night at a location just north of Guys’ Gyros. She often frequents the same location during lunch hours too. It was noted that Minke Mies also lives just north of Guys’ Gyros, so maybe Hennie is staying at Minke’s place during those times. Minke Mies stops at Taxiarchon Park on January 8th at 11pm and does not leave until 3:30am in the morning, and he stops at Ahaggo Museum around 3:30am on January 14th and leaves at 7:50am. In addition to these three, Isia Vann was also noticed driving out at night and staying at a different location from her house right by Spetson Park on January 6th from 11pm to 7:30am and again by Ahaggo Museum on January 10th from 11:00pm to 3:30am. Isia is also a security employee like the others. It is important to note that although all of these people engaged in night movements, only one person seemed to be going to these locations at a time. They were all on separate times during the day. The level of confidence for this pattern was high because nobody else was making these random drives and stops in the middle of the night.

Pattern 6
On the night of January 10th, several employees from the IT and engineering department go to a Carnero Street house and do not leave until later in the night. Lucas Alcazar, Lars Azada, Felix Balas, Isak Baza, Linnea Bergen, Isande Borrasca, Nils Calixto, Axel Cazas, Gustav Cazar, Lidelse Dedos, Birgitta Frente, Vira Frente, Adra Nubarron, Marin Onda, and Brand Tempestad all got together after work hours in what looks like potentially Lars Azada’s house. This event is significant because it could be a secret meeting, or it could be an afternoon work party. The level of confidence for this pattern was average. Given that there were no other meetings like this in these worker’s daily routines, this event may be just an innocuous Friday evening work gathering. 

Pattern 7
Two employees were identified traveling to the hotel during lunch hours. Brand Tempestad and Isande Borrasca were noticed driving to and from the Chostus Hotel on January 8th, 10th, 14th, and 17th at roughly the same time during the day. This trend is significant because this was an odd time of day for the two to be getting together at a hotel. They appear to be meeting in secret for something. They are arriving and leaving at roughly the same time, so they seem like they are meeting in secret for something. Whether that is for an affair or for planning a kidnapping, that is yet to be determined, but the level of confidence for this pattern was high since this event took place on multiple occasions.

![alt text](https://github.com/natvalenz/Kronos-Geospatial/blob/main/Picture7.png) 
Figure 7: Brand and Isande were noticed going to the same hotel during the middle of the day during lunch hours on several dates in the past two weeks.


Pattern 8 
On January 18th, there was another important event where several people went to Kronos Capital during lunch. Kanon Herrero, Loreto Bodrigi, Edvard Vann, Elsa Orilla, and Adra Nubarron from both security and engineering departments were all at the event. Adra Nubarron was the only person that stayed the night at the park area and did not leave until the following day. Leaving the next day was significant because there was no one else at the Capital, and it is very suspicious that she stayed the night. The level of confidence about this pattern was low since there were not any other conflicting GPS or card data for Adra. 

Pattern 9
There were some significant gaps in Elsa Orilla and Kanon Herrero’s card and GPS data. Sometimes there would be no GPS coordinates for one person, but there were matching transactions of the same price on both of their cards. Elsa’s car did not move, but she had loyalty card movements for several dates including January 6th, 7th, 8th, 10th, 13th, 15th, and 16th. Kanon Herrero’s car did not move, but he had credit card movements on January 9th, 14th, and 17th. Kanon had credit card charges around lunch time that corresponded to Elsa’s loyalty card charges. After putting the data together, researchers noted that the couple was probably together during lunch and shared the same company vehicle. Elsa and Kanon were also together during the weekends and tended to spend most of their time with each other. The level of confidence on this trend was average since there could be multiple explanations for conflicting card data. 

Pattern 10
Trucks had GPS data going all-around normal routes but no corresponding card charges. The truck drivers seemed to go back and forth to and from GAStech more often than other departments. Normal routines appeared to happen during the morning and lunch with the corresponding card transactions. Maybe the truck drivers did not have loyalty or credit card data for those transactions. Further information would be needed to determine why the truck had GPS information showing, for example truck 104, going back and forth from the airport and GAStech during evening hours. Henk Mies usually drives truck 104, but he showed no card data to support the multiple airport visits. In addition, Irene Nant had a loyalty card charge on January 10th for $3,489.36 at Carlyle Chemical Inc, but it was not possible to determine what truck she was driving that day. The truck GPS inconsistencies are significant because the use of the trucks for illicit activities is possible, but the level of confidence is low. The records showing who used what truck is needed to clarify what is going on.

Pattern 11
There were some occasions where employees seemed to drive to some locations but did not seem to buy anything which is significant because these two datasets do not corroborate one another. Bertrand Ovan was driving all around town but had no card data for it in the evening on January 11th. However, this was a weekend, and he did not appear to have any other unusual activity the past couple of weeks. Another employee, Nils Calixto, went to Kronos Mart during lunch on January 17th but did not buy anything. This was the only mismatching data Nils had when the GPS and card data was compared, so maybe he did not want to buy anything at Kronos Mart. The level of confidence about this pattern was average since it makes sense that people sometimes go into store locations and do not buy anything.

Pattern 12
Lucas Alcazar gets home late from work on several days including the 6th, 8th, 15th, and 17th. It seemed like Lucas might be staying at the office to work late during those days, or he could be planning the kidnappings. No other person was at the office during those times, so these events are significant. The level of confidence about this pattern was high because Lucas drives to and from work on several nights. 


## Project Results
[(Back to top)](#table-of-contents)
<br>
#### 3. Like most datasets, the data you were provided is imperfect, with possible issues such as missing data, conflicting data, data of varying resolutions, outliers, or other kinds of confusing data. Considering data is primarily spatiotemporal, describe how you identified and addressed the uncertainties and conflicts inherent in this data to reach your conclusions in questions 1 and 2.

There were several unique patterns that have emerged from this data set, and all these patterns should be followed up and further investigated by law enforcement teams. Researchers had to navigate around missing and conflicting data, making it closely resemble other realistic situations. GPS latitude and longitude coordinates were mapped onto the tourist locations and cross checked with credit card and loyalty data to verify purchases and travel, identify typical patterns, and to detect outliers. Suspicious behavior emerged in the data sets which led to questions and further investigations. Several suspects were identified when detecting trends and outliers in the daily activities of the GAStech employees. Minke Mies engaged in several unusual patterns with outliers in both the card transaction data and the GPS locations, and thus, became the number one suspect who should be questioned first. People who were involved with Minke should be investigated next, including Hennie Osvaldo, Inga Ferro, Loreto Bodrogi, and Isia Vann. Lucas Alcazar was also identified as a main suspect since he participated in the outlier credit card transaction and was seen driving late at night to and from GAStech. The other events that came across as highly suspicious included the two employees sneaking to the hotel during the middle of the day, the gathering at the Carnero House on January 10th, and the meeting at Kronos Capital on January 18th. In total, researchers have identified twelve suspicious patterns with potential suspects and handed over their findings to local authorities. Geospatial visualizations, interactive mapping, and outlier detection were key to figuring out which patterns to pursue to help with the investigation. Hopefully, they catch these kidnappers soon! 

## CONTRIBUTORS
[(Back to top)](#table-of-contents)
<br>
### Nicole Menke
[![](https://github.com/nicolemenke.png?size=50)](https://github.com/nicolemenke)
