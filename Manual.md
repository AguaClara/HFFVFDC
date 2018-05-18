#**High Flow Float Valve**
###Alycia Storch, Julia Timko, Felix Yang

May 11, 2018

## Manual
###Introduction
The high flow float valve is designed to control the flow rate of water into the distribution tank. The distribution tank is the storage tank that contains clean water exiting the treatment plant before it is distributed to the community, and overflows when the tank is full. Overflow happens mainly during off-peak hours from midnight to dawn when demand is low. Avoiding overflow is desirable because any excess treated drinking water is wasted. To avoid this waste, the float valve will decrease the flow rate as the tank fills up.

That excess flow will instead back up the pipe system and begin to raise the elevation of water in the entrance tank within the plant. As soon as the plant operator sees that the water level is rising in the entrance tank, action can be taken to reduce flow coming into the plant.

The float valve consists of a slider pipe, a float on top of the slider pipe, a tee connected to the distribution tank inlet pipe, and bushings inside the tee that the slider pipe will slide through. The water entering the distribution tank will go through the tee and through the holes in the slider pipe that are within the tee. The more holes exposed, the higher the flow rate. As the tank fills up, the float will remain on the top of the water and will cause the slider pipe to rise, which will decrease the number of holes exposed within the tee. When the tank is full, no holes will be exposed within the tee and the flow will only be due to the leaking present within the float valve.

The High Flow Float Valve (HFFV) team was in charge of designing a generalized model for float valves in future plants. Initially, the team built a standard 2 inch diameter float valve to test in the lab. As the semester progressed, the team used this sample float valve to test the functionality of the design and develop a more standardized method of HFFV creation. The arbitrary decisions regarding measurements made at the beginning of the semester were necessary to develop and code design functions that the team wrote at the end of the semester.

<center><img src="https://raw.githubusercontent.com/AguaClara/float_valve/master/Pictures/schematic.png"></center>
<p>
    <em><center>This is a schematic diagram of the extreme positions of the float valve in the distribution tank.  </center></em>
</p>

###Fabrication Details
####Material List
| Part                    | Quantity/Size | Price in 2018 |
|:----------------------- |:-------------:|:-----------------:|
| 2" PVC Tee              |       1       |       $2.25       |
| 2" PVC Pipe             |     5 ft      |      $10.56       |
| 1.5" PVC Pipe           |     5 ft     |       $7.92       |
| 1" PVC Pipe             |     5 ft     |       $5.40       |
| 2" to 1.5" PVC Bushings |       2       |       $1.74       |
| 5/8" Hose Clamp         |       1       |       $8.34       |

All parts were bought from McMaster Carr.
###Tools needed
* Bandsaw
* Hackzall
* Drill Press or Cordless Drill
* Measuring tape and Calipers
* PVC Primer
* PVC glue
* Sandpaper

###Design Details
A lot of the fabrication decisions were done on assumptions that had no clear mathematical calculations behind them. After successfully fabricating an HFFV system, the team developed a more generalized and systematic approach for designing HFFVs at different scales by creating model design functions. This more methodical approach is found in the Generalized Approach section.

####Slider Pipe Length
The slider pipe length was designed with the intention of being able to operate between half capacity and full capacity of the distribution tank. This assumption led the team to fabricate a slider pipe that was approximately half the height of the distribution tank used in the experiment. This desired length of half the distribution tank height doesn't take into account the length that has to be added to the pipe including plugs that constrain movement of the pipe, and the float.

#####Total Length
<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/diagram%20of%20full%20pipe.jpg?raw=true"  height = 400></center>
<p>
    <em><center>This is a diagram of the full length of the slider pipe assembly.  </center></em>
</p>

<center>The total slider pipe length is determined by

$$PipeLength= Length_{Active}+2PlugClearance+\frac{OD_{slider pipe}}{2}
$$

where PlugClearance is the distance from the bottom of the sliderpipe to the center of the plug, $Length_{Active}$ is the length that the slider pipe can move, the second PlugClearance is the distance between the center of the top plug to the bottom of the triangular notch, and $OD_{sliderpipe}$ is the distance from the top of the slider pipe to the top of the float.

####Slider Pipe Hole Size and Pattern
Initially, the team intended for the pattern of the holes on the slider pipe to decrease as the pipe moved up. After designing and constructing a slider pipe with this reasoning, the team determined that it would be difficult to design a hole pattern that would make the flow rate linearly decrease with the water level. The team later decided to redesign the hole pattern and tee to accommodate this linearly decreasing flow rate requirement. This new design can be found in the Generalized Approach section.

For the initial design, the team developed a hole pattern constrained by a few parameters including available head, height of the distribution tank, and flow rate. The number and size of exposed holes is dependent on the flow rate, as higher flow rates require more, larger holes. The team standardized the size of the holes used to be $1/4 \mathrm{in}$ . The team considered these values for each of the other parameters:


* Available head: $1 \mathrm m - 2\mathrm m$
* Distribution Tank Height: $.75 \mathrm m$
* Flow Rate: $1 \mathrm L/\mathrm s$
* Pipe Diameter: $2 \mathrm {in}$

The above value for distribution tank height was the height of the large capacity bucket found in the lab. The flow rate was set as $1 \mathrm L/\mathrm s$ because that was the assumed maximum flow rate of the faucet in the lab. The team picked $2 \mathrm{in}$ diameter piping because that size was easily available in the lab.

$$MaxNumHoles = {TotalFlow \over FlowPerHole}$$

$$MaxNumHoles = {1 \mathrm L/\mathrm s \over .1 \mathrm L/\mathrm s} = 10 \ \mathrm {Holes}$$

After determining the maximum number of exposed holes needed, the team had to create a hole pattern that would decrease the flow as the float valve moved up. The team set the initial number of exposed holes to ten and decreased the number of holes with each row. Although it was later found that this did not in fact create a linearly decreasing flow effect, this was the basis for the float valve fabricated in the lab.

The team arbitrarily set the number of rows exposed at a given time to three. The team found the spacing between each of these rows by dividing the exposed space within the tee by 3, the number of rows exposed at a given time. This way, as one row would leave the tee, another would enter.

$$ RowSpacing = {HeightOfTeeExposed \over NumberOfRowsExposed \ \mathrm {Rows}}$$

$$ RowSpacing = {3.6875 \mathrm{in} \over 3 }= 1.229 \mathrm{in}$$

Using this row spacing, the team found it possible to fit seven rows on the slider pipe of the tee. By decreasing the number of holes every other row, the team created this hole patten in a fusion file:

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/HolePattern2.png?raw=true" height=300></center>

####Rate of Leakage
Rate of leakage is the flow rate of the HFFV into the distribution tank once it shuts off completely, exposing no holes to the tee. It is a parameter that is dependent on the area between the outer diameter of the slider pipe and the inner diameter of the bushing that surrounds it. It is determined by how much the bushings are sanded, something that the team was attempting to standardize. However, because of the initial condition for the HFFV be almost frictionless so that it could freely move vertically, the team had to determine the rate of leakage experimentally.

It is important because it determines how long the plant operator has to respond before the distribution tank overflows. For example, if the capacity of the distribution tank is 1000 Liters and the tank shuts off at 90% capacity and rate of leakage is .1 L/s, then the tank fills up in approximately 1000 seconds or 17 minutes. The rate of leakage was measured and recording in the Experimental Results section.

####Float size
To determine the length of the float, the team assumed there is negligible friction force between the slider pipe and the tee since the slider pipe can slide through the tee easily. The team also decided to aim for the water level to be at half the height of the float. This meant that the buoyant force has to support the weight of the top half of the float, the apparent weight in water of the bottom half of the float, and the apparent weight in water of the slider pipe. The team used the following equation to find the apparent weights in water:
$$ApparentWeight_{object}=Weight_{object}-\rho_{water}\cdot Volume_{object} \cdot g$$
where $\rho_{water}$ is the density of water and $g$ is acceleration due to gravity.
The team used these equations to solve for the length of the float:
$$BuoyantForce=\frac{1}{2}\cdot \pi \cdot (\frac{ID_{float}}{2})^2 \cdot L_{Float} \cdot \rho_{water} \cdot g$$

$$BuoyantForce=\frac{1}{2}Weight_{Float}+\frac{1}{2}ApparentWeight_{Float}+ApparentWeight_{SliderPipe}
$$
$$\frac{1}{2}Weight_{Float}=\frac{1}{2}\pi[(\frac{OD_{Float}}{2})^2-(\frac{ID_{Float}}{2})^2] \cdot L_{Float}\cdot \rho_{PVC}\cdot g$$
$$\frac{1}{2}ApparentWeight_{Float}= \frac{1}{2}\cdot Weight_{Float}-\frac{1}{2}Volume_{Float}\cdot \rho_{water}\cdot g $$
$$\frac{1}{2}Volume_{Float}=\frac{1}{2}\cdot (\frac{ID_{Float}}{2})^2\cdot \pi\cdot L_{Float}\cdot \rho_{water}\cdot g$$
$$ApparentWeight_{SliderPipe}= Weight_{SliderPipe}-Volume_{SliderPipe}\cdot \rho_{water}\cdot g$$
$$Volume_{SliderPipe}= \frac{Weight_{SliderPipe}}{\rho_{PVC}\cdot g}$$
$$ApparentWeight_{SliderPipe}=Weight_{SliderPipe}\cdot (1-\frac{\rho_{water}}{\rho_{PVC}}) $$

After combining these equations and solving for $L_{Float}$, the team got the following equation:
$$L_{Float}= \frac{4\cdot Weight_{SliderPipe}\cdot (1-\frac{\rho_{water}}{\rho_{water}})}{g\cdot \pi(ID_{Float}^2\cdot \rho_{water}-OD_{Float}^2\cdot \rho_{PVC}+ID_{Float}^2\cdot \rho_{PVC})} $$
In the team's case, the slider pipe was made first so the team could easily weigh it and plug the weight into the above equation. When this is not the case, the weight can be approximated by the weight of a PVC pipe of the same diameter and length with the following equation:
$$Weight_{SliderPipe}= \pi\cdot (OD_{SliderPipe}^2-ID_{SliderPipe}^2)\cdot L_{SliderPipe}\cdot \rho_{PVC}\cdot g $$
Plugging this into the equation for $L_{Float}$ gives:
$$L_{Float}= \frac{4\cdot \pi\cdot (OD_{SliderPipe}^2-ID_{SliderPipe}^2)\cdot L_{SliderPipe}\cdot \rho_{PVC}\cdot g\cdot (1-\frac{\rho_{water}}{\rho_{water}})}{g\cdot \pi(ID_{Float}^2\cdot \rho_{water}-OD_{Float}^2\cdot \rho_{PVC}+ID_{Float}^2\cdot \rho_{PVC}))} $$

With an earlier model of the Float Valve, the tee was not frictionless so the team determined the float size by testing the friction force between the slider pipe and tee. Normally, there are calculations that can be used to find the friction between two smooth pipes. However, because the bushings needed to be sanded down, they were not completely smooth and the equation would not be accurate for this setup. The team used a spring available in the lab to test and estimate the force of friction exerted by the slider pipe assembly.

First, the team found the spring constant $k$ of the spring by hanging a weight off the spring and measuring the change in length from it's original orientation.

$$ F=k\cdot \Delta(x) $$
$$k= \frac{F}{\Delta(x)} $$
$$ k =229.8 N/m $$

Then the spring was held in one end of the pipe and pulled, and the change in distance of the spring was measured. Finally, the team measured the friction force by multiplying the $k$ determined in the previous step and the change in distance recorded. The team converted this force to the mass of the float by dividing by the force of gravity.

$$ F=k\cdot \Delta(x)= 229.8N/m \cdot .03313m= 17.67 N $$
$$ \mathrm{Mass}_{\mathrm{Float}}=\frac{F}{9.81 m/s^2} = 1.76 kg$$

The buoyant force has to overcome the friction force in order for the float to move up and down smoothly. The team found the volume of the float by dividing the mass of the float by density of water, then dividing that volume by the cross-sectional area of the desired pipe to get length.

$$\mathrm{Volume}_{\mathrm{Float}}=\frac{\mathrm{Mass}_{\mathrm{Float}}}{\rho_{\mathrm{water}}}=\frac{1.76kg}{1000kg/m^3}=.00176m^3   $$
$$L_{\mathrm{Float}}= \mathrm{Volume}_{\mathrm{Float}}/\mathrm{Area}_{\mathrm{Float}}=\frac{.00176m^3}{3.142 in^2}=35.05$$
From here, the length of 36" was used, because 35" was the bare minimum to overcome the friction force.

###Procedure

The High Flow Float Valve team assembled a 2" float valve in order to test the model's functionality and ease of fabrication. In the future, there will be 3 different size HFFV models, (2 in, 4in, and 8in) each requiring the same fabrication methods, but at larger scales. For now, the team fabricated the smallest scale HFFV, which has a 2" diameter tee and 1.5" diameter slider pipe. The procedure involved the construction of three distinct parts: the slider pipe, the tee, and the float. HFFV only fabricated and tested the small scale design as the original intention of the team was only to test the feasibility of fabricating such a device.

####Slider Pipe

The slider pipe requires a notch at the top of the pipe to fit a float, holes in the active length portion of the pipe (the range of the slider pipe where it can be exposed to the tee) to allow water to pass, and holes for a hose clamp to secure the float and for plugs to constrain the active length. The team started fabrication by cutting a piece of 1.5" diameter pipe to 41cm using the table clamp and the reciprocating saw. This length was calculated in the section above.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/active%20length.jpg?raw=true"  height = 300></center>
<p>
    <em><center>The photo on the left shows the pipe in the closed position while the photo on the right shows the pipe in the open position. The length of pipe that the tee is able to move through is called the active length. </center></em>
</p>


The team then used the bandsaw and the angle alignment tool to produce two cuts in the top of the pipe to form a notch as shown below.  This notch was used to secure the float to the pipe with a hose clamp later. The angles used to cut were 45 degrees. However, it was not necessary that this measurement be extremely precise, because the notch simply serves as a holding space for the float.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/TopOfSliderPipe.png?raw=true"  height = 300></center>
<p>
    <em><center>Picture of the top of the slider pipe with the notch cut into it to hold the float in place.</center></em>
</p>


The team then used a template created from the Fusion design to accurately drill the holes in the slider pipe. The team printed the template and punctured small holes through the centers of each hole on the paper. The team then laid this template around the slider pipe and drew marks on the slider pipe through the small holes to indicate where to drill. The team aligned the template so that the distance from the bottom hole to the top of the plugs was the height necessary according to the equation below:

$$
H_{\mathrm{FirstHole}} = H_{\mathrm{FirstPlug}} + R_{\mathrm{Plug}} + (H_{\mathrm{Tee}} - H_{\mathrm{Bushing}})$$

$$H_{\mathrm{FirstHole}} = {1 \over 2} \mathrm{in} + {1 \over 4} \mathrm {in}+ (5 {11 \over 16} \mathrm{in} - 1\mathrm{in} )$$

$$H_{\mathrm{FirstHole}} = 5 {7 \over 16} \mathrm{in}$$

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/HolePattern2.png?raw=true" height=300></center>

<p>
    <em><center>CAD drawing of the hole pattern on the slider pipe. </center></em>
</p>

The team then cut holes according to the markings on the pipe using the drill press fitted with a 1/4" drill bit as determined by the calculations in the Design Details section.


<center><img src= " https://github.com/AguaClara/float_valve/blob/master/Pictures/Marking%20pipe%20for%20holes.JPG?raw=true" height = 300> <img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Drilling%20holes.JPG?raw=true" height=300></center>

<p>
    <em><center>Marking drilling locations on the pipe and using the drill press to cut those holes. </center> </em>
</p>

####Tee

Next, the team cut each of the PVC bushings to 1" in height using the band saw. These were cut because it allowed for more space available in the tee to be exposed to holes.

<center><img src="https://raw.githubusercontent.com/AguaClara/float_valve/master/Pictures/bushings_before_cut%20copy.jpg" height=300><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Bushing%20about%20to%20be%20cut.jpg?raw=true"  height = 300> </center>
<p>
    <em><center> Bushings are shown on the left with marks drawn on them as a guide for bandsaw cuts.</center> </em>
</p>

\
The team then created a handmade sanding tool. This tool was made from an arbitrarily long 1" PVC pipe with a thick piece of sandpaper PVC-glued around its circumference.

 <center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Sander.JPG?raw=true" height=300></center>
 <p>
     <em><center>The team used a handmade sanding tool to sand down the inside of the bushings. It consisted of pipe with a piece of sandpaper glued around it. </center></em>
 </p>

\
The team then used the tool shown above, as well as a handheld file, to sand down the inside of the bushings so that the 1.5" pipe could slide easily through. The initial fabrication of the bushings had enough friction force to hold the tee up like shown in the picture below. However, it was then sanded to the point that the tee could fall freely. This was done so that during operation the slider pipe would be able to slide vertically in accordance with the water level.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/SandingPipe.png?raw=true" height=300> <img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/SliderPipeNoHoles.JPG?raw=true" height = 300></center>
<p>
    <em><center> The team spent ten minutes sanding down the bushings to their desired width. On the right is a photo of the pipe sitting in the sanded tee.  </center></em>
</p>

####Float
Originally, the team incorrectly calculated the dimensions for a smaller sized float. The frictional force that the smaller size float supported was 13.25 N while the measured friction force was 17.67 N. The first set of instructions were kept under subsection "Smaller Float" so that, given a better sanded tee with a smaller friction force, a procedure for fabrication is available.


#####Smaller Float

To create the 1" float, the team cut 1" PVC pipe into 3, 13" pieces using the bandsaw and hackzall and glued a strip of PVC sheet that was cut using the bandsaw to either end of all three pipes, with 1" arbitrary spacing between each pipe. The team used this design because, after calculating the required length of the float had it been just one pipe, it was clear that it would be too long for proper function both in the tank the team is using for testing and in the distribution tank itself. By using three pipes instead of one, the team was able to decrease the overall length of the float by three, which better accommodates the testing tank.

The team originally found that a float of just one 1" diameter pipe would have to be 35.05" long. To get the length for the three-pipe float the team simply divided by three to get an approximate length of 12" and decided to round up to 13" to account for any errors made in finding the required buoyant force. The team chose to overestimate the length instead of underestimate to make sure the buoyant force of the float would be large enough to support the weight of the float valve.

The spacing between the pipes was required because the center float pipe was hose clamped to the top of the slider pipe and part of the notch at the top of the slider pipe would block the other two pipes had there not been space between them. In the 2" float spacing between pipes is not required because the 2" pipes are big enough that the notches on the top of the slider pipe is no longer in the way.


<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/1%20inch%20float%20vs%202%20inch%20float.jpg?raw=true" ></center>
<p>
    <em><center>The picture on the left shows the original 1" diameter float setup. In the middle and on the right is the float using 2" diameter PVC pipe.  </center></em>
</p>

#####Correctly-Sized Float for Bushings with Friction

To create the 2" float, a similar procedure was used to cut them to the same length, requiring the team to cut 2" PVC pipe into 3, 13" pieces using a bandsaw and hackzall. However, because of this, the larger size spacing between the float was not required, because the lip was no longer in the way for the 2" size. For the 2" caps, the team used a 2 1/2" hole saw in the drill press to cut six circular pieces out of PVC sheet. These pieces were glued to both ends of each pipe to seal them for use as floats.

####Final assembly
After putting the float, slider pipe, and tee together, the team completed the experimental setup. Below is a picture of the complete assembly.
<center><img src="https://raw.githubusercontent.com/AguaClara/float_valve/master/Pictures/complete.jpg" height= 300></center>
<p>
    <em><center> This is the full assembly sitting outside of the testing tank.   </center></em>
</p>


###Experimental Setup
Our experimental setup consisted of the sink apparatus and the slider pipe assembly. It was important to realistically replicate the setup of a plant distribution tank and water route in order to test the slider pipe assembly that was built. The team was principally testing to evaluate functionality of the float valve and adjusted the designs based on what they gathered from the trials ran. Additionally, testing was done to find the leak rate of the apparatus and to see if the float was large enough to support the weight of the slider pipe.

####Materials List
| Part                            | Quantity |       Size        | Price in 2018 |
|:------------------------------- |:--------:|:-----------------:| ------------- |
| Flexible Tubing                 |   5 ft   |    1" diameter    | $7.35         |
| Hose clamp                      |    1     |    2" diameter    | 10 for $7.17  |
| Barbed PVC Fitting NPT Male End |    1     |    1" diameter    | $1.97         |
| PVC Tee                         |    1     |    1" diameter    | $0.81         |
| PVC Elbow                       |    1     |    1" diameter    | $0.61         |
| PVC Elbow                       |    1     |    2" diameter    | $1.82         |
| PVC Bushing                     |    1     | 2" to 1" diameter | $1.74         |
| PVC Coupling                    |    1     |    2" diameter    | $1.09         |
| PVC Pipe                        |  3" x 3  |    2" diameter    | $16.00        |
| PVC Pipe                        |   4 ft   |    1" diameter    | $5.40         |
| PVC Coupling                    |    1     |    1" diameter    | $0.48         |
| Fernco Fitting                  |    1     |    2" diameter    | $4.71         |
| Clear PVC Pipe                  |   2 ft   |    2" diameter    | $23.38              |

All parts ordered from McMaster Carr.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/setup2.png?raw=true" height= 600></center>
<p>
    <em><center> The experimental setup required a flow of water from the sink faucet that travelled past a PVC tee and into the distribution tank.  </center></em>
</p>

####Water Flow
In order to determine the flowrate of the water out of the sink, the team had to test the time it took for a flow to fill a bucket. The bucket was marked with the level of 3 liters, so the team found the right position of the faucet knob that would fill up to the 3 liter mark in 3 seconds, hereby ensuring a flow rate of 1L/s.


####Water Route
The team then took a piece of 1" diameter flexible tubing and used a hose clamp to secure it to the faucet. This flexible tubing connected via a barbed fitting to a 1" diameter pipe on a raised platform. The team raised this portion in order to deliver more head upon entering the distribution tank. At the top of this platform, the team inserted a 1" tee. The team then connected the clear PVC pipe to the free end of this tee. The tee exposed the water to atmospheric pressure to eliminate pressure head, and the clear PVC pipe was attached to prevented the water from spilling out. It was important to eliminate pressure head in order to get a consistent measurement of the head and pressure of the water entering the system. As the float began to rise and the holes in the slider pipe closed off, the head that was needed to push water through the HFFV began to build up. Although the flow began each trial at a rate of 1 L/s, the team adjusted the flow rate of the sink during the trial to keep a constant head of water entering the system.


The tee then led into a 1" elbow that diverted the water down into a 3' long 1" pipe. The team expanded this 1" pipe by using a 1" diameter to 2" diameter bushing. Then a 2" elbow was used to get the water to flow horizontally into the float valve tee. Between the elbow and the tee were two small pieces of 2" diameter PVC, which were connected by a Fernco fitting. One end was glued into the elbow, while the other was glued into the tee of the float valve. The team used a Fernco fitting so that the float valve would not be permanently attached to the experimental setup and could be removed if needed. The team positioned the float valve roughly in the center of the tank, both vertically and horizontally. It was centered vertically to allow for the largest range of motion of the slider pipe. It was centered horizontally within the tank to ensure that the float did not hit the sides of the tank.


<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/constant_head_chamber.png?raw=true" height= 300></center>
<p>
    <em><center> This photo shows the top of the experimental apparatus and shows the flow of the water through the pipes. The water comes from the faucet and into the top pipe where it either continues to enter the slider pipe assembly or builds up pressure in the head chamber. </center></em>
</p>


###Experimental Results
After running trials with the fabricated float valve, the HFFV team found that, given enough sanding, the valve moved freely in the vertical plane. However, three main things were taken into further consideration. These were the float size, the leak rate, and the amount of head.

In regards to float size, the team had to try multiple iterations until finding a float size that worked. Ultimately, the team coded a function returning the length of the necessary float size and was able to fabricate a working float based on this calculation, which was covered in the Design Details section.

As mentioned before, the leak rate was a value that the team could only measure experimentally. The team found the leak rate for the system built in the lab and later generalized that leak rate to future float valves. The leak rate for the sample fabricated system was determined by running the system with the valve in its closed position. The flow rate out of the faucet was adjusted in order to keep the water in the head chamber at a constant height. This meant that pressure going into the system was kept constant, meaning that the flow rate out of the faucet was equal to the leak rate of the float valve. The team calculated this flow rate as $.06 \mathrm {L / s}$. The generalized equation and the process the team went through to develop that equation can be found in the Generalized Approach section.

The last experimental finding was in regards to the amount of head entering the system. It was found that more head would increase the velocity of the water moving through the float valve and therefore increase the flow rate. Because of this, the team recognized the necessity of including the head as a variable in the design function for the float valve. The flow rate, pipe diameter, and number of holes are all dependent on the head and therefore this value cannot be ignored.

###Generalized Approach
####Introduction
The experimental portion of our research this semester was in an effort to test fabrication methods and functionality of the overall design. Because of this, the most significant findings are in the more generalized calculations below. The designs in this section have been revised since the team's original conception of the float valve to be more universal and easy to construct. Although the team tried to take into account all important parameters, there are a few more design considerations that have to be addressed. Those will be discussed in the Future Work section.

The main difference between the experimental design and the reimagined design, is that in the new design the slider pipe no longer runs through the tee exposing new holes. All holes through which water can flow are exposed within the tee at the beginning and leave the tee in order to decrease the flow. This changes the pattern of holes on the slider pipe, as well as the overall lengths of the tee and the slider pipe. These changes will be discussed below.

#### Design Scale Flow Rate Ranges
The original flow rate that HFFV was tasked to design for was 20 L/s but after doing calculations the team determined how to scale up and down the HFFV system based on the design flow rate.

The HFFV was designed to accommodate three different scales for three ranges of flow rates. The team determined these designs by using the minor headloss equation to find the maximum flow rate that different tee sizes could handle. First, the team solved for velocity given the available head. Then, the team found the flow rate Q as a result of the given area of the tee. The available headloss was assumed to be 1m because that was the amount of head available for the 20 L/s plant that the HFFV team assigned to create a design for.


$$\frac{V^2}{2g}=Head_{Availible}$$
$$V=\sqrt{2gHead_{Availible}}=3.132 m/s$$
$$Q=VA_{Tee}$$
$$Q_{2 in}=VA_{2in}=3.132m/s\cdot .02m^2=6.34 L/s\approx6L/s$$
$$Q_{4 in}=VA_{4in}=3.132m/s\cdot .08m^2=25.4 L/s\approx25L/s$$
$$Q_{8 in}=VA_{8in}=3.132m/s\cdot .32m^2=101.6 L/s\approx100L/s$$


####Pipe sizing

Using these max flow rates, the team determined the ranges for three different sizes of pipe: 1L/s to 6 L/s, 6L/s to 25L/s, and 25L/s to 100 L/s. If additional head were available, the ranges for each of the scales would be larger due to the higher velocity of water running through the tee.

The pipe sizing that will be associated with each of these ranges will be the following.

**1L/s to 6 L/s** : 2 inch tee and 1.5 inch slider pipe and float

**6L/s to 25L/s** : 4 inch tee and 3 inch slider pipe and float

**25L/s to 100 L/s** : 8 inch tee and 6 inch slider pipe and float

####Active Length
The active length is a variable that the team used to represent the length of pipe exposed in the tee at a given time. This length is space available to fill with holes. Because all possibly exposed holes will begin inside of the pipe, half of the slider pipe will be  covered in holes and the other half will be solid. This length is the active length. The active length is roughly 1/3 the overall height of the distribution tank.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/New%20DIstribution%20Tank.png?raw=true" height= 800></center>
<p>
    <em><center> This diagram shows the new distribution tank setup.   </center></em>
</p>

The reason why the active length is not exactly 1/3 the height of the distribution tank, is because there are limitations to the height that the slider pipe can travel. Because the slider pipe has the float on top, plugs on the bottom, and bushings within the tee, there is dead material on the top and bottom that restricts it's travel. Because of this, the active length is 1/3 the height once those lengths of extra material are subtracted.

$$ ActiveLength = {Height_{Distribution \ Tank} - ExtraBottomMaterial - ExtraTopMaterial - 2 \cdot Bushing Height\over 3}
$$


The $ExtraBottomMaterial$, $ExtraTopMaterial$, and $BushingHeight$ are all determined by the size of the slider pipe being used. This means that the active length can be calculated given just the distribution tank height and the diameter of the slider pipe.


####Slider Pipe Length
Once the active length of the tank has been determined, the length of the slider pipe can be found. The length of the slider pipe is roughly twice the active length. The top half of the slider pipe is the area where holes can be drilled, and the bottom half is solid. As the slider pipe moves up, less holes are exposed.



<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/New%20Slider%20Pipe.png?raw=true" height= 800></center>
<p>
    <em><center> This diagram shows the new layout of the slider pipe.  </center></em>
</p>

The actual length of the slider pipe is slightly longer than twice the active length in order to account for the extra material on the top and bottom. The height of the float is subtracted in this equation in order to calculate the length of the slider pipe without the float attached.


$$ SliderPipeLength = 2 \cdot ActiveLength + ExtraBottomMaterial + ExtraTopMaterial + 2 \cdot Bushing Height - FloatHeight
$$

As demonstrated before the $ActiveLength$ depends on the height of the distribution tank and slider pipe diameter while the $ExtraBottomMaterial$, $ExtraTopMaterial$, $BushingHeight$, and $FloatHeight$ only depend on the slider pipe diameter. This means the slider pipe length can be calculated with just distribution tank height and the slider pipe diameter.

####Hole Sizing

As the HFFV scales up, hole diameter size increases in order to accommodate the extra flow. These sizes were determined by testing how much flow would come out of an orifice and capping the maximum number of holes exposed to the tee at 75 holes. The team capped this as the maximum number of holes because too avoid having too many holes, which would make fabrication difficult and compromise the structural integrity of the slider pipe.  The team used the flow orifice equation shown below.

$$ Q=\pi\cdot A\cdot \sqrt{2gh}=\frac{\pi_{vc} d^2\pi\sqrt{2gh}}{4}$$

where $\pi_{vc}$ is the vena contract coefficient (typically .62), $Q$ is the target flow rate which is $1\over 10$th the plant's flow rate, $A$ is the slider hole area that is being considered and $h$ is the amount of head available.

$$ Q_{1/4in} = 0.08696 liter / second$$

This means that out of one 1/4"orifice, approximately .09 L/s can flow. Dividing the ranges of plant flow rates in the 2 inch HFFV system gives the following:

$$ Number Holes_{Max}=\frac{6L/s}{Q_{1/4in}}=69$$
$$ Number Holes_{Min}=\frac{1L/s}{Q_{1/4in}}=11.5$$

This fulfills our constraint that maximum number of holes has to be below 75. Therefore, size .25" holes are appropriate for the 2 inch diameter tee HFFV system. Similar calculations were done for .5" and 1" holes.

$$ Q_{1/2in} = 0.35 L/s$$

This means that out of one 1/2" orifice approximately .35 L/s can flow. Dividing the ranges of plant flow rates in the 4 inch HFFV system gives the following:
$$ Number Holes_{Max}=\frac{25L/s}{Q_{1/2in}}=72$$
$$ Number Holes_{Min}=\frac{6L/s}{Q_{1/2in}}=17$$

Thus, for the 4 inch HFFV systems, 1/2" holes will be used in the slider pipe.

$$ Q_{1in} = 1.391 L/s$$
This means that out of one 1" orifice, approximately 1.391 L/s can flow. Dividing the ranges of plant flow rates in the 8 inch HFFV system gives the following:
$$ Number Holes_{Max}=\frac{100L/s}{Q_{1in}}=72$$
$$ Number Holes_{Min}=\frac{25L/s}{Q_{1in}}=18$$
Thus for the 8 inch HFFV systems 1" holes will be used in the slider pipe.

####Hole Pattern
The hole pattern in the generalized approach is designed with the idea of simplicity in mind. Only the top half of the slider pipe will have holes, which is the active length. The tee will be the same length as the active length so that when the slider pipe is completely down all the holes are exposed and as the slider pipe moves up, holes leave the tee but no new holes enter. This allows for a more linear decrease in flow as the slider pipe rises with the water level.

To get the hole pattern for a given flow rate, the number of holes necessary for full flow out of the slider pipe is needed. This is found by dividing the flow  rate coming into the slider pipe by the flow rate out of one hole.
$$Q_{OneHole}= \pi_{vc}\cdot A_{hole}\cdot \sqrt {2gh}$$
$$NumberHoles= Q_{Plant}/Q_{OneHole} $$

The team decided to standardize the spacing between each row of holes to be four times the diameter of the holes. The number of rows is then found by dividing the active length by the row spacing and rounding down to the nearest integer. The approximate number of holes per row is then found by dividing the number of holes by number of rows and rounding down to the nearest integer. The remaining holes that were left out because of rounding down are then distributed into the rows one hole and one row at a time, starting with the top row, until there are no more extra holes remaining.
$$Spacing_{Row}=4\cdot D_{Hole}$$
$$NumberRows= floor(ActiveLength/Spacing_{Row})$$
$$HolesPerRow= floor(NumberHoles/NumberRows)$$
$$RemainingHoles=NumberHoles- NumberHolesPerRow\cdot NumberRows$$

If the flow rate is small enough that the number of holes needed is less than the number of rows, then the row spacing is no longer four times the hole diameter. Instead, the active length is divided by the number of holes and this is the new row spacing and there is one hole per row so that the holes span the entire active length.
$$Spacing_{Row}= Length_{Active}/NumberHoles $$
####Rate of Leakage

Since the entrance and exit points in the tee that the slider pipe goes through are not water tight, there is some leakage through those spaces when the float valve closes. This leakage is impossible to eliminate if the slider pipe is to slide freely. Since the purpose of the float valve is to prevent the distribution tank from overflowing, the team needed to ensure that the leak rate would not overfill the tank during the 8 off-peak hours from midnight to 8am. Because the leak rate is solely dependent on the amount of head available and the gap through which the water is leaking, the team was not able to change the amount of $Q_{leak}$. However, the layout of the holes in the slider pipe are dependent on the rate of leakage and have to be positioned precisely. The slider pipe should turn off the flow when the water level is at a height that would allow the leaking slot to fill the rest of the distribution tank in the given 8 hours.

The team calculated the relationship between the area of the slot through which the water was leaking and the flow rate of the water going through using the following equation.

$$Q_{leak} = V \cdot A_{vc}$$
$$A_{vc} = A_{slot} \cdot \pi _{vc}$$
$$Q_{leak} = \sqrt{2gh_L} \cdot A_{slot} \cdot \pi_{vc}$$
$$A_{slot} = {Q_{leak} \over \sqrt{2gh_L} \cdot 2 \cdot \pi_{vc}}$$

$V$ is the velocity of the water, $A_{VC}$ is the area of the vena contracta, or the slot through which the water is leaking, $h_L$ is the height of the head, and $\pi_{VC}$ is the vena contracta coefficient, which was estimated as 0.62. Given this formula and an experimental measurement of the leak rate, the team found the area of the slot for the specific experimental apparatus. However a more general solution was sought to estimate leak rates based on design parameters rather than estimate the area of the slot based on experimental data.

The area and width of the gap is dependent on the pipe sizing of the inner diameter of the bushing ,$ID_{B}$, and outer diameter of the slider pipe, ${OD_{Slider Pipe}}$. Depending on the magnitude of the difference between these two measurements the area, $A_{slot}$, and width, $W_{gap}$, will be greater or smaller. The major problem with generalizing the leak rate is that it is hard to standardize how large this gap will be. This is because the method that is used to sand the bushing is not exact, so the $ID_{B}$ has to be determined using the equations below. Slider pipe outer diameter was determined using Mcmaster measurements.

$$A_{slot} = {\pi \over 4} \cdot (ID_{B}^2 - OD_{Slider_Pipe}^2)$$
$${4 \cdot A_{slot} \over \pi} = ID_{B}^2 - OD_{Slider_Pipe}^2  $$
$$ID_{B}= \sqrt {{4 \cdot A_{slot} \over \pi}+OD_{Slider_Pipe}^2 }$$
$$ID_{B} = 4.84 cm $$
$$W_{gap} = {ID_{B} - OD_{Slider_Pipe} \over 2}$$
$$W_{gap} = {4.84-4.826 \over 2} = .007 cm $$

Assuming that this gap width for all future float valves stays constant, the flow rate of leakage can be estimated given the amount of head available, the inner diameter of the sanded bushing, and the outer diameter of the slider pipe.

$$Q_{leak} = 2 \cdot{ \sqrt{2gh_L} \cdot {\pi \over 4} \cdot (ID_{B}^2 - OD_{Slider_Pipe}^2) \cdot \pi_{vc}}$$

The coefficient 2 is in front because there are two locations where there are leaks: at the top and bottom of the tee.


###Future Work
The team identified a few areas that would need future work in order to complete the High Flow Float Valve system. The first factor the team wanted to address, was that during the experimental process, the team had a difficult time ensuring that the float valve was exactly vertical to the ground. The float valve tended to bend and sag a little bit, meaning that the slider pipe was not vertical. This caused more friction within the tee and made it harder for the slider pipe to slide smoothly upward as the water level rose. In order to solve this problem in an accurately-sized plant, the team suggests that several brackets be used to hold the inlet tube securely to the wall of the distribution tank. This should prevent the slider pipe assembly from sagging downward.


The team was working on generalizing a hole pattern for the original design of the float valve when the second design came to fruition. Since there are pros and cons to both designs, finishing generalizing the hole pattern and writing code that gives the hole pattern based on flow rate, head, and the height of the distribution tank would be the next step for the original design.

Since the team started working on the second design near the end of the semester, it was never actually fabricated or tested. This should be the next step for this design. The elongated tee is a component that is especially important to fabricate and test since it is fairly unique from the original design and requires multiple parts. Additionally, experimental results that were used in the design such as the rate of leakage are all from experimenting with the original design so it is important to see if these things change with the second design.



Further down in the design process, the team suggests that the float valve design be expanded to include pressure breaks. Currently, the design will not work as seamlessly as intended if there is too much head entering the system. If pressure breaks with individual, smaller float valves were installed periodically along the path to the distribution tank, then the overflow signal would pass up the path and alert the plant operator. This design would most likely vary based on the plant, but would be one step in taking the float valve design to the next stage of the design process.

###Conclusion
The High Flow Float Valve team was assigned with the task of designing a float valve that would alter the flow rate of the filtered water into the distribution tank as the tank filled. A float valve is a necessary upgrade to AguaClara plants, because there is currently a lot of clean water being wasted when distribution tanks overflow. After building a small-scaled experimental float valve, the HFFV team was able to better design a general float valve model for future distribution tanks. This design relies solely on the flow rate of the plant, the head upon entering the distribution tank, and the height of the distribution tank. The team based this design off of the small-scale HFFV built in the lab. However, a full-scale float valve would have to be built to test the team's findings.

The team has been in close contact with AguaClara engineers in Honduras during this design process. The findings from this report will be shared with the AguaClara engineers so the float valve design can be tested and hopefully implemented in AguaClara plants.
