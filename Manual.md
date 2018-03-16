circumference#**High Flow Float Valve**
###Alycia Storch, Julia Timko, Felix Yang

<div class="alert alert-block alert-danger">
Please do not delete my comments from the report. Just address them and next time I will check that you have fixed these things. If you disagree with any of them, add your own comment with your reasoning below it. (Or if they are distracting, then save a copy of this and label it as your first draft and remind me that you did that when you submit next).
</div>

## Manual
###Introduction
The high flow float valve will control the flow rate of water into the distribution tank. The distribution tank is the storage tank for clean water exiting the treatment plant before it is distributed to the community, and overflows when the tank is full. Overflow happens mainly during off-peak hours from midnight to dawn when demand is low. Avoiding overflow is desirable because the excess treated drinking water is wasted. To avoid the tank overflowing , the float valve will decrease the flow rate as the tank fills up.

The float valve consists of a slider pipe, a tee connected to the distribution tank inlet pipe, a float on top of the slider pipe, and bushings inside the tee that the slider pipe will slide through. The slider pipe has an increasing number of holes from bottom to top. The water entering the distribution tank will go through the tee and through the hole in the slider pipe that are within the tee. The more holes exposed, the higher the flow rate. As the tank fills up, the float will cause the slider pipe to rise, which will decrease the number of holes exposed within the tee. When the tank is full, no holes will be exposed within the tee and the flow will stop.

<div class="alert alert-block alert-danger">

In the first sectence, consider lower case "high flow float valve" as it is not a proper noun here. Also consider "The high flow float valve will control" rather than "serve to control." Also what is the "distribution tank," and when does it overflow? Distribution tank to me means the final tank after the full treatment train, but before going out to the community. Explanation in the final three sentences is very good. Not enough connection as to why is it bad is the distribution tank overflows.

addresed - felix

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

All parts were bought from McMaster Carr
###Tools needed
* bandsaw
* Hackzall
* Drill Press or Cordless Drill
* Measuring tools like measuring tape and Calipers
* PVC Primer
* PVC glue
* sandpaper

<div class="alert alert-block alert-danger">
Please include source (i.e. McMaster Carr) and the approximate unit price in the table. Consider adding a table of tools needed for fabrication as described in your procedure. (Include the sandpaper, saws, extra PVC for sanding tool etc.)

addressed - Aly
</div>

###Design Details
####Slider Pipe Hole Size and Pattern
The team was constrained by a couple of parameters including available head, height of the distribution tank, flow rate, and pipe diameter of the pipe running into the distribution tank. The number of exposed holes was set to be 10 holes for maximum flow and 0 holes for minimum flow. And the goal was to solve for slider pipe hole diameter given the following parameters of the plant in Honduras.

* Available Head - 1m - 2m
* Height of distribution tank - 1.83 m or 6 ft
* Flow rate - 20 L/s
* Pipe Diameter - 8 inch

The goal was to use a diameter that would give us about 2 L/s or 1/10th of the flow rate of the plant: The flow_orifice equation was used by finding the amount of flow coming out of each hole.

$$ Q=\pi*A*\sqrt{2gh}
$$
Where pi is the vena contract coefficient, A is the slider hole area that is being considered and h was the amount of head available. The hole sizing that was closest to the target flow rate per hole was 1" inch. These calculations were made again in the small scale design file with the following parameters given
* Available head = 1m - 2m
* Height of distribution tank - 70 cm
* Flow Rate = 1 L/s
* Pipe Diameter - 2 inch
The above value for height was used because that was the height of a large capacity bucket found in the lab and flow rate. Pipe diameter was determined to be 2 inch because that size piping is very available in the lab. Using the above parameters hole size was determined to be 1/4" inch.

The next step was to determine the spacing and pattern of the holes on the slider pipe. To determine the hole pattern, the team used python to calculate the flow rate through the holes given the amount of head and flow rate available in the lab. The team found that the flow rate through one 1/4" hole is approximately 1/10th of the total flow rate into the float valve. Since the float valve should have full flow when the tee is at the highest level, the team created a pattern that had 10 holes exposed at this level. The team also decided to have 3 rows of holes exposed in the tee at one time to allow for a gradual increase in flow and to also best fit the height of the slider pipe. The spacing between each row was found by dividing the length that would be exposed in the tee by the number of rows exposed at one time. This way, once one row leaves the tee, a new row enters.

###Procedure

The High Flow Float Valve team is planning to assemble a small-scale float valve in order to test the model's functionality before switching to the larger, realistic size. The full scale size will have an 8" diameter inlet pipe and tee and a 6" diameter slider pipe. For now, the team is just fabricating a small-scale model which is 1/4th in scale and has a 2" diameter tee and 1.5" diameter slider pipe. The procedure involved the construction of three distinct parts: the slider pipe, the tee, and the float. HFFV will only be fabricating and testing the small scale design as the original intention of the team was only to test the feasibility of fabricating such a device.

####Slider Pipe


To form the slider pipe, the team started by cutting a piece of 1.5" diameter pipe to 41cm using the table clamp and the reciprocating saw. This length was calculated by the following equation, allotting an extra 3.5cm as an arbitrary buffer to allow space for additions at the top of the pipe:

$$ L_{\mathrm{Pipe}} = {1 \over 2} \times H_{\mathrm{DistributionTank}} + 3.5\mathrm{cm} $$

$$ L_{\mathrm{Pipe}} = {1 \over 2} (75\mathrm{cm}) + 3.5\mathrm{cm} = 41.0 \mathrm{cm}  $$

The team then used the bandsaw and the angle alignment tool to produce two cuts in the top of the pipe to form a notch as shown below.  This notch will be used to secure the float to the pipe with a hose clamp later. The angles used cut were close to 45 degrees. However, it was not necessary that this measurement be extremely precise, because the notch simply serves as a holding space for the float.

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

The team then a cut holes according to the markings on the pipe using the drill press fitted with a 1/4 in drill bit as determined by the caluclations in the "Design Details" section.

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
Next, the team cut each of the PVC bushings to 1" in height using the band saw.

<div class="alert alert-block alert-danger">
Consider overlaying your photos with arrows/labels. For example pointing out the bushings in the photo on the left below. (I am not very fabrication driven so I don't know what a bushing is, so incoming freshmen may not know as well. Remember that the audience here is a new member of AguaClara). Great visuals used.
</div>

<center><img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Bushings%20with%20marked%20cuts.jpg?raw=true" height=300> <img src="https://github.com/AguaClara/float_valve/blob/master/Pictures/Bushing%20about%20to%20be%20cut.jpg?raw=true"  height = 300></center>

\
The team then created a handmade sanding tool. This tool was made from an arbitrarily long 1" PVC pipe with a thick piece of sandpaper PVC-glued to around its circumference.

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


###Special Components
If your subteam uses a particular part that is unique and you could foresee a future subteam needing to order it or learn more about it, please include basic information like the vendor where it was purchased, catalog/item number, and a link to any documentation.
