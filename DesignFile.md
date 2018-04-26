```python
from aide_design.play import*
from aide_design.physchem import*
import math
Q_Plant=20*u.L/u.s
Temp_Plant=20*u.degC
RatioVCOrifice=.62
Nu=viscosity_kinematic(Temp_Plant)
print(Nu)
Max_Num_Holes=10
Q_Per_Hole=Q_Plant/Max_Num_Holes
print(Q_Per_Hole)
#Rows_Per_T_Active_Area= 1 or 2
#Active_Height_Of_T=.13*u.m
#Min/Max_Orifices_Per_Row=
Avail_Head_High_Est=2*u.m
Avail_Head_Low_Est=1*u.m

FS_Diam=8*u.inch
Area_Outlet=((FS_Diam/2)**2)*u.pi/4
#SS_Diam=4*u.inch     SS - Small scale
FS_FV_Diam=6*u.inch
#SS_FV_Diam=3*u.inch     SS- Small Scale
SliderPipeLength=.762*u.m
Slider_Hole_Diam=1*u.inch
Area_Slider_Hole=(((Slider_Hole_Diam/2)**2)*u.pi/4)
print(Area_Slider_Hole.to(u.m**2))
V_Outlet=Q_Plant/((FS_Diam/2)**2)*u.pi/4
print(V_Outlet.to(u.m/u.s))

V_Hole=(Q_Per_Hole/Area_Slider_Hole)
print(V_Hole.to(u.m/u.s))
Reynolds=re_pipe(Q_Per_Hole, Slider_Hole_Diam, Nu)
print(Reynolds)
Range_Slider=1.2*u.m
Z_Top_Hole=1.343*u.m
Z_Bot_Hole=.368*u.m
Range_Slider=1.2*u.m ## needs to be updated
Z_Top_Hole=1.343*u.m ## and here
Z_Bot_Hole=.368*u.m ## same here

def K_Minor_Calc(D1,D2):
  K_L=(1-D1**2/D2**2)**2
  return(K_L)
K_Minor_Calc(8*u.inch,6*u.inch)
  ##From left to right D1->D2,
K_Minor_Inlet=K_Minor_Calc(FS_Diam,FS_FV_Diam)
 ##K minor value for first contraction
print(K_Minor_Inlet)

HL_Inlet=headloss_exp(Q_Plant, FS_FV_Diam, K_Minor_Inlet)
print(HL_Inlet)

HL_Slider_Hole=head_orifice(Slider_Hole_Diam, RatioVCOrifice, Q_Per_Hole)
print(HL_Slider_Hole)


flow_orifice_1= flow_orifice(Slider_Hole_Diam, 1*u.m, RatioVCOrifice)
print(flow_orifice_1*Max_Num_Holes)
flow_orifice_2= flow_orifice(Slider_Hole_Diam, 2*u.m, RatioVCOrifice)
print(flow_orifice_2.to(u.L/u.s))

#Function to solve for slider hole diameter
def Slider_Diam(FlowRate,Headloss_Avail):
  Diameter=((4*FlowRate)/(math.pi*(2*u.gravity*Headloss_Avail)**.5))**.5
  return(Diameter)

# Function to solve for Float length
# def Float_Length(r, fricForce, temp):
  # floatLength = (fricForce/u.gravity)/(density_water(temp) * math.pi * r**2 * (.5))
  # return floatLength.to(u.m)
# Float_Length(.5*u.inch, 17.67*u.N, Temp_Plant)

# Alternate function to solve for float length assuming negligible frictional force
# In this function "S" is used to denote "Slider Pipe" and "F" is used to denote "Float"
#import math
#OD_Slider_Pipe = 1.9 * (u.inch)
#ID_Slider_Pipe = 1.610 * (u.inch)
#OD_Float = 2.375 * (u.inch)
#Length_Slider_Pipe = 16 * (u.inch)
#Assembly_Weight = .5 * (u.kg)
#Density = density_water(20)
#def Float_Length (Total_Weight, dens, OD_F, Length_S, OD_S, ID_S):
  # floatLength = (2)* (4 * Total_Weight - (dens * math.pi)*(Length_S * (OD_S**2 - ID_S**2) + ((.25 * u.inch) * OD_F**2)))/ (OD_F**2 * dens * math.pi)
#  floatLength = ( 8 * Total_Weight / (OD_F**2 * dens * math.pi)) - (2 * Length_S * (OD_S**2 - ID_S**2)/ OD_F**2) - (1/2 * u.inch)
#  return floatLength.to(u.m)
#Float_Length(Assembly_Weight, Density, OD_Float, Length_Slider_Pipe, OD_Slider_Pipe, ID_Slider_Pipe)


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
def Float_Length2(dens_water, dens_pvc, OD_F, ID_F, OD_SP, ID_SP, L_SP, weight_SP,g):
  #Equation given dimensions of slider pipe:
  floatlength_diam = (((((OD_SP)**2-(ID_SP)**2)*L_SP*dens_pvc)*(1-dens_water/dens_pvc))/((ID_F)**2*dens_water-(OD_F)**2*dens_pvc+(ID_F)**2*dens_pvc)).to(u.inch)
  #equation given weight of slider pipe:
  floatlength_weight= ((4*weight_SP*(1-dens_water/dens_pvc))/(math.pi*g*((ID_F)**2*dens_water-(OD_F)**2*dens_pvc+(ID_F)**2*dens_pvc))).to(u.inch)
  return(floatlength_diam, floatlength_weight)
Float_Length2(Density_Water, Density_PVC, OD_Float, ID_Float, OD_Slider_Pipe, ID_Slider_Pipe, Length_Slider_Pipe, Weight_Slider_Pipe, grav)



  ##The the float was designed in relation to the frictional force so that when the float is in the plant, it will sit half submerged in the water.
```python
from aide_design.play import*
from aide_design.physchem import*
import math
def HFFV(FlowRate,Head): ##Given flowrate and head this will tell you the parameters to use for your HFFV system but doesn't include float size and slider pipe length.
  if (FlowRate>=(1*u.L/u.s)) and (FlowRate<=(6*u.L/u.s)):
    Slider_Pipe_Diam=1.5*u.inch
    Tee_Diam=2*u.inch
    Hole_Diam=.25*u.inch
    Flow_orifice= flow_orifice(Hole_Diam, Head, RatioVCOrifice)
    Number_Holes=round((FlowRate/Flow_orifice.to(u.L/u.s)),1)
    print('Slider pipe diameter is '+str(Slider_Pipe_Diam))
    print('Tee diameter is ' +str(Tee_Diam))
    print('Hole Diameter is ' +str(Hole_Diam))
    print('Max number of holes required is '+str(Number_Holes))

  elif (FlowRate>=(6*u.L/u.s)) and (FlowRate<=(25*u.L/u.s)):
    Slider_Pipe_Diam=3*u.inch
    Tee_Diam=4*u.inch
    Hole_Diam=.5*u.inch
    Flow_orifice= flow_orifice(Hole_Diam, Head, RatioVCOrifice)
    Number_Holes=round((FlowRate/Flow_orifice.to(u.L/u.s)),1)
    print('Slider pipe diameter is '+str(Slider_Pipe_Diam))
    print('Tee diameter is ' +str(Tee_Diam))
    print('Hole Diameter is ' +str(Hole_Diam))
    print('Max number of holes required is '+str(Number_Holes))
  elif (FlowRate>=(25*u.L/u.s)) and (FlowRate<=(100*u.L/u.s)):
    Slider_Pipe_Diam=6*u.inch
    Tee_Diam=8*u.inch
    Hole_Diam=1*u.inch
    Flow_orifice= flow_orifice(Hole_Diam, Head, RatioVCOrifice)
    Number_Holes=round((FlowRate/Flow_orifice.to(u.L/u.s)),1)
    print('Slider pipe diameter is '+str(Slider_Pipe_Diam))
    print('Tee diameter is ' +str(Tee_Diam))
    print('Hole Diameter is ' +str(Hole_Diam))
    print('Max number of holes required is '+str(Number_Holes))

  return

def Slider_Pipe_Length(Height_Distribution_Tank,Plug_Diam,Slider_Pipe_Diam,Tee_Diam):
  Tee_Height=Tee_Length(Tee_Diam)
  Bot_Extra_Material=Plug_Diam/2+.5*u.inch ##Standard plug diam is half inch diameter
  Top_Extra_Material=Float_Diameter*(1+2**(.5))+Plug_Diam/2+.5*u.inch
  Active_Length=(Height_Distribution_Tank-Bot_Extra_Material-Top_Extra_Material-Tee_Height/2)+Tee_Height
  SP_Length=Active_Length+Top_Extra_Material+Bot_Extra_Material+Slider_Pipe_Diam/2
  print('Slider pipe length is '+str(Slider_Pipe_Length))

def Tee_Length(Tee_Diam):
  if Tee_Diam==2*u.inch:
    Length=5.25*u.inch
    return(Length)
  elif Tee_Diam==4*u.inch:
    Length=8.675*u.inch
    Return(Length)
  elif Tee_Diam==8*u.inch:
    Length=18*u.inch    
    Return(Length)
Tee_Length(2*u.inch)

```
