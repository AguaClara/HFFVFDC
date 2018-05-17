```python
from aide_design.play import*
from aide_design.physchem import*
import math
Q_Plant=20*u.L/u.s
Temp_Plant=20*u.degC
RatioVCOrifice=.62
Nu=viscosity_kinematic(Temp_Plant)

def Area_Leak(Q_Leak,Vena_Contracta,Head):
  Area=Q_Leak/(Vena_Contracta*(2*u.gravity*Head)**.5)
  return(Area.to(u.m**2))

Area=Area_Leak(.06*u.L/u.s,RatioVCOrifice,1.05*u.m)/2
print(Area)
OD_Slider_Pipe=1.9*u.inch
ID_Bushing=(OD_Slider_Pipe**2+(4*Area/np.pi))**.5
def Slider_Pipe_Leak_Width(ID_Bushing,OD_Slider_Pipe):
  Leak_Spacing=(ID_Bushing-OD_Slider_Pipe)/2
  return(Leak_Spacing)
Slider_Pipe_Leak_Width(ID_Bushing,OD_Slider_Pipe).to(u.cm)
def Q_Leak(Head,Vena_Contracta,Area_Gap):
  Q=2*((2*u.gravity*Head)**.5)*Vena_Contracta*Area_Gap
  return(Q.to(u.L/u.s))
Leak_Total=(Q_Leak(1.05*u.m,RatioVCOrifice,Area)).to(u.L/u.hr)
print(Leak_Total*8*u.hr)


# Function to solve for float length assuming negligible friction between slider pipe and tee. Contains equations to solve using the inner and outer diameters of the slider pipe or the weight of the slider pipe.
import math
OD_Slider_Pipe = 1.9 * (u.inch)
ID_Slider_Pipe = 1.610 * (u.inch)
OD_Float = 1.9 * (u.inch)
ID_Float = 1.610 * (u.inch)
Length_Slider_Pipe = 16 * (u.inch)
Density_Water = density_water(20* u.degC).to(u.kg/u.inch**3)
Density_PVC= 0.0226 * (u.kg/u.inch**3)
Weight_Slider_Pipe= 3.758 * (u.N)
grav= 9.81 * (u.m/u.s**2)

# Function gives required minimum length of float based on the outer and inner diameters and the length of the slider pipe
def Float_Length_dim(dens_water, dens_pvc, OD_F, ID_F, OD_SP, ID_SP, L_SP, g):
  #Equation given dimensions of slider pipe:
  floatlength_dim = (((((OD_SP)**2-(ID_SP)**2)*L_SP*dens_pvc)*(1-dens_water/dens_pvc))/((ID_F)**2*dens_water-(OD_F)**2*dens_pvc+(ID_F)**2*dens_pvc)).to(u.inch)
  print('The minimum required float length based on slider pipe dimensions is ' +str(floatlength_dim))
  return
Float_Length_dim(Density_Water, Density_PVC, OD_Float, ID_Float, OD_Slider_Pipe, ID_Slider_Pipe, Length_Slider_Pipe, grav)

# Function gives required minimum length of float based on the weight of the slider pipe
def Float_Length_Weight(dens_water, dens_pvc, OD_F, ID_F, weight_SP,g):
  #equation given weight of slider pipe:
  floatlength_weight= ((4*weight_SP*(1-dens_water/dens_pvc))/(math.pi*g*((ID_F)**2*dens_water-(OD_F)**2*dens_pvc+(ID_F)**2*dens_pvc))).to(u.inch)
  print('The minimum required float length based on slider pipe length is ' +str(floatlength_weight))
  return
Float_Length_Weight(Density_Water, Density_PVC, OD_Float, ID_Float, Weight_Slider_Pipe, grav)


##Active Length function that returns the active length to be used in the following two functions
def Active_Length(Height_Distribution_Tank,Slider_Pipe_Diam):
  Plug_Diam=.5*u.inch ##Standard plug diam is half inch diameter
  Bot_Extra_Material=Plug_Diam/2+.5*u.inch
  Top_Extra_Material=Slider_Pipe_Diam*(1+2**(.5))+Plug_Diam/2+.5*u.inch
  Bushing_Height = 1*u.inch
  Act_Length=((Height_Distribution_Tank - Bot_Extra_Material - Top_Extra_Material - 2*Bushing_Height)*(1/3)).to(u.inch)
  return (Act_Length)
Active_Length(2*u.m, 1.5*u.inch)
Active_Length(2.5*u.m, 6*u.inch)


##Calculates the necessary length of the slider pipe
def Slider_Pipe_Length(Active_Length, Slider_Pipe_Diam):
  Plug_Diam=.5*u.inch ##Standard plug diam is half inch diameter
  Bot_Extra_Material=Plug_Diam/2+.5*u.inch
  Top_Extra_Material=(Slider_Pipe_Diam*(1+2**(.5)))/2+Plug_Diam/2+.5*u.inch
  Bushing_Height = 1*u.inch
  SP_Length = (Active_Length*(2) +Top_Extra_Material+Bot_Extra_Material + 2*Bushing_Height - (Slider_Pipe_Diam*2**(.5))/2).to(u.inch)
  return (SP_Length)
Slider_Pipe_Length(Active_Length(2*u.m, 1.5*u.inch), 1.5*u.inch)

##Calculates the pipe between tee and bushings
def Pipe_Tee_To_Bushing_Length(Height_Distribution_Tank,Slider_Pipe_Diam):
  if Slider_Pipe_Diam == 1.5*u.inch:
    Height_Tee=5.25*u.inch
    Height_Coupling=(2+27/32)*u.inch
    Height_Coupling_In=1.375*u.inch

  if Slider_Pipe_Diam == 3*u.inch:
    Height_Tee=8.675*u.inch
    Height_Coupling=(4+(7/32))*u.inch
    Height_Coupling_In=1.5*u.inch

  if Slider_Pipe_Diam == 6*u.inch:
    Height_Tee=18*u.inch
    Height_Coupling=7.5*u.inch ##guess
    Height_Coupling_In=1.5*u.inch

  Height_Lip=1/8*u.inch
  Height_Active=Active_Length(Height_Distribution_Tank,Slider_Pipe_Diam)
  H_Bushing=1*u.inch
  Length=(Height_Tee+2*Height_Coupling-2*Height_Coupling_In+2*Height_Lip-H_Active-2*H_Bushing)/2
  return(Length)



##Calculates the total height of the tee
def Total_Tee_Height(Active_Length):
  Bushing_Height = 1*u.inch
  Tee_Height= (Active_Length + 2 * Bushing_Height).to(u.inch)
  return (Tee_Height)
Total_Tee_Height(Active_Length(2.5*u.m, 6*u.inch))


def Tee_Length(Tee_Diam):
  if Tee_Diam==2*u.inch:
    Length=5.25*u.inch
    return(Length)
  elif Tee_Diam==4*u.inch:
    Length=8.675*u.inch
    return(Length)
  elif Tee_Diam==8*u.inch:
    Length=18*u.inch    
    return(Length)
  Tee_Length(2*u.inch)
  Slider_Pipe_Length(1*u.m,1.5*u.inch,2*u.inch)
  HFFV(25*u.L/u.s,1*u.m,1*u.m)


#I designed a hole pattern dependent on the ratio of the hole size to the active length. The idea is that there will be a row in an interval of the Hole_Diam*4. I kept the old code in case we want to scrap this. - julia
def Hole_Pattern_Small_Scale (FlowRate,Head,Height_Distribution_Tank,Slider_Pipe_Diam):
    if (FlowRate>=(1*u.L/u.s)) and (FlowRate<=(6*u.L/u.s)):
      Hole_Diam=.25*u.inch
    elif (FlowRate>=(6*u.L/u.s)) and (FlowRate<=(25*u.L/u.s)):
      Hole_Diam=.5*u.inch
    elif (FlowRate>=(25*u.L/u.s)) and (FlowRate<=(100*u.L/u.s)):
      Hole_Diam=1*u.inch
    Flow=flow_orifice(Hole_Diam, Head, .62)
    Num_Of_Holes_Exposed = int(round((FlowRate/Flow.to(u.L/u.s)),0))
    Num_Of_Rows_Exposed = int(math.floor(Active_Length(Height_Distribution_Tank,Slider_Pipe_Diam)/(Hole_Diam * 4)))
    Num_Per_Row = math.floor(Num_Of_Holes_Exposed / Num_Of_Rows_Exposed)
    if (Num_Per_Row > 0):
      Row_Spacing = Hole_Diam*4
      Remainder_Holes = Num_Of_Holes_Exposed % Num_Of_Rows_Exposed
      Pattern_Array = [Num_Per_Row for i in range (Num_Of_Rows_Exposed)]
      for x in range (0, Remainder_Holes):
        Pattern_Array[x] = Pattern_Array[x] + 1
    else:
      Row_Spacing = (Active_Length(Height_Distribution_Tank,Slider_Pipe_Diam)/Num_Of_Holes_Exposed).to(u.inch)
      Pattern_Array = [1 for i in range (Num_Of_Holes_Exposed)]
    print ('The hole pattern is ' + str(Pattern_Array))
    print ('The space between rows is ' + str(Row_Spacing))
    return
Hole_Pattern_Small_Scale(1*u.L/u.s,1*u.m, 2*u.m, 1.5*u.inch)


  ##The the float was designed in relation to the frictional force so that when the float is in the plant, it will sit half submerged in the water.
```python
from aide_design.play import*
from aide_design.physchem import*
import math
def HFFV(FlowRate,Head,Height_Distribution_Tank): ##Given flowrate, head, and height of distribution tank this will tell you the parameters to use for your HFFV system but doesn't include float size and slider pipe length.
  RatioVCOrifice=.62
  if (FlowRate>=(1*u.L/u.s)) and (FlowRate<=(6*u.L/u.s)):
    Slider_Pipe_Diam=1.5*u.inch
    Tee_Diam=2*u.inch
    Hole_Diam=.25*u.inch

  elif (FlowRate>=(6*u.L/u.s)) and (FlowRate<=(25*u.L/u.s)):
    Slider_Pipe_Diam=3*u.inch
    Tee_Diam=4*u.inch
    Hole_Diam=.5*u.inch

  elif (FlowRate>=(25*u.L/u.s)) and (FlowRate<=(100*u.L/u.s)):
    Slider_Pipe_Diam=6*u.inch
    Tee_Diam=8*u.inch
    Hole_Diam=1*u.inch

  Flow_orifice= flow_orifice(Hole_Diam, Head, RatioVCOrifice)
  Number_Holes=math.floor(FlowRate/Flow_orifice.to(u.L/u.s))
  SP_Length=Slider_Pipe_Length(Active_Length(Height_Distribution_Tank,Slider_Pipe_Diam), Slider_Pipe_Diam)
  print('Slider pipe diameter is '+str(Slider_Pipe_Diam))
  print('Slider pipe length is '+str(SP_Length))
  print('Tee diameter is ' +str(Tee_Diam))
  print ('The total tee height is ' + str(Total_Tee_Height(Active_Length(Height_Distribution_Tank,Slider_Pipe_Diam))))
  print('Hole Diameter is ' +str(Hole_Diam))
  print('Number of holes required is ' +str(Number_Holes))
  Hole_Pattern_Small_Scale(FlowRate,Head,Height_Distribution_Tank,Slider_Pipe_Diam)


  return

One_Liter=HFFV(1*u.L/u.s,1*u.m,1.5*u.m)

```
