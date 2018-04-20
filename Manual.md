#**High Flow Float Valve**
###Alycia Storch, Julia Timko, Felix Yang

<div class="alert alert-block alert-danger">
Please do not delete my comments from the report. Just address them and next time I will check that you have fixed these things. If you disagree with any of them, add your own comment with your reasoning below it. (Or if they are distracting, then save a copy of this and label it as your first draft and remind me that you did that when you submit next).
</div>

## Manual
###Introduction
The high flow float valve will control the flow rate of water into the distribution tank. The distribution tank is the storage tank for clean water exiting the treatment plant before it is distributed to the community, and overflows when the tank is full. Overflow happens mainly during off-peak hours from midnight to dawn when demand is low. Avoiding overflow is desirable because the excess treated drinking water is wasted. To avoid the tank overflowing, the float valve will decrease the flow rate as the tank fills up.

The float valve consists of a slider pipe, a tee connected to the distribution tank inlet pipe, a float on top of the slider pipe, and bushings inside the tee that the slider pipe will slide through. The slider pipe has an increasing number of holes from bottom to top. The water entering the distribution tank will go through the tee and through the holes in the slider pipe that are within the tee. The more holes exposed, the higher the flow rate. As the tank fills up, the float will remain on the top of the water and will cause the slider pipe to rise, which will decrease the number of holes exposed within the tee. When the tank is full, no holes will be exposed within the tee and the flow will stop.

<div class="alert alert-block alert-danger">
In the first sentence, consider lower case "high flow float valve" as it is not a proper noun here. Also consider "The high flow float valve will control" rather than "serve to control." Also what is the "distribution tank," and when does it overflow? Distribution tank to me means the final tank after the full treatment train, but before going out to the community. Explanation in the final three sentences is very good. Not enough connection as to why is it bad is the distribution tank overflows.

addressed - felix
</div>

###Fabrication Details
####Material List
| Part                    | Quantity/Size | Price at the time |
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

<div class="alert alert-block alert-danger">
Please include source (i.e. McMaster Carr) and the approximate unit price in the table. Consider adding a table of tools needed for fabrication as described in your procedure. (Include the sandpaper, saws, extra PVC for sanding tool etc.)

addressed - Aly
</div>

###Design Details
#### Design Scale Flow Rate Ranges
The HFFV was designed to accommodate three different scales for three ranges of flow rates. The team determined these designs by using the minor headloss equation to find the maximum flow rate that different tee sizes could handle. First, the team solved for velocity given the available head. Then, the team found the flow rate Q as a result of the given area of the tee. The available headloss available was assumed to be 1m.

$$\frac{V^2}{2g}=Head_{Availible}$$
$$V=\sqrt{2gHead_{Availible}}=3.132 m/s$$
$$Q=VA_{Tee}$$
$$Q_{2 in}=VA_{2in}=3.132m/s*.02m^2=6.34 L/s\approx6L/s$$
$$Q_{4 in}=VA_{4in}=3.132m/s*.08m^2=25.4 L/s\approx25L/s$$
$$Q_{8 in}=VA_{8in}=3.132m/s*.32m^2=101.6 L/s\approx100L/s$$

Using these max flow rates, the team determined the ranges for three different sizes of pipe: 1L/s to 6 L/s, 6L/s to 25L/s, and 25L/s to 100 L/s. If additional head were available, the ranges for each of the scales would be larger due to the higher velocity of water running through the tee.


####Slider Pipe Length
The slider pipe length depends on the height of the distribution tank and the tee used in the apparatus. It is the sum of the length of the tee and the space free for the pipe to move below the tee.

#####Active Length
The active length is the portion of the slider pipe that slides through the tee, from the bottom plugs to the top plugs. The active length is

$$ActiveLength=\frac{Height_{tank}-TopExtraMaterial-BottomExtraMaterial}{2} +{Height_{tee} \over 2}$$


where $Height_{tank}$ is the height of the distribution tank, $TopExtraMaterial$ is the length from the top plugs to the top of the float, and $BottomExtraMaterial$ is the length from the bottom plugs to the bottom of the float. This is the active length because the slider pipe should be able to span the length from a distance of $BottomExtraMaterial$ from the bottom of the tank to a distance of $TopExtraMaterial$ from the top of the tank. Half the height of the tee is added because there must always be pipe within the tee, so the length of the tee is part of the pipe length when the valve is both open and closed.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/diagram%20of%20float%20attached%20to%20pipe.jpg?raw=true"  height = 300></center>

The value of TopExtraMaterial is
$$TopExtraMaterial= OuterDiameter_{float}*(1+\sqrt{2})+PlugClearance$$
where $PlugClearance$ is the amount of space left between the center of the plug and the edge of the pipe. The team decided to leave half an inch of space between the bottom of the bottom plugs and the bottom of the slider pipe, as well as the top of the top plug and the top of the slider pipe directly above the plugs. With 0.5" diameter plugs, this gives a $PlugClearance$ of 0.75". To find $TopExtraMaterial$, the distance from the top plugs to the top of the float is needed. From the top plugs to the bottom of the notch in the top of the slider pipe is the $PlugClearance$. Using the fact that the angle of the notch is 45º, from the bottom of the notch to the center of the float is $\sqrt{2}\frac{OuterDiameter_{float}}{2}$ and from the center of the float to the top of the float is $\frac{OuterDiameter_{float}}{2}$.

The value of $BottomExtraMaterial$ is the distance from the bottom plugs to the bottom of the slider pipe which is equal to $PlugClearance$.

#####Total Length
<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/diagram%20of%20full%20pipe.jpg?raw=true"  height = 300></center>

The total slider pipe length is
$$PipeLength= ActiveLength+BottomExtraMaterial+PlugClearance+\frac{OuterDiameter_{slider pipe}}{2}
$$
because from the bottom to the bottom plugs is $BottomExtraMaterial$, then from the bottom plugs to the top plugs is $ActiveLength$, from the top plugs to the bottom of the notch is $PlugClearance$, and from the bottom of the notch to the top of the notch is equal to the outer radius of the slider pipe by geometry.


####Slider Pipe Hole Size and Pattern
The team was constrained by a couple of parameters including available head, height of the distribution tank, and flow rate. The number and size of exposed holes is dependent on the flow rate, as higher flow rates require more, larger holes. The goal was to solve for  slider pipe hole diameter and number of holes given the following parameters of the plant in Honduras.

* Available Head: 1m - 2m
* Height of distribution tank: 1.83 m or 6 ft
* Flow rate: 20 L/s

As the HFFV scales up, hole diameter size increases. These sizes were determined by testing how much flow would come out of an orifice and capping the maximum number of holes exposed to the tee at 75 holes. The team capped this as the maximum number of holes, because having too many holes would make fabrication difficult and would risk not having enough space in the tee to fit all holes. The team used the flow orifice equation shown below.

$$ Q=\pi*A*\sqrt{2gh}=\frac{\pi_{vc} d^2\pi\sqrt{2gh}}{4}$$

where $\pi_{vc}$ is the vena contract coefficient (typically .62), $Q$ is the target flow rate which is $1\over 10$th the plant's flow rate, $A$ is the slider hole area that is being considered and $h$ is the amount of head available.
$$ Q_{1/4in} = 0.08696 liter / second$$
This means that out of one 1/4"orifice, approximately .09 L/s can flow. Dividing the ranges of plant flow rates in the 2 inch HFFV system gives the following:
$$ Number Holes_{Max}=\frac{6L/s}{Q_{1/4in}}=69$$
$$ Number Holes_{Min}=\frac{1L/s}{Q_{1/4in}}=11.5$$
This fulfills our constraint that maximum number of holes has to be below 75. Similar calculations were done for .5" and 1" holes.

$$ Q_{1/2in} = 0.35 L/s$$

This means that out of one 1/2" orifice approximately .35 L/s can flow. Dividing the ranges of plant flow rates in the 4 inch HFFV system gives the following:
$$ Number Holes_{Max}=\frac{25L/s}{Q_{1/2in}}=72$$
$$ Number Holes_{Min}=\frac{L/s}{Q_{1/2in}}=17$$

Thus, for the 4 inch HFFV systems, 1/2" holes will be used in the slider pipe.

$$ Q_{1in} = 1.391 liter / second$$
This means that out of one 1" orifice, approximately 1.391 L/s can flow. Dividing the ranges of plant flow rates in the 8 inch HFFV system gives the following:
$$ Number Holes_{Max}=\frac{100L/s}{Q_{1in}}=72$$
$$ Number Holes_{Min}=\frac{25L/s}{Q_{1in}}=18$$
Thus for the 8 inch HFFV systems 1" holes will be used in the slider pipe.

These calculations were made again in the small scale design file with the following parameters given.
* Available head: 1m - 2m
* Flow Rate: 1 L/s
* Pipe Diameter: 2"
The above value for height was used because that was the height of a large capacity bucket found in the lab and flow rate. The team picked 2" piping because that size is commonly available in the lab. Using the above parameters, the team determined the appropriate hole size to be 1/4". These calculations can be found in the design file.

The next step was to determine the spacing and pattern of the holes on the slider pipe. To determine the hole pattern, the team used python to calculate the flow rate through the holes given the amount of head and flow rate available in the lab. The team found that the flow rate through one 1/4" hole given 1m of head is approximately 1/10th of the total flow rate into the float valve. Since the float valve should have full flow when the tee is at the highest level, the team created a pattern that had 10 holes exposed at this level. The team also decided to have 3 rows of holes exposed in the tee at one time to allow for a gradual increase in flow and to also best fit the height of the slider pipe. The team found the spacing between each row by dividing the exposed space within the tee by the number of rows exposed at one time. This way, once one row leaves the tee, a new row enters.

####Rate of Leakage
$$ {Q_{\mathrm{leak}} \over Q_{\mathrm{plant}}} = {{\Delta h \over \Delta t} \over {\mathrm{Height}_{\mathrm{tank}} \over 8 \mathrm{hrs}}}$$
$$ Q_{\mathrm{leak}} = Q_{\mathrm{plant}}{{.03Height_{}\over 8hrs} \over {\mathrm{Height}_{\mathrm{tank}} \over 8 \mathrm{hrs}}}$$
$$Q_{\mathrm{leak}} = 20 L/s*.03 = .6 L/s$$
$$Q_{\mathrm{leak - Small Scale}} = 1 L/s*.03 = .03 L/s$$

The team derived this ratio aiming for the last 3% of the height of the tank to fill up during off-peak hours which has a duration of 8 hours from midnight to 8 am. The amount of time it takes to fill up the whole height of the tank was used in the bottom fraction. Using this ratio, the team deterimed the target $Q_leak$ to be .6 L/s in the full scale design.

####Float size
The team determined the float size by testing the friction force between the slider pipe and tee. First, the team found the sprink constant $k$ by hanging a weight off the spring and measuring the change in length from it's origination orientation.

$$ F=k*\Delta(x) $$
$$k= \frac{F}{\Delta(x)} $$
$$ k =229.8 N/m $$

Then the spring was held in one end of the pipe and pulled, and the change in distance of the spring was measured. Finally, the team measured the friction force by multiplying the $k$ determined in the previous step and the change in distance recorded. The team converted this force to the mass of the float by dividing by the force of gravity.

$$ F=k*\Delta(x)= 229.8N/m * .03313m= 17.67 N $$
$$ \mathrm{Mass}_{\mathrm{Float}}=\frac{F}{9.81 m/s^2} = 1.76 kg$$

The buoyant force has to overcome the friction force in order for the float to move up and down smoothly. The team found the volume of the float by dividing the mass of the float by density of water, then dividing that volume by the cross-sectional area of the desired pipe to get length.

$$\mathrm{Volume}_{\mathrm{Float}}=\frac{\mathrm{Mass}_{\mathrm{Float}}}{\rho_{\mathrm{water}}}=\frac{1.76kg}{1000kg/m^3}=.00176m^3   $$
$$L_{\mathrm{Float}}= \mathrm{Volume}_{\mathrm{Float}}/\mathrm{Area}_{\mathrm{Float}}=\frac{.00176m^3}{3.142 in^2}=35.05$$
From here, the length of 36" was used, because 35" was the bare minimum to overcome the friction force.
###Procedure

The High Flow Float Valve team assembled a 2" float valve in order to test the model's functionality and ease of fabrication. In the future, there will be 3 different size HFFV models, (2 in, 4in, and 8in) each requiring the same fabrication methods, but at larger scales. For now, the team fabricated the smallest scale HFFV, which has a 2" diameter tee and 1.5" diameter slider pipe. The procedure involved the construction of three distinct parts: the slider pipe, the tee, and the float. HFFV only fabricated and tested the small scale design as the original intention of the team was only to test the feasibility of fabricating such a device.

####Slider Pipe


The slider pipe requires a notch at the top of the pipe to fit a float, holes in the active length portion of the pipe (the range of the slider pipe where it can be exposed to the tee) to allow water to pass, and holes for a hose clamp to secure the float and for plugs to constrain the active length. The team started fabrication by cutting a piece of 1.5" diameter pipe to 41cm using the table clamp and the reciprocating saw. This length was calculated using the equation in the section above.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/active%20length.jpg?raw=true"  height = 300></center>

The team then used the bandsaw and the angle alignment tool to produce two cuts in the top of the pipe to form a notch as shown below.  This notch was used to secure the float to the pipe with a hose clamp later. The angles used to cut were 45 degrees. However, it was not necessary that this measurement be extremely precise, because the notch simply serves as a holding space for the float.

<div class="alert alert-block alert-danger">
Avoid "model float valve of smaller dimensions" because it is wordy. "small-scale float valve" works just as well. Even better would be to include what scale the model is. Same idea with the phrase "functionality of it", "the model's functionality" is more streamlined.

Will you also be constructing the full scale model? The sentence referring to "the larger, necessary size" is ambiguous.

-addressed felix

Is 1.5" pvc pipe the conventional way to refer to pvc pipe of diameter 1.5"? If so keep it, if not make it reflect convention. (I don't know myself)

-made everything consistent. not sure about convention still felix

Why 41cm length? Where did you get this number from? Include relevant equations. If no equations were used, say that that is an assumed value. If it is a value that Monroe gave you, ask him how he got it.

Is the "buoy" the float? Be consistent with the names you give to the different parts of your design.
-addressed felix/aly
</div>

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/TopOfSliderPipe.png?raw=true"  height = 300></center>


The team then used a template created from the Fusion design to accurately drill the holes in the slider pipe. The team printed the template and punctured small holes through the centers of each hole on the paper. The team then laid this template around the slider pipe and drew marks on the slider pipe through the small holes to indicate where to drill. The team aligned the template so that the distance from the bottom hole to the top of the plugs was the height necessary according to the equation below:

$$
H_{\mathrm{FirstHole}} = H_{\mathrm{FirstPlug}} + R_{\mathrm{Plug}} + (H_{\mathrm{Tee}} - H_{\mathrm{Bushing}})$$

$$H_{\mathrm{FirstHole}} = {1 \over 2} \mathrm{in} + {1 \over 4} \mathrm {in}+ (5 {11 \over 16} \mathrm{in} - 1\mathrm{in} )$$

$$H_{\mathrm{FirstHole}} = 5 {7 \over 16} \mathrm{in}$$


<div class="alert alert-block alert-danger">
BIG ONE: Where did the template made in Fusion come from? How did you determine the hole pattern? This is a key part of understanding this design. Include equations, development of design. What is that fusion template gets lost in the cloud and the next team has to recreate it?

The second and third sentences are confusing. It takes a few readings to understand that you are puncturing the paper. Make it a little more explicit.

Also does it matter where you lay the template on the slider? Align it from the bottom, the top?

addressed - Aly and Julia (some in design details)
</div>

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/HolePattern2.png?raw=true" height=300></center>

The team then cut holes according to the markings on the pipe using the drill press fitted with a 1/4" drill bit as determined by the calculations in the "Design Details" section.

<div class="alert alert-block alert-danger">
BIG ONE: How big are the holes supposed to be? And how did you get that value? Again root it in the theory and maths.
-find in design section felix
</div>

<div class="alert alert-block alert-danger">
Sometimes there are spaces after the photos before the text and sometimes not. Chose one or the other.
</div>

<center><img src= " https://github.com/AguaClara/float_valve/blob/master/Pictures/Marking%20pipe%20for%20holes.JPG?raw=true" height = 300> <img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Drilling%20holes.JPG?raw=true" height=300></center>


####Tee

\
Next, the team cut each of the PVC bushings to 1" in height using the band saw. These were cut because it made more space available in the tee for exposure to holes.  

<div class="alert alert-block alert-danger">
Consider overlaying your photos with arrows/labels. For example pointing out the bushings in the photo on the left below. (I am not very fabrication driven so I don't know what a bushing is, so incoming freshmen may not know as well. Remember that the audience here is a new member of AguaClara). Great visuals used.
Bushing labeled
</div>

<center><img src="https://raw.githubusercontent.com/AguaClara/float_valve/master/Pictures/bushings_before_cut%20copy.jpg" height=300><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Bushing%20about%20to%20be%20cut.jpg?raw=true"  height = 300> </center>
<center> Bushings are shown on the left with marks drawn on them as a guide for bandsaw cuts.</center>

\
The team then created a handmade sanding tool. This tool was made from an arbitrarily long 1" PVC pipe with a thick piece of sandpaper PVC-glued around its circumference.

<div class="alert alert-block alert-danger">
Reconsider "thick piece of sandpaper PVC-glued to around its circumfrence". Too many words and PVC-glued seems informal.
</div>

 <center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Sander.JPG?raw=true" height=300></center>

\
The team then used this tool, as well as a handheld file, to sand down the inside of the bushings so that the 1.5" pipe could slide easily through.

<div class="alert alert-block alert-danger">
Why is it important that the pipe easily slide through? Is it important to minimize the sliding friction between the parts so that the float floats enough to allow the correct amount of flow? Keep connecting what you're doing to the why of what you're doing. What is driving the design of the float valve in terms of equations and assumptions, and fluids, etc.?

Great photos! This step by step is easy to follow and clear.
</div>

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/SandingPipe.png?raw=true" height=300> <img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/SliderPipeNoHoles.JPG?raw=true" height = 300></center>

<div class="alert alert-block alert-danger">
For the next submission, add in a section about future/anticipated steps. This will give me an opportunity to read through and get a greater understanding. It also allows more of an opportunity to give you feedback on writing style and format.
</div>

####Float
Originally, the team incorrectly calculated the dimensions for a smaller sized float. The friction force that the smaller size float supported was 13.25 N while the measured friction force was 17.67 N. The first set of instructions were kept so that, given a better sanded tee with a smaller friction force, a procedure for fabrication is available.

#####Smaller Float

To create the 1" float, the team cut 1" PVC pipe into 3, 13" pieces using the bandsaw and hackzall and glued a strip of PVC sheet that was cut using the bandsaw to either end of all three pipes, with 1" arbitrary spacing between each pipe. The team used this design because, after calculating the required length of the float had it been just one pipe, it was clear that it would be too long for proper function both in the tank the team is using for testing and in the distribution tank itself. By using three pipes instead of one, the team was able to decrease the overall length of the float by three, which better accommodates the testing tank.

The team originally found that a float of just one 1" diameter pipe would have to be 35.05" long. To get the length for the three-pipe float the team simply divided by three to get an approximate length of 12" and decided to round up to 13" to account for any errors made in finding the required buoyant force. Since a larger float provides the potential for more buoyant force, but will still only provide what is needed, it was not an issue to round up.

The spacing between the pipes was required because the center float pipe was hose clamped to the top of the slider pipe and part of the notch at the top of the slider pipe would block the other two pipes had there not been space between them. In the 2" float spacing between pipes is not required as seen in the pictures.

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/1%20inch%20float%20vs%202%20inch%20float.jpg?raw=true" height=300></center>

#####Correctly sized Float

To create the 2" float, a similar procedure was used to cut them to the same length, requiring the team to cut 2" PVC pipe into 3, 13" pieces using a bandsaw and hackzall. However, because of this, the larger size spacing between the float was not required, because the lip was no longer in the way for the 2" size. For the 2" caps, the team used a 2 1/2" hole saw in the drill press to cut six circular pieces out of PVC sheet. These pieces were glued to both ends of each pipe to seal them for use as floats.

####Final assembly
After putting the float, slider pipe, and tee together, the team completed the experimental setup. Below is a picture of the complete assembly.
<center><img src="https://raw.githubusercontent.com/AguaClara/float_valve/master/Pictures/complete.jpg" height= 300></center>


###Experimental Setup
Our experimental setup consisted of the water flow setup and the slider pipe assembly.

####Materials List
| Part                            | Quantity |       Size        |
|:------------------------------- |:--------:|:-----------------:|
| Flexible Tubing                 |   5 ft   |    1" diameter    |
| Hose clamp                      |    1     |    2" diameter    |
| Barbed PVC Fitting NPT Male End |    1     |    1" diameter    |
| PVC Tee                         |    1     |    1" diameter    |
| PVC Elbow                       |    1     |    1" diameter    |
| PVC Elbow                       |    1     |    2" diameter    |
| PVC Bushing                     |    1     | 2" to 1" diameter |
| PVC Coupling                    |    1     |    2" diameter    |
| PVC Pipe                        |  3" x 3  |    2" diameter    |
| PVC Pipe                        |   4 ft   |    1" diameter    |
| PVC Coupling                    |    1     |    1" diameter    |
| Fernco Fitting                  |    1     |    2" diameter    |
| Clear PVC Pipe                  |   2 ft   |    2" diameter    |


<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/setup2.png?raw=true" height= 300></center>

####Water Flow
In order to check the flow of the water out of the sink, the team had to test the time it took for a flow to fill a bucket. The bucket was marked with the level of 3 liters, so the team found the right position of the faucet knob that would fill up to the 3 liter mark in 3 seconds, hereby ensuring a flow rate of 1L/s.

####Water Route
The team then took a piece of 1" diameter flexible tubing and used a hose clamp to secure it to the faucet. This flexible tubing led to a barbed fitting on a raised platform on the counter of the lab bench. The team did this in order to ensure more head upon entering the distribution tank. At the top of this platform, the team inserted a 1" tee. The team then connected the clear PVC pipe to the free end of this tee. The tee exposed the water to atmospheric pressure to eliminate pressure head, and the clear PVC pipe prevented the water from spilling out. By adjusting the flow rate of the sink and allowing a given amount of water to enter this clear PVC pipe, the team was able to keep the amount of head entering the system constant.

The tee then led into a 1" elbow that diverted the water down into a 3-foot long 1" pipe. The team expanded this 1" pipe by using a 1" diameter to 2" diameter bushing to connect the water path to the apparatus. The team then used a 2" elbow to get the water to flow horizontally into the float valve tee. Between the elbow and the tee were two small pieces of 2" diameter PVC, which were connected by a Fernco fitting. One end was glued into the elbow, while the other was glued into the tee of the float valve. The team used a Fernco fitting so that the float valve would not be permanently attached to the experimental setup and could be removed if needed. The team positioned the float valve roughly in the center of the tank, both vertically and horizontally. It was centered vertically to allow for the largest range of motion of the slider pipe. It was centered horizontally within the tank to ensure that the float did not hit the sides of the tank.
<center><img src="https://raw.githubusercontent.com/AguaClara/float_valve/master/Pictures/constant_head_chamber.png" height= 300></center>
